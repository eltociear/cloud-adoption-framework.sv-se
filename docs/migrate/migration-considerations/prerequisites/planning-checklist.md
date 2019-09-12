---
title: Migeringsmiljö – checklista för planering
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Verifiera miljöberedskapen inför migrering
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 8d216d65685c7e58fc622a5d7f820f0c23097fa4
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/06/2019
ms.locfileid: "70833302"
---
# <a name="migration-environment-planning-checklist---validate-environmental-readiness-prior-to-migration"></a>Planeringschecklista för migreringsmiljön – Verifiera att miljön är redo inför migreringen

Som ett första steg i migreringsprocessen måste du skapa rätt miljö i molnet för att ta emot, vara värd för och stödja migrering av tillgångarna. Den här artikeln innehåller en lista över saker att kontrollera i den aktuella miljön innan migrering.

Följande checklista överensstämmer med riktlinjerna i [avsnittet Redo](../../../ready/index.md) i Ramverk för molnimplementering. I detta avsnitt kan du få hjälp med att utföra följande uppgifter.

## <a name="effort-type-assumption"></a>Antagande om projekttyp

Den här artikeln och checklistan förutsätter en migreringsmetod med _värdbyte_ eller _molnövergång_.

## <a name="governance-alignment"></a>Styrningsjustering

Det första och viktigaste beslutet om en migreringsklar miljö är valet av styrningsjustering. Har enighet nåtts avseende justering av styrning med migreringsgrunden? Molnimplementeringsteamet bör åtminstone veta om migreringen landar i en enkel miljö med begränsad styrning, en helt styrd miljöfabrik eller något däremellan. Mer alternativ och vägledning om styrningsjustering finns i artikeln om [styrning- och anpassningsefterlevnad](../../expanded-scope/governance-or-compliance.md).

## <a name="cloud-readiness-implementation"></a>Implementering av molnberedskap

Oavsett om du väljer att använda en mer omfattande molnstyrningsstrategi för din första migrering måste du se till att molndistributionsmiljön har konfigurerats för att stödja dina arbetsbelastningar.

Om du planerar att anpassa migreringen till en molnstyrningsstrategi från början måste du tillämpa de [fem disciplinerna för molnstyrningn](../../../governance/governance-disciplines.md) för att fatta rätt beslut om principer, verktygskedjor och verkställande mekanismer som anpassar din molnmiljö med företagets övergripande krav. Mer information om hur du implementerar den här modellen med hjälp av Azure-tjänster finns i [design guiderna för styrning](../../../governance/journeys/index.md) i Ramverk för molnimplementering.

Om din ursprungliga migrering inte är noggrant anpassad till en bredare strategi för molnstyrning måste den allmänna organisations-, åtkomst- och infrastruktur planeringen fortfarande hanteras. Se [guiden för Azure-beredskap](../../../ready/azure-readiness-guide/index.md) för hjälp med dessa beslut om molnberedskap.

> [!CAUTION]
> Vi rekommenderar starkt att du utvecklar en styrningsstrategi för allt som går bortom din ursprungliga migrering av arbetsbelastningen.

Oavsett vilken styrningsnivå du behöver måste du fatta beslut om följande.

### <a name="resource-organization"></a>Resursorganisering

Baserat på beslutet om styrningsjustering bör en metod för organisation och distribution av resurser upprättas inför migreringen.

### <a name="nomenclature"></a>Namngivning

En konsekvent metod för att namnge resurser, tillsammans med konsekventa namngivningsscheman, bör fastställas innan migreringen.

### <a name="resource-governance"></a>Resursstyrning

Ett beslut om verktyg för att styra resurser bör fattas innan migreringen. Verktygen behöver inte implementeras fullständigt, men en riktning bör väljas och testas. Vi rekommenderar att molnstyrningsteamet definierar och kräver implementering av en minimal livskraftig produkt (MVP) för styrningsverktyg innan migreringen.

## <a name="network"></a>Nätverk

Dina molnbaserade arbetsbelastningar kommer att behöva virtuella nätverk som stöder åtkomst för slutanvändare och administratörer. Baserat på beslut om resursorganisation och resursstyrning bör du välja en nätverksmetod som anpassar det till kraven på IT-säkerhet. Dessutom bör dina nätverksbeslut justeras med eventuella hybridnätverks krav som krävs för att hantera arbetsbelastningarna i förteckningen av kvarvarande migreringsuppgifter och ge åtkomst till lokala resurser.

## <a name="identity"></a>Identitet

Molnbaserade identitetstjänster är ett krav för att erbjuda identitets- och åtkomsthantering (IAM) för dina molnresurser. Anpassa din strategi för identitetshantering till dina molnimplementeringsplaner innan du fortsätter. Till exempel, när du migrerar befintliga lokala tillgångar, bör du överväga att stödja en hybrid identitetsmetod med hjälp av [katalogsynkronisering](../../../decision-guides/identity/index.md) för att tillåta en konsekvent uppsättning användarautentiseringsuppgifter i dina miljöer lokalt och i molnet under och efter migreringen.

## <a name="next-steps"></a>Nästa steg

Om miljön uppfyller minimikraven kan den betraktas som godkänd inför migreringen. [Kulturell komplexitet och förändringsledning](./culture-complexity.md) bidrar till att anpassa roller och ansvarsområden så att rätt förväntningar råder under genomförandet av planen.

> [!div class="nextstepaction"]
> [Kulturell komplexitet och förändringsledning](./culture-complexity.md)
