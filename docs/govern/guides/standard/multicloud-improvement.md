---
title: 'Standard Enterprise-guide: Förbättringar i multimolnet'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: 'Standard Enterprise-guide: Förbättringar i multimolnet'
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: d1953e190e2581d96db443be00aad74a6b94d5f9
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/16/2019
ms.locfileid: "71028440"
---
# <a name="small-to-medium-enterprise-guide-multicloud-improvement"></a>Guide för små till medel stora företag: Förbättringar i multimolnet

Den här artikeln går vidare genom att lägga till kontroller för att införa ett moln.

## <a name="advancing-the-narrative"></a>Med den här berättelsenn

Microsoft känner av att kunderna använder flera moln för ett bestämt syfte. Den fiktiva kunden i den här guiden är inget undantag. Parallellt med Azures implementerings resa har företags framgångar lett till förvärvet av en liten, men komplett verksamhet. Företaget kör alla sina IT-åtgärder på en annan moln leverantör.

Den här artikeln beskriver hur saker ändras när den nya organisationen integreras. Vi förutsätter att företaget har slutfört var och en av de styrnings iterationer som beskrivs i den här styrnings guiden.

### <a name="changes-in-the-current-state"></a>Ändringar i det aktuella läget

I föregående fas av den här delen hade företaget börjat aktivt skicka produktions program till molnet via CI/CD-pipelines.

Sedan dess har vissa saker ändrats som påverkar styrning:

- Identiteten styrs av en lokal instans av Active Directory. Hybrid identitet under lättas genom replikering till Azure Active Directory.
- IT-åtgärder eller moln åtgärder hanteras i stor utsträckning av Azure Monitor och relaterade automatiseringar.
- Haveri beredskap/affärs kontinuiteten kontrol leras av Azure Vault instances.
- Azure Security Center används för att övervaka säkerhets överträdelser och attacker.
- Azure Security Center och Azure Monitor används båda för att övervaka styrning av molnet.
- Azure-ritningar, Azure Policy och Azure-hanterings grupper används för att automatisera efterlevnaden av principen.

### <a name="incrementally-improve-the-future-state"></a>Förbättra framtida tillstånd stegvis

Målet är att integrera förvärvs företaget i befintliga åtgärder där det är möjligt.

## <a name="changes-in-tangible-risks"></a>Förändringar i materiella risker

**Företags förvärvs kostnad:** Förvärv av den nya verksamheten beräknas vara lönsam på ungefär fem år. På grund av den långsamma avkastnings graden vill styrelsen kontrol lera anskaffnings kostnaderna så mycket som möjligt. Det finns en risk för kostnads kontroll och teknisk integrering som står i konflikt med varandra.

Den här affärs risken kan utökas till några tekniska risker:

- Molnbaserad migrering kan producera ytterligare anskaffnings kostnader.
- Den nya miljön är kanske inte korrekt styrd, vilket kan leda till princip överträdelser.

## <a name="incremental-improvement-of-the-policy-statements"></a>Stegvis förbättring av princip uttrycken

Följande ändringar i principen hjälper dig att åtgärda de nya riskerna och vägledningen:

- Alla till gångar i ett sekundärt moln måste övervakas via befintliga verktyg för drift hantering och säkerhets övervakning.
- Alla organisations enheter måste vara integrerade i den befintliga identitets leverantören.
- Den primära identitets leverantören bör styra autentiseringen till till gångar i det sekundära molnet.

## <a name="incremental-improvement-of-governance-practices"></a>Inkrementell förbättring av styrningsmetoder

Det här avsnittet av artikeln ändrar designen för styrnings MVP till att inkludera nya Azure-principer och en implementering av Azure Cost Management. Tillsammans uppfyller dessa design ändringar de nya företags princip uttrycken.

1. Anslut nätverken. Det här steget utförs av nätverkets och IT-säkerhetsteamen och stöds av moln styrnings teamet. Om du lägger till en anslutning från MPLS/lånad rad leverantör till det nya molnet integreras nätverk. Genom att lägga till routningstabeller och brand Väggs konfigurationer styr du åtkomst och trafik mellan miljöerna.
1. Konsolidera identitets leverantörer. Beroende på vilka arbets belastningar som finns i det sekundära molnet finns det en mängd olika alternativ för konsolidering av identitets leverantörer. Följande är några exempel:
    1. För program som autentiserar med OAuth 2 kan användare från Active Directory i det sekundära molnet bara replikeras till den befintliga Azure AD-klienten. Detta säkerställer att alla användare kan autentiseras i klienten.
    1. I den andra extrema federationen tillåter Federation att ou flödar till Active Directory lokalt, sedan till Azure AD-instansen.
1. Lägg till till gångar till Azure Site Recovery.
    1. Azure Site Recovery har utformats från början som ett hybrid-eller multicloud-verktyg.
    1. Virtuella datorer i det sekundära molnet kan vara skyddade av samma Azure Site Recovery processer som används för att skydda lokala till gångar.
1. Lägg till till gångar till Azure Cost Management.
    1. Azure Cost Management har utformats från början som ett multimoln-verktyg.
    1. Virtuella datorer i det sekundära molnet kan vara kompatibla med Azure Cost Management för vissa moln leverantörer. Ytterligare kostnader kan tillkomma.
1. Lägg till till gångar till Azure Monitor.
    1. Azure Monitor utformades som ett hybrid moln verktyg från början.
    1. Virtuella datorer i det sekundära molnet kan vara kompatibla med Azure Monitor agenter, så att de kan tas med i Azure Monitor för drifts övervakning.
1. Använd verk ställande verktyg för styrning.
    1. Styrnings tvång är molnbaserad.
    1. Företags principerna som fastställs i styrnings guiden är inte molnbaserade. Implementeringen kan variera från molnet till molnet, men principerna kan tillämpas på den sekundära providern.

När ett moln har införts växer fortsätter design ändringarna ovan att fortsätta till vuxen.

## <a name="conclusion"></a>Sammanfattning

I den här artikel serien beskrivs den stegvisa utvecklingen av styrningens bästa metoder, justerade med upplevelsen av det här fiktiva företaget. Genom att starta små, men med rätt bas, kunde företaget flytta snabbt och fortfarande använda rätt mängd styrning vid rätt tidpunkt. Själva MVP: en skyddar inte kunden. I stället skapade den grunden för att hantera risker och lägga till skydd. Därifrån har du tillämpat styrnings nivåer för att åtgärda konkreta risker. Den exakta resan som presenteras här justerar inte 100% med upplevelsen av någon läsare. I stället fungerar det som ett mönster för stegvis styrning. Läsaren uppmanas att forma dessa bästa metoder för att passa sina egna unika begränsningar och styrnings krav.