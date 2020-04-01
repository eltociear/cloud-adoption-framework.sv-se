---
title: Exempel princip satser för säkerhets bas linje
description: Se dessa policys för exempel på säkerhets bas linjer för att hjälpa till att hantera organisationens behov.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 47aeccac0f98d21d2740a27ded12696372efaaa0
ms.sourcegitcommit: da7ebd67a0ebf29361f093f00e10217b212a2eb2
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/01/2020
ms.locfileid: "80527513"
---
# <a name="security-baseline-sample-policy-statements"></a>Exempel princip satser för säkerhets bas linje

Enskilda moln princips instruktioner är rikt linjer för att åtgärda specifika risker som identifieras under riskbedömningen. Dessa instruktioner bör ge en kortfattad sammanfattning av riskerna och planer för att hantera dem. Varje uttrycks definition ska innehålla dessa delar av informationen:

- **Teknisk risk:** En sammanfattning av risken som den här principen kommer att åtgärda.
- **Princip instruktion:** En tydlig Sammanfattning av princip kraven.
- **Tekniska alternativ:** Rekommendationer, specifikationer eller andra rikt linjer som IT-team och utvecklare kan använda när de implementerar principen.

Följande exempel på princip satser riktar sig mot vanliga säkerhets-relaterade affärs risker. Dessa instruktioner är exempel som du kan referera till när du använder policy-instruktioner för att uppfylla organisationens behov. Dessa exempel är inte avsedda att vara proskriptiga och det finns potentiellt flera princip alternativ för att hantera varje identifierad risk. Arbeta tätt med affärs-, säkerhets-och IT-team för att identifiera de bästa principerna för din unika uppsättning risker.

## <a name="asset-classification"></a>Till gångs klassificering

**Teknisk risk:** Till gångar som inte identifieras korrekt som verksamhets kritiska eller som rör känsliga data kanske inte får tillräckligt med skydd, vilket leder till potentiella data läckor eller verksamhets avbrott.

**Princip instruktion:** Alla distribuerade till gångar måste kategoriseras efter allvarlighets grad och data klassificering. Klassificeringarna måste granskas av moln styrnings teamet och program ägaren innan distributionen till molnet.

**Alternativ för potentiell design:** Upprätta [resurs märknings standarder](../../decision-guides/resource-tagging/index.md) och se till att IT-personalen använder dem konsekvent på alla distribuerade resurser med hjälp av [Azure Resource Taggar](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags).

## <a name="data-encryption"></a>Datakryptering

**Teknisk risk:** Det finns en risk för att skyddade data exponeras under lagring.

**Princip instruktion:** Alla skyddade data måste krypteras när de är i vilo läge.

**Alternativ för potentiell design:** I artikeln [Översikt över Azure-kryptering](https://docs.microsoft.com/azure/security/security-azure-encryption-overview) finns en beskrivning av hur data i rest-kryptering utförs på Azure-plattformen. Ytterligare kontroller, till exempel vid kryptering av konto data och kontroll över hur lagrings konto inställningar kan ändras bör också beaktas.

## <a name="network-isolation"></a>Nätverksisolering

**Teknisk risk:** Anslutning mellan nätverk och undernät i nätverk medför potentiella sårbarheter som kan leda till data läckor eller avbrott i verksamhets kritiska tjänster.

**Princip instruktion:** Nätverks under nät som innehåller skyddade data måste isoleras från andra undernät. Nätverks trafik mellan skyddade data undernät ska granskas regelbundet.

**Alternativ för potentiell design:** I Azure hanteras nätverks-och under nät isolering via [virtuella Azure-nätverk](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview).

## <a name="secure-external-access"></a>Säker extern åtkomst

**Teknisk risk:** Att tillåta åtkomst till arbets belastningar från det offentliga Internet innebär en risk för intrång som resulterar i obehörig data exponering eller affärs avbrott.

**Princip instruktion:** Det går inte att komma åt ett undernät som innehåller skyddade data direkt via offentlig Internet eller mellan data Center. Åtkomst till dessa undernät måste dirigeras via mellanliggande undernät. All åtkomst till dessa undernät måste komma via en brand Väggs lösning som kan utföra paket genomsökning och blockera funktioner.

**Alternativ för potentiell design:** I Azure, säkra offentliga slut punkter genom att distribuera en [DMZ mellan det offentliga Internet och ditt molnbaserade nätverk](https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/secure-vnet-dmz?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json). Överväg distribution, konfiguration och automatisering av [Azure-brandväggen](https://docs.microsoft.com/azure/firewall).

## <a name="ddos-protection"></a>DDoS-skydd

**Teknisk risk:** DDoS-attacker (distributed denial of Service) kan leda till ett affärs avbrott.

**Princip instruktion:** Distribuera metoder för automatisk DDoS-minskning till alla offentligt tillgängliga nätverks slut punkter. Ingen offentlig webbplats som backas upp av IaaS bör exponeras för Internet utan DDoS.

**Alternativ för potentiell design:** Använd [Azure DDoS Protection](https://docs.microsoft.com/azure/virtual-network/ddos-protection-overview) standard för att minimera störningar som orsakas av DDoS-attacker.

## <a name="secure-on-premises-connectivity"></a>Säker lokal anslutning

**Teknisk risk:** Okrypterad trafik mellan ditt moln nätverk och lokalt via det offentliga Internet är sårbar för avlyssning, vilket introducerar risken för data exponering.

**Princip instruktion:** Alla anslutningar mellan lokala och molnbaserade nätverk måste antingen ske via en säker krypterad VPN-anslutning eller en särskild privat WAN-länk.

**Alternativ för potentiell design:** Använd ExpressRoute eller Azure VPN i Azure för att upprätta privata anslutningar mellan dina lokala och molnbaserade nätverk.

## <a name="network-monitoring-and-enforcement"></a>Nätverks övervakning och verk ställande

**Teknisk risk:** Ändringar i nätverks konfigurationen kan leda till nya sårbarheter och data exponerings risker.

**Princip instruktion:** Styrnings verktyg måste granska och genomdriva krav på nätverks konfiguration som definieras av säkerhets bas linje teamet.

**Alternativ för potentiell design:** I Azure kan nätverks aktivitet övervakas med hjälp av [azure Network Watcher](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview), och [Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-network-recommendations) kan hjälpa dig att identifiera säkerhets problem. Med Azure Policy kan du begränsa nätverks resurser och resurs konfigurations principer enligt gränser som definieras av säkerhets teamet.

## <a name="security-review"></a>Säkerhets granskning

**Teknisk risk:** Med tiden uppstår nya säkerhetshot och angrepps typer, vilket ökar risken för exponering eller avbrott i moln resurserna.

**Princip instruktion:** Trender och potentiella utnyttjanden som kan påverka moln distributioner bör regelbundet granskas av säkerhets teamet för att tillhandahålla uppdateringar av verktyget för säkerhets bas linjer som används i molnet.

**Alternativ för potentiell design:** Upprätta ett regelbundet säkerhets gransknings möte som innehåller relevanta IT-och styrelse grupp medlemmar. Granska befintliga säkerhets data och mått för att skapa luckor i den aktuella policyn och säkerhets bas linje verktyget, och uppdatera principen för att åtgärda eventuella nya risker. Använd [Azure Advisor](https://docs.microsoft.com/azure/advisor/advisor-overview) och [Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-intro) för att få användbara insikter om nya hot som är speciella för dina distributioner.

## <a name="next-steps"></a>Nästa steg

Använd de exempel som nämns i den här artikeln som utgångs punkt för att utveckla principer som åtgärdar vissa säkerhets risker som överensstämmer med dina moln implementerings planer.

Om du vill börja utveckla dina egna anpassade princip satser som är relaterade till säkerhets bas linjen hämtar du [säkerhets bas linje mal len](./template.md).

För att påskynda införandet av denna disciplin väljer du den [Åtgärds bara styrnings guide](../guides/index.md) som bäst passar din miljö. Ändra sedan designen så att du kan lägga till dina företags princip beslut.

Skapa på risker och toleranser och upprätta en process för styrning och kommunikation av principer för säkerhets bas linjen.

> [!div class="nextstepaction"]
> [Upprätta rutiner för regelefterlevnad](./compliance-processes.md)
