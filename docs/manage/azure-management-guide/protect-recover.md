---
title: Skydda och återställa i Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Förhindra instabilitet i verksamheten genom att snabba upp återställningen
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: 83ac1abd6ce35b62f64722d101f599726c7b26b3
ms.sourcegitcommit: bf9be7f2fe4851d83cdf3e083c7c25bd7e144c20
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 11/04/2019
ms.locfileid: "73565421"
---
# <a name="protect-and-recover-in-azure"></a>Skydda och återställa i Azure

_Skydd och återställning_ är det tredje och sista området i baslinjen för all molnhantering.

![Baslinje för molnhantering](../../_images/manage/management-baseline.png)

I [Driftsmässig efterlevnad i Azure](./operational-compliance.md) är målet att minska risken för verksamhetsavbrott. Syftet med den här artikeln är att minska varaktigheten och konsekvenserna av avbrott som inte kan förhindras.

Den här tabellen beskriver det föreslagna minimikravet för en hanteringsbaslinje för miljöer i företagsklass:

|Process  |Verktyg  |Syfte  |
|---------|---------|---------|
|Skydda data|Azure Backup|Säkerhetskopiera data och virtuella datorer i molnet.|
|Skydda miljön|Azure Security Center|Öka säkerheten och implementera avancerat skydd mot hot i dina hybridarbetsbelastningar.|

::: zone target="docs"

## <a name="azure-backup"></a>Azure Backup

::: zone-end
::: zone target="chromeless"

## <a name="azure-backuptabupdbackupatemanagement"></a>[Azure Backup](#tab/UpdbackupateManagement)

::: zone-end

Med Azure Backup kan du säkerhetskopiera, skydda och återställa data i Microsoft-molnet. Azure Backup ersätter din befintliga lokala eller externa säkerhetskopieringslösning med en molnbaserad lösning. Den här nya lösningen är tillförlitlig, säker och kostnadseffektiv. Azure Backup kan också skydda och återställa lokala resurser i en enda enhetlig lösning.

### <a name="enable-backup-for-an-azure-vm"></a>Aktivera säkerhetskopiering för en virtuell Azure-dator

1. I Azure-portalen väljer du **Virtuella datorer** och väljer den virtuella dator som du vill replikera.
1. Välj **Säkerhetskopiera** i rutan **Åtgärder**.
1. Skapa eller välj ett befintligt Azure Recovery Services-valv.
1. Välj **Skapa (eller redigera) en ny princip**.
1. Konfigurera schema och kvarhållningsperiod.
1. Välj **OK**.
1. Välj **Aktivera säkerhetskopiering**.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/HubsExtension/Resources/resourceType/Microsoft.Compute%2FVirtualMachines]" submitText="Go to Virtual Machines" :::

::: zone-end

::: zone target="docs"

[Översikt](https://docs.microsoft.com/azure/backup/backup-introduction-to-azure-backup)

## <a name="azure-site-recovery"></a>Azure Site Recovery

::: zone-end
::: zone target="chromeless"

## <a name="azure-site-recoverytabsiterecovery"></a>[Azure Site Recovery](#tab/siterecovery)

::: zone-end

Azure Site Recovery är en kritisk komponent i din strategi för haveriberedskap.

Site Recovery replikerar virtuella datorer och arbetsbelastningar som finns i en primär Azure-region. Tjänsten replikerar dem till en kopia som finns i en sekundär region. När ett avbrott inträffar i din primära region växlar du över till kopian som körs i den sekundära regionen. Sedan fortsätter du att komma åt dina program och tjänster därifrån. Den här proaktiva metoden för återställning kan minska återställningstiden avsevärt. När du inte längre behöver återställningsmiljön kan produktionstrafiken återgå till den ursprungliga miljön.

### <a name="replicate-an-azure-vm-to-another-region-with-site-recovery"></a>Replikera en virtuell Azure-dator till en annan region med Site Recovery

Följande steg beskriver hur du använder Site Recovery för Azure-till-Azure-replikering, dvs. replikering av en virtuell Azure-dator till en annan region.
>
> [!TIP]
> Beroende på ditt scenario kan de exakta stegen skilja sig något.
>

### <a name="enable-replication-for-the-azure-vm"></a>Aktivera replikering för virtuella Azure-datorer

1. I Azure-portalen väljer du **Virtuella datorer** och väljer den virtuella dator som du vill replikera.
1. Välj **Haveriberedskap** i rutan **Åtgärder**.
1. Välj **Konfigurera haveriberedskap** > **Målregion** och välj den målregion som du ska replikera till.
1. I den här snabbstarten lämnar du standardvärdena för alla andra alternativ.
1. Välj **Aktivera replikering** så startas ett jobb som aktiverar replikering för den virtuella datorn.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/HubsExtension/Resources/resourceType/Microsoft.Compute%2FVirtualMachines]" submitText="Go to Virtual Machines" :::

::: zone-end

### <a name="verify-settings"></a>Kontrollera inställningarna

När replikeringen har slutförts kan du kontrollera replikeringsstatus, kontrollera replikeringshälsotillstånd och testa distributionen.

1. I den virtuella datormenyn väljer du **Haveriberedskap**.
1. Kontrollera replikeringshälsotillstånd, återställningspunkter som har skapats samt käll- och målregioner på kartan.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/HubsExtension/Resources/resourceType/Microsoft.Compute%2FVirtualMachines]" submitText="Go to Virtual Machines" :::

::: zone-end

### <a name="learn-more"></a>Läs mer

- [Översikt över Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview)
- [Replikera en virtuell Azure-dator till en annan region](https://docs.microsoft.com/azure/site-recovery/azure-to-azure-quickstart)
