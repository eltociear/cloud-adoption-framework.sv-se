---
title: Förutsättningar för migrering
description: Förstå de förutsättningar som hjälper dig att förbereda för migrering till molnet och undvika vanliga orsaker till migreringsfel.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: eb7d0c8b0ee6ebd328ffd4807199e0b0e2620d35
ms.sourcegitcommit: 238e7a06b56950cebdcc8f75924849fc995e6ff2
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 02/12/2020
ms.locfileid: "77173326"
---
# <a name="prerequisites-for-migration"></a>Förutsättningar för migrering

Innan du påbörjar migrering måste _miljön_ för ditt migreringsmål förberedas för de kommande ändringarna. I det här fallet avser miljö den tekniska grunden i molnet. Miljö innebär även den företagsmiljö och det tankesätt som driver migreringen. På samma sätt omfattar miljön kulturen i de team som genomför ändringarna samt dem som tar emot resultatet. Bristande förberedelser för dessa ändringar är den vanligaste orsaken till misslyckade migreringar. Den här artikelserien går igenom de föreslagna förutsättningarna för att förbereda miljön.

## <a name="objective"></a>Mål

Säkerställa affärsmässig, kulturell och teknisk beredskap innan en iterativ migreringsplan påbörjas.

## <a name="review-business-drivers"></a>Granska affärsdrivande faktorer

Innan du påbörjar molnmigrering bör du läsa vägledningen för [Planera](../../../strategy/index.md) och [Redo](../../../ready/index.md) i Cloud Adoption Framework så att organisationen är förberedd inför processerna för molnimplementering och migrering. I synnerhet bör du granska de affärskrav och förväntade resultat som driver migreringen:

- [Komma igång: Migrera](../../../getting-started/migrate.md)
- [Varför går vi över till molnet?](../../../strategy/motivations.md)

## <a name="definition-of-done"></a>Definitionen av *klar*

Förutsättningarna uppfylls när följande bekräftas:

- **Affärsmässig beredskap.** Molnstrategiteamet har definierat och prioriterat en uppgiftslista på hög nivå för migrering som representerar den del av den digitala egendomen som ska migreras i de kommande två eller tre lanseringarna. Molnstrategiteamet och molnimplementeringsteamet har kommit överens om en inledande strategi för ändringshantering.
- **Kulturell beredskap.** Roller, ansvarsområden och förväntningar för molnimplementeringsteamet, molnstrategiteamet samt berörda användare har godkänts vad gäller de arbetsbelastningar som ska migreras i de kommande två eller tre lanseringarna.
- **Teknisk beredskap.** Den landningszon (eller allokerat värdutrymme i molnet) som tar emot de migrerade tillgångarna uppfyller minimikraven för att hantera den första migrerade arbetsbelastningen.

> [!CAUTION]
> Förberedelse är nyckeln till framgång för migrering. Dock kan överdrivet mycket förberedelse leda till *analysförlamning*, där för mycket tid som ägnas åt planering kan fördröja migrering avsevärt. De processer och krav som definieras i det här avsnittet är avsedda att hjälp dig fatta beslut, men låt dem inte hindra dig från att ta dig igenom processen.
>
> Välj en relativt enkel arbetsbelastning för den inledande migreringen. Använd de processer som beskrivs i det här avsnittet när du planerar och implementerar den här första migreringen. Arbetet med den första migreringen utgör en snabb demonstration av molnprinciper för ditt team och gör att de lär sig hur molnet fungerar. Allt eftersom teamet bygger på erfarenheten bör du införa dessa kunskaper vid genomförandet av större och mer komplexa migreringar.

## <a name="accountability-during-prerequisites"></a>Ansvarstagande under förutsättningar

Två team ansvarar för beredskap under fasen för förutsättningar:

- **Molnstrategiteamet:** Den här teamet ansvarar för att identifiera och prioritera de första två eller tre arbetsbelastningar som är kandidater för migrering.
- **Molnimplementeringsteamet:** Det här teamet ansvarar för att validera beredskapen hos den tekniska miljön och gångbarheten med att migrera de föreslagna arbetsbelastningarna.

En enskild medlem från varje grupp ska identifieras som ansvarig för var och en av de tre definitionerna av ”klar” i föregående avsnitt.

## <a name="responsibilities-during-prerequisites"></a>Ansvarsområden under förutsättningar

Utöver det övergripande ansvaret finns det åtgärder som en person eller en grupp måste vara direkt ansvarig för. Här följer några sådana ansvarsområden som påverkar dessa aktiviteter:

- **Affärsprioritering.** Fatta affärsbeslut om de arbetsbelastningar som ska migreras samt allmänna begränsningar vad gäller tidsschemat. Mer information finns i avsnittet om [affärsmotiveringar gällande molnmigrering](../../../strategy/motivations.md).
- **Beredskap för ändringshantering.** Upprätta och förmedla planen för att spåra tekniska ändringar under migrering.
- **Inriktning av företagsanvändare.** Upprätta en plan för att förbereda den bredare gruppen med företagsanvändare för genomförandet av migrering.
- **Inventering och analys av digital egendom.** Körning av de verktyg som krävs för att inventera och analysera den digitala egendomen. Mer information finns i Cloud Adoption Framework-genomgången av [digital egendom](../../../digital-estate/index.md).
- **Molnberedskap.** Utvärdera målmiljön för distribution för att säkerställa att den överensstämmer med kraven för de första arbetsbelastningskandidaterna. Mer information finns i [konfigurationsguiden för Azure](../../../ready/azure-setup-guide/index.md).

I de återstående artiklarna i den här serien får du hjälp med genomförandet av dessa.

## <a name="next-steps"></a>Nästa steg

Nu när du har en allmän förståelse för förutsättningarna är du redo att behandla den första förutsättningen angående [tidiga beslut vid migrering](./decisions.md).

> [!div class="nextstepaction"]
> [Tidiga beslut vid migrering](./decisions.md)
