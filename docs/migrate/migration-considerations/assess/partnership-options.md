---
title: Förstå partnerskaps- och supportalternativ
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Beskriver alternativ och metoder som stödjer migrering
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 5eabc654c174ac3eff895e6b2ff94700789f5de5
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/17/2019
ms.locfileid: "72549171"
---
# <a name="understand-partnership-options"></a>Förstå partnerskapsalternativ

Under migreringen utför teamet för molnimplementering den faktiska migreringen av arbetsbelastningar till molnet. Till skillnad från de samarbets- och problemlösningsuppgifter som du utför när du definierar [digital egendom](../../../digital-estate/index.md) eller skapar kärninfrastruktur i molnet, brukar migreringen vara en serie repetitiva körningsuppgifter. Utöver de repetitiva aspekterna utförs sannolikt testning och justering som kräver djupgående kunskap hos den valda molnleverantören. Repetitiva typer av processer hanteras ibland bäst av en partner, vilket minskar belastningen på personalen. Dessutom är det ibland enklare för partners att använda djupgående teknisk expertis när de repetitiva processerna ställs inför körningsavvikelser.

Partners har ofta ett nära samarbete med en enda molnleverantör eller ett litet antal molnleverantörer. För att bättre illustrera partnerskapsalternativen antar vi i resten av den här artikeln att Microsoft Azure är den valda molnleverantören.

Under planering, skapande eller migrering har ett företag vanligtvis fyra alternativ när man använder sig av partners:

- **Guidad självbetjäning.** Det befintliga tekniska teamet kör migreringen med hjälp av Microsoft.
- **FastTrack for Azure.** Microsoft FastTrack for Azure-programmet används för att påskynda migreringen.
- **Lösningspartner.** Genom att ansluta sig till Azures lösnings- eller molnlösningspartners kan man påskynda migreringen.
- **Självbetjäning som stöds.** Körningen slutförs av den befintliga tekniska personalen med stöd från Microsoft.

## <a name="guided-self-service"></a>Guidad självbetjäning

Om en organisation planerar en Azure-migrering på egen hand, finns Microsoft alltid där för att underlätta processen. För att hjälpa till att snabbt komma igång med migreringen till Azure har Microsoft och dess partners utvecklat en omfattande uppsättning arkitekturer, guider, verktyg och tjänster som minskar riskerna och påskyndar migreringen av virtuella datorer, program och databaser. Dessa verktyg och tjänster har stöd för ett brett urval av operativsystem, programmeringsspråk, ramverk och databaser.

- **Verktyg för utvärdering och migrering.** Azure innehåller en mängd olika verktyg som kan användas i olika faser vid din molnomvandling, bland annat en utvärdering av din befintliga infrastruktur. Mer information finns i avsnittet ”Utvärdera” i kapitlet ”Migrering” nedan.
- **[Microsoft Cloud Adoption Framework](../../index.md).** I det här ramverket finns en strukturerad metod för molnimplementering och migrering. Den baseras på bästa praxis över många kund engagemang i Microsoft och är ordnade som en serie steg, från arkitektur och design till implementering. För varje steg finns det vägledning som hjälper dig med utformningen av programarkitekturen.
- **[Designmönster för molnet](https://docs.microsoft.com/azure/architecture/patterns).** Azure innehåller användbara molndesignmönster som kan användas till att skapa tillförlitliga, skalbara och säkra arbetsbelastningar i molnet. Varje mönster beskriver problemet som mönstret är avsett att hantera, överväganden när du ska tillämpa mönstret och ett exempel baserat på Azure. De flesta av mönstren innehåller kodexempel eller kodstycken som visar hur du implementerar mönstret i Azure. De avser dock alla typer av distribuerade system, oavsett om det är Azure eller någon annan molnplattform.
- **[Grunderna för molnet](https://docs.microsoft.com/azure/architecture/guide).** I grunderna kan du läsa mer om de grundläggande metoderna för implementering av viktiga begrepp. I guiden får teknisk personal hjälp att tänka ut lösningar som använder sig av mer än en enda Azure-tjänst.
- **[Exempelscenarier](https://docs.microsoft.com/azure/architecture/example-scenario).** Guiden innehåller referenser från verkliga kundimplementeringar och beskriver de verktyg, metoder och processer som tidigare kunder har följt för att uppnå specifika affärsmål.
- **[Referensarkitekturer](https://docs.microsoft.com/azure/architecture/reference-architectures).** Referensarkitekturerna ordnas efter scenario, där relaterade arkitekturer finns i samma grupp. Varje arkitektur innehåller bästa praxis, tillsammans med överväganden för skalbarhet, tillgänglighet, hanterbarhet och säkerhet. De flesta innehåller även en distribuerbar lösning.

## <a name="fasttrack-for-azure"></a>FastTrack for Azure

Med [FastTrack för Azure](https://azure.microsoft.com/roadmap/fasttrack-for-azure) kan du få direkthjälp av Azure-ingenjörer som samarbetar med våra partnerföretag, så att du snabbt och enkelt kan skapa de Azure-lösningar du behöver. FastTrack innehåller metodtips och verktyg från verkliga kundupplevelser som hjälper kunderna från installation, konfiguration och utveckling till produktion av Azure-lösningar, bland annat:

- Datacentermigrering
- Windows Server på Azure
- Linux på Azure
- SAP på Azure
- Affärskontinuitet och haveriberedskap (BCDR)
- Databehandling med höga prestanda*
- Molnbaserade appar
- DevOps
- Appmodernisering
- Analys i molnskala**
- Smarta appar
- Intelligenta agenter**
- Datamodernisering till Azure
- Säkerhet och hantering
- Globalt distribuerade data
- IoT***

*Begränsad förhandsversion i Kanada, Storbritannien, USA och Västeuropa

**Begränsad förhandsversion i Storbritannien och Västeuropa

***Tillgänglig under andra halvåret 2019

Vid ett typiskt FastTrack for Azure-engagemang hjälper Microsoft till med att definiera affärsvisionen när man planerar och utvecklar Azure-lösningar. Teamet bedömer arkitekturbehoven och erbjuder vägledning, designprinciper, verktyg och resurser som hjälper till att skapa, distribuera och hantera Azure-lösningar. Teamet hittar kvalificerade partners för distributionstjänster vid begäran och kontrollerar regelbundet att distributionen fungerar, samt hjälper till att ta bort blockerare.

Följande huvudfaser ingår i ett normalt FastTrack for Azure-engagemang:

- **Identifiering.** Identifiera viktiga intressenter, förstå målet eller visionen för de problem som ska lösas och sedan bedöma arkitekturbehovet.
- **Lösningshantering.** Lär dig designprinciper för att skapa program, granska arkitekturen för program och lösningar, samt få vägledning och verktyg för funktionstest hela vägen fram till produktion.
- **Kontinuerligt partnerskap.** Azures tekniker och programhanterare kontrollerar vid flera tillfällen att distributionen fungerar och hjälper till att ta bort blockerare.

## <a name="microsoft-services-offerings-aligned-to-cloud-adoption-framework-approaches"></a>Microsofts tjänsterbjudanden som är anpassade till Cloud Adoption Framework-metoder

![Microsoft-tjänster – Cloud Adoption Framework-metod](../../../_images/migrate/mcs-program-approach.jpg)

**Utvärdera:** Microsoft-tjänster använder sig av en [enhetlig, data-och verktygs driven metod](https://download.microsoft.com/download/C/7/C/C7CEA89D-7BDB-4E08-B998-737C13107361/Secure_Cloud_Insights_Datasheet_EN_US.pdf) som består av arkitektur workshops, Azure real tids information, säkerhets-och identitets hot modeller och olika verktyg för att ge insikter om utmaningar, risker, rekommendationer och problem med en befintlig Azure-miljö med viktiga resultat som [modernisering-översikt på hög nivå](https://download.microsoft.com/download/F/7/2/F72FAD7E-8BBD-4E04-8C7B-9AC4FE04A150/Cloud_Adoption_Discovery_and_Roadmap_Datasheet.pdf).

**Anta:** Med Microsoft-tjänsternas [Azure Cloud Foundation](https://download.microsoft.com/download/D/8/7/D872DFD0-1C46-4145-95E4-B5EAB2958B96/Hybrid_Cloud_Foundation_Datasheet_EN_US.pdf)kan du upprätta din grundläggande Azure-design, mönster och styrnings arkitektur genom att mappa dina krav till den mest lämpliga referens arkitekturen och planera, utforma och distribuera infrastrukturen. hantering, säkerhet och identitet som krävs för arbets belastningar.

**Migrera/optimera:** Microsoft-tjänsternas [Cloud modernisering-lösning](https://download.microsoft.com/download/3/7/3/373F90E3-8568-44F3-B096-CD9C1CD28AB7/Cloud_Modernization_Datasheet_EN_US.pdf) erbjuder en omfattande metod för att flytta program och infrastruktur till Azure, samt för att optimera och modernisera en gång i molnet som backas upp av strömlinjeformad migrering.

**Förnya:** Microsoft-tjänsternas [CCoE-lösning (Cloud Center of expert)](https://download.microsoft.com/download/F/8/B/F8BBE4BD-E5F8-4DFB-82F7-C0A4E17051BB/Cloud_Center_of_Excellence_Datasheet_EN_US.pdf) erbjuder ett DevOps coaching-engagemang och använder DevOps-principer tillsammans med fördefinierad molnbaserad tjänst hantering och säkerhets kontroller för att hjälpa till att driva företags innovation, öka flexibiliteten och minska tiden till värde inom en säker, förutsägbar och flexibel tjänst leverans-och hanterings funktioner för tjänster.

## <a name="azure-support"></a>Azure Support

Om du har frågor eller behöver hjälp kan du [skapa en supportbegäran](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/newsupportrequest). Om din supportbegäran kräver djupgående teknisk vägledning kan du gå till [Azure Support-avtal](https://azure.microsoft.com/support/plans) för att få det lämpligaste avtalet för dina behov.

## <a name="azure-solutions-partner"></a>Azure-lösningspartner

Microsofts certifierade lösningsleverantörer är specialister på de senaste lösningarna som baseras på teknik från Microsoft för kunder i hela världen. Ta hjälp av en erfaren partner och optimera din verksamhet i molnet.

Få hjälp av partners med färdiga eller anpassade Azure-lösningar, samt av partners som kan hjälpa dig att distribuera och hantera dessa lösningar:

- **[Hitta en partner för molnlösningar](https://www.microsoft.com/solution-providers/home).** En certifierad leverantör av molnlösningar kan hjälpa dig att dra full nytta av molnet genom att utvärdera affärsmålen för molnimplementering, identifiera rätt molnlösning för dina affärsbehov och hjälpa företaget att bli mer flexibelt och effektivt.
- **[Hitta en partner för hanterade tjänster](https://www.microsoft.com/solution-providers/search?cacheId=16a3b49b-fef2-449d-bdf0-628008114cca).** En Azure-partner för hanterade tjänster hjälper dig att överföra företaget till Azure genom att vägleda dig genom alla delar av processen. Partners för hanterade molntjänster hjälper kunderna från konsulttjänster till migrering och driftshantering och visar alla fördelar som en molnimplementering kan innebära. De agerar också som en enda kontaktpunkt för vanlig support, etablering och fakturering med en flexibel affärsmodell där du betalar per användning.

## <a name="next-steps"></a>Nästa steg

När du har valt en partner och en supportstrategi kan du uppdatera [kvarvarande uppgifter för lansering och iteration](./release-iteration-backlog.md) så att de visar planerade insatser och tilldelningar.

> [!div class="nextstepaction"]
> [Hantera ändringar med kvarvarande uppgifter för lansering och iteration](./release-iteration-backlog.md)
