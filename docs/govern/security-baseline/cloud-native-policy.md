---
title: Cloud – ursprunglig säkerhets bas linje princip
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Cloud – ursprunglig säkerhets bas linje princip
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 9c9676684ebec0a34fcc2dc845935c598814ea52
ms.sourcegitcommit: 7ffb0427bba71177f92618b2f980e864b72742f4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/29/2019
ms.locfileid: "73047867"
---
# <a name="cloud-native-security-baseline-policy"></a>Cloud – ursprunglig säkerhets bas linje princip

[Säkerhets bas linjen](./index.md) är en av de [fem disciplinerna i moln styrning](../governance-disciplines.md). Den här disciplinen fokuserar på allmänna säkerhets ämnen, inklusive skydd av nätverk, digitala till gångar, data osv. Som beskrivs i [princip gransknings guiden](../policy-compliance/cloud-policy-review.md)innehåller moln implementerings ramverket tre nivåer av **exempel princip**: Cloud-Native, Enterprise och Cloud-design-policy-kompatibel för var och en av de olika ämnes nivåerna. Den här artikeln beskriver den molnbaserade exempel principen för säkerhets bas linje disciplin.

> [!NOTE]
> Microsoft har ingen möjlighet att diktera företags-eller IT-policy. Den här artikeln hjälper dig att förbereda för en intern princip granskning. Det förutsätts att den här exempel principen kommer att utökas, val IDE ras och testas mot företagets policy innan du försöker använda den. All användning av den här exempel principen rekommenderas inte.

## <a name="policy-alignment"></a>Princip justering

I den här exempel principen används ett moln baserat scenario, vilket innebär att de verktyg och plattformar som tillhandahålls av Azure är tillräckliga för att hantera affärs risker som ingår i en distribution. I det här scenariot förutsätts att en enkel konfiguration av Azure-standardtjänsterna ger tillräckligt med till gångs skydd.

## <a name="cloud-security-and-compliance"></a>Säkerhet och efterlevnad i molnet

Säkerheten är integrerad i alla aspekter av Azure, som erbjuder unika säkerhets fördelar som härleds från Global säkerhets information, avancerade kund riktade kontroller och en säker, härdad infrastruktur. Denna kraftfulla kombination hjälper dig att skydda dina program och data, stöder ditt arbete för efterlevnad och tillhandahåller kostnadseffektiv säkerhet för organisationer i alla storlekar. Med den här metoden skapas en stark start position för en säkerhets princip, men det går inte att negera behovet av en lika stark säkerhets praxis som rör de säkerhets tjänster som används.

### <a name="built-in-security-controls"></a>Inbyggda säkerhetskontroller

Det är svårt att upprätthålla en stark säkerhets infrastruktur när säkerhets kontrollerna inte är intuitiva och behöver konfigureras separat. Azure innehåller inbyggda säkerhets kontroller för olika tjänster som hjälper dig att skydda data och arbets belastningar snabbt och hantera risker i hybrid miljöer. Integrerade partner lösningar gör det också möjligt för dig att enkelt överföra befintliga skydd till molnet.

### <a name="cloud-native-identity-policies"></a>Cloud-interna identitets principer

Identiteten blir det nya kant linje kontroll planet för säkerhet, med den rollen från det traditionella nätverket. Nätverks-perimeterna har blivit allt vanligare och det kan inte vara så effektivt som det var innan ankomsten från BYOD (ta med din egen enhet) och moln program. Azure Identity Management och Access Control möjliggör sömlös och säker åtkomst till alla dina program.

Ett exempel på en molnbaserad princip för identitet i molnet och lokala kataloger kan innehålla krav som följande:

- Auktoriserad åtkomst till resurser med rollbaserad åtkomst kontroll (RBAC), Multi-Factor Authentication och enkel inloggning (SSO).
- Snabb minskning av användar identiteter som misstänks vara komprometterade.
- Just-in-Time (JIT), bara för att få åtkomst per uppgift för att begränsa exponering av privilegierade autentiseringsuppgifter för administratörer.
- Utökad användar identitet och åtkomst till principer i flera miljöer via Azure Active Directory.

Även om det är viktigt att förstå [identitets bas](../identity-baseline/index.md) linjen i samband med säkerhets bas linjen, utvärderar de [fem disciplinerna för moln styrning](../index.md) ut [identitets bas linjen](../identity-baseline/index.md) som en egen disciplin, separat från säkerhets bas linjen.

### <a name="network-access-policies"></a>Nätverks åtkomst principer

Nätverks kontrollen omfattar konfiguration, hantering och skydd av nätverks element, till exempel virtuella nätverk, belastnings utjämning, DNS och gatewayer. Kontrollerna ger ett sätt för tjänster att kommunicera och samverka. Azure innehåller en robust och säker nätverks infrastruktur som stöder dina anslutnings krav för program och tjänster. Nätverks anslutningen är möjlig mellan resurser som finns i Azure, mellan lokala och Azure-värdbaserade resurser och till och från Internet och Azure.

En molnbaserad princip för nätverks kontroller kan innehålla krav som följande:

- Hybrid anslutningar till lokala resurser är kanske inte tillåtna i en moln intern princip. Om en hybrid anslutning visar sig nödvändig är ett mer stabilt exempel på säkerhets princip för företag en mer relevant referens.
- Användare kan upprätta säkra anslutningar till och inom Azure med hjälp av virtuella nätverk och nätverks säkerhets grupper.
- Inbyggd Windows Azure-brandvägg skyddar värdar från skadlig nätverks trafik via begränsad port åtkomst. Ett användbart exempel på den här principen är ett krav för att blockera (eller inte aktivera) trafik direkt till en virtuell dator via SSH/RDP.
- Tjänster som Azure Application Gateway Web Application Firewall (WAF) och Azure DDoS Protection skydda program och se till att det finns tillgänglighet för virtuella datorer som körs i Azure. Dessa funktioner bör inte inaktive ras.

### <a name="data-protection"></a>Dataskydd

En av nycklarna till data skydd i molnet är redovisning av de möjliga tillstånd som dina data kan inträffa i och vilka kontroller som är tillgängliga för varje tillstånd. I syfte att använda rekommendationer för Azure data säkerhet och kryptering, fokuserar vi på följande data tillstånd:

- Data krypterings kontroller är inbyggda i tjänster från virtuella datorer till lagring och SQL Database.
- När data flyttas mellan moln och kunder kan de skyddas med krypterings protokoll som är bransch standard.
- Azure Key Vault gör det möjligt för användare att skydda och kontrol lera kryptografiska nycklar, lösen ord, anslutnings strängar och certifikat som används av molnappar och-tjänster.
- Azure Information Protection hjälper till att klassificera, märka och skydda känsliga data i appar.

Även om dessa funktioner är inbyggda i Azure, kräver var och en av ovanstående konfiguration och kan öka kostnaderna. Justering av varje moln intern funktion med en [data klassificerings strategi](../policy-compliance/data-classification.md) är starkt föreslagen.

### <a name="security-monitoring"></a>Säkerhetsövervakning

Säkerhets övervakning är en proaktiv strategi som granskar dina resurser för att identifiera system som inte uppfyller organisationens standarder eller bästa praxis. Azure Security Center tillhandahåller enhetlig säkerhets bas linje och Avancerat skydd för arbets belastningar i hybrid moln. Med Security Center kan du tillämpa säkerhets principer i arbets belastningarna, begränsa exponeringen för hot och identifiera och reagera på attacker, inklusive:

- Enhetlig vy över säkerheten i alla lokala och molnbaserade arbets belastningar med Azure Security Center.
- Kontinuerlig övervakning och säkerhets utvärdering för att säkerställa efterlevnad och åtgärda eventuella sårbarheter.
- Interaktiva verktyg och sammanhangsbaserad Hot information för strömlinjeformad undersökning.
- Omfattande loggning och integrering med befintlig säkerhets information.
- Minskar behovet av kostsamma, ej integrerade, en säkerhets lösning.

### <a name="extending-cloud-native-policies"></a>Utöka molnets egna principer

Att använda molnet kan minska en del av säkerhets belastningen. Microsoft tillhandahåller fysisk säkerhet för Azure-datacenter och skyddar moln plattformen mot infrastruktur hot som en DDoS-attack. Med tanke på att Microsoft har tusentals cybersäkerhet-specialister som arbetar med säkerhet varje dag, är resurserna för att upptäcka, förhindra eller minimera cyberattacker stora. I själva verket var organisationerna i själva verket på väg om huruvida molnet var säkert, men det är nu viktigt att den nivå av investeringar i människor och specialiserad infrastruktur som görs av leverantörer, som Microsoft gör molnet säkrare än de flesta lokalt Data Center.

Även om den här investeringen i en Cloud-inbyggd säkerhets bas linje, rekommenderar vi att en säkerhets bas linje princip utökar standard principerna för molnet. Följande är exempel på utökade principer som bör övervägas, även i en moln intern miljö:

- **Säkra virtuella datorer.** Säkerheten bör vara varje organisations högsta prioritet och det krävs flera saker för att göra det effektivt. Du måste bedöma säkerhets status, skydda mot säkerhetshot och sedan identifiera och svara snabbt på hot som inträffar.
- **Skydda innehållet i den virtuella datorn.** Det är viktigt att konfigurera vanliga automatiserade säkerhets kopieringar för att skydda mot användar fel. Detta är inte tillräckligt för, men. Du måste också se till att säkerhets kopiorna är säkra från cyberattacker och är tillgängliga när du behöver dem.
- **Övervaka program.** Det här mönstret omfattar flera aktiviteter, inklusive inblick i hälso tillståndet för dina virtuella datorer, förståelse för samverkan mellan dem och hur du kan övervaka de program som de virtuella datorerna körs på. Alla dessa aktiviteter är viktiga för att hålla dina program igång dygnet runt.
- **Skydda och granska data åtkomst.** Organisationer bör granska all data åtkomst och utnyttja avancerade funktioner för maskin inlärning för att anropa avvikelser från vanliga åtkomst mönster.
- **Praxis för redundans.** Moln åtgärder som har låg tolerans för fel måste kunna redundansväxla eller återställa från en cybersäkerhet eller plattforms incident. Dessa procedurer får inte bara dokumenteras, utan bör användas i kvartal.

## <a name="next-steps"></a>Nästa steg

Nu när du har granskat policyn för exempel säkerhets bas linjen för molnbaserade lösningar går du tillbaka till [princip gransknings guiden](../policy-compliance/cloud-policy-review.md) för att börja bygga på det här exemplet för att skapa egna principer för moln införande.

> [!div class="nextstepaction"]
> [Bygg egna principer med princip gransknings guiden](../policy-compliance/cloud-policy-review.md)
