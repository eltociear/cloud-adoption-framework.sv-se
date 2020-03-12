---
title: Prioritera och definiera arbets belastningar för moln införande
description: Använd ramverket för moln införande för Azure för att lära dig hur du prioriterar och definierar arbets belastningar för en moln implementerings plan.
author: BrianBlanchard
ms.author: brblanch
ms.date: 07/01/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: plan
ms.openlocfilehash: 9f374bbe149e132fde4c44a8c0ecd9246615bac0
ms.sourcegitcommit: 388e32dd4861039149c846c926c0e9230cf28ae3
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/12/2020
ms.locfileid: "79140628"
---
# <a name="prioritize-and-define-workloads-for-a-cloud-adoption-plan"></a>Prioritera och definiera arbets belastningar för en moln implementerings plan

Att upprätta tydliga, åtgärds bara prioriteringar är en av hemligheterna för att genomföra molnet. Det naturliga frestelsen är att investera tid i att definiera alla arbets belastningar som kan påverkas under moln införande. Men det är counterproductive, särskilt tidigt i införande processen.

I stället rekommenderar vi att ditt team fokuserar på att noggrant prioritera och dokumentera de första 10 arbets belastningarna. När implementeringen av implementerings planen har påbörjats kan teamet underhålla en lista över de näst 10 högsta prioritets arbets belastningarna. Den här metoden ger tillräckligt med information för att planera för kommande iterationer.

Genom att begränsa planen till 10 arbets belastningar uppmuntrar du flexibiliteten och justeringen av prioriteringar när affärs villkoren ändras. Den här metoden gör det också utrymme för moln implementerings teamet att lära sig och förfina uppskattningar. Viktigast är att det tar bort omfattande planering som en barriär för effektiv affärs förändring.

<!-- markdownlint-disable MD026 -->

## <a name="what-is-a-workload"></a>Vad är en arbets belastning?

I samband med ett moln införande är en arbets belastning en samling IT-tillgångar (servrar, virtuella datorer, program, data eller apparater) som gemensamt stöder en definierad process. Arbets belastningar kan ha stöd för mer än en process. Arbets belastningar kan också vara beroende av andra delade till gångar eller större plattformar. En arbets belastning bör dock ha definierade gränser för beroende till gångar och de processer som är beroende av arbets belastningen. Ofta kan arbets belastningar visualiseras genom att övervaka nätverks trafiken mellan IT-tillgångar.

## <a name="prerequisites"></a>Förutsättningar

De strategiska inmatningarna från krav listan gör följande uppgifter mycket enklare att utföra. Om du behöver hjälp med att samla in data som beskrivs i den här artikeln granskar du [kraven](./prerequisites.md).

## <a name="initial-workload-prioritization"></a>Inledande arbets belastnings prioritering

Under den [stegvisa rationalisering](../digital-estate/rationalize.md)bör ditt team enas om en "kraft med 10"-metod, som består av 10 prioriterade arbets belastningar. Dessa arbets belastningar fungerar som en ursprunglig gränser för införande av planering.

Om du bestämmer att en digital egendom rationalisering inte behövs, rekommenderar vi att moln implementerings teamen och moln strategi teamet samtycker till en lista med 10 program som fungerar som migreringens första fokus. Vi rekommenderar att de här 10 arbets belastningarna innehåller en blandning av enkla arbets belastningar (färre än 10 resurser i en fristående distribution) och mer avancerade arbets belastningar. De 10 arbets belastningarna startar prioriterings processen för arbets belastning.

> [!NOTE]
> Kraften hos 10 fungerar som en ursprunglig gränser för planering, för att fokusera på energi och investering i tidiga analyser. Arbetet med att analysera och definiera arbets belastningar kan dock orsaka ändringar i listan över prioriterade arbets belastningar.

## <a name="add-workloads-to-your-cloud-adoption-plan"></a>Lägg till arbets belastningar i din moln implementerings plan

I föregående artikel, [Cloud adoption plan och Azure DevOps](./template.md)skapade du en moln implementerings plan i Azure DevOps.

Du kan nu representera arbets belastningarna i den kraftfulla 10-listan i din moln implementerings plan. Det enklaste sättet att göra detta är via Mass redigering i Microsoft Excel. Om du vill förbereda din arbets station för Mass redigering, se [Mass Lägg till eller ändra arbets objekt med Excel](https://docs.microsoft.com/azure/devops/boards/backlogs/office/bulk-add-modify-work-items-excel?view=azure-devops).

Steg 5 i artikeln visar att du kan välja **indatalistor**. Välj i stället **fråge lista**. Välj sedan frågan **arbets belastnings mal len** i list rutan **Välj en fråga** . Den frågan läser in alla ansträngningar som rör migreringen av en enskild arbets belastning i kalkyl bladet.

När arbets uppgifterna för arbets belastnings mal len har lästs in följer du de här stegen för att börja lägga till nya arbets belastningar:

1. Kopiera alla objekt som har taggen för **arbets belastnings mal len** i den högra kolumnen längst till höger.
2. Klistra in de kopierade raderna under det sista rad objektet i tabellen.
3. Ändra rubrik cellen för den nya funktionen från **arbets belastnings mal len** till namnet på din nya arbets belastning.
4. Klistra in cellen ny arbets belastnings namn i kolumnen tagg för alla rader under den nya funktionen. Var noga med att inte ändra taggar eller namn på de rader som är relaterade till funktionen faktisk **arbets belastnings mal len** . Du kommer att behöva dessa arbets uppgifter när du lägger till nästa arbets belastning i moln implementerings planen.
5. Gå vidare till steg 8 i Mass redigerings anvisningarna för att publicera kalkyl bladet. Det här steget skapar alla arbets objekt som krävs för att migrera din arbets belastning.

Upprepa steg 1 till 5 för var och en av arbets belastningarna i 10-listans potens.

## <a name="define-workloads"></a>Definiera arbets belastningar

När de ursprungliga prioriteterna har definierats och arbets belastningar har lagts till i planen, kan var och en av arbets belastningarna definieras genom djupare kvalitativ analys. Innan du inkluderar en arbets belastning i moln implementerings planen försöker du tillhandahålla följande data punkter för varje arbets belastning.

### <a name="business-inputs"></a>Affärs indata

| Data punkt | Beskrivning | Indata |
|---|---|---|
| Arbets belastnings namn | Vad heter den här arbets belastningen? |         |
| Arbets belastnings Beskrivning | Vad gör den här arbets belastningen i en mening? |         |
| Antagande motivation | Vilken av de här arbets belastningarna för moln införande påverkas? |         |
| Primär sponsor | Av dessa intressenter påverkas, vilket är den primära sponsor som begär föregående motivation? |         |
| Affärsenhet | Vilken affär senhet ansvarar för kostnaden för den här arbets belastningen? |         |
| Affärs processer | Vilka affärs processer kommer att påverkas av ändringar i arbets belastningen? |         |
| Företags team | Vilka affärs team kommer att påverkas av ändringar? |         |
| Affärs intressenter | Finns det några chefer vars verksamhet kommer att påverkas av ändringar? |         |
| Affärsresultat | Hur mäter företaget resultatet av den här ansträngningen? |         |
| Mått | Vilka mått ska användas för att spåra framgång? |         |
| Efterlevnad | Finns det några krav på tredje parts efterlevnad för den här arbets belastningen? |         |
| Program ägare | Vem är det som är konto för påverkan på program som är kopplade till den här arbets belastningen? |         |
| Låsnings perioder för företag | Finns det några tillfällen då företaget inte tillåter ändringar? |         |
| Geografiska områden | Påverkas de geografiska områden som påverkas av den här arbets belastningen? |         |

### <a name="technical-inputs"></a>Tekniska inmatningar

| Data punkt | Beskrivning | Indata |
|---|---|---|
| Implementerings metod | Är detta en kandidat för migrering eller innovation? |         |
| Lead för programops | Visar en lista över de parter som ansvarar för prestanda och tillgänglighet för den här arbets belastningen. |         |
| Serviceavtal | Visa en lista över service nivå avtal (RTO/återställnings krav). |         |
| Allvarlighets grad | Visa en lista över den aktuella program kritiskheten. |         |
| Dataklassificering | Ange klassificeringen av data känslighet. |         |
| Drifts geografiska områden | Lista de geografiska områden där arbets belastningen är eller bör vara värd. |         |
| Program | Ange en inledande lista eller ett antal program som ingår i den här arbets belastningen. |         |
| Virtuella datorer | Ange en inledande lista eller antal virtuella datorer eller servrar som ingår i arbets belastningen. |         |
| Datakällor | Ange en inledande lista eller ett antal data källor som ingår i arbets belastningen. |         |
| Beroenden | Lista de till gångs beroenden som inte ingår i arbets belastningen. |         |
| Geografiska diagram över användar trafik | Visa en lista över geografiska diagram med en betydande samling användar trafik. |         |

## <a name="confirm-priorities"></a>Bekräfta prioriteter

Baserat på de sammanställda data bör moln strategi teamet och molnet för att utvärdera prioriteringarna uppfyllas. Att klargöra affärs data punkter kan göra ändringar i prioriteringar. Teknisk komplexitet eller beroenden kan leda till ändringar som rör personal tilldelningar, tids linjer eller sekvenser av tekniska ansträngningar.

Efter en granskning bör båda teamen vara bekanta med att bekräfta de resulterande prioriteringarna. Den här uppsättningen med dokumenterade, validerade och bekräftade prioriteringar är den prioriterade efter släpning i molnet.

## <a name="next-steps"></a>Nästa steg

För alla arbets belastningar i den prioriterade moln implementeringen är teamet nu redo att [Justera till gångar](./assets.md).

> [!div class="nextstepaction"]
> [Justera till gångar för prioriterade arbets belastningar](./assets.md)
