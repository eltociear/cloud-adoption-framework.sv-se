---
title: Skydda och hantera
description: Få mer information om säkerhets- och hanteringsmetoder som du kan använda för att hantera din miljö när du har migrerat till Azure.
author: matticusau
ms.author: mlavery
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.custom: fasttrack-new, AQC
ms.localizationpriority: high
ms.openlocfilehash: 1af3ed5ea3b9291263a5ad8da43c65d51570651e
ms.sourcegitcommit: 4948a5f458725e8a0c7206f08502422965a549d5
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 02/04/2020
ms.locfileid: "76994105"
---
# <a name="secure-and-manage"></a>Skydda och hantera

När du har migrerat miljön till Azure är det viktigt att tänka på vilken säkerhet och vilka metoder som används för att hantera miljön. Azure tillhandahåller många funktioner för att uppfylla de här behoven i din lösning.

# <a name="azure-monitortabmonitor"></a>[Azure Monitor](#tab/monitor)

Azure Monitor maximerar programmens tillgänglighet och prestanda genom att leverera en heltäckande lösning för att samla in, analysera och arbeta med telemetri från dina molnmiljöer och lokala miljöer. Det hjälper dig att förstå hur dina program fungerar och identifierar proaktivt problem som påverkar dem och de resurser som de förlitar sig på.

## <a name="use-and-configure-azure-monitor"></a>Använda och konfigurera Azure Monitor

1. Gå till **Övervaka** i Azure-portalen.
2. Välj **Mått**, **Loggar** eller **Service Health** för översikter.
3. Välj någon av de relevanta insikterna.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/Microsoft_Azure_Monitoring/AzureMonitoringBrowseBlade/overview]" submitText="Go to Azure Monitor" :::

::: zone-end

::: zone target="docs"

## <a name="learn-more"></a>Läs mer

- [Översikt över Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/overview).

::: zone-end

# <a name="azure-service-healthtabservicehealth"></a>[Azure Service Health](#tab/servicehealth)

Med Azure Service Health får du anpassad vägledning och support när problem med Azure-tjänsterna påverkar dig. Tjänsten kan meddela dig, hjälpa dig att förstå hur olika problem påverkar dig och hålla dig uppdaterad under tiden att problemen blir lösta. Dessutom får du hjälp med förberedelser inför planerat underhåll och ändringar som kan påverka tillgängligheten för dina resurser.

I Azure Service Health ingår:

- **Azure-status:** En global vy över Azure-tjänsternas hälsotillstånd.
- **Service Health:** En anpassad vy över hälsotillståndet hos dina Azure-tjänster.
- **Resource Health:** En mer djupgående vy över hälsotillståndet för de enskilda resurserna som Azure-tjänsterna tillhandahåller.

I kombination ger de här funktionerna en heltäckande vy över Azure-hälsotillståndet, på en detaljnivå som är relevant för dig.

## <a name="access-service-health"></a>Komma åt Service Health

1. Gå till **Övervaka** i Azure-portalen.
2. Välj **Service Health**.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/Microsoft_Azure_Health/AzureHealthBrowseBlade/serviceIssues]" submitText="Go to Service Health" :::

::: zone-end

::: zone target="docs"

## <a name="learn-more"></a>Läs mer

Läs mer i [Azure Service Health-dokumentationen](https://docs.microsoft.com/azure/service-health).

::: zone-end

# <a name="azure-advisortabadvisor"></a>[Azure Advisor](#tab/advisor)

Azure Advisor är en anpassad molnkonsult som hjälper dig att följa bästa praxis för att optimera dina Azure-distributioner. Den analyserar din resurskonfiguration och användningstelemetri. Den rekommenderar sedan lösningar för att förbättra prestanda, säkerhet och hög tillgänglighet för dina resurser samtidigt som den söker efter möjligheter att minska de totala Azure-kostnaderna.

## <a name="access-azure-advisor"></a>Komma åt Azure Advisor

1. Gå till **Advisor** i Azure-portalen eller sök efter resursen.
2. Välj **Hög tillgänglighet**, **Säkerhet**, **Prestanda**, **Kostnad**

::: zone target="chromeless"

::: form action="OpenBlade[#blade/Microsoft_Azure_Expert/AdvisorMenuBlade/overview]" submitText="Go to Azure Advisor" :::

::: zone-end

::: zone target="docs"

## <a name="learn-more"></a>Läs mer

[Översikt](https://docs.microsoft.com/azure/advisor/advisor-overview).

::: zone-end

# <a name="azure-security-centertabsecurity"></a>[Azure Security Center](#tab/security)

Azure Security Center är ett enhetligt system för hantering av infrastruktursäkerhet som stärker dina datacentras säkerhetstillstånd och tillhandahåller avancerat skydd för dina hybridarbetsbelastningar såväl i molnet, oavsett om de finns i Azure eller inte, som lokalt.

## <a name="access-azure-security-center"></a>Komma åt Azure Security Center

1. Gå till **Security Center** i Azure-portalen eller sök efter resursen.
2. Välj **Rekommendationer**.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/Microsoft_Azure_Security/SecurityMenuBlade/0]" submitText="Go to Security Center" :::

::: zone-end

::: zone target="docs"

## <a name="learn-more"></a>Läs mer

[Översikt](https://docs.microsoft.com/azure/security-center/security-center-intro)

::: zone-end

# <a name="azure-backuptabbackup"></a>[Azure Backup](#tab/backup)

Azure Backup är en Azure-baserad tjänst som du använder för att säkerhetskopiera (eller skydda) och återställa data i Microsoft-molnet. Azure Backup ersätter din befintliga lokala eller externa säkerhetskopieringslösning med en tillförlitlig och säker molnbaserad lösning med ett konkurrenskraftigt pris.

## <a name="enable-backup-for-an-azure-vm"></a>Aktivera säkerhetskopiering för en virtuell Azure-dator

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

::: zone-end

# <a name="azure-site-recoverytabsiterecovery"></a>[Azure Site Recovery](#tab/siterecovery)

Tidigare i den här guiden diskuterade vi hur Azure Site Recovery kan användas som en del av migreringskörningen. Men den utgör också en viktig komponent i din strategi för haveriberedskap när migreringen är klar.

Med Azure Site Recovery-tjänsten kan du replikera virtuella datorer och arbetsbelastningar som finns i en primär Azure-region till en kopia som finns i en sekundär region. När ett avbrott uppstår i den primära regionen kan du redundansväxla till kopian som körs i den sekundära regionen och fortsätta att komma åt dina program och tjänster därifrån. När avbrottet i den primära kopian av den virtuella datorn är över kan du växla tillbaka till den.

## <a name="replicate-an-azure-vm-to-another-region-with-site-recovery-service"></a>Replikera en virtuell Azure-dator till en annan region med Site Recovery-tjänsten

Följande steg beskriver processen för att använda Site Recovery-tjänsten för att replikera en virtuell Azure-dator till en annan region (Azure-till-Azure):

>
> [!TIP]
> Beroende på ditt scenario kan de exakta stegen skilja sig något.
>

## <a name="enable-replication-for-the-azure-vm"></a>Aktivera replikering för virtuella Azure-datorer

1. I Azure-portalen väljer du **Virtuella datorer** och väljer den virtuella dator som du vill replikera.
1. I **Åtgärder** väljer du **Haveriberedskap**.
1. I **Konfigurera haveriberedskap** > **Målregion** väljer du den målregion som du ska replikera till.
1. Acceptera de andra standardinställningarna för denna Snabbstart.
1. Välj **Aktivera replikering**. Ett jobb startas som aktiverar replikering för den virtuella datorn.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/HubsExtension/Resources/resourceType/Microsoft.Compute%2FVirtualMachines]" submitText="Go to Virtual Machines" :::

::: zone-end

## <a name="verify-settings"></a>Kontrollera inställningarna

När replikeringen har slutförts kan du kontrollera replikeringsstatus, kontrollera replikeringshälsotillstånd och testa distributionen.

1. I den virtuella datormenyn väljer du **Haveriberedskap**.
2. Kontrollera replikeringshälsotillstånd, återställningspunkter som har skapats samt käll- och målregioner på kartan.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/HubsExtension/Resources/resourceType/Microsoft.Compute%2FVirtualMachines]" submitText="Go to Virtual Machines" :::

::: zone-end

::: zone target="docs"

## <a name="learn-more"></a>Läs mer

- [Översikt över Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview)
- [Replikera en virtuell Azure-dator till en annan region](https://docs.microsoft.com/azure/site-recovery/azure-to-azure-quickstart)

::: zone-end
