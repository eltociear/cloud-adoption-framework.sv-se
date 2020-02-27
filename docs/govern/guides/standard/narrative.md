---
title: 'Standard företags styrning: efter eget styrnings strategi'
description: Använd ramverket för moln införande för Azure för att lära dig hur du etablerar ett användnings fall för styrning under en vanlig distributions resa i Enterprise Cloud.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: d963053806a6a43476c7597be5dd628b6e187e06
ms.sourcegitcommit: af45c1c027d7246d1a6e4ec248406fb9a8752fb5
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 02/27/2020
ms.locfileid: "77709285"
---
# <a name="standard-enterprise-governance-guide-the-narrative-behind-the-governance-strategy"></a>Standard styrnings guide för företag: de som står bakom styrnings strategin

I följande beskrivare beskrivs användnings fallet för styrning under en [standard företags införande resa i molnet](./index.md). Innan du implementerar resan är det viktigt att förstå antaganden och rationella som återges i den här informationen. Sedan kan du bättre justera styrnings strategin till din egen organisations resa.

## <a name="back-story"></a>Bak text

Brädet för regissörer startade året med planer på att Förstärk företaget på flera olika sätt. De använder sig av ledarskap för att förbättra kund upplevelsen för att få marknads andelar. De skickas också för nya produkter och tjänster som kommer att placera företaget som en tanke ledare i branschen. De initierade också en parallell ansträngning för att minska avfallet och avskurna onödiga kostnader. Även om skrämma, visar åtgärds tavlan och ledarskap att denna ansträngning fokuserar så mycket kapital som möjligt vid framtida tillväxt.

Tidigare har företagets informations chef uteslutits från dessa strategiska konversationer. Men eftersom den framtida synen är kopplad till teknisk tillväxt, har den ett säte i tabellen som hjälper dig att hjälpa dessa stora planer. Nu förväntas vi leverera på nya sätt. Teamet är inte för beredda för dessa ändringar och det är sannolikt att det är svårt med inlärnings kurvan.

## <a name="business-characteristics"></a>Företagsegenskaper

Företaget har följande affärs profil:

- Alla försäljning och åtgärder finns i ett enda land, med en låg andel globala kunder.
- Verksamheten fungerar som en enda affär senhet med budgeterad till funktioner, inklusive försäljning, marknadsföring, åtgärder och IT.
- De flesta affärsvyer som en kapital dränering eller ett kostnads ställe.

## <a name="current-state"></a>Nuvarande tillstånd

Här är det aktuella läget för företagets IT-och moln åtgärder:

- DEN fungerar i två miljöer med värdbaserade infrastrukturer. En miljö innehåller produktions till gångar. Den andra miljön innehåller haveri beredskap och vissa dev/test-tillgångar. Dessa miljöer finns i två olika leverantörer. DEN refererar till dessa två Data Center som Prod respektive DR.
- DEN angav molnet genom att migrera alla e-postkonton för slutanvändare till Office 365. Migreringen slutfördes för sex månader sedan. Några andra IT-tillgångar har distribuerats till molnet.
- Program utvecklings teamen arbetar i en dev/test-kapacitet för att lära sig mer om moln funktioner.
- Business Intelligences gruppen (BI) experimenterar med Big data i molnet och för att granska data på nya plattformar.
- Företaget har en löst definierad princip som anger att personlig kund information och ekonomiska data inte kan hanteras i molnet, vilket begränsar verksamhets kritiska program i de aktuella distributionerna.
- IT-investeringar styrs av stora av kapital kostnaden. Dessa investeringar planeras årligen. Under de senaste åren har investeringar inkluderat lite mer än grundläggande underhålls krav.

## <a name="future-state"></a>Framtida tillstånd

Följande ändringar förväntas under de närmaste åren:

- INFORMATIONS gruppen är att granska principen om personliga data och finansiella data för att tillåta framtida tillstånds mål.
- Program utvecklingen och BI-teamen vill frisläppa molnbaserade lösningar för produktion under de närmaste 24 månaderna, baserat på vad som krävs för kund engagemang och nya produkter.
- Det här året kommer IT-teamet att avsluta arbets belastningarna för haveri beredskap i DR-datacenter genom att migrera 2 000-VM: ar till molnet. Detta förväntas ge en uppskattad kostnad på $25M USD under de kommande fem åren.
    ![lokala kostnader jämfört med Azure-kostnader som demonstrerar en avkastning på $25M USD under de kommande fem åren](../../../_images/govern/calculator-small-to-medium-enterprise.png)
- Företaget planerar att ändra hur det gör IT-investeringar genom att flytta in den utbetalade kapital kostnaden som en drifts kostnad i den. Den här ändringen ger bättre kostnads kontroll och gör det möjligt för IT att påskynda andra planerade insatser.

## <a name="next-steps"></a>Nästa steg

Företaget har utvecklat en företags princip för att forma styrnings implementeringen. Företags principen innehåller många av de tekniska besluten.

> [!div class="nextstepaction"]
> [Granska den inledande företags principen](./initial-corporate-policy.md)
