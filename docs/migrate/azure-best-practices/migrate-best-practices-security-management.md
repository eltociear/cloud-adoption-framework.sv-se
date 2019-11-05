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
ms.openlocfilehash: ca56669818add8e54d7c4805a19879412da54567
ms.sourcegitcommit: bf9be7f2fe4851d83cdf3e083c7c25bd7e144c20
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 11/04/2019
ms.locfileid: "73564769"
---
# <a name="best-practices-for-securing-and-managing-workloads-migrated-to-azure"></a>Metodtips för att skydda och hantera arbetsbelastningar som migreras till Azure

När du planerar och utformar inför migreringen måste du, förutom att fundera över själva migreringen, ta hänsyn till din säkerhets- och hanteringsmodell i Azure efter migreringen. I den här artikeln beskrivs planering och metodtips för att skydda din Azure-distribution efter migreringen, och för pågående aktiviteter för att köra distributionen på en optimal nivå.

> [!IMPORTANT]
> De metodtips och åsikter som beskrivs i den här artikeln baseras på de tillgängliga funktionerna i Azure-plattformen och -tjänsten när den skrevs. Funktioner förändras över tid.

## <a name="secure-migrated-workloads"></a>Skydda migrerade arbetsbelastningar

Efter migreringen är den mest kritiska uppgiften att skydda migrerade arbetsbelastningar mot interna och externa hot. Dessa metodtips hjälper dig att göra det:

- [Arbeta med Azure Security Center](#best-practice-follow-azure-security-center-recommendations): Lär dig hur du arbetar med övervakning, utvärderingar och rekommendationer från Azure Security Center.
- [Kryptera dina data](#best-practice-encrypt-data): få bästa metoder för att kryptera dina data i Azure.
- [Konfigurera program mot skadlig kod](#best-practice-protect-vms-with-antimalware): skydda dina virtuella datorer mot skadlig kod och skadliga attacker.
- [Säkra webbappar](#best-practice-secure-web-apps): Håll känslig information säker i migrerade webb program.
- [Granska prenumerationer](#best-practice-review-subscriptions-and-resource-permissions): kontrol lera vem som har åtkomst till dina Azure-prenumerationer och-resurser efter migreringen.
- [Arbeta med loggar](#best-practice-review-audit-and-security-logs): granska dina Azures gransknings-och säkerhets loggar med jämna mellanrum.
- [Granska andra säkerhetsfunktioner](#best-practice-evaluate-other-security-features): förstå och utvärdera avancerade säkerhetsfunktioner som Azure erbjuder.

## <a name="best-practice-follow-azure-security-center-recommendations"></a>Bästa praxis: Följ Azure Security Center rekommendationer

Microsoft arbetar hårt för att säkerställa att Azure-klientorganisationsadministratörer har den information som behövs för att aktivera säkerhetsfunktioner som skyddar arbetsbelastningar mot attacker. Azure Security Center tillhandahåller enhetlig säkerhetshantering. Från Security Center kan du tillämpa säkerhetsprinciper i arbetsbelastningar, begränsa hotexponering samt identifiera och åtgärda attacker. Security Center analyserar resurser och konfigurationer i Azure-klientorganisationer och ger säkerhetsrekommendationer, inklusive:

- **Centraliserad principhantering** – Säkerställ att företagets eller reglerade säkerhetskrav följer standarden genom att hantera principer centralt i alla dina arbetsbelastningar i hybridmoln.
- **Kontinuerlig säkerhetsbedömning** – Övervaka säkerheten i datorer, nätverk, lagring, datatjänster och program så att du kan identifiera potentiella säkerhetsproblem.
- **Rekommendationer som kan åtgärdas** – Åtgärda säkerhetsproblem innan de kan utnyttjas av angripare med hjälp av rangordnade säkerhetsrekommendationer.
- **Rangordnade aviseringar och incidenter** – Fokusera på de mest kritiska hoten först med rangordnade säkerhetsaviseringar och incidenter.

Förutom utvärderingar och rekommendationer innehåller Azure Security Center andra säkerhetsfunktioner som kan aktiveras för specifika resurser.

- **JIT-åtkomst (just-in-time).** Minska nätverkets angreppsyta med begränsad just-in-time-åtkomst till hanteringsportar på virtuella Azure-datorer.
  - Om RDP-port 3389 är öppen på Internet exponeras virtuella datorer för kontinuerlig obehörig aktivitet. Azures IP-adresser är välkända och hackare söker kontinuerligt av dem för attacker på öppna 3389-portar.
  - Med just-in-time används nätverkssäkerhetsgrupper (NSG) och inkommande regler som begränsar hur lång tid en specifik port är öppen.
  - Med just-in-time aktiverat kontrollerar Security Center att en användare har skrivbehörighet enligt rollbaserad åtkomstkontroll (RBAC) för en virtuell dator. Ange även regler för hur användarna kan ansluta till virtuella datorer. Om behörigheterna är okej godkänns en åtkomstbegäran och Security Center konfigurerar NSG:er att tillåta inkommande trafik till de valda portarna under den tid du anger. NSG:er återgår till sitt tidigare tillstånd när tiden går ut.
- **Anpassningsbara programkontroller.** Håll programvara och skadlig kod borta från virtuella datorer genom att begränsa vilka appar som körs på dem med hjälp av dynamiska listor över tillåtna.
  - Med anpassningsbara programkontroller kan du godkänna appar och förhindra att falska användare eller administratörer installerar ej godkända appar eller kontrollerar appar på dina virtuella datorer.
    - Du kan blockera eller avisera om försök att köra skadliga appar, undvika oönskade eller skadliga appar och säkerställa efterlevnad av organisationens appsäkerhetsprincip.
- **Övervakning av filintegritet.** Säkerställ integriteten för filer som körs på virtuella datorer.
  - Du behöver inte installera program vara för att orsaka problem med virtuella datorer. Att ändra en systemfil kan också orsaka fel eller prestandaförsämring. Med övervakning av filintegritet undersöks ändringar av systemfiler och registerinställningar, och du meddelas om något uppdateras.
  - Security Center rekommenderar vilka filer du bör övervaka.

**Läs mer:**

- [Läs mer](https://docs.microsoft.com/azure/security-center/security-center-intro) om Azure Security Center.
- [Läs mer](https://docs.microsoft.com/azure/security-center/security-center-just-in-time) om just-in-time-åtkomst till virtuella datorer.
- [Läs mer](https://docs.microsoft.com/azure/security-center/security-center-adaptive-application) om att tillämpa anpassningsbara programkontroller.
- [Kom igång](https://docs.microsoft.com/azure/security-center/security-center-file-integrity-monitoring) med övervakning av filintegritet.

## <a name="best-practice-encrypt-data"></a>Bästa praxis: kryptera data

Kryptering är en viktig del av Azures säkerhetspraxis. Att se till att kryptering är aktiverat på alla nivåer hjälper till att förhindra att obehöriga parter får åtkomst till känsliga data, inklusive data under överföring och i vila.

### <a name="encryption-for-iaas"></a>Kryptering för IaaS

- **Virtuella datorer:** För virtuella datorer kan du använda Azure Disk Encryption för att kryptera dina Windows-och Linux-IaaS VM-diskar.
  - Diskkryptering tillhandahåller volymkryptering av operativsystem- och datadiskar med hjälp av BitLocker för Windows och DM-Crypt för Linux.
  - Du kan använda en krypteringsnyckel som skapas av Azure eller ange egna krypteringsnycklar, som skyddas i Azure Key Vault.
  - Med diskkryptering skyddas IaaS-VM-data i vila (på disken) och vid start av virtuella datorer.
    - Azure Security Center varnar dig om du har virtuella datorer som inte är krypterade.
- **Lagring:** Skydda i rest-data som lagras i Azure Storage.
  - Data som lagras i Azure Storage-konton kan krypteras med hjälp av Microsoft-genererade AES-nycklar som är FIPS 140-2-kompatibla, eller så kan du använda egna nycklar.
  - Kryptering för lagringstjänst aktiveras för alla nya och befintliga lagringskonton och kan inte inaktiveras.

### <a name="encryption-for-paas"></a>Kryptering för PaaS

Till skillnad från IaaS där du hanterar dina egna virtuella datorer och infrastruktur hanteras plattform och infrastruktur i en PaaS-modell av providern, vilket gör att du kan fokusera på central applogik och -funktioner. Med så många olika typer av PaaS-tjänster utvärderas varje tjänst separat av säkerhetsskäl. Som ett exempel tittar vi på hur vi kan aktivera kryptering för Azure SQL Database.

- **Always Encrypted:** Använd guiden Always Encrypted i SQL Server Management Studio för att skydda data i vila.
  - Du skapar en Always Encrypted-nyckel för att kryptera enskilda kolumndata.
  - Always Encrypted-nycklar kan lagras som krypterade i databasmetadata eller lagras i betrodda nyckelarkiv, till exempel Azure Key Vault.
  - Appändringar krävs sannolikt för att använda den här funktionen.
- **Transparent data kryptering (TDE):** Skydda Azure SQL Database med kryptering och dekryptering i real tid av databasen, tillhör ande säkerhets kopior och transaktionsloggfiler i vila.
  - TDE gör att krypteringsaktiviteter kan genomföras utan ändringar på applagret.
  - TDE kan använda krypteringsnycklar från Microsoft, eller så kan du ange egna nycklar med hjälp av Bring Your Own Key-stöd.

**Läs mer:**

- [Läs mer](https://docs.microsoft.com/azure/security/azure-security-disk-encryption-overview) om Azure Disk Encryption för virtuella IaaS-datorer.
- [Aktivera](https://docs.microsoft.com/azure/security/azure-security-disk-encryption-windows) kryptering för virtuella IaaS-datorer för Windows.
- [Läs mer](https://docs.microsoft.com/azure/storage/common/storage-service-encryption) om Azure-kryptering för lagringstjänst för vilande data.
- [Läs](https://docs.microsoft.com/azure/sql-database/sql-database-always-encrypted-azure-key-vault) en översikt över Always Encrypted.
- [Läs mer](https://docs.microsoft.com/azure/sql-database/transparent-data-encryption-azure-sql?view=sql-server-2017) om TDE för Azure SQL Database.
- [Läs mer](https://docs.microsoft.com/azure/sql-database/transparent-data-encryption-byok-azure-sql) om TDE med Bring Your Own Key.

## <a name="best-practice-protect-vms-with-antimalware"></a>Bästa praxis: skydda virtuella datorer med program mot skadlig kod

I synnerhet kanske äldre Azure-migrerade virtuella datorer inte har rätt nivå av program mot skadlig kod installerade. Azure tillhandahåller en kostnadsfri slutpunktslösning som hjälper till att skydda virtuella datorer mot virus, spionprogram och annan skadlig kod.

- Microsoft Antimalware för Azure genererar aviseringar när känd skadlig eller oönskad programvara försöker installera sig själv.
- Det är en lösning med en agent som körs i bakgrunden utan mänsklig inblandning.
- I Azure Security Center kan du enkelt identifiera virtuella datorer som inte har slutpunktsskydd igång och installera Microsoft Antimalware vid behov.

![Program mot skadlig kod för virtuella datorer](./media/migrate-best-practices-security-management/antimalware.png)
*Program mot skadlig kod för virtuella datorer*

**Läs mer:**

- [Läs mer](https://docs.microsoft.com/azure/security/azure-security-antimalware) om Microsoft Antimalware.

## <a name="best-practice-secure-web-apps"></a>Bästa praxis: säkra webbappar

Migrerade webbappar har ett par problem:

- De flesta äldre webbappar har känslig information i konfigurationsfiler. Filer som innehåller sådan information kan innebära säkerhetsproblem när appar säkerhetskopieras eller när appkod checkas in i eller ut från källkontroll.
- När du migrerar webbappar som finns på en virtuell dator flyttar du dessutom sannolikt datorn från ett lokalt nätverk och en brandväggsskyddad miljö till en Internetriktad miljö. Se till att du konfigurerar en lösning som utför samma arbete som dina lokala skyddsresurser.

Azure tillhandahåller ett par lösningar:

- **Azure Key Vault:** I dag vidtar webbappars utvecklare steg för att se till att känslig information inte läcker ut från dessa filer. En metod för att skydda information är att extrahera den från filer och placera den i Azure Key Vault.
  - Du kan använda Key Vault för att centralisera lagringen av apphemligheter och kontrollera deras distribution. Det gör att säkerhetsinformation inte behöver lagras i appfiler.
  - Appar kan på ett säkert sätt komma åt information i valvet med hjälp av URI:er, utan att behöva anpassad kod.
  - Med Azure Key Vault kan du låsa åtkomst via Azure-säkerhetskontroller och sömlöst implementera "uppdatering av nycklar". Microsoft kan inte se eller extrahera dina data.
- **App Service-miljön:** Om en app som du migrerar behöver extra skydd kan du överväga att lägga till en App Service-miljön och brand vägg för webbaserade program för att skydda app-resurserna.
  - Azure App Service-miljön tillhandahåller en fullständigt isolerad och dedikerad miljö där du kan köra App Service-appar som Windows- och Linux-webbappar, Docker-containrar, mobilappar och funktioner.
  - Den är användbar för appar som är mycket storskaliga, kräver isolering och säker nätverksåtkomst eller har hög minnesanvändning.
- **Brand vägg för webbaserade program:** En funktion i Azure Application Gateway som tillhandahåller centraliserat skydd för Web Apps.
  - Den skyddar webbappar utan att kräva ändringar i serverdelskoden.
  - Den skyddar flera webbappar samtidigt bakom en programgateway.
  - En brandvägg för webbaserade program kan övervakas med hjälp av Azure Monitor och integreras i Azure Security Center.

![Skydda webbappar](./media/migrate-best-practices-security-management/web-apps.png)

*Azure Key Vault*

**Läs mer:**

- [Få en översikt](https://docs.microsoft.com/azure/key-vault/key-vault-overview) över Azure Key Vault.
- [Läs mer](https://docs.microsoft.com/azure/application-gateway/waf-overview) om brandvägg för webbaserade program.
- [Få en introduktion](https://docs.microsoft.com/azure/app-service/environment/intro) till App Service-miljöer.
- [Lär dig hur du](https://docs.microsoft.com/azure/key-vault/tutorial-web-application-keyvault) konfigurerar en webbapp för att läsa hemligheter från Key Vault.
- [Läs mer](https://docs.microsoft.com/azure/application-gateway/waf-overview) om brandvägg för webbaserade program.

## <a name="best-practice-review-subscriptions-and-resource-permissions"></a>Bästa praxis: granska prenumerationer och resurs behörigheter

När du migrerar dina arbetsbelastningar och kör dem i Azure flyttas personal med arbetsbelastningsåtkomst runt. Ditt säkerhetsteam bör regelbundet granska åtkomst till din Azure-klientorganisation och -resursgrupper. Azure har erbjudanden för identitetshantering och åtkomstkontrollsäkerhet, inklusive rollbaserad åtkomstkontroll (RBAC) för att ge behörighet att komma åt Azure-resurser.

- RBAC tilldelar åtkomstbehörigheter för säkerhetshuvudkonton. Säkerhetshuvudkonton representerar användare, grupper (en uppsättning användare), tjänsthuvudnamn (identitet som används av appar och tjänster) och hanterade identiteter (en Azure Active Directory-identitet som hanteras automatiskt av Azure).
- RBAC kan tilldela roller till säkerhetshuvudkonton, till exempel ägare, deltagare och läsare, samt rolldefinitioner (en samling behörigheter) som definierar de åtgärder som kan utföras av rollerna.
- RBAC kan också ange omfång som avgör gränsen för en roll. Omfånget kan anges på flera nivåer, inklusive en hanteringsgrupp, prenumeration, resursgrupp eller resurs.
- Se till att administratörer med Azure-åtkomst endast kan komma åt resurser som du vill tillåta. Om de fördefinierade rollerna i Azure inte är tillräckligt detaljerade kan du skapa anpassade roller för att avgränsa och begränsa åtkomstbehörigheter.

![Åtkomstkontroll](./media/migrate-best-practices-security-management/subscription.png)
*Åtkomstkontroll – IAM*

**Läs mer:**

- [Om](https://docs.microsoft.com/azure/role-based-access-control/overview) RBAC.
- [Lär dig](https://docs.microsoft.com/azure/role-based-access-control/role-assignments-portal) att hantera åtkomst med hjälp av RBAC och Azure-portalen.
- [Läs mer](https://docs.microsoft.com/azure/role-based-access-control/custom-roles) om anpassade roller.

## <a name="best-practice-review-audit-and-security-logs"></a>Bästa praxis: granska gransknings-och säkerhets loggar

Azure Active Directory (Azure AD) tillhandahåller aktivitetsloggar som visas i Azure Monitor. Loggarna registrerar de åtgärder som utförs i Azure-klientorganisationen, när de utfördes och vem som utförde dem.

- Spårningsloggar visar historiken för aktiviteter i klientorganisationen. Inloggningsaktivitetsloggar visar vem som utförde aktiviteterna.
- Åtkomst till säkerhetsrapporter är beroende av din Azure AD-licens. I kostnads fri och grundläggande visas en lista över riskfyllda användare och inloggningar. I Premium 1-och Premium 2-versioner får du underliggande händelse information.
- Du kan dirigera aktivitetsloggar till olika slutpunkter för långsiktig kvarhållning och datainsikter.
- Gör det till en vana att granska loggarna eller integrera SIEM-verktygen (Security Information and Event Management) för att automatiskt granska avvikelser. Om du inte använder Premium 1 eller 2 måste du göra mycket analys själv eller med SIEM-systemet. Analys innefattar att söka efter riskfyllda inloggningar och händelser, och andra mönster för användarangrepp.

![Användare och grupper](./media/migrate-best-practices-security-management/azure-ad.png)

*Azure AD-användare och -grupper*

**Läs mer:**

- [Läs mer](https://docs.microsoft.com/azure/active-directory/reports-monitoring/concept-activity-logs-azure-monitor) om Azure AD-aktivitetsloggar i Azure Monitor.
- [Lär dig hur du](https://docs.microsoft.com/azure/active-directory/reports-monitoring/concept-audit-logs) granskar aktivitetsrapporter i Azure AD-portalen.

## <a name="best-practice-evaluate-other-security-features"></a>Bästa praxis: utvärdera andra säkerhetsfunktioner

Azure innehåller andra säkerhetsfunktioner som tillhandahåller avancerade säkerhetsalternativ. Vissa av dessa metodtips kräver tilläggslicenser och premiumalternativ.

- **Implementera administrativa Azure AD-enheter (AU).** Det kan vara svårt att delegera administrativa uppgifter till supportpersonal med bara grundläggande Azure-åtkomstkontroll. Att ge supportpersonal åtkomst att administrera alla grupper i Azure AD kanske inte är den idealiska metoden för organisationens säkerhet. Med AU kan du fördela Azure-resurser i containrar på ett sätt som liknar lokala organisationsenheter (OU). Om du vill använda AU måste AU-administratören ha en premium Azure AD-licens. [Läs mer](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-administrative-units).
- **Använd multifaktorautentisering.** Om du har en premium Azure AD-licens kan du aktivera och tillämpa multifaktorautentisering på dina administratörskonton. Nätfiske är det vanligaste sättet som kontons autentiseringsuppgifter komprometteras. När en obehörig har ett administratörskontos autentiseringsuppgifter finns det inget som hindrar dem från omfattande åtgärder, till exempel att ta bort alla resursgrupper. Du kan tillämpa multifaktorautentisering på flera olika sätt, bland annat med e-post, en autentiseringsapp och textmeddelanden. Som administratör kan du välja det minst störande alternativet. Multifaktorautentisering integreras med hotanalys och principer för villkorlig åtkomst för att slumpmässigt kräva ett svar på en multifaktorautentiseringsutmaning. Läs mer om [säkerhetsvägledning](https://docs.microsoft.com/azure/active-directory/authentication/multi-factor-authentication-security-best-practices) och [hur du konfigurerar multifaktorautentisering](https://docs.microsoft.com/azure/active-directory/authentication/multi-factor-authentication-security-best-practices).
- **Implementera villkorlig åtkomst.** I de flesta små och medelstora organisationer finns Azure-administratörer och supportteamet förmodligen i en enda geografisk region. I det här fallet kommer de flesta inloggningar från samma områden. Om IP-adresserna för dessa platser är relativt statiska är det rimligt att du inte ser administratörsinloggningar utanför dessa områden. Även om en fjärransluten obehörig skulle kompromettera en administratörs autentiseringsuppgifter kan du implementera säkerhetsfunktioner, till exempel villkorlig åtkomst kombinerat med multifaktorautentisering, för att förhindra inloggning från fjärranslutna platser eller från falska platser från slumpmässiga IP-adresser. [Läs mer](https://docs.microsoft.com/azure/active-directory/conditional-access/overview) om villkorlig åtkomst och [granska metodtips](https://docs.microsoft.com/azure/active-directory/conditional-access/best-practices) för villkorlig åtkomst i Azure AD.
- **Granska behörigheter för företagsprogram.** Över tid väljer administratörer Microsoft- och tredjepartslänkar utan att känna till deras inverkan på organisationen. Länkar kan öppna medgivandeskärmar som tilldelar behörigheter till Azure-appar, och kan tillåta åtkomst att läsa Azure AD-data eller till och med fullständig åtkomst att hantera hela Azure-prenumerationen. Du bör regelbundet granska apparna som administratörer och användare har gett åtkomst till Azure-resurser. Se till att dessa appar bara har de behörigheter som krävs. Varje kvartal eller halvår kan du dessutom skicka e-post till användare med en länk till appsidor så att de är medvetna om vilka appar de har gett åtkomst till sina organisationsdata. [Läs mer](https://docs.microsoft.com/azure/active-directory/manage-apps/application-types) om programtyper och [hur du styr](https://docs.microsoft.com/azure/active-directory/manage-apps/remove-user-or-group-access-portal) apptilldelningar i Azure AD.

## <a name="managed-migrated-workloads"></a>Hanterade migrerade arbetsbelastningar

I det här avsnittet rekommenderar vi några metodtips för Azure-hantering, inklusive:

- [Hantera resurser](#best-practice-name-resource-groups): metod tips för Azures resurs grupper och resurser, inklusive Smart namngivning, förhindra oavsiktlig borttagning, hantering av resurs behörigheter och effektiv resurs markering.
- [Använd skisser](#best-practice-implement-blueprints): få en snabb översikt över hur du använder ritningar för att skapa och hantera dina distributions miljöer.
- [Granska arkitekturer](#best-practice-review-azure-reference-architectures): se exempel på Azure-arkitekturer för att lära dig av när du skapar distributioner efter migreringen.
- [Konfigurera hanterings grupper](#best-practice-manage-resources-with-azure-management-groups): om du har flera prenumerationer kan du samla in dem i hanterings grupper och använda styrnings inställningar för dessa grupper.
- [Konfigurera åtkomst principer](#best-practice-deploy-azure-policy): tillämpa efterlevnadsprinciper på dina Azure-resurser.
- [Implementera en BCDR-strategi](#best-practice-implement-a-bcdr-strategy): samla in en strategi för affärs kontinuitet och haveri beredskap (BCDR) för att skydda data, din miljö och få resurser igång när avbrott uppstår.
- [Hantera virtuella datorer](#best-practice-use-managed-disks-and-availability-sets): gruppera virtuella datorer i tillgänglighets grupper för återhämtning och hög tillgänglighet. Använd hanterade diskar för enkel disk- och lagringshantering för virtuella datorer.
- [Övervaka resursanvändning](#best-practice-monitor-resource-usage-and-performance): Aktivera diagnostikloggning för Azure-resurser, skapa aviseringar och spel böcker för proaktiv fel sökning och Använd Azure-instrumentpanelen för en enhetlig vy över din distributions hälsa och status.
- [Hantera support och uppdateringar](#best-practice-manage-updates): förstå ditt support avtal för Azure och hur du implementerar det, få bästa praxis för att hålla virtuella datorer uppdaterade och placera processer i stället för ändrings hantering.

## <a name="best-practice-name-resource-groups"></a>Bästa praxis: namnge resurs grupper

Om resursgrupperna har beskrivande namn som administratörer och medlemmar i supportteamet enkelt kan identifiera och navigera förbättras produktiviteten och effektiviteten avsevärt.

- Vi rekommenderar att du följer Azures namngivningskonventioner.
- Om du synkroniserar din lokala Active Directory till Azure AD med hjälp av Azure AD Connect bör du överväga att matcha namnen på säkerhetsgrupper lokalt mot namnen på resursgrupper i Azure.

![Namngivning](./media/migrate-best-practices-security-management/naming.png)

*Namngivning av resursgrupper*

**Läs mer:**

- [Läs mer](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions) om namngivningskonventioner.

## <a name="best-practice-implement-delete-locks-for-resource-groups"></a>Bästa praxis: implementera ta bort lås för resurs grupper

Det sista du behöver är att en resursgrupp försvinner eftersom den tagits bort av misstag. Vi rekommenderar att du implementerar borttagningslås så att det inte sker.

![Borttagningslås](./media/migrate-best-practices-security-management/locks.png)

*Borttagningslås*

**Läs mer:**

- [Läs mer](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-lock-resources) om att låsa resurser för att förhindra oväntade ändringar.

## <a name="best-practice-understand-resource-access-permissions"></a>Bästa praxis: förstå resurs åtkomst behörigheter

En prenumerationsägare har åtkomst till alla resursgrupper och resurser i prenumerationen.

- Var försiktig med att ge personer den här värdefulla tilldelningen. Det är viktigt att förstå konsekvenserna av dessa typer av behörigheter för att hålla miljön säker och stabil.
- Se till att placera resurser i lämpliga resursgrupper:
  - Matcha resurser med liknande livscykel tillsammans. Du bör helst inte behöva flytta en resurs när du behöver ta bort en hel resursgrupp.
  - Resurser som rör en funktion eller arbetsbelastning bör placeras tillsammans för förenklad hantering.

**Läs mer:**

- [Läs mer](https://azure.microsoft.com/blog/organizing-subscriptions-and-resource-groups-within-the-enterprise) om att organisera prenumerationer och resursgrupper.

## <a name="best-practice-tag-resources-effectively"></a>Bästa praxis: tagga resurser effektivt

Om du bara använder ett resursgruppsnamn som är relaterat till resurser får du ofta inte tillräckligt med metadata för effektiv implementering av mekanismer som intern fakturering eller hantering i en prenumeration.

- Som ett metodtips bör du använda Azure-taggar för att lägga till användbara metadata som kan efterfrågas och rapporteras.
- Taggar ger ett sätt att organisera resurser logiskt med egenskaper som du definierar. Taggar kan tillämpas direkt på resursgrupper eller resurser.
- Taggar kan tillämpas på en resursgrupp eller på enskilda resurser. En resursgrupps taggar ärvs inte av resurserna i gruppen.
- Du kan automatisera taggning med PowerShell eller Azure Automation, eller tagga enskilda grupper och resurser. Taggningsmetod eller självbetjäning. Om du har ett system för begäranden och ändringshantering kan du enkelt använda informationen i begäran för att fylla i företagsspecifika resurstaggar.

![Taggning](./media/migrate-best-practices-security-management/tagging.png)
*Taggning*

**Läs mer:**

- [Läs mer](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags) om taggning och taggbegränsningar.
- [Granska](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags#powershell) PowerShell- och CLI-exempel för att konfigurera taggning och tillämpa taggar från en resursgrupp på dess resurser.
- [Läs](https://www.azurefieldnotes.com/2016/07/18/azure-resource-tagging-best-practices) metodtips om Azure-taggning.

## <a name="best-practice-implement-blueprints"></a>Bästa praxis: implementera skisser

Precis som en skiss tillåter tekniker och arkitekter att skissa designparametrarna för ett projekt kan Azure Blueprints göra det möjligt för molnarkitekter och centrala IT-grupper att definiera en upprepningsbar uppsättning med Azure-resurser som implementerar och tillämpar en organisations standarder, mönster och krav. Med hjälp av Azure Blueprints kan utvecklingsteam snabbt skapa nya miljöer som uppfyller organisationens krav på efterlevnad och som har en uppsättning inbyggda komponenter, till exempel nätverk, för att påskynda utveckling och leverans.

- Använd skisser för att samordna distributionen av resursgrupper, Azure Resource Manager-mallar och princip- och rolltilldelningar.
- Skisser lagras i en globalt distribuerad Azure Cosmos DB. Skissobjekt replikeras till flera Azure-regioner. Replikering ger låg svarstid, hög tillgänglighet och konsekvent åtkomst till skisser, oavsett vilken region en skiss distribuerar resurser till.

**Läs mer:**

- [Läs mer](https://docs.microsoft.com/azure/governance/blueprints/overview) om skisser.
- [Granska](https://azure.microsoft.com/blog/customizing-azure-blueprints-to-accelerate-ai-in-healthcare) ett skissexempel som används för att påskynda AI inom hälsovård.

## <a name="best-practice-review-azure-reference-architectures"></a>Bästa praxis: granska Azure Reference arkitekturer

Det kan kännas överväldigande att skapa säkra, skalbara och hanterbara arbetsbelastningar i Azure. Med kontinuerliga ändringar kan det vara svårt att hålla reda på olika funktioner för en optimal miljö. Att ha en referens att lära dig av kan vara till hjälp när du utformar och migrerar dina arbetsbelastningar. Azure och Azure-partner har skapat flera exempel på referensarkitekturer för olika typer av miljöer. Dessa exempel är utformade för att ge idéer som du kan lära dig av och bygga vidare på.

Referensarkitekturer ordnas efter scenario. De innehåller bästa praxis och råd om hantering, tillgänglighet, skalbarhet och säkerhet.
Azure App Service-miljön tillhandahåller en fullständigt isolerad och dedikerad miljö där du kan köra App Service-appar, inklusive Windows- och Linux-webbappar, Docker-containrar, mobilappar och funktioner. App Service lägger till kraften hos Azure i ditt program, med säkerhet, belastningsutjämning, automatisk skalning och automatiserad hantering. Du kan även dra nytta av dess DevOps-funktioner, till exempel kontinuerlig distribution från Azure DevOps och GitHub, pakethantering, mellanlagringsmiljöer, anpassade domäner och SSL-certifikat. App Service är användbart för appar som behöver isolering och säker nätverksåtkomst, och de som använder stora mängder minne och andra resurser som behöver skalas.

**Läs mer:**

- [Läs mer](https://docs.microsoft.com/azure/architecture/reference-architectures) om Azure-referensarkitekturer.
- [Granska](https://docs.microsoft.com/azure/architecture/example-scenario) Azures exempelscenarier.

## <a name="best-practice-manage-resources-with-azure-management-groups"></a>Bästa praxis: hantera resurser med Azures hanterings grupper

Om din organisation har flera prenumerationer behöver du hantera åtkomst, principer och efterlevnad för dem. Med Azures hanteringsgrupper får du en hanteringsnivå över prenumerationsnivån.

- Du kan ordna prenumerationerna i containrar som kallas hanteringsgrupper och tillämpa styrningsvillkor för dem.
- Alla prenumerationer i en hanteringsgrupp ärver automatiskt hanteringsgruppens villkor.
- Hanteringsgrupper ger storskalig hantering i företagsklass, oavsett vilken typ av prenumeration du har.
- Du kan till exempel tillämpa en hanteringsgruppsprincip som begränsar regionerna där virtuella datorer kan skapas. Den här principen tillämpas sedan för alla hanteringsgrupper, prenumerationer och resurser under hanteringsgruppen.
- Du kan skapa en flexibel struktur för hanteringsgrupper och prenumerationer, för att organisera dina resurser i en hierarki för enhetlig princip- och åtkomsthantering.

Följande diagram visar ett exempel på att skapa en hierarki för styrning med hjälp av hanteringsgrupper.

![Hanteringsgrupper](./media/migrate-best-practices-security-management/management-groups.png)
*Hanteringsgrupper*

**Läs mer:**

- [Läs mer](https://docs.microsoft.com/azure/governance/management-groups/index) om att organisera resurser i hanteringsgrupper.

## <a name="best-practice-deploy-azure-policy"></a>Bästa praxis: Distribuera Azure Policy

Azure Policy är en tjänst i Azure som används för att skapa, tilldela och hantera principer.

- Principer tillämpar olika regler och effekter på dina resurser så att resurserna efterlever dina företagsstandarder och serviceavtal.
- Azure Policy utvärderar resurserna och söker efter sådana som inte följer principerna.
- Du kan till exempel skapa en princip som endast tillåter en specifik SKU-storlek för virtuella datorer i miljön. Azure Policy utvärderar inställningen när den skapar och uppdaterar resurser, och när den söker efter befintliga resurser.
- Azure innehåller några inbyggda principer som du kan tilldela, eller så kan du skapa egna.

![Azure Policy](./media/migrate-best-practices-security-management/policy.png)
*Azure Policy*

**Läs mer:**

- [Få en översikt](https://docs.microsoft.com/azure/governance/policy/overview) över Azure Policy.
- [Läs mer](https://docs.microsoft.com/azure/governance/policy/tutorials/create-and-manage) om att skapa och hantera principer för att säkerställa efterlevnad.

## <a name="best-practice-implement-a-bcdr-strategy"></a>Bästa praxis: implementera en BCDR-strategi

Planering av BCDR (affärskontinuitet och haveriberedskap) är en viktig övning som du bör utföra som en del i planeringsprocessen för Azure-migrering. I juridiska termer kan dina kontrakt innehålla en force majeure-paragraf som eliminerar skyldigheter på grund av en större kraft, till exempel orkaner eller jordbävningar. Men du har också skyldigheter som rör din förmåga att se till att tjänsterna fortsätter att köras, och återställs när det behövs, vid ett haveri. Din förmåga att göra detta kan avgöra ditt företags framtid.

BCDR-strategin måste i huvudsak omfatta:

- **Säkerhets kopiering av data:** Se till att dina data är säkra så att du enkelt kan återställa dem om avbrott uppstår.
- **Haveri beredskap:** Hur du håller dina appar elastiska och tillgängliga om avbrott uppstår.

### <a name="set-up-bcdr"></a>Konfigurera BCDR

När du migrerar till Azure är det viktigt att förstå att även om Azure-plattformen tillhandahåller dessa inbyggda återhämtningsfunktioner måste du utforma Azure-distributionen för att dra nytta av Azure-funktioner och -tjänster som tillhandahåller hög tillgänglighet, haveriberedskap och säkerhetskopiering.

- Din BCDR-lösning beror på företagets mål och påverkas av din strategi för Azure-distributionen. IaaS- (infrastruktur som en tjänst) och PaaS-distributioner (plattform som en tjänst) innebär olika utmaningar för BCDR.
- När BCDR-lösningarna är på plats bör de testas regelbundet för att kontrollera att strategin fortfarande är användbar.

### <a name="back-up-an-iaas-deployment"></a>Säkerhetskopiera en IaaS-distribution

I de flesta fall tas en lokal arbetsbelastning ur bruk efter migreringen och din lokala strategi för säkerhetskopiering av data måste utökas eller ersättas. Om du migrerar hela datacentret till Azure måste du utforma och implementera en fullständig säkerhetskopieringslösning med hjälp av Azure-tekniker eller integrerade tredjepartslösningar.

För arbetsbelastningar som körs på virtuella Azure IaaS-datorer bör du fundera på följande säkerhetskopieringslösningar:

- **Azure Backup:** Tillhandahåller programkonsekventa säkerhets kopieringar för virtuella Azure Windows-och Linux-datorer.
- **Lagrings ögonblicks bilder:** Tar ögonblicks bilder av Blob Storage.

#### <a name="azure-backup"></a>Azure Backup

Med Azure Backup skapas dataåterställningspunkter som lagras i Azure Storage. Azure Backup kan säkerhetskopiera Azure-VM-diskar och Azure Files (förhandsversion). Azure Files tillhandahåller filresurser i molnet som kan nås via SMB.

Du kan använda Azure Backup för att säkerhetskopiera virtuella datorer på ett par olika sätt.

- **Direkt säkerhetskopiering från VM-inställningar.** Du kan säkerhetskopiera virtuella datorer med Azure Backup direkt från alternativen för virtuella datorer i Azure-portalen. Du kan säkerhetskopiera den virtuella datorn en gång per dag och du kan återställa den virtuella dator disken efter behov. Azure Backup tar appmedvetna dataögonblicksbilder (VSS) och ingen agent installeras på den virtuella datorn.
- **Direkt säkerhetskopiering i ett Recovery Services-valv.** Du kan säkerhetskopiera virtuella IaaS-datorer genom att distribuera ett Azure Backup Recovery Services-valv. Det ger en enda plats för att spåra och hantera säkerhetskopior samt detaljerade alternativ för säkerhetskopiering och återställning. Säkerhetskopieringen sker upp till tre gånger per dag, på fil-/mappnivå. Den är inte appmedveten och Linux stöds inte. Installera MARS-agenten (Microsoft Azure Recovery Services) på varje virtuell dator som du vill säkerhetskopiera med den här metoden.
- **Skydda den virtuella datorn med Azure Backup Server.** Azure Backup Server tillhandahålls utan kostnad med Azure Backup. Den virtuella datorn säkerhetskopieras till lokal Azure Backup Server-lagring. Sedan säkerhetskopierar du Azure Backup Server till Azure i ett valv. Säkerhetskopieringen är appmedveten, med fullständig kornighet för säkerhetskopieringsfrekvens och -kvarhållning. Du kan säkerhetskopiera på appnivå, till exempel genom att säkerhetskopiera SQL Server eller SharePoint.

Av säkerhetsskäl krypterar Azure Backup rörliga data med AES 256 och skickar dem via HTTPS till Azure. Säkerhetskopierade vilande data i Azure krypteras med hjälp av [kryptering för lagringstjänst (SSE)](https://docs.microsoft.com/azure/storage/common/storage-service-encryption?toc=%2fazure%2fstorage%2fqueues%2ftoc.json), och data för överföring och lagring.

![Azure Backup](./media/migrate-best-practices-security-management/iaas-backup.png)
*Azure Backup*

**Läs mer:**

- [Läs mer](https://docs.microsoft.com/azure/backup/backup-introduction-to-azure-backup) om olika typer av säkerhetskopior.
- [Planera en infrastruktur för säkerhetskopiering](https://docs.microsoft.com/azure/backup/backup-azure-vms-introduction) för virtuella Azure-datorer.

#### <a name="storage-snapshots"></a>Ögonblicksbilder för lagring

Virtuella Azure-datorer lagras som sidblobbar i Azure Storage.

- Ögonblicksbilder registrerar blobtillståndet vid en viss tidpunkt.
- Som en alternativ säkerhetskopieringsmetod för Azure-VM-diskar kan du ta en ögonblicksbild av lagringsblobbar och kopiera dem till ett annat lagringskonto.
- Du kan kopiera en hel blob eller använda en inkrementell ögonblicksbildskopia för att bara kopiera deltaändringar och minska lagringsutrymmet.
- Som en extra försiktighetsåtgärd kan du aktivera mjuk borttagning för bloblagringskonton. När den här funktionen är aktiverad markeras en blob som tas bort för borttagning men rensas inte omedelbart. Under övergångsperioden kan blobben återställas.

**Läs mer:**

- [Läs mer](https://docs.microsoft.com/azure/storage/blobs/storage-blobs-introduction) om Azure Blob Storage.
- [Lär dig hur du](https://docs.microsoft.com/azure/storage/blobs/storage-blob-snapshots) skapar en blobögonblicksbild.
- [Granska ett exempelscenario](https://azure.microsoft.com/blog/microsoft-azure-block-blob-storage-backup) för säkerhetskopiering av bloblagring.
- [Läs mer](https://docs.microsoft.com/azure/storage/blobs/storage-blob-soft-delete) om mjuk borttagning.
- [Haveriberedskap och forcerad redundans (förhandsversion) i Azure Storage](https://docs.microsoft.com/azure/storage/common/storage-disaster-recovery-guidance?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)

#### <a name="third-party-backup"></a>Säkerhetskopiering från tredje part

Dessutom kan du använda tredjepartslösningar för att säkerhetskopiera virtuella Azure-datorer och lagringscontainrar till lokal lagring eller andra molnleverantörer. [Läs mer](https://azuremarketplace.microsoft.com/marketplace/apps?search=backup&page=1) om säkerhetskopieringslösningar på Azure Marketplace.

### <a name="set-up-disaster-recovery-for-iaas-apps"></a>Konfigurera haveriberedskap för IaaS-appar

Förutom att skydda data måste BCDR-planeringen ta hänsyn till hur appar och arbetsbelastningar ska förbli tillgängliga i händelse av ett haveri. För arbetsbelastningar som körs på virtuella Azure IaaS-datorer och Azure-lagring bör du fundera på följande lösningar:

#### <a name="azure-site-recovery"></a>Azure Site Recovery

Azure Site Recovery är den primära Azure-tjänsten för att se till att virtuella Azure-datorer kan tas online och VM-appar kan göras tillgängliga vid avbrott.

Site Recovery replikerar virtuella datorer från en primär till en sekundär Azure-region. När ett haveri inträffar redundansväxlar du virtuella datorer från den primära regionen och fortsätter att komma åt dem som vanligt i den sekundära regionen. När driften återgår till det normala kan du återställa virtuella datorer till den primära regionen.

![Azure Site Recovery](./media/migrate-best-practices-security-management/site-recovery.png)

*Site Recovery*

**Läs mer:**

- [Granska](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-disaster-recovery-guidance) haveriberedskapsscenarier för virtuella Azure-datorer.
- [Lär dig hur du](https://docs.microsoft.com/azure/site-recovery/azure-to-azure-replicate-after-migration) konfigurerar haveriberedskap för en virtuell Azure-dator efter migreringen.

## <a name="best-practice-use-managed-disks-and-availability-sets"></a>Bästa praxis: Använd hanterade diskar och tillgänglighets uppsättningar

Azure använder tillgänglighetsuppsättningar för att gruppera virtuella datorer logiskt och för att isolera virtuella datorer i en uppsättning från andra resurser. Virtuella datorer i en tillgänglighetsuppsättning sprids över flera feldomäner med separata undersystem, för att skydda mot lokala fel, och de sprids också över flera uppdateringsdomäner så att inte alla virtuella datorer i en uppsättning startas om på samma gång.

Hanterade Azure-diskar förenklar diskhantering för virtuella Azure IaaS-datorer genom att hantera de lagringskonton som är associerade med VM-diskarna.

- Vi rekommenderar att du använder hanterade diskar där det är möjligt. Du behöver bara ange vilken typ av lagring du vill använda och vilken diskstorlek du behöver och sedan skapar och hanterar Azure disken, i bakgrunden.
- Du kan konvertera befintliga diskar till hanterade.
- Du bör skapa virtuella datorer i tillgänglighetsuppsättningar för hög återhämtning och tillgänglighet. Vid planerade eller oplanerade avbrott säkerställer tillgänglighetsuppsättningar att minst en av dina virtuella datorer i uppsättningen fortfarande är tillgänglig.

![Hanterade diskar](./media/migrate-best-practices-security-management/managed-disks.png)

*Hanterade diskar*

**Läs mer:**

- [Få en översikt](https://docs.microsoft.com/azure/virtual-machines/windows/managed-disks-overview) över hanterade diskar.
- [Läs mer](https://docs.microsoft.com/azure/virtual-machines/windows/convert-unmanaged-to-managed-disks) om att konvertera diskar till hanterade.
- [Lär dig hur du](https://docs.microsoft.com/azure/virtual-machines/windows/manage-availability) hanterar tillgängligheten för virtuella Windows-datorer i Azure.

## <a name="best-practice-monitor-resource-usage-and-performance"></a>Bästa praxis: övervaka resursanvändning och prestanda

Du kanske har flyttat dina arbetsbelastningar till Azure för dess omfattande skalningsfunktioner. Men om du flyttar din arbetsbelastning innebär det inte att Azure automatiskt implementerar skalning utan åtgärd från dig. Som exempel:

- Om din marknadsföringsorganisation kör en ny TV-annons som genererar 300 % mer trafik kan det orsaka problem med webbplatstillgänglighet. Arbetsbelastningen du migrerade nyligen kan nå tilldelade gränser och krascha.
- Ett annat exempel kan vara en DDoS-attack (Distributed Denial-of-Service) på den migrerade arbetsbelastningen. I det här fallet kanske du inte vill skala, utan förhindra att attackernas källa når dina resurser.

Dessa två fall har olika lösningar, men för båda behöver du en insikt om vad som händer med användnings- och prestandaövervakning.

- Azure Monitor kan visa dessa mått och ge svar med aviseringar, automatisk skalning, händelsehubbar, logikappar med mera.
- Förutom Azure-övervakning kan du integrera ditt SIEM-program från tredje part för att övervaka gransknings- och prestandahändelser i Azure-loggarna.

![Azure Monitor](./media/migrate-best-practices-security-management/monitor.png)
*Azure Monitor*

**Läs mer:**

- [Läs mer](https://docs.microsoft.com/azure/azure-monitor/overview) om Azure Monitor.
- [Få metodtips](https://docs.microsoft.com/azure/architecture/best-practices/monitoring) om övervakning och diagnostik.
- [Läs mer](https://docs.microsoft.com/azure/architecture/best-practices/auto-scaling) om autoskalning.
- [Lär dig hur du](https://docs.microsoft.com/azure/security-center/security-center-export-data-to-siem) dirigerar Azure-data till ett SIEM-verktyg.

## <a name="best-practice-enable-diagnostic-logging"></a>Bästa praxis: Aktivera diagnostisk loggning

Azure-resurser genererar ett antal loggningsmått och telemetridata.

- Som standard är inte diagnostisk loggning aktiverad för de flesta resurstyper.
- Genom att aktivera diagnostisk loggning för dina resurser kan du efterfråga loggningsdata och skapa aviseringar och spelböcker baserat på det.
- När du aktiverar diagnostisk loggning har varje resurs en specifik uppsättning kategorier. Du väljer en eller flera loggningskategorier och en plats för loggdata. Loggar kan skickas till ett lagringskonto, en händelsehubb eller till Azure Monitor-loggar.

![Diagnostisk loggning](./media/migrate-best-practices-security-management/diagnostics.png)
*Diagnostisk loggning*

**Läs mer:**

- [Läs mer](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs) om att samla in och använda loggdata.
- [Läs vad som stöds](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-diagnostic-logs-schema) för diagnostisk loggning.

## <a name="best-practice-set-up-alerts-and-playbooks"></a>Bästa praxis: Konfigurera aviseringar och spel böcker

Med diagnostisk loggning aktiverad för Azure-resurser kan du börja använda loggningsdata för att skapa anpassade aviseringar.

- Med aviseringar meddelas du proaktivt när villkor hittas i dina övervakningsdata. Sedan kan du åtgärda problem innan systemanvändarna märker dem. Du kan avisera om till exempel måttvärden, loggsökningsfrågor, aktivitetslogghändelser, plattformshälsa och webbplatstillgänglighet.
- När aviseringar utlöses kan du köra en logikappsspelbok. En spelbok hjälper dig att automatisera och samordna ett svar på en specifik avisering. Spelböcker baseras på Azure-logikappar. Du kan använda logikappsmallar för att skapa spelböcker, eller skapa egna.
- Som ett enkelt exempel kan du skapa en avisering som utlöses när en portsökning sker mot en nätverkssäkerhetsgrupp. Du kan konfigurera en spelbok som kör och låser sökningskällans IP-adress.
- Ett annat exempel kan vara en app med en minnesläcka. När minnesanvändningen når en viss punkt kan en spelbok återvinna processen.

![Aviseringar](./media/migrate-best-practices-security-management/alerts.png)
*Aviseringar*

**Läs mer:**

- [Läs mer](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-alerts) om aviseringar.
- [Läs mer](https://docs.microsoft.com/azure/security-center/security-center-playbooks) om säkerhetsspelböcker som svarar på Security Center-aviseringar.

## <a name="best-practice-use-the-azure-dashboard"></a>Bästa praxis: använda Azure-instrumentpanelen

Azure-portalen är en webbaserad enhetlig konsol som du kan använda för att skapa, hantera och övervaka allt från enkla webbappar till komplexa molnprogram. Den innehåller en anpassningsbar instrumentpanel och hjälpmedelsalternativ.

- Du kan skapa flera instrumentpaneler och dela dem med andra som har åtkomst till dina Azure-prenumerationer.
- Med den här delade modellen har ditt team insyn i Azure-miljön, så att de kan vara proaktiva när de hanterar system i molnet.

![Azure-instrumentpanel](./media/migrate-best-practices-security-management/dashboard.png)
*Azure-instrumentpanel*

**Läs mer:**

- [Lär dig hur du](https://docs.microsoft.com/azure/azure-portal/azure-portal-dashboards) skapar en instrumentpanel.
- [Läs mer](https://docs.microsoft.com/azure/azure-portal/azure-portal-dashboards-structure) om instrumentpanelsstruktur.

## <a name="best-practice-understand-support-plans"></a>Bästa praxis: förstå support avtal

Vid något tillfälle måste du samarbeta med din supportpersonal eller Microsofts supportpersonal. Det är viktigt att ha en uppsättning principer och procedurer för support vid scenarier som haveriberedskap. Dessutom bör dina administratörer och supportpersonal utbildas i att implementera dessa principer.

- Om ett problem med Azure-tjänsten mot förmodan påverkar din arbetsbelastning bör administratörer veta hur de skickar in en supportbegäran till Microsoft på det lämpligaste och effektivaste sättet.
- Bekanta dig med de olika supportplanerna som erbjuds för Azure. De sträcker sig från svarstider som är dedikerade för Developer-instanser till Premier Support med en svarstid på mindre än 15 minuter.

![Supportplaner](./media/migrate-best-practices-security-management/support.png)
*Supportplaner*

**Läs mer:**

- [Få en översikt](https://azure.microsoft.com/support/options) över Azure-supportplaner.
- [Läs mer](https://azure.microsoft.com/support/legal/sla) om serviceavtal (SLA).

## <a name="best-practice-manage-updates"></a>Bästa praxis: hantera uppdateringar

Det är en enorm uppgift att se till att virtuella Azure-datorer är uppdaterade med de senaste operativsystems- och programuppdateringarna. Möjligheten att kontrollera alla virtuella datorer, för att ta reda på vilka uppdateringar de behöver och automatiskt skicka dessa uppdateringar, är mycket värdefull.

- Du kan använda Uppdateringshantering i Azure Automation för att hantera operativsystemsuppdateringar för datorer som kör Windows- och Linux-datorer som distribueras i Azure, lokalt och i andra molnleverantörer.
- Använd Uppdateringshantering för att snabbt bedöma status för tillgängliga uppdateringar på alla agentdatorer och hantera installationen av uppdateringar.
- Du kan aktivera Uppdateringshantering för virtuella datorer direkt via ett Azure Automation-konto. Du kan också uppdatera en enskild virtuell dator från VM-sidan i Azure-portalen.
- Dessutom kan virtuella Azure-datorer registreras med System Center Configuration Manager. Du kan sedan migrera Configuration Manager-arbetsbelastningen till Azure och utföra rapportering och programuppdateringar från ett enda webbgränssnitt.

![VM-uppdateringar](./media/migrate-best-practices-security-management/updates.png)
*Uppdateringar*

**Läs mer:**

- [Läs mer](https://docs.microsoft.com/azure/automation/automation-update-management) om uppdateringshantering i Azure.
- [Lär dig hur du](https://docs.microsoft.com/azure/automation/oms-solution-updatemgmt-sccmintegration) integrerar Configuration Manager med uppdateringshantering.
- [Vanliga frågor och svar](https://docs.microsoft.com/sccm/core/understand/configuration-manager-on-azure) om Configuration Manager i Azure.

## <a name="implement-a-change-management-process"></a>Implementera en ändringshanteringsprocess

Precis som med andra produktionssystem kan alla typer av ändringar påverka din miljö. En ändringshanteringsprocess som kräver att begäranden skickas in för att göra ändringar i produktionssystem är ett värdefullt tillägg i den migrerade miljön.

- Du kan ta fram metodtipsramverk för ändringshantering för att öka medvetenheten hos administratörer och supportpersonal.
- Du kan använda Azure Automation för hjälp med konfigurationshantering och ändringsspårning för migrerade arbetsflöden.
- När du tillämpar ändringshanteringsprocessen kan du använda spårningsloggar för att länka Azure-ändringsloggar till förmodat (eller inte) befintliga ändringsbegäranden. Så om du ser att en ändring görs utan motsvarande ändringsbegäran kan du undersöka vad som gått fel i processen.

Azure har en lösning för ändringsspårning i Azure Automation:

- Lösningen spårar ändringar i Windows- och Linux-programvara och -filer, Windows-registernycklar, Windows-tjänster och Linux-daemon.
- Ändringar på övervakade servrar skickas till Azure Monitor-tjänsten i molnet för bearbetning.
- Logik tillämpas på mottagna data och molntjänsten registrerar data.
- På instrumentpanelen Ändringsspårning kan du enkelt se vilka ändringar som gjorts i serverinfrastrukturen.

![Ändringshantering](./media/migrate-best-practices-security-management/change.png)
*Ändringshantering*

**Läs mer:**

- [Läs mer](https://docs.microsoft.com/azure/automation/automation-change-tracking) om ändringsspårning.
- [Läs mer](https://docs.microsoft.com/azure/automation/automation-intro) om Azure Automation-funktioner.

## <a name="next-steps"></a>Nästa steg

Läs andra metodtips:

- [Metodtips](./migrate-best-practices-networking.md) för nätverk efter migrering.
- [Metodtips](./migrate-best-practices-costs.md) för säkerhet och hantering efter migrering.
