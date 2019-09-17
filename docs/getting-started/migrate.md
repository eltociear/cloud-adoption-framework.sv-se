---
title: Komma igång med en moln migrerings resa
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Komma igång med en moln migrerings resa
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: overview
ms.openlocfilehash: 7c35d64e3106c2a34670d4dc05614de087f5d5c3
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/16/2019
ms.locfileid: "71023420"
---
# <a name="getting-started-with-a-cloud-migration-journey"></a>Komma igång med en moln migrerings resa

Lär dig mer om att använda Microsoft Cloud implementerings ramverk för Azure för att påbörja en migrering av moln migrering. Det här ramverket innehåller omfattande vägledning för över gång av äldre program arbets belastningar med hjälp av innovativa molnbaserade tekniker.

## <a name="executive-summary"></a>Sammanfattning

Ramverket för moln införande hjälper kunder att åta sig en förenklad moln implementering. Det här ramverket innehåller detaljerad information som täcker en slutpunkt-till-slutpunkt-körning av molnet, som börjar med riktade affärs resultat och justerar moln beredskap och-utvärderingar med tydliga definierade affärs mål. Dessa resultat uppnås via en definierad sökväg för moln införande. Med migration-baserad implementering fokuserar den definierade sökvägen i stor utsträckning på att slutföra en migrering av lokala arbets belastningar till molnet. Ibland omfattar den här resan modernisering av arbets belastningar för att öka avkastningen på investeringar från migreringens ansträngning.

Det här ramverket är främst utformat för moln arkitekter och moln strategi team som leder till moln implementerings ansträngningar. Många ämnen i det här ramverket är dock relevanta för andra roller i företaget och det. Cloud Architects fungerar ofta som underlättare för att engagera var och en av de relevanta rollerna. Den här exekutiva sammanfattningen är utformad för att förbereda de olika rollerna innan du underlätterar konversationer.

> [!NOTE]
> Den här vägledningen är för närvarande en offentlig för hands version. Terminologi, metoder och vägledning testas grundligt med kunder, partner och Microsoft Teams under för hands versionen. Därför kan innehålls förteckningen och vägledningen ändras något över tid.

## <a name="motivations"></a>Motiveringar

Moln migreringar kan hjälpa företag att uppnå sina önskade affärs resultat. En tydligare kommunikation av motivation, affärs drivande faktorer och mätningar av framgång är viktiga grunder för att fatta beslut i hela moln migreringen. I följande tabell klassificeras motiveringar för att under lätta den här konversationen. Det förutsätts att de flesta företag kommer att ha motivation i varje klassificering. Syftet med den här tabellen är inte att begränsa resultat, utan i stället gör det lättare att prioritera övergripande mål och motivation:

<!-- markdownlint-disable MD033 -->

|Kritiska affärs händelser | Motivation vid migrering | Nyskapande motivation |
|---------|---------|---------|
| Avsluta data Center<br/><br/>Sammanslagningar, förvärv eller Divestiture<br/><br/>Minskning av kapital utgifter<br/><br/>Slut på support för verksamhets kritiska tekniker<br/><br/>Svar på ändringar i regelefterlevnad<br/><br/>Möta nya krav för data suveränitet<br/><br/>Minska störningar och förbättra IT-stabiliteten|Kostnadsbesparingar<br/><br/>Minskning av leverantör eller teknisk komplexitet<br/><br/>Optimering av interna åtgärder<br/><br/>Öka affärsflexibiliteten<br/><br/>Förbered dig för nya tekniska funktioner<br/><br/>Skala för att uppfylla marknadens krav<br/><br/>Skala för att uppfylla geografiska krav|Förbered dig för nya tekniska funktioner<br/><br/>Bygg nya tekniska funktioner<br/><br/>Skala för att uppfylla marknadens krav<br/><br/>Skala för att uppfylla geografiska krav<br/><br/>Förbättra kund upplevelse/engagemang<br/><br/>Omvandla produkter eller tjänster<br/><br/>Störa marknaden med nya produkter eller tjänster|

<!-- markdownlint-enable MD033 -->

När ett svar på kritiska affärs händelser är den högsta prioriteten är det viktigt att delta i [moln implementering](#cloud-implementation) tidigt, ofta parallellt med strategi och planerings ansträngningar. Att vidta en sådan metod kräver en tillväxt tänkesätt och en möjlighet att upprepade gånger förbättra processer, baserat på de direkt lektioner som du har lärt dig.

När en förflyttnings motivation är en prioritet, kommer [strategi och planering](#cloud-strategy-and-planning) att spela en viktig roll tidigt i processen. Det rekommenderas dock starkt att [implementeringen](#cloud-implementation) av den första arbets belastningen utförs parallellt med planering, för att hjälpa teamet att förstå och planera för de inlärnings kurvor som är kopplade till molnet.

När Innovations motivation är den högsta prioriteten kräver strategin och planeringen ytterligare investeringar tidigt i processen för att säkerställa balans i portföljen och göra anpassningen av investeringen i molnet. Mer information om hur du realiserar nyskapande motivation finns i [förstå Innovations resan](./innovate.md).

Att förbereda alla deltagare över migreringens ansträngning med en medvetenhet om motivationen garanterar att du får ett välfattande beslut. Följande metod för migrering beskriver hur Microsoft föreslår att kunderna vägleder dessa beslut i en konsekvent metod.

## <a name="migration-approach"></a>Metod för migrering

Ramverket för moln införande upprättar en övergripande uppbyggnad av plan, klar, och antar de typer av insatser som krävs för alla moln införande. Den här exekutiva sammanfattningen bygger på det högnivå flödet för att upprätta iterativa processer som kan under lätta lyft/Shift/optimera insatser **och** modernisering ansträngningar i en enda metod i alla aktiviteter för moln migrering.

Den här metoden består av två metoder eller fokus områden: Moln strategi & planering och moln implementering. [Motivet](#motivations) eller det önskade affärs resultatet för en molnbaserad migrering bestämmer ofta hur mycket ett team bör investera i [strategi och planering](#cloud-strategy-and-planning) och [implementering](#cloud-implementation). Dessa motivation kan också påverka besluten att köra var för sig eller parallellt.

## <a name="cloud-implementation"></a>Moln implementering

Cloud implementation är en iterativ process för att migrera och ställa av den digitala fastigheten i justering med riktade företags resultat och ändrings hanterings kontroller. Under varje iteration migreras eller förvaras arbets belastningar i justeringen med strategin och planen. Beslut om IaaS, PaaS eller hybrider görs under utvärderings fasen till optimerad kontroll och körning. Dessa beslut kommer att driva de verktyg som används under migreringen. Den här modellen kan användas med minimal strategi och planering. Men för att säkerställa bästa möjliga affärs avkastning, rekommenderar vi att både IT och verksamheten justeras på en tydlig strategi och planerar att hjälpa implementerings aktiviteterna.

![Moln implementerings ramverkets moln implementerings metod](../_images/operational-transformation-migrate.png)

Fokus på den här ansträngningen är migreringen eller modernisering av arbets belastningar. En arbets belastning är en samling infrastruktur, program och data som gemensamt stöder ett gemensamt affärs mål, eller körning av en gemensam affärs process. Exempel på arbets belastningar kan innefatta saker som ett branschspecifika program, en HR-löne lösning, en CRM-lösning, ett arbets flöde för godkännande av affärs dokument eller en Business Intelligence lösning. Arbets belastningar kan också innehålla delade tekniska resurser som ett informations lager som stöder flera andra lösningar. I vissa fall kan en arbets belastning representeras av en enda till gång som en fristående server, program eller data plattform.

Migrering av moln betraktas ofta som ett enda projekt i ett bredare program för att effektivisera IT-verksamheten, kostnader och komplexitet. Moln implementerings metodiken hjälper till att justera de tekniska ansträngningarna i en serie arbets belastnings migreringar till affärs värden på högre nivå som beskrivs i moln strategin och planen.

**Komma igång:** För att komma igång med en moln implementering, finns guiden [Azure migration guide](../migrate/azure-migration-guide/index.md) och [Azure readiness guide](../ready/azure-readiness-guide/index.md) de verktyg och hög nivå processer som krävs för att lyckas med körningen av en moln implementering. Genom att migrera din första arbets belastning med hjälp av de här guiderna får du hjälp att lösa inledande inlärnings kurvor tidigt i planerings processen. Därefter bör ytterligare överväganden ges till den [expanderade omfångs check listan](../migrate/expanded-scope/index.md), [metod tips för migrering](../migrate/azure-best-practices/index.md) och [migrering](../migrate/migration-considerations/index.md), för att justera rikt linjerna med din ansträngnings unika begränsningar, processer, team strukturer och mål.

## <a name="cloud-strategy-and-planning"></a>Moln strategi och planering

Moln strategi och planering är en metod som fokuserar på att justera affärs resultat, prioriteringar och begränsningar för att upprätta en klar strategi för migrering och planering. Resultat planen (eller efter släpning av migreringen) beskriver metoden för migrering och modernisering i IT-portföljen, som kan omfatta hela Data Center, flera arbets belastningar eller diverse olika samlingar av infrastruktur, program och data. En korrekt hantering av IT-portföljen i moln implementeringen hjälper till att driva önskade affärs resultat.

![Översikt över Cloud Adoption Framework](../_images/caf-overview.png)

**Komma igång:** I resten av den här artikeln förbereds läsaren för korrekt tillämpning av moln strategi och planerings metodik för moln införande. Det beskriver också ytterligare resurser och länkar som kan hjälpa läsaren att använda den här metoden för att vägleda moln implementerings ansträngningar.

### <a name="methodology-explained"></a>Förklarad metod

Moln strategi-och planerings metodiken i molnet bygger på en stegvis metod för moln implementering som anpassar sig efter smidig teknik strategier, kulturell mognad baserat på tillväxt tänkesätts metoder och strategier som styrs av affärs resultat. Den här metoden består av följande hög nivå komponenter som vägleder implementeringen av varje strategi.

Som du ser i bilden ovan, justerar det här ramverket strategiska beslut till ett litet antal inneslutna processer, som körs inom en iterativ modell. Det beskrivs i ett linjärt dokument och var och en av följande processer förväntas vara mogna parallellt med iterationer av moln implementeringen. Länkarna för varje process har stöd för att definiera slut tillstånd och förfaller till önskat slut tillstånd:

- **[Plan](../strategy/index.md):** När den tekniska implementeringen är justerad med tydliga affärs mål är det mycket enklare att mäta och justera framgång i flera moln implementerings ansträngningar, oavsett tekniska beslut.
- **[Redo](../ready/index.md):** Att förbereda affärs-, kultur-, folk-och miljö för kommande ändringar leder till framgång i varje arbete och påskyndar implementeringen och ändrings projekt.
- **Implementera:** Se till att du har rätt implementering av önskade ändringar, över IT-och affärs processer, för att uppnå affärs resultat.
  - **[Migrera](../migrate/index.md):** Iterativ körning av [moln implementerings metoden](#cloud-implementation) som följer den testade processen för att utvärdera, migrera, optimera och skydda & hantera för att skapa en upprepnings bar process för migrering av arbets belastningar.
- **[Arbeta](../operating-model/index.md):** Definiera en hanterbar drifts modell för att hantera aktiviteter under och länge efter införandet.
  - **[Organisera](../organize/index.md):** Justera människor och team för att leverera rätt moln drift och införande.
  - **[Styrning](../govern/index.md):** Justera företags principen mot materiella risker, med hjälp av princip-, process-och molnbaserad styrnings verktyg.
  - **[Hantera](../manage/index.md):** Utöka IT-driften för att säkerställa att molnbaserade lösningar kan köras genom säkra, kostnads effektiva processer med moderna, molnbaserade drift verktyg.

I den här versionen av migreringen används det här ramverket för att lösa tvetydigheter, hantera ändringar och vägleda arbets grupper med hjälp av affärs resultat.

### <a name="common-cultural-changes-resulting-from-adherence-to-this-methodology"></a>Vanliga kulturella ändringar som orsakas av den här metoden

Ansträngningen för att realisera de önskade affärs resultaten kan utlösa mindre ändringar i kulturen, och till viss grad en viss grad av verksamhetens kultur. Följande är några vanliga kulturella ändringar som visas i den här processen:

- IT-teamet antar förmodligen nya kunskaper för att stödja arbets belastningar i molnet.
- Körningen av en molnbaserad migrering uppmuntrar till iterativa eller flexibla metoder.
- Att ta med moln styrning tenderar också att inspirera DevOps-metoder.
- Att skapa ett moln strategi team kan leda till närmare integration mellan företag och IT-ledare.
- De här ändringarna tenderar att leda till verksamhet och IT-flexibilitet.

Kulturell förändring är inte målet för molnbaserad migrering eller ramverket för moln införande, men det är ett vanligt resultat.
Kulturella ändringar är inte direkt guidade, i stället är de diskreta ändringarna i kulturen inbäddade i de föreslagna process förbättringarna och tillvägagångs sätten i rikt linjerna.

### <a name="common-technical-efforts-associated-with-this-methodology"></a>Vanliga tekniska ansträngningar som är kopplade till den här metoden

Under implementeringen av moln strategin och planerar IT-teamet kommer att fokusera en stor del av sin tid på migreringen av befintliga digitala till gångar till molnet. Under den här ansträngningen förväntas minimala kod ändringar, men de kan ofta begränsas till konfigurations ändringar. I många fall kan en stark affärs justering göras för modernisering som en del av migreringen av molnet.

### <a name="common-workload-examples"></a>Vanliga arbets belastnings exempel

Moln strategi och planering riktar ofta sig till en bred samling arbets belastningar och program. I portföljen migreras vanligt vis vanliga program eller arbets belastnings typer. Följande är några exempel:

- Line-of-business-program
- Program som riktas mot kund
- Program från tredje part
- Plattformar för data analys
- Globalt distribuerade lösningar
- Mycket skalbara lösningar

### <a name="common-technologies-migrated"></a>Vanliga tekniker har migrerats

Tekniken som migreras till molnet ökar ständigt när moln leverantörer lägger till nya funktioner. Här följer några exempel på de tekniker som ofta visas i en migrering:

- Windows och SQL Server
- Linux-databaser och databaser med öppen källkod (OSS)
- Ostrukturera/NoSQL-databaser
- SAP på Azure
- Analys (informations lager, Data Lake)

## <a name="next-steps-lifecycle-solution"></a>Nästa steg: Livs cykel lösning

Ramverket för moln införande är en livs cykel lösning. Den är utformad för att hjälpa läsare som bara påbörjar sin resa, samt läsare som är djupgående i migreringen. Därför är innehållet mycket Sammanhangs beroende och mål grupp. Nästa steg är bäst att justera till den övergripande processen som läsaren vill förbättra härnäst.

> [!div class="nextstepaction"]
> [Planera](../plan/index.md)
>
> [Redo](../ready/index.md)
>
> [Migrera](../migrate/index.md)
>
> [Hantera](../manage/index.md)
>
> [Styras](../govern/index.md)
