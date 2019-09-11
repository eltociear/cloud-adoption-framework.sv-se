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
ms.openlocfilehash: 14bd697a3332466fb97043d3420d80b1dca50679
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/06/2019
ms.locfileid: "70818139"
---
# <a name="secure-monitoring-and-management-tools"></a>Säkra övervaknings- och hanteringsverktyg

När en migrering är klar ska migrerade tillgångar hanteras av kontrollerade IT-åtgärder. Den här artikeln är inte avsedd att föreslå en avvikelse från bästa praxis för drift. I stället bör följande betraktas som en MVP (Minimum Viable Product) för att skydda och hantera migrerade tillgångar antingen från IT-åtgärder eller oberoende när IT-åtgärderna tas online.

## <a name="monitoring"></a>Övervakning

*Övervakning* syftar till insamling och analys av data för att avgöra prestanda, hälsotillstånd och tillgänglighet för affärsarbetsbelastningen och de resurser som arbetsbelastningen är beroende av. Azure innehåller flera tjänster som utför en specifik roll eller aktivitet individuellt i övervakningsutrymmet. Tillsammans levererar dessa tjänster en heltäckande lösning för att samla in, analysera och agera utifrån telemetrin från dina arbetsbelastningsprogram och de Azure-resurser som stöder dem. Få insyn i hälsa och prestanda för appar, infrastruktur och data i Azure med verktyg för molnövervakning som Azure Monitor, Log Analytics och Application Insights. Använd dessa verktyg för molnövervakning för att vidta åtgärder och integrera med dina tjänsthanteringslösningar:

- **Kärnövervakning.** Kärnövervakning ger grundläggande nödvändig övervakning för alla Azure-resurser. Dessa tjänster kräver minimal konfiguration och samlar in kärntelemetri som premiumövervakningstjänsterna använder.
- **Djupgående övervakning av program och infrastruktur.** Azure-tjänster innehåller omfattande funktioner för att samla in och analysera övervakningsdata på en djupare nivå. Dessa tjänster bygger på kärnövervakning och drar nytta av vanliga funktioner i Azure. De tillhandahåller kraftfull analys med insamlade data, vilket ger dig unika insikter om dina program och om infrastrukturen.

Läs mer om [Azure Monitor](/azure/azure-monitor/overview) för övervakning av migrerade tillgångar.

## <a name="security-monitoring"></a>Säkerhetsövervakning

Förlita dig på Azure Security Center för enhetlig säkerhetsövervakning och avancerade skyddsmeddelanden i dina olika arbetsbelastningar i hybridmoln. Med Security Center får du full synlighet och kontroll över säkerheten för molnprogram i Azure. Identifiera snabbt hot och vidta åtgärder, och minska exponeringen genom att aktivera adaptivt hotskydd. Den inbyggda instrumentpanelen innehåller omedelbara insikter om säkerhetsaviseringar och sårbarheter som kräver uppmärksamhet. Azure Security Center kan bidra med många funktioner, däribland:

- **Centraliserad principövervakning.** Säkerställ att företagets eller reglerade säkerhetskrav följer standarden genom att hantera principer centralt i arbetsbelastningar i hybridmoln.
- **Kontinuerlig säkerhetsutvärdering.** Övervaka säkerheten i datorer, nätverk, lagring, datatjänster och program så att du kan identifiera potentiella säkerhetsproblem.
- **Åtgärdsinriktade rekommendationer.** Åtgärda säkerhetsrisker innan de kan utnyttjas av angripare. Inkludera prioriterade och åtgärdsinriktade säkerhetsrekommendationer.
- **Avancerat molnförsvar.** Minska hot med just-in-time-åtkomst till hanteringsportar och listor över säkra för att styra program som körs på dina virtuella datorer.
- **Rangordnade aviseringar och incidenter.** Fokusera på de mest kritiska hoten först med prioriterade säkerhetsaviseringar och incidenter.
- **Integrerade säkerhetslösningar.** Samla in, sök efter och analysera säkerhetsdata från flera olika källor såsom anslutna partnerlösningar.

Läs mer om [Azure Security Center](/azure/security-center) för att skydda migrerade tillgångar.

## <a name="protect-assets-and-data"></a>Skydda tillgångar och data

Azure Backup ger dig möjlighet att skydda virtuella datorer, filer och data. Azure Backup kan bidra med många funktioner, däribland:

- Säkerhetskopiera virtuella datorer.
- Säkerhetskopiera filer.
- Säkerhetskopiera SQL Server-databaser.
- Återställa skyddade tillgångar.

Läs mer om [Azure Backup](/azure/backup) för att skydda migrerade tillgångar.
