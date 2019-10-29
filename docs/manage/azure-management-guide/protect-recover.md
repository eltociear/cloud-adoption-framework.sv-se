---
title: Skydda och återställa i Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Gör verksamheten stabilare genom att sänka återställningstiden
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: a79164435772f571849d0a836f43b53ce3bca087
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/17/2019
ms.locfileid: "72557014"
---
# <a name="protect-and-recover-in-azure"></a>Skydda och återställa i Azure

Skydd och återställning är det tredje och sista området i baslinjen för all molnhantering.

![Baslinje för molnhantering](../../_images/manage/management-baseline.png)

I den förra artikeln om efterlevnad i driften var målet att minska risken för avbrott i verksamheten. Den här artikeln om skydd och återställning syftar till att minska längden på och effekten av de avbrott som inte kan undvikas.

I den här tabellen ser du rekommenderade minimikrav för alla typer av miljöer i företagsklass.

|Process  |Verktyg  |Syfte  |
|---------|---------|---------|
|Skydda data|Azure Backup|Säkerhetskopiera data och virtuella datorer i molnet|
|Skydda miljön|Azure Security Center|

::: zone target="docs"

## <a name="azure-backup"></a>Azure Backup

::: zone-end
::: zone target="chromeless"

## <a name="azure-backuptabupdbackupatemanagement"></a>[Azure Backup](#tab/UpdbackupateManagement)

::: zone-end

Azure Backup är en Azure-tjänst som du använder till att säkerhetskopiera (eller skydda) och återställa data i Microsoft-molnet. Azure Backup ersätter din befintliga lokala eller externa säkerhetskopieringslösning med en tillförlitlig och säker molnbaserad lösning med ett konkurrenskraftigt pris. Du kan också använda den till att skydda och återställa lokala resurser i en och samma lösning.

### <a name="enable-backup-for-an-azure-vm"></a>Aktivera säkerhetskopiering för en virtuell Azure-dator

1. I Azure-portalen väljer du **Virtuella datorer** och väljer den virtuella dator som du vill replikera.
1. I **Åtgärder** väljer du **Säkerhetskopiering**.
1. Skapa eller välj ett befintligt Recovery Services-valv.
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

Med Azure Site Recovery-tjänsten kan du replikera virtuella datorer och arbetsbelastningar som finns i en primär Azure-region till en kopia som finns i en sekundär region. När ett avbrott uppstår i den primära regionen kan du redundansväxla till kopian som körs i den sekundära regionen och fortsätta att komma åt dina program och tjänster därifrån. Den här proaktiva metoden för återställning kan minska återställningstiden avsevärt. När du inte längre behöver återställningsmiljön kan produktionstrafiken återgå till den ursprungliga miljön.

### <a name="replicate-an-azure-vm-to-another-region-with-site-recovery-service"></a>Replikera en virtuell Azure-dator till en annan region med Site Recovery-tjänsten

Följande steg beskriver processen för att använda Site Recovery-tjänsten för att replikera en virtuell Azure-dator till en annan region (Azure-till-Azure):

>
> [!TIP]
> Beroende på ditt scenario kan de exakta stegen skilja sig något.
>

### <a name="enable-replication-for-the-azure-vm"></a>Aktivera replikering för virtuella Azure-datorer

1. I Azure-portalen väljer du **Virtuella datorer** och väljer den virtuella dator som du vill replikera.
1. I **Åtgärder** väljer du **Haveriberedskap**.
1. I **Konfigurera haveriberedskap** > **Målregion** väljer du den målregion du ska replikera till.
1. Acceptera de andra standardinställningarna för denna Snabbstart.
1. Välj **Aktivera replikering** så startas ett jobb som aktiverar replikering för den virtuella datorn.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/HubsExtension/Resources/resourceType/Microsoft.Compute%2FVirtualMachines]" submitText="Go to Virtual Machines" :::

::: zone-end

### <a name="verify-settings"></a>Kontrollera inställningarna

När replikeringen har slutförts kan du kontrollera replikeringsstatus, kontrollera replikeringshälsotillstånd och testa distributionen.

1. I den virtuella datormenyn väljer du **Haveriberedskap**.
2. Kontrollera replikeringshälsotillstånd, återställningspunkter som har skapats samt käll- och målregioner på kartan.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/HubsExtension/Resources/resourceType/Microsoft.Compute%2FVirtualMachines]" submitText="Go to Virtual Machines" :::

::: zone-end

### <a name="learn-more"></a>Läs mer

- [Översikt över Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview)
- [Replikera en virtuell Azure-dator till en annan region](https://docs.microsoft.com/azure/site-recovery/azure-to-azure-quickstart)
