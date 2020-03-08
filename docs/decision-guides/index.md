---
title: Beslutsguider för arkitektur
description: Använd dessa komponentmönster och modeller för viktig infrastruktur för molndistribution för att stödja dina distributionsscenarier i molnet.
author: rotycenh
ms.author: v-tyhopk
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.custom: governance
ms.openlocfilehash: 66ff53f203a07f5f61ae2ba448f56d6531ffaa94
ms.sourcegitcommit: 58ea417a7df3318e3d1a76d3807cc4e7e3976f52
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/07/2020
ms.locfileid: "78892454"
---
# <a name="architectural-decision-guides"></a>Beslutsguider för arkitektur

I beslutsguiderna för arkitektur i Cloud Adoption Framework beskrivs mönster och modeller som är till hjälp när du skapar designriktlinjer för molnstyrning. Varje beslutsguide fokuserar på en central infrastrukturdel i molndistributioner och visar en lista med mönster och modeller som kan stödja specifika molndistributionsscenarier.

När du börjar upprätta molnstyrning för din organisation får du en baslinjeöversikt från åtgärdsinriktade styrningsresor. I dessa resor görs dock antaganden om behov och prioriteringar som inte nödvändigtvis stämmer överens med din organisation.

Beslutsguiderna kompletterar exemplen på styrningsresor genom att erbjuda alternativa mönster och modeller som hjälper dig att rikta in de arkitektoniska designval som görs i exempeldesignvägledningen med dina egna krav.

## <a name="decision-guidance-categories"></a>Kategorier av beslutsvägledning

Var och en av följande kategorier representerar en grundläggande teknik för alla molndistributioner. I exemplen på styrningsresor fattas designbeslut relaterade till dessa tekniker baserat på behoven i exempelföretag, och vissa av dessa beslut stämmer kanske inte med din organisations behov. I avsnitten nedan beskrivs alternativ för var och en av dessa kategorier, så att du kan välja ett mönster eller en modell som passar dina behov bättre.

[Prenumerationer](./subscriptions/index.md): Planera molndistributionens prenumerationsdesign och kontostruktur så att de passar organisationens ägarskap, fakturering och hantering.

[Identitet](./identity/index.md): Integrera molnbaserade identitetstjänster med dina befintliga identitetsresurser för att stödja auktorisering och åtkomstkontroll i din IT-miljö.

[Policyframtvingande](./policy-enforcement/index.md): Definiera och framtvinga organisationens principregler för molndistribuerade resurser och arbetsbelastningar som överensstämmer med dina styrningskrav.

[Resurskonsekvens](./resource-consistency/index.md): Se till att distribution och organisering av dina molnbaserade resurser passar för att framtvinga krav för resurshantering och policy.

[Resurstaggning](./resource-tagging/index.md): Organisera dina molnbaserade resurser för att stödja faktureringsmodeller, metoder för molnredovisning och hantering samt för att optimera resursutnyttjande och kostnader. Resurstaggning kräver ett konsekvent och välorganiserat schema för namngivning och metadata.

[Programvarudefinierade nätverk](./software-defined-network/index.md): Distribuera säkra arbetsbelastningar till molnet med hjälp av snabb distribution och ändring av virtualiserade nätverksfunktioner. Programvarudefinierade nätverk (SDN) kan stödja agila arbetsflöden, isolera resurser och integrera molnbaserade system med din befintliga IT-infrastruktur.

[Kryptering](./encryption/index.md): Skydda känsliga data med hjälp av kryptering för att uppfylla organisationens krav på efterlevnad och säkerhetsprinciper.

[Loggning och rapportering](./logging-and-reporting/index.md): Övervaka loggdata som genereras av molnbaserade resurser. Analys av data ger hälsorelaterade insikter om åtgärder, underhåll och efterlevnadsstatus för arbetsbelastningar.

## <a name="next-steps"></a>Nästa steg

Lär dig hur prenumerationer och konton fungerar som grund för en molndistribution.

> [!div class="nextstepaction"]
> [Prenumerationsdesign](./subscriptions/index.md)
