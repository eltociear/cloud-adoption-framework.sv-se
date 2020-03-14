---
title: Planera för Azure Server Management Services
description: Lär dig mer om verktygen och Förbered dig för de resurser som krävs för att hantera Azure Server Management-tjänster.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 97d4b52b50f943dfd0e146e84d4e5fc5a1d97711
ms.sourcegitcommit: 5411c3b64af966b5c56669a182d6425e226fd4f6
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/13/2020
ms.locfileid: "79312624"
---
# <a name="phase-1-prerequisite-planning-for-azure-server-management-services"></a>Fas 1: planering för Azure Server Management Services som krävs

I den här fasen får du bekanta dig med Azure Server Management Suite med tjänster och planerar hur du distribuerar de resurser som behövs för att implementera dessa hanterings lösningar.

## <a name="understand-the-tools-and-services"></a>Förstå verktygen och tjänsterna

Granska [Azure Server Management-verktyg och-tjänster](./tools-services.md) för en detaljerad översikt över:

- De hanterings områden som ingår i pågående Azure-åtgärder.
- De Azure-tjänster och-verktyg som hjälper dig att stödja dig inom dessa områden.

Du ska använda flera av de här tjänsterna tillsammans för att uppfylla dina hanterings krav. Dessa verktyg refereras ofta till i den här vägledningen.

I följande avsnitt beskrivs planering och förberedelser som krävs för att använda dessa verktyg och tjänster.

## <a name="log-analytics-workspace-and-automation-account-planning"></a>Planera Log Analytics arbets yta och Automation-konto

Många av de tjänster som du ska använda för att publicera Azures hanterings tjänster kräver en Log Analytics arbets yta och ett länkat Azure Automation-konto.

En [Log Analytics-arbetsyta](https://docs.microsoft.com/azure/azure-monitor/learn/quick-create-workspace) är en unik miljö för lagring av Azure Monitor-loggdata. Varje arbetsyta har sitt eget datalager och sin egen konfiguration. Datakällor och lösningar konfigureras för att lagra data i specifika arbetsytor. Azure-övervakningslösningar kräver att alla servrar är anslutna till en arbetsyta, så att det går att lagra och komma åt deras loggdata.

Vissa av hanterings tjänsterna kräver ett [Azure Automation](https://docs.microsoft.com/azure/automation/automation-intro) -konto. Du använder det här kontot och funktionerna i Azure Automation för att integrera Azure-tjänster och andra offentliga system för att distribuera, konfigurera och hantera dina Server hanterings processer.

Följande Azure Server Management Services kräver en länkad Log Analytics arbets yta och ett Automation-konto:

- [Azure-Uppdateringshantering](https://docs.microsoft.com/azure/automation/automation-update-management)
- [Ändringsspårning och inventering](https://docs.microsoft.com/azure/automation/change-tracking)
- [Hybrid Runbook Worker](https://docs.microsoft.com/azure/automation/automation-hybrid-runbook-worker)
- [Önskad tillstånds konfiguration](https://docs.microsoft.com/azure/virtual-machines/extensions/dsc-overview)

Den andra fasen i den här vägledningen fokuserar på att distribuera tjänster och automation-skript. Det visar hur du skapar en Log Analytics-arbetsyta och ett Automation-konto. Den här vägledningen visar också hur du använder Azure Policy för att säkerställa att nya virtuella datorer är anslutna till rätt arbets yta.

Exemplen i den här vägledningen förutsätter en distribution som inte redan har servrar som har distribuerats till molnet. Mer information om principerna och överväganden vid planering av dina arbets ytor finns i [Hantera loggdata och arbets ytor i Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/platform/manage-access).

## <a name="planning-considerations"></a>Planera överväganden

Tänk på följande när du förbereder de arbets ytor och konton som du behöver för onboarding Management Services:

- **Azure-geografiska områden och regelefterlevnad:** Azure-regioner är indelade i *geografiska*områden. En [Azure-geografi](https://azure.microsoft.com/global-infrastructure/geographies) säkerställer att data placering, suveränitet, efterlevnad och återhämtnings krav uppfylls inom geografiska gränser. Om dina arbets belastningar omfattas av data suveränitet eller andra krav på efterlevnad måste arbets ytor och Automation-konton distribueras till regioner i samma Azure-geografi som de arbets belastnings resurser som de stöder.
- **Antal arbets ytor:** Som en GUID-princip skapar du det minsta antal arbets ytor som krävs per Azure-geografi. Vi rekommenderar minst en arbets yta för varje Azure-geografi där dina beräknings-eller lagrings resurser finns. Den här inledande justeringen hjälper till att undvika framtida reglerings problem när du migrerar data till olika geografiska områden.
- **Data kvarhållning och capping:** Du kan också behöva vidta data lagrings principer eller capping krav för data behandling när du skapar arbets ytor eller Automation-konton. Mer information om dessa principer och ytterligare överväganden vid planering av arbets ytor finns [i hantera loggdata och arbets ytor i Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/platform/manage-access).
- **Region mappning:** Länkning av en Log Analytics-arbetsyta och ett Azure Automation-konto stöds bara mellan vissa Azure-regioner. Om Log Analytics arbets ytan till exempel finns i *östra* regionen måste det länkade Automation-kontot skapas i *EastUS2* -regionen som ska användas med hanterings tjänster. Om du har ett Automation-konto som har skapats i en annan region kan det inte länka till en arbets yta i *öster*. Valet av distributions region kan kraftigt påverka kraven för Azure geografi. Kontakta [region mappnings tabellen](https://docs.microsoft.com/azure/automation/how-to/region-mappings) för att avgöra vilken region som ska vara värd för dina arbets ytor och Automation-konton.
- **Multihoming för arbets yta:** Azure Log Analytics-agenten stöder multihoming i vissa situationer, men agenten har flera begränsningar och utmaningar när de körs i den här konfigurationen. Om Microsoft inte har rekommenderat det för ditt scenario rekommenderar vi inte att du konfigurerar multihoming på den Log Analytics agenten.

## <a name="resource-placement-examples"></a>Exempel på resurs placering

Det finns flera olika modeller för att välja den prenumeration där du placerar Log Analytics-arbetsytan och automation-kontot. I korthet placerar du arbets ytan och automation-kontona i en prenumeration som ägs av teamet som ansvarar för att implementera tjänsten Uppdateringshantering och Ändringsspårning-och inventerings tjänsten.

Följande är exempel på några sätt att distribuera arbets ytor och Automation-konton.

### <a name="placement-by-geography"></a>Placering efter geografi

Små och medel stora miljöer har en enda prenumeration och flera hundra resurser som sträcker sig över flera Azure-geografiska områden. I dessa miljöer skapar du en Log Analytics arbets yta och ett Azure Automation konto i varje geografi.

Du kan skapa en arbets yta och ett Azure Automation konto, som ett par, i varje resurs grupp. Distribuera sedan paret i motsvarande geografi till de virtuella datorerna.

Om dina principer för inkompatibilitet inte dikterar resurserna i vissa regioner kan du skapa ett par för att hantera alla virtuella datorer. Vi rekommenderar också att du placerar arbets ytans och automations konto par i separata resurs grupper för att ge mer detaljerad rollbaserad åtkomst kontroll (RBAC).

Exemplet i följande diagram har en prenumeration med två resurs grupper som var och en finns i en annan geografi:

![Arbets ytans modell för små till medel stora miljöer](./media/workspace-model-small.png)

### <a name="placement-in-a-management-subscription"></a>Placering i en hanterings prenumeration

Större miljöer omfattar flera prenumerationer och har en central IT-avdelning som äger övervakning och efterlevnad. I dessa miljöer skapar du par av arbets ytor och Automation-konton i en IT-hanterings prenumeration. I den här modellen lagrar virtuella dator resurser i ett geografiskt data i motsvarande geografi arbets yta i IT-hanterings prenumerationen. Om program team behöver köra automatiserings uppgifter men inte kräver länkade arbets ytor och Automation-konton, kan de skapa separata Automation-konton i sina egna program prenumerationer.

![Arbets ytans modell för stora miljöer](./media/workspace-model-large.png)

### <a name="decentralized-placement"></a>Decentraliserad placering

I en alternativ modell för stora miljöer kan program utvecklings teamet vara ansvarig för korrigering och hantering. I det här fallet placerar du arbets ytans och automation-kontots par i program team prenumerationerna tillsammans med andra resurser.

  ![Arbets ytans konto modell för decentraliserade miljöer](./media/workspace-model-decentralized.png)

## <a name="create-a-workspace-and-automation-account"></a>Skapa en arbets yta och ett Automation-konto

När du har valt det bästa sättet att placera och organisera arbets ytor och konto par måste du se till att du har skapat dessa resurser innan du påbörjar onboarding-processen. I automatiserings exemplen senare i den här vägledningen skapar du en arbets yta och ett Automation-konto par åt dig. Men om du vill publicera med hjälp av Azure Portal och du inte har en befintlig arbets yta och ett Automation-konto måste du skapa ett.

Om du vill skapa en Log Analytics-arbetsyta med hjälp av Azure Portal går du till [skapa en arbets yta](https://docs.microsoft.com/azure/azure-monitor/learn/quick-create-workspace#create-a-workspace). Skapa sedan ett matchande Automation-konto för varje arbets yta genom att följa stegen i [skapa ett Azure Automation konto](https://docs.microsoft.com/azure/automation/automation-quickstart-create-account).

> [!NOTE]
> När du skapar ett Automation-konto med hjälp av Azure Portal försöker portalen som standard att skapa kör som-konton för både Azure Resource Manager och de klassiska distributions modell resurserna. Om du inte har klassiska virtuella datorer i din miljö och du inte är medadministratör i prenumerationen skapar portalen ett Kör som-konto för Resource Manager, men genererar ett fel när du distribuerar det klassiska kör som-kontot. Om du inte tänker använda klassiska resurser kan du ignorera det här felet.
>
> Du kan också skapa kör som-konton med hjälp av [PowerShell](https://docs.microsoft.com/azure/automation/manage-runas-account#creating-a-run-as-account-using-powershell).

## <a name="next-steps"></a>Nästa steg

Lär dig hur du kan [publicera dina servrar](./onboarding-overview.md) till Azure Server Management Services.

> [!div class="nextstepaction"]
> [Publicera till Azure Server Management Services](./onboarding-overview.md)
