---
title: Förbättringar av distributions accelerations disciplin
description: Förstå de potentiella aktiviteter som ett företag utför för att utveckla och ta del av dess distributions accelerations disciplin i varje fas av moln införande.
author: alexbuckgit
ms.author: abuck
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 97f8a82295a8eff5614c965ba583fcbf8d50f501
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/31/2020
ms.locfileid: "80434591"
---
# <a name="deployment-acceleration-discipline-improvement"></a>Förbättringar av distributions accelerations disciplin

Distributions accelerations disciplin fokuserar på att etablera principer som säkerställer att resurser distribueras och konfigureras konsekvent och upprepas och att de förblir kompatibla under hela sin livs cykel. Inom de fem disciplinerna i moln styrning innehåller distributions acceleration beslut om automatiserade distributioner, käll kontrolls artefakter, övervakning av distribuerade resurser för att bibehålla önskad status och granskning av all efterlevnad åtgärder.

Den här artikeln beskriver några potentiella uppgifter som företaget kan delta i för att utveckla och mogna distributions accelerations disciplinen bättre. Dessa uppgifter kan delas upp i planering, uppbyggnad, införande och drifts faser för implementering av en moln lösning, som sedan upprepas på att tillåta utveckling av en [stegvis metod för moln styrning](../guides/index.md#an-incremental-approach-to-cloud-governance).

![Fyra faser i antagandet](../../_images/govern/adoption-phases.png)

*Figur 1 – implementerings faser för den stegvisa metoden för moln styrning.*

Det är omöjligt för något dokument att redovisa kraven i alla företag. I den här artikeln beskrivs de föreslagna minimi-och potentiella exempel aktiviteterna för varje fas i processens mognads process. Det första målet med dessa aktiviteter är att hjälpa dig att skapa en [policy MVP](../guides/index.md#an-incremental-approach-to-cloud-governance) och upprätta ett ramverk för stegvisa princip förbättringar. Ditt moln styrnings team måste bestämma hur mycket du ska investera i dessa aktiviteter för att förbättra dina funktioner för identitets styrning av identiteter.

> [!CAUTION]
> Varken de minsta eller potentiella aktiviteter som beskrivs i den här artikeln är justerade med specifika företags principer eller krav för tredje parts efterlevnad. Den här vägledningen är utformad för att hjälpa till att under lätta de konversationer som kommer att leda till justering av båda kraven med en modell för moln styrning.

## <a name="planning-and-readiness"></a>Planering och beredskap

Den här fasen av styrnings mognads bryggor förenar indelningen mellan affärs resultat och insats bara strategier. Under den här processen definierar ledarskaps gruppen vissa mått, mappar dessa mått till den digitala egendomen och börjar planera den totala migreringen.

**Minsta antal föreslagna aktiviteter:**

- Utvärdera dina [verktygskedjan alternativ för distributions acceleration](./toolchain.md) och implementera en hybrid strategi som passar din organisation.
- Utveckla ett utkast till rikt linjer för arkitektur och distribuera till viktiga intressenter.
- Utbilda och involvera de personer och grupper som påverkas av rikt linjerna för arkitektur utveckling.
- Utbilda utvecklings team och IT-personal för att förstå DevSecOps-principer och strategier och vikten av helt automatiserade distributioner i distributions accelerations disciplinen.

**Potentiella aktiviteter:**

- Definiera roller och tilldelningar som styr distributions accelerationen i molnet.

## <a name="build-and-predeployment"></a>Bygg och för distribution

**Minsta antal föreslagna aktiviteter:**

- För nya molnbaserade program ska du införa helt automatiserade distributioner tidigt i utvecklings processen. Den här investeringen förbättrar tillförlitligheten för dina test processer och garanterar konsekvens i dina utvecklings-, frågor och produktions miljöer.
- Lagra alla distributions artefakter som mallar för distribution eller konfigurations skript med en käll kontroll plattform, till exempel GitHub eller Azure DevOps.
- Lagra alla hemligheter, lösen ord, certifikat och anslutnings strängar i [Azure Key Vault](https://docs.microsoft.com/azure/key-vault)
- Överväg ett pilot test innan du implementerar [verktygskedjan för distributions acceleration](./toolchain.md), och se till att det effektiviserar distributionerna så mycket som möjligt. Använd feedback från pilot test under fasen för distribution, och upprepa vid behov.
- Utvärdera programens logiska och fysiska arkitektur och identifiera möjligheter att automatisera distributionen av program resurser eller förbättra delar av arkitekturen med hjälp av andra molnbaserade resurser.
- Uppdatera rikt linjer för arkitektur som innehåller distributions-och användar implementerings planer och distribuera till viktiga intressenter.
- Fortsätt att utbilda de personer och grupper som påverkas mest av arkitektur rikt linjerna.

**Potentiella aktiviteter:**

- Definiera en pipeline för kontinuerlig integrering och kontinuerlig distribution (CI/CD) för att helt hantera uppdateringar av ditt program via utvecklings-, frågor och produktions miljöer.

## <a name="adopt-and-migrate"></a>Införa och migrera

Migrering är en stegvis process som fokuserar på förflyttning, testning och införande av program eller arbets belastningar i en befintlig digital egendom.

**Minsta antal föreslagna aktiviteter:**

- Migrera din [distributions accelerations verktygskedjan](./toolchain.md) från utveckling till produktion.
- Uppdatera dokument för arkitektur rikt linjer och distribuera till viktiga intressenter.
- Utveckla utbildningsmaterial och dokumentation, medvetenhets kommunikation, incitament och andra program för att hjälpa till att skydda utvecklaren och den.

**Potentiella aktiviteter:**

- Kontrol lera att de bästa metoderna som definierats under konstruktions-och för distributions faserna är korrekt utförda.
- Se till att varje program eller arbets belastning överensstämmer med distributionens accelerations strategi före lanseringen.

## <a name="operate-and-post-implementation"></a>Drift och efter implementering

När omvandlingen är klar måste styrning och åtgärder vara aktiva för den naturliga livs cykeln för ett program eller en arbets belastning. Den här fasen av styrnings förfallo tid fokuserar på de aktiviteter som vanligt vis kommer efter att lösningen har implementerats och omvandlings cykeln börjar stabilisera sig.

**Minsta antal föreslagna aktiviteter:**

- Anpassa din [distributions accelerations verktygskedjan](./toolchain.md) baserat på ändringar i organisationens ändrade identitets behov.
- Automatisera meddelanden och rapporter för att varna dig om potentiella konfigurations problem eller skadliga hot.
- Övervaka och rapportera om användning och Resursanvändning.
- Rapport om statistik efter distribution och distribution till intressenter.
- Ändra arkitektur rikt linjerna för att vägleda framtida införande processer.
- Fortsätt att kommunicera med och träna de berörda personerna och teamen regelbundet och se till att du följer rikt linjerna för arkitektur.

**Potentiella aktiviteter:**

- Konfigurera ett övervaknings-och rapporterings verktyg för önskad tillstånds konfiguration.
- Granska konfigurations verktyg och skript regelbundet för att förbättra processer och identifiera vanliga problem.
- Arbeta med utvecklings-, drift-och säkerhets team för att hjälpa mogna DevSecOps-metoder och dela upp organisations silor som leder till ineffektivitet.

## <a name="next-steps"></a>Nästa steg

Nu när du förstår begreppet moln identitets styrning kan du undersöka [identitets bas linjen verktygskedjan](./toolchain.md) för att identifiera de Azure-verktyg och-funktioner som du behöver när du utvecklar disciplinen för identitets styrning på Azure-plattformen.

> [!div class="nextstepaction"]
> [Identitets bas linje verktygskedjan för Azure](./toolchain.md)
