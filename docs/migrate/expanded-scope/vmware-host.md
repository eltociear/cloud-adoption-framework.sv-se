---
title: Påskynda migrering med VMWare-värdar
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Påskynda migrering med VMWare-värdar
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/10/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: b09c1dcbb36e5f630ca0ae86c95c5c874e29d60b
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/17/2019
ms.locfileid: "72558212"
---
# <a name="accelerate-migration-with-vmware-hosts"></a>Påskynda migrering med VMWare-värdar

Migrering av hela VMWare-värdar kan flytta flera arbets belastningar och flera till gångar i en enda migrering. Följande rikt linjer visar omfånget för [Azure migration-guiden](../azure-migration-guide/index.md) via en VMware-värd migrering.

## <a name="general-scope-expansion"></a>Allmän omfångsutökning

De flesta av de ansträngningar som krävs för att utöka omfattningen sker under förutsättningarna och migreringsprocessen för migreringen.

## <a name="suggested-prerequisites"></a>Föreslagna förutsättningar

När du migrerar din första VMWare-värd till Azure finns det ett antal förutsättningar som måste uppfyllas för att förbereda identitets-, nätverks-och hanterings krav. När dessa krav är uppfyllda bör varje ytterligare värd kräva mycket mindre ansträngning för att migrera. Dessa krav anpassas till några viktiga åtgärder: skydda din Azure-miljö, hantering av privata moln och nätverk för privata moln.

### <a name="secure-your-azure-environment"></a>Skydda din Azure-miljö

Implementera lämplig moln lösning för RBAC-och nätverks anslutningar i din Azure-miljö. Den [säkra din miljö guide](https://docs.microsoft.com/azure/vmware-cloudsimple/private-cloud-secure.md?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json) kan hjälpa dig med den här implementeringen.

### <a name="private-cloud-management"></a>Hantering av privata moln

Det finns två obligatoriska uppgifter och en valfri uppgift för att upprätta hantering av privata moln. Att [eskalera privata moln privilegier](https://docs.microsoft.com/azure/vmware-cloudsimple/escalate-privileges.md?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json) och [arbets belastnings-DNS och DHCP-installation](https://docs.microsoft.com/azure/vmware-cloudsimple/dns-dhcp-setup.md?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json) är de bästa metoderna.

Om målet är att [migrera arbets belastningar med Layer 2 utsträckta nätverk](https://docs.microsoft.com/azure/vmware-cloudsimple/migration-layer-2-vpn.md?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)krävs den här tredje bästa praxis.

### <a name="private-cloud-networking"></a>Nätverk för privata moln

När hanterings kraven har upprättats kan det privata moln nätverket upprättas med följande metod tips:

- [VPN-anslutning till privat moln](https://docs.microsoft.com/azure/vmware-cloudsimple/set-up-vpn.md?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)
- [Lokal nätverks anslutning med ExpressRoute](https://docs.microsoft.com/azure/vmware-cloudsimple/on-premises-connection.md?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)
- [Virtuell Azure-nätverksanslutning med ExpressRoute](https://docs.microsoft.com/azure/vmware-cloudsimple/azure-expressroute-connection.md?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)
- [Konfigurera DNS-namnmatchning](https://docs.microsoft.com/azure/vmware-cloudsimple/on-premises-dns-setup.md?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)

### <a name="integration-with-the-cloud-adoption-plan"></a>Integrering med moln implementerings planen

När förutsättningarna är uppfyllda ingår varje VMWare-värd i [moln implementerings planen](../../plan/template.md). I moln implementerings planen lägger du till varje värd som ska migreras som en [distinkt arbets belastning](../../plan/workloads.md). Inom varje arbets belastning kan de virtuella datorer som ska migreras läggas till som [till gångar](../../plan/workloads.md). Om du vill lägga till arbets belastningar och till gångar i implementerings planen läser du [lägga till/redigera arbets objekt med Excel](https://docs.microsoft.com/azure/devops/boards/backlogs/office/bulk-add-modify-work-items-excel?view=azure-devops).

## <a name="migrate-process-changes"></a>Ändringar i migreringsprocessen

Under varje iteration, kommer antagande teamet att fungera genom efter släpning för att migrera arbets belastningar med högsta prioritet. Processen ändras inte i själva verket för VMWare-värdar. När nästa arbets belastning i efter släpning är en VMWare-värd används det verktyg som används.

### <a name="suggested-action-during-the-migrate-process"></a>Föreslagna åtgärder under migreringsprocessen

Följande är några exempel på de verktyg som kan användas i migreringen:

- [Inbyggda VMWare-verktyg](https://docs.microsoft.com/azure/vmware-cloudsimple/migrate-workloads.md?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)
- [Azure Data Box](https://docs.microsoft.com/azure/vmware-cloudsimple/migration-using-azure-data-box.md?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)

Arbets belastningar kan också migreras via redundans för haveri beredskap med hjälp av följande verktyg:

- [Säkerhetskopiera virtuella arbets belastnings datorer](https://docs.microsoft.com/azure/vmware-cloudsimple/backup-workloads-veeam.md?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)
- [Konfigurera privat moln som en katastrof återställnings plats med Zerto](https://docs.microsoft.com/azure/vmware-cloudsimple/disaster-recovery-zerto.md?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)
- [Konfigurera privat moln som en katastrof återställnings plats med VMware SRM](https://docs.microsoft.com/azure/vmware-cloudsimple/disaster-recovery-site-recovery-manager.md?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)

## <a name="next-steps"></a>Nästa steg

Gå tillbaka till [checklistan för utökat omfång](./index.md) och se till att din migreringsmetod är helt anpassad till kraven.

> [!div class="nextstepaction"]
> [Utökad checklista](./index.md)
