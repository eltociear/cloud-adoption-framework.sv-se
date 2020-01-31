---
title: Skapa hybridmolnskonsekvens
description: Definiera metoden för att skapa en enhetlig hybrid moln lösning.
author: BrianBlanchard
ms.author: brblanch
ms.date: 12/27/2018
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 95dfcf1dea3a6b1734f770609ced4c9b2c0b069b
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 01/28/2020
ms.locfileid: "76799105"
---
# <a name="create-hybrid-cloud-consistency"></a>Skapa hybridmolnskonsekvens

Den här artikeln vägleder dig genom de övergripande metoderna för att skapa hybrid molnets konsekvens.

Hybrid distributions modeller under migreringen kan minska risken och bidra till en smidig infrastruktur över gång. Moln plattformarna ger störst flexibilitet när det gäller affärs processer. Många organisationer är tveka för att göra flytten till molnet. De föredrar i stället att ha fullständig kontroll över sina mest känsliga data. Lokala servrar tillåter tyvärr inte samma takt för innovation som i molnet. En hybrid moln lösning ger snabb utveckling och kontroll över lokal hantering.

## <a name="integrate-hybrid-cloud-consistency"></a>Integrera hybrid molnets konsekvens

Med en hybrid moln lösning kan organisationer skala data behandlings resurser. Det eliminerar också behovet av att göra enorma kapital utgifter för att hantera kortsiktiga toppar i efter frågan. Om du ändrar ditt företag kan du behöva frigöra lokala resurser för mer känsliga data eller program. Det är enklare, snabbare och billigare att avetablera moln resurser. Du betalar bara för de resurser som din organisation tillfälligt använder, i stället för att behöva köpa och underhålla ytterligare resurser. Den här metoden minskar mängden utrustning som kan vara inaktiv under långa tids perioder. Med hybrid molnbaserad data behandling får du alla fördelar med moln data behandling, skalbarhet och kostnads effektivitet med lägsta möjliga risk för data exponering.

![att skapa enhetlig hybrid moln över identitet, hantering, säkerhet, data, utveckling och DevOps](../../_images/hybrid-consistency.png)
*bild 1 – skapa hybrid molnets konsekvens för identitet, hantering, säkerhet, data, utveckling och DevOps.*

En verklig hybrid moln lösning måste tillhandahålla fyra komponenter, som var och en ger avsevärda fördelar:

- **Gemensam identitet för lokala program och moln program:** Den här komponenten förbättrar användar produktiviteten genom att ge användarna enkel inloggning (SSO) till alla sina program. Det garanterar också konsekvens när program och användare passerar nätverks-eller moln gränser.
- **Integrerad hantering och säkerhet i hela hybrid molnet:** Den här komponenten ger dig ett sammanhållet sätt för att övervaka, hantera och skydda miljön, vilket möjliggör ökad synlighet och kontroll.
- **En konsekvent data plattform för data Center och molnet:** Den här komponenten skapar data portabilitet, kombinerat med sömlös åtkomst till lokala och molnbaserade data tjänster för djupgående inblick i alla data källor.
- **Enhetlig utvecklings-och DevOps över molnet och lokala data Center:** Med den här komponenten kan du flytta program mellan de två miljöerna efter behov. Produktiviteten i utvecklare förbättras eftersom båda platserna nu har samma utvecklings miljö.

Här följer några exempel på dessa komponenter från ett Azure-perspektiv:

- Azure Active Directory (Azure AD) fungerar med lokala Active Directory för att tillhandahålla gemensam identitet för alla användare. Enkel inloggning lokalt och via molnet gör det enkelt för användare att säkert komma åt de program och till gångar som de behöver. Administratörer kan hantera säkerhets-och styrnings kontroller och har också flexibiliteten att justera behörigheter utan att påverka användar upplevelsen.
- Azure tillhandahåller integrerade hanterings-och säkerhets tjänster för både moln-och lokal infrastruktur. Dessa tjänster innehåller en integrerad uppsättning verktyg som används för att övervaka, konfigurera och skydda hybrid moln. Den här heltäckande metoden för hantering är specifikt riktad mot verkliga utmaningar som ansiktes organisationer överväger en hybrid moln lösning.
- Azure Hybrid Cloud tillhandahåller vanliga verktyg som garanterar säker åtkomst till alla data, sömlöst och effektivt. Azure Data Services kombinerar med Microsoft SQL Server för att skapa en konsekvent data plattform. En konsekvent hybrid moln modell gör att användarna kan arbeta med både drifts-och analys data. Samma tjänster tillhandahålls lokalt och i molnet för data lager hantering, data analys och data visualisering.
- Azure Cloud Services, kombinerat med Azure Stack lokalt, tillhandahåller enhetlig utvecklings-och DevOps. Konsekvens i molnet och lokalt innebär att ditt DevOps-team kan skapa program som körs i en miljö och enkelt kan distribueras till rätt plats. Du kan också återanvända mallar i hybrid lösningen som kan förenkla DevOps-processer.

## <a name="azure-stack-in-a-hybrid-cloud-environment"></a>Azure Stack i en hybrid moln miljö

Azure Stack är en hybrid moln lösning som gör det möjligt för organisationer att köra Azure-konsekventa tjänster i sitt Data Center. Det ger en förenklad utvecklings-, hanterings-och säkerhets miljö som är konsekvent med Azures offentliga moln tjänster. Azure Stack är ett tillägg till Azure. Du kan använda den för att köra Azure-tjänster från dina lokala miljöer och sedan flytta till Azure-molnet om och när det behövs.

Med Azure Stack kan du distribuera och använda både IaaS och PaaS med samma verktyg och erbjuda samma upplevelse som det offentliga Azure-molnet. Hantering av Azure Stack, vare sig via webb GRÄNSSNITTs portalen eller via PowerShell, har ett enhetligt utseende och känsla för IT-administratörer och slutanvändare med Azure.

Azure och Azure Stack öppna nya hybrid användnings fall för både kund-och interna affärs program:

- **Kant-och frånkopplade lösningar.** För att lösa svars tid och anslutnings krav kan kunderna bearbeta data lokalt i Azure Stack och sedan samla in dem i Azure för ytterligare analys. De kan använda vanliga program logik i båda. Många kunder är intresserade av det här gräns scenariot för olika kontexter, till exempel fabriks golv, kryssnings-fartyg och mina axlar.
- **Moln program som uppfyller olika regler.** Kunder kan utveckla och distribuera program i Azure, med fullständig flexibilitet för att distribuera lokalt på Azure Stack för att uppfylla reglernas eller princip kraven. Inga kod ändringar behövs. Exempel på program är global granskning, ekonomisk rapportering, extern Exchange-handel, onlinespel och utgifts rapportering. Kunder kan ibland titta på att distribuera olika instanser av samma program till Azure eller Azure Stack, baserat på affärs-och tekniska krav. Azure uppfyller de flesta krav, Azure Stack kompletterar distributions metoden vid behov.
- **Moln programs modell lokalt.** Kunder kan använda Azure-webbtjänster, behållare, Server lös och mikrotjänst-arkitekturer för att uppdatera och utöka befintliga program eller bygga nya. Du kan använda konsekventa DevOps processer i Azure i molnet och Azure Stack lokalt. Det finns ett växande intresse i Application modernisering, även för viktiga verksamhets kritiska program.

Azure Stack erbjuds via två distributions alternativ:

- **Azure Stack integrerade system:** Azure Stack integrerade system erbjuds via Microsoft-och maskin varu partner för att skapa en lösning som ger en nyskapande utveckling i molnet med enkel hantering. Eftersom Azure Stack erbjuds som ett integrerat system med maskin vara och program vara får du flexibilitet och kontroll samtidigt som du börjar använda innovation från molnet. Azure Stack integrerade system intervall i storlek från 4 till 12 noder. De stöds gemensamt av maskin varu partnern och Microsoft. Använd Azure Stack integrerade system för att möjliggöra nya scenarier för dina produktions arbets belastningar.
- **Azure Stack Development Kit:** Microsoft Azure Stack Development Kit är en distribution av Azure Stack med en nod. Du kan använda den för att utvärdera och lära dig mer om Azure Stack. Du kan också använda paketet som en utvecklings miljö där du kan utveckla med hjälp av API: er och verktyg som är konsekventa med Azure. Azure Stack Development Kit är inte avsedd att användas som produktions miljö.

## <a name="azure-stack-one-cloud-ecosystem"></a>Azure Stack ett eko system med ett moln

Du kan påskynda Azure Stack initiativ genom att använda det fullständiga Azure-eko systemet:

- Azure säkerställer att de flesta program och tjänster som är certifierade för Azure fungerar på Azure Stack. Flera ISV: er utökar lösningar till Azure Stack. Dessa ISV: er omfattar Bitnami, Docker, Kemp: Technologies, pivotal Cloud Foundry, Red Hat Enterprise Linux och SUSE Linux.
- Du kan välja att låta Azure Stack levereras och hanteras som en fullständigt hanterad tjänst. Flera partners kommer att ha hanterade tjänst erbjudanden i Azure och Azure Stack strax. Dessa partner omfattar Tieto, Yourhosting, Revera, fram och NTT. Dessa partners levererar hanterade tjänster för Azure via Cloud Solution Provider (CSP)-programmet. De utökar sina erbjudanden för att inkludera hybrid lösningar.
- Som ett exempel på en komplett, fullständigt hanterad hybrid moln lösning ger Avanade ett allt-i-ett-erbjudande. Den omfattar moln omvandlings tjänster, program vara, infrastruktur, installation och konfiguration och pågående hanterade tjänster. På så sätt kan kunderna använda Azure Stack precis som med Azure idag.
- Leverantörer kan hjälpa till att påskynda Application modernisering-initiativ genom att bygga heltäckande Azure-lösningar för kunder. De får djupgående Azures kunskaps uppsättningar, domän-och bransch kunskap och process kunskaper, till exempel DevOps. Varje Azure Stack moln är en möjlighet för en leverantör att utforma lösningen och leda och påverka system distributionen. De kan också anpassa de funktioner som ingår och leverera drifts aktiviteter. Exempel på leverantörer är Avanade, DXC, Dell EMC-tjänster, inlednings grupp, HPE Pointnext och PwC (tidigare PricewaterhouseCoopers).
