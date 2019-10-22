---
title: Skydda och hantera
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Säkra övervaknings- och hanteringsverktyg
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 86a88183b7743a4fb326d325e97f90c4f4a5aa24
ms.sourcegitcommit: f3371811a36e12533ecbc3aa936e2a68e0cee25f
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/21/2019
ms.locfileid: "72683766"
---
# <a name="secure-monitoring-and-management-tools"></a>Säkra övervaknings- och hanteringsverktyg

När en migrering är klar ska migrerade tillgångar hanteras av kontrollerade IT-åtgärder. Den här artikeln är inte avsedd att föreslå en avvikelse från bästa praxis för drift. I stället bör följande betraktas som en MVP (Minimum Viable Product) för att skydda och hantera migrerade tillgångar antingen från IT-åtgärder eller oberoende när IT-åtgärderna tas online.

## <a name="monitoring"></a>Övervakning

*Övervakning* syftar till insamling och analys av data för att avgöra prestanda, hälsotillstånd och tillgänglighet för affärsarbetsbelastningen och de resurser som arbetsbelastningen är beroende av. Azure innehåller flera tjänster som utför en specifik roll eller aktivitet individuellt i övervakningsutrymmet. Tillsammans levererar dessa tjänster en heltäckande lösning för att samla in, analysera och agera utifrån telemetrin från dina arbetsbelastningsprogram och de Azure-resurser som stöder dem. Få insyn i hälsa och prestanda för appar, infrastruktur och data i Azure med verktyg för molnövervakning som Azure Monitor, Log Analytics och Application Insights. Använd dessa verktyg för molnövervakning för att vidta åtgärder och integrera med dina tjänsthanteringslösningar:

- **Kärnövervakning.** Kärnövervakning ger grundläggande nödvändig övervakning för alla Azure-resurser. Dessa tjänster kräver minimal konfiguration och samlar in kärntelemetri som premiumövervakningstjänsterna använder.
- **Djupgående övervakning av program och infrastruktur.** Azure-tjänster innehåller omfattande funktioner för att samla in och analysera övervakningsdata på en djupare nivå. Dessa tjänster bygger på kärnövervakning och drar nytta av vanliga funktioner i Azure. De tillhandahåller kraftfull analys med insamlade data, vilket ger dig unika insikter om dina program och om infrastrukturen.

Läs mer om [Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/overview) för övervakning av migrerade tillgångar.

## <a name="security-monitoring"></a>Säkerhetsövervakning

Förlita dig på Azure Security Center för enhetlig säkerhetsövervakning och avancerade skyddsmeddelanden i dina olika arbetsbelastningar i hybridmoln. Med Security Center får du full synlighet och kontroll över säkerheten för molnprogram i Azure. Identifiera snabbt hot och vidta åtgärder, och minska exponeringen genom att aktivera adaptivt hotskydd. Den inbyggda instrumentpanelen innehåller omedelbara insikter om säkerhetsaviseringar och sårbarheter som kräver uppmärksamhet. Azure Security Center kan bidra med många funktioner, däribland:

- **Centraliserad principövervakning.** Säkerställ att företagets eller reglerade säkerhetskrav följer standarden genom att hantera principer centralt i arbetsbelastningar i hybridmoln.
- **Kontinuerlig säkerhetsutvärdering.** Övervaka säkerheten i datorer, nätverk, lagring, datatjänster och program så att du kan identifiera potentiella säkerhetsproblem.
- **Åtgärdsinriktade rekommendationer.** Åtgärda säkerhetsrisker innan de kan utnyttjas av angripare. Inkludera prioriterade och åtgärdsinriktade säkerhetsrekommendationer.
- **Avancerat molnförsvar.** Minska hot med just-in-time-åtkomst till hanteringsportar och listor över säkra för att styra program som körs på dina virtuella datorer.
- **Rangordnade aviseringar och incidenter.** Fokusera på de mest kritiska hoten först med prioriterade säkerhetsaviseringar och incidenter.
- **Integrerade säkerhetslösningar.** Samla in, sök efter och analysera säkerhetsdata från flera olika källor såsom anslutna partnerlösningar.

Läs mer om [Azure Security Center](https://docs.microsoft.com/azure/security-center) för att skydda migrerade tillgångar.

## <a name="service-health-monitoring"></a>Service Health-övervakning

Med Azure Service Health får du anpassade aviseringar och hjälp när du påverkas av problem med Azure-tjänsterna. Tjänsten kan meddela dig om olika händelser, hjälpa dig att förstå hur olika problem påverkar dig och hålla dig uppdaterad tills problemen har lösts. Dessutom får du hjälp med förberedelser inför planerat underhåll och ändringar som kan påverka tillgängligheten för dina resurser.

- **Service Health-instrumentpanelen.** Kontrollera det övergripande hälsotillståndet för dina Azure-tjänster och Azure-regioner med detaljerade uppdateringar om eventuella problem med tjänsterna, planerat underhåll och tjänstövergångar.
- **Service Health-aviseringar.** Konfigurera aviseringar som meddelar dig och dina team om en tjänst får problem, t.ex. ett avbrott eller kommande planerat underhåll.
- **Service Health-historik.** Granska tidigare problem med tjänster och hämta officiella sammanfattningar och rapporter från Microsoft.

Läs mer om [Azure Service Health](https://docs.microsoft.com/azure/service-health) och hur du håller dig uppdaterad om hälsotillståndet för dina migrerade resurser.

## <a name="protect-assets-and-data"></a>Skydda tillgångar och data

Azure Backup ger dig möjlighet att skydda virtuella datorer, filer och data. Azure Backup kan bidra med många funktioner, däribland:

- Säkerhetskopiera virtuella datorer.
- Säkerhetskopiera filer.
- Säkerhetskopiera SQL Server-databaser.
- Återställa skyddade tillgångar.

Läs mer om [Azure Backup](https://docs.microsoft.com/azure/backup) för att skydda migrerade tillgångar.

## <a name="optimize-resources"></a>Optimera resurser

Azure Advisor är din anpassade guide för bästa praxis i Azure. Tjänsten analyserar konfigurationen och användningen av telemetri och ger rekommendationer som hjälper dig att optimera dina Azure-resurser för hög tillgänglighet, säkerhet, prestanda och kostnad. Med Advisors infogade åtgärder kan du snabbt och enkelt åtgärda dina rekommendationer och optimera dina distributioner.

- **Bästa praxis för Azure.** Optimera migrerade resurser för hög tillgänglighet, säkerhet, prestanda och kostnad.
- **Vägledning steg för steg.** Åtgärda rekommendationer effektivt med guidade snabblänkar.
- **Aviseringar om nya rekommendationer.** Håll dig informerad om nya rekommendationer, till exempel hur du kan optimera storleken för virtuella datorer och spara pengar.

Läs mer om [Azure Advisor](https://docs.microsoft.com/azure/advisor/advisor-overview) och hur du kan optimera dina migrerade resurser.
