---
title: Reparation av tillgångar före migrering
description: Lär dig hur du kan åtgärda eventuella till gångar som du anser är inkompatibla med den valda moln leverantören innan migreringen börjar.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 8cc66b6995cf9221c81254974196c7839313045a
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/31/2020
ms.locfileid: "80429371"
---
# <a name="remediate-assets-prior-to-migration"></a>Reparera tillgångar före migrering

Under utvärderingsprocessen i migreringen vill teamet identifiera alla konfigurationer som skulle göra en tillgång inkompatibel med den valda molnleverantören. *Reparera* är en kontrollpunkt i migreringsprocessen där det säkerställs att dessa inkompatibiliteter har lösts. Den här artikeln innehåller några vanliga reparationsuppgifter som referens. Där upprättas även en skelettprocess för beslut om huruvida reparation är en lämplig investering.

## <a name="common-remediation-tasks"></a>Vanliga reparationsåtgärder

I företagsmiljöer finns det tekniska skulder. En del av dessa är att förvänta och är inte tecken på att något är fel. Arkitekturbeslut som passade bra för en lokal miljö är kanske inte helt lämpliga på en molnplattform. I endera fallet kan det krävs vanliga reparationsåtgärder för att förbereda tillgångarna för migrering. Följande är några exempel:

- **Mindre uppgraderingar av värd.** Ibland behöver en föråldrad värd uppgraderas före replikering.
- **Mindre uppgraderingar av gäst-OS.** Det är mer troligt att ett operativsystem behöver korrigeras eller uppgraderas före replikering.
- **Ändringar av serviceavtal.** Säkerhetskopiering och återställning förändras på betydande sätt på en molnplattform. Det är troligt att tillgångar behöver mindre ändringar i sina säkerhetskopieringsprocesser för att säkerställa fortsatt funktion i molnet.
- **PaaS-migrering.** I vissa fall kan en PaaS-distribution av en datastruktur eller ett program krävas för att påskynda distributionen. Mindre ändringar kan krävas för att förbereda lösningen för PaaS-distribution.
- **PaaS-kodändringar.** Det är inte ovanligt att anpassade program kräver smärre kodändringar för att bli redo för PaaS. Exempel kan vara metoder som bland annat skriver till en lokal disk eller användningen av sessionstillstånd i minnet.
- **Ändringar i programkonfiguration.** Migrerade program kan kräva ändringar av variabler, till exempel nätverkssökvägar till beroende tillgångar, ändringar i tjänstkonto eller uppdateringar av beroende IP-adresser.
- **Mindre ändringar av nätverkssökvägar.** Dirigeringsmönster kan behöva ändras så att de korrekt dirigerar användartrafik till nya tillgångar.
    > [!NOTE]
    > Detta är inte produktions dirigering till nya till gångar, utan i stället för att det ska finnas tillräckligt med routning till till gångarna i allmänhet.

## <a name="large-scale-remediation-tasks"></a>Storskaliga reparationsuppgifter

När ett datacenter är underhålls, korrigeras och uppdateras på rätt sätt finns det troligtvis inte mycket behov av reparation. Reparationsrika miljöer tenderar att vara gemensamma för stora företag, organisationer som har gjort omfattande nedskärningar inom IT, vissa äldre hanterade tjänstmiljöer samt förvärvsrika miljöer. I alla dessa typer av miljöer kan reparation uppta en stor del av migreringsarbetet. När följande reparationsuppgifter förekommer ofta och påverkar migreringens hastighet eller konsekvens negativt kan det vara bra att dela upp reparationen i ett parallellt arbete och team (på ett liknande sätt som parallell körning av molnimplementering och molnstyrning).

- **Frekventa uppgraderingar av värd.** När ett stort antal värdar måste uppgraderas för att slutföra migreringen av en arbetsbelastning är det troligt att migreringsteamet drabbas av fördröjningar. Det kan vara bra att dela ut berörda program och åtgärda stegen innan du inkluderar berörda program i alla planerade versioner.
- **Frekventa uppgraderingar av gäst-OS.** Stora företag har ofta servrar som körs på inaktuella versioner av Linux eller Windows. Utöver de tydliga säkerhetsriskerna med att använda ett inaktuellt operativsystem finns det även kompatibilitetsproblem som förhindrar att berörda arbetsbelastningar migreras. När ett stort antal virtuella datorer kräver OS-reparation kan det vara klokt att dela upp dessa arbeten i en parallell iteration.
- **Stora kodändringar.** Äldre anpassade program kan kräva betydligt fler ändringar för att förberedas för PaaS-distribution. I så fall kan det vara bra att ta bort dem fullständigt från kvarvarande uppgifter för migrering och i stället hantera dem i ett helt separat program.

## <a name="decision-framework"></a>Beslutsramverk

Det kan vara enkelt att utföra reparationer för mindre arbetsbelastningar, vilket är en av orsakerna till att det rekommenderas att man väljer en mindre arbetsbelastning för den första migreringen. När migreringsarbetet börjar mogna och du hanterar större arbetsbelastningar kan reparation dock vara en tidskrävande och kostsam process. Till exempel kan reparationsåtgärder för en Windows Server 2003-migrering som omfattar en tillgångspool med fler än 5 000 virtuella datorer fördröja en migrering med flera månader. När sådan storskalig reparation krävs kan följande frågor hjälpa dig att fatta beslut:

- Har alla arbetsbelastningar som påverkas av reparationen identifierats och angetts i de kvarvarande uppgifterna för migrering?
- Kommer en migrering ge liknande avkastning på investering (ROI) för arbetsbelastningar som inte berörs?
- Kan de berörda tillgångarna repareras i enlighet med den ursprungliga tidslinjen för migrering? Hur skulle ändringar i tidslinjen påverka ROI?
- Är det ekonomiskt gångbart att reparera tillgångarna parallellt med migreringsarbetet?
- Finns det tillräckligt med bandbredd så att personalen kan reparera och migrera? Bör en partner anlitas till att utföra en eller båda uppgifterna?

Om dessa frågor inte ger gynnsamma kan det vara värt att överväga några alternativa metoder som går bortom grundläggande strategier för IaaS-värdbyte:

- **Containeranpassning.** Vissa tillgångar kan hanteras i en containeranpassad miljö utan reparation. Detta kan ge mindre fördelaktig prestanda och löser inte problem med säkerhet eller kompatibilitet.
- **Automation.** Beroende på kraven för arbetsbelastning och reparation kan det vara mer lönsamt att skripta distributionen till nya tillgångar med hjälp av en DevOps-metod.
- **Återskapa.** När reparationskostnaderna är mycket höga och affärsvärde är lika högt kan en arbetsbelastning vara en bra kandidat för återskapande eller arkitekturomarbetning.

## <a name="next-steps"></a>Nästa steg

När reparationen är klar är [replikeringsaktiviteterna](./replicate.md) redo.

> [!div class="nextstepaction"]
> [Replikera tillgångar](./replicate.md)
