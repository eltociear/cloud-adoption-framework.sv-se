---
title: Förbättringar av identitets bas linje disciplin
description: Förstå de potentiella aktiviteter som ett företag utför för att utveckla och mogna sin identitets bas linje disciplin i varje fas av moln införande.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: f1ee4e64e86ccb3648badad38d2118be11b76cc7
ms.sourcegitcommit: af45c1c027d7246d1a6e4ec248406fb9a8752fb5
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 02/27/2020
ms.locfileid: "77709370"
---
# <a name="identity-baseline-discipline-improvement"></a>Förbättringar av identitets bas linje disciplin

Identitets bas disciplinen fokuserar på sätt att etablera principer som garanterar konsekvens och kontinuitet i användar identiteter oavsett vilken moln leverantör som är värd för programmet eller arbets belastningen. I den fem ämnes gruppen i moln styrning innehåller identitets bas linjer beslut om [hybrid identitets strategi](../../decision-guides/identity/index.md), utvärdering och tillägg av identitets lager, implementering av enkel inloggning (samma inloggning), granskning och övervakning av obehörig användning eller skadliga aktörer. I vissa fall kan det också innebära beslut att modernisera, konsolidera eller integrera flera identitets leverantörer.

I den här artikeln beskrivs några potentiella uppgifter som företaget kan använda för att utveckla och ta del av identitets bas disciplinen bättre. Dessa uppgifter kan delas upp i planering, uppbyggnad, införande och drifts faser för implementering av en moln lösning, som sedan upprepas på att tillåta utveckling av en [stegvis metod för moln styrning](../guides/index.md#an-incremental-approach-to-cloud-governance).

![Fyra faser i antagandet](../../_images/govern/adoption-phases.png)

*Figur 1 – implementerings faser för den stegvisa metoden för moln styrning.*

Det är omöjligt för något dokument att redovisa kraven i alla företag. I den här artikeln beskrivs de föreslagna minimi-och potentiella exempel aktiviteterna för varje fas i processens mognads process. Det första målet med dessa aktiviteter är att hjälpa dig att skapa en [policy MVP](../guides/index.md#an-incremental-approach-to-cloud-governance) och upprätta ett ramverk för stegvisa princip förbättringar. Ditt moln styrnings team måste bestämma hur mycket du ska investera i dessa aktiviteter för att förbättra dina funktioner för identitets styrning av identiteter.

> [!CAUTION]
> Varken de minsta eller potentiella aktiviteter som beskrivs i den här artikeln är justerade med specifika företags principer eller krav för tredje parts efterlevnad. Den här vägledningen är utformad för att hjälpa till att under lätta de konversationer som kommer att leda till justering av båda kraven med en modell för moln styrning.

## <a name="planning-and-readiness"></a>Planering och beredskap

Den här fasen av styrnings mognads bryggor förenar indelningen mellan affärs resultat och insats bara strategier. Under den här processen definierar ledarskaps gruppen vissa mått, mappar dessa mått till den digitala egendomen och börjar planera den totala migreringen.

**Minsta antal föreslagna aktiviteter:**

- Utvärdera dina [verktygskedjan](./toolchain.md) -alternativ och implementera en hybrid strategi som passar din organisation.
- Utveckla ett utkast till rikt linjer för arkitektur och distribuera till viktiga intressenter.
- Utbilda och involvera de personer och grupper som påverkas av rikt linjerna för arkitektur utveckling.

**Potentiella aktiviteter:**

- Definiera roller och tilldelningar som ska styra identitets-och åtkomst hantering i molnet.
- Definiera dina lokala grupper och mappa till motsvarande molnbaserade roller.
- Lager identitets leverantörer (inklusive databas drivna identiteter som används av anpassade program).
- Konsolidera och integrera identitets leverantörer där duplicering finns, för att förenkla den övergripande identitets lösningen och minska risken.
- Utvärdera hybrid kompatibilitet för befintliga identitets leverantörer.
- För identitets leverantörer som inte är hybrid kompatibla kan du utvärdera alternativen för konsolidering eller ersättning.

## <a name="build-and-predeployment"></a>Bygg och för distribution

Det krävs flera tekniska och tekniska krav för att kunna migrera en miljö. Den här processen fokuserar på beslut, beredskap och kärn infrastrukturen som fortsätter med migreringen.

**Minsta antal föreslagna aktiviteter:**

- Överväg ett pilot test innan du implementerar din [identitet verktygskedjan](./toolchain.md), och se till att det underlättar användar upplevelsen så mycket som möjligt.
- Använd feedback från pilot test i för distributionen. Upprepa tills resultatet är acceptabelt.
- Uppdatera rikt linjer för arkitektur som innehåller distributions-och användar implementerings planer och distribuera till viktiga intressenter.
- Överväg att upprätta ett tidigt antagande program och distribuera till ett begränsat antal användare.
- Fortsätt att utbilda de personer och grupper som påverkas mest av arkitektur rikt linjerna.

**Potentiella aktiviteter:**

- Utvärdera din logiska och fysiska arkitektur och Bestäm en [hybrid identitets strategi](../../decision-guides/identity/index.md).
- Mappa identitets åtkomst hanterings principer, till exempel inloggnings-ID-tilldelningar, och välj lämplig autentiseringsmetod för Azure AD.
  - Aktivera klient begränsningar för administrativa konton om den är federerad.
- Integrera dina lokala och molnbaserade kataloger.
- Överväg att använda följande åtkomst modeller:
  - [Åtkomst modell med minst behörighet](https://docs.microsoft.com/windows-server/identity/ad-ds/plan/security-best-practices/implementing-least-privilege-administrative-models) .
  - Åtkomst modell för [Privileged Identity-bas linje](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/pim-configure) .
- Slutför all förintegrerings information och granska [metod tips för identitet](https://docs.microsoft.com/azure/security/azure-security-identity-management-best-practices).
  - Aktivera enkel identitet, enkel inloggning (SSO) eller sömlös SSO.
  - Konfigurera Multi-Factor Authentication för administratörer.
  - Konsolidera eller integrera identitets leverantörer, om det behövs.
  - Implementera verktyg som krävs för att centralisera hanteringen av identiteter.
  - Aktivera just-in-Time (JIT)-åtkomst och roll ändrings aviseringar.
  - Genomför en riskanalys av viktiga administratörs aktiviteter för att tilldela inbyggda roller.
  - Överväg en uppdaterad distribution av starkare autentisering för alla användare.
  - Aktivera privilegierad identitets bas linje (PIM) för JIT (med tidsbegränsad aktivering) för ytterligare administrativa roller.
  - Separera användar konton från globala administratörs konton (se till att administratörer inte oavsiktligt kan öppna e-postmeddelanden eller köra program som är kopplade till sina globala administratörs konton).

## <a name="adopt-and-migrate"></a>Införa och migrera

Migrering är en stegvis process som fokuserar på förflyttning, testning och införande av program eller arbets belastningar i en befintlig digital egendom.

**Minsta antal föreslagna aktiviteter:**

- Migrera din [identitets verktygskedjan](./toolchain.md) från utveckling till produktion.
- Uppdatera dokument för arkitektur rikt linjer och distribuera till viktiga intressenter.
- Utveckla utbildningsmaterial och dokumentation, medvetenhets kommunikation, stimulans åtgärder och andra program för att hjälpa att använda användar införande.

**Potentiella aktiviteter:**

- Kontrol lera att de bästa metoderna som definierats under fasen för att bygga för distribution är korrekt utförda.
- Validera och förfina din [hybrid identitets strategi](../../decision-guides/identity/index.md).
- Se till att varje program eller arbets belastning fortsätter att överensstämma med identitets strategin före lanseringen.
- Verifiera att enkel inloggning (SSO) och sömlös enkel inloggning fungerar som förväntat för dina program.
- Minska eller eliminera antalet alternativa identitets lager.
- Granska behovet av identitets lager i appar eller i databaser. Identiteter som faller utanför en korrekt identitets leverantör (första part eller tredje part) kan utgöra en risk för programmet och användarna.
- Aktivera villkorlig åtkomst för [lokala federerade program](https://docs.microsoft.com/azure/active-directory/active-directory-device-registration-on-premises-setup).
- Distribuera identitet i globala regioner i flera hubbar med synkronisering mellan regioner.
- Upprätta en central rollbaserad åtkomst kontroll (RBAC) Federation.

## <a name="operate-and-post-implementation"></a>Drift och efter implementering

När omvandlingen är klar måste styrning och åtgärder vara aktiva för den naturliga livs cykeln för ett program eller en arbets belastning. Den här fasen av styrnings förfallo tid fokuserar på de aktiviteter som vanligt vis kommer efter att lösningen har implementerats och omvandlings cykeln börjar stabilisera sig.

**Minsta antal föreslagna aktiviteter:**

- Anpassa din [identitets bas linje verktygskedjan](./toolchain.md) baserat på ändringar i din organisations ändrade identitets behov.
- Automatisera meddelanden och rapporter för att varna dig om potentiella skadliga hot.
- Övervaka och rapportera om system användning och användar implementerings förlopp.
- Rapport om statistik efter distribution och distribution till intressenter.
- Förfina rikt linjerna för arkitekturen för att vägleda framtida införande processer.
- Kommunicera och i hela tiden utbilda de berörda teamen regelbundet så att du kan se till att rikt linjerna för arkitekturen går fortare.

**Potentiella aktiviteter:**

- Genomför regelbunden granskning av identitets principer och praxis.
- Se till att känsliga användar konton (VD, VD, VD osv.) alltid är aktiverade för Multi-Factor Authentication och avvikande inloggnings identifiering.
- Sök efter skadliga aktörer och data överträdelser regelbundet, särskilt sådana som rör identitets bedrägeri, till exempel potentiella administratörs konto övertag Ande.
- Konfigurera ett övervaknings-och rapporterings verktyg.
- Överväg att integrera mer tätt med säkerhets-och bedrägeri skydds system.
- Granska åtkomst rättigheter för utökade användare eller roller regelbundet.
  - Identifiera alla användare som är berättigade att aktivera administratörs behörighet.
- Granska uppdaterings processer för registrering, offboarding och autentiseringsuppgift.
- Undersök ökande nivåer av Automation och kommunikation mellan IAM-moduler (Identity Access Management).
- Överväg att implementera en DevSecOps-metod (Development Security Operations).
- Genomför en effekt analys för att mäta resultat om kostnader, säkerhet och användar införande.
- Skapa en effekt rapport med jämna mellanrum som visar förändringar i mått som skapats av systemet och beräkna verksamhets påverkan för [hybrid identitets strategin](../../decision-guides/identity/index.md).
- Upprätta integrerad övervakning som rekommenderas av [Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-intro).

## <a name="next-steps"></a>Nästa steg

Nu när du förstår begreppet moln identitets styrning kan du undersöka [identitets bas linjen verktygskedjan](./toolchain.md) för att identifiera de Azure-verktyg och-funktioner som du behöver när du utvecklar disciplinen för identitets styrning på Azure-plattformen.

> [!div class="nextstepaction"]
> [Identitets bas linje verktygskedjan för Azure](./toolchain.md)
