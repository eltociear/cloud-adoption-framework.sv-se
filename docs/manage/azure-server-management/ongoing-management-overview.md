---
title: Pågående hantering och säkerhet
description: Använd ramverket för moln införande för Azure för att lära dig att fokusera på de drift-och säkerhetskonfigurationer som kommer att stödja dina pågående åtgärder.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: a68479bf128ea79383a5529b82a7866e399abc71
ms.sourcegitcommit: 959cb0f63e4fe2d01fec2b820b8237e98599d14f
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/11/2020
ms.locfileid: "79094581"
---
# <a name="phase-3-ongoing-management-and-security"></a>Fas 3: pågående hantering och säkerhet

När du har registrerat Azure Server Management Services måste du fokusera på de drift-och säkerhets inställningar som kommer att stödja dina pågående åtgärder. Vi börjar med att skydda din miljö genom att granska Azure Security Center. Vi konfigurerar sedan principer för att hålla dina servrar kompatibla och automatisera vanliga uppgifter. I det här avsnittet beskrivs följande ämnen:

- **[Åtgärda säkerhets rekommendationer.](#address-security-recommendations)** Azure Security Center ger förslag på hur du kan förbättra säkerheten i din miljö. När du implementerar de här rekommendationerna ser du effekten som visas i en säkerhets poäng.
- **[Aktivera principen för gäst konfiguration.](./guest-configuration-policy.md)** Använd den Azure Policy funktionen för gäst konfiguration för att granska inställningarna på en virtuell dator. Du kan till exempel kontrol lera om några certifikat håller på att gå ut.
- **[Spåra och Avisera viktiga ändringar.](./enable-tracking-alerting.md)** När du felsöker är det första frågan att överväga vad som har ändrats? I den här artikeln får du lära dig hur du spårar ändringar och skapar aviseringar för att proaktivt övervaka kritiska komponenter.
- **[Skapa uppdaterings scheman.](./update-schedules.md)** Schemalägg installationen av uppdateringar så att alla dina servrar har de senaste versionerna.
- **[Vanliga Azure Policy exempel.](./common-policies.md)** Den här artikeln innehåller exempel på vanliga hanterings principer.

## <a name="address-security-recommendations"></a>Åtgärda säkerhets rekommendationer

Azure Security Center är den centrala platsen för att hantera säkerheten för din miljö. Du ser en övergripande bedömning och riktade rekommendationer.

Vi rekommenderar att du granskar och implementerar rekommendationerna från den här tjänsten. Information om ytterligare förmåner för Azure Security Center finns i [följ Azure Security Center rekommendationer](https://docs.microsoft.com/azure/migrate/migrate-best-practices-security-management#best-practice-follow-azure-security-center-recommendations).

## <a name="next-steps"></a>Nästa steg

Lär dig hur du [aktiverar den Azure policy funktionen för gäst konfiguration](./guest-configuration-policy.md) .

> [!div class="nextstepaction"]
> [Princip för gäst konfiguration](./guest-configuration-policy.md)
