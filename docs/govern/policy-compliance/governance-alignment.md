---
title: Anpassa styrnings utformningen till företags principen
description: Använd ramverket för moln införande för Azure för att lära dig hur du skapar arkitektur val och design mönster som uppfyller dina princip krav.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.openlocfilehash: b68710606f0b361caec66e390e3ac826c1944a2e
ms.sourcegitcommit: af45c1c027d7246d1a6e4ec248406fb9a8752fb5
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 02/27/2020
ms.locfileid: "77708401"
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
