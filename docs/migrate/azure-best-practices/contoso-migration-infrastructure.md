---
title: Distribuera en migreringsinfrastruktur
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Se hur Contoso konfigurerar en Azure-infrastruktur för migrering till Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/1/2018
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
services: azure-migrate
ms.openlocfilehash: c367bb500cf9271603cab07ac07649607bfc04a4
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/16/2019
ms.locfileid: "71024347"
---
# <a name="deploy-a-migration-infrastructure"></a>Distribuera en migreringsinfrastruktur

Den här artikeln visar hur det fiktiva företaget Contoso förbereder den lokala infrastrukturen för migrering, konfigurerar en Azure-infrastruktur inför migreringen och kör verksamheten i en hybridmiljö. Tänk på följande när du använder det här exemplet för att planera dina egna åtgärder för infrastrukturmigrering:

- Den tillhandahållna exempelarkitekturen gäller endast för Contoso. Se över din egen organisations affärsbehov, struktur och tekniska krav när du fattar viktiga infrastruktursbeslut om prenumerationsdesign eller nätverksarkitektur.
- Huruvida du behöver alla delarna som beskrivs i den här artikeln beror på din strategi för migrering. Om du till exempel endast skapar molnbaserade appar i Azure kan du behöva en mindre komplex nätverksstruktur.

## <a name="overview"></a>Översikt

Innan Contoso kan migrera till Azure är det viktigt att förbereda en Azure-infrastruktur. I allmänhet finns det sex breda områden som Contoso behöver tänka på:

> [!div class="checklist"]
>
> - **Steg 1: Azure-prenumerationer.** Hur planerar Contoso att köpa Azure och interagera med Azure-plattformen och -tjänsterna?
> - **Steg 2: Hybrididentitet.** Hur kommer Contoso hantera och kontrollera åtkomsten till lokala resurser och Azure-resurser efter migreringen? Hur utökar eller flyttar Contoso identitetshanteringen till molnet?
> - **Steg 3: Haveriberedskap och återhämtning.** Hur ser Contoso till att dess appar och infrastruktur är motståndskraftiga om avbrott och haverier uppstår?
> - **Steg 4: Nätverk.** Hur ska Contoso utforma en nätverksinfrastruktur och upprätta anslutningar mellan det lokala datacentret och Azure?
> - **Steg 5: Säkerhet**. Hur skyddar de hybrid-/Azure-distributionen?
> - **Steg 6: Styrning.** Hur kommer Contoso anpassa distributionen till säkerhets- och styrningskrav?

## <a name="before-you-start"></a>Innan du börjar

Innan vi börjar titta på infrastrukturen kanske du vill läsa mer om de Azure-funktioner som vi diskuterar i den här artikeln:

- Det finns flera alternativ för att köpa Azure-åtkomst, inklusive ”betala per användning”, Enterprise-avtal (EA), öppen licensiering från Microsoft-återförsäljare eller från Microsoft-partner (kallas även molnlösningsleverantörer). Läs om [köpalternativ](https://azure.microsoft.com/pricing/purchase-options)och hur [Azure-prenumerationer organiseras](https://azure.microsoft.com/blog/organizing-subscriptions-and-resource-groups-within-the-enterprise).
- Få en översikt över[Identitets- och åtkomsthantering](https://www.microsoft.com/trustcenter/security/identity) med Azure. Läs särskilt om [Azure AD och att utöka lokala Active Directory till molnet](https://docs.microsoft.com/azure/active-directory/identity-fundamentals). Det finns en användbar nedladdningsbar e-bok om [Identitets-och åtkomst hantering (IAM)](https://azure.microsoft.com/resources/hybrid-cloud-identity) i en hybridmiljö.
- Azure tillhandahåller en robust nätverksinfrastruktur med alternativ för hybridanslutning. Få en översikt över [nätverk och nätverksåtkomstkontroll](https://docs.microsoft.com/azure/security/security-network-overview).
- Få en introduktion till [Azure-säkerhet](https://docs.microsoft.com/azure/security/azure-security) och läs om hur du utformar en [styrningsplan](https://docs.microsoft.com/azure/security/governance-in-azure).

## <a name="on-premises-architecture"></a>Lokal arkitektur

Här är ett diagram som visar Contosos aktuella lokala infrastruktur.

 ![Contosos architecture](./media/contoso-migration-infrastructure/contoso-architecture.png)

- Contoso har ett huvudsakligt datacenter finns i New York i östra USA.
- Det finns ytterligare tre lokala avdelningar i USA.
- Huvuddatacentret är anslutet till Internet med en Metro Ethernet-anslutning för fiber (500 Mbit/s).
- Varje avdelning ansluts lokalt till Internet med hjälp av anslutningar i företagsklass med IPsec VPN-tunnlar tillbaka till huvuddatacentret. Konfigurationen innebär att hela nätverket är permanent anslutet och optimerar Internet-anslutningen.
- Huvuddatacentret är helt virtualiserat med VMware. Contoso har två ESXi 6.5-virtualiseringsvärdar som hanteras av vCenter Server 6.5.
- Contoso använder Active Directory för identitetshantering och DNS-servrar i det interna nätverket.
- Domänkontrollanterna i datacentret körs på virtuella VMware-datorer. Domänkontrollanterna på de lokala avdelningarna körs på fysiska servrar.

## <a name="step-1-buy-and-subscribe-to-azure"></a>Steg 1: Köp och prenumerera på Azure

Contoso måste lista ut hur man köper Azure, hur man utformar prenumerationer och hur man licensierar tjänster och resurser.

### <a name="buy-azure"></a>Köpa Azure

Contoso satsar på med ett [Enterprise-avtal (EA).](https://azure.microsoft.com/pricing/enterprise-agreement) Detta innebär att Contoso accepterar ett ekonomiskt åtagande gentemot Azure som ger Contoso stora fördelar, inklusive flexibla faktureringsalternativ och optimerad prissättning.

- Contoso uppskattade sina årliga kostnader för Azure. När avtalet undertecknades betalade Contoso för hela det första året.
- Contoso måste använda upp detta belopp innan året är slut för att inte gå miste om värdet av investeringen.
- Om Contoso av någon anledning överskrider sitt åtagande och lägger till mer kommer Microsoft att debitera dem för mellanskillnaden.
- Alla kostnader som uppstår utöver åtagandet kommer att ha samma pris som kostnaderna i Contosos avtal. Att överskrida åtagandet medför inga tilläggsavgifter.

### <a name="manage-subscriptions"></a>Hantera prenumerationer

När Contoso har betalat för Azure måste de bestämma hur de ska hantera Azure-prenumerationer. Contoso har ett EA och därmed finns det ingen gräns för hur många Azure-prenumerationer de kan konfigurera.

- En Azure Enterprise-registrering definierar hur företaget utformar och använder Azure-tjänsterna och definierar en grundläggande styrningsstruktur.
- Contoso börjar med att definiera ett kodskelett för Enterprise-registrering. Contoso använde [den här artikeln](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-subscription-governance) för att lära sig om och utforma ett kodskelett.
- För tillfället har Contoso bestämt sig för att använda en funktionell metod för att hantera prenumerationer.
  - Inom företaget kommer Contoso att använda en enda IT-avdelning som kontrollerar Azure-budgeten. Detta är den enda gruppen med prenumerationer.
  - Contoso kommer att utöka modellen i framtiden så att andra företagsgrupper kan registrera sig som avdelningar i Enterprise-registreringen.
  - Inom IT-avdelningen har Contoso strukturerat två prenumerationer: produktion och utveckling.
  - Om Contoso behöver ytterligare prenumerationer i framtiden måste de hantera åtkomst, principer och efterlevnad för dessa prenumerationer. Contoso gör detta genom att införa [Azure-hanteringsgrupper](https://docs.microsoft.com/azure/azure-resource-manager/management-groups-overview) som ytterligare ett lager ovanför prenumerationer.

  ![Företagsstruktur](./media/contoso-migration-infrastructure/enterprise-structure.png)

### <a name="examine-licensing"></a>Granska licensieringen

När prenumerationerna har konfigurerats kan Contoso titta på Microsoft-licensieringen. Licensieringsstrategin beror på vilka resurser som Contoso vill migrera till Azure och hur virtuella Azure-datorer och -tjänster är valda och distribuerade.

#### <a name="azure-hybrid-benefit"></a>Azure Hybrid-förmån

När Contoso distribuerar virtuella datorer i Azure innehåller standardavbildningar en licens. Contoso debiteras för dessa licenser för varje minut som programvaran används. Contoso har dock varit en Microsoft-kund under en lång tid och har använt Enterprise-avtal och öppna licenser med Software Assurance (SA).

Azure Hybrid Benefit låter Contoso spara pengar på migreringen, genom att låta företaget omvandla eller återanvända licenser för Windows Server Datacenter och Standard Edition som omfattas av Software Assurance för virtuella Azure-datorer och SQL Server-arbetsbelastningar. Detta gör det möjligt för Contoso att betala ett lägre beräkningspris för virtuella datorer och SQL Server. [Läs mer](https://azure.microsoft.com/pricing/hybrid-benefit).

#### <a name="license-mobility"></a>License Mobility

Med License Mobility genom Software Assurance kan Microsofts volymlicensieringskunder som Contoso distribuera berättigade serverprogram med aktiv Software Assurance på Azure. Därmed behöver de inte köpa nya licenser. Utan tillkommande rörlighetsavgifter är det lätt att distribuera befintliga licenser i Azure. [Läs mer](https://azure.microsoft.com/pricing/license-mobility).

#### <a name="reserve-instances-for-predictable-workloads"></a>Reservera instanser för förutsägbara arbetsbelastningar

Förutsägbara arbetsbelastningar är de som alltid måste vara tillgängliga med aktiva virtuella datorer. Till exempel branschspecifika appar, såsom ett SAP ERP-system. Å andra sidan är oförutsägbara arbetsbelastningar de som varierar, till exempel virtuella datorer som är på vid hög efterfrågan och av när efterfrågan är låg.

![Reserverad instans](./media/contoso-migration-infrastructure/reserved-instance.png)

I utbyte mot att använda reserverade instanser för vissa virtuella datorer som måste upprätthållas under långa tidsperioder, kan Contoso få både en rabatt och prioriterad kapacitet. Med [Reserverade Azure-instanser](https://azure.microsoft.com/pricing/reserved-vm-instances), tillsammans med Azure Hybrid Benefit, kan Contoso spara upp till 82 % på det ordinarie priset enligt principen ”betala per användning” (april 2018).

## <a name="step-2-manage-hybrid-identity"></a>Steg 2: Hantera hybrididentitet

Att ge och styra användaråtkomst till Azure-resurser med identitets- och åtkomsthantering (IAM) är ett viktigt steg i att sammanställa en Azure-infrastruktur.

- Contoso bestämmer sig för att utöka sin lokala Active Directory till molnet, i stället för att bygga ett nytt separat system i Azure.
- Därför skapar de en Azure-baserad Active Directory.
- Contoso har inte Office 365 på plats så de måste etablera en ny Azure AD.
- Office 365 använder Azure AD för användarhantering. Om Contoso hade använt Office 365 skulle de redan ha en Azure AD-klient och använda den som primärkatalog.
- [Lär dig](https://support.office.com/article/understanding-office-365-identity-and-azure-active-directory-06a189e7-5ec6-4af2-94bf-a22ea225a7a9) mer om Azure AD för Office 365 och lär [dig lägga till](https://docs.microsoft.com/azure/active-directory/active-directory-how-subscriptions-associated-directory) en prenumeration i en befintlig Azure AD-klient.

### <a name="create-an-azure-ad"></a>Skapa en Azure AD

Contoso använder versionen Azure AD Free som ingår i en Azure-prenumeration. Contosos administratörer konfigurerar en katalog enligt följande:

1. I [Azure portal](https://portal.azure.com) navigerar de till **Skapa en resurs** > **Identitet** > **Azure Active Directory**.
2. I **Skapa katalog** anger de ett namn för katalogen, ett preliminärt domännamn och region där Azure AD-katalogen ska skapas.

    ![Skapa Azure AD](./media/contoso-migration-infrastructure/azure-ad-create.png)

    > [!NOTE]
    > Katalogen som skapades levereras med ett initialt domännamn enligt mönstret **domännamn**.onmicrosoft.com. Namnet kan inte ändras eller tas bort. De måste i stället lägga till sitt registrerade domännamn i Azure AD.

### <a name="add-the-domain-name"></a>Lägg till domännamn

För att använda sitt standarddomännamn måste Contosos administratörer lägga till det i Azure AD som anpassat domännamn. Med det här alternativet kan de tilldela välbekanta användarnamn. En användare kan till exempel logga in med e-postadressen billg@contoso.com istället för att behöva billg@contosomigration.microsoft.com.

För att konfigurera ett anpassat domännamn lägger de till det i katalogen. Därefter lägger de till en DNS-post och kontrollerar namnet i Azure AD.

1. I **Anpassade domän namn** > **Lägg till anpassad domän** lägger de till domänen.
2. För att använda en DNS-post i Azure måste de registrera den hos domänregistratorn.

    - I listan **med anpassade domännamn** antecknar de DNS-informationen för namnet. Den använder en MX-inmatning.
    - De behöver åtkomst till namnserver för att göra detta. De loggar in på Contoso.com-domänen och skapar en ny MX-post för DNS-posten som tillhandahålls av Azure AD med hjälp av den antecknade informationen.

3. När DNS-posterna har spridits väljer de **Verifiera** i domänens namninformation för att kontrollera det anpassade domännamnet.

     ![Azure AD DNS](./media/contoso-migration-infrastructure/azure-ad-dns.png)

### <a name="set-up-on-premises-and-azure-groups-and-users"></a>Konfigurera lokala och Azure-grupper och -användare

Nu när Azure AD är igång måste Contosos administratörer lägga till anställda i lokala Active Directory-grupper som ska synkroniseras med Azure Active Directory. De bör använda lokala gruppnamn som motsvarar namnen på resursgrupperna i Azure. Detta gör det enklare att identifiera matchningar i synkroniseringsyfte.

#### <a name="create-resource-groups-in-azure"></a>Skapa resursgrupper i Azure

Resursgrupper i Azure samlar Azure-resurser. Med hjälp av ett resursgrupps-ID kan Azure utföra åtgärder på resurserna i gruppen.

- En Azure-prenumeration kan ha flera resursgrupper, men en resursgrupp kan bara finnas i en enda prenumeration.
- Dessutom kan en enda resursgrupp ha flera resurser, men en resurs kan bara tillhöra en enda resursgrupp.

Contosos administratörer konfigurerar Azure-resursgrupper enligt följande tabell.

<!-- markdownlint-disable MD033 -->

**Resursgrupp** | **Detaljer**
--- | ---
**ContosoCobRG** | Den här gruppen innehåller alla resurser som rör företagskontinuitet (COB). Den innehåller valv som Contoso ska använda för tjänsterna Azure Site Recovery och Azure Backup.<br/><br/> Den innehåller också resurser som används för migrering, inklusive Azure Migrate och Azure Database Migration Service.
**ContosoDevRG** | Den här gruppen innehåller utvecklings- och testresurser.
**ContosoFailoverRG** | Den här gruppen fungerar som en landningszon för resurser efter redundansväxling.
**ContosoNetworkingRG** | Den här gruppen innehåller alla nätverksresurser.
**ContosoRG** | Den här gruppen innehåller resurser som rör produktionsprogram och -databaser.

<!-- markdownlint-disable MD026 -->

De skapar resursgrupper på följande sätt:

1. I Azure Portal > **Resursgrupper** lägger de till en grupp.
2. För varje grupp anger de ett namn och den prenumeration och region som gruppen tillhör.
3. Resursgrupper visas i listan över **resursgrupper.**

    ![Resursgrupper](./media/contoso-migration-infrastructure/resource-groups.png)

##### <a name="scaling-resource-groups"></a>Skalanpassa resursgrupper

I framtiden kommer Contoso att lägga till andra resursgrupper efter behov. De kan till exempel definiera en resursgrupp för varje app eller tjänst så att de kan hanteras och skyddas separat.

#### <a name="create-matching-security-groups-on-premises"></a>Skapa matchande säkerhetsgrupper lokalt

1. I den lokala Active Directory konfigurerar Contosos administratörer säkerhetsgrupper med namn som matchar namnen på säkerhetsgrupperna i Azure.

    ![Lokala Active Directory-säkerhetsgrupper](./media/contoso-migration-infrastructure/on-prem-ad.png)

2. Av praktiska skäl skapar de ytterligare en grupp som kommer att läggas till i alla andra grupper. Den här gruppen har rättigheter till alla resursgrupper i Azure. Ett begränsat antal globala administratörer kommer att läggas till i den här gruppen.

### <a name="synchronize-active-directory"></a>Synkronisera Active Directory

Contoso vill etablera en gemensam identitet för åtkomst till resurser lokalt och i molnet. De kan göra detta genom att integrera lokala Active Directory med Azure AD. Med den här modellen:

- Kan användare och organisationer använda en enda identitet för att komma åt lokala program och molntjänster som Office 365 eller tusentals andra webbplatser på Internet.
- Administratörer kan använda grupperna i Active Directory för att implementera [rollbaserad åtkomstkontroll](https://docs.microsoft.com/azure/role-based-access-control/role-assignments-portal) i Azure.

För att under lätta integreringen använder Contoso verktyget [ Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect). När du installerar och konfigurerar verktyget på en domänkontrollant synkroniseras lokala Active Directory-identiteter med Azure AD.

### <a name="download-the-tool"></a>Hämta verktyget

1. I Azure Portal går Contosos administratörer till **Azure Active Directory** > **Azure AD Connect** och hämtar den senaste versionen av verktyget till den server som används för synkronisering.

    ![Hämta Azure AD Connect](./media/contoso-migration-infrastructure/download-ad-connect.png)

2. De startar installationen av **AzureADConnect.msi** med **Använd expressinställningar**. Det här är den vanligaste installationen och kan användas för en topologi med en skog med hash-synkronisering av lösenord för autentisering.

    ![Anlutningsguiden för Azure AD](./media/contoso-migration-infrastructure/ad-connect-wiz1.png)

3. I **Anslut till Azure AD** anger de autentiseringsuppgifterna för att ansluta till Azure AD (i formuläret admin@contoso.com eller admin@contoso.onmicrosoft.com).

    ![Anlutningsguiden för Azure AD](./media/contoso-migration-infrastructure/ad-connect-wiz2.png)

4. I **Anslut till AD DS** anger de inloggningsuppgifter för den lokala Active Directory (i formatet CONTOSO\admin eller contoso.com\admin).

     ![Anlutningsguiden för Azure AD](./media/contoso-migration-infrastructure/ad-connect-wiz3.png)

5. När de är **redo för konfigurering** väljer de **Starta synkroniseringsprocessen när konfigurationen är klar** för att starta synkroniseringen omedelbart. Sedan är det dags att installera.

Tänk på följande:

- Contoso har en direktanslutning till Azure. Om din lokala Active Directory ligger bakom en proxyserver ska du läsa den här [artikeln.](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-troubleshoot-connectivity)

- Efter den första synkroniseringen visas lokala Active Directory-objekt i Azure AD-katalogen.

    ![Lokal Active Directory i Azure](./media/contoso-migration-infrastructure/on-prem-ad-groups.png)

- Contosos IT-team finns med i varje grupp, baserat på dess roll.

    ![Lokala Active Directory-medlemmar i Azure](./media/contoso-migration-infrastructure/on-prem-ad-group-members.png)

### <a name="set-up-rbac"></a>Konfigurera rollbaserad åtkomstkontroll

[Rollbaserad åtkomstkontroll](https://docs.microsoft.com/azure/role-based-access-control/role-assignments-portal) (RBAC) i Azure ger tillgång till ingående åtkomsthantering för Azure. Med rollbaserad åtkomstkontroll kan du bevilja exakt den åtkomstnivå som användarna behöver för att kunna utföra sitt arbete. Du tilldelar en lämplig roll för åtkomstkontroll till användare, grupper och program på omfattningsnivå. Omfånget för en rolltilldelning kan vara en prenumeration, en resursgrupp eller en enskild resurs.

Contosos administratörer tilldelar nu roller till grupperna i Active Directory som de synkroniserade lokalt.

1. I resursgruppen **ControlCobRG** väljer de **åtkomst kontroll (IAM)**  > **Lägg till rolltilldelning**.
2. I **Lägg till rolltilldelning** > **Roll** > **Deltagare** väljer de gruppen **ContosoCobRG** från listan. Gruppen visas sedan i listan med **Valda medlemmar**.
3. De upprepar detta med samma behörigheter för de andra resursgrupperna (förutom för **ContosoAzureAdmins**) genom att lägga till deltagarbehörigheterna i det konto som motsvarar resursgruppen.
4. Gruppen **ContosoAzureAdmins** tilldelas rollen **Ägare**.

    ![Lokala Active Directory-medlemmar i Azure](./media/contoso-migration-infrastructure/on-prem-ad-groups.png)

## <a name="step-3-design-for-resiliency"></a>Steg 3: Designa för elasticitet

### <a name="set-up-regions"></a>Konfigurera regioner

Azureresurser distribueras i regioner.

- Regioner organiseras geografiskt och garanterar att krav på dataplacering, landsbaserad placering, efterlevnad och elasticitet stöds inom geografiska gränser.
- En region består av en uppsättning datacenter. De är distribuerade inom en latensdefinierad perimeter och ansluts via ett dedikerat regionalt nätverk med låg latens.
- Varje Azure-region är kopplad till en annan region av säkerhetsskäl.
- Läs om [Azure-](https://azure.microsoft.com/global-infrastructure/regions)regioner och lär dig [hur regioner paras ihop](https://docs.microsoft.com/azure/best-practices-availability-paired-regions).

Contoso har beslutat att gå med USA, östra 2 (finns i Virginia) som den primära regionen och centrala USA (finns i Iowa) som den sekundära regionen. Det finns ett par orsaker till detta:

- Contosos datacenter ligger i New York och Contoso tänkte på svarstiden till den närmaste datacentret.
- Regionen USA, östra 2 har alla tjänster och produkter som Contoso måste använda. Alla Azure-regioner är inte samma i fråga om vilka produkter och tjänster som finns tillgängliga. Du kan titta på [Azure-produkter efter region](https://azure.microsoft.com/global-infrastructure/services).
- Azure-regionen centrala USA är parkopplad med USA, östra 2.

Eftersom Contoso funderar på att använda en hybridmiljö måste de tänka på hur de ska bygga in motståndskraft och en katastrofberedskapsplan i sin regionsdesign. Strategier sträcker sig i stort sett från en distribution med en region, som förlitar sig på Azures plattformsfunktioner såsom feldomäner och regional parkoppling, till en fullskalig aktiv/aktiv-modell där molntjänster och databaser distribueras och används av användare från två regioner.

Contoso har valt något som ligger i mitten. De kommer att distribuera appar och resurser i en primärregion och kvarhålla en fullständig kopia av infrastrukturen i sekundärregionen som kan fungera som en fullständig säkerhetskopia vid apphaveri eller ett regionalt driftsstopp.

### <a name="set-up-availability"></a>Konfigurera tillgänglighet

**Tillgänglighetsuppsättningar:**

Tillgänglighetsuppsättningar hjälper till att skydda appar och data från lokala maskinvaru- och nätverksavbrott i ett datacenter.

- Tillgänglighetsuppsättningar distribuerar virtuella Azure-datorer över olika fysiska maskinvaruenheter i ett datacenter.
- Feldomäner representerar underliggande maskinvara som delar en strömkälla och nätverksomkopplare inom datacentret. Virtuella datorer i en tillgänglighetsuppsättning distribueras över olika feldomäner för att minimera driftstörningar som orsakas av enstaka maskinvaru- eller nätverksfel.
- En uppdateringsdomän representerar maskinvara som kan underhållas eller startas om samtidigt. Tillgänglighetsuppsättningar distribuerar även virtuella datorer över flera uppdateringsdomäner för att säkerställa att minst en instans alltid körs.

Contoso implementerar tillgänglighetsuppsättningar när arbetsbelastningar på virtuella datorer kräver hög tillgänglighet. [Läs mer](https://docs.microsoft.com/azure/virtual-machines/windows/manage-availability).

**Tillgänglighetszoner:**

Tillgänglighetszoner hjälper till att skydda appar och data från fel som påverkar ett helt datacenter inom en region.

- Varje tillgänglighetszon är en unik fysisk plats inom en Azure-region.
- Varje zon utgörs av ett eller flera datacenter som är utrustade med oberoende kraft, kylning och nätverk.
- Det finns minst tre separata zoner i alla aktiverade regioner.
- Den fysiska avgränsningen av zonerna inom en region skyddar program och data mot datacenterfel.

Contoso distribuerar tillgänglighetszoner som appanrop för skalbarhet, hög tillgänglighet och återhämtning. [Läs mer](https://docs.microsoft.com/azure/availability-zones/az-overview).

### <a name="set-up-backup"></a>Konfigurera säkerhetskopiering

**Azure Backup:**

Med Azure Backup kan du säkerhetskopiera och återställa virtuella Azure-diskar.

- Med Azure Backup kan du automatisera säkerhetskopiering av diskavbildningar för virtuella datorer som lagras i Azure Storage.
- Säkerhetskopieringarna är konsekventa mellan olika appar och säkerställer att säkerhetskopierade data är konsekventa och att programmen startar efter återställning.
- Azure Backup har stöd för lokalt redundant lagring (LRS) för att replikera flera kopior av dina säkerhetskopieringsdata inom ett datacenter i händelse av lokala maskinvarufel.
- I händelse av ett regionalt avbrott stöder Azure Backup också geo-redundant lagring (GRS) som replikerar dina säkerhetskopierade data till en sekundär, kopplad region.
- Azure Backup krypterar data under överföring med AES 256. Säkerhetskopiering av data i vila krypteras med hjälp av [kryptering för lagringstjänst (SSE)](https://docs.microsoft.com/azure/storage/common/storage-service-encryption?toc=%2fazure%2fstorage%2fqueues%2ftoc.json).

Contoso använder Azure Backup med GRS på alla virtuella produktionsdatorer för att säkerställa att arbetsbelastningsdata säkerhetskopieras och kan återställas snabbt i händelse av driftstopp eller annat avbrott. [Läs mer](https://docs.microsoft.com/azure/backup/backup-introduction-to-azure-backup).

### <a name="set-up-disaster-recovery"></a>Konfigurera haveriberedskap

**Azure Site Recovery:**

Azure Site Recovery bidrar till att säkerställa affärskontinuitet genom att se till att appar och arbetsbelastningar körs under regionala driftstopp.

- Azure Site Recovery replikerar ständigt virtuella Azure-datorer från en primär till en sekundär region så att fungerande kopior alltid finns på båda platserna.
- I händelse av ett avbrott i den primära regionen växlar programmet eller tjänsten över till att använda virtuella datorer som har replikerats in den sekundära regionen, vilket minskar eventuella avbrott.
- När verksamheten återgår till det normala kan dina program eller tjänster växla över till virtuella datorer i den primära regionen.

Contoso implementerar Azure Site Recovery för alla virtuella produktionsdatorer som används i verksamhetskritiska arbetsbelastningar, vilket garanterar minimal störning under ett avbrott i den primära regionen. [Läs mer](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview)

## <a name="step-4-design-a-network-infrastructure"></a>Steg 4: Utforma en nätverksinfrastruktur

Med den regionala designen på plats är Contoso redo att fundera på en nätverksstrategi. Det måste tänka på hur det lokala datacentret och Azure ansluter och kommunicerar med varandra och hur nätverksinfrastrukturen ska utformas i Azure. I synnerhet måste Contoso:

- **Planera hybridnätverksanslutning.** Fundera på hur anslutningar mellan lokala nätverk och Azure ska gå till.
- **Utforma en Azure-nätverksinfrastruktur.** Bestämma sig för hur nätverk ska distribueras över regioner. Hur ska nätverk kommunicera inom samma region och mellan regioner?
- **Utforma och konfigurera Azure-nätverk.** Konfigurera Azure-nätverk och -undernät och bestäm vad som ska finnas i dem.

### <a name="plan-hybrid-network-connectivity"></a>Planera hybridnätverksanslutning

Contoso övervägde ett [antal utformningar](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking) för hybridnätverk mellan Azure och det lokala datacentret. [Läs mer](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/considerations) om att jämföra alternativ.

Som en påminnelse består den lokala nätverksinfrastrukturen i Contoso för närvarande av datacentret i New York och lokala grenar i östra USA. Alla platser har en anslutning till Internet i företagsklass. Varje avdelning ansluts sedan till datacentret via en IPSec VPN-tunnel via Internet.

![Contosos nätverk](./media/contoso-migration-infrastructure/contoso-networking.png)

Så här har Contoso valt att implementera hybridanslutningar:

1. De konfigurerade en ny plats-till-plats-VPN-anslutning mellan Contosos datacenter i New York och de två Azure-regionerna i USA, östra 2 och centrala USA.
2. Trafik från det lokala kontoret på väg till Azures virtuella nätverk kommer att dirigeras via Contosos huvuddatacenter.
3. När Contoso skalar upp Azure-distributionen kommer de att upprätta en ExpressRoute-anslutning mellan datacentret och Azure-regionerna. När detta sker behåller Contoso endast plats-till-plats-VPN-anslutningen för redundans.
    - [Lär dig](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/considerations) mer om att välja mellan VPN och ExpressRoute for hybridlösningar.
    - Kontrollera [platser och stöd för ExpressRoute](https://docs.microsoft.com/azure/expressroute/expressroute-locations-providers).

**Endast VPN:**

![Contosos VPN](./media/contoso-migration-infrastructure/hybrid-vpn.png)

**VPN och ExpressRoute:**

![Contosos VPN/ExpressRoute](./media/contoso-migration-infrastructure/hybrid-vpn-expressroute.png)

### <a name="design-the-azure-network-infrastructure"></a>Utforma en Azure-nätverksinfrastruktur

Det är viktigt att Contoso etablerar ett nätverk på ett sätt som gör hybriddistributionen säker och skalbar. Därför väljer Contoso en långsiktig metod och utformar motståndskraftiga virtuella nätverk i företagsklass. [Läs mer](https://docs.microsoft.com/azure/virtual-network/virtual-network-vnet-plan-design-arm) om att planera virtuella nätverk.

Contoso har valt att implementera en nätverksmodell från hubb till hubb för att ansluta de två regionerna:

- I varje region använder Contoso en hubb och navmodell.
- Contoso använder Azures nätverkspeering för att ansluta nätverken och hubbarna.

#### <a name="network-peering"></a>Nätverkspeering

Azure tillhandahåller nätverkspeering för att ansluta virtuella nätverk och hubbar. Global peering tillåter anslutningar mellan virtuella nätverk/hubbar i olika regioner. Lokal peering ansluter virtuella nätverk i samma region. VNet-peering har flera fördelar:

- Nätverkstrafiken mellan peerkopplade virtuella nätverk är privat.
- Trafiken mellan de virtuella nätverken finns i Microsoft-stamnätverket. Vid kommunikation mellan virtuella nätverk krävs inget offentligt Internet, inga gatewayer eller ingen kryptering.
- Peering ger en standardanslutning med korta svarstider och hög bandbredd mellan resurser i olika virtuella nätverk.

[Läs mer](https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview) om nätverkspeering.

#### <a name="hub-to-hub-across-regions"></a>Hubb-till-hubb över regioner

Contoso distribuerar en hubb i varje region. Hubben är ett virtuellt nätverk (VNet) i Azure som fungerar som en central anslutningspunkt till det lokala nätverket. De virtuella hubbnätverken ansluts till varandra med global VNET-peering. Global VNet-peering ansluter virtuella nätverk i olika Azure-regioner.

- Hubben i varje region peerkopplas till dess partnerhubb i den andra regionen.
- Hubben peerkopplas till varje nätverk i regionen och kan anslutas till alla nätverksresurser.

    ![Global peering](./media/contoso-migration-infrastructure/global-peering.png)

#### <a name="hub-and-spoke-model-within-a-region"></a>Hubb- och ekermodell inom en region

I varje region kommer Contoso att distribuera virtuella nätverk för olika syften som ekernätverk till regionshubben. Virtuella nätverk inom en region använder peering för att ansluta till deras sin hubb och till varandra.

#### <a name="design-the-hub-network"></a>Utforma hubbnätverket

I Contosos hubb- och ekermodell måste de överväga hur trafik ska dirigeras från det lokala datacentret och Internet. Så här har Contoso valt att hantera dirigering för såväl USA, östra 2 och centrala USA:

- Contoso utformar ett nätverk som kallas "reverse c", eftersom det här är den sökväg som paketen följer från det inkommande till det utgående nätverket.
- Nätverksarkitekturen har två gränser, en icke betrodd zon för klientdelen och en betrodd zon för serverdelen.
- En brandvägg har ett nätverkskort i varje zon för att kontrollera åtkomsten till betrodda zoner.
- Från Internet:
  - Internettrafiken påträffar en belastningsutjämnad offentlig IP-adress i perimeternätverket.
  - Trafiken dirigeras genom brandväggen och brandväggsreglerna tillämpas.
  - När nätverksåtkomstkontroller har implementerats vidarebefordras trafiken till en lämplig plats i den betrodda zonen.
  - Utgående trafik från det virtuella nätverket kommer att dirigeras till Internet via användardefinierade vägar. Trafiken tvingas genom brandväggen och inspekteras enligt Contosos principer.
- Från Contosos datacenter:
  - Inkommande trafik via plats-till-plats-VPN (eller ExpressRoute) påträffar den offentliga IP-adressen för Azure VPN-gatewayen.
  - Trafiken dirigeras genom brandväggen och brandväggsreglerna tillämpas.
  - När brandväggsreglerna har tillämpas vidarebefordras trafiken till en intern belastningsutjämnare (Standard-SKU) i den betrodda interna zonens undernät.
  - Utgående trafik från det betrodda undernätet till det lokala datacentret via VPN dirigeras genom brandväggen vars regler tillämpas, innan det skickas via plats-till-plats-VPN-anslutningen.

### <a name="design-and-set-up-azure-networks"></a>Utforma och konfigurera Azure-nätverk

Nu när Contosos har en topologi för nätverk och trafikdirigering är de redo att konfigurera Azure-nätverk och -undernät.

- Contoso implementerar ett privat nätverk i Klass A på Azure (0.0.0.0 till 127.255.255.255). Detta fungerar, eftersom de för närvarande har ett lokalt privat adressutrymme av klass B 172.160.0/16, så Contoso kan vara säkra på att adresserna inte överlappar.
- De kommer att distribuera virtuella nätverk i de primära och sekundära regionerna.
- Contoso kommer att använda en namngivningskonvention som innehåller prefixet **VNet** och regionförkortningen **EUS2** eller **CUS**. Med den här standarden heter hubbnätverken **VNet-Hub-EUS2** (USA, östra 2) och **VNet-Hub-CUS** (centrala USA).
- Contoso har ingen [IPAM-lösning](https://docs.microsoft.com/windows-server/networking/technologies/ipam/ipam-top) så de måste planera en nätverksroutning utan NAT.

#### <a name="virtual-networks-in-east-us-2"></a>Virtuella nätverk i USA, östra 2

USA, östra 2 är den primära regionen som Contoso planerar att använda för att distribuera resurser och tjänster. Så här kommer Contoso att utforma sina nätverk:

- **Hubb:** Det virtuella hubbnätverket i USA, östra 2, är den centrala primära anslutningspunkten till det lokala datacentret.
- **Virtuella nätverk:** Virtuella ekernätverk i USA, östra 2 kan användas för att isolera arbetsbelastningar vid behov. Utöver det virtuella hubbnätverket kommer Contoso att ha två virtuella ekernätverk i USA, östra 2:
  - **VNET-DEV-EUS2**. Det här virtuella nätverket ger utvecklings- och testteamet ett fullt funktionellt nätverk för utvecklingsprojekt. Det kommer att fungera som att produktionstestområde. Det innebär att produktionsinfrastrukturen måste fungera här.
    - **VNET-PROD-EUS2**. Azure IaaS-produktionskomponenter kommer att finnas i det här nätverket.
  - Varje virtuella nätverk har sin egen adressyta utan att överlappa varandra. Contoso planerar att konfigurera routning utan att behöva NAT.
- **Undernät:**
  - Det finns ett undernät i varje nätverk för varje appnivå
  - Varje undernät i produktionsnätverket har ett matchande undernät i det virtuella utvecklingsnätverket.
  - Dessutom har produktionsnätverket ett undernät för domänkontrollanter.

De virtuella nätverken i USA, östra 2 sammanfattas i tabellen nedan.

**VNet** | **Område** | **Peer**
--- | --- | ---
**VNET-HUB-EUS2** | 10.240.0.0/20 | VNET-HUB-CUS2, VNET-DEV-EUS2, VNET-PROD-EUS2
**VNET-DEV-EUS2** | 10.245.16.0/20 | VNET-HUB-EUS2
**VNET-PROD-EUS2** | 10.245.32.0/20 | VNET-HUB-EUS2, VNET-PROD-CUS

![Hubb- och ekermodell i den primära regionen](./media/contoso-migration-infrastructure/primary-hub-peer.png)

#### <a name="subnets-in-the-east-us-2-hub-network-vnet-hub-eus2"></a>Undernät i hubbnätverket USA, östra 2 (VNET-HUB-EUS2)

**Undernät/zon** | **CIDR** | **Användbara IP-adresser
--- | --- | ---
**IB-UntrustZone** | 10.240.0.0/24 | 251
**IB-TrustZone** | 10.240.1.0/24 | 251
**OB-UntrustZone** | 10.240.2.0/24 | 251
**OB-TrustZone** | 10.240.3.0/24 | 251
**GatewaySubnets** | 10.240.10.0/24 | 251

#### <a name="subnets-in-the-east-us-2-dev-network-vnet-dev-eus2"></a>Undernät i utvecklarnätverket USA, östra 2 (VNET-DEV-EUS2)

Det virtuella utvecklingsnätverket används av utvecklingsteamet som ett testområde för produktion. Det har tre undernät.

**Undernät** | **CIDR** | **Adresser** | **I undernät**
--- | --- | --- | ---
**DEV-FE-EUS2** | 10.245.16.0/22 | 1019 | Virtuella datorer för klientdel/webbnivå
**DEV-APP-EUS2** | 10.245.20.0/22 | 1019 | Virtuella datorer på appnivå
**DEV-DB-EUS2** | 10.245.24.0/23 | 507 | Virtuella databasdatorer

#### <a name="subnets-in-the-east-us-2-production-network-vnet-prod-eus2"></a>Undernät i produktionsnät i USA, östra 2 (VNET-PROD-EUS2)

Azure IaaS-komponenter ligger i produktionsnätverket. Varje appnivå har sitt eget undernät. Undernäten motsvarar de som finns i utvecklingsnätverket, samt ytterligare ett undernät för domänkontrollanter.

**Undernät** | **CIDR** | **Adresser** | **I undernät**
--- | --- | --- | ---
**PROD-FE-EUS2** | 10.245.32.0/22 | 1019 | Virtuella datorer för klientdel/webbnivå
**PROD-APP-EUS2** | 10.245.36.0/22 | 1019 | Virtuella datorer på appnivå
**PROD-DB-EUS2** | 10.245.40.0/23 | 507 | Virtuella databasdatorer
**PROD-DC-EUS2** | 10.245.42.0/24 | 251 | Virtuella datorer för domänkontrollant

![Hubbnätverksarkitektur](./media/contoso-migration-infrastructure/azure-networks-eus2.png)

#### <a name="virtual-networks-in-central-us-secondary-region"></a>Virtuella nätverk i centrala USA (sekundär region)

Centrala USA är Contosos sekundära region. Så här kommer Contoso att utforma sina nätverk:

- **Hubb:** Det virtuella hubbnätverket i USA, östra 2 är den centrala anslutningspunkten till det lokala datacentret och de virtuella ekernätverken i USA, östra 2 kan användas för att isolera arbetsbelastningar vid behov och hantera dem avskilt från de andra ekrarna.
- **Virtuella nätverk:** Contoso kommer att ha två virtuella nätverk i centrala USA:
  - VNET-PROD-CUS. Det här virtuella nätverket är ett produktionsnätverk som liknar VNET-PROD_EUS2.
  - VNET-ASR-CUS. Det här virtuella nätverket fungerar som en plats där virtuella datorer skapas efter redundansväxling från det lokala datacentret eller som en plats för virtuella Azure-datorer som har redundansväxlats från den primära till den sekundära regionen. Det här nätverket liknar produktionsnätverken men har inga domänkontrollanter.
  - Varje virtuella nätverk i regionen har sin egen adressyta utan att överlappa varandra. Contoso konfigurerar routning utan NAT.
- **Undernät:** Undernäten kommer att konstrueras på ett liknande sätt som i USA, östra 2. Undantaget är att Contoso inte behöver ett undernät för domänkontrollanter.

De virtuella nätverken i centrala USA sammanfattas i tabellen nedan.

**VNet** | **Område** | **Peer**
--- | --- | ---
**VNET-HUB-CUS** | 10.250.0.0/20 | VNET-HUB-EUS2, VNET-ASR-CUS, VNET-PROD-CUS
**VNET-ASR-CUS** | 10.255.16.0/20 | VNET-HUB-CUS, VNET-PROD-CUS
**VNET-PROD-CUS** | 10.255.32.0/20 | VNET-HUB-CUS, VNET-ASR-CUS, VNET-PROD-EUS2

![Hubb- och ekermodell i en kopplad region](./media/contoso-migration-infrastructure/paired-hub-peer.png)

#### <a name="subnets-in-the-central-us-hub-network-vnet-hub-cus"></a>Undernät i hubbnätverket för centrala USA (VNET-HUB-CUS)

**Undernät** | **CIDR** | **Användbara IP-adresser**
--- | --- | ---
**IB-UntrustZone** | 10.250.0.0/24 | 251
**IB-TrustZone** | 10.250.1.0/24 | 251
**OB-UntrustZone** | 10.250.2.0/24 | 251
**OB-TrustZone** | 10.250.3.0/24 | 251
**GatewaySubnet** | 10.250.2.0/24 | 251

#### <a name="subnets-in-the-central-us-production-network-vnet-prod-cus"></a>Undernät i produktionsnät i centrala USA (VNET-PROD-CUS2)

Parallellt med produktionsnätverket i den primära regionen USA, östra 2, finns det ett produktionsnätverk i den sekundära regionen centrala USA.

**Undernät** | **CIDR** | **Adresser** | **I undernät**
--- | --- | --- | ---
**PROD-FE-CUS** | 10.255.32.0/22 | 1019 | Virtuella datorer för klientdel/webbnivå
**PROD-APP-CUS** | 10.255.36.0/22 | 1019 | Virtuella datorer på appnivå
**PROD-DB-CUS** | 10.255.40.0/23 | 507 | Virtuella databasdatorer
**PROD-DC-CUS** | 10.255.42.0/24 | 251 | Virtuella datorer för domänkontrollant

#### <a name="subnets-in-the-central-us-failoverrecovery-network-in-central-us-vnet-asr-cus"></a>Undernät i det redundans för centrala USA/återställningsnätverk i centrala USA (VNET-ASR-CUS)

VNET-ASR-CUS-nätverket används för redundans mellan regioner. Site Recovery kommer att användas för att replikera och redundansväxla virtuella Azure-datorer mellan regionerna. Det fungerar också som ett Contoso-datacenter för Azure-nätverket för skyddade arbetsbelastningar som är kvar lokalt, men som redundansväxlas till Azure för haveriberedskap.

VNET-ASR-CUS är samma grundläggande undernät som det virtuella produktionsnätverket i USA, östra 2, men utan domänkontrollant.

**Undernät** | **CIDR** | **Adresser** | **I undernät**
--- | --- | --- | ---
**ASR-FE-CUS** | 10.255.16.0/22 | 1019 | Virtuella datorer för klientdel/webbnivå
**ASR-APP-CUS** | 10.255.20.0/22 | 1019 | Virtuella datorer på appnivå
**ASR-DB-CUS** | 10.255.24.0/23 | 507 | Virtuella databasdatorer

![Hubbnätverksarkitektur](./media/contoso-migration-infrastructure/azure-networks-cus.png)

#### <a name="configure-peered-connections"></a>Konfigurera peeranslutningar

Hubben i varje region kommer att peeranslutas till hubben i den andra regionen och till alla virtuella nätverk i hubbregionen. Därmed kan hubbarna kommnuicera och alla virtuella nätverk för en region kan visas. Tänk på följande:

- Peering skapar en tvåsidig anslutning. En från den initierande peer-datorn på det första virtuella nätverket och ett annat på det andra virtuella nätverket.
- I en hybriddistribution måste trafik som passerar mellan peer-datorer vara synlig från VPN-anslutningen mellan det lokala datacentret och Azure. För att aktivera detta finns det vissa inställningar som måste konfigureras för peer-anslutningar.

För anslutningar från virtuella ekernätverk via hubben till det lokala datacentret måste Contoso låta trafik vidarebefordras och ställa om VPN-gatewayerna.

##### <a name="domain-controller"></a>Domänkontrollant

För domänkontrollanterna i nätverket VNET-PROD-EUS2 vill Contoso att trafiken ska flöda såväl mellan hubb-/produktionsnätverket EUS2 som över VPN-anslutningen till det lokala datacentret. För att göra detta måste Contosos administratörer tillåta följande:

1. Konfigurationerna **Tillåt vidarebefordrad trafik** och **Tillåt gatewaytrafik** på peer-anslutningen. I vårt exempel är det anslutningen från VNET-HUB-EUS2 till VNET-PROD-EUS2.

    ![Peering](./media/contoso-migration-infrastructure/peering1.png)

2. **Tillåt vidarebefordrad trafik** och **Använd fjärrgateways** på den andra sidan av peeranslutningen på anslutningen från VNET-PROD-EUS2 till VNet-Hub-EUS2.

    ![Peering](./media/contoso-migration-infrastructure/peering2.png)

3. Lokalt konfigurerar de en statisk väg som dirigerar den lokala trafiken till routning via VPN-tunneln till det virtuella nätverket. Konfigurationen slutförs på den gateway som tillhandahåller VPN-tunneln från Contoso till Azure. De använder RRAS för detta.

    ![Peering](./media/contoso-migration-infrastructure/peering3.png)

##### <a name="production-networks"></a>Produktionsnätverk

Ett peernätverk med ekrar kan inte se andra peernätverk med ekrar i en annan region via en hubb.

För att Contosos produktionsnätverk i båda regioner ska se varandra måste Contosos administratörer skapa en direkt peeranslutning för VNET-PROD-EUS2 och VNET-PROD-CUS.

![Peering](./media/contoso-migration-infrastructure/peering4.png)

### <a name="set-up-dns"></a>Konfigurera DNS

När du distribuerar resurser i virtuella nätverk har du ett par alternativ för domännamnsmatchning. Du kan använda namnmatchning från Azure eller tillhandahålla DNS-servrar för matchning. Vilken typ av namnmatchning du använder beror på hur dina resurser behöver kommunicera med varandra. Få [mer information](https://docs.microsoft.com/azure/virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances#azure-provided-name-resolution) om Azure DNS-tjänsten.

Contosos administratörer har beslutat att tjänsten Azure DNS inte är lämplig för hybridmiljön. I stället kommer de att använda lokala DNS-servrar.

- Eftersom det här är ett hybridnätverk måste alla lokala virtuella datorer och virtuella Azure-datorer kunna matcha namn. Det innebär att anpassade DNS-inställningar måste tillämpas på alla virtuella nätverk.
- Contoso har för närvarande domänkontrollanter i Contosos datacenter och på de lokala kontoren. De primära DNS-servrarna är CONTOSODC1 (172.16.0.10) och CONTOSODC2 (172.16.0.1)
- När virtuella nätverk distribueras kommer de lokala domänkontrollanterna att ställas in så att de används som DNS-servrar i nätverken.
- Om du vill konfigurera detta när du använder anpassat DNS i virtuella nätverk måste en IP-adress för Azures rekursiva matchare (till exempel 168.63.129.16) läggas till i DNS-listan. För att göra detta konfigurerar Contoso DNS-serverinställningar på varje virtuella nätverk. Till exempel skulle anpassade DNS-inställningar för VNET-HUB-EUS2-nätverket vara följande:

    ![Anpassad DNS](./media/contoso-migration-infrastructure/custom-dns.png)

Utöver de lokala domänkontrollanterna ska Contoso implementera ytterligare fyra för Azure-nätverken, två för varje region. Det här är vad Contoso planerar att distribuera i Azure.

**Region** | **DC** | **VNet** | **Undernät** | **IP-adress**
--- | --- | --- | --- | ---
EUS2 | CONTOSODC3 | VNET-PROD-EUS2 | PROD-DC-EUS2 | 10.245.42.4
EUS2 | CONTOSODC4 | VNET-PROD-EUS2 | PROD-DC-EUS2 | 10.245.42.5
CUS | CONTOSODC5 | VNET-PROD-CUS | PROD-DC-CUS | 10.255.42.4
CUS | CONTOSODC6 | VNET-PROD-CUS | PROD-DC-CUS | 10.255.42.4

När Contoso har distribuerat de lokala domänkontrollanterna måste de uppdatera DNS-inställningarna på nätverken för varje region för att inkludera de nya domänkontrollanterna i DNS-serverlistan.

#### <a name="set-up-domain-controllers-in-azure"></a>Konfigurera domänkontrollanter i Azure

När Contosos administratörer har uppdaterat nätverksinställningarna är de redo att bygga ut domänkontrollanterna i Azure.

1. De distribuerar en ny virtuell Windows Server-dator till ett lämpligt virtuellt nätverk i Azure Portal.
2. De skapar tillgänglighetsuppsättningar på varje plats för den virtuella datorn. Tillgänglighetsuppsättningar gör följande:

    - De ser till att infrastrukturen hos Azure skiljer de virtuella datorerna i olika infrastrukturer i Azure-regionen.
    - De ger Contoso berättigande till 99,95 % SLA för virtuella datorer i Azure. [Läs mer](https://docs.microsoft.com/azure/virtual-machines/windows/tutorial-availability-sets).

    ![Tillgänglighetsgrupp](./media/contoso-migration-infrastructure/availability-group.png)

3. När den virtuella datorn har distribuerats öppnas nätverksgränssnittet för den virtuella datorn. De konfigurerar den privata IP-adressen som statisk och anger en giltig adress.

    ![Nätverkskort för virtuell dator](./media/contoso-migration-infrastructure/vm-nic.png)

4. De kopplar nu en ny datadisk till den virtuella datorn. Den här disken innehåller Active Directory-databasen och Sysvol-resursen.
    - Disk storleken avgör antalet IOPS som stöds.
    - Med tiden kan de behöva öka diskstorleken efter hand som miljön växer.
    - Enheten bör inte vara inställd på läsning/skrivning för värdcachelagring. Active Directory-databaser har inte stöd för detta.

     ![Active Directory-disk](./media/contoso-migration-infrastructure/ad-disk.png)

5. När disken har lagts till ansluter de till den virtuella datorn via fjärrskrivbord och öppnar serverhanteraren.

6. Sedan körs guiden Ny volym i **Fil-och lagrings tjänster** och kontrollerar att enheten får bokstaven F: eller senare på den lokala virtuella datorn.

     ![Guiden ny volym](./media/contoso-migration-infrastructure/volume-wizard.png)

7. I Serverhanteraren lägger de till rollen **Active Directory Domain Services**. Sedan konfigurerar de den virtuella datorn som en domänkontrollant.

      ![Serverroll](./media/contoso-migration-infrastructure/server-role.png)

8. När den virtuella datorn har konfigurerats som en domänkontrollant och startats om öppnar de DNS-hanteraren och konfigurerar Azure DNS-matcharen som en vidarebefordrare. Detta gör att domänkontrollanten kan vidarebefordra DNS-frågor som inte kan lösas i Azure DNS.

    ![DNS-vidarebefordrare](./media/contoso-migration-infrastructure/dns-forwarder.png)

9. De uppdaterar nu de anpassade DNS-inställningarna för varje virtuella nätverk med lämplig domänkontrollant för regionen. De inkluderar lokala domänkontrollanter i listan.

### <a name="set-up-active-directory"></a>Konfigurera Active Directory

Active Directory är en kritisk tjänst i nätverk och måste vara korrekt konfigurerad. Contosos administratörer skapar Active Directory webbplatser för Contosos datacenter och för regionerna EUS2 och CUS.

1. De skapar två nya platser (AZURE-EUS2 och AZURE-CUS) samt en plats för datacentret (ContosoDatacenter).
2. När du har skapat platserna skapar de undernät på platserna för att matcha de virtuella nätverken med datacentret.

    ![Undernät för datakontrollanter](./media/contoso-migration-infrastructure/dc-subnets.png)

3. Sedan skapar de två platslänkar för att ansluta allt. Domänkontrollanterna bör sedan flyttas till deras plats.

    ![Länkar till domänkontrollanter](./media/contoso-migration-infrastructure/dc-links.png)

4. När allt har konfigurerats är Active Directory-topologin för replikering på plats.

    ![Replikering av domänkontrollant](./media/contoso-migration-infrastructure/ad-resolution.png)

5. När allt är klart visas en lista över domänkontrollanter och platser i det lokala Active Directory Administrationscenter.

    ![Active Directory Administrationscenter](./media/contoso-migration-infrastructure/ad-center.png)

## <a name="step-5-plan-for-governance"></a>Steg 5: Planera för styrning

Azure har en serie styrningskontroller för olika tjänster och delar av Azure-plattformen. [Läs mer](https://docs.microsoft.com/azure/security/governance-in-azure) om du vill ha en grundläggande förståelse av alternativen.

När de konfigurerade identitets- och åtkomstkontroll började Contoso redan etablera vissa aspekter av styrning och säkerhet. Generellt sett finns det tre områden att ta hänsyn till:

- **Principer:** Azure Policy tillämpar och verkställer regler och effekter på dina resurser så att resurserna förblir kompatibla med företagskrav och serviceavtal.
- **Lås:** Med Azure kan du låsa prenumerationer, resursgrupper och andra resurser så att de bara kan ändras av de som har behörighet att göra det.
- **Taggar:** Resurser kan styras, granskas och hanteras med taggar. Taggarna kopplar metadata till resurser som ger information om resurser eller ägare.

### <a name="set-up-policies"></a>Konfigurera principer

Azure Policy kör en utvärdering av resurserna och söker efter sådana som inte är kompatibla med principdefinitionerna. Du kan till exempel ha en princip som endast tillåter vissa typer av virtuella datorer eller kräver att resurser har en specifik tagg.

Principer innehåller en principdefinition. En principtilldelning anger i vilket omfång en princip ska tillämpas. Omfånget kan vara allt från en hanteringsgrupp till en resursgrupp. [Läs mer](https://docs.microsoft.com/azure/governance/policy/tutorials/create-and-manage) om att skapa och hantera principer.

Contoso vill komma igång med ett par principer:

- De vill ha en princip för att säkerställa att resurserna bara kan distribueras i regionerna EUS2 och CUS.
- De vill begränsa SKU:er för virtuella datorer till endast godkända SKU:er. Avsikten är att se till att dyra SKU:er för virtuella datorer inte används.

#### <a name="limit-resources-to-regions"></a>Begränsa resurser till regioner

Contoso använder den inbyggda principdefinitionen **Tillåtna platser** för att begränsa resursregioner.

1. I Azure Portal väljer du**Alla tjänster** och söker efter **Princip**.
2. Välj **Tilldelningar** > **Tilldela princip**.
3. I principlistan väljer du **Tillåtna platser**.
4. Ställ in **Omfånget** som namnet på Azure-prenumerationen och välj de två regionerna i listan över tillåtna.

    ![Regioner som tillåts av princip](./media/contoso-migration-infrastructure/policy-region.png)

5. Som standard är principen inställd på **Neka**, vilket innebär att distributionen kommer att misslyckas om någon påbörjar den i en prenumeration som inte är i EUS2 eller CUS. Det här är vad som händer om någon i Contoso-prenumerationen försöker konfigurera en distribution i USA, västra.

    ![Principen misslyckades](./media/contoso-migration-infrastructure/policy-failed.png)

#### <a name="allow-specific-vm-skus"></a>Tillåt specifika SKU:er för virtuella datorer

Contoso kommer att använda den inbyggda principdefinitionen **Tillåt SKU:er för virtuella datorer** för att begränsa typen av virtuella datorer som kan skapas i prenumerationen.

![Princip för SKU](./media/contoso-migration-infrastructure/policy-sku.png)

#### <a name="check-policy-compliance"></a>Kontrollera efterlevnad av principer

Principerna träder i kraft omedelbart och Contoso kan kontrollera att de tillämpas på resurserna.

1. Välj länken **Efterlevnad** i Azure Portal.
2. Instrumentpanelen för efterlevnad visas. Du kan öka detaljnivån om du vill ha mer information.

    ![Principefterlevnad](./media/contoso-migration-infrastructure/policy-compliance.png)

### <a name="set-up-locks"></a>Konfigurera lås

Contoso har länge använt ITIL-ramverket för att hantera sina system. En av de viktigaste aspekterna av ramverket är ändringskontroll och Contoso vill se till att ändrings kontrollen implementeras i Azure-distributionen.

Contoso ska implementera lås enligt följande:

- Alla komponenter för produktion eller redundans måste befinna sig i en grupp som har ett ReadOnly-lås. Det innebär att låset måste tas bort för att det ska gå att ändra eller ta bort produktionsobjekt.
- Resursgrupper som inte är för produktion kommer att ha CanNotDelete-lås. Det innebär att behöriga användare kan läsa eller ändra en resurs, men inte ta bort den.

[Läs mer](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-lock-resources) om lås.

### <a name="set-up-tagging"></a>Konfigurera taggning

För att kunna spåra resurser när de läggs till blir det allt viktigare för Contoso att associera resurser med en lämplig avdelning, kund och miljö.

Utöver att tillhandahålla information om resurser och ägare gör taggar att Contoso kan addera och gruppera resurser och använda denna information för interna faktureringssyften.

Contoso måste visualisera sina Azure-tillgångar på ett sätt som passar företaget bäst. Till exempel per roll eller avdelning. Observera att resurserna inte behöver ligga i samma resursgrupp för att ha samma tagg. Contoso skapar en enkel taggtaxonomi så att alla använder samma taggar.

**Taggnamn** | **Värde**
--- | ---
CostCenter | 12345: Det måste vara ett giltigt kostnadsställe från SAP.
BusinessUnit | Namn på affärsenhet (från SAP). Matchar CostCenter.
ApplicationTeam | E-postalias för teamet som äger supporten för appen.
CatalogName | Namnet på appen eller ShareServices per tjänstkatalog som resursen stöder.
ServiceManager | E-postalias för ITIL Service Manager för resursen.
COBPriority | Prioritet som har angetts av företaget för affärskontinuitet och haveriberedskap. Värden från 1 till 5.
ENV | DEV, STG, PROD är möjliga värden. De står för utveckling, mellanlagring och produktion.

Exempel:

 ![Azure-taggar](./media/contoso-migration-infrastructure/azure-tag.png)

När taggen har skapats kommer Contoso att gå tillbaka och skapa nya principdefinitioner och principtilldelningar för att verkställa användningen av taggarna genom hela organisationen.

## <a name="step-6-consider-security"></a>Steg 6: Säkerhetsöverväganden

Säkerhet är viktigt i molnet och Azure tillhandahåller en mängd olika säkerhetsverktyg och -funktioner. De hjälper dig att skapa säkra lösningar på den säkra Azure-plattformen. Läs [Förtroende för det tillförlitliga molnet](https://azure.microsoft.com/overview/trusted-cloud) för att lära dig mer om Azure-säkerhet.

Det finns några aspekter för Contoso att tänka på:

- **Azure Security Center:** Azure Security Center erbjuder enhetlig säkerhetshantering och avancerat skydd mot hot i olika hybridmolnarbetsbelastningar. Med Security Center kan du tillämpa säkerhetsprinciper i arbetsbelastningarna, begränsa hotexponeringen samt identifiera och åtgärda attacker. [Läs mer](https://docs.microsoft.com/azure/security-center/security-center-intro).
- **Nätverkssäkerhetsgrupper:** En nätverkssäkerhetsgrupp är ett filter (brandvägg) som innehåller en lista över säkerhetsregler som tillåter eller nekar nätverkstrafik till resurser som är anslutna till virtuella Azure-nätverk (VNet). [Läs mer](https://docs.microsoft.com/azure/virtual-network/security-overview).
- **Datakryptering:** Med Azure Disk Encryption kan du kryptera IaaS-diskar för virtuella Windows- och Linux-datorer. [Läs mer](https://docs.microsoft.com/azure/security/azure-security-encryption-atrest).

### <a name="work-with-the-azure-security-center"></a>Arbeta med Azure Security Center

Contoso vill ha en snabbvisning av det nya hybridmolnets säkerhetsställning, i synnerhet för Azure-arbetsbelastningarna. Contoso har därför valt att implementera Azure Security Center och börjar med följande funktioner:

- Centraliserad principhantering
- Kontinuerlig utvärdering
- Användbara rekommendationer

#### <a name="centralize-policy-management"></a>Centraliserad principhantering

Med centraliserad principhantering kan Contoso säkerställa efterlevnad med säkerhetskrav genom att hantera principer centralt för hela miljön. De kan snabb och enkelt implementera en princip som gäller för samtliga Azure-resurser.

![Säkerhetsprincip](./media/contoso-migration-infrastructure/security-policy.png)

#### <a name="assess-and-action"></a>Utvärdera och vidta åtgärder

Contoso kan dra nytta av kontinuerlig säkerhetsbedömning som övervakar säkerheten i datorer, nätverk, lagring, data och program så att de kan identifiera potentiella säkerhetsproblem.

- Security Center analyserar säkerhetsläget för Contosos beräknings-, infrastruktur-och dataresurser och Azure-appar och -tjänster.
- Med kontinuerlig utvärdering kan Contosos driftsteam identifiera potentiella säkerhetsproblem, till exempel system som saknar säkerhetsuppdateringar eller exponerade nätverksportar.
- I synnerhet Contoso vill se till att alla virtuella datorer är skyddade. Security Center hjälper med detta, kontrollerar de virtuella datorernas hälsotillstånd och ger rekommenderade åtgärder för att åtgärda säkerhetssårbarheter innan de utnyttjas.

![Övervakning](./media/contoso-migration-infrastructure/monitoring.png)

### <a name="work-with-nsgs"></a>Arbeta med nätverkssäkerhetsgrupper

Contoso kan begränsa nätverkstrafiken till resurser i ett virtuellt nätverk med hjälp av nätverkssäkerhetsgrupper.

- En nätverkssäkerhetsgrupp innehåller en lista över säkerhetsregler som tillåter eller nekar inkommande eller utgående nätverkstrafik baserat på käll- eller mål-IP-adress, port och protokoll.
- När regler tillämpas för ett undernät tillämpas de för alla resurser i undernätet. Förutom nätverksgränssnitt omfattar detta även instanser av Azure-tjänster som distribuerats i undernätet.
- Med programsäkerhetsgrupper kan du konfigurera nätverkssäkerhet som ett naturligt tillägg till ett programs struktur, så att du kan gruppera virtuella datorer och definiera nätverkssäkerhetsprinciper baserat på dessa grupper.
  - Programsäkerhetsgrupper gör att Contoso kan återanvända sin säkerhetsprincip i stor skala utan manuellt underhåll av explicita IP-adresser. Plattformen hanterar komplexiteten med explicita IP-adresser och flera regeluppsättningar så att du kan fokusera på affärslogik.
  - Contoso kan ange en programsäkerhetsgrupp som källa och mål i en säkerhetsregel. När en säkerhetsprincip har definierats kan Contoso skapa virtuella datorer och tilldela de virtuella datorernas nätverkskort till en grupp.

Contoso implementerar en blandning av nätverkssäkerhetsgrupper och programsäkerhetsgrupper. Contoso oroar sig för hanteringen av nätverkssäkerhetsgrupper. Det oroar sig också för överanvändning av nätverkssäkerhetsgrupper och den ökade komplexiteten för driftspersonalen. Det här är vad Contoso planerar att göra:

- All trafik till och från alla undernät (nord-syd) kommer att omfattas av en nätverkssäkerhetsgruppregel, förutom för GatewaySubnets i hubbnätverket.
- Alla brandväggar eller domänkontrollanter kommer att skyddas av såväl undernätets nätverkssäkerhetsgrupp som nätverkskortets nätverkssäkerhetsgrupper.
- Alla produktionsprogram kommer att ha tillämpade programsäkerhetsgrupper.

Contoso har skapat en modell av hur detta kommer att se ut för dess program.

![Säkerhet](./media/contoso-migration-infrastructure/asg.png)

Nätverkssäkerhetsgrupperna som är associerade med programsäkerhetsgrupperna kommer att konfigureras med minst behörighet så att endast tillåtna paket kan flöda från en del av nätverket till målet.

**Åtgärd** | **Namn** | **Källa** | **Mål** | **Port**
--- | --- | --- | --- | ---
Allow | AllowiInternetToFE | VNET-HUB-EUS1/IB-TrustZone | APP1-FE 80, 443
Allow | AllowWebToApp | APP1-FE | APP1-APP | 80, 443
Allow | AllowAppToDB | APP1-APP | APP1-DB | 1433
Neka | DenyAllInbound | Any | Any | Any

### <a name="encrypt-data"></a>Kryptera data

Azure Disk Encryption integreras med Azure Key Vault så att du kan kontrollera och hantera diskkrypteringsnycklar och hemligheter i Key Vault-prenumerationen. Det säkerställer att alla data på virtuella datordiskar är krypterade i vila i Azure Storage.

- Contoso har avgjort att vissa virtuella datorer behöver kryptering.
- Contoso kommer att använda kryptering på virtuella datorer med kunddata, konfidentiella data eller PPI-data.

## <a name="conclusion"></a>Sammanfattning

I den här artikeln konfigurerade Contoso en Azure-infrastruktur och -policy för Azure-prenumeration, hybrididentifiering, haveriberedskap, nätverk, styrning och säkerhet.

Alla steg som utfördes av Contoso krävs inte för en migrering till molnet. I det här fallet ville man planera en nätverksinfrastruktur som kan användas för alla typer av migreringar och som är säker, elastisk och skalbar.

Med den här infrastrukturen på plats är Contoso redo att gå vidare och testa migreringen.

## <a name="next-steps"></a>Nästa steg

Nu när Contoso har konfigurerat sin Azure-infrastruktur är de redo att börja migrera arbetsbelastningar till molnet. Se avsnittet [översikt av migreringsmönster och -exempel](./contoso-migration-overview.md#windows-server-workloads) för ett urval av scenarier som använder den här exempelinfrastrukturen som migreringsmål.
