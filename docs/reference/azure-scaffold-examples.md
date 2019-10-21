---
title: Scenarier och exempel för prenumerations styrning
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Innehåller exempel på hur du implementerar Azures prenumerations styrning för vanliga scenarier.
author: rdendtler
ms.author: rodend
ms.date: 01/03/2017
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: reference
ms.openlocfilehash: ffda6a8f11954895e934f310c1a53c95fb2e1351
ms.sourcegitcommit: b30952f08155513480c6b2c47a40271c2b2357cf
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/15/2019
ms.locfileid: "72378048"
---
# <a name="examples-of-implementing-azure-enterprise-scaffold"></a>Exempel på implementering av Azure Enterprise-Autogenerera

> [!NOTE]
> Azure Enterprise-ramverk har integrerats i Microsoft Cloud adoptions ramverket. Innehållet i den här artikeln visas nu i avsnittet [klart](../ready/index.md) i det nya ramverket. Den här artikeln är inaktuell i början av 2020. Om du vill börja använda den nya processen går du till [klar översikt](../ready/index.md), [skapar din första landnings zon](../ready/azure-setup-guide/migration-landing-zone.md)och/eller de överväganden som finns i [landnings zonen](../ready/considerations/index.md).

Den här artikeln innehåller exempel på hur ett företag kan implementera rekommendationer för en [Azure Enterprise-Autogenerera](./azure-scaffold.md). Det använder ett fiktivt företag som heter Contoso för att illustrera bästa praxis för vanliga scenarier.

## <a name="background"></a>Bakgrund

Contoso är ett globalt företag som tillhandahåller lösningar för leverans kedja för kunder. De tillhandahåller allt från en program vara som en tjänst modell till en distribuerad distribuerad modell lokalt. De utvecklar program vara i hela världen med viktiga utvecklings Center i Indien, USA och Kanada.

ISV-delen av företaget är indelad i flera oberoende affär senheter som hanterar produkter i en betydande verksamhet. Varje affär senhet har sina egna utvecklare, produkt chefer och arkitekter.

Företaget för ETS (Enterprise Technology Services) tillhandahåller centraliserad IT-kapacitet och hanterar flera data Center där affär senheter är värdar för sina program. Tillsammans med att hantera data Center, ger ETS-organisationen och hanterar centraliserat samarbete (till exempel e-post och webbplatser) och nätverks-/telefoni tjänster. De hanterar också kund riktade arbets belastningar för mindre affär senheter som inte har drift personal.

Följande personer används i den här artikeln:

- Dave är den ETS Azure-administratören.
- Alice är Contosos utvecklings chef i affär senheten för leverans kedjan.

Contoso måste bygga en branschspecifika app och en app som riktas mot kund. Den har valt att köra apparna på Azure. Dave läser artikeln för förebyggande [prenumerations styrning](./azure-scaffold.md) och är redo att implementera rekommendationerna.

## <a name="scenario-1-line-of-business-application"></a>Scenario 1: branschspecifika program

Contoso bygger ett BitBucket (Source Code Management System) som ska användas av utvecklare över hela världen. Programmet använder IaaS (Infrastructure as a Service) för att vara värd för och består av webb servrar och en databas server. Utvecklare får åtkomst till servrar i sina utvecklings miljöer, men de behöver inte åtkomst till servrarna i Azure. Contoso ETS vill tillåta att program ägaren och teamet hanterar programmet. Programmet är endast tillgängligt i Contosos företags nätverk. Dave måste konfigurera prenumerationen för det här programmet. Prenumerationen kommer också att vara värd för annan program vara som är relaterad till utvecklare i framtiden.

### <a name="naming-standards-and-resource-groups"></a>Namngivnings standarder och resurs grupper

Dave skapar en prenumeration som stöder utvecklingsverktyg som är gemensamma för alla affär senheter. Dave måste skapa meningsfulla namn för prenumerationen och resurs grupperna (för programmet och nätverken). Han skapar följande prenumeration och resurs grupper:

| Objekt | Namn | Beskrivning |
| --- | --- | --- |
| Prenumeration |Contoso ETS DeveloperTools-produktion |Stöder vanliga utvecklarverktyg |
| Resursgrupp |BitBucket-Prod-rg |Innehåller programmets webb server och databas server |
| Resursgrupp |corenetworks-Prod-rg |Innehåller virtuella nätverk och plats-till-plats-Gateway-anslutning |

### <a name="role-based-access-control"></a>Rollbaserad åtkomstkontroll

När du har skapat sin prenumeration vill du se till att lämpliga team och program ägare kan komma åt sina resurser. Dave känner av att varje team har olika krav. Han använder grupper som har synkroniserats från Contosos lokala Active Directory för att Azure Active Directory och ger rätt åtkomst nivå till teamen.

Dave tilldelar följande roller för prenumerationen:

| Roll | Tilldelad | Beskrivning |
| --- | --- | --- |
| [Ägare](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#owner) |Hanterat ID från Contosos lokala Active Directory |Detta ID styrs av just-in-Time (JIT)-åtkomst via Contosos identitets hanterings verktyg och säkerställer att prenumerationens ägar åtkomst är fullständigt granskad |
| [Säkerhets läsare](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#security-reader) |Avdelning för säkerhets-och risk hantering |Med den här rollen kan användare se Azure Security Center och status för resurserna |
| [Nätverksdeltagare](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#network-contributor) |Nätverks team |Med den här rollen kan Contosos nätverks team hantera plats-till-plats-VPN och virtuella nätverk |
| *Anpassad roll* |Program ägare |Dave skapar en roll som ger möjlighet att ändra resurser i resurs gruppen. Mer information finns i [anpassade roller i Azure RBAC](https://docs.microsoft.com/azure/role-based-access-control/custom-roles) |

### <a name="policies"></a>Policy

Dave har följande krav för att hantera resurser i prenumerationen:

- Eftersom utvecklings verktygen har stöd för utvecklare över hela världen vill han inte hindra användare från att skapa resurser i någon region. Han behöver dock veta var resurserna skapas.
- Han är bekymrad över kostnaderna. Därför vill han förhindra att program ägare skapar onödigt dyra virtuella datorer.
- Eftersom det här programmet hanterar utvecklare i många affär senheter vill han tagga varje resurs med affär senheten och program ägaren. Genom att använda dessa taggar kan ETS fakturera lämpliga team.

Han skapar följande principer via [Azure policy](https://docs.microsoft.com/azure/azure-policy/azure-policy-introduction):

| Fält | Verkan | Beskrivning |
| --- | --- | --- |
| location |Händelse |Granska skapandet av resurserna i vilken region som helst |
| typ |autentiseringsregel |Neka skapande av virtuella datorer i G-serien |
| tags |autentiseringsregel |Kräv program ägar tag gen |
| tags |autentiseringsregel |Kräv kostnads ställe tag gen |
| tags |slå |Lägg till tagg namn **BusinessUnit** och tagg värde **ETS** till alla resurser |

### <a name="resource-tags"></a>Resurstaggar

Dave vet att han måste ha en speciell information på fakturan för att identifiera kostnads stället för BitBucket-implementeringen. Dessutom vill Dave veta alla resurser som ETS äger.

Han lägger till följande [taggar](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags) i resurs grupperna och resurserna.

| Taggnamn | Tagg värde |
| --- | --- |
| ApplicationOwner |Namnet på den person som hanterar det här programmet |
| CostCenter |Kostnads Center för den grupp som betalar för Azure-förbrukningen |
| BusinessUnit |**ETS** (affär senheten som är associerad med prenumerationen) |

### <a name="core-network"></a>Kärn nätverk

Contosos informations säkerhets-och riskhanterings team granskar Daves föreslagna plan för att flytta programmet till Azure. De vill se till att programmet inte är synligt för Internet. Dave har också appar för utvecklare som i framtiden kommer att flyttas till Azure. De här apparna kräver offentliga gränssnitt. För att uppfylla dessa krav tillhandahåller han både interna och externa virtuella nätverk och en nätverks säkerhets grupp för att begränsa åtkomsten.

Han skapar följande resurser:

| Resurstyp | Namn | Beskrivning |
| --- | --- | --- |
| Virtual Network |internt-VNet |Används med BitBucket-programmet och är anslutet via ExpressRoute till Contosos företags nätverk. Ett undernät (`bitbucket`) tillhandahåller programmet med ett specifik IP-adressutrymme |
| Virtual Network |externt-VNet |Tillgängligt för framtida program som kräver offentliga slut punkter |
| Nätverkssäkerhetsgrupp |BitBucket – NSG |Säkerställer att den här arbets Belastningens attack yta minimeras genom att endast tillåta anslutningar på port 443 för under nätet där programmet finns (`bitbucket`) |

### <a name="resource-locks"></a>Resurs lås

Dave känner av att anslutningen från Contosos företags nätverk till det interna virtuella nätverket måste skyddas från alla Wayward-skript eller oavsiktlig borttagning.

Han skapar följande [resurs lås](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-lock-resources):

| Lås typ | Resurs | Beskrivning |
| --- | --- | --- |
| **CanNotDelete** |internt-VNet |Hindrar användare från att ta bort det virtuella nätverket eller undernät, men förhindrar inte tillägg av nya undernät |

### <a name="azure-automation"></a>Azure Automatisering

Dave har inget att automatisera för det här programmet. Även om han skapade ett Azure Automation-konto, används den inte för första gången.

### <a name="azure-security-center"></a>Azure Security Center

Contoso-Hantering av IT-tjänster (ITSM) måste snabbt identifiera och hantera hot. De vill också veta vilka problem som kan finnas.

För att uppfylla dessa krav aktiverar Dave [Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-intro) och ger åtkomst till rollen säkerhets läsare.

## <a name="scenario-2-customer-facing-app"></a>Scenario 2: kundriktad app

Företaget som är ledande i leverans kedjans affär senhet har identifierat olika möjligheter att öka engagemang med Contosos kunder genom att använda ett förmåns kort. Alices team måste skapa det här programmet och avgöra att Azure ökar sin förmåga att möta företagets behov. Alice arbetar med Dave från ETS för att konfigurera två prenumerationer för utveckling och drift av det här programmet.

### <a name="azure-subscriptions"></a>Azure-prenumerationer

Dave loggar in på Azure-Enterprise Portal och ser att avdelningen för leverans kedjan redan finns. Men eftersom det här projektet är det första utvecklings projektet för leverans kedjans team i Azure, känner Dave igen behovet av ett nytt konto för Alices utvecklings team. Han skapar kontot "R & D" för hennes team och tilldelar åtkomst till Alice. Alice loggar in via Azure Portal och skapar två prenumerationer: en för att hålla utvecklings servrarna och en för att hålla produktions servrarna. Hon följer de tidigare etablerade namngivnings standarderna när de skapade följande prenumerationer:

| Användning av prenumeration | Namn |
| --- | --- |
| Utveckling |Contoso SupplyChain ResearchDevelopment LoyaltyCard Development |
| Produktion |Contoso SupplyChain-åtgärder LoyaltyCard produktion |

### <a name="policies"></a>Policy

Dave och Alice diskuterar programmet och identifierar att det här programmet endast tjänar kunder i Nord amerikanska regionen. Alice och hennes team plan för att använda Azures program tjänst miljö och Azure SQL för att skapa programmet. De kan behöva skapa virtuella datorer under utvecklingen. Alice vill se till att deras utvecklare har de resurser de behöver för att utforska och undersöka problem utan att behöva hämta ETS.

För **utvecklings prenumerationen**skapar de följande princip:

| Fält | Verkan | Beskrivning |
| --- | --- | --- |
| location |Händelse |Granska skapandet av resurserna i vilken region som helst |

De begränsar inte vilken typ av SKU en användare kan skapa under utveckling och de kräver inte taggar för några resurs grupper eller resurser.

För **produktions prenumerationen**skapar de följande principer:

| Fält | Verkan | Beskrivning |
| --- | --- | --- |
| location |autentiseringsregel |Förhindra att några resurser skapas utanför USA-datacentren |
| tags |autentiseringsregel |Kräv program ägar tag gen |
| tags |autentiseringsregel |Kräv avdelnings tagg |
| tags |slå |Lägg till tagg i varje resurs grupp som visar produktions miljön |

De begränsar inte vilken typ av SKU som en användare kan skapa i produktion.

### <a name="resource-tags"></a>Resurstaggar

Dave vet att han måste ha speciell information för att identifiera rätt affärs grupper för fakturering och ägande. Han definierar resurs taggar för resurs grupper och resurser.

| Taggnamn | Tagg värde |
| --- | --- |
| ApplicationOwner |Namnet på den person som hanterar det här programmet |
| Avdelning |Kostnads Center för den grupp som betalar för Azure-förbrukningen |
| EnvironmentType |**Produktion** (även om prenumerationen omfattar **produktion** i namnet, inklusive den här taggen möjliggör enkel identifiering när du tittar på resurser i portalen eller på fakturan) |

### <a name="core-networks"></a>Kärn nätverk

Contosos informations säkerhets-och riskhanterings team granskar Daves föreslagna plan för att flytta programmet till Azure. De vill se till att programmet för lojalitets kort är korrekt isolerat och skyddat i ett DMZ nätverk. För att uppfylla detta krav, kan du med Dave och Alice skapa ett externt virtuellt nätverk och en nätverks säkerhets grupp för att isolera förmåns kort programmet från contoso företags nätverk.

För **utvecklings prenumerationen**skapar de:

| Resurstyp | Namn | Beskrivning |
| --- | --- | --- |
| Virtual Network |internt-VNet |Hanterar utvecklings miljön contoso lojalitets kort och är ansluten via ExpressRoute till Contosos företags nätverk |

För **produktions prenumerationen**skapar de:

| Resurstyp | Namn | Beskrivning |
| --- | --- | --- |
| Virtual Network |externt-VNet |Är värd för programmet för förmåns kort och är inte anslutet direkt till Contosos ExpressRoute. Koden skickas via deras käll kods system direkt till PaaS-tjänsterna. |
| Nätverkssäkerhetsgrupp |loyaltycard – NSG |Säkerställer att angrepps ytan för den här arbets belastningen minimeras genom att endast tillåta Inbound kommunikation på TCP 443. Contoso undersöker också användningen av en brand vägg för webbaserade program för ytterligare skydd. |

### <a name="resource-locks"></a>Resurs lås

Dave och Alice ger och bestämmer sig för att lägga till resurs lås på några av nyckel resurserna i miljön för att förhindra oavsiktlig borttagning under en Errant kod-push.

De skapar följande Lås:

| Lås typ | Resurs | Beskrivning |
| --- | --- | --- |
| **CanNotDelete** |externt-VNet |Förhindra att personer tar bort det virtuella nätverket eller undernät. Låset förhindrar inte tillägg av nya undernät |

### <a name="azure-automation"></a>Azure Automatisering

Alice och hennes utvecklings team har omfattande Runbooks för att hantera miljön för det här programmet. Runbooks gör det möjligt att lägga till/ta bort noder för programmet och andra DevOps-uppgifter.

Om du vill använda dessa Runbooks aktiverar du [Automation](https://docs.microsoft.com/azure/automation/automation-intro).

### <a name="azure-security-center"></a>Azure Security Center

Contoso-Hantering av IT-tjänster (ITSM) måste snabbt identifiera och hantera hot. De vill också veta vilka problem som kan finnas.

För att uppfylla dessa krav aktiverar Dave Azure Security Center. Han ser till att Azure Security Center övervakar resurserna och ger åtkomst till DevOps-och säkerhets teamen.

## <a name="next-steps"></a>Nästa steg

- Mer information om hur du skapar Resource Manager-mallar finns i [metod tips för att skapa Azure Resource Manager mallar](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-template-best-practices).
