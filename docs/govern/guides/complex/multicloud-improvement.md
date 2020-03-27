---
title: 'Komplex företags styrning: multicloud-förbättringar'
description: Använd ramverket för moln införande för Azure för att lära dig mer om flera moln och hur du integrerar flera moln organisationer för komplexa företag.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 05ee11a452044157458d5c27f3f1f522f0f1e617
ms.sourcegitcommit: ea63be7fa94a75335223bd84d065ad3ea1d54fdb
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/27/2020
ms.locfileid: "80357071"
---
<!-- cSpell:ignore MPLS -->

# <a name="governance-guide-for-complex-enterprises-multicloud-improvement"></a>Styrnings guide för komplexa företag: förbättringar i multimolnet

## <a name="advancing-the-narrative"></a>Med den här berättelsenn

Microsoft känner av att kunderna kan använda flera moln för olika behov. Det fiktiva företaget i den här hand boken är inget undantag. På parallellt med deras Azure-implementering har företags framgång lett till förvärv av en liten men kompletterande verksamhet. Företaget kör alla sina IT-åtgärder på en annan moln leverantör.

Den här artikeln beskriver hur saker ändras när den nya organisationen integreras. Vi förutsätter att företaget har slutfört var och en av de styrnings iterationer som beskrivs i den här styrnings guiden.

### <a name="changes-in-the-current-state"></a>Ändringar i det aktuella läget

I föregående fas av den här delen hade företaget börjat implementera kostnads kontroller och kostnads övervakning, eftersom moln utgifter blir en del av företagets regelbundna drifts kostnader.

Sedan dess har vissa saker ändrats som påverkar styrning:

- Identiteten styrs av en lokal instans av Active Directory. Hybrid identitet under lättas genom replikering till Azure Active Directory.
- IT-åtgärder eller moln åtgärder hanteras i stor utsträckning av Azure Monitor och relaterade automatiserings funktioner.
- Verksamhets kontinuitet och haveri beredskap (BCDR) styrs av Azure Vault instances.
- Azure Security Center används för att övervaka säkerhets överträdelser och attacker.
- Azure Security Center och Azure Monitor används båda för att övervaka styrning av molnet.
- Azure-ritningar, Azure Policy-och hanterings grupper används för att automatisera efterlevnaden av principen.

### <a name="incrementally-improve-the-future-state"></a>Förbättra framtida tillstånd stegvis

Målet är att integrera förvärvs företaget i befintliga åtgärder där det är möjligt.

## <a name="changes-in-tangible-risks"></a>Förändringar i materiella risker

**Företags förvärvs kostnad:** Förvärv av den nya verksamheten beräknas vara lönsam på ungefär fem år. På grund av den långsamma avkastnings graden vill styrelsen kontrol lera anskaffnings kostnaderna så mycket som möjligt. Det finns en risk för kostnads kontroll och teknisk integrering som står i konflikt med varandra.

Den här affärs risken kan utökas till några tekniska risker:

- Det finns en risk för att molnbaserad migrering producerar ytterligare anskaffnings kostnader.
- Det finns också en risk för att den nya miljön inte regleras på ett korrekt sätt eller resulterar i princip överträdelser.

## <a name="incremental-improvement-of-the-policy-statements"></a>Stegvis förbättring av princip uttrycken

Följande ändringar i principen hjälper dig att åtgärda de nya riskerna och guidens implementering.

- Alla till gångar i ett sekundärt moln måste övervakas via befintliga verktyg för drift hantering och säkerhets övervakning.
- Alla organisationsenheter måste vara integrerade i den befintliga identitets leverantören.
- Den primära identitets leverantören bör styra autentiseringen till till gångar i det sekundära molnet.

## <a name="incremental-improvement-of-the-best-practices"></a>Stegvis förbättring av bästa praxis

Det här avsnittet av artikeln förbättrar designen för styrnings MVP till att inkludera nya Azure-principer och en implementering av Azure Cost Management. Tillsammans kommer dessa två design ändringar att uppfylla de nya företags princip satserna.

1. Anslut nätverken. Utföras av nätverk och IT-säkerhet, stöds av styrning.
    1. Om du lägger till en anslutning från MPLS eller lånad rad leverantör till det nya molnet integreras nätverk. Genom att lägga till routningstabeller och brand Väggs konfigurationer styr du åtkomst och trafik mellan miljöerna.
2. Konsolidera identitets leverantörer. Beroende på vilka arbets belastningar som finns i det sekundära molnet finns det en mängd olika alternativ för konsolidering av identitets leverantörer. Detta är några exempel:
    1. För program som autentiserar med OAuth 2 kan användare i Active Directory i det sekundära molnet enkelt replikeras till den befintliga Azure AD-klienten.
    2. På den andra extrema, kan federationen mellan de två lokala identitets leverantörerna tillåta användare från de nya Active Directory-domänerna att replikeras till Azure.
3. Lägg till till gångar till Azure Site Recovery.
    1. Azure Site Recovery har skapats som ett hybrid-och multicloud-verktyg från början.
    2. Virtuella datorer i det sekundära molnet kan vara skyddade av samma Azure Site Recovery processer som används för att skydda lokala till gångar.
4. Lägg till till gångar till Azure Cost Management.
    1. Azure Cost Management har skapats som ett multicloud-verktyg från början.
    2. Virtuella datorer i det sekundära molnet kan vara kompatibla med Azure Cost Management för vissa moln leverantörer. Ytterligare kostnader kan tillkomma.
5. Lägg till till gångar till Azure Monitor.
    1. Azure Monitor har skapats som ett hybrid moln verktyg från början.
    2. Virtuella datorer i det sekundära molnet kan vara kompatibla med Azure Monitor agenter, så att de kan tas med i Azure Monitor för drifts övervakning.
6. Verk ställande verktyg för styrning.
    1. Styrnings tvång är molnbaserad.
    2. Företags principerna som fastställs i styrnings guiden är inte molnbaserade. Implementeringen kan variera från molnet till molnet, men princip instruktionerna kan tillämpas på den sekundära providern.

För att kunna använda molnet bör det finnas ett krav som baseras på tekniska behov eller specifika affärs behov. Allt eftersom införandet av molnet växer ökar komplexiteten och säkerhets riskerna.

## <a name="next-steps"></a>Nästa steg

I många stora företag kan de fem disciplinerna i moln styrning vara Blocker att fatta. Nästa artikel har några ytterligare idéer om hur du kan göra styrningen till en grupp sport för att säkerställa långsiktig framgång i molnet.

> [!div class="nextstepaction"]
> [Flera olika styrnings nivåer](./multiple-layers-of-governance.md)
