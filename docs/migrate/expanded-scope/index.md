---
title: Checklista för molnmigrering med utökat omfång
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Checklista för molnmigrering med utökat omfång
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/19/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 4daf4b01a2fde83de1040f224b8096475a24fe60
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/24/2019
ms.locfileid: "71224354"
---
# <a name="expanded-scope-for-cloud-migration"></a>Utökat omfång för molnmigrering

[Azure-migreringsguiden](../azure-migration-guide/index.md) i Cloud Adoption Framework är den rekommenderade startpunkten för läsare som är intresserade av en värdbytesmigrering till Azure, vilket även kallas ”lift and shift”-migrering. Guiden vägleder dig genom ett antal förutsättningar, verktyg och metoder för att migrera virtuella datorer till molnet.

Den här guiden är en effektiv baslinje som du gör dig bekant med den här typen av migrering, men den inbegriper vissa antaganden. Dessa antaganden inriktar guiden med en stor andel av Cloud Adoption Frameworks läsare genom att tillhandahålla en förenklad metod för migreringar. I det här Cloud Adoption Framework-avsnittet behandlas vissa migreringsscenarier med utökat omfång, vilket ger vägledning till projekt som de antagandena inte gäller för.

## <a name="cloud-migration-expanded-scope-checklist"></a>Checklista för molnmigrering med utökat omfång

I följande checklista visas vanliga komplexitetsområden som kan kräva att migreringens omfång utökas bortom [Azure-migreringsguiden](../azure-migration-guide/index.md).

- **Affärsdrivna omfångsändringar:**
  - [Balansera portföljen](./balance-the-portfolio.md)
  - [Stöd för globala marknader](../../decision-guides/regions/index.md)
  - Kostnadsmedvetenhet under en migrering *(kommer Q3 2019)*
- **Kulturdrivna omfångsändringar:**
  - Ändringshantering och godkännandeprocesser *(kommer Q3 2019)*
  - Chefsberedskap *(kommer Q3 2019)*
  - [Kunskapsberedskap](./suggested-skills.md)
  - Inrikta stöd (partner, tjänster och support) *(kommer Q3 2019)*
- **Omfångsändringar baserade på teknisk strategi:**
  - Begränsningar i befintliga datacenter *(kommer Q3 2019)*
  - Migrering i stor skala – hög volym eller hastighet för migreringar *(kommer Q3 2019)*
  - [Flera datacenter](./multiple-datacenters.md)
  - [Datakraven överskrider nätverkskapaciteten](./network-capacity-exceeded.md)
  - Ändringshantering och lösningsdokumentation *(kommer Q3 2019)*
  - [Strategi för styrning eller efterlevnad](./governance-or-compliance.md)
- **Arbetsbelastningsspecifika omfångsändringar:**
  - Utforma arbetsbelastningar för motståndskraft *(kommer Q3 2019)*
  - Inrikta migrering med programmönster *(kommer Q3 2019)*

Om någon av dessa komplexiteter överensstämmer med ditt scenario kommer det här Cloud Adoption Framework-avsnittet sannolikt att ge den typ av vägledning som behövs för att korrekta inrikta omfånget i migreringsprocesserna.

Vart och ett av de här scenarierna behandlas av de olika artiklarna i det här Cloud Adoption Framework-avsnittet.

## <a name="scope-options-explained"></a>Förklaring av omfångsalternativ

För att hjälpa dig förstå vare scenario för omfångsutökning ges i följande lista en kort sammanfattning av de rubriker som används i ovanstående checklista.

### <a name="business-driven-scope-changes"></a>Affärsdrivna omfångsändringar

- **Balansera portföljen för molnimplementering:** Teamet för molnstrategi är intresserade av att investera mer i migrering (värdbyte av befintliga arbetsbelastningar och program med minimala ändringar) eller innovation (refaktorisering eller återskapande av de arbetsbelastningar eller program som använder modern molnteknik). Ofta är balans mellan de två prioriteringarna nyckeln till framgång. I den här guiden balansering av portföljen för molnimplementering ett övergripande ämne som behandlas i varje migreringsprocess.
- **Stöd för globala marknader:** Verksamheten verkar i flera geografiska områden med olika krav för datasuveränitet. För att uppfylla de kraven bör ytterligare överväganden tas med i beräkningen för granskningen av förutsättningar och distributionen av tillgångar under migrering.

### <a name="culture-driven-scope-changes"></a>Kulturdrivna omfångsändringar

- **Ändringshantering och godkännandeprocesser:** När din organisations kultur är komplex, starkt matrisbaserad eller silobaserad blir processerna för ändringshantering och godkännanden utmanande. Vägledning om hur du hanterar den här komplexiteten finns i processerna för utvärdering, migrering och optimering.
- **Chefsberedskap:** Rätt nivå av chefsstöd och ledarskap är mycket viktigt för att migreringsarbete ska lyckas. Om chefsteamet inte är redo att engagera är det osannolikt att stödet följer därefter. Den här komplexiteten behandlas under processerna för förutsättningar och utvärdering.
- **Kunskapsberedskap:** När molnimplementeringsteamet eller andra stödjande team inte är redo att genomföra implementeringen kan det snabbt medföra komplexitet i migreringsarbetet. Den här utmaningen behandlas under var och en av migreringsprocesserna på en särskild sida om kunskapsberedskap.
- **Inrikta stöd (alternativ för partner, tjänster och support):** I var och en av de processer som beskrivs finns sätt för en partner, tjänster från molnleverantören och stöd från molnleverantören att underlätta genomförandet. I vart och ett av processavsnitten finns det en sida om stödinriktning där alternativen beskrivs närmare.

### <a name="technical-strategy-driven-scope-changes"></a>Omfångsändringar baserade på teknisk strategi

- **Begränsningar i befintliga datacenter:** Företag väljer ofta att migrera till molnet eftersom kapaciteten, hastigheten och stabiliteten hos ett befintligt datacenter inte längre räcker till. Tyvärr ökar dessa begränsningar komplexiteten i migreringsprocessen, vilket gör att ytterligare planering krävs under processerna för utvärdering och migrering.
- **Migrering i stor skala:** Migreringar som överstiger 2 000 tillgångar kommer sannolikt stöta på begränsningar som kräver ytterligare planering och en disciplinerad metod för genomförande. Processerna för utvärdering och migrering justeras för att ta med komplexiteten för skala i beräkningen.
- **Flera datacenter:** Migrering av flera datacenter ökar komplexiteten avsevärt. Under processerna för utvärdering, optimering och hantering diskuteras ytterligare överväganden.
- **Ändringshantering och lösningsdokumentation:** Stora inventarier med digital egendom, komplexa lösningsarkitekturer, långvarig teknisk skuld och beroendeförhållanden kan ge upphov till en komplexitet som bör behandlas under processerna för utvärdering, migrering och optimering.
- **Strategi för styrning eller efterlevnad:** När styrning och efterlevnad är viktiga för att en migrering ska lyckas krävs ytterligare inriktning mellan IT-styrningsteamen och teamen för molnimplementering.

### <a name="workload-specific-scope-changes"></a>Arbetsbelastningsspecifika omfångsändringar

- **Utforma arbetsbelastningar för motståndskraft:** Gemensamma molndesignprinciper kan underlätta förberedelsen av verksamhetskritiska arbetsbelastningar för förbättrad motståndskraft. Den här artikeln förklarar effekten på en migreringsprocess när motståndskraft är ett arbetsbelastningskrav. Den går även igenom några gemensamma principer som kan inkluderas i den allmänna miljökonfigurationen för att förbättra miljöns motståndskraft.
- **Inrikta migrering med programmönster:** Migreringsmönstret för en arbetsbelastning kan påverka den migreringsväg som väljs. I den här artikeln beskrivs några omfångsändringar som skulle integreras på arbetsobjektnivå för en migreringsuppgiftslista för att spegla olika metoder för migrering per arbetsbelastning.

## <a name="next-steps"></a>Nästa steg

Bläddra i innehållsförteckningen till vänster för att åtgärda specifika behov eller omfångsändringar. Alternativt utgör den första omfångsförbättringen i listan, [Balansera portföljen](./balance-the-portfolio.md), en bra startpunkt vid granskning av dessa scenarier.

> [!div class="nextstepaction"]
> [Balansera portföljen](./balance-the-portfolio.md)
