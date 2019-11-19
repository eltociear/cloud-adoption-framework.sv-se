---
title: Distribuera moln implementerings planen till Azure DevOps
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Distribuera mallen för moln implementerings planen
author: BrianBlanchard
ms.author: brblanch
ms.date: 07/01/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: plan
ms.openlocfilehash: 8860fe9f4c689d2d2072a3a494b42c58b532a524
ms.sourcegitcommit: 50788e12bb744dd44da14184b3e884f9bddab828
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 11/18/2019
ms.locfileid: "74160549"
---
# <a name="cloud-adoption-plan-and-azure-devops"></a>Moln implementerings plan och Azure-DevOps

Azure DevOps är en uppsättning molnbaserade verktyg för Azure-kunder som hanterar repetitiva projekt. Den innehåller också verktyg för att hantera distributions pipeliner och andra viktiga aspekter av DevOps. 

I den här artikeln får du lära dig hur du snabbt distribuerar en efter släpning till Azure DevOps med hjälp av en mall för att planera en moln implementering. Den här mallen justerar moln implementerings ansträngningarna till en standardiserad process baserat på vägledningen i moln implementerings ramverket.

## <a name="create-your-cloud-adoption-plan"></a>Skapa en implementerings plan för molnet

Om du vill distribuera implementerings planen för molnet öppnar du [Azure DevOps demo Generator](https://aka.ms/adopt/plan/generator). Det här verktyget distribuerar mallen till din Azure DevOps-klient. Följande steg krävs för att använda verktyget:

1. Kontrol lera att det **valda fältet Mall** är inställt på **moln implementerings plan**. Om den inte är det väljer du **Välj mall** för att välja rätt mall.
2. Välj din Azure DevOps-organisation i list rutan **Välj organisation** .
3. Ange ett namn för det nya projektet. Moln implementerings planen kommer att ha det här namnet när det distribueras till din Azure DevOps-klient.
4. Välj **skapa projekt** om du vill skapa ett nytt projekt i din klient organisation, baserat på plan mal len. I förlopps indikatorn visas hur du distribuerar projektet.
5. När distributionen är färdig väljer du **navigera till projekt** för att se det nya projektet.

När projektet har skapats kan du fortsätta med den här artikel serien och se hur du kan ändra mallen så att den passar din moln implementerings plan.

Ytterligare support och vägledning för det här verktyget finns i [demo generator för Azure DevOps Services](https://docs.microsoft.com/azure/devops/demo-gen/?toc=/azure/devops/demo-gen/toc.json&bc=/azure/devops/demo-gen/breadcrumb/toc.json&view=azure-devops).

## <a name="bulk-edit-the-cloud-adoption-plan"></a>Mass redigering av moln införande planen

När plan projektet har distribuerats kan du använda Microsoft Excel för att ändra det. Det är mycket enklare att skapa nya arbets belastningar eller resurser i planen genom att använda Excel än genom att använda Azure DevOps webb läsar upplevelse.

Om du vill förbereda din arbets station för Mass redigering, se [Mass Lägg till eller ändra arbets objekt med Excel](https://docs.microsoft.com/azure/devops/boards/backlogs/office/bulk-add-modify-work-items-excel?view=azure-devops).

## <a name="use-the-cloud-adoption-plan"></a>Använd moln implementerings planen

Moln implementerings planen organiserar aktiviteter efter aktivitets typ:

- **Epics:** En *episka* representerar en övergripande fas i moln införande livs cykel.
- **Funktioner:** Funktionerna används för att organisera vissa mål i varje fas. Migreringen av en speciell arbets belastning skulle till exempel vara en funktion.
- **Användar berättelser:** Användar nyhets gruppen fungerar i logiska samlingar av aktiviteter baserat på ett speciellt mål.
- **Uppgifter:** Aktiviteter är det faktiska arbetet som ska utföras.

På varje lager sekvenseras aktiviteter baserat på beroenden. Aktiviteterna är länkade till artiklar i moln implementerings ramverket för att klargöra målet eller uppgiften i handen.

Den tydligaste vyn av moln implementerings planen kommer från vyn **Epics** efter släpning. Information om hur du ändrar till vyn **Epics** efter släpning finns i artikeln om att [Visa en efter släpning](https://docs.microsoft.com/azure/devops/boards/backlogs/define-features-epics?view=azure-devops#view-a-backlog-or-portfolio-backlog). I den här vyn är det enkelt att planera och hantera det arbete som krävs för att slutföra den aktuella fasen av livs cykeln för införande.

> [!NOTE]
> Det aktuella läget för moln implementerings planen fokuserar kraftigt på migrering. Uppgifter som rör styrning, innovation eller åtgärder måste fyllas i manuellt.

## <a name="align-the-cloud-adoption-plan"></a>Justera moln implementerings planen

Översikts sidorna för strategi-och planerings faserna i moln implementerings livs cykeln varje referens för [strategin för moln införande ramverk och planering](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/Microsoft-Cloud-Adoption-Framework-Strategy-and-Plan-Template.docx). Mallen organiserar de beslut och data punkter som ska justera mallen för moln implementerings planen med dina egna planer. Om du inte redan har gjort det kanske du vill slutföra övningarna som är relaterade till [strategin](../strategy/index.md) och [Planera](../plan/index.md) innan du justerar det nya projektet.

Följande artiklar stöder justering av moln implementerings planen:

- [Arbets belastningar](./workloads.md): justera funktionerna i molnmigrering episka för att avbilda varje arbets belastning som ska migreras eller förvaras. Lägg till och ändra dessa funktioner för att samla in ansträngningen för att migrera de 10 främsta arbets belastningarna.
- [Till gångar](./assets.md): varje till gång (virtuell dator, program eller data) representeras av användarnas berättelser under varje arbets belastning. Lägg till och ändra dessa användar berättelser så att de passar din digitala egendom.
- [Rationalisering](./review-rationalization.md): när varje arbets belastning definieras kan de första antagandena om den arbets belastningen anropas. Detta kan leda till ändringar i aktiviteterna under varje till gång.
- [Skapa versions planer](./iteration-paths.md): upprepnings Sök vägar upprättar versions planer genom att justera ansträngningarna med olika versioner och iterationer.
- [Upprätta tids linjer](./timelines.md): definiera start-och slutdatum för varje iteration skapar en tids linje för att hantera det övergripande projektet.

Dessa fem artiklar hjälper till med var och en av de justerings uppgifter som krävs för att börja hantera dina implementerings åtgärder. Nästa steg hjälper dig att komma igång med justerings övningen.

## <a name="next-steps"></a>Nästa steg

Börja justera ditt plan projekt genom att [definiera och prioritera arbets belastningar](./workloads.md).

> [!div class="nextstepaction"]
> [Definiera och prioritera arbets belastningar](./workloads.md)
