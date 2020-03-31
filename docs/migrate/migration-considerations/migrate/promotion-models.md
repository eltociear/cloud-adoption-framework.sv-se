---
title: Typer av befordrans modeller
description: Lär dig mer om tre vanliga kampanj modeller som används i moln migreringar och hur du väljer modell som påverkar de aktiviteter som visas i Migrera och optimera processer.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 81a11a06236840658e87dbee1d0bed72579e7f6e
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/31/2020
ms.locfileid: "80432515"
---
# <a name="promotion-models-single-step-staged-or-flight"></a>Kampanj modeller: enkla steg, mellanlagrade eller Flight

Migrering av en arbetsbelastning diskuteras ofta som en enskild aktivitet. I verkligheten är det en samling av mindre aktiviteter som möjliggör överföringen av en digital tillgång till molnet. En av de sista aktiviteterna i en migrering är befordran av en tillgång till produktion. Befordran är den tidpunkt då produktionssystemet ändras för slutanvändare. Det kan ofta vara så enkelt som att ändra nätverksroutingen och omdirigera användare till den nya produktionstillgången. Befordran är också den punkt där avdelningen för IT- eller molndrift ändrar fokus på driftshanteringsprocessen från det tidigare produktionssystemet till de nya.

Det finns flera modeller för befordran. Den här artikeln beskriver tre av de vanligaste vid molnmigrering. Valet av befordringsmodell ändrar de aktiviteter som utförs inom processerna för migrering och optimering. Därför ska befordringsmodellen bestämmas tidigt för en version.

## <a name="impact-of-promotion-model-on-migrate-and-optimize-activities"></a>Befordringsmodellen inverkan på aktiviteter för migrering och optimering

I var och en av de följande modellerna för befordran replikerar och mellanlagrar det valda migrationsverktyget de tillgångar som utgör arbetsbelastningen. Efter mellanlagring behandlar de olika modellerna tillgången på lite olika sätt.

- **Befordran i ett steg.** I en modell med befordran i *ett steg* fungerar mellanlagringsprocessen även som befordran. När alla tillgångar mellanlagrats leds användartrafiken om och mellanlagring blir produktion. I ett sådant fall är befordran en del av migrationsprocessen. Det är den snabbaste migreringsmodellen. Denna modell gör det dock svårare att integrera robusta aktiviteter för testning och optimering. Denna modelltyp förutsätter dessutom att migreringsteamet har tillgång till miljön för mellanlagring och produktion, vilket bryter mot de krav på separation av uppgifter som finns i vissa miljöer.
  > [!NOTE]
  >Innehållsförteckningen för denna plats listar befordringsaktiviteten som en det av optimeringsprocessen. I en modell med ett steg sker befordran under migreringsprocessen. När denna modell används ska roller och ansvarsområden uppdateras för att spegla detta.
- **Mellanlagrad.** I modellen med *mellanlagrad* befordran anses arbetsbelastningen vara migrerad när den mellanlagrats, men ännu inte befordrats. Innan befordran genomgår den migrerade arbetsbelastningen en serie prestandatest, affärstest och optimeringsförändringar. Den befordras sedan vid ett senare datum tillsammans med en plan för affärstestning. Denna metod förbättrar balansen mellan kostnad och prestanda samtidigt som det är lättare att utföra affärsvalidering.
- **Förhandsversion.** Modellen med en *förhandsversion* kombinerar modellerna för mellanlagring och ett stegs-modellen. I modellen med förhandsversion behandlas tillgångarna i arbetsbelastningen som produktionstillgångar efter mellanlagring. Efter en kortare period av automatisk testning dirigeras produktionstrafik till arbetsbelastningen. Det är dock en delmängd av trafiken. Den trafiken fungerar som en första körning av produktion och testning. Om arbetsbelastningen fungerar vad gäller funktion och prestanda migreras ytterligare trafik. När all produktionstrafik flyttats över till de nya tillgångarna anses arbetsbelastningen vara helt befordrad.

Den valda befordringsmodellen påverkar sekvensen på aktiviteterna som utförs. Den påverkar även roller och ansvarsområden för teamet för molnimplementering. Det kan även påverka sammansättningen av en sprint eller flera sprintar.

## <a name="single-step-promotion"></a>Befordran i ett steg

Denna modell använder automatiseringsverktyg för migrering för att replikera, mellanlagra och befordra tillgångar. Tillgångarna replikeras i en avskärmad mellanlagringsmiljö som styrs av migreringsverktyget. När alla tillgångar replikerats kan verktyget utföra en automatiserad process för att befordra tillgångarna i den valda prenumerationen i ett steg. Under tiden som den mellanlagras fortsätter verktyget att replikera tillgången vilket minimerar förlusten av data mellan de två miljöerna. När en tillgång befordras bryts länken mellan källsystemet och det replikerade systemet. Med denna metod förloras de ändringar som sker i de ursprungliga källsystemen.

**Fördelar** Fördelarna med den här metoden är:

- Modellen innebär mindre ändringar av målsystemen.
- Kontinuerlig replikering minimerar dataförlust.
- Om mellanlagringsprocessen misslyckas kan den snabbt tas bort och upprepas.
- Replikering och upprepade mellanlagringstest möjliggör en inkrementell process för skriptning och testning.

**Nackdelar** Nackdelarna med den här metoden är:

- Tillgångar som mellanlagras i verktygets isolerade sandbox-miljö tillåter inte komplexa testmodeller.
- Under replikering förbrukar migreringsverktyget bandbredd i det lokala datacentret. Mellanlagring av många tillgångar under en längre tid har exponentiell effekt på tillgänglig bandbredd vilket kan påverka migreringsprocessen och även arbetsbelastningar i produktion i den lokala miljön.

## <a name="staged-promotion"></a>Befordran med mellanlagring

I denna modell används sandbox-miljön som hanteras av migreringsverktyget för begränsade tester. De replikerade tillgångarna införs sedan i molnmiljön, vilket fungerar som en utökad mellanlagringsmiljö. De migrerade tillgångarna körs i molnet medan ytterligare tillgångar replikeras, mellanlagras och migreras. När fullständiga arbetsbelastningar blir tillgängliga inleds mer omfattande testning. När alla tillgångar som är relaterade till en prenumeration har migrerats befordras prenumerationen och alla arbetsbelastningar till produktion. I detta scenario sker inga förändringar av arbetsbelastningarna under befordringsprocessen. Ändringar brukar istället ske i nätverks- och identitetslagren med omdirigering av användare till den nya miljön och indragning av behörigheter för teamet för molnimplementering.

**Fördelar** Fördelarna med den här metoden är:

- Denna modell tillhandahåller möjligheter för mer korrekta verksamhetstester.
- Arbetsbelastningen kan undersökas noggrannare för att optimera tillgångens prestanda och kostnad.
- Ett större antal tillgångar kan replikeras inom samma tids- och bandbreddsbegränsningar.

**Nackdelar** Nackdelarna med den här metoden är:

- Det valda migreringsverktyget kan inte utföra fortgående replikering efter migrering.
- En sekundär typ av datareplikering krävs för att synkronisera data mellan plattformarna under mellanlagringen.

## <a name="flight-promotion"></a>Befordran av förhandsversion

Denna modell liknar befordringsmodellen med mellanlagring. Det finns dock en avgörande skillnad. När prenumerationen är klar för befordran sker omdirigering av användare i etapper eller förhandsversioner. För varje förhandsversion omdirigeras fler användare till produktionssystemen.

**Fördelar** Fördelarna med den här metoden är:

- Denna modell minskar riskerna med en stor migrering eller befordringsaktivitet. Fel i den migrerade lösningen kan identifieras med mindre påverkan på affärsprocesserna.
- Den tillåter övervakning av arbetsbelastningen prestandabehov i molnmiljön under en längre tid, vilket ger större möjlighet till korrekta beslut vad gäller storleksanpassning.
- Fler tillgångar kan replikeras inom samma tids- och bandbreddsbegränsningar.

**Nackdelar** Nackdelarna med den här metoden är:

- Det valda migreringsverktyget kan inte utföra fortgående replikering efter migrering.
- En sekundär typ av datareplikering krävs för att synkronisera data mellan plattformarna under mellanlagringen.

## <a name="next-steps"></a>Nästa steg

När en befordransmodell definierats och godkänts av teamet för molnimplementering kan [tillgångsreparation](./remediate.md) inledas.

> [!div class="nextstepaction"]
> [Reparation av tillgångar före migrering](./remediate.md)
