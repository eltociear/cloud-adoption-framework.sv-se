---
title: Aktivera server hanterings tjänster på en enskild virtuell dator för utvärdering
description: Aktivera server hanterings tjänster på en enskild virtuell dator för utvärdering
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: d73b9f5a13150b0c3b13feff3f21a765a36ac4a8
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 01/28/2020
ms.locfileid: "76808047"
---
# <a name="enable-server-management-services-on-a-single-vm-for-evaluation"></a>Aktivera server hanterings tjänster på en enskild virtuell dator för utvärdering

Lär dig hur du aktiverar Server hanterings tjänster på en enskild virtuell dator för utvärdering.

> [!NOTE]
> Skapa den nödvändiga [Log Analytics arbets ytan och Azure Automation kontot](./prerequisites.md#create-a-workspace-and-automation-account) innan du implementerar Azure Management Services på en virtuell dator.

Det är enkelt att publicera Azure Server Management-tjänster på enskilda virtuella datorer i Azure Portal. Du kan bekanta dig med de här tjänsterna innan du påpublicerar dem. När du väljer en virtuell dator instans visas alla lösningar i listan över [hanterings verktyg och tjänster](./tools-services.md) på menyn **åtgärder** eller **övervakning** . Du väljer en lösning och följer guiden för att publicera den.

![Skärm bild av inställningar för virtuella datorer i Azure Portal](./media/onboarding-single-vm.png)

## <a name="related-resources"></a>Relaterade resurser

Mer information om hur du kan publicera dessa lösningar på enskilda virtuella datorer finns i:

- [Publicera Uppdateringshantering-, Ändringsspårning-och inventerings lösningar från den virtuella Azure-datorn](https://docs.microsoft.com/azure/automation/automation-onboard-solutions-from-vm)
- [Publicera Azure-övervakning för virtuella datorer](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-enable-single-vm)

## <a name="next-steps"></a>Nästa steg

Lär dig hur du använder Azure Policy för att publicera virtuella Azure-datorer i stor skala.

> [!div class="nextstepaction"]
> [Konfigurera Azure Management Services för en prenumeration](./onboard-at-scale.md)
