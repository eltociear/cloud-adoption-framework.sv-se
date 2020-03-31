---
title: 'Komplex företags styrning: förbättra disciplinen för resurs konsekvens'
description: Använd ramverket för moln införande för Azure för att lära dig om återställning, storleks kontroll och övervakning av kontroller för att förbättra styrnings bas linjen och åtgärda risker.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 148a89cd63bfa7c29caea9f5b8f74f64132aed08
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/31/2020
ms.locfileid: "80434334"
---
# <a name="governance-guide-for-complex-enterprises-improve-the-resource-consistency-discipline"></a>Styrnings guide för komplexa företag: förbättra disciplinen för resurs konsekvens

Den här artikeln går vidare genom att lägga till resurs konsekvens kontroller till styrnings-MVP: en som stöder verksamhets kritiska program.

## <a name="advancing-the-narrative"></a>Med den här berättelsenn

Moln implementerings teamen har uppfyllt alla krav för att flytta skyddade data. Med dessa program ingår SLA-åtaganden för verksamheten och behöver support från IT-avdelningen. Direkt bakom teamet som migrerar två Data Center, är flera program utvecklings-och BI-team redo att börja lansera nya lösningar i produktionen. IT-åtgärder är nya för moln åtgärder och behöver snabbt integrera befintliga operativa processer.

### <a name="changes-in-the-current-state"></a>Ändringar i det aktuella läget

- DEN flyttar aktivt produktions arbets belastningar med skyddade data till Azure. Vissa arbets belastningar med låg prioritet betjänar produktions trafiken. Mer kan klippas ut så snart som det går att logga ut på beredskap för att stödja arbets belastningarna.
- Program utvecklings teamen är redo för produktions trafik.
- BI-teamet är redo att integrera förutsägelser och insikter i de system som kör åtgärder för de tre affär senheterna.

### <a name="incrementally-improve-the-future-state"></a>Förbättra framtida tillstånd stegvis

- IT-åtgärder är nya för moln åtgärder och behöver snabbt integrera befintliga operativa processer.
- Ändringarna i det aktuella och framtida läget ger nya risker som kräver nya princip instruktioner.

## <a name="changes-in-tangible-risks"></a>Förändringar i materiella risker

**Affärs avbrott:** Det finns en potentiell risk för en ny plattform som orsakar avbrott i verksamhets kritiska affärs processer. IT-avdelningen och teamen som körs på olika moln-antaganden är relativt inerfarenhet med moln åtgärder. Detta ökar risken för avbrott och måste åtgärdas och regleras.

Den här affärs risken kan utökas till flera tekniska risker:

1. Feljusterade operativa processer kan leda till avbrott som inte kan upptäckas eller minimeras snabbt.
2. Externt intrång eller denial of Service-attacker kan orsaka affärs avbrott.
3. Uppdrags kritiska till gångar kanske inte identifieras korrekt och fungerar därför inte korrekt.
4. Identifierade eller felmärkta till gångar kanske inte stöds av befintliga processer för drift hantering.
5. Konfiguration av distribuerade till gångar kanske inte uppfyller prestanda förväntningarna.
6. Loggningen kanske inte är korrekt inspelad och centraliserad för att möjliggöra reparationer av prestanda problem.
7. Återställnings principer kan Miss lyckas eller tar längre tid än förväntat.
8. Inkonsekventa distributions processer kan leda till säkerhets luckor som kan leda till data läckor eller avbrott.
9. Konfigurations luckor eller missade korrigeringar kan leda till oönskade säkerhets luckor som kan leda till data läckor eller avbrott.
10. Konfigurationen kanske inte tillämpar kraven för definierade service avtal eller krav för allokerad återställning.
11. Distribuerade operativ system eller program kanske inte uppfyller kraven för operativ system och program härdning.
12. Det finns en risk för inkonsekvens på grund av flera team som arbetar i molnet.

## <a name="incremental-improvement-of-the-policy-statements"></a>Stegvis förbättring av princip uttrycken

Följande ändringar i principen hjälper dig att åtgärda de nya riskerna och guidens implementering. Listan ser bra ut, men införandet av dessa principer kan vara enklare än vad som visas.

1. Alla distribuerade till gångar måste kategoriseras efter allvarlighets grad och data klassificering. Klassificeringarna bör granskas av moln styrnings teamet och program ägaren innan distributionen till molnet.
2. Undernät som innehåller verksamhets kritiska program måste skyddas av en brand Väggs lösning som kan upptäcka intrång och reagera på attacker.
3. Styrnings verktyg måste granska och genomdriva krav på nätverks konfiguration som definieras av säkerhets bas linje teamet.
4. Styrnings verktyg måste kontrol lera att alla till gångar som är relaterade till verksamhets kritiska program eller skyddade data ingår i övervakningen av resurs uttömdning och optimering.
5. Styrnings verktyg måste verifiera att lämplig nivå av loggnings data samlas in för alla verksamhets kritiska program eller skyddade data.
6. Styrnings processen måste verifiera att säkerhets kopiering, återställning och SLA-krav implementeras korrekt för verksamhets kritiska program och skyddade data.
7. Styrnings verktyg måste begränsa distributionen av virtuella datorer till godkända avbildningar.
8. Styrnings verktyg måste framtvinga att automatiska uppdateringar **förhindras** på alla distribuerade till gångar som stöder verksamhets kritiska program. Överträdelser måste granskas med operativa hanterings team och åtgärdas i enlighet med Operations policys. Till gångar som inte uppdateras automatiskt måste ingå i processer som ägs av IT-åtgärder för att snabbt och effektivt uppdatera dessa servrar.
9. Styrnings verktyg måste verifiera taggning relaterad till kostnader, allvarlighets grad, SLA, program och data klassificering. Alla värden måste justeras mot fördefinierade värden som hanteras av moln styrnings teamet.
10. Styrnings processer måste innehålla revisioner vid distributions platsen och regelbundet för att säkerställa konsekvens för alla till gångar.
11. Trender och utnyttjande som kan påverka moln distributioner bör regelbundet granskas av säkerhets teamet för att tillhandahålla uppdateringar av verktyget för säkerhets bas linjer som används i molnet.
12. Innan du släpper i produktionen måste alla verksamhets kritiska program och skyddade data läggas till i den avsedda operativa övervaknings lösningen. Till gångar som inte kan identifieras av det valda verktyget för IT-åtgärder kan inte släppas för produktions användning. Eventuella ändringar som krävs för att göra till gångar som kan identifieras måste göras till de relevanta distributions processerna för att se till att till gångar kan upptäckas i framtida distributioner.
13. När det upptäcks är till gångs storlek val IDE rad av drift hanterings grupper för att kontrol lera att till gången uppfyller prestanda kraven.
14. Distributions verktyg måste godkännas av moln styrnings teamet för att säkerställa fort löp ande styrning av distribuerade till gångar.
15. Distributions skripten måste finnas i den centrala lagrings platsen som är tillgänglig för gruppen moln styrning för regelbunden granskning och granskning.
16. Gransknings processer för styrning måste verifiera att distribuerade till gångar är korrekt konfigurerade i justering med SLA-och återställnings krav.

## <a name="incremental-improvement-of-the-best-practices"></a>Stegvis förbättring av bästa praxis

I det här avsnittet av artikeln får du förbättra designen för styrnings MVP för att inkludera nya Azure-principer och en implementering av Azure Cost Management. Tillsammans kommer dessa två design ändringar att uppfylla de nya företags princip satserna.

Efter erfarenheten av det här fiktiva exemplet antas det att ändringar av skyddade data redan har inträffat. Genom att bygga vidare på det bästa sättet lägger du till krav för drifts övervakning, så att du kan prenumerera på verksamhets kritiska program.

**IT-prenumeration för företag:** Lägg till följande i företags IT-prenumerationen, som fungerar som hubb.

1. Som ett externt beroende måste moln drifts teamet definiera verktyg för drifts övervakning, verktyg för affärs kontinuitet och haveri beredskap (BCDR) och automatiserad reparations verktyg. Moln styrnings teamet kan sedan stödja nödvändiga identifierings processer.
    1. I det här användnings fallet väljer moln drifts teamet Azure Monitor som det primära verktyget för övervakning av verksamhets kritiska program.
    2. Teamet väljer också Azure Site Recovery som det primära BCDR-verktyget.
2. Azure Site Recovery implementering.
    1. Definiera och Distribuera Azure Site Recovery valv för säkerhets kopierings-och återställnings processer.
    2. Skapa en Azure-resurs hanterings mall för att skapa ett valv i varje prenumeration.
3. Azure Monitor implementering.
    1. När en verksamhets kritisk prenumeration identifieras kan du skapa en Log Analytics-arbetsyta.

**Individuell moln införande prenumeration:** Följande säkerställer att varje prenumeration kan identifieras av övervaknings lösningen och kan tas med i BCDR-metoder.

1. Azure Policy för verksamhets kritiska noder:
    1. Granska och Använd endast standard roller.
    2. Granska och framtvinga kryptering av program för alla lagrings konton.
    3. Granska och Framtvinga användning av godkända nätverks under nät och VNet per nätverks gränssnitt.
    4. Granska och genomdriva begränsningen för användardefinierade vägvals tabeller.
    5. Granska och genomdriva distributionen av Log Analytics agenter för virtuella Windows-och Linux-datorer.
2. Azure-skiss:
    1. Skapa en skiss med namnet `mission-critical-workloads-and-protected-data`. I den här skissen används till gångar utöver den skyddade data skissen.
    2. Lägg till de nya Azure-principerna i skissen.
    3. Använd skissen på alla prenumerationer som förväntas vara värd för ett verksamhets kritiskt program.

## <a name="conclusion"></a>Sammanfattning

Genom att lägga till dessa processer och ändringar i styrnings MVP: n kan du åtgärda många av de risker som är kopplade till resurs styrningen. Tillsammans lägger de till de kontroller för återställning, storlek och övervakning som krävs för att ge moln medveten verksamhet.

## <a name="next-steps"></a>Nästa steg

Eftersom moln införande växer och levererar ytterligare affärs värde, kommer de risker och moln styrnings behov också att förändras. För det fiktiva företaget i den här hand boken är nästa utlösare när distributions skalan överskrider 1 000 till gångar till molnet eller månads kostnaden överskrider $10 000 USD per månad. I det här läget lägger moln styrnings teamet till Cost Management kontroller.

> [!div class="nextstepaction"]
> [Förbättra Cost Managements disciplinen](./cost-management-improvement.md)
