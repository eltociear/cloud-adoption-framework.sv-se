---
title: Metodtips för att skydda och hantera arbetsbelastningar som migreras till Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: När du har migrerat till Azure kan du få metodtips om drift, hantering och skydd av migrerade arbetsbelastningar.
author: BrianBlanchard
ms.author: brblanch
ms.date: 12/08/2018
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: b7d2ac8d624115c9d843ded8a045cd68f4050650
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/06/2019
ms.locfileid: "70825866"
---
# <a name="best-practices-for-securing-and-managing-workloads-migrated-to-azure"></a>Metodtips för att skydda och hantera arbetsbelastningar migreras till Azure

Som du planerar och utformar för migrering, förutom att tänka på migreringen, måste du överväga din modell för säkerhet och hantering i Azure efter migreringen. Den här artikeln beskrivs planering och bästa praxis för att skydda din Azure-distribution när du har migrerat och för pågående aktiviteter att hålla din distribution som körs på optimal nivå.

> [!IMPORTANT]
> Bästa praxis och yttranden som beskrivs i den här artikeln baseras på Azure-plattformen och bearbeta funktioner som är tillgängliga vid tidpunkten för skrivning. Funktioner och möjligheter ändras med tiden.

## <a name="secure-migrated-workloads"></a>Skydda migrerade arbetsbelastningar

Efter migreringen är den mest kritiska uppgiften att skydda migrerade arbetsbelastningar från interna och externa hot. Dessa metodtips hjälper dig att göra det:

- [Arbeta med Azure Security Center](#best-practice-follow-azure-security-center-recommendations): Lär dig hur du arbetar med övervakning, utvärderingar och rekommendationer som tillhandahålls av Azure Security Center.
- [Kryptera dina data](#best-practice-encrypt-data): Få metodtips för att kryptera dina data i Azure.
- [Konfigurera program mot skadlig kod](#best-practice-protect-vms-with-antimalware): Skydda dina virtuella datorer mot skadlig kod och skadliga attacker.
- [Skydda webbappar](#best-practice-secure-web-apps): Skydda känslig information i migrerade webbappar.
- [Granska prenumerationer](#best-practice-review-subscriptions-and-resource-permissions): Kontrollera vilka som har åtkomst till dina Azure-prenumerationer och -resurser efter migreringen.
- [Arbeta med loggar](#best-practice-review-audit-and-security-logs): Granska regelbundet dina spårnings- och säkerhetsloggar i Azure.
- [Granska andra säkerhetsfunktioner](#best-practice-evaluate-other-security-features): Förstå och utvärdera avancerade säkerhetsfunktioner som Azure erbjuder.

## <a name="best-practice-follow-azure-security-center-recommendations"></a>Metodtips: Följ Azure Security Center-rekommendationer

Microsoft arbetar hårt för att säkerställa att Azure-klientorganisationsadministratörer har den information som behövs för att aktivera säkerhetsfunktioner som skyddar arbetsbelastningar mot attacker. Azure Security Center erbjuder enhetlig säkerhetshantering. I Security Center kan du tillämpa säkerhetsprinciper i arbetsbelastningarna, begränsa exponeringen för hot, och identifiera och svara på attacker. Security Center analyserar resurser och konfigurationer över Azure-klienter och gör säkerhetsrekommendationer, inklusive:

- **Centraliserad principhantering** – Säkerställ att företagets eller reglerade säkerhetskrav följer standarden genom att hantera principer centralt i alla dina arbetsbelastningar i hybridmoln.
- **Kontinuerlig säkerhetsbedömning** – Övervaka säkerheten i datorer, nätverk, lagring, datatjänster och program så att du kan identifiera potentiella säkerhetsproblem.
- **Rekommendationer som kan åtgärdas** – Åtgärda säkerhetsproblem innan de kan utnyttjas av angripare med hjälp av rangordnade säkerhetsrekommendationer.
- **Rangordnade aviseringar och incidenter** – Fokusera på de mest kritiska hoten först med rangordnade säkerhetsaviseringar och incidenter.

Förutom utvärderingar och rekommendationer innehåller Azure Security Center andra säkerhetsfunktioner som kan aktiveras för specifika resurser.

- **JIT-åtkomst (just-in-time).** Minska nätverkets angreppsyta med begränsad just-in-time-åtkomst till hanteringsportar på virtuella Azure-datorer.
  - Om RDP-port 3389 är öppen på Internet exponeras virtuella datorer för kontinuerlig obehörig aktivitet. Azure IP-adresser är välkänd och hackare avsökning kontinuerligt dem för attacker på Öppna 3389 portar.
  - Just-in-time använder nätverkssäkerhet grupper (NSG) och inkommande regler som gräns för hur lång tid som en specifik port är öppen.
  - Med just-in-aktiveringen, kontrollerar Security Center att en användare har rollbaserad åtkomstkontroll (RBAC) skrivåtkomst åtkomstbehörigheter för en virtuell dator. Dessutom kan ange regler för hur användare kan ansluta till virtuella datorer. Om behörigheterna är OK, en åtkomstbegäran har godkänts och konfigurerar Security Center NSG: er för att tillåta inkommande trafik till de markerade portarna för den tid anger du. NSG:er återgår till sitt tidigare tillstånd när tiden går ut.
- **Anpassningsbara programkontroller.** Håll programvara och skadlig kod borta från virtuella datorer genom att begränsa vilka appar som körs på dem med hjälp av dynamiska listor över tillåtna.
  - Med anpassningsbara programkontroller kan du godkänna appar och förhindra att falska användare eller administratörer installerar ej godkända appar eller kontrollerar appar på dina virtuella datorer.
    - Du kan blockera eller avisera om försök att köra skadliga appar, undvika oönskade eller skadliga appar och säkerställa efterlevnad av organisationens appsäkerhetsprincip.
- **Övervakning av filintegritet.** Säkerställ integriteten för filer som körs på virtuella datorer.
  - Du behöver inte installera programvara för att orsaka problem med virtuella datorer. Ändra en fil kan även orsaka försämring av VM-fel eller prestanda. Filen integritet övervakning undersöker systemfiler och registerinställningar för ändringar och meddelar dig om det har uppdaterats.
  - Security Center rekommenderar som du bör övervaka.

**Lära sig mer:**

- [Läs mer](/azure/security-center/security-center-intro) om Azure Security Center.
- [Läs mer](/azure/security-center/security-center-just-in-time) om just-in-time-åtkomst till virtuell dator.
- [Lär dig mer om](/azure/security-center/security-center-adaptive-application) tillämpa anpassningsbara programkontroller.
- [Kom igång](/azure/security-center/security-center-file-integrity-monitoring) med övervakning av filintegritet.

## <a name="best-practice-encrypt-data"></a>Metodtips: Kryptera data

Kryptering är en viktig del av Azures säkerhetspraxis. Att se till att kryptering är aktiverat på alla nivåer hjälper till att förhindra att obehöriga parter får åtkomst till känsliga data, inklusive data under överföring och i vila.

### <a name="encryption-for-iaas"></a>Kryptering för IaaS

- **Virtuella datorer:** För virtuella datorer kan du använda Azure Disk Encryption för att kryptera dina IaaS-VM-diskar för Windows och Linux.
  - Diskkryptering tillhandahåller volymkryptering av operativsystem- och datadiskar med hjälp av BitLocker för Windows och DM-Crypt för Linux.
  - Du kan använda en krypteringsnyckel som skapas av Azure eller ange egna krypteringsnycklar, som skyddas i Azure Key Vault.
  - Med Disk Encryption, IaaS VM-data är skyddade i vila (på disk) och under VM start.
    - Azure Security Center varnar dig om du har virtuella datorer som inte är krypterade.
- **Lagring:** Skydda vilande data som lagras i Azure Storage.
  - Data som lagras i Azure Storage-konton kan krypteras med hjälp av Microsoft-genererade AES-nycklar som är FIPS 140-2-kompatibla, eller så kan du använda egna nycklar.
  - Kryptering av lagringstjänst är aktiverat för alla nya och befintliga lagringskonton och kan inte inaktiveras.

### <a name="encryption-for-paas"></a>Kryptering för PaaS

Till skillnad från IaaS där du hanterar dina egna virtuella datorer och infrastruktur hanteras plattform och infrastruktur i en PaaS-modell av providern, vilket gör att du kan fokusera på central applogik och -funktioner. Med så många olika typer av PaaS-tjänster utvärderas varje tjänst separat av säkerhetsskäl. Som ett exempel tittar vi på hur vi kan aktivera kryptering för Azure SQL Database.

- **Always Encrypted:** Använd Always Encrypted-guiden i SQL Server Management Studio för att skydda vilande data.
  - Du skapar en Always Encrypted-nyckel för att kryptera enskilda kolumndata.
  - Alltid krypterad nycklar kan lagras krypterade i databasmetadata eller lagras i betrodda viktiga butiker, till exempel Azure Key Vault.
  - Appändringar krävs sannolikt för att använda den här funktionen.
- **Transparent datakryptering (TDE):** Skydda Azure SQL Database med kryptering och dekryptering i realtid av databasen, associerade säkerhetskopior och vilande transaktionsloggfiler.
  - TDE gör att krypteringsaktiviteter kan genomföras utan ändringar på applagret.
  - TDE kan använda krypteringsnycklar som tillhandahålls av Microsoft eller du kan ange dina egna nycklar med stöd för Bring Your Own Key.

**Lära sig mer:**

- [Lär dig mer om](/azure/security/azure-security-disk-encryption-overview) Azure Disk Encryption för virtuella IaaS-datorer.
- [Aktivera](/azure/security/azure-security-disk-encryption-windows) kryptering för IaaS Windows-datorer.
- [Lär dig mer om](/azure/storage/common/storage-service-encryption) Azure Storage Service Encryption för vilande data.
- [Läs](/azure/sql-database/sql-database-always-encrypted-azure-key-vault) en översikt över Always Encrypted.
- [Läs mer om](/azure/sql-database/transparent-data-encryption-azure-sql?view=sql-server-2017) transparent Datakryptering för Azure SQL Database.
- [Läs mer](/azure/sql-database/transparent-data-encryption-byok-azure-sql) om TDE med Bring Your Own Key.

## <a name="best-practice-protect-vms-with-antimalware"></a>Metodtips: Skydda virtuella datorer med program mot skadlig kod

I synnerhet kanske äldre Azure-migrerade virtuella datorer inte har rätt nivå av program mot skadlig kod installerade. Azure tillhandahåller en kostnadsfri slutpunktslösning som hjälper till att skydda virtuella datorer mot virus, spionprogram och annan skadlig kod.

- Microsoft Antimalware för Azure genererar varningar när känd skadlig eller oönskad programvara försöker installera sig själv.
- Det är en enskild agent-lösning som körs i bakgrunden utan mänsklig inblandning.
- I Azure Security Center kan du enkelt identifiera virtuella datorer som inte har slutpunktsskydd körs och installera Microsoft Antimalware efter behov.

![Program mot skadlig kod för virtuella datorer](./media/migrate-best-practices-security-management/antimalware.png)
*program mot skadlig kod för virtuella datorer*

**Lära sig mer:**

- [Läs mer](/azure/security/azure-security-antimalware) om Microsoft Antimalware.

## <a name="best-practice-secure-web-apps"></a>Metodtips: Skydda webbappar

Migrerade webbappar har ett par problem:

- De flesta äldre webbprogram brukar ha känslig information i konfigurationsfiler. Filer som innehåller sådan information kan uppvisa säkerhetsproblem när appar säkerhetskopieras eller när kod kontrolleras till eller från källkontroll.
- När du migrerar webbappar som finns på en virtuell dator flyttar du dessutom sannolikt datorn från ett lokalt nätverk och en brandväggsskyddad miljö till en Internetriktad miljö. Se till att du konfigurerar en lösning som utför samma arbete som dina lokala skyddsresurser.

Azure tillhandahåller ett par lösningar:

- **Azure Key Vault:** I dag vidtar webbapputvecklare åtgärder för att känslig information inte ska läcka från dessa filer. En metod för att skydda information är att extrahera den från filer och placera den i Azure Key Vault.
  - Du kan använda Key Vault för att centralisera lagring av apphemligheter och styra spridningen. Det gör att säkerhetsinformation inte behöver lagras i appfiler.
  - Appar kan på ett säkert sätt komma åt information i valvet med hjälp av URI:er, utan att behöva anpassad kod.
  - Med Azure Key Vault kan du låsa åtkomst via Azure-säkerhetskontroller och sömlöst implementera "uppdatering av nycklar". Microsoft kan inte se eller extrahera dina data.
- **App Service-miljön:** Om en app som du migrerar behöver extra skydd kan du överväga att lägga till en App Service-miljö och brandvägg för webbaserade program för att skydda appresurserna.
  - Azure App Service-miljön tillhandahåller en fullständigt isolerad och dedikerad miljö där du kan köra App Service-appar som Windows- och Linux-webbappar, Docker-containrar, mobilappar och funktioner.
  - Den är användbar för appar som är mycket storskaliga, kräver isolering och säker nätverksåtkomst eller har hög minnesanvändning.
- **Brandvägg för webbaserade program:** En funktion i Azure Application Gateway som tillhandahåller centraliserat skydd för webbappar.
  - Den skyddar webbappar utan att kräva ändringar i serverdelskoden.
  - Den skyddar flera webbappar samtidigt bakom en programgateway.
  - En brandvägg för webbaserade program kan övervakas med hjälp av Azure Monitor och integreras i Azure Security Center.

![Skydda webbappar](./media/migrate-best-practices-security-management/web-apps.png)

*Azure Key Vault*

**Läs mer:**

- [Få en översikt](/azure/key-vault/key-vault-overview) över Azure Key Vault.
- [Läs mer](/azure/application-gateway/waf-overview) om brandvägg för webbaserade program.
- [Få en introduktion](/azure/app-service/environment/intro) till App Service-miljöer.
- [Lär dig hur du](/azure/key-vault/tutorial-web-application-keyvault) konfigurerar en webbapp för att läsa hemligheter från Key Vault.
- [Läs mer](/azure/application-gateway/waf-overview) om brandvägg för webbaserade program.

## <a name="best-practice-review-subscriptions-and-resource-permissions"></a>Metodtips: Granska prenumerationer och resursbehörigheter

När du migrerar dina arbetsbelastningar och kör dem i Azure flyttas personal med arbetsbelastningsåtkomst runt. Ditt säkerhetsteam bör regelbundet granska åtkomst till din Azure-klientorganisation och -resursgrupper. Azure har erbjudanden för identitetshantering och åtkomstkontrollsäkerhet, inklusive rollbaserad åtkomstkontroll (RBAC) för att ge behörighet att komma åt Azure-resurser.

- RBAC tilldelar åtkomstbehörigheter för säkerhetshuvudkonton. Säkerhetsobjekt representerar användare, grupper (en uppsättning användare), tjänsthuvudnamn (identitet som används av appar och tjänster) och hanterade identiteter (en Azure Active Directory-identitet hanteras automatiskt av Azure).
- RBAC kan tilldela roller till säkerhetsprinciper, till exempel ägare, deltagare och läsare och rollen definitioner (en samling av behörigheter) som definierar vilka åtgärder som kan utföras av rollerna.
- RBAC kan också ange omfång som avgör gränsen för en roll. Omfånget kan anges på flera nivåer, inklusive en hanteringsgrupp, prenumeration, resursgrupp eller resurs.
- Se till att administratörer med Azure-åtkomst endast kan komma åt resurser som du vill tillåta. Om de fördefinierade rollerna i Azure inte är tillräckligt detaljerade kan du skapa anpassade roller för att avgränsa och begränsa åtkomstbehörigheter.

![Åtkomstkontroll](./media/migrate-best-practices-security-management/subscription.png)
*åtkomstkontroll - IAM*

**Lära sig mer:**

- [Om](/azure/role-based-access-control/overview) RBAC.
- [Lär dig](/azure/role-based-access-control/role-assignments-portal) att hantera åtkomst med RBAC och Azure-portalen.
- [Läs mer](/azure/role-based-access-control/custom-roles) om anpassade roller.

## <a name="best-practice-review-audit-and-security-logs"></a>Metodtips: Granska spårnings- och säkerhetsloggar

Azure Active Directory (Azure AD) tillhandahåller aktivitetsloggar som visas i Azure Monitor. Loggarna registrerar de åtgärder som utförs i Azure-klientorganisationen, när de utfördes och vem som utförde dem.

- Granskningsloggar visar historiken för uppgifter i klienten. Inloggningsaktivitet loggar show som utfört uppgifterna.
- Åtkomst till säkerhetsrapporter är beroende av din Azure AD-licens. I Kostnadsfri och Basic visas en lista över riskfyllda användare och inloggningar. I Premium 1- och Premium 2-versioner visas underliggande händelseinformation.
- Du kan dirigera aktivitetsloggar till olika slutpunkter för långsiktig kvarhållning och datainsikter.
- Gör det till en vana att granska loggarna eller integrera SIEM-verktygen (Security Information and Event Management) för att automatiskt granska avvikelser. Om du inte använder Premium 1 eller 2, kommer du behöva göra mycket analys dig själv eller med din SIEM-system. Analys innefattar att söka efter riskfyllda inloggningar och händelser, och andra mönster för användarangrepp.

![Användare och grupper](./media/migrate-best-practices-security-management/azure-ad.png)

*Azure AD-användare och -grupper*

**Läs mer:**

- [Lär dig mer om](/azure/active-directory/reports-monitoring/concept-activity-logs-azure-monitor) Azure AD-aktivitetsloggar i Azure Monitor.
- [Lär dig hur du](/azure/active-directory/reports-monitoring/concept-audit-logs) granskar aktivitetsrapporter i Azure AD-portalen.

## <a name="best-practice-evaluate-other-security-features"></a>Metodtips: Utvärdera andra säkerhetsfunktioner

Azure innehåller andra säkerhetsfunktioner som tillhandahåller avancerade säkerhetsalternativ. Vissa av dessa metodtips kräver tilläggslicenser och premiumalternativ.

- **Implementera administrativa Azure AD-enheter (AU).** Det kan vara svårt att delegera administrativa uppgifter till supportpersonal med bara grundläggande Azure-åtkomstkontroll. Att ge supportpersonal åtkomst att administrera alla grupper i Azure AD kanske inte är den idealiska metoden för organisationens säkerhet. Med hjälp av automatiska uppdateringar kan du särskilja Azure-resurser i behållare på ett liknande sätt till lokala organisationsenheter (OU). Om du vill använda Australien måste AU-administratören ha en Azure AD premium-licens. [Läs mer](/azure/active-directory/users-groups-roles/directory-administrative-units).
- **Använd multifaktorautentisering.** Om du har en premium Azure AD-licens kan du aktivera och tillämpa multifaktorautentisering på dina administratörskonton. Nätfiske är det vanligaste sättet som kontons autentiseringsuppgifter komprometteras. När en obehörig har ett administratörskontos autentiseringsuppgifter finns det inget som hindrar dem från omfattande åtgärder, till exempel att ta bort alla resursgrupper. Du kan tillämpa multifaktorautentisering på flera olika sätt, bland annat med e-post, en autentiseringsapp och textmeddelanden. Som administratör kan du välja det minst störande alternativet. Multifaktorautentisering integreras med hotanalys och principer för villkorlig åtkomst för att slumpmässigt kräva ett svar på en multifaktorautentiseringsutmaning. Läs mer om [säkerhetsvägledning](/azure/active-directory/authentication/multi-factor-authentication-security-best-practices) och [hur du konfigurerar multifaktorautentisering](/azure/active-directory/authentication/multi-factor-authentication-security-best-practices).
- **Implementera villkorlig åtkomst.** I de flesta små och medelstora organisationer finns Azure-administratörer och supportteamet förmodligen i en enda geografisk region. I det här fallet kommer de flesta inloggningar från samma områden. Om IP-adresserna för dessa platser är relativt statiska är det rimligt att du inte ser administratörsinloggningar utanför dessa områden. Även om en fjärransluten obehörig skulle kompromettera en administratörs autentiseringsuppgifter kan du implementera säkerhetsfunktioner, till exempel villkorlig åtkomst kombinerat med multifaktorautentisering, för att förhindra inloggning från fjärranslutna platser eller från falska platser från slumpmässiga IP-adresser. [Läs mer](/azure/active-directory/conditional-access/overview) om villkorlig åtkomst och [granska metodtips](/azure/active-directory/conditional-access/best-practices) för villkorlig åtkomst i Azure AD.
- **Granska behörigheter för företagsprogram.** Över tid väljer administratörer Microsoft- och tredjepartslänkar utan att känna till deras inverkan på organisationen. Länkar kan öppna medgivandeskärmar som tilldelar behörigheter till Azure-appar, och kan tillåta åtkomst att läsa Azure AD-data eller till och med fullständig åtkomst att hantera hela Azure-prenumerationen. Du bör regelbundet granska apparna som administratörer och användare har gett åtkomst till Azure-resurser. Se till att dessa appar bara har de behörigheter som krävs. Varje kvartal eller halvår kan du dessutom skicka e-post till användare med en länk till appsidor så att de är medvetna om vilka appar de har gett åtkomst till sina organisationsdata. [Läs mer](/azure/active-directory/manage-apps/application-types) om programtyper, och [kontrollerar](/azure/active-directory/manage-apps/remove-user-or-group-access-portal) apptilldelningar i Azure AD.

## <a name="managed-migrated-workloads"></a>Hanterade migrerade arbetsbelastningar

I det här avsnittet rekommenderar vi några metodtips för Azure-hantering, inklusive:

- [Hantera resurser](#best-practice-name-resource-groups): Metodtips för Azure-resursgrupper och -resurser, inklusive smart namngivning, förhindrande av oavsiktlig borttagning, hantering av resursbehörigheter och effektiv resurstaggning.
- [Använd skisser](#best-practice-implement-blueprints): Få en snabb översikt över hur du använder skisser för att skapa och hantera distributionsmiljöer.
- [Granska arkitekturer](#best-practice-review-azure-reference-architectures): Granska exempel på Azure-arkitekturer att lära dig av när du skapar distributioner efter migreringen.
- [Konfigurera hanteringsgrupper](#best-practice-manage-resources-with-azure-management-groups): Om du har flera prenumerationer kan du samla dem i hanteringsgrupper och använda styrningsinställningar för dessa grupper.
- [Konfigurera åtkomstprinciper](#best-practice-deploy-azure-policy): Tillämpa efterlevnadsprinciper på dina Azure-resurser.
- [Implementera en BCDR-strategi](#best-practice-implement-a-bcdr-strategy): Utforma en BCDR-strategi (affärskontinuitet och haveriberedskap) för att se till att data skyddas, miljön är motståndskraftig och resurser fungerar vid avbrott.
- [Hantera virtuella datorer](#best-practice-use-managed-disks-and-availability-sets): Gruppera virtuella datorer i tillgänglighetsgrupper för motståndskraft och hög tillgänglighet. Använd hanterade diskar för enkel disk- och lagringshantering för virtuella datorer.
- [Övervaka resursanvändning](#best-practice-monitor-resource-usage-and-performance): Aktivera diagnostisk loggning för Azure-resurser, skapa aviseringar och spelböcker för proaktiv felsökning och använd Azure-instrumentpanelen för en enhetlig vy över distributionens hälsa och status.
- [Hantera support och uppdateringar](#best-practice-manage-updates): Förstå Azure-supportplanen och hur du implementerar den, få metodtips för att se till att virtuella datorer är uppdaterade och inför processer för ändringshantering.

## <a name="best-practice-name-resource-groups"></a>Metodtips: Namnge resursgrupper

Om resursgrupperna har beskrivande namn som administratörer och medlemmar i supportteamet enkelt kan identifiera och navigera förbättras produktiviteten och effektiviteten avsevärt.

- Vi rekommenderar att du följer Azures namngivningskonventioner.
- Om du synkroniserar din lokala Active Directory till Azure AD med hjälp av Azure AD Connect bör du överväga att matcha namnen på säkerhetsgrupper lokalt mot namnen på resursgrupper i Azure.

![Namnge](./media/migrate-best-practices-security-management/naming.png)

*Namngivning av resursgrupper*

**Läs mer:**

- [Läs mer](/azure/architecture/best-practices/naming-conventions) om namngivningskonventioner.

## <a name="best-practice-implement-delete-locks-for-resource-groups"></a>Metodtips: Implementera borttagningslås för resursgrupper

Det sista du behöver är att en resursgrupp försvinner eftersom den tagits bort av misstag. Vi rekommenderar att du implementerar borttagningslås så att det inte sker.

![Borttagningslås](./media/migrate-best-practices-security-management/locks.png)

*Borttagningslås*

**Läs mer:**

- [Läs mer](/azure/azure-resource-manager/resource-group-lock-resources) om att låsa resurser för att förhindra oväntade ändringar.

## <a name="best-practice-understand-resource-access-permissions"></a>Metodtips: Förstå resursåtkomstbehörigheter

En prenumerationsägare har åtkomst till alla resursgrupper och resurser i prenumerationen.

- Lägg till personer sparsamt i den här värdefulla tilldelningen. Det är viktigt i att skydda din miljö, säkra och stabila att förstå konsekvenserna av dessa typer av behörigheter.
- Kontrollera att du placera resurser i lämpliga resurser för grupper:
  - Matcha resurser med liknande livscykel tillsammans. Vi rekommenderar behöver du inte flytta en resurs när du vill ta bort en hela resursgruppen.
  - Resurser som har stöd för en funktion eller en arbetsbelastning ska placeras tillsammans för förenklad hantering.

**Lära sig mer:**

- [Läs mer](https://azure.microsoft.com/blog/organizing-subscriptions-and-resource-groups-within-the-enterprise) om att organisera prenumerationer och resursgrupper.

## <a name="best-practice-tag-resources-effectively"></a>Metodtips: Tagga resurser effektivt

Om du bara använder ett resursgruppsnamn som är relaterat till resurser får du ofta inte tillräckligt med metadata för effektiv implementering av mekanismer som intern fakturering eller hantering i en prenumeration.

- Som bästa praxis bör du använda Azure taggar för att lägga till användbara metadata som kan efterfrågas och rapporteras.
- Taggar är ett sätt att organisera resurser med egenskaper som du definierar logiskt. Taggar kan användas till resursgrupper eller resurser direkt.
- Taggar kan tillämpas på en resursgrupp eller på enskilda resurser. En resursgrupps taggar ärvs inte av resurserna i gruppen.
- Du kan automatisera taggning med PowerShell eller Azure Automation, eller tagga enskilda grupper och resurser. Taggningsmetod eller självbetjäning. Om du har ett system för begäranden och ändringshantering kan du enkelt använda informationen i begäran för att fylla i företagsspecifika resurstaggar.

![Taggning](./media/migrate-best-practices-security-management/tagging.png)
*Taggning*

**Lära sig mer:**

- [Lär dig mer om](/azure/azure-resource-manager/resource-group-using-tags) taggning och tagga begränsningar.
- [Granska](/azure/azure-resource-manager/resource-group-using-tags#powershell) PowerShell och CLI-exempel att ställa in taggar och för att lägga till taggar från en resursgrupp på dess resurser.
- [Läs](https://www.azurefieldnotes.com/2016/07/18/azure-resource-tagging-best-practices) metodtips om Azure-taggning.

## <a name="best-practice-implement-blueprints"></a>Metodtips: Implementera skisser

Precis som en skiss tillåter tekniker och arkitekter att skissa designparametrarna för ett projekt kan Azure Blueprints göra det möjligt för molnarkitekter och centrala IT-grupper att definiera en upprepningsbar uppsättning med Azure-resurser som implementerar och tillämpar en organisations standarder, mönster och krav. Med hjälp av Azure Blueprints kan utvecklingsteam snabbt skapa nya miljöer som uppfyller organisationens krav på efterlevnad och som har en uppsättning inbyggda komponenter, till exempel nätverk, för att påskynda utveckling och leverans.

- Använd skisser för att samordna distributionen av resursgrupper, Azure Resource Manager-mallar och princip- och rolltilldelningar.
- Skisser lagras i en globalt distribuerad Azure Cosmos DB. Skissobjekt replikeras till flera Azure-regioner. Replikering ger mindre fördröjning, hög tillgänglighet och konsekvent åtkomst till skiss, oavsett den region som distribuerar en skiss resurser.

**Lära sig mer:**

- [Läs](/azure/governance/blueprints/overview) om skisser.
- [Granska](https://azure.microsoft.com/blog/customizing-azure-blueprints-to-accelerate-ai-in-healthcare) ett skissexempel som används för att påskynda AI inom hälsovård.

## <a name="best-practice-review-azure-reference-architectures"></a>Metodtips: Granska Azure-referensarkitekturer

Det kan kännas överväldigande att skapa säkra, skalbara och hanterbara arbetsbelastningar i Azure. Med kontinuerliga ändringar kan det vara svårt att hålla jämna steg med olika funktioner för en optimal miljö. En referens till Lär dig från kan vara till hjälp när du utformar och migrera dina arbetsbelastningar. Azure och Azure partner har skapat flera exempel referensarkitekturer för olika typer av miljöer. De här exemplen är utformad att ge förslag som du kan läsa från och bygger på.

Referensarkitekturer ordnas efter scenario. De innehåller rekommenderade metoder och råd om hantering, tillgänglighet, skalbarhet och säkerhet.
Azure App Service-miljön tillhandahåller en fullständigt isolerad och dedikerad miljö där du kan köra App Service-appar, inklusive Windows- och Linux-webbappar, Docker-containrar, mobilappar och funktioner. App Service lägger till kraften hos Azure i ditt program med säkerhet, belastningsutjämning, automatisk skalning och automatiserad hantering. Du kan också dra nytta av dess DevOps-funktioner, till exempel kontinuerlig distribution från Azure DevOps och GitHub, pakethantering, miljöer, anpassad domän och SSL-certifikat. App Service är användbart för appar som behöver isolering och säker nätverksåtkomst och de som använder hög mängder minne och andra resurser som behöver skala.

**Lära sig mer:**

- [Lär dig mer om](/azure/architecture/reference-architectures) Azure-referensarkitekturer.
- [Granska](/azure/architecture/example-scenario) Azures exempelscenarier.

## <a name="best-practice-manage-resources-with-azure-management-groups"></a>Metodtips: Hantera resurser med Azure-hanteringsgrupper

Om din organisation har flera prenumerationer behöver du hantera åtkomst, principer och efterlevnad för dem. Med Azures hanteringsgrupper får du en hanteringsnivå över prenumerationsnivån.

- Du kan ordna prenumerationerna i containrar som kallas hanteringsgrupper och tillämpa styrningsvillkor för dem.
- Alla prenumerationer i en hanteringsgrupp ärver automatiskt hanteringsgruppens villkor.
- Hanteringsgrupper ger storskalig hantering i företagsklass, oavsett vilken typ av prenumeration du har.
- Du kan till exempel tillämpa en hanteringsgruppsprincip som begränsar regionerna där virtuella datorer kan skapas. Den här principen tillämpas sedan för alla hanteringsgrupper, prenumerationer och resurser under hanteringsgruppen.
- Du kan skapa en flexibel struktur för hanteringsgrupper och prenumerationer, för att organisera dina resurser i en hierarki för enhetlig princip- och åtkomsthantering.

Följande diagram visar ett exempel på att skapa en hierarki för styrning med hjälp av hanteringsgrupper.

![Hanteringsgrupper](./media/migrate-best-practices-security-management/management-groups.png)
*hanteringsgrupper*

**Lära sig mer:**

- [Läs mer](/azure/governance/management-groups/index) om att organisera resurser i hanteringsgrupper.

## <a name="best-practice-deploy-azure-policy"></a>Metodtips: Distribuera Azure Policy

Azure Policy är en tjänst i Azure som används för att skapa, tilldela och hantera principer.

- Principer tillämpar olika regler och effekterna på resurserna, så att resurserna följer företagets standarder och serviceavtal.
- Azure Policy utvärderar dina resurser, söker efter sådana som inte är kompatibla med företagets säkerhetsprinciper.
- Du kan till exempel skapa en princip som tillåter bara en viss SKU-storlek för virtuella datorer i din miljö. Azure Policy kommer att utvärdera den här inställningen när du skapar och uppdaterar resurser, och när du skannar befintliga resurser.
- Azure erbjuder några inbyggda principer som du kan tilldela eller skapa egna.

![Azure Policy](./media/migrate-best-practices-security-management/policy.png)
*Azure Policy*

**Lära sig mer:**

- [Få en översikt](/azure/governance/policy/overview) över Azure Policy.
- [Läs mer](/azure/governance/policy/tutorials/create-and-manage) om att skapa och hantera principer för att säkerställa efterlevnad.

## <a name="best-practice-implement-a-bcdr-strategy"></a>Metodtips: Implementera en BCDR-strategi

Planering av BCDR (affärskontinuitet och haveriberedskap) är en viktig övning som du bör utföra som en del i planeringsprocessen för Azure-migrering. I juridiska termer kan dina kontrakt innehålla en force majeure-paragraf som eliminerar skyldigheter på grund av en större kraft, till exempel orkaner eller jordbävningar. Men du har också skyldigheter som rör din förmåga att se till att tjänsterna fortsätter att köras, och återställs när det behövs, vid ett haveri. Din förmåga att göra detta kan avgöra ditt företags framtid.

BCDR-strategin måste i huvudsak omfatta:

- **Säkerhetskopiering av data:** Hur du skyddar dina data så att du enkelt kan återställa dem vid avbrott.
- **Haveriberedskap:** Hur du ser till att dina appar är motståndskraftiga och tillgängliga vid avbrott.

### <a name="set-up-bcdr"></a>Konfigurera BCDR

När du migrerar till Azure är det viktigt att förstå att även om Azure-plattformen tillhandahåller dessa inbyggda återhämtningsfunktioner måste du utforma Azure-distributionen för att dra nytta av Azure-funktioner och -tjänster som tillhandahåller hög tillgänglighet, haveriberedskap och säkerhetskopiering.

- Din BCDR-lösning beror på företagets mål och påverkas av din strategi för Azure-distributionen. IaaS- (infrastruktur som en tjänst) och PaaS-distributioner (plattform som en tjänst) innebär olika utmaningar för BCDR.
- När BCDR-lösningarna är på plats bör de testas regelbundet för att kontrollera att strategin fortfarande är användbar.

### <a name="back-up-an-iaas-deployment"></a>Säkerhetskopiera en IaaS-distribution

I de flesta fall tas en lokal arbetsbelastning ur bruk efter migreringen och din lokala strategi för säkerhetskopiering av data måste utökas eller ersättas. Om du migrerar hela datacentret till Azure måste du utforma och implementera en fullständig säkerhetskopieringslösning med hjälp av Azure-tekniker eller integrerade tredjepartslösningar.

För arbetsbelastningar som körs på virtuella Azure IaaS-datorer bör du fundera på följande säkerhetskopieringslösningar:

- **Azure Backup:** Tillhandahåller programkonsekventa säkerhetskopior för virtuella Azure-datorer för Windows och Linux.
- **Ögonblicksbilder för lagring:** Tar ögonblicksbilder av bloblagring.

#### <a name="azure-backup"></a>Azure Backup

Med Azure Backup skapas dataåterställningspunkter som lagras i Azure Storage. Azure Backup kan säkerhetskopiera Azure-VM-diskar och Azure Files (förhandsversion). Azure Files tillhandahåller filresurser i molnet, tillgängliga via SMB.

Du kan använda Azure Backup för att säkerhetskopiera virtuella datorer på ett par olika sätt.

- **Direkt säkerhetskopiering från VM-inställningar.** Du kan säkerhetskopiera virtuella datorer med Azure Backup direkt från alternativen för virtuella datorer i Azure-portalen. Du kan säkerhetskopiera den virtuella datorn en gång om dagen och återställa VM-disken efter behov. Azure Backup tar appmedvetna dataögonblicksbilder (VSS) och ingen agent installeras på den virtuella datorn.
- **Direkt säkerhetskopiering i ett Recovery Services-valv.** Du kan säkerhetskopiera virtuella IaaS-datorer genom att distribuera ett Azure Backup Recovery Services-valv. Det ger en enda plats för att spåra och hantera säkerhetskopior samt detaljerade alternativ för säkerhetskopiering och återställning. Säkerhetskopieringen sker upp till tre gånger per dag, på fil-/mappnivå. Den är inte appmedveten och Linux stöds inte. Installera MARS-agenten (Microsoft Azure Recovery Services) på varje virtuell dator som du vill säkerhetskopiera med den här metoden.
- **Skydda den virtuella datorn med Azure Backup Server.** Azure Backup Server tillhandahålls utan kostnad med Azure Backup. Den virtuella datorn säkerhetskopieras till lokal Azure Backup Server-lagring. Sedan säkerhetskopierar du Azure Backup Server till Azure i ett valv. Säkerhetskopieringen är appmedveten, med fullständig kornighet för säkerhetskopieringsfrekvens och -kvarhållning. Du kan säkerhetskopiera på appnivå, till exempel genom att säkerhetskopiera SQL Server eller SharePoint.

Av säkerhetsskäl krypterar Azure Backup rörliga data med AES 256 och skickar dem via HTTPS till Azure. Säkerhetskopierade vilande data i Azure krypteras med hjälp av [kryptering för lagringstjänst (SSE)](/azure/storage/common/storage-service-encryption?toc=%2fazure%2fstorage%2fqueues%2ftoc.json), och data för överföring och lagring.

![Azure Backup](./media/migrate-best-practices-security-management/iaas-backup.png)
*Azure Backup*

**Lära sig mer:**

- [Lär dig mer om](/azure/backup/backup-introduction-to-azure-backup) olika typer av säkerhetskopior.
- [Planera en infrastruktur för säkerhetskopiering](/azure/backup/backup-azure-vms-introduction) för virtuella Azure-datorer.

#### <a name="storage-snapshots"></a>Ögonblicksbilder av lagring

Virtuella Azure-datorer lagras som sidblobar i Azure Storage.

- Ögonblicksbilder avbilda blob-tillstånd vid en viss tidpunkt.
- Som en alternativ metod för säkerhetskopiering för Virtuella Azure-diskar, kan du ta en ögonblicksbild av storage-blobbar och kopiera dem till ett annat lagringskonto.
- Du kan kopiera en hel blob eller använda en inkrementell ögonblicksbild kopia kopiera endast deltaändringar och minska lagringsutrymmet.
- Du kan aktivera mjuk borttagning för blob storage-konton som en extra försiktighetsåtgärd. När den här funktionen är aktiverad markeras en blob som tas bort för borttagning men rensas inte omedelbart. Under övergångsperioden kan blobben återställas.

**Läs mer:**

- [Lär dig mer om](/azure/storage/blobs/storage-blobs-introduction) Azure blob-lagring.
- [Lär dig hur du](/azure/storage/blobs/storage-blob-snapshots) skapa en blobögonblicksbild.
- [Granska ett exempelscenario](https://azure.microsoft.com/blog/microsoft-azure-block-blob-storage-backup) för blob storage-säkerhetskopiering.
- [Läs mer](/azure/storage/blobs/storage-blob-soft-delete) om mjuk borttagning.
- [Haveriberedskap och forcerad redundans (förhandsversion) i Azure Storage](/azure/storage/common/storage-disaster-recovery-guidance?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)

#### <a name="third-party-backup"></a>Säkerhetskopiering från tredje part

Du kan dessutom använda lösningar från tredje part för att säkerhetskopiera virtuella Azure-datorer och storage-behållare till lokal lagring eller andra molnleverantörer. [Läs mer](https://azuremarketplace.microsoft.com/marketplace/apps?search=backup&page=1) om säkerhetskopieringslösningar på Azure Marketplace.

### <a name="set-up-disaster-recovery-for-iaas-apps"></a>Konfigurera haveriberedskap för IaaS-appar

Förutom att skydda data måste BCDR-planeringen ta hänsyn till hur appar och arbetsbelastningar ska förbli tillgängliga i händelse av ett haveri. För arbetsbelastningar som körs på virtuella Azure IaaS-datorer och Azure-lagring bör du fundera på följande lösningar:

#### <a name="azure-site-recovery"></a>Azure Site Recovery

Azure Site Recovery är den primära Azure-tjänst för att säkerställa som virtuella Azure-datorer kan anslutas och VM appar som har gjorts tillgängliga vid avbrott.

Site Recovery replikerar virtuella datorer från en primär till sekundär Azure-region. När en katastrof inträffar du redundansväxlar virtuella datorer från den primära regionen och fortsatt åtkomst till dem som vanligt i den sekundära regionen. När driften återgår till det normala kan du återställa virtuella datorer till den primära regionen.

![Azure Site Recovery](./media/migrate-best-practices-security-management/site-recovery.png)

*Site Recovery*

**Läs mer:**

- [Granska](/azure/virtual-machines/virtual-machines-disaster-recovery-guidance) scenarier för haveriberedskap för virtuella Azure-datorer.
- [Lär dig hur du](/azure/site-recovery/azure-to-azure-replicate-after-migration) konfigurerar haveriberedskap för en virtuell Azure-dator efter migreringen.

## <a name="best-practice-use-managed-disks-and-availability-sets"></a>Metodtips: Använd hanterade diskar och tillgänglighetsuppsättningar

Azure använder tillgänglighetsuppsättningar för att gruppera virtuella datorer logiskt och för att isolera virtuella datorer i en uppsättning från andra resurser. Virtuella datorer i en tillgänglighetsuppsättning sprids över flera feldomäner med separata undersystem, för att skydda mot lokala fel, och de sprids också över flera uppdateringsdomäner så att inte alla virtuella datorer i en uppsättning startas om på samma gång.

Hanterade Azure-diskar förenklar diskhantering för virtuella Azure IaaS-datorer genom att hantera de lagringskonton som är associerade med VM-diskarna.

- Vi rekommenderar att du använder hanterade diskar där det är möjligt. Du behöver bara ange typ av lagring som du vill använda och storleken på disken du behöver, och skapar hanterar Azure disken åt dig, i bakgrunden.
- Du kan konvertera befintliga diskar som hanteras.
- Du bör skapa virtuella datorer i tillgänglighetsuppsättningar för hög flexibilitet och tillgänglighet. Vid planerade eller oplanerade avbrott säkerställer tillgänglighetsuppsättningar att minst en av dina virtuella datorer i uppsättningen fortfarande är tillgänglig.

![Hanterade diskar](./media/migrate-best-practices-security-management/managed-disks.png)

*Hanterade diskar*

**Läs mer:**

- [Få en översikt](/azure/virtual-machines/windows/managed-disks-overview) av hanterade diskar.
- [Lär dig mer om](/azure/virtual-machines/windows/convert-unmanaged-to-managed-disks) konvertera diskar som hanteras.
- [Lär dig hur du](/azure/virtual-machines/windows/manage-availability) hanterar tillgängligheten för virtuella Windows-datorer i Azure.

## <a name="best-practice-monitor-resource-usage-and-performance"></a>Metodtips: Övervaka resursanvändning och prestanda

Du kanske har flyttat dina arbetsbelastningar till Azure för dess omfattande skalningsfunktioner. Flytta din arbetsbelastning betyder inte dock att Azure automatiskt implementerar skalning utan kommentarer. Som exempel:

- Om organisationen marknadsföring skickar en ny TV-annons som driver 300% mer trafik, kan det leda till problem med tillgängligheten för platsen. Din nyligen migrerade arbetsbelastning kan orsaka tilldelade gränser och krascher.
- Ett annat exempel kanske en distribuerad denial of service (DDoS)-attack på din migrerade arbetsbelastning. I det här fallet kanske du inte vill att skala, men för att förhindra att källan för attackerna från att nå dina resurser.

Båda fallen har olika lösningar, men båda du behöver du en överblick över vad som händer med användnings- och prestandaövervakning.

- Azure Monitor kan lyfta fram de här måtten och ge svar med aviseringar, automatisk skalning, händelsehubbar, logic apps och mycket mer.
- Du kan integrera din SIEM tredjepartsprogram att övervaka Azure loggarna för gransknings- och prestanda händelser utöver Azure-övervakning.

![Azure Monitor](./media/migrate-best-practices-security-management/monitor.png)
*Azure Monitor*

**Lära sig mer:**

- [Lär dig mer om](/azure/azure-monitor/overview) Azure Monitor.
- [Få metodtips](/azure/architecture/best-practices/monitoring) för övervakning och diagnostik.
- [Lär dig mer om](/azure/architecture/best-practices/auto-scaling) automatisk skalning.
- [Lär dig hur du](/azure/security-center/security-center-export-data-to-siem) dirigerar Azure-data till ett SIEM-verktyg.

## <a name="best-practice-enable-diagnostic-logging"></a>Metodtips: Aktivera diagnostisk loggning

Azure-resurser genererar ett antal loggningsmått och telemetridata.

- Som standard har de flesta typer av resurser inte Diagnostisk loggning är aktiverat.
- Du kan fråga efter loggningsdata och skapa aviseringar och spelböcker baserat på den genom att aktivera Diagnostisk loggning för dina resurser.
- När du aktiverar diagnostikloggning har varje resurs en specifik uppsättning kategorier. Du väljer en eller flera loggningskategorier och en plats för loggdata. Loggar kan skickas till ett lagringskonto, en händelsehubb eller till Azure Monitor-loggar.

![Diagnostisk loggning](./media/migrate-best-practices-security-management/diagnostics.png)
*Diagnostisk loggning*

**Lära sig mer:**

- [Lär dig mer om](/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs) samla in och använda loggdata.
- [Läs vad som stöds](/azure/monitoring-and-diagnostics/monitoring-diagnostic-logs-schema) för diagnostisk loggning.

## <a name="best-practice-set-up-alerts-and-playbooks"></a>Metodtips: Konfigurera aviseringar och spelböcker

Med diagnostisk loggning aktiverad för Azure-resurser kan du börja använda loggningsdata för att skapa anpassade aviseringar.

- Aviseringar meddela proaktivt dig när villkor finns i dina övervakningsdata. Du kan sedan åtgärda problem innan systemanvändare uppmärksamma dem. Du kan meddela på måttvärden, loggsökningsfrågor, händelser i aktivitetsloggen, plattform hälsotillstånd och tillgänglighet för webbplatsen.
- Du kan köra en Logic App Spelbok när aviseringarna utlöses. En spelbok hjälper dig att automatisera och samordna ett svar på en specifik avisering. Spelböcker baseras på Azure Logic Apps. Du kan använda Logic App-mallar för att skapa spelböcker eller skapa egna.
- Som ett enkelt exempel kan du skapa en avisering utlöses när en port-genomsökning utnyttjas mot en grupp. Du kan ställa in en spelbok som körs och låser IP-adressen för genomsökning ursprunget.
- Ett annat exempel kanske en app med en minnesläcka. När minnesanvändningen hämtar till en viss punkt, kan en spelbok återanvända processen.

![Aviseringar](./media/migrate-best-practices-security-management/alerts.png)
*aviseringar*

**Lära sig mer:**

- [Lär dig mer om](/azure/monitoring-and-diagnostics/monitoring-overview-alerts) aviseringar.
- [Läs mer](/azure/security-center/security-center-playbooks) om säkerhetsspelböcker som svarar på Security Center-aviseringar.

## <a name="best-practice-use-the-azure-dashboard"></a>Metodtips: Använd Azure-instrumentpanelen

Azure-portalen är en webbaserad enhetlig konsol som du kan använda för att skapa, hantera och övervaka allt från enkla webbappar till komplexa molnprogram. Den innehåller en anpassningsbar instrumentpanel och hjälpmedelsalternativ.

- Du kan skapa flera instrumentpaneler och dela dem med andra som har åtkomst till dina Azure-prenumerationer.
- Med den här delade modell har ditt team insyn i Azure-miljön, så att de kan vara proaktiv när du hanterar system i molnet.

![Azure-instrumentpanelen](./media/migrate-best-practices-security-management/dashboard.png)
*Azure-instrumentpanelen*

**Lära sig mer:**

- [Lär dig hur du](/azure/azure-portal/azure-portal-dashboards) skapa en instrumentpanel.
- [Läs mer](/azure/azure-portal/azure-portal-dashboards-structure) om instrumentpanelsstruktur.

## <a name="best-practice-understand-support-plans"></a>Metodtips: Förstå supportplaner

Vid något tillfälle måste du samarbeta med din supportpersonal eller Microsofts supportpersonal. Det är viktigt att ha en uppsättning principer och procedurer för support vid scenarier som haveriberedskap. Dessutom bör dina administratörer och supportpersonal utbildas i att implementera dessa principer.

- Om ett problem med Azure-tjänsten mot förmodan påverkar din arbetsbelastning bör administratörer veta hur de skickar in en supportbegäran till Microsoft på det lämpligaste och effektivaste sättet.
- Bekanta dig med de olika supportplanerna som erbjuds för Azure. De röra sig om svarstider som är dedikerad till Developer-instanser till Premier support med en svarstid på mindre än 15 minuter.

![Supportavtal](./media/migrate-best-practices-security-management/support.png)
*supportavtal*

**Lära sig mer:**

- [Få en översikt](https://azure.microsoft.com/support/options) av Azure-supportavtal.
- [Läs mer](https://azure.microsoft.com/support/legal/sla) om serviceavtal (SLA).

## <a name="best-practice-manage-updates"></a>Metodtips: Hantera uppdateringar

Det är en enorm uppgift att se till att virtuella Azure-datorer är uppdaterade med de senaste operativsystems- och programuppdateringarna. Möjligheten att ansluta alla virtuella datorer om du vill ta reda på vilka uppdateringar som de behöver och att skicka den automatiskt dessa uppdateringar är mycket användbart.

- Du kan använda uppdateringshantering i Azure Automation för att hantera uppdateringar av operativsystemet för datorer som kör Windows och Linux-datorer som distribueras i Azure, lokalt och i andra molnleverantörer.
- Använda uppdateringshantering för att snabbt bedöma status för tillgängliga uppdateringar på alla agentdatorer och hantera installationen av uppdateringen.
- Du kan aktivera uppdateringshantering för virtuella datorer direkt från ett Azure Automation-konto. Du kan också uppdatera en enskild virtuell dator från sidan virtuell dator i Azure-portalen.
- Dessutom kan virtuella Azure-datorer som kan registreras med System Center Configuration Manager. Du kan sedan migrera Configuration Manager-arbetsbelastningar till Azure och göra uppdateringar för rapporterings- och programvara från ett enda webbgränssnitt.

![VM-uppdateringar](./media/migrate-best-practices-security-management/updates.png)
*uppdateringar*

**Lära sig mer:**

- [Lär dig mer om](/azure/automation/automation-update-management) uppdateringshantering i Azure.
- [Lär dig hur du](/azure/automation/oms-solution-updatemgmt-sccmintegration) integrera Configuration Manager med hantering av uppdateringar.
- [Vanliga frågor och svar](/sccm/core/understand/configuration-manager-on-azure) om Configuration Manager i Azure.

## <a name="implement-a-change-management-process"></a>Implementera en ändringshanteringsprocess

Precis som med andra produktionssystem kan alla typer av ändringar påverka din miljö. En ändringshanteringsprocess som kräver att begäranden skickas in för att göra ändringar i produktionssystem är ett värdefullt tillägg i den migrerade miljön.

- Du kan skapa den bästa praxis ramverk för ändringshantering för att öka medvetenheten i administratörer och supportpersonal.
- Du kan använda Azure Automation för att hjälpa till med konfigurationshantering och spårning av ändringar för dina migrerade arbetsflöden.
- När tvingande av processen för ändringshantering, du kan använda granskningsloggar för att länka Azure ändra loggar i antas vara (eller inte) befintliga ändringsbegäranden. Så om du ser att en ändring görs utan motsvarande ändringsbegäran kan du undersöka vad som gått fel i processen.

Azure har en lösning för ändringsspårning i Azure Automation:

- Lösningen spårar ändringar i Windows- och Linux-programvara och -filer, Windows-registernycklar, Windows-tjänster och Linux-daemon.
- Ändringar på övervakade servrar skickas till Azure Monitor-tjänsten i molnet för bearbetning.
- Logik tillämpas på mottagna data och molntjänsten registrerar data.
- På instrumentpanelen för ändringsspårning kan du enkelt se ändringar som gjorts i din serverinfrastruktur.

![Ändringshantering](./media/migrate-best-practices-security-management/change.png)
*ändringshantering*

**Lära sig mer:**

- [Lär dig mer om](/azure/automation/automation-change-tracking) ändringsspårning.
- [Lär dig mer om](/azure/automation/automation-intro) Azure Automation-funktioner.

## <a name="next-steps"></a>Nästa steg

Granska andra metodtips:

- [Bästa praxis](migrate-best-practices-networking.md) för nätverk efter migreringen.
- [Bästa praxis](migrate-best-practices-costs.md) för kostnadshantering efter migreringen.
