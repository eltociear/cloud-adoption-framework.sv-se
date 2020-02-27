---
title: Exempel princip satser för identitets bas linje
description: Använd ramverket för moln införande för Azure för att hämta exempel på principer för bas linje princip för identiteter som kan hjälpa dig att skapa ett konto utdrag.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 4cf67b9580fb6b3970dc9982d9df94a809a73f36
ms.sourcegitcommit: af45c1c027d7246d1a6e4ec248406fb9a8752fb5
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 02/27/2020
ms.locfileid: "77709302"
---
# <a name="identity-baseline-sample-policy-statements"></a>Exempel princip satser för identitets bas linje

Enskilda moln princips instruktioner är rikt linjer för att åtgärda specifika risker som identifieras under riskbedömningen. Dessa instruktioner bör ge en kortfattad sammanfattning av riskerna och planer för att hantera dem. Varje uttrycks definition ska innehålla dessa delar av informationen:

- **Teknisk risk:** En sammanfattning av risken som den här principen kommer att åtgärda.
- **Princip instruktion:** En tydlig Sammanfattning av princip kraven.
- **Design alternativ:** Rekommendationer, specifikationer eller andra rikt linjer som IT-team och utvecklare kan använda när de implementerar principen.

Följande exempel på princip satser hanterar vanliga affärs risker för identiteter. Dessa instruktioner är exempel som du kan referera till när du använder policy-instruktioner för att uppfylla organisationens behov. Dessa exempel är inte avsedda att vara proskriptiga och det finns potentiellt flera princip alternativ för att hantera varje identifierad risk. Arbeta nära företags-och IT-team för att identifiera de bästa principerna för din unika uppsättning risker.

## <a name="lack-of-access-controls"></a>Brist på åtkomst kontroller

**Teknisk risk:** Inställningarna för otillräcklig eller ad hoc-åtkomstkontroll kan leda till risk för obehörig åtkomst till känsliga eller verksamhets kritiska resurser.

**Princip instruktion:** Alla till gångar som distribueras till molnet bör kontrol leras med hjälp av identiteter och roller som godkänts av aktuella styrnings principer.

**Potentiella design alternativ:** [Azure Active Directory villkorlig åtkomst](https://docs.microsoft.com/azure/active-directory/conditional-access/overview) är standard mekanismen för åtkomst kontroll i Azure.

## <a name="overprovisioned-access"></a>Överetablerat åtkomst

**Teknisk risk:** Användare och grupper med kontroll över resurser utöver deras ansvars områden kan leda till att obehöriga ändringar leder till avbrott eller säkerhets risker.

**Princip instruktion:** Följande principer kommer att implementeras:

- En åtkomst modell med minst behörighet kommer att tillämpas på alla resurser som ingår i verksamhets kritiska program eller skyddade data.
- Utökade behörigheter bör vara ett undantag och alla sådana undantag måste registreras med moln styrnings teamet. Undantag kommer att granskas regelbundet.

**Potentiella design alternativ:** Se [metod tips för Azure Identity Management](https://docs.microsoft.com/azure/security/azure-security-identity-management-best-practices) för att implementera en rollbaserad åtkomst kontroll (RBAC) som begränsar åtkomst baserat på [behovet av att känna till och ha](https://wikipedia.org/wiki/Need_to_know) [säkerhets](https://wikipedia.org/wiki/Principle_of_least_privilege) principer som krävs.

## <a name="lack-of-shared-management-accounts-between-on-premises-and-the-cloud"></a>Brist på delade hanterings konton mellan lokalt och molnet

**Teknisk risk:** IT-hantering eller administrativ personal med konton på din lokala Active Directory kanske inte har tillräcklig åtkomst till moln resurser, kanske inte kan effektivt lösa drift-eller säkerhets problem.

**Princip instruktion:** Alla grupper i den lokala Active Directory-infrastrukturen med utökade privilegier ska mappas till en godkänd RBAC-roll.

**Potentiella design alternativ:** Implementera en hybrid identitets lösning mellan din molnbaserade Azure Active Directory och din lokala Active Directory och Lägg till nödvändiga lokala grupper i de RBAC-roller som krävs för att utföra sitt arbete.

## <a name="weak-authentication-mechanisms"></a>Svaga autentiseringsmekanismer

**Teknisk risk:** Identitets hanterings system med otillräckligt säkra metoder för användarautentisering, till exempel kombinationer av grundläggande användar-och lösen ord, kan leda till komprometterade eller hackade lösen ord, vilket ger en större risk för obehörig åtkomst till säkra moln system.

**Princip instruktion:** Alla konton krävs för att logga in på skyddade resurser med en Multi-Factor Authentication-metod.

**Potentiella design alternativ:** För Azure Active Directory implementerar du [Azure Multi-Factor Authentication](https://docs.microsoft.com/azure/active-directory/authentication/concept-mfa-howitworks) som en del av din användar godkännande process.

## <a name="isolated-identity-providers"></a>Isolerade identitets leverantörer

**Teknisk risk:** Inkompatibla identitets leverantörer kan leda till att du inte kan dela resurser eller tjänster med kunder eller andra affärs partner.

**Princip instruktion:** Distribution av program som kräver kundautentisering måste använda en godkänd identitets leverantör som är kompatibel med den primära identitets leverantören för interna användare.

**Potentiella design alternativ:** Implementera [Federation med Azure Active Directory](https://docs.microsoft.com/azure/active-directory/hybrid/whatis-fed) mellan dina interna och kundens identitets leverantörer eller Använd [Azure Active Directory B2B](https://docs.microsoft.com/azure/active-directory/b2b/what-is-b2b)

## <a name="identity-reviews"></a>Identitets granskningar

**Teknisk risk:** När företaget förändras över tid kan tillägg av nya moln distributioner eller andra säkerhets problem öka risken för obehörig åtkomst till säkra resurser.

**Princip instruktion:** Moln styrnings processer måste innehålla kvartals Visa med identitets hanterings team för att identifiera skadliga aktörer eller användnings mönster som bör förhindras av konfiguration av moln till gångar.

**Potentiella design alternativ:** Upprätta ett kvartals Visa säkerhets gransknings möte som omfattar både styrnings grupp medlemmar och IT-personal som ansvarar för att hantera identitets tjänster. Granska befintliga säkerhets data och mått för att skapa luckor i den aktuella identitets hanterings principen och-verktyg och uppdatera principer för att åtgärda eventuella nya risker.

## <a name="next-steps"></a>Nästa steg

Använd de exempel som nämns i den här artikeln som utgångs punkt för att utveckla principer för att hantera specifika affärs risker som överensstämmer med dina moln implementerings planer.

Om du vill börja utveckla dina egna anpassade princip satser som är relaterade till identitets bas linjen laddar du ned [mall för identitets bas linjen](./template.md).

För att påskynda införandet av denna disciplin väljer du den [Åtgärds bara styrnings guide](../guides/index.md) som bäst passar din miljö. Ändra sedan designen så att du kan lägga till dina företags princip beslut.

Skapa på risker och toleranser, upprätta en process för styrning och kommunikation av identitets bas policyn.

> [!div class="nextstepaction"]
> [Upprätta rutiner för regelefterlevnad](./compliance-processes.md)
