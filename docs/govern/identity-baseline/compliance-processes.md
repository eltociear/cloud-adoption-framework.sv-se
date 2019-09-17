---
title: Principer för regelefterlevnad för identitetens bas linje
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Principer för regelefterlevnad för identitetens bas linje
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: f391f8233aa425ccf0ff61e625a2575fb9450b88
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/16/2019
ms.locfileid: "71028829"
---
# <a name="identity-baseline-policy-compliance-processes"></a>Principer för regelefterlevnad för identitetens bas linje

Den här artikeln beskriver en metod för policys öknings processer som styr [identitets bas linjen](./index.md). Effektiv styrning av identiteten börjar med återkommande manuella processer som hjälper identitets principen att antas och revisioner. Detta kräver en regelbunden medverkan av moln styrnings teamet och intresserade affärs-och IT-intressenter för att granska och uppdatera principen och säkerställa efterlevnaden av policyn. Dessutom kan många pågående övervaknings-och verk ställnings processer automatiseras eller kompletteras med verktyg för att minska kostnaderna för styrning och tillåta snabbare svar på princip avvikelse.

## <a name="planning-review-and-reporting-processes"></a>Planering, granskning och rapportering av processer

Med identitets hanterings verktyg får du till gång till funktioner som underlättar användar hantering och åtkomst kontroll i en moln distribution. De kräver dock också bra betänkta processer och principer som stöder organisationens mål. Följande är en uppsättning exempel processer som ofta ingår i bas linje disciplinen för identiteter. Använd de här exemplen som utgångs punkt när du planerar de processer som gör att du kan fortsätta att uppdatera identitets policyn baserat på affärs förändringar och feedback från IT-teamen med uppgift att sätta igång styrnings vägledningen i praktiken.

**Inledande riskbedömning och planering:** Som en del av ditt första antagande av identitets bas disciplinen kan du identifiera dina kärn affärs risker och toleranser relaterade till moln identitets hantering. Använd den här informationen för att diskutera tekniska risker med medlemmar i IT-teamet som ansvarar för att hantera identitets tjänster och utveckla en bas linje uppsättning med säkerhets principer för att minimera riskerna för att fastställa din inledande styrnings strategi.

**Distributions planering:** Innan du distribuerar bör du gå igenom åtkomst behoven för arbets belastningar och utveckla en strategi för åtkomst kontroll som överensstämmer med etablerade företags identitets principer. Dokumentera eventuella luckor mellan behov och aktuell princip för att avgöra om princip uppdateringar krävs och ändra principen efter behov.

**Distributions testning:** Som en del av distributionen kommer moln styrnings teamet, i samarbete med IT-team som ansvarar för identitets tjänster, att kunna granska distributionen för att verifiera efterlevnad av identitets principer.

**Årlig planering:** På årsbasis bör du utföra en övergripande granskning av identitets hanterings strategin. Utforska de planerade ändringarna i Identity Services-miljön och uppdaterade moln implementerings strategier för att identifiera eventuell risk ökning eller behöver ändra aktuella identitets infrastruktur mönster. Använd även den här tiden för att granska de senaste metod tipsen för identitets hantering och integrera dem i dina principer och gransknings processer.

**Kvartals vis planering:** En gång i kvartalet utför en allmän granskning av gransknings data för identitets-och åtkomst kontroll och följer moln implementerings teamen för att identifiera eventuella nya risker eller drifts krav som kräver uppdateringar av identitets principen eller ändringar i åtkomst kontrollen strategi.

Den här planerings processen är också en lämplig tid att utvärdera det aktuella medlemskapet i moln styrnings teamet för kunskaps luckor som rör nya eller föränderliga principer och risker som rör identiteten. Bjud in relevant IT-personal för att delta i granskningar och planering som antingen tillfälliga tekniska rådgivare eller permanenta medlemmar i teamet.

**Utbildning och utbildning:** En gång i månaden kan du erbjuda utbildning för att se till att IT-personal och utvecklare är uppdaterade på de senaste kraven för identitets principer. Som en del av den här processen kan du granska och uppdatera dokumentation, vägledning eller andra utbildnings resurser för att se till att de är synkroniserade med de senaste företags princip uttrycken.

**Granskningar av månads granskning och rapportering:** Varje månad bör du utföra en granskning på alla moln distributioner för att säkerställa att deras fortsatta anpassningar med identitets policyn. Använd den här granskningen för att kontrol lera användarnas åtkomst till företags förändringar för att se till att användarna har rätt åtkomst till moln resurser och se till att åtkomst strategier som RBAC följs konsekvent. Identifiera privilegierade konton och dokumentera deras syfte. Den här gransknings processen skapar en rapport för moln strategi teamet och varje moln antagande team som beskriver den övergripande principen. Rapporten lagras också för granskning och juridiskt syfte.

## <a name="ongoing-monitoring-processes"></a>Pågående övervaknings processer

Avgöra om din identitets styrnings strategi lyckas beror på insyn i aktuella och tidigare tillstånd för dina identitets system. Utan möjlighet att analysera moln distributionens relevanta mått och relaterade data kan du inte identifiera ändringar i riskerna eller identifiera överträdelser av dina risk toleranser. De löpande styrnings processer som beskrivs ovan kräver kvalitets data för att säkerställa att principen kan ändras för att stödja företagets föränderliga behov.

Se till att IT-teamen har implementerat automatiska övervaknings system för dina identitets tjänster som samlar in loggar och gransknings information som du behöver för att utvärdera risken. Vara proaktivt vid övervakning av dessa system för att säkerställa att det går att identifiera och minska eventuella policy överträdelser, och se till att alla ändringar av din identitets infrastruktur återspeglas i övervaknings strategin.

## <a name="violation-triggers-and-enforcement-actions"></a>Fel utlösare och tvingande åtgärder

Överträdelser av identitets principer kan leda till obehörig åtkomst till känsliga data och leda till allvarlig störning av verksamhets kritiska program och tjänster. När överträdelser identifieras bör du vidta åtgärder för att justera med principen så snart som möjligt. IT-teamet kan automatisera de flesta fel utlösare med hjälp av de verktyg som beskrivs i [identitets bas linjen verktygskedjan](./toolchain.md).

Följande utlösare och tvingande åtgärder innehåller exempel som du kan referera till när du planerar att använda övervaknings data för att lösa princip överträdelser:

- **Misstänkt aktivitet har identifierats:** Användar inloggningar som identifieras från anonyma proxy-IP-adresser, okända platser eller efterföljande inloggningar från icke-skilda geografiska platser kan tyda på ett potentiellt konto intrång eller försök till skadlig åtkomst. Inloggningen kommer att blockeras tills användar identiteten kan verifieras och lösen ords återställning.
- **Läckta användarautentiseringsuppgifter:** Konton med användar namn och lösen ord som läcker till Internet inaktive ras tills användar identiteten kan verifieras och lösen ords återställning.
- **Otillräckliga åtkomst kontroller har identifierats:** Alla skyddade till gångar där åtkomst begränsningar inte uppfyller säkerhets kraven kommer att ha åtkomst blockerad tills resursen har blivit kompatibel.

## <a name="next-steps"></a>Nästa steg

Använd [mallen för moln hantering](./template.md)för att dokumentera de processer och utlösare som överensstämmer med den aktuella moln implementerings planen.

Vägledning om hur du kör moln hanterings principer i justering med implementerings planer finns i artikeln om disciplin förbättringar.

> [!div class="nextstepaction"]
> [Förbättringar av identitets bas linje disciplin](./discipline-improvement.md)
