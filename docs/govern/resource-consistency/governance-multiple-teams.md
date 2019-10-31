---
title: Styrnings design i Azure för flera team
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Vägledning för att konfigurera Azures styrnings kontroller för flera team, flera arbets belastningar och flera miljöer.
author: alexbuckgit
ms.author: abuck
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 5459d775051b831112029fe1502a62a13c21e1c2
ms.sourcegitcommit: e0a783dac15bc4c41a2f4ae48e1e89bc2dc272b0
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/30/2019
ms.locfileid: "73058765"
---
# <a name="governance-design-for-multiple-teams"></a>Styrningsdesign för flera team

Målet med den här vägledningen är att hjälpa dig att lära dig att utforma en resurs styrnings modell i Azure som stöd för flera team, flera arbets belastningar och flera miljöer. Först ska du titta på en uppsättning hypotetiska styrnings krav och sedan gå igenom flera exempel på implementeringar som uppfyller dessa krav.

Kraven är:

- Företaget planerar att överta nya moln roller och ansvars områden till en uppsättning användare och därför kräver identitets hantering för flera team med olika resurs åtkomst behov i Azure. Detta identitets hanterings system krävs för att lagra identiteten för följande användare:
  - Den person i organisationen som ansvarar för ägarskapet av **prenumerationer**.
  - Den person i organisationen som ansvarar för de **delade infrastruktur resurser** som används för att ansluta ditt lokala nätverk till ett virtuellt Azure-nätverk.
  - Två personer i din organisation som ansvarar för att hantera en **arbets belastning**.
- Stöd för flera **miljöer**. En miljö är en logisk gruppering av resurser, t. ex. virtuella datorer, virtuella nätverk och nätverks trafik tjänster för routning. Dessa resurs grupper har liknande hanterings-och säkerhets krav och används vanligt vis för ett särskilt ändamål, till exempel testning eller produktion. I det här exemplet är kravet för fyra miljöer:
  - En **delad infrastruktur miljö** som innehåller resurser som delas av arbets belastningar i andra miljöer. Till exempel ett virtuellt nätverk med ett Gateway-undernät som ger anslutning till lokalt.
  - En **produktions miljö** med de mest restriktiva säkerhets principerna. Kan omfatta interna eller externa riktade arbets belastningar.
  - En för **produktions miljö** för utveckling och testning. Den här miljön har säkerhets-, efterlevnads-och kostnads principer som skiljer sig från dem i produktions miljön. I Azure tar detta en Enterprise Dev/Test prenumerations form.
  - En **sand Box miljö** för koncept bevis-och utbildnings syfte. Den här miljön tilldelas vanligt vis per medarbetare som deltar i utvecklings aktiviteter och har strikt procedur-och drift säkerhets kontroller på plats för att förhindra att företags data Informas här. I Azure har dessa formen av Visual Studio-prenumerationer. Dessa prenumerationer bör _inte_ heller vara knutna till företagets Azure Active Directory.
- En **behörighets modell med minst privilegium** där användare saknar behörighet som standard. Modellen måste ha stöd för följande:
  - En enda betrodd användare (som behandlas som ett tjänst konto) i prenumerations omfånget med behörighet att tilldela resurs åtkomst rättigheter.
  - Varje arbets belastnings ägare nekas åtkomst till resurser som standard. Resurs åtkomst behörighet beviljas uttryckligen av den enda betrodda användaren i resurs grupps omfånget.
  - Hanterings åtkomst för resurserna för delad infrastruktur är begränsad till ägare av den delade infrastrukturen.
  - Hanterings åtkomst för varje arbets belastning som är begränsad till arbets Belastningens ägare (i produktion) och ökande kontroll nivåer som utveckling ökar från dev till att testas till Prod.
  - Företaget vill inte behöva hantera roller oberoende av varandra i de tre huvud miljöerna och behöver därför bara använda [inbyggda roller](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles) som är tillgängliga i Azures rollbaserad åtkomst kontroll (RBAC). Om företaget absolut kräver anpassade RBAC-roller krävs ytterligare processer för att synkronisera anpassade roller i de tre miljöerna.
- Kostnads uppföljning per arbets belastnings ägarens namn, miljö eller både och.

## <a name="identity-management"></a>Identitetshantering

Innan du kan utforma identitets hantering för din styrnings modell är det viktigt att förstå de fyra huvud områdena som den omfattar:

- **Administration:** Processer och verktyg för att skapa, redigera och ta bort användar identitet.
- **Autentisering:** Verifierar användar identitet genom att verifiera autentiseringsuppgifter, till exempel användar namn och lösen ord.
- **Auktorisering:** Avgöra vilka resurser som en autentiserad användare får åtkomst till eller vilka åtgärder de har behörighet att utföra.
- **Granskning:** Granska loggar och annan information med jämna mellanrum för att identifiera säkerhets problem som rör användar identitet. Detta omfattar att granska misstänkta användnings mönster, granska användar behörigheter med jämna mellanrum för att kontrol lera att de är korrekta och andra funktioner.

Det finns bara en tjänst som är betrodd av Azure för identitet och som är Azure Active Directory (Azure AD). Du kommer att lägga till användare i Azure AD och använda det för alla funktioner som anges ovan. Men innan du tittar på hur du konfigurerar Azure AD är det viktigt att förstå de privilegierade konton som används för att hantera åtkomst till dessa tjänster.

När din organisation har registrerat sig för ett Azure-konto tilldelades minst en ägare till Azure- **kontot** . Dessutom har en Azure AD- **klient** skapats, om inte en befintlig klient organisation redan var kopplad till din organisations användning av andra Microsoft-tjänster som Office 365. En **Global administratör** med fullständig behörighet för Azure AD-klienten var associerad när den skapades.

Användar identiteter för både Azure-kontots ägare och den globala Azure AD-administratören lagras i ett mycket säkert identitets system som hanteras av Microsoft. Azure-kontots ägare har behörighet att skapa, uppdatera och ta bort prenumerationer. Den globala Azure AD-administratören har behörighet att utföra många åtgärder i Azure AD, men i den här design guiden fokuserar vi på att skapa och ta bort användar identitet.

> [!NOTE]
> Din organisation kanske redan har en befintlig Azure AD-klient om det finns en befintlig Office 365-, Intune-eller Dynamics-licens som är associerad med ditt konto.

Azure-kontots ägare har behörighet att skapa, uppdatera och ta bort prenumerationer:

![Azure-konto med Azure konto hanteraren och global administratör för Azure AD](../../_images/govern/design/governance-3-0.png)
*figur 1 – ett Azure-konto med en global administratör för konto hanteraren och Azure AD.*

Den globala Azure AD- **administratören** har behörighet att skapa användar konton:

![Azure-konto med Azure konto hanteraren och global administratör i Azure AD](../../_images/govern/design/governance-3-0a.png)
*figur 2 – den globala Azure AD-administratören skapar nödvändiga användar konton i klienten.*

De två första kontona, **APP1 arbets belastnings ägare** och **APP2 arbets belastnings ägare** är associerade med en individ i din organisation som ansvarar för att hantera en arbets belastning. **Nätverks åtgärds** kontot ägs av den person som ansvarar för resurserna för delad infrastruktur. Slutligen är **prenumerationens ägar** konto associerat med den person som ansvarar för ägarskapet för prenumerationer.

## <a name="resource-access-permissions-model-of-least-privilege"></a>Resurs åtkomst behörighets modell med minst privilegium

Nu när ditt identitets hanterings system och användar konton har skapats måste du bestämma hur du ska använda RBAC-roller (rollbaserad åtkomst kontroll) för varje konto som stöd för en behörighets modell med minst behörighet.

Det finns ett annat krav som anger att resurserna som är kopplade till varje arbets belastning isoleras från varandra så att ingen arbets belastnings ägare har hanterings åtkomst till någon annan arbets belastning som de inte äger. Det finns också ett krav för att implementera den här modellen med hjälp av inbyggda roller för rollbaserad åtkomst kontroll i Azure.

Varje RBAC-roll tillämpas på ett av tre omfång i Azure: **prenumeration**, **resurs grupp**och sedan en enskild **resurs**. Roller ärvs i lägre omfattning. Om en användare till exempel har tilldelats den [inbyggda ägar rollen](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#owner) på prenumerations nivån, tilldelas rollen även den användaren i resurs gruppen och den enskilda resurs nivån om den inte åsidosätts.

Därför måste du bestämma vilka åtgärder en viss typ av användare får ta med i vart och ett av dessa tre omfång för att kunna skapa en modell med behörigheter med lägst behörighet. Till exempel är kravet för en arbets belastnings ägare att ha behörighet att hantera åtkomst till de resurser som är kopplade till arbets belastningen och inga andra. Om du har tilldelat den inbyggda ägar rollen i prenumerations omfånget, skulle varje arbets belastnings ägare ha hanterings åtkomst till alla arbets belastningar.

Vi tar en titt på två exempel på behörighets modeller för att förstå det här konceptet lite bättre. I det första exemplet har modellen bara förtroende för tjänst administratören som skapar resurs grupper. I det andra exemplet tilldelar modellen den inbyggda ägar rollen till varje arbets belastnings ägare i prenumerations omfånget.

I båda exemplen finns en prenumerations tjänst administratör som har tilldelats den inbyggda ägar rollen i prenumerations omfånget. Kom ihåg att den inbyggda ägar rollen beviljar alla behörigheter, inklusive hantering av åtkomst till resurser.
![prenumerations tjänst administratör med ägar rollen](../../_images/govern/design/governance-2-1.png)
*bild 3 – en prenumeration med en tjänst administratör som har tilldelats den inbyggda ägar rollen.*

1. I det första exemplet finns **arbets belastnings ägare A** utan behörigheter i prenumerations omfånget – de har inga resurs åtkomst hanterings rättigheter som standard. Den här användaren vill distribuera och hantera resurserna för deras arbets belastning. De måste kontakta **tjänst administratören** för att begära att en resurs grupp skapas.
    ![arbets belastnings ägare begär skapande av resurs grupp A](../../_images/govern/design/governance-2-2.png)
2. **Tjänst administratören** granskar sin begäran och skapar **resurs grupp A**. I det här läget har **arbets belastnings ägaren** fortfarande inte behörighet att göra något.
    ![tjänst administratör skapar resurs grupp A](../../_images/govern/design/governance-2-3.png)
3. **Tjänst administratören** lägger till **arbets belastnings ägare a** i **resurs gruppen a** och tilldelar den [inbyggda rollen deltagare](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#contributor). Deltagar rollen beviljar alla behörigheter för **resurs gruppen A** förutom att hantera åtkomst behörighet.
    ![tjänst administratör lägger till arbets belastnings ägare a till resurs gruppen a](../../_images/govern/design/governance-2-4.png)
4. Vi antar att **arbets Belastningens ägare a** har krav på att ett par team medlemmar ska kunna visa data om processor-och nätverks trafiken som en del av kapacitets planeringen för arbets belastningen. Eftersom **arbets belastnings ägare A** tilldelas rollen deltagare har de inte behörighet att lägga till en användare i **resurs gruppen A**. De måste skicka denna begäran till **tjänst administratören**.
    ![arbets belastnings ägare begär arbets deltagare läggs till i resurs gruppen](../../_images/govern/design/governance-2-5.png)
5. **Tjänst administratören** granskar begäran och lägger till de två **arbets belastnings deltagarnas** användare i **resurs grupp A**. Ingen av dessa två användare kräver behörighet att hantera resurser, så de tilldelas den [inbyggda rollen läsare](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#contributor).
    ![tjänst administratör lägger till arbets belastnings deltagare i resurs gruppen A](../../_images/govern/design/governance-2-6.png)
6. Därefter kräver **arbets belastnings ägare B** också en resurs grupp som innehåller resurserna för deras arbets belastning. Precis som med **arbets belastnings ägare A**har **arbets belastnings ägaren B** inlednings vis inte behörighet att vidta några åtgärder i prenumerations omfånget, så de måste skicka en begäran till **tjänst administratören**.
    ![arbets belastnings ägare B begär Anden om att skapa resurs grupp B](../../_images/govern/design/governance-2-7.png)
7. **Tjänst administratören** granskar begäran och skapar **resurs grupp B**.  ![tjänst administratör skapar resurs grupp B](../../_images/govern/design/governance-2-8.png)
8. **Tjänst administratören** lägger sedan till **arbets belastnings ägare b** till **resurs grupp b** och tilldelar den inbyggda rollen deltagare.
    ![tjänst administratör lägger till arbets Belastningens ägare B till resurs grupp B](../../_images/govern/design/governance-2-9.png)

I det här läget är var och en av arbets belastnings ägarna isolerade i sin egen resurs grupp. Ingen av arbets belastnings ägarna eller deras grupp medlemmar har hanterings åtkomst till resurserna i någon annan resurs grupp.

![prenumeration med resurs grupper A och B](../../_images/govern/design/governance-2-10.png)
*figur 4 – en prenumeration med två arbets belastnings ägare isolerade med sin egen resurs grupp.*

Den här modellen är en modell med minst privilegium&mdash;varje användare tilldelas rätt behörighet i rätt resurs hanterings omfång.

Tänk dock på att alla aktiviteter i det här exemplet utfördes av **tjänst administratören**. Även om det här är ett enkelt exempel och kanske inte verkar vara ett problem eftersom det bara fanns två arbets belastnings ägare, är det lätt att tänka på vilka typer av problem som skulle leda till en stor organisation. **Tjänst administratören** kan till exempel bli en Flask hals med en stor efter släpning av begär Anden som resulterar i fördröjningar.

Vi tar en titt på det andra exemplet som minskar antalet uppgifter som utförs av **tjänst administratören**.

1. I den här modellen tilldelas **arbets belastnings ägare A** den inbyggda ägar rollen i prenumerations omfånget, vilket gör att de kan skapa sina egna resurs grupper: **resurs grupp A**.  ![tjänst administratör lägger till arbets belastnings ägare A i prenumerationen](../../_images/govern/design/governance-2-11.png)
2. När **resurs grupp a** skapas läggs **arbets Belastningens ägare A** till som standard och ärver den inbyggda ägar rollen från prenumerations omfånget.
    ![arbets belastnings ägare A skapar resurs grupp A](../../_images/govern/design/governance-2-12.png)
3. Den inbyggda ägar rollen ger **arbets belastnings ägaren** behörighet att hantera åtkomst till resurs gruppen. **Arbets belastnings ägare A** lägger till två **arbets belastnings deltagare** och tilldelar den inbyggda rollen rollen till var och en av dem.
    ![arbets belastnings ägare A lägger till arbets belastnings deltagare](../../_images/govern/design/governance-2-13.png)
4. **Tjänst administratören** lägger nu till **arbets belastnings ägare B** i prenumerationen med den inbyggda ägar rollen.
    ![tjänst administratör lägger till arbets belastnings ägare B i prenumerationen](../../_images/govern/design/governance-2-14.png)
5. **Arbets Belastningens ägare b** skapar **resurs grupp b** och läggs till som standard. Sedan ärver **arbets Belastningens ägare B** den inbyggda ägar rollen från prenumerations omfånget.
    ![arbets belastnings ägare B skapar resurs grupp B](../../_images/govern/design/governance-2-15.png)

Observera att i den här modellen utförde **tjänst administratören** färre åtgärder än de gjorde i det första exemplet på grund av delegeringen av hanterings åtkomst till var och en av de enskilda arbets belastnings ägarna.

![prenumeration med resurs grupper A och B](../../_images/govern/design/governance-2-16.png)
*figur 5 – en prenumeration med en tjänst administratör och två arbets belastnings ägare, som alla tilldelats den inbyggda ägar rollen.*

Men eftersom både **arbets belastnings ägare A** och **arbets belastnings ägare B** tilldelas den inbyggda ägar rollen i prenumerations omfånget, har de alla ärvda inbyggda ägar roller för var och en av resurs grupperna. Det innebär att inte bara har full åtkomst till en annans resurser, de kan också delegera hanterings åtkomst till var och en av resurs grupperna. Till exempel har **arbets Belastningens ägare B** behörighet att lägga till andra användare i **resurs gruppen A** och kan tilldela dem en roll, inklusive den inbyggda ägar rollen.

Om du jämför varje exempel med kraven ser du att båda exemplen har stöd för en enda betrodd användare i prenumerations omfånget med behörighet att bevilja resurs åtkomst behörighet till de två arbets belastnings ägarna. Var och en av de två arbets belastnings ägarna hade inte åtkomst till resurs hantering som standard och kräver att **tjänst administratören** uttryckligen tilldelar dem behörigheter. Men endast det första exemplet stöder kravet att de resurser som är kopplade till varje arbets belastning isoleras från varandra, så att ingen arbets belastnings ägare har åtkomst till resurserna för någon annan arbets belastning.

## <a name="resource-management-model"></a>Resurs hanterings modell

Nu när du har utformat en behörighets modell med minsta behörighet kan vi gå vidare och ta en titt på några praktiska program i dessa styrnings modeller. Kom ihåg krav som du måste ha stöd för följande tre miljöer:

1. **Miljö för delad infrastruktur:** En grupp resurser som delas av alla arbets belastningar. Detta är resurser som nätverks-gatewayer, brand väggar och säkerhets tjänster.
2. **Produktions miljö:** Flera grupper med resurser som representerar flera produktions arbets belastningar. Dessa resurser används för att vara värd för privata och offentliga program artefakter. Dessa resurser har vanligt vis de tätt flesta styrnings-och säkerhets modeller som skyddar resurserna, program koden och data från obehörig åtkomst.
3. För **produktions miljö:** Flera grupper med resurser som representerar flera färdiga arbets belastningar som inte är produktion. Dessa resurser används för utveckling och testning av dessa resurser kan ha en mer avslappnad styrnings modell för att ge ökad flexibilitet i utvecklare. Säkerheten i dessa grupper bör öka närmare "produktion" för att få en program utvecklings process.

För var och en av dessa tre miljöer finns det ett krav för att spåra kostnads data efter **arbets belastnings ägare**, **miljö**eller både och. Det innebär att du vill veta den kontinuerliga kostnaden för den **delade infrastrukturen**, kostnaderna för enskilda användare i både för produktions-och **produktions** miljöerna och slutligen den totala **kostnaden för för** **produktion och**  **produktions** miljöer.

Du har redan lärt dig att resurserna är begränsade till två nivåer: **prenumeration** och **resurs grupp**. Det första beslutet är därför att organisera miljöer efter **prenumeration**. Det finns bara två möjligheter: en enda prenumeration eller flera prenumerationer.

Innan du tittar på exempel på var och en av dessa modeller kan vi granska hanterings strukturen för prenumerationer i Azure.

Kom ihåg från kraven att du har en person i organisationen som ansvarar för prenumerationer, och den här användaren äger **prenumerations ägar** kontot i Azure AD-klienten. Detta konto har dock inte behörighet att skapa prenumerationer. Endast **Azure-kontots ägare** har behörighet att göra detta:

![en Azure-konto ägare skapar en prenumeration](../../_images/govern/design/governance-3-0b.png)
*figur 6 – en Azure-konto ägare skapar en prenumeration.*

När prenumerationen har skapats kan Azure- **kontots ägare** lägga till **prenumerationens ägar** konto till prenumerationen med **ägar** rollen:

![Azure-kontots ägare lägger till prenumerations ägarens användar konto i prenumerationen med ägar rollen.](../../_images/govern/design/governance-3-0c.png)
*figur 7 – ägaren av Azure-kontot lägger till användar kontot för **prenumerations ägare** i prenumerationen med **ägar** rollen.*

**Prenumerationens ägare** kan nu skapa **resurs grupper** och delegera resurs åtkomst hantering.

Först ska vi titta på ett exempel på en resurs hanterings modell med en enda prenumeration. Det första beslutet är att justera resurs grupper i de tre miljöerna. Du kan välja mellan två alternativ:

1. Justera varje miljö till en enda resurs grupp. Alla delade infrastruktur resurser distribueras till en enda **delad infrastruktur** resurs grupp. Alla resurser som är kopplade till utvecklings arbets belastningar distribueras till en enda **utvecklings** resurs grupp. Alla resurser som är kopplade till produktions arbets belastningar distribueras till en enda **produktions** resurs grupp för **produktions** miljön.
2. Skapa separata resurs grupper för varje arbets belastning med hjälp av en namn konvention och taggar för att justera resurs grupper med var och en av de tre miljöerna.

Vi börjar med att utvärdera det första alternativet. Du använder den behörighets modell som diskuterades i föregående avsnitt, med en enda prenumerations tjänst administratör som skapar resurs grupper och lägger till användare till dem med antingen den inbyggda rollen **deltagare** eller **läsare** .

1. Den första resurs gruppen som distribueras representerar den **delade infrastruktur** miljön. **Prenumerationens ägare** skapar en resurs grupp för resurserna för delade infrastrukturer med namnet `netops-shared-rg`.
    ![att skapa en resurs grupp](../../_images/govern/design/governance-3-0d.png)
2. **Prenumerations ägaren** lägger till **användar kontot för nätverks åtgärder** i resurs gruppen och tilldelar rollen **deltagare** .
    ![att lägga till en nätverks åtgärds användare](../../_images/govern/design/governance-3-0e.png)
3. **Nätverks drift användaren** skapar en [VPN-gateway](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways) och konfigurerar den för att ansluta till den lokala VPN-enheten. **Nätverks drifts** användaren använder också ett par med [taggar](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags) för var och en av resurserna: *miljö: Shared* och *managedBy: netOps*. När **prenumerations tjänst administratören** exporterar en kostnads rapport justeras kostnaderna med var och en av dessa taggar. På så sätt kan **prenumerations tjänst administratören** pivotera kostnader med hjälp av *miljö* tag gen och *managedBy* -taggen. Observera räknaren för **resurs gränser** överst till höger i bilden. Varje Azure-prenumeration har [tjänst begränsningar](https://docs.microsoft.com/azure/azure-subscription-service-limits)och hjälper dig att förstå effekterna av dessa gränser. du kommer att följa den virtuella nätverks gränsen för varje prenumeration. Det finns en gräns på 1000 virtuella nätverk per prenumeration och när det första virtuella nätverket har distribuerats finns det nu 999 tillgängligt.
    ![att skapa en VPN-gateway](../../_images/govern/design/governance-3-1.png)
4. Två fler resurs grupper har distribuerats. Det första heter `prod-rg`. Den här resurs gruppen är justerad till produktions miljön. Den andra heter `dev-rg` och justeras i utvecklings miljön. Alla resurser som är kopplade till produktions arbets belastningar distribueras till produktions miljön och alla resurser som är kopplade till utvecklings arbets belastningarna distribueras till utvecklings miljön. I det här exemplet distribuerar du bara två arbets belastningar till var och en av dessa två miljöer, så att du inte får några begränsningar för Azure-prenumerationen. Tänk dock på att varje resurs grupp har en gräns på 800 resurser per resurs grupp. Om du fortsätter att lägga till arbets belastningar i varje resurs grupp kommer den här gränsen att nås.
    ![skapa resurs grupper](../../_images/govern/design/governance-3-2.png)
5. Den första **arbets belastnings ägaren** skickar en begäran till **prenumerations tjänstens administratör** och läggs till i alla resurs grupper för utvecklings-och produktions miljön med **deltagar** rollen. Som du tidigare har lärt dig kan du använda rollen **deltagare** för att utföra andra åtgärder än att tilldela en roll till en annan användare. Den första **arbets belastnings ägaren** kan nu skapa de resurser som är kopplade till arbets belastningen.
    ![lägger till bidrags givare](../../_images/govern/design/governance-3-3.png)
6. Den första **arbets belastnings ägaren** skapar ett virtuellt nätverk i var och en av de två resurs grupperna med ett par virtuella datorer i var och en. Den första **arbets belastnings ägaren** använder *miljö* -och *managedBy* -taggarna för alla resurser. Observera att räknaren för Azure Service Limit nu är 997 virtuella nätverk kvar.
    ![att skapa virtuella nätverk](../../_images/govern/design/governance-3-4.png)
7. Vart och ett av de virtuella nätverken har ingen anslutning till lokalt när de skapas. I den här typen av arkitektur måste varje virtuellt nätverk peer-kopplas till *Hub-VNet* i den **delade infrastruktur** miljön. Peering av virtuella nätverk skapar en anslutning mellan två separata virtuella nätverk och tillåter att nätverks trafiken färdas mellan dem. Observera att peering av virtuella nätverk inte är transitivt. En peering måste anges i vart och ett av de två virtuella nätverk som är anslutna, och om bara ett av de virtuella nätverken anger att anslutningen är ofullständig. För att illustrera effekterna av detta anger den första **arbets belastnings ägaren** en peering mellan **Prod-VNet** och **Hub-VNet**. Den första peer kopplingen skapas, men inga trafikflöden eftersom kompletterande peering från **hubb-VNet** till **Prod-VNet** ännu inte har angetts. Den första **arbets belastnings ägaren** kontaktar **nätverks drifts** användaren och begär denna kompletterande peering-anslutning.
    ![att skapa en peering-anslutning](../../_images/govern/design/governance-3-5.png)
8. Användare av **nätverks åtgärder** granskar begäran, godkänner den och anger sedan peering i inställningarna för **hubb-VNet**. Peering-anslutningen är nu klar och nätverks trafiken flödar mellan de två virtuella nätverken.
    ![att skapa en peering-anslutning](../../_images/govern/design/governance-3-6.png)
9. Nu skickar en andra **arbets belastnings ägare** en begäran till **prenumerations tjänstens administratör** och läggs till i de befintliga resurs grupperna för **produktions** -och **utvecklings** miljön med **deltagar** rollen. Den andra **arbets belastnings ägaren** har samma behörigheter för alla resurser som den första **arbets belastnings ägaren** i varje resurs grupp.
    ![lägger till bidrags givare](../../_images/govern/design/governance-3-7.png)
10. Den andra **arbets belastnings ägaren** skapar ett undernät **i det virtuella** nätverket för virtuella nätverk och lägger sedan till två virtuella datorer. Den andra **arbets belastnings ägaren** använder *miljö* -och *managedBy* -taggarna för varje resurs.
    ![att skapa undernät](../../_images/govern/design/governance-3-8.png)

I den här exempel resurs hanterings modellen kan vi hantera resurser i de tre nödvändiga miljöerna. Resurserna för delad infrastruktur skyddas eftersom det bara finns en enda användare i prenumerationen med behörighet att komma åt dessa resurser. Var och en av arbets belastnings ägarna kan använda delade infrastruktur resurser utan att ha några behörigheter för själva delade resurser. Den här hanterings modellen uppfyller dock inte kraven för arbets belastnings isolering – var och en av de två **arbets belastnings ägarna** kan komma åt resurserna för den andra arbets belastningen.

Det finns ett annat viktigt övervägande för den här modellen som kanske inte är direkt uppenbar. I det här exemplet var det **APP1 arbets belastnings ägare** som begärde nätverks-peering **-anslutningen med hubb-VNet** för att tillhandahålla anslutning till lokalt. **Nätverks åtgärder** som användaren har utvärderat som begäran baserat på de resurser som distribueras med den arbets belastningen. När **prenumerations ägaren** har lagt till **APP2 arbets belastnings ägare** med **deltagar** rollen, hade den användaren hanterings behörighet för alla resurser i resurs gruppen **Prod-RG** .

![Diagram som visar hanterings behörighet](../../_images/govern/design/governance-3-10.png)

Det innebär att **APP2 arbets belastnings ägare** hade behörighet att distribuera sitt eget undernät med virtuella datorer i **det virtuella nätverket för virtuella** nätverk. Som standard har de virtuella datorerna nu till gång till det lokala nätverket. **Nätverks åtgärds** användaren är inte medveten om dessa datorer och godkände inte anslutningen till lokalt.

Nu ska vi titta på en enda prenumeration med flera resurs grupper för olika miljöer och arbets belastningar. Observera att i föregående exempel var resurserna för varje miljö lätt att identifiera eftersom de fanns i samma resurs grupp. Nu när du inte längre har grupperat, måste du förlita dig på en namngivnings konvention för resurs grupper för att kunna tillhandahålla den funktionen.

1. Resurserna för **delad infrastruktur** kommer fortfarande att ha en separat resurs grupp i den här modellen, vilket är detsamma. Varje arbets belastning kräver två resurs grupper – en för varje **utvecklings** -och **produktions** miljö. För den första arbets belastningen skapar **prenumerations ägaren** två resurs grupper. Det första heter **APP1-Prod-RG** och den andra heter **APP1-dev-RG**. Som tidigare nämnts identifierar den här namngivnings konventionen resurserna som associeras med den första arbets belastningen, **APP1**och antingen **utvecklings** -eller **produktions** miljön. *Prenumerations* ägaren lägger återigen till **APP1 arbets belastnings ägare** i resurs gruppen med **deltagar** rollen.
    ![lägger till bidrags givare](../../_images/govern/design/governance-3-12.png)
2. På samma sätt som i det första exemplet distribuerar **APP1 arbets belastnings ägare** ett virtuellt nätverk med namnet **APP1-Prod-VNet** till **produktions** miljön, och en annan namngiven **APP1-dev-VNet** i **utvecklings** miljön. **APP1 arbets belastnings ägare** skickar en begäran till användaren med **nätverks åtgärder** för att skapa en peering-anslutning. Observera att **APP1 arbets belastnings ägare** lägger till samma taggar som i det första exemplet och att begränsnings räknaren har minskats till 997 virtuella nätverk som återstår i prenumerationen.
    ![att skapa en peering-anslutning](../../_images/govern/design/governance-3-13.png)
3. **Prenumerationens ägare** skapar nu två resurs grupper för **APP2 arbets belastnings ägare**. Efter samma konventioner som för **APP1 arbets belastnings ägare**heter resurs grupperna **APP2-Prod-RG** och **APP2-dev-RG**. **Prenumerations ägaren** lägger till **APP2 arbets belastnings ägare** till varje resurs grupp med **deltagar** rollen.
    ![lägger till bidrags givare](../../_images/govern/design/governance-3-14.png)
4. *APP2 arbets belastnings ägare* distribuerar virtuella nätverk och virtuella datorer till resurs grupperna med samma namn konventioner. Taggar läggs till och begränsnings räknaren har minskats till 995 virtuella nätverk kvar i *prenumerationen*.
    ![distribution av virtuella nätverk och virtuella datorer](../../_images/govern/design/governance-3-15.png)
5. *APP2 arbets belastnings ägare* skickar en begäran till *nätverks drifts* användaren att peer *-nätverket APP2-net-VNet* med *hubb-VNet*. Den *nätverks åtgärd* som användaren skapar peering-anslutningen.
    ![att skapa en peering-anslutning](../../_images/govern/design/governance-3-16.png)

Den resulterande hanterings modellen liknar det första exemplet, med flera viktiga skillnader:

- Var och en av de två arbets belastningarna isoleras efter arbets belastning och miljö.
- Den här modellen krävde två fler virtuella nätverk än den första exempel modellen. Även om detta inte är en viktig skillnad med bara två arbets belastningar är den teoretiska gränsen för antalet arbets belastningar för den här modellen 24.
- Resurserna är inte längre grupperade i en enda resurs grupp för varje miljö. Gruppering av resurser kräver en förståelse för de namngivnings konventioner som används för varje miljö.
- Varje peer-kopplat virtuella nätverks anslutningar granskades och godkändes av *nätverks drifts* användaren.

Nu ska vi titta på en resurs hanterings modell med flera prenumerationer. I den här modellen kommer du att justera var och en av de tre miljöerna till en separat prenumeration: en prenumeration på **delade tjänster** , **produktions** prenumeration och slutligen en **utvecklings** prenumeration. Övervägandena för den här modellen liknar en modell som använder en enda prenumeration i som du måste bestämma för att justera resurs grupper till arbets belastningar. Redan fastställt är att skapa en resurs grupp för varje arbets belastning uppfyller kraven för arbets belastnings isolering, så du kommer att se den modellen i det här exemplet.

1. I den här modellen finns tre *prenumerationer*: *delad infrastruktur*, *produktion*och *utveckling*. Var och en av dessa tre prenumerationer kräver en *prenumerations ägare*, och i det enkla exemplet använder du samma användar konto för alla tre. Resurserna för *delad infrastruktur* hanteras på samma sätt som de två första exemplen ovan, och den första arbets belastningen är kopplad till *APP1-RG* i *produktions* miljön och samma resurs grupp med samma namn i *utvecklingen* miljö. *APP1 arbets belastnings ägare* läggs till i varje resurs grupp med *deltagar* rollen.
    ![lägger till bidrags givare](../../_images/govern/design/governance-3-17.png)
2. Som i de tidigare exemplen skapar *APP1 arbets belastnings ägare* resurserna och begär peering-anslutningen till det virtuella nätverket för *delad infrastruktur* . *APP1-arbetsbelastnings ägare* lägger bara till *managedBy* -taggen eftersom det inte längre behövs någon av *miljö* tag gen. Det innebär att resurserna är för varje miljö grupperade nu i samma *prenumeration* och att *miljö* tag gen är redundant. Begränsnings räknaren minskas till 999 virtuella nätverk kvar.
    ![att skapa en peering-anslutning](../../_images/govern/design/governance-3-18.png)
3. Slutligen upprepar *prenumerations ägaren* processen för den andra arbets belastningen och lägger till resurs grupperna med *APP2 arbets belastnings ägare* i * Contributor-rollen. Gräns räknaren för var och en av miljö prenumerationerna överförs till 998 virtuella nätverk kvar.

Den här hanterings modellen har fördelarna med det andra exemplet ovan. Den viktigaste skillnaden är dock att gränserna är mindre av ett problem på grund av att de är spridda över två *prenumerationer*. Nack delen är att kostnads data som spåras med taggar måste aggregeras i alla tre *prenumerationer*.

Därför kan du välja någon av dessa två exempel på resurs hanterings modeller, beroende på prioriteten för dina behov. Om du förväntar dig att din organisation inte ska uppnå tjänst gränserna för en enskild prenumeration kan du använda en enda prenumeration med flera resurs grupper. Om din organisation förväntar sig många arbets belastningar kan flera prenumerationer för varje miljö vara bättre.

## <a name="implementing-the-resource-management-model"></a>Implementera resurs hanterings modellen

Du har lärt dig om flera olika modeller för att styra åtkomsten till Azure-resurser. Nu ska du gå igenom de steg som krävs för att implementera resurs hanterings modellen med en prenumeration för var och en av de **delade infrastruktur**-, **produktions**-och **utvecklings** miljöerna från design guiden. Du har en **prenumerations ägare** för alla tre miljöer. Varje arbets belastning isoleras i en **resurs grupp** med en **arbets belastnings ägare** tillagd med **deltagar** rollen.

> [!NOTE]
> Läs [förstå resurs åtkomst i Azure](https://docs.microsoft.com/azure/role-based-access-control/rbac-and-directory-admin-roles) om du vill veta mer om relationen mellan Azure-konton och prenumerationer.

Följ de här stegen:

1. Skapa ett [Azure-konto](https://docs.microsoft.com/azure/active-directory/sign-up-organization) om din organisation inte redan har ett. Den person som registrerar sig för Azure-kontot blir Azures konto administratör och organisationens ledarskap måste välja en individ att anta den här rollen. Den här personen kommer att ansvara för:
    - Skapar prenumerationer.
    - Skapa och administrera [Azure Active Directory-klienter (Azure AD)](https://docs.microsoft.com/azure/active-directory/active-directory-whatis) som lagrar användar identitet för dessa prenumerationer.
2. Organisationens ledarskaps team bestämmer vilka personer som ansvarar för:
    - Hantering av användar identitet; en [Azure AD-klient](https://docs.microsoft.com/azure/active-directory/develop/active-directory-howto-tenant) skapas som standard när organisationens Azure-konto skapas och konto administratören läggs till som standard [Azure AD global administratör](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles) . Din organisation kan välja en annan användare för att hantera användar identitet genom [att tilldela rollen global administratör för Azure AD till användaren](https://docs.microsoft.com/azure/active-directory/active-directory-users-assign-role-azure-portal).
    - Prenumerationer, vilket innebär följande användare:
        - Hantera kostnader som är kopplade till resursanvändning i den prenumerationen.
        - Implementera och upprätthålla minsta behörighets modell för resurs åtkomst.
        - Håll koll på tjänst begränsningarna.
    - Delade infrastruktur tjänster (om organisationen bestämmer sig för att använda den här modellen), vilket innebär att den här användaren är ansvarig för:
        - Lokalt till Azure nätverks anslutning.
        - Ägande rätt till nätverks anslutning i Azure via peering av virtuella nätverk.
    - Arbets belastnings ägare.
3. Azure AD global-administratören [skapar nya användar konton](https://docs.microsoft.com/azure/active-directory/add-users-azure-active-directory) för:
    - Den person som ska vara **prenumerations ägare** för varje prenumeration som är associerad med varje miljö. Observera att detta bara är nödvändigt om prenumerations **tjänst administratören** inte kommer att behövas med hantering av resurs åtkomst för varje prenumeration/miljö.
    - Den person som ska vara **användare av nätverks åtgärder**.
    - De personer som är **arbets belastnings ägare**.
4. Azure-konto administratören skapar följande tre prenumerationer med hjälp av [Azure-konto portalen](https://account.azure.com):
    - En prenumeration för den **delade infrastruktur** miljön.
    - En prenumeration för **produktions** miljön.
    - En prenumeration för **utvecklings** miljön.
5. Azure-konto administratören [lägger till prenumerations tjänstens ägare i varje prenumeration](https://docs.microsoft.com/azure/billing/billing-add-change-azure-subscription-administrator#to-assign-a-user-as-an-administrator).
6. Skapa en godkännande process för **arbets belastnings ägare** för att begära att resurs grupper skapas. Godkännande processen kan implementeras på många sätt, t. ex. via e-post, eller så kan du använda ett process hanterings verktyg som [SharePoint-arbetsflöden](https://support.office.com/article/introduction-to-sharepoint-workflow-07982276-54e8-4e17-8699-5056eff4d9e3). Godkännande processen kan följa dessa steg:
    - **Ägaren av arbets belastningen** förbereder en struktur för nödvändiga Azure-resurser i antingen **utvecklings** miljön, **produktions** miljön eller både och skickar den till **prenumerations ägaren**.
    - **Prenumerations ägaren** granskar struktur listan och validerar de begärda resurserna för att säkerställa att de begärda resurserna är lämpliga för planerad användning, t. ex. för att kontrol lera att de begärda [storlekarna för virtuella datorer](https://docs.microsoft.com/azure/virtual-machines/windows/sizes) är eventuella.
    - Om begäran inte godkänns, meddelas **arbets Belastningens ägare** . Om begäran godkänns skapar **prenumerations ägaren** [den begärda resurs gruppen](https://docs.microsoft.com/azure/azure-resource-manager/manage-resource-groups-portal#create-resource-groups) enligt organisationens [namn konventioner](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions), och [lägger till **arbets belastnings ägaren** ](https://docs.microsoft.com/azure/role-based-access-control/role-assignments-portal#add-a-role-assignment) med [rollen **deltagare** ](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#contributor) och skickar ett meddelande till den **arbets belastnings ägare** som resurs gruppen har skapats.
7. Skapa en godkännande process för arbets belastnings ägare för att begära en virtuell nätverks-peering-anslutning från ägaren till den delade infrastrukturen. Som i föregående steg kan denna godkännande process implementeras med hjälp av e-post eller ett process hanterings verktyg.

Nu när du har implementerat styrnings modellen kan du distribuera dina delade infrastruktur tjänster.

## <a name="related-resources"></a>Relaterade resurser

[Inbyggda roller för Azure-resurser](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles)

## <a name="next-steps"></a>Nästa steg

> [!div class="nextstepaction"]
> [Lär dig mer om att distribuera en grundläggande infrastruktur](../../infrastructure/virtual-machines/basic-workload.md)
