---
title: Beslutsguide för kryptering
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Lär dig om kryptering som en central tjänst i Azure-migreringar.
author: rotycenh
ms.author: v-tyhopk
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.custom: governance
ms.openlocfilehash: ef608f27f75d5a47e3e23a568e576310b8962ea8
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/06/2019
ms.locfileid: "70817102"
---
# <a name="encryption-decision-guide"></a>Beslutsguide för kryptering

Kryptering av data skyddar dem mot obehörig åtkomst. En korrekt implementerad krypteringsprincip ger ytterligare säkerhetslager för dina molnbaserade arbetsbelastningar och skyddar mot angripare och andra obehöriga användare både i och utanför organisationen och nätverken.

Hoppa till: [Nyckelhantering](#key-management) | [Datakryptering](#data-encryption) | [Läs mer](#learn-more)

Strategin för molnkryptering fokuserar på krav för företagspolicy och efterlevnad. Det är önskvärt att kryptera resurser, och många Azure-tjänster såsom Azure Storage och Azure SQL Database har kryptering som standard. Kryptering medför dock kostnader som kan öka svarstiden och den övergripande resursanvändningen.

För krävande arbetsbelastningar kan det vara mycket viktigt att få rätt balans mellan kryptering och prestanda samt att bestämma hur data och trafik krypteras. Krypteringsmekanismer kan variera vad gäller kostnad och komplexitet, och både tekniska och policyrelaterade krav kan påverka dina beslut om hur kryptering tillämpas samt hur du lagrar och hanterar kritiska hemligheter och nycklar.

Efterlevnad med företagspolicy och tredje part är de största faktorerna vid planering av en krypteringsstrategi. Azure tillhandahåller flera standardmekanismer som kan uppfylla vanliga krav för kryptering av både vilande data och data som överförs. För princip- eller efterlevnadskrav som fordrar striktare kontroller, till exempel standardiserad hemlighets- och nyckelhantering, kryptering under användning eller dataspecifik kryptering, behöver du dock utveckla en mer sofistikerad krypteringsstrategi för att uppfylla dessa krav.

## <a name="key-management"></a>Nyckelhantering

Kryptering av data i molnet är beroende av säker lagring, hantering och driftsanvändning av krypteringsnycklar. Ett nyckelhanteringssystem är mycket viktigt för din organisations möjlighet att skapa, lagra och hantera kryptografiska nycklar samt viktiga lösenord, anslutningssträngar och annan konfidentiell IT-information.

Moderna nyckelhanteringssystem såsom Azure Key Vault stöder lagring och hantering av programvaruskyddade nycklar för utvecklings- och testningsanvändning samt HSM-skyddade nycklar (Hardware Security Module, maskinvarusäkerhetsmodul) för maximalt skydd av produktionsarbetsbelastningar eller känsliga data.

Vid planering av en molnmigrering kan följande tabell hjälpa dig att bestämma hur du ska lagra och hantera krypteringsnycklar, certifikat och hemligheter som är kritiska för skapandet av säkra och hanterbara molndistributioner:

| Fråga | Molnbaserat | Bring your own key | Hold your own key |
|---------------------------------------------------------------------------------------------------------------------------------------|--------------|--------|-------------|
| Saknar din organisation centraliserad nyckel- och hemlighetshantering?                                                                    | Ja          | Nej     | Nej          |
| Kommer du att behöva begränsa skapandet av nycklar och hemligheter till enheter till din lokala maskinvara när dessa nycklar används i molnet? | Nej           | Ja    | Nej          |
| Har organisationen regler eller principer som kan förhindra att nycklar lagras på annan plats?                | Nej           | Nej     | Ja         |

### <a name="cloud-native"></a>Molnbaserat

Med molnbaserad nyckelhantering skapas, hanteras och lagras alla nycklar och hemligheter i ett molnbaserat valv såsom Azure Key Vault. Den här metoden förenklar många IT-uppgifter som rör nyckelhantering, till exempel säkerhetskopiering, lagring och förnyelse av nycklar.

Användning av ett molnbaserat nyckelhanteringssystem inbegriper följande antaganden:

- Du litar på att molnlösningen för nyckelhantering skapar och hanterar samt är värd för organisationens hemligheter och nycklar.
- Du aktiverar alla lokala program och tjänster som förlitar sig på användning av krypteringstjänster eller hemligheter för åtkomst till systemet för nyckelhantering.

### <a name="bring-your-own-key"></a>Bring your own key

Med en BYOK-metod (Bring Your Own Key) skapar du nycklar på dedikerad HSM-maskinvara i din lokala miljö och överför sedan dessa nycklar på ett säkert sätt till ett molnbaserat hanteringssystem såsom Azure Key Vault för användning med dina molnhanterade resurser.

**Antaganden gällande Bring Your Own Key:** Skapande av nycklar lokalt och användning av nycklarna med ett molnbaserat system för nyckelhantering inbegriper följande antaganden:

- Du litar på att den underliggande infrastrukturen för säkerhet och åtkomstkontroll på molnplattformen är värd för och använder dina nycklar och hemligheter.
- Dina molnbaserade program eller tjänster kan komma åt och använda nycklar och hemligheter på ett robust och säkert sätt.
- Enligt regler eller organisationspolicy måste du se till att skapandet och hanteringen av organisationens hemligheter och nycklar sker lokalt.

### <a name="on-premises-hold-your-own-key"></a>Lokalt (Hold Your Own Key)

I vissa fall kan det finnas regelmässiga, principrelaterade eller tekniska anledningar till varför du inte kan lagra nycklar i ett molnbaserat system för nyckelhantering. I dessa fall måste du skapa nycklar med hjälp av lokal maskinvara, lagra och hantera dem med hjälp av ett lokalt nyckelhanteringssystem och upprätta en mekanism för att tillåta molnbaserade resurser att få åtkomst till dessa nycklar för krypteringsändamål. Observera att HYOK (Hold Your Own Key, håll din egen nyckel) kanske inte är kompatibelt med alla Azure-baserade tjänster.

**Antaganden gällande lokal nyckelhantering:** Användning av ett lokalt nyckelhanteringssystem inbegriper följande antaganden:

- Enligt regler eller organisationspolicy måste du se till att skapandet, hanteringen och värdhanteringen av organisationens hemligheter och nycklar sker lokalt.
- Alla molnbaserade program eller tjänster som förlitar sig på användning av krypteringstjänster eller hemligheter kan komma åt det lokala systemet för nyckelhantering.

## <a name="data-encryption"></a>Datakryptering

Kom ihåg att olika datatillstånd har olika krypteringsbehov när du planerar krypteringspolicyn:

| Datatillstånd | Data |
|-----|-----|
| Data under överföring | Intern nätverkstrafik, Internetanslutningar och anslutningar mellan datacenter eller virtuella nätverk |
| Vilande data    | Databaser, filer, virtuella enheter och PaaS-lagring |
| Data som används     | Data som läses in i RAM-minne eller i CPU-cache |

### <a name="data-in-transit"></a>Data under överföring

Data under överföring är data som flyttas mellan resurser i interna nätverk, mellan datacenter eller externa nätverk eller via Internet.

Kryptering av data som överförs sker vanligtvis genom att SSL/TLS-protokoll krävs för trafik. Trafik som överförs mellan dina molnhanterade resurser och externa nätverk eller det offentliga Internet bör alltid krypteras. PaaS-resurser framtvingar även SSL/TLS-kryptering av trafik som standard. Huruvida du framtvingar kryptering för trafik mellan IaaS-resurser som hanteras i dina virtuella nätverk är ett beslut som dina molnimplementeringsteam och arbetsbelastningsägare fattar, och det brukar allmänt rekommenderas.

**Antaganden gällande kryptering av data under överföring:** Implementering av rätt krypteringspolicy för data under överföring förutsätter följande:

- Alla offentligt tillgängliga slutpunkter i din molnmiljö kommer att kommunicera med det offentliga Internet via SSL/TLS-protokoll.
- Vid anslutning av molnnätverk till lokala eller andra externa nätverk över det offentliga Internet använder du krypterade VPN-protokoll.
- Vid anslutning av molnnätverk till lokala eller andra externa nätverk med hjälp av en dedikerad WAN-anslutning såsom ExpressRoute använder du ett VPN eller en annan krypteringsteknik lokalt tillsammans med ett motsvarande virtuellt VPN eller virtuell krypteringsteknik som distribuerats till ditt molnnätverk.
- Om du har känsliga data som inte ska inkluderas i trafikloggar eller andra diagnostikrapporter som är synliga för IT-personal krypterar du all trafik mellan resurserna i ditt virtuella nätverk.

### <a name="data-at-rest"></a>Vilande data

Vilande data representerar alla data som inte aktivt flyttas eller bearbetas, däribland filer, databaser, VM-enheter, PaaS-lagringskonton eller liknande tillgångar. Kryptering av lagrade data skyddar virtuella enheter eller filer mot obehörig åtkomst från antingen penetration via externa nätverk, otillåtna interna användare eller oavsiktliga lanseringar.

PaaS-lagring och databasresurser framtvingar generellt kryptering som standard. IaaS-resurser kan skyddas genom kryptering av data på nivån för virtuell disk eller kryptering av hela det lagringskonto som är värd för dina virtuella enheter. Alla dessa tillgångar kan utnyttja antingen Microsoft-hanterade eller kundhanterade nycklar som lagras i Azure Key Vault.

Kryptering för vilande data omfattar även mer avancerade tekniker för databaskryptering, till exempel kryptering på kolumnnivå och radnivå, vilket ger mycket större kontroll över exakt vilka data som skyddas.

Dina övergripande krav vad gäller policy och efterlevnad, känsligheten hos de data som lagras samt prestandakraven för dina arbetsbelastning bör avgöra vilka tillgångar som kräver kryptering.

**Antaganden gällande kryptering av vilande data.** Kryptering av vilande data förutsätter följande:

- Du lagrar data som inte är avsedda för offentlig konsumtion.
- Dina arbetsbelastningar kan acceptera den ytterligare kostnaden för diskkryptering.

### <a name="data-in-use"></a>Data som används

Kryptering för data som används innebär skydd av data i icke-beständig lagring, till exempel RAM eller CPU-cache. Användning av tekniker såsom fullständig minneskryptering och enklavtekniker som Intels Secure Guard Extensions (SGX). Detta omfattar även kryptografiska tekniker, till exempel homomorfisk kryptering som kan användas för att skapa säkra och betrodda körningsmiljöer.

**Antaganden gällande kryptering av data som används:** Kryptering av data som används förutsätter följande:

- Du måste konstant hålla dataägarskap separat från den underliggande molnplattformen, även på RAM- och CPU-nivå.

## <a name="learn-more"></a>Läs mer

Mer information om kryptering och nyckelhantering i Azure finns här:

- [Översikt över Azure-kryptering](/azure/security/security-azure-encryption-overview). En detaljerad beskrivning av hur Azure använder kryptering för att skydda både vilande data och data under överföring.
- [Azure Key Vault](/azure/key-vault/key-vault-overview). Key Vault är det primära nyckelhanteringssystemet för lagring och hantering av kryptografiska nycklar, hemligheter och certifikat i Azure.
- [Bästa praxis för datasäkerhet och kryptering i Azure](/azure/security/azure-security-data-encryption-best-practices). En diskussion om bästa praxis för datasäkerhet och kryptering i Azure.
- [Konfidentiell databehandling i Azure](https://azure.microsoft.com/solutions/confidential-compute/). Azure-initiativet för konfidentiell databehandling erbjuder verktyg och teknik för skapandet av betrodda körningsmiljöer eller andra krypteringsmekanismer för att skydda data som används.

## <a name="next-steps"></a>Nästa steg

Kryptering är bara en av huvudkomponenterna för infrastruktur som kräver arkitektoniska beslut under en process för att implementera moln. Gå till [översikten över beslutsguider](../index.md) om vill veta mer om alternativa mönster eller modeller som används vid utformningsbeslut för andra typer av infrastrukturer.

> [!div class="nextstepaction"]
> [Beslutsguider för arkitektur](../index.md)