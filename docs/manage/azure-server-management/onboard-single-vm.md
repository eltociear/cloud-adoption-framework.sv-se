---
title: Aktivera server hanterings tjänster på en virtuell dator
description: Använd ramverket för moln införande för Azure för att lära dig hur du aktiverar Azure Server Management-tjänster på en enda virtuell dator.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: d79539e6708a46a905e1b69a4d6bd186eaff2d0f
ms.sourcegitcommit: 0ea426f2f471eb7310c6f09478be1306cf7bf0d8
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/05/2020
ms.locfileid: "78341699"
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
