---
title: Planerings lista för migrerings miljö
description: Verifiera miljöberedskapen inför migrering
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: acf6c3b8dacd94c51a6fa9a857efad48eda727a0
ms.sourcegitcommit: 72a280cd7aebc743a7d3634c051f7ae46e4fc9ae
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/02/2020
ms.locfileid: "78222254"
---
# <a name="migration-environment-planning-checklist-validate-environmental-readiness-prior-to-migration"></a>Planerings check lista för migrerings miljö: validera miljö beredskap innan migrering

Som ett första steg i migreringsprocessen måste du skapa rätt miljö i molnet för att ta emot, vara värd för och stödja migrering av tillgångarna. Den här artikeln innehåller en lista över saker att kontrollera i den aktuella miljön innan migrering.

Följande checklista överensstämmer med riktlinjerna i [avsnittet Redo](../../../ready/index.md) i Ramverk för molnimplementering. I detta avsnitt kan du få hjälp med att utföra följande uppgifter.

## <a name="effort-type-assumption"></a>Antagande om projekttyp

Den här artikeln och checklistan förutsätter en migreringsmetod med _värdbyte_ eller _molnövergång_.

## <a name="governance-alignment"></a>Styrningsjustering

Det första och viktigaste beslutet om en migreringsklar miljö är valet av styrningsjustering. Har enighet nåtts avseende justering av styrning med migreringsgrunden? Som minst bör moln implementerings gruppen förstå om migreringen hamnar i en enda miljö med begränsad styrning, en helt styrd miljö fabrik eller någon variant i mellan. För ytterligare vägledning om styrnings justering, se [metoden regler](../../../govern/index.md).

## <a name="operations-management-alignment"></a>Justering av Operations Management

Innan du migrerar till gångar till molnet är det viktigt att förstå eventuella krav eller begränsningar avseende drift hantering. Som minst bör migreringen omfatta alla implementeringar som krävs för att uppfylla drifts bas linjen. Mer information om åtgärds justering finns i avsnittet [Hantera metod](../../../manage/index.md).

## <a name="cloud-readiness-implementation"></a>Implementering av molnberedskap

Oavsett om du väljer att använda en mer omfattande molnstyrningsstrategi för din första migrering måste du se till att molndistributionsmiljön har konfigurerats för att stödja dina arbetsbelastningar.

Om du planerar att anpassa migreringen till en molnstyrningsstrategi från början måste du tillämpa de [fem disciplinerna för molnstyrningn](../../../govern/governance-disciplines.md) för att fatta rätt beslut om principer, verktygskedjor och verkställande mekanismer som anpassar din molnmiljö med företagets övergripande krav. Mer information om hur du implementerar den här modellen med hjälp av Azure-tjänster finns i [design guiderna för styrning](../../../govern/guides/index.md) i Ramverk för molnimplementering.

Om din ursprungliga migrering inte är noggrant anpassad till en bredare strategi för molnstyrning måste den allmänna organisations-, åtkomst- och infrastruktur planeringen fortfarande hanteras. I [installations guiden för Azure](../../../ready/azure-setup-guide/index.md) hittar du hjälp med dessa beslut om moln beredskap.

> [!CAUTION]
> Vi rekommenderar starkt att du utvecklar en styrningsstrategi för allt som går bortom din ursprungliga migrering av arbetsbelastningen.

Oavsett vilken styrningsnivå du behöver måste du fatta beslut om följande.

### <a name="resource-organization"></a>Resursorganisering

Baserat på beslutet om styrningsjustering bör en metod för organisation och distribution av resurser upprättas inför migreringen.

### <a name="nomenclature"></a>Namngivning

En konsekvent metod för att namnge resurser, tillsammans med konsekventa namngivningsscheman, bör fastställas innan migreringen.

### <a name="resource-governance"></a>Resursstyrning

Ett beslut om verktyg för att styra resurser bör fattas innan migreringen. Verktygen behöver inte implementeras fullständigt, men en riktning bör väljas och testas. Moln styrnings teamet bör definiera och kräva implementering av en minimal livskraftig produkt (MVP) för styrnings verktyg innan migrering.

## <a name="network"></a>Nätverk

Dina molnbaserade arbetsbelastningar kommer att behöva virtuella nätverk som stöder åtkomst för slutanvändare och administratörer. Baserat på beslut om resursorganisation och resursstyrning bör du välja en nätverksmetod som anpassar det till kraven på IT-säkerhet. Dessutom bör dina nätverksbeslut justeras med eventuella hybridnätverks krav som krävs för att hantera arbetsbelastningarna i förteckningen av kvarvarande migreringsuppgifter och ge åtkomst till lokala resurser.

## <a name="identity"></a>Identitet

Molnbaserade identitetstjänster är ett krav för att erbjuda identitets- och åtkomsthantering (IAM) för dina molnresurser. Anpassa din strategi för identitetshantering till dina molnimplementeringsplaner innan du fortsätter. Till exempel, när du migrerar befintliga lokala tillgångar, bör du överväga att stödja en hybrid identitetsmetod med hjälp av [katalogsynkronisering](../../../decision-guides/identity/index.md) för att tillåta en konsekvent uppsättning användarautentiseringsuppgifter i dina miljöer lokalt och i molnet under och efter migreringen.

## <a name="next-steps"></a>Nästa steg

Om miljön uppfyller minimikraven kan den betraktas som godkänd inför migreringen. [Kulturell komplexitet och förändringsledning](./cultural-complexity.md) bidrar till att anpassa roller och ansvarsområden så att rätt förväntningar råder under genomförandet av planen.

> [!div class="nextstepaction"]
> [Kulturell komplexitet och förändringsledning](./cultural-complexity.md)
