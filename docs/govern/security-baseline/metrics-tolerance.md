---
title: Mått, indikatorer och risk tolerans för säkerhets bas linjer
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Mått, indikatorer och risk tolerans för säkerhets bas linjer
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 2eeab224a9f025b9e93cf407626455e74d69ccd4
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/16/2019
ms.locfileid: "71030392"
---
# <a name="security-baseline-metrics-indicators-and-risk-tolerance"></a>Mått, indikatorer och risk tolerans för säkerhets bas linjer

Den här artikeln är avsedd att hjälpa dig att kvantifiera affärs risk toleransen när det gäller säkerhets bas linjen. Genom att definiera mått och indikatorer kan du skapa ett affärs ärende för att göra en investering som förfaller i säkerhets bas linjen.

## <a name="metrics"></a>Mått

Säkerhets bas linjen fokuserar i allmänhet på att identifiera potentiella sårbarheter i dina moln distributioner. Som en del av din riskanalys vill du samla in data som är relaterade till din säkerhets miljö för att ta reda på hur mycket risk du möter, och hur viktig investering i säkerhets bas linje styrningen är till dina planerade moln distributioner.

Varje organisation har olika säkerhets miljöer och-krav och olika potentiella källor med säkerhets data. Följande är exempel på användbara mått som du bör samla för att utvärdera risk tolerans inom ramen för säkerhets bas linjen:

- **Data klassificering:** Antal molnbaserade data och tjänster som inte är klassificerade enligt organisationens sekretess, efterlevnad eller krav på affärs påverkan.
- **Antal känsliga data lager:** Antal lagrings slut punkter eller databaser som innehåller känsliga data och som bör skyddas.
- **Antal okrypterade data lager:** Antalet känsliga data lager som inte är krypterade.
- **Attack yta:** Hur många data källor, tjänster och program som är molnbaserade. Vilken procent andel av dessa data källor klassificeras som känslig? Hur många procent av dessa program och tjänster är verksamhets kritiska?
- **Standarder som omfattas:** Antalet säkerhets standarder som definieras av säkerhets teamet.
- **Resurser som omfattas:** Distribuerade till gångar som omfattas av säkerhets standarder.
- **Övergripande standarder kompatibilitet:** Förhållandet mellan överensstämmelse med säkerhets standarder.
- **Attacker efter allvarlighets grad:** Hur många koordinerade försök att avbryta dina molnbaserade tjänster, t. ex. genom DDoS-attacker (distributed denial of Service), har din infrastruktur upplevelse? Vad är storlek och allvarlighets grad för de här angreppen?
- **Skydd mot skadlig kod:** Procent andel distribuerade virtuella datorer (VM) som har all nödvändig program vara, brand vägg eller annan säkerhets program vara installerad.
- **Svars tid för korrigering:** Hur lång tid det har varit sedan de virtuella datorerna hade haft operativ system och program varu uppdateringar tillämpade.
- **Rekommendationer för säkerhets hälsa:** Antalet säkerhets program rekommendationer för att lösa hälso krav för distribuerade resurser, sorterade efter allvarlighets grad.

## <a name="risk-tolerance-indicators"></a>Risk tolerans indikatorer

Cloud Platforms tillhandahåller en bas linje uppsättning funktioner som gör det möjligt för små distributions grupper att konfigurera grundläggande säkerhets inställningar utan ytterligare planering. Det innebär att små utvecklings-/testnings-eller experiment-eller experiment-arbetsbelastningar som inte innehåller känsliga data representerar en relativt låg risk nivå och sannolikt inte behöver mycket på vägen för formell säkerhets bas linje princip. Men så snart viktiga data eller verksamhets kritiska funktioner flyttas till molnet ökar säkerhets riskerna, medan toleransen för dessa risker minskar snabbt. När mer av dina data och funktioner distribueras till molnet, desto sannolikare behöver du en ökad investering i säkerhets bas linje disciplinen.

I det tidiga skedet av moln implementeringen arbetar du med IT-säkerhetsteamet och affärs intressenterna för att identifiera [affärs risker](./business-risks.md) relaterade till säkerhet, och avgör sedan en acceptabel bas linje för säkerhets risk tolerans. Det här avsnittet av moln implementerings ramverket innehåller exempel, men detaljerade risker och bas linjer för ditt företag eller distributioner kan vara olika.

När du har en bas linje kan du fastställa de lägsta benchmark-värden som representerar en oacceptabel ökning av dina identifierade risker. Dessa riktmärken fungerar som utlösare för när du behöver vidta åtgärder för att åtgärda dessa risker. Här följer några exempel på hur säkerhets mått, till exempel de som beskrivs ovan, kan motivera en ökad investering i säkerhets bas linjen.

- **Utlösare för verksamhets kritiska arbets belastningar.** Ett företag som distribuerar verksamhets kritiska arbets belastningar till molnet bör investera i säkerhets bas linjen för att förhindra avbrott i tjänsten eller känslig data exponering.
- **Skyddad data utlösare.** Ett företag som är värd för data i molnet och som kan klassificeras som konfidentiellt, privat eller på annat sätt omfattas av reglerings frågor. De behöver en säkerhets bas linje disciplin för att säkerställa att dessa data inte omfattas av förlust, exponering eller stöld.
- **Utlösare för externa attacker.** Ett företag som upplever allvarliga attacker mot sin nätverks infrastruktur _x_ gånger per månad kan dra nytta av säkerhets bas linje disciplinen.
- **Utlösare för standard efterlevnad.** Ett företag med mer än _x%_ av resurser som följer säkerhets standarder bör investera i säkerhets bas linje disciplin för att säkerställa att standarder tillämpas konsekvent i din IT-infrastruktur.
- **Storleks utlösare för moln egendom.** Ett företag som är värd för fler än _x_ program, tjänster eller data källor. Stora moln distributioner kan dra nytta av investeringar i säkerhets bas linje disciplinen för att säkerställa att deras totala angrepps yta är korrekt skyddad mot obehörig åtkomst eller andra externa hot.
- **Utlösare för säkerhets program efterlevnad.** Ett företag där mindre än _x%_ av de distribuerade virtuella datorerna har alla nödvändiga säkerhets program installerade. En säkerhets bas linje disciplin kan användas för att säkerställa att program vara installeras konsekvent på all program vara.
- **Korrigerar utlösare.** Ett företag där distribuerade virtuella datorer eller tjänster där operativ system eller program uppdateringar inte har verkställts under de senaste _x_ dagarna. En säkerhets bas linje disciplin kan användas för att säkerställa att uppdatering hålls uppdaterad inom ett obligatoriskt schema.
- **Säkerhet – fokuserat.** Vissa företag kommer att ha starka säkerhets-och data sekretess krav även för test-och experiment arbets belastningar. Dessa företag måste investera i säkerhets bas linje disciplinen innan eventuella distributioner kan påbörjas.

De exakta mått och utlösare som du använder för att mäta risk toleransen och nivån av investeringar i säkerhets bas linje disciplinen är specifika för din organisation, men exemplen ovan bör fungera som en användbar bas för diskussioner i din organisation för moln styrning.

## <a name="next-steps"></a>Nästa steg

Använda [mallen för moln hantering](./template.md), dokument mått och tolerans indikatorer som överensstämmer med den aktuella moln implementerings planen.

Granska exempel principer för säkerhets bas linjer som start punkt för att utveckla principer som åtgärdar specifika affärs risker som överensstämmer med dina moln implementerings planer.

> [!div class="nextstepaction"]
> [Granska exempel principer](./policy-statements.md)
