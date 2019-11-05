---
title: Anpassa design guiden för moln styrning med företags principer
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Anpassa design guiden för moln styrning med företags principer
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.openlocfilehash: 6b3fd0ca16bf54e5eaf026037ba1f59c2043f4e7
ms.sourcegitcommit: bf9be7f2fe4851d83cdf3e083c7c25bd7e144c20
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 11/04/2019
ms.locfileid: "73566153"
---
# <a name="align-your-cloud-governance-design-guide-with-corporate-policy"></a>Anpassa design guiden för moln styrning med företags principer

När du har [definierat moln principer](./policy-definition.md) baserat på dina [identifierade risker](./business-risk.md)måste du skapa en åtgärds bara vägledning som överensstämmer med dessa principer för IT-personal och utvecklare som ska referera till. Genom att skapa en design guide för moln styrning kan du ange olika struktur-, teknik-och bearbetnings alternativ baserat på de princip satser som du har genererat för var och en av de [fem styrnings ämnes områden](../governance-disciplines.md).

En design guide för moln styrning bör upprätta arkitektur val och design mönster för var och en av kärn infrastrukturs komponenterna i moln distributioner som bäst uppfyller dina princip krav. Tillsammans med dessa bör du tillhandahålla en övergripande förklaring av den teknik, de verktyg och processer som har stöd för var och en av dessa design beslut.

Även om analys-och policy instruktionerna i en viss grad kan vara moln plattforms oberoende, bör din design guide tillhandahålla plattformsspecifik implementerings information som dina IT-och dev-team kan använda när de skapar och distribuerar molnbaserade arbets belastningar. Fokusera på arkitekturen, verktygen och funktionerna i din valda plattform när du fattar design beslut och ger vägledning.

Även om Cloud design guiderna bör ta hänsyn till några av de tekniska uppgifter som är associerade med varje infrastruktur komponent, är de inte avsedda att vara omfattande tekniska dokument eller specifikationer. Se till att dina guider innehåller dina princip instruktioner och tydligt tillstånds design beslut i ett format som är enkelt för personalen att förstå och referera till.

<!-- markdownlint-enable MD033 -->

## <a name="use-the-actionable-governance-guides"></a>Använd de stödda styrnings guiderna

Om du planerar att använda Azure-plattformen för ditt moln införande, tillhandahåller moln implementerings ramverket [stöd linjer för styrning](../guides/index.md) som illustrerar den stegvisa metoden för organisations modellen för moln införande ramverk. De här vägledningarna innehåller en mängd vanliga antagande scenarier, inklusive affärs risker, tolerans krav och policy-instruktioner som ingick i att skapa en minimal livskraftig produkt (MVP) för styrning. De här guiderna visar en sammanfattning av verklig kund upplevelse av moln införande processen i Azure.

Varje moln implementering har unika mål, prioriteringar och utmaningar, och dessa exempel bör ge en lämplig mall för att konvertera principen till vägledning. Välj det bästa scenariot för din situation som utgångs punkt och forma det så att det passar dina specifika princip behov.

## <a name="next-steps"></a>Nästa steg

Med design vägledning på plats kan du upprätta policys för att säkerställa efterlevnad av principer.

> [!div class="nextstepaction"]
> [Upprätta policyer för princip överensstämmelse](./processes.md)
