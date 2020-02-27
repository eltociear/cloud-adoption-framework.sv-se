---
title: 'Standard företags styrning: förbättra resurs konsekvens'
description: Använd ramverket för moln införande för Azure för att lära dig mer om att förbättra en styrnings bas linje och åtgärda risker genom att lägga till kontroller för återställning, storleks kontroll och övervakning.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: e50d3e258a4b040d1f9cfaa1b274ed977c49b14d
ms.sourcegitcommit: af45c1c027d7246d1a6e4ec248406fb9a8752fb5
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 02/27/2020
ms.locfileid: "77709115"
---
# <a name="standard-enterprise-governance-guide-improving-resource-consistency"></a>Standard styrnings guide för företag: förbättra resurs konsekvens

Den här artikeln går vidare genom att lägga till resurs konsekvens kontroller för att stödja verksamhets kritiska appar.

## <a name="advancing-the-narrative"></a>Med den här berättelsenn

Nya kund upplevelser, nya förutsägelse verktyg och migrerad infrastruktur fortsätter att förloppet. Företaget är nu redo att börja använda dessa till gångar i produktions kapaciteten.

### <a name="changes-in-the-current-state"></a>Ändringar i det aktuella läget

I föregående fas av den här delen var program utvecklingen och BI-teamen nästan klara att integrera kund-och finans data i produktions arbets belastningar. IT-teamet var i gång för att dra tillbaka DR-datacenter.

Sedan dess har vissa saker ändrats som påverkar styrning:

- DEN har dragit tillbaka 100% av DR-datacenter, före schemat. I processen identifierades en uppsättning till gångar i produktions data centret som kandidater till moln migrering.
- Teamen för program utveckling är nu klara för produktions trafik.
- BI-teamet är redo att mata in förutsägelser och insikter i drift system i produktions data centret.

### <a name="incrementally-improve-the-future-state"></a>Förbättra framtida tillstånd stegvis

Innan du använder Azure-distributioner i produktions affärs processer måste moln åtgärderna vara mogna. I samband med varandra krävs ytterligare styrnings ändringar för att säkerställa att till gångar kan köras korrekt.

Ändringarna i det aktuella och framtida läget ger nya risker som kräver nya princip instruktioner.

## <a name="changes-in-tangible-risks"></a>Förändringar i materiella risker

**Affärs avbrott:** Det finns en potentiell risk för en ny plattform som orsakar avbrott i verksamhets kritiska affärs processer. IT-avdelningen och teamen som körs på olika moln-antaganden är relativt inerfarenhet med moln åtgärder. Detta ökar risken för avbrott och måste åtgärdas och regleras.

Den här affärs risken kan utökas till flera tekniska risker:

1. Externt intrång eller denial of Service-attacker kan orsaka affärs avbrott.
2. Uppdrags kritiska till gångar kanske inte identifieras korrekt och kan därför inte användas på rätt sätt.
3. Identifierade eller felmärkta till gångar kanske inte stöds av befintliga processer för drift hantering.
4. Konfigurationen av distribuerade till gångar kanske inte uppfyller prestanda förväntningarna.
5. Loggningen kanske inte är korrekt inspelad och centraliserad för att möjliggöra reparationer av prestanda problem.
6. Återställnings principer kan Miss lyckas eller tar längre tid än förväntat.
7. Inkonsekventa distributions processer kan leda till säkerhets luckor som kan leda till data läckor eller avbrott.
8. Konfigurations luckor eller missade korrigeringar kan leda till oönskade säkerhets luckor som kan leda till data läckor eller avbrott.
9. Konfigurationen kanske inte tillämpar kraven för definierade service avtal eller krav för allokerad återställning.
10. Distribuerade operativ system eller program kanske inte uppfyller härdnings kraven.
11. Med så många team som arbetar i molnet, finns det risk för inkonsekvens.

## <a name="incremental-improvement-of-the-policy-statements"></a>Stegvis förbättring av princip uttrycken

Följande ändringar i principen hjälper dig att åtgärda de nya riskerna och guidens implementering. Listan ser länge ut, men det kan vara lättare att införa dessa principer.

1. Alla distribuerade till gångar måste kategoriseras efter allvarlighets grad och data klassificering. Klassificeringarna bör granskas av moln styrnings teamet och program ägaren innan distributionen till molnet.
2. Undernät som innehåller verksamhets kritiska program måste skyddas av en brand Väggs lösning som kan upptäcka intrång och reagera på attacker.
3. Styrnings verktyg måste granska och genomdriva krav på nätverks konfiguration som definieras av Security Management-teamet.
4. Styrnings verktyg måste kontrol lera att alla till gångar som är relaterade till verksamhets kritiska appar eller skyddade data ingår i övervakningen av resurs uttömdning och optimering.
5. Styrnings verktyg måste verifiera att lämplig nivå av loggnings data samlas in för alla verksamhets kritiska program eller skyddade data.
6. Styrnings processen måste verifiera att säkerhets kopiering, återställning och SLA-krav implementeras korrekt för verksamhets kritiska program och skyddade data.
7. Styrnings verktyg måste begränsa distribution av virtuella datorer till enbart godkända avbildningar.
8. Styrnings verktyg måste framtvinga att automatiska uppdateringar förhindras på alla distribuerade till gångar som stöder verksamhets kritiska program. Överträdelser måste granskas med operativa hanterings team och åtgärdas i enlighet med Operations policys. Till gångar som inte uppdateras automatiskt måste ingå i processer som ägs av IT-åtgärder.
9. Styrnings verktyg måste verifiera taggning relaterad till kostnader, allvarlighets grad, SLA, program och data klassificering. Alla värden måste justeras mot fördefinierade värden som hanteras av styrnings teamet.
10. Styrnings processer måste innehålla revisioner vid distributions platsen och regelbundet för att säkerställa konsekvens för alla till gångar.
11. Trender och utnyttjande som kan påverka moln distributioner bör regelbundet granskas av säkerhets teamet för att tillhandahålla uppdateringar av verktyg för säkerhets hantering som används i molnet.
12. Innan du släpper i produktionen måste alla verksamhets kritiska appar och skyddade data läggas till i den avsedda operativa övervaknings lösningen. Till gångar som inte kan identifieras av den valda IT-driften, kan inte släppas för produktions användning. Eventuella ändringar som krävs för att göra till gångar som kan identifieras måste göras till de relevanta distributions processerna för att se till att till gångar kan upptäckas i framtida distributioner.
13. När det upptäcks kommer operativa hanterings team att ändra till gångar, så att till gångar uppfyller prestanda kraven.
14. Distributions verktyg måste godkännas av moln styrnings teamet för att säkerställa fort löp ande styrning av distribuerade till gångar.
15. Distributions skripten måste finnas i en central lagrings plats som kan nås av moln styrnings teamet för regelbunden granskning och granskning.
16. Gransknings processer för styrning måste verifiera att distribuerade till gångar är korrekt konfigurerade i justering med SLA-och återställnings krav.

## <a name="incremental-improvement-of-governance-practices"></a>Inkrementell förbättring av styrningsmetoder

Det här avsnittet av artikeln ändrar designen för styrnings MVP till att inkludera nya Azure-principer och en implementering av Azure Cost Management. Tillsammans kommer dessa två design ändringar att uppfylla de nya företags princip satserna.

1. Moln drifts teamet definierar verktyg för drift övervakning och automatiserad reparation. Moln styrnings teamet kommer att ha stöd för dessa identifierings processer. I det här användnings fallet väljer moln drifts teamet Azure Monitor som det primära verktyget för övervakning av verksamhets kritiska program.
2. Skapa en lagrings plats i Azure DevOps för att lagra och version av alla relevanta Resource Manager-mallar och skriptbaserade konfigurationer.
3. Implementering av Azure Recovery Services Vault:
    1. Definiera och Distribuera Azure Recovery Services Vault för säkerhets kopierings-och återställnings processer.
    2. Skapa en Resource Manager-mall för att skapa ett valv i varje prenumeration.
4. Uppdatera Azure Policy för alla prenumerationer:
    1. Granska och Genomdriv allvarlighets grad och data klassificering för alla prenumerationer för att identifiera prenumerationer med verksamhets kritiska till gångar.
    2. Granska och Använd endast godkända avbildningar.
5. Azure Monitor implementering:
    1. När en verksamhets kritisk arbets belastning har identifierats skapar du en Azure Monitor-arbetsyta.
    2. Under testningen av distributionen distribuerar moln drifts teamet de nödvändiga agenterna och testerna.
6. Uppdatera Azure Policy för alla prenumerationer som innehåller verksamhets kritiska program.
    1. Granska och framtvinga tillämpning av en NSG för alla nätverkskort och undernät. Nätverks-och IT-säkerhet definierar NSG.
    2. Granska och tillämpa användningen av godkända nätverks under nät och virtuella nätverk för varje nätverks gränssnitt.
    3. Granska och genomdriva begränsningen för användardefinierade vägvals tabeller.
    4. Granska och tillämpa distribution av Azure Monitor agenter för alla virtuella datorer.
    5. Granska och genomdriva att Azure Recovery Services-valv finns i prenumerationen.
7. Brandväggskonfiguration:
    1. Identifiera en konfiguration av Azure-brandväggen som uppfyller säkerhets kraven. Du kan också identifiera en tredje parts apparat som är kompatibel med Azure.
    1. Skapa en Resource Manager-mall för att distribuera brand väggen med nödvändiga konfigurationer.
8. Azure-skiss:
    1. Skapa en ny Azure-skiss med namnet `protected-data`.
    2. Lägg till brand väggen och Azure Vault-mallarna i skissen.
    3. Lägg till de nya principerna för skyddade data prenumerationer.
    4. Publicera skissen till alla hanterings grupper som ska vara värd för verksamhets kritiska program.
    5. Använd den nya skissen för varje berörd prenumeration samt befintliga ritningar.

## <a name="conclusion"></a>Sammanfattning

Dessa ytterligare processer och ändringar i styrnings-MVP: n hjälper till att åtgärda många av de risker som är kopplade till resurs styrning. Tillsammans ger de till gång till återställnings-, storleks-och övervaknings kontroller som ger moln medveten drift.

## <a name="next-steps"></a>Nästa steg

När moln implementeringen fortsätter och levererar ytterligare affärs värde, kommer risker och moln styrnings behov också att ändras. För det fiktiva företaget i den här hand boken är nästa utlösare när distributions skalan överskrider 100 till gångar till molnet eller månads kostnaden överskrider $1 000 per månad. I det här läget lägger moln styrnings teamet till Cost Management kontroller.

> [!div class="nextstepaction"]
> [Förbättra Cost Management](./cost-management-improvement.md)
