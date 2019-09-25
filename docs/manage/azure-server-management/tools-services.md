---
title: Verktyg och tjänster för Azure Server Management
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Verktyg och tjänster för Azure Server Management
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: dbb00a411eb7905ad557e1acdc2a98d4d03cff49
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/24/2019
ms.locfileid: "71221417"
---
# <a name="azure-server-management-tools-and-services"></a>Verktyg och tjänster för Azure Server Management

Som beskrivs i översikten [](./index.md) över det här avsnittet täcker Azure Server Management Services-serien dessa områden:

- [Migrera](#migrate)
- [Skydda](#secure)
- [Skydda](#protect)
- [Övervaka](#monitor)
- [Konfigurera](#configure)
- [Styras](#govern)

I följande avsnitt beskrivs kortfattat dessa hanterings områden och länkar till detaljerad information om de viktigaste Azure-tjänsterna som har stöd för dem.

## <a name="migrate"></a>Migrera

Migration Services kan hjälpa dig att migrera dina arbets belastningar till Azure. För att tillhandahålla den bästa vägledningen börjar Azure Migrate tjänsten genom att mäta lokala server prestanda och utvärdera lämplighet för migrering. När Azure Migrate har slutfört utvärderingen kan du använda [Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview) och [Azure Database migration service](https://docs.microsoft.com/azure/dms/dms-overview) för att migrera dina lokala datorer till Azure.

## <a name="secure"></a>Skydda

[Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-intro) är ett omfattande säkerhets hanterings program. Genom att registrera dig på Security Center kan du snabbt få en bedömning av miljöns status för säkerhet och regelefterlevnad. Instruktioner för hur du registrerar dina servrar på Azure Security Center finns i [Konfigurera Azure Management Services för en prenumeration](./onboard-at-scale.md#azure-security-center).

## <a name="protect"></a>skydda

För att skydda dina data måste du planera för säkerhets kopiering, hög tillgänglighet, kryptering, auktorisering och relaterade drifts problem. De här avsnitten är mycket omfattande online, så här fokuserar vi på att skapa en plan för affärs kontinuitets haveri beredskap (BCDR). Vi innehåller referenser till dokumentation som beskriver i detalj hur du implementerar och distribuerar den här typen av plan.

När du bygger data skydds strategier bör du först överväga att dela upp dina arbets belastnings program på olika nivåer, eftersom varje nivå vanligt vis kräver en egen unik skydds plan. Mer information om hur du skapar program som ska vara elastiska finns i [utforma elastiska program för Azure](https://docs.microsoft.com/azure/architecture/resiliency).

Det mest grundläggande data skyddet är säkerhets kopiering. Om du vill påskynda återställnings processen i händelse av Server avbrott bör du säkerhetskopiera inte bara data utan också serverkonfigurationer. Backup är en effektiv mekanism för hantering av oavsiktliga data borttagningar och utpressnings angrepp. [Azure Backup](https://docs.microsoft.com/azure/backup) kan hjälpa dig att skydda dina data på Azure och lokala servrar som kör Windows eller Linux. Mer information om den här tjänstens funktioner och instruktions guider finns i [Azure Backup-dokumentationen](https://docs.microsoft.com/azure/backup/backup-overview).

Det kan ta lång tid att återställa via säkerhets kopiering. Bransch standarden är vanligt vis en dag. Om en arbets belastning kräver verksamhets kontinuitet för maskin varu haverier eller data Center avbrott, bör du överväga att använda datareplikering. [Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview) tillhandahåller kontinuerlig replikering av dina virtuella datorer, en lösning som ger minimal data förlust. Site Recovery stöder också flera scenarier för replikering, t. ex. replikering av virtuella Azure-datorer mellan två Azure-regioner, mellan lokala servrar och mellan lokala och Azure. Mer information finns i matrisen [fullständig Azure Site Recovery replikering](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview#what-can-i-replicate).

För dina fil Server data är en annan tjänst att överväga [Azure File Sync](https://docs.microsoft.com/azure/storage/files/storage-sync-files-planning). Med den här tjänsten kan du centralisera din organisations fil resurser i Azure Files samtidigt som du behåller flexibilitet, prestanda och kompatibilitet för en lokal fil server. Följ anvisningarna för att distribuera Azure File Sync om du vill använda den här tjänsten.

## <a name="monitor"></a>Övervaka

[Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/overview) innehåller en vy över olika resurser, t. ex. program, behållare och virtuella datorer. Den samlar även in data från flera olika källor.

- Azure Monitor for VMs ([](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-overview)insikter) ger en djupgående vy över hälsa för virtuella datorer, prestanda trender och beroenden. Tjänsten övervakar hälso tillståndet för operativ systemen för dina virtuella Azure-datorer, skalnings uppsättningar för virtuella datorer och datorer i din lokala miljö.
- Log Analytics ([loggar](https://docs.microsoft.com/azure/azure-monitor/platform/data-collection#logs)) är en funktion i Azure Monitor. Dess roll är central för den övergripande Azure-hanterings artikeln. Den fungerar som data lager för logg analys och för många andra Azure-tjänster. Det erbjuder ett omfattande frågespråk och en analys motor som ger insikter om hur dina program och resurser fungerar.
- [Azure aktivitets logg](https://docs.microsoft.com/azure/azure-monitor/platform/activity-logs-overview) är också en funktion i Azure Monitor. Den ger inblick i händelser på prenumerations nivå som inträffar i Azure.

## <a name="configure"></a>Konfigurera

Flera tjänster passar in i den här kategorin. De kan hjälpa dig att automatisera operativa uppgifter, hantera serverkonfigurationer, mäta uppdaterings efterlevnad, schemalägga uppdateringar och identifiera ändringar på dina servrar. Dessa tjänster är kärnan till stöd för pågående åtgärder.

- [Uppdateringshantering](https://docs.microsoft.com/azure/automation/automation-update-management#viewing-update-assessments) automatiserar distributionen av korrigeringar i din miljö, inklusive distribution till operativ system instanser som körs utanför Azure. Det stöder både Windows-och Linux-operativsystem och spårar viktiga säkerhets problem och avvikelser som orsakas av uppdateringar som saknas.
- [Ändringsspårning och inventering](https://docs.microsoft.com/azure/automation/change-tracking) ger inblick i program varan som körs i din miljö och hämtar eventuella ändringar som har inträffat.
- Med [Azure Automation](https://docs.microsoft.com/azure/automation/automation-intro) kan du köra python-och PowerShell-skript eller Runbooks för att automatisera aktiviteter i din miljö. När du använder den med [hybrid Runbook Worker](https://docs.microsoft.com/azure/automation/automation-hybrid-runbook-worker)kan du utöka dina runbooks även till dina lokala resurser.
- Med [Azure Automation tillstånds konfiguration](https://docs.microsoft.com/azure/automation/automation-dsc-overview) kan du push-överföra PowerShell Desired State Configuration (DSC)-konfigurationer direkt från Azure. I sin tur gör DSC att du kan övervaka och bevara operativ system och arbets belastnings konfigurationer i gäst.

## <a name="govern"></a>Styrning

Att införa och flytta till molnet skapar nya hanterings utmaningar och kräver en annan tänkesätt när du växlar från en drifts hanterings börda till övervakning och styrning. Moln implementerings ramverket för Azure börjar med [styrning](../../govern/index.md). Det förklarar hur du migrerar till molnet, hur resan ser ut och vem som bör delta.

Styrnings utformningen för standard organisationer skiljer sig ofta från styrnings design för komplexa företag. Mer information om styrnings metod tips för en standard organisation finns i [standard styrnings guide](../../govern/guides/standard/index.md). Mer information om styrning av bästa praxis för ett komplext företag finns i [styrnings guide för komplexa företag](../../govern/guides/complex/index.md).

## <a name="billing-information"></a>Faktureringsinformation

Om du vill veta mer om priser för Azure Management Services går du till följande sidor:

- [Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery)

- [Azure Backup](https://azure.microsoft.com/pricing/details/backup)

- [Azure Monitor](https://azure.microsoft.com/pricing/details/monitor)

- [Azure Security Center](https://azure.microsoft.com/pricing/details/security-center)

- [Azure Uppdateringshantering-tjänst](https://azure.microsoft.com/pricing/details/automation)

- [Azure Ändringsspårning-och inventerings tjänster](https://azure.microsoft.com/pricing/details/automation)

- [Önskad tillstånds konfiguration](https://azure.microsoft.com/pricing/details/automation)

- [Azure Automation tjänst](https://azure.microsoft.com/pricing/details/automation)

- [Azure Policy](https://azure.microsoft.com/pricing/details/azure-policy)

- [Azure File Sync tjänst](https://azure.microsoft.com/pricing/details/storage/blobs)

> [!NOTE]
> Azure Uppdateringshantering-lösningen är kostnads fri, men det finns en låg kostnad för data inmatning. Som en tumregel är de första 5 GB per månad då data inmatningen är kostnads fri. Vi observerar vanligt vis att varje dator använder ca 25 MB per månad. Så om 200-datorer per månad omfattas kostnads fritt. Multiplicera antalet ytterligare servrar med 25 MB per månad för varje ytterligare Server. Multiplicera med kostnaden för lagring för den totala mängden lagring som behövs. [Lagrings kostnaderna finns här](https://azure.microsoft.com/pricing/details/storage). Varje ytterligare Server bör ha en nominell inverkan på kostnaderna.
