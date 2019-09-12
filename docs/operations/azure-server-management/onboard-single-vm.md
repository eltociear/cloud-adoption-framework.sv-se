---
title: Aktivera hanterings tjänster på en enskild virtuell dator för utvärdering
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Aktivera hanterings tjänster på en enskild virtuell dator för utvärdering
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 4ebf0bf17fafcd495414d32fe04882c36634d4e2
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/06/2019
ms.locfileid: "70825242"
---
# <a name="enable-management-services-on-a-single-vm-for-evaluation"></a>Aktivera hanterings tjänster på en enskild virtuell dator för utvärdering

Lär dig hur du aktiverar hanterings tjänster på en enskild virtuell dator för utvärdering.

> [!NOTE]
> Skapa den nödvändiga [Log Analytics arbets ytan och Azure Automation kontot](./prerequisites.md#create-a-workspace-and-automation-account) innan du registrerar virtuella datorer i Azure Management Services.

Det är enkelt att publicera enskilda virtuella datorer till Azure Server Management Services i Azure Portal. Med portalen kan du bekanta dig med dessa tjänster innan du registrerar dem på dina virtuella datorer. När du väljer en virtuell dator instans visas alla lösningar som diskuteras i listan över [hanterings verktyg och tjänster](./tools-services.md) under antingen menyn **åtgärder** eller menyn **övervakning** . Du kan välja varje lösning och följa guiden för att publicera den.

![Skärm bild av inställningar för virtuella datorer i Azure Portal](./media/onboarding-single-vm.png)

## <a name="related-resources"></a>Relaterade resurser

Mer information om onboarding av enskilda virtuella datorer till varje lösning finns i:

- [Publicera Uppdateringshantering-, Ändringsspårning-och inventerings lösningar från den virtuella Azure-datorn](/azure/automation/automation-onboard-solutions-from-vm)
- [Publicera Azure-övervakning för virtuell dator](/azure/azure-monitor/insights/vminsights-enable-single-vm)

## <a name="next-steps"></a>Nästa steg

Lär dig hur du använder Azure Policy för att publicera virtuella Azure-datorer i stor skala.

> [!div class="nextstepaction"]
> [Konfigurera Azure Management Services för en prenumeration](./onboard-at-scale.md)
