---
title: Omstrukturera en Team Foundation Server-distribution till Azure DevOps Services i Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Läs om hur Contoso omstrukturerar sin lokala Team Foundation Server-distribution genom att migrera den till Azure DevOps Services i Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/11/2018
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
services: site-recovery
ms.openlocfilehash: fc992a4c00a1acd99481d6090563ecef38c5fedb
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/06/2019
ms.locfileid: "70832314"
---
# <a name="refactor-a-team-foundation-server-deployment-to-azure-devops-services"></a>Omstrukturera en Team Foundation Server-distribution till Azure DevOps Services

Denna artikel beskriver hur det fiktiva företaget Contoso omstrukturerar sin lokala Team Foundation Server-distribution genom att migrera den till Azure DevOps Services i Azure. Contosos utvecklingsteam har använt TFS för gruppsamarbete och källkontroll under de senaste fem åren. De vill nu flytta till en molnbaserad lösning för utveckling och testning samt för källkontroll. Azure DevOps Services kommer att ha betydelse när de flyttar till en Azure DevOps-modell och utvecklar nya molnspecifika tjänster.

## <a name="business-drivers"></a>Affärsdrivande faktorer

IT-ledningsgruppen har arbetat tillsammans med affärspartner för att identifiera framtida mål. Partners är inte alltför bekymrade över nya utvecklingsverktyg och tekniker, men har fångat upp följande punkter:

- **Programvara:** Oavsett huvudverksamhet så är alla företag nu programvaruföretag, inklusive Contoso. Företagsledningen är intresserad av hur IT kan hjälpa företaget med nya arbetsmetoder för användare och upplevelser för sina kunder.
- **Effektivitet:** Contoso måste effektivisera processer och ta bort onödiga procedurer för utvecklare och användare. Detta kommer att ge företaget möjlighet att effektivare uppfylla kundernas krav. Verksamheten behöver att IT-avdelningen agerar snabbt, utan att slösa tid eller pengar.
- **Smidighet:** Contoso IT behöver uppfylla verksamhetskraven och reagera snabbare än marknaden för att uppnå framgång i en global ekonomi. It får inte vara ett hinder för verksamheten.

## <a name="migration-goals"></a>Migreringsmål

Contosos molnteam har fastställt mål för migreringen till Azure DevOps Services:

- Teamet behöver ett verktyg för att migrera data till molnet. Det ska behövas få manuella processer.
- Arbetsobjekt och historik för det senaste året måste migreras.
- De vill inte behöva skapa nya användarnamn och lösenord. Alla aktuella systemtilldelningar måste bibehållas.
- De vill gå från versionskontroll med Team Foundation (TFVC) till Git.
- Övergången till Git kommer bara att beröra den senaste versionen av källkoden. Det kommer att ske under stilleståndstid när allt arbete kommer att stoppas under övergången. De förstår att endast den aktuella huvudgrenens historik kommer att vara tillgänglig efter flytten.
- De är bekymrade över ändringen och vill testa den innan de flyttar allt. De vill ha kvar tillgång till TFS även efter övergången till Azure DevOps Services.
- De har flera samlingar och vill börja med en som bara har några få projekt för att bättre förstå processen.
- De förstår att TFS-samlingar har ett ”ett till ett”-förhållande med Azure DevOps Services organisationer så de kommer att ha flera URL:er. Detta överensstämmer dock med deras aktuella separationsmodell för kodbas och projekt.

## <a name="proposed-architecture"></a>Föreslagen arkitektur

- Contoso kommer att flytta sina TFS-projekt till molnet och inte längre ha projekt eller källkontroll lokalt.
- TFS kommer att migreras till Azure DevOps Services.
- Contoso har idag en TFS-samling med namnet `ContosoDev` som kommer att migreras till en Azure DevOps Services-organisation som heter `contosodevmigration.visualstudio.com`.
- Projekt, arbetsobjekt, fel och itereringar från det senaste året kommer att migreras till Azure DevOps Services.
- Contoso kommer att använda Azure Active Directory, som de konfigurerade när de [införde sin Azure-infrastruktur](contoso-migration-infrastructure.md) i början av sin migreringsplanering.

![Scenariots arkitektur](./media/contoso-migration-tfs-vsts/architecture.png)

## <a name="migration-process"></a>Migreringsprocess

Så här genomför Contoso migreringen:

1. Många förberedelser måste göras. Som ett första steg måste Contoso uppgradera sin TFS-implementering till en nivå som stöds. Contoso kör TFS 2017 uppdatering 3, men för att kunna använda databasmigrering måste de köra en 2018-version som stöds och de senaste uppdateringarna.
2. Efter uppgradering kör Contoso TFS-migreringsverktyget för att validera sin samling.
3. Contoso bygger en uppsättning förberedelsefiler och utför en testmigrering.
4. Contoso kör sedan en full migrering som inkluderar arbetsobjekt, fel, sprintar och kod.
5. Efter migreringen flyttar Contoso sin kod från TFVC till Git.

![Migreringsprocessen](./media/contoso-migration-tfs-vsts/migration-process.png)

## <a name="prerequisites"></a>Förutsättningar

Det här behöver Contoso för att köra detta scenario.

<!-- markdownlint-disable MD033 -->

**Krav** | **Detaljer**
--- | ---
**Azure-prenumeration** | Contoso skapade prenumerationer i en tidigare artikel i den här serien. Om du inte har någon Azure-prenumeration kan du skapa ett [kostnadsfritt konto](https://azure.microsoft.com/pricing/free-trial).<br/><br/> Om du skapar ett kostnadsfritt konto är du administratör för din prenumeration och kan utföra alla åtgärder.<br/><br/> Om du använder en befintlig prenumeration och inte är administratör måste du be administratören att ge dig ägar- eller deltagarbehörighet.<br/><br/> Om du behöver mer detaljerade behörigheter läser du [den här artikeln](/azure/site-recovery/site-recovery-role-based-linked-access-control).
**Azure-infrastruktur** | Contoso konfigurerar Azure-infrastrukturen enligt beskrivningen i [Azure-infrastruktur för migrering.](contoso-migration-infrastructure.md)
**Lokal TFS-server** | Den lokala servern måste köra TFS 2018 uppgradering 2 eller uppdateras till detta som en del av denna process.

## <a name="scenario-steps"></a>Scenariosteg

Så här slutför Contoso migreringen:

> [!div class="checklist"]
>
> - **Steg 1: Skapa ett Azure storage-konto.** Detta lagringskonto kommer att användas under migreringsprocessen.
> - **Steg 2: Uppgradera TFS.** Contoso kommer att uppgradera sin version till TFS 2018 uppgradering 2.
> - **Steg 3: Validera samlingen.** Contoso kommer att validera TFS-samlingen för att förbereda migreringen.
> - **Steg 4: Skapa förberedelsefil.** Contoso kommer att skapa migreringsfilerna med TFS migreringsverktyg.

## <a name="step-1-create-a-storage-account"></a>Steg 1: skapar ett lagringskonto

1. I Azure-portalen skapar Contosos administratörer ett lagringskonto (**contosodevmigration**).
2. De placerar kontot i den sekundära region de använder för redundans – USA, centrala. De använder ett allmänt standardkonto med lokalt redundant lagring.

    ![Lagringskonto](./media/contoso-migration-tfs-vsts/storage1.png)

**Behöver du mer hjälp?**

- [Introduktion till Azure Storage](/azure/storage/common/storage-introduction).
- [Skapa ett lagringskonto](/azure/storage/common/storage-create-storage-account).

## <a name="step-2-upgrade-tfs"></a>Steg 2: Uppgradera TFS

Contosos administratörer uppgraderar TFS-servern till TFS 2018 uppdatering 2. Innan de börjar:

- De laddar ned [TFS 2018 uppdatering 2](https://visualstudio.microsoft.com/downloads)
- De kontrollerar [maskinvarukraven](/tfs/server/requirements) och läser igenom [viktig information](/visualstudio/releasenotes/tfs2018-relnotes) och [potentiella uppgraderingsproblem](/tfs/server/upgrade/get-started#before-you-upgrade-to-tfs-2018).

De uppgraderar så här:

1. De börjar med att säkerhetskopiera TFS-servern (som körs på en virtuell dator med VMware) och tar en VMware-ögonblicksbild.

    ![TFS](./media/contoso-migration-tfs-vsts/upgrade1.png)

2. TFS-installationsprogrammet startar och de väljer lokal installation. Installationsprogrammet behöver Internetåtkomst.

    ![TFS](./media/contoso-migration-tfs-vsts/upgrade2.png)

3. När installationen är klar startar guiden för serverkonfiguration.

    ![TFS](./media/contoso-migration-tfs-vsts/upgrade3.png)

4. Efter verifiering slutför guiden uppgraderingen.

     ![TFS](./media/contoso-migration-tfs-vsts/upgrade4.png)

5. De verifierar TFS-installationen genom att granska projekts, arbetsobjekt och kod.

     ![TFS](./media/contoso-migration-tfs-vsts/upgrade5.png)

> [!NOTE]
> Vissa TFS-uppgraderingar behöver köra konfigurationsguiden efter uppgraderingen. [Läs mer](/azure/devops/reference/configure-features-after-upgrade?utm_source=ms&utm_medium=guide&utm_campaign=vstsdataimportguide&view=vsts).

**Behöver du mer hjälp?**

Lär dig om [uppgradering av TFS](/tfs/server/upgrade/get-started).

## <a name="step-3-validate-the-tfs-collection"></a>Steg 3: Validera TFS-samlingen

Contosos administratörer kör TFS-migreringsverktyget mot ContosoDev-samlingens databas för att validera den innan migreringen.

1. De laddar ned och packar upp [TFS-migreringsverktyget](https://www.microsoft.com/download/details.aspx?id=54274). Det är viktigt att ladda ned versionen för den TFS-uppdatering som körs. Versionen kan kontrolleras i administratörskonsolen.

    ![TFS](./media/contoso-migration-tfs-vsts/collection1.png)

2. De kör verktyget för att validera sina data genom att ange URL:en för projektsamlingen:

        `TfsMigrator validate /collection:http://contosotfs:8080/tfs/ContosoDev`

3. Verktyget visar ett fel.

    ![TFS](./media/contoso-migration-tfs-vsts/collection2.png)

4. De letar upp loggfilerna i mappen `Logs`, precis innan verktygets plats. En loggfil skapas för varje större validering. `TfsMigration.log` har huvudinformationen.

    ![TFS](./media/contoso-migration-tfs-vsts/collection3.png)

5. De hittar denna post som är relaterad till identitet.

    ![TFS](./media/contoso-migration-tfs-vsts/collection4.png)

6. De kör `TfsMigrator validate /help` på kommandoraden och ser att kommandot `/tenantDomainName` verkar behövas för att validera identiteter.

     ![TFS](./media/contoso-migration-tfs-vsts/collection5.png)

7. De kör valideringskommandot igen och inkluderar detta värde, tillsammans med sitt Azure AD-namn: `TfsMigrator validate /collection: http://contosotfs:8080/tfs/ContosoDev /tenantDomainName:contosomigration.onmicrosoft.com`.

    ![TFS](./media/contoso-migration-tfs-vsts/collection7.png)

8. Skärmen för inloggning till Azure AD visas och de anger autentiseringsuppgifterna för en global administratör.

     ![TFS](./media/contoso-migration-tfs-vsts/collection8.png)

9. Valideringen godkänns och bekräftas av verktyget.

    ![TFS](./media/contoso-migration-tfs-vsts/collection9.png)

## <a name="step-4-create-the-migration-files"></a>Steg 4: Skapa migreringsfilerna

Nu när valideringen är slutförd kan Contosos administratörer använda TFS-migreringsverktyget för att skapa migreringsfilerna.

1. De kör förberedelsesteget i verktyget.

    `TfsMigrator prepare /collection:http://contosotfs:8080/tfs/ContosoDev /tenantDomainName:contosomigration.onmicrosoft.com /accountRegion:cus`

     ![Förbered](./media/contoso-migration-tfs-vsts/prep1.png)

    Förbereda gör följande:
    - Söker igenom samlingen för att hitta en lista på alla användare och fyller i identitetsloggen (**IdentityMapLog.csv**).
    - Förbereder anslutningen till Azure Active Directory för att hitta en post för varje identitet.
    - Contoso har redan infört Azure AD och synkroniserat det med Azure AD Connect, så förbereda bör kunna hitta överensstämmande identiteter och markera dem som aktiva.

2. Skärmen för inloggning till Azure AD visas och de anger autentiseringsuppgifterna för en global administratör.

    ![Förbered](./media/contoso-migration-tfs-vsts/prep2.png)

3. Förbereda slutförs och verktyget rapporterar att importfilerna skapats korrekt.

    ![Förbered](./media/contoso-migration-tfs-vsts/prep3.png)

4. De kan nu se att både filerna IdentityMapLog.csv och import.json skapats i en ny mapp.

    ![Förbered](./media/contoso-migration-tfs-vsts/prep4.png)

5. Filen import.json innehåller importinställningar. Den innehåller information som önskat organisationsnamn och information om lagringskonto. De flesta fälten fylls i automatiskt. Vissa fält måste fyllas i av användaren. Contoso öppnar filen och lägger till organisationsnamnet som ska skapas för Azure DevOps Services: **contosodevmigration**. Med detta namn kommer deras URL för Azure DevOps Services att vara **contosodevmigration.visualstudio.com**.

    ![Förbered](./media/contoso-migration-tfs-vsts/prep5.png)

    > [!NOTE]
    > Organisationen måste skapas innan migreringen men kan ändras efter migreringen.

6. De granskar identitetsloggfilen som visar de konton som kommer att överföras till Azure DevOps Services under import.

    - Aktiva identiteter innebär identiteter som kommer att bli användare i Azure DevOps Services efter import.
    - I Azure DevOps Services kommer dessa identiteter att vara licensierade och visas som en användare i organisationen efter migrering.
    - Dessa identiteter är markerade som **Aktiv** i kolumnen **Förväntad importstatus** i filen.

    ![Förbered](./media/contoso-migration-tfs-vsts/prep6.png)

## <a name="step-5-migrate-to-azure-devops-services"></a>Steg 5: Migrera till Azure DevOps Services

När förberedelserna är klara kan Contosos administratörer fokusera på migreringen. Efter migreringen kommer de att byta från TFVC till Git för versionskontroll.

Innan de startar planerar administratörerna in stilleståndstid med utvecklingsteamet för att kunna ta samlingen offline för migrering. Detta är stegen för migreringen:

1. **Koppla från samlingen.** Identitetsdata för samlingen finns i TFS-serverns konfigurationsdatabas när samlingen är ansluten och online. När en samling kopplas bort från TFS-servern tar den en kopia av dessa identitetsdata och förpackar dem med samlingen för transport. Utan dessa data kan identitetsdelen av importen inte genomföras. Det rekommenderas att samlingen förblir frånkopplad tills dess att importen slutförts, eftersom det inte går att importera de ändringar som inträffar under importen.
2. **Skapa säkerhetskopia.** Nästa steg i migreringsprocessen är att skapa en säkerhetskopia som kan importeras i Azure DevOps Services. Data-tier Application Component Packages (DACPAC) är en SQL Server-funktion som gör det möjligt för databasändringar att packas in i en enskild fil och distribueras till andra instanser av SQL. Den kan även återställas direkt till Azure DevOps Services och används därför för att få in samlingsdata i molnet. Contoso använder verktyget SqlPackage.exe för att skapa DACPAC. Detta verktyg ingår i SQL Server Data Tools.
3. **Ladda upp till lagring.** När DACPAC skapats laddar de upp den till Azure Storage. När den laddats upp får de en signatur för delad åtkomst (SAS) som gör att TFS-migrationsverktyget får tillgång till lagringen.
4. **Fyll i importen.** Contoso kan sedan fylla i saknade fält i importfilen, inklusive DACPAC-inställningen. Till att börja med anger de att de vill utföra en **testimport** för att kontrollera att allt fungerar korrekt innan de genomför migreringen.
5. **Utföra en testkörning.** Testkörningar hjälper till att testa migrering av samlingar. Testkörningar sparas en begränsad tid och tas bort innan en verklig migrering. De tas bort automatiskt efter en viss tid. En kommentar om när testkörningen tas bort finns med i det e-postmeddelande om lyckad import som skickas efter importen. Notera detta och anpassa planeringen.
6. **Slutföra produktionsmigreringen.** När testmigreringen utförts genomför Contosos administratörer den slutliga migreringen genom att uppdatera filen **import.json** och köra importen igen.

### <a name="detach-the-collection"></a>Koppla från samlingen

Innan de börjar gör Contosos administratörer en lokal SQL Server-säkerhetskopia och tar en VMware-ögonblicksbild av TFS-servern innan frånkopplingen.

1. I TFS administratörskonsol väljer de den samling de vill frånkoppla (**ContosoDev**).

    ![Migrera](./media/contoso-migration-tfs-vsts/migrate1.png)

2. I **Allmänt** väljer de **Koppla från samling**.

    ![Migrera](./media/contoso-migration-tfs-vsts/migrate2.png)

3. I guiden Koppla bort teamprojektsamling > **Servicemeddelande** anger de ett meddelande för användare som försöker ansluta till projekt i samlingen.

    ![Migrera](./media/contoso-migration-tfs-vsts/migrate3.png)

4. I **Frånkopplingsförlopp** övervakar de processen och väljer **Nästa** när processen slutförs.

    ![Migrera](./media/contoso-migration-tfs-vsts/migrate4.png)

5. I **Beredskapskontroller** väljer de **Koppla från** när kontrollerna slutförts.

    ![Migrera](./media/contoso-migration-tfs-vsts/migrate5.png)

6. De väljer **Stäng** för att slutföra.

    ![Migrera](./media/contoso-migration-tfs-vsts/migrate6.png)

7. Samlingen visas inte längre i TFS-administratörskonsolen.

    ![Migrera](./media/contoso-migration-tfs-vsts/migrate7.png)

### <a name="generate-a-dacpac"></a>Skapa en DACPAC

Contoso skapar en säkerhetskopia (DACPAC) för import till Azure DevOps Services.

- SqlPackage.exe i SQL Server Data Tools används för att skapa DACPAC. Flera versioner av SqlPackage.exe installeras med SQL Server Data Tools, under mappar med namn som 120, 130 och 140. Det är viktigt att välja rätt version för att skapa DACPAC.
- TFS 2018-importer måste använda SqlPackage.exe från mappen 140 eller högre. För CONTOSOTFS finns filen i mappen: **C:\Program (x86)\Microsoft Visual Studio\2017\Enterprise\Common7\IDE\Extensions\Microsoft\SQLDB\DAC\140**.

Contosos administratörer skapar DACPAC så här:

1. De öppnar en kommandotolk och går till platsen där SQLPackage.exe finns. De skriver följande kommando för att skapa DACPAC:

    ``` console
    SqlPackage.exe /sourceconnectionstring:"Data Source=SQLSERVERNAME\INSTANCENAME;Initial Catalog=Tfs_ContosoDev;Integrated Security=True" /targetFile:C:\TFSMigrator\Tfs_ContosoDev.dacpac /action:extract /p:ExtractAllTableData=true /p:IgnoreUserLoginMappings=true /p:IgnorePermissions=true /p:Storage=Memory
    ```

    ![Säkerhetskopiera](./media/contoso-migration-tfs-vsts/backup1.png)

2. Följande meddelande visas när kommandot körts.

    ![Säkerhetskopiera](./media/contoso-migration-tfs-vsts/backup2.png)

3. De verifierar DACPAC-filens egenskaper

    ![Säkerhetskopiera](./media/contoso-migration-tfs-vsts/backup3.png)

### <a name="update-the-file-to-storage"></a>Ladda upp filen till lagringsplatsen

När DACPAC skapats laddar Contoso upp den till Azure Storage.

1. De laddar ned och installerar [Azure Storage Explorer](https://azure.microsoft.com/features/storage-explorer).

    ![Ladda upp](./media/contoso-migration-tfs-vsts/backup5.png)

2. De ansluter till prenumerationen och letar upp lagringskontot de skapade för migreringen (**contosodevmigration**). De skapar en ny blob-container, **azuredevopsmigration**.

    ![Ladda upp](./media/contoso-migration-tfs-vsts/backup6.png)

3. De specificerar att DACPAC-filen ska laddas upp som en blockblob.

    ![Ladda upp](./media/contoso-migration-tfs-vsts/backup7.png)

4. När filen har laddats upp väljer de filnamnet > **Skapa SAS**. De expanderar de blob-containers som finns under lagringskontot och väljer containern med importfilerna och väljer sedan **Hämta signatur för delad åtkomst**.

    ![Ladda upp](./media/contoso-migration-tfs-vsts/backup8.png)

5. De godkänner standardvärdena och väljer **Skapa**. Det ger tillgång under 24 timmar.

    ![Ladda upp](./media/contoso-migration-tfs-vsts/backup9.png)

6. De kopierar URL:en för signaturen för delad åtkomst så att den kan användas av TFS-migreringsverktyget.

    ![Ladda upp](./media/contoso-migration-tfs-vsts/backup10.png)

> [!NOTE]
> Migreringen måste ske inom denna tidsperiod, annars kommer behörigheten att sluta gälla.
> Skapa inte en SAS-nyckel från Azure-portalen. Nycklar som skapas på detta sätt är kopplade till kontot och fungerar inte med importen.

### <a name="fill-in-the-import-settings"></a>Fyll i importinställningarna

Tidigare fyllde Contosos administratörer delvis i importspecifikationsfilen (import.json). Nu måste de lägga till kvarvarande inställningar.

De öppnar filen import.json och fyller i följande fält:

- **Plats:** Plats för SAS-nyckeln som skapades ovan.
- **Dacpac:** Ange namnet på den DACPAC-fil du laddade upp till lagringskontot. Ta med filtillägget ”.dacpac”.
- **ImportType:** Ställ in på DryRun så länge.

![Importera inställningar](./media/contoso-migration-tfs-vsts/import1.png)

### <a name="do-a-dry-run-migration"></a>Göra en testmigrering

Contosos administratörer börjar med en testmigrering för att säkerställa att allt fungerar korrekt.

1. De öppnar en kommandotolk och går till platsen där TfsMigration finns (`C:\TFSMigrator`).
2. Först validerar de importfilen. De vill vara säkra på att filen är korrekt formaterad och att SAS-nyckeln fungerar.

    `TfsMigrator import /importFile:C:\TFSMigrator\import.json /validateonly`

3. Valideringen returnerar ett fel som anger att SAS-nyckeln behöver en längre förfallotid.

    ![Testkörning](./media/contoso-migration-tfs-vsts/test1.png)

4. De använder Azure Storage Explorer för att skapa en ny SAS-nyckel med en förfallotid på sju dagar.

    ![Testkörning](./media/contoso-migration-tfs-vsts/test2.png)

5. De uppdaterar `import.json`-filen och kör valideringen igen. Den här gången slutförs den utan fel.

    `TfsMigrator import /importFile:C:\TFSMigrator\import.json /validateonly`

    ![Testkörning](./media/contoso-migration-tfs-vsts/test3.png)

6. De startar testmigreringen:

    `TfsMigrator import /importFile:C:\TFSMigrator\import.json`

7. Ett meddelande visas för att bekräfta migreringen. Notera hur länge mellanlagrade data kommer att sparas efter testkörningen.

    ![Testkörning](./media/contoso-migration-tfs-vsts/test4.png)

8. Skärmen för inloggning till Azure AD visas och ska fyllas i med autentiseringsuppgifter för en Contoso-administratör.

    ![Testkörning](./media/contoso-migration-tfs-vsts/test5.png)

9. Ett meddelande visar information om importen.

    ![Testkörning](./media/contoso-migration-tfs-vsts/test6.png)

10. Efter ungefär 15 minuter går de till URL:en och ser följande information:

     ![Testkörning](./media/contoso-migration-tfs-vsts/test7.png)

11. När migreringen slutförts loggar en utvecklingsledare in till Azure DevOps Services för att kontrollera att testkörningen fungerat korrekt. Efter autentisering behöver Azure DevOps Services en del information för att bekräfta organisationen.

    ![Testkörning](./media/contoso-migration-tfs-vsts/test8.png)

12. I Azure DevOps Services kan utvecklingsledaren se att projekten migrerats till Azure DevOps Services. Det finns en kommentar om att organisationen kommer att tas bort om 15 dagar.

    ![Testkörning](./media/contoso-migration-tfs-vsts/test9.png)

13. Utvecklingsledaren öppnar ett av projekten och öppnar **Arbetsuppgifter** > **Tilldelade till mig**. Det här visar att data för arbetsuppgifter har migrerats tillsammans med identitet.

    ![Testkörning](./media/contoso-migration-tfs-vsts/test10.png)

14. Utvecklingsledaren kontrollerar även andra projekt och kod för att bekräfta att källkoden och historiken migrerats.

    ![Testkörning](./media/contoso-migration-tfs-vsts/test11.png)

### <a name="run-the-production-migration"></a>Köra produktionsmigreringen

När testmigreringen är klar går Contosos administratörer vidare med produktionsmigreringen. De tar bort testmigreringen, uppdaterar migreringsinställningarna och kör importen igen.

1. I Azure DevOps Services-portalen tar de bort organisationen som skapades för testimporten.
2. De uppdaterar filen import.json för att ställa in **ImportType** till **ProductionRun**.

    ![Produktion](./media/contoso-migration-tfs-vsts/full1.png)

3. De startar sedan migreringen precis som för testmigreringen: `TfsMigrator import /importFile:C:\TFSMigrator\import.json`.
4. Ett meddelande visas för att bekräfta migreringen och varna om att data kan förvaras på en säker mellanlagringsplats i upp till sju dagar.

    ![Produktion](./media/contoso-migration-tfs-vsts/full2.png)

5. I skärmen för inloggning till Azure AD anger de autentiseringsuppgifter för en Contoso-administratör.

    ![Produktion](./media/contoso-migration-tfs-vsts/full3.png)

6. Ett meddelande visar information om importen.

    ![Produktion](./media/contoso-migration-tfs-vsts/full4.png)

7. Efter cirka 15 minuter går de till URL:en och ser följande information:

    ![Produktion](./media/contoso-migration-tfs-vsts/full5.png)

8. När migreringen slutförts loggar en utvecklingsledare in till Azure DevOps Services för att kontrollera att migreringen genomförts korrekt. Efter inloggning kan utvecklingsledaren se att projekt har migrerats.

    ![Produktion](./media/contoso-migration-tfs-vsts/full6.png)

9. Utvecklingsledaren öppnar ett av projekten och öppnar **Arbetsuppgifter** > **Tilldelade till mig**. Det här visar att data för arbetsuppgifter har migrerats tillsammans med identitet.

    ![Produktion](./media/contoso-migration-tfs-vsts/full7.png)

10. Utvecklingsledaren kontrollerar andra arbetsobjekt för att bekräfta.

    ![Produktion](./media/contoso-migration-tfs-vsts/full8.png)

11. Utvecklingsledaren kontrollerar även andra projekt och kod för att bekräfta att källkoden och historiken migrerats.

    ![Produktion](./media/contoso-migration-tfs-vsts/full9.png)

### <a name="move-source-control-from-tfvc-to-git"></a>Flytta källkontroll från TFVC till GIT

Nu när migreringen är klar vill Contoso övergå från källkodshantering i TFVC till Git. De måste importera den källkod de har i sin Azure DevOps Services-organisation som Git-repos i samma organisation.

1. I Azure DevOps Services-portalen öppnar de en av de tillgängliga TFVC-repos ( **$/PolicyConnect**) och granskar den.

    ![Git](./media/contoso-migration-tfs-vsts/git1.png)

2. De väljer listrutan **Källa** > **Importera**.

    ![Git](./media/contoso-migration-tfs-vsts/git2.png)

3. I **Källtyp** väljer de **TFVC** och anger sökvägen till aktuell repo. De har bestämt sig för att inte migrera historiken.

    ![Git](./media/contoso-migration-tfs-vsts/git3.png)

    > [!NOTE]
    > På grund av skillnader i hur TFVC och Git lagrar versionskontrollinformation rekommenderar vi att Contoso inte migrerar historiken. Detta är den metod som Microsoft använde när de migrerade Windows och andra produkter från centraliserad versionskontroll till Git.

4. Efter importen granskar administratörerna koden.

    ![Git](./media/contoso-migration-tfs-vsts/git4.png)

5. De upprepar processen för den andra lagringsplatsen ( **$/SmartHotelContainer**).

    ![Git](./media/contoso-migration-tfs-vsts/git5.png)

6. När de granskat källan är utvecklingsledarna överens om att migreringen till Azure DevOps Services är klar. Azure DevOps Services är nu källan för all utveckling i de team som var inblandade i migreringen.

    ![Git](./media/contoso-migration-tfs-vsts/git6.png)

**Behöver du mer hjälp?**

[Lär dig mer om att](/azure/devops/repos/git/import-from-TFVC?view=vsts) importera från TFVC.

## <a name="clean-up-after-migration"></a>Rensa efter migrering

När migreringen är klar måste Contoso göra följande:

- Läsa artikeln [efter import](/azure/devops/articles/migration-post-import?view=vsts) för information om ytterligare importaktiviteter.
- Ta bort TFVC-lagringsplatserna eller göra dem skrivskyddade. Kodbaserna får inte användas men kan användas som historikreferens.

## <a name="post-migration-training"></a>Utbildning efter migrering

Contoso måste utbilda relevant personal i Azure DevOps Services och Git.
