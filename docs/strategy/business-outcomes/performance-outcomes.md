---
title: Exempel på prestanda resultat
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Exempel på prestanda resultat
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: strategy
ms.openlocfilehash: d772f7c8a2e7c76770a6496bb85acbac54debfe4
ms.sourcegitcommit: 7ffb0427bba71177f92618b2f980e864b72742f4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/29/2019
ms.locfileid: "73048351"
---
# <a name="examples-of-performance-outcomes"></a>Exempel på prestanda resultat

Som vi har diskuterat i [företags resultat](./index.md)kan flera potentiella affärs resultat fungera som grund för alla omvandlings resor i konversationer med verksamheten. Den här artikeln fokuserar på ett gemensamt verksamhets mått: prestanda.

I dagens tekniska samhälle antar kunderna att programmen kommer att fungera väl och alltid är tillgängliga. När den här förväntan inte har uppfyllts orsakar det ryktes skada som kan vara kostsamt och långvarigt.

## <a name="performance"></a>Prestanda

De största tjänsterna inom molnbaserad databehandling körs i ett globalt nätverk av säkra datacenter, som regelbundet uppgraderas till den senaste generationen av snabb och effektiv maskinvara för databehandling. Detta ger flera fördelar jämfört med ett enda företags data Center, till exempel minskad nätverks fördröjning för program och större stor drifts för delar.

Transformera ditt företag och minska kostnaderna med en energi effektiv infrastruktur som omfattar mer än 100 mycket säkra resurser i hela världen, länkade av ett av de största nätverken på jorden. Azure har fler globala regioner än någon annan moln leverantör. Detta översätter till den skala som krävs för att hämta program närmare användare runtom i världen, bevara data placering och tillhandahålla omfattande alternativ för efterlevnad och återhämtning för kunder.

- **Exempel 1:** Ett tjänste företag arbetade med en värd leverantör som är värd för flera drift infrastruktur till gångar. Dessa system drabbades av frekventa avbrott och dåliga prestanda. Företaget migrerade sina till gångar till Azure för att dra nytta av molnets SLA-och prestanda kontroller. Avbrotts tiden som den lidit kostar den cirka 15 000 USD per minut för avbrott. Med fyra till åtta timmars avbrott per månad var det enkelt att motivera den här organisations omvandlingen.

- **Exempel 2:** Ett konsument investerings företag var i det tidiga skedet av en moln aktive rad program Innovations ansträngning. Agile-processer och DevOps förföll sig väl, men program prestanda var höga. Som en mer mogen omvandling startade företaget ett program för att övervaka och automatisera storleks ändringar baserat på användnings krav. Företaget kunde eliminera storleks problem genom att använda Azures verktyg för prestanda hantering, vilket resulterar i en överraskande på 5 procent i transaktioner.

## <a name="reliability"></a>Tillförlitlighet

Med molnbaserad data behandling blir säkerhets kopiering, haveri beredskap och affärs kontinuitet enklare och billigare, eftersom data kan speglas på flera redundanta platser i moln leverantörens nätverk.

En av de viktiga funktionerna är att se till att företagets data aldrig förloras och att programmen är tillgängliga trots Server krascher, strömavbrott eller natur katastrofer. Du kan hålla dina data säkra och återställa genom att säkerhetskopiera till Azure.

Azure Backup är en enkel lösning som minskar infrastruktur kostnaderna samtidigt som du tillhandahåller förbättrade säkerhetsmekanismer för att skydda dina data mot utpressnings tro Jan. Med en lösning kan du skydda arbets belastningar som körs i Azure och lokalt i Linux, Windows, VMware och Hyper-V. Du kan garantera affärs kontinuiteten genom att hålla dina program igång i Azure.

Azure Site Recovery gör det enkelt att testa haveri beredskap genom att replikera program mellan Azure-regioner. Du kan också replikera lokala virtuella VMware-och Hyper-V-datorer och fysiska servrar till Azure för att vara tillgängliga om den primära platsen slutar fungera. Och du kan återställa arbets belastningar till den primära platsen när den är igång igen.

- **Exempel:** Ett olje-och gas företag använde Azure-teknik för att implementera en fullständig webbplats återställning. Företaget valde att inte helt utnyttja molnet för dagliga åtgärder, men molnets funktioner för haveri beredskap och affärs kontinuitet (DRBC) har fortfarande skyddat sitt Data Center. När en orkan är utformad hundratals mil påbörjade deras implementerings partner att återskapa platsen till Azure. Innan Storm är intryckt körs alla verksamhets kritiska till gångar i Azure, vilket förhindrar avbrott.

## <a name="next-steps"></a>Nästa steg

Lär dig hur du [använder mallen för affärs resultat](./business-outcome-template.md).

> [!div class="nextstepaction"]
> [Använd mallen affärs resultat](./business-outcome-template.md)
