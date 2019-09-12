---
title: Pågående hantering och säkerhet
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Pågående hantering och säkerhet
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: c8b6c5085117f965bedd5947bfbc2725aedf96e4
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/06/2019
ms.locfileid: "70833107"
---
# <a name="phase-3-ongoing-management-and-security"></a>Fas 3: Pågående hantering och säkerhet

När du har registrerat Azures hanterings tjänster måste du fokusera på de drift-och säkerhetskonfigurationer som kommer att stödja dina pågående åtgärder. Vi börjar med att skydda din miljö genom att granska Azure Security Center. Vi konfigurerar sedan principer för att hålla dina servrar kompatibla och automatisera vanliga uppgifter. I det här avsnittet beskrivs följande ämnen:

- **[Åtgärda säkerhets rekommendationer.](#address-security-recommendations)** Azure Security Center ger förslag på hur du kan förbättra säkerheten i din miljö. När du implementerar de här rekommendationerna kan du se hur påverkan visas i en säkerhets poäng.
- **[Aktivera principen för gäst konfiguration.](./guest-configuration-policy.md)** Aktivera funktionen Azure Policy gäst konfiguration för att granska inställningarna på en virtuell dator. Du kan till exempel kontrol lera om några certifikat håller på att gå ut.
- **[Spåra och Avisera viktiga ändringar.](./enable-tracking-alerting.md)** När du felsöker är det första frågan att överväga vad som har ändrats? I den här artikeln får du lära dig hur du spårar ändringar och skapar aviseringar för att proaktivt övervaka kritiska komponenter.
- **[Skapa uppdaterings scheman.](./update-schedules.md)** Schemalägg installationen av uppdateringar så att alla dina servrar har de senaste servrarna.
- **[Vanliga Azure Policy exempel.](./common-policies.md)** Innehåller exempel på vanliga hanterings principer.

## <a name="address-security-recommendations"></a>Åtgärda säkerhets rekommendationer

Azure Security Center är den centrala platsen för att hantera säkerheten för din miljö. Du ser en övergripande bedömning och riktade rekommendationer.

Vi rekommenderar att du granskar och implementerar rekommendationerna från den här tjänsten. Information om ytterligare förmåner för Azure Security Center finns i [följ Azure Security Center rekommendationer](/azure/migrate/migrate-best-practices-security-management#best-practice-follow-azure-security-center-recommendations).

## <a name="next-steps"></a>Nästa steg

Lär dig hur du [aktiverar den Azure policy funktionen för gäst konfiguration](./guest-configuration-policy.md) .

> [!div class="nextstepaction"]
> [Princip för gäst konfiguration](./guest-configuration-policy.md)
