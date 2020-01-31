---
title: Påskynda migrering med VMware-värdar
description: Påskynda migrering med VMware-värdar
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/10/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 77d75127a497778056634f8a84a9021fa874a726
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 01/28/2020
ms.locfileid: "76802930"
---
# <a name="accelerate-migration-with-vmware-hosts"></a>Påskynda migrering med VMware-värdar

Migrering av hela VMware-värdar kan flytta flera arbets belastningar och flera till gångar i en enda migrering. Följande rikt linjer utökar omfånget för [Azure migration-guiden](../azure-migration-guide/index.md) via en VMware-värd migrering. De flesta insatser som krävs i denna omfattnings expansion sker under förutsättningarna och migreringsprocessen av migreringen.

## <a name="suggested-prerequisites"></a>Föreslagna förutsättningar

När du migrerar din första VMware-värd till Azure måste du uppfylla ett antal krav för att förbereda krav för identitet, nätverk och hantering. När dessa krav är uppfyllda bör varje ytterligare värd kräva mycket mindre ansträngning för att migrera. I följande avsnitt finns mer information om kraven.

### <a name="secure-your-azure-environment"></a>Skydda din Azure-miljö

Implementera lämplig moln lösning för rollbaserad åtkomst kontroll och nätverks anslutning i din Azure-miljö. Den [säkra din miljö guide](https://docs.microsoft.com/azure/vmware-cloudsimple/private-cloud-secure?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json) kan hjälpa dig med den här implementeringen.

### <a name="private-cloud-management"></a>Hantering av privata moln

Det finns två obligatoriska uppgifter och en valfri uppgift för att upprätta hantering av privata moln. Att [eskalera privata moln privilegier](https://docs.microsoft.com/azure/vmware-cloudsimple/escalate-privileges?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json) och [arbets belastnings-DNS och DHCP-installation](https://docs.microsoft.com/azure/vmware-cloudsimple/dns-dhcp-setup?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json) är de bästa metoderna.

Om målet är att [migrera arbets belastningar med hjälp av Layer 2 utsträckta nätverk](https://docs.microsoft.com/azure/vmware-cloudsimple/migration-layer-2-vpn?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json), krävs även den här tredje bästa praxis.

### <a name="private-cloud-networking"></a>Privata nätverk i molnet

När hanterings kraven har upprättats kan du upprätta privata moln nätverk med hjälp av följande metod tips:

- [VPN-anslutning till privat moln](https://docs.microsoft.com/azure/vmware-cloudsimple/set-up-vpn?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)
- [Lokal nätverks anslutning med ExpressRoute](https://docs.microsoft.com/azure/vmware-cloudsimple/on-premises-connection?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)
- [Virtuell Azure-nätverksanslutning med ExpressRoute](https://docs.microsoft.com/azure/vmware-cloudsimple/azure-expressroute-connection?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)
- [Konfigurera DNS-namnmatchning](https://docs.microsoft.com/azure/vmware-cloudsimple/on-premises-dns-setup?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)

### <a name="integration-with-the-cloud-adoption-plan"></a>Integrering med moln implementerings planen

När du har uppfyllt de andra förutsättningarna bör du inkludera varje VMware-värd i [moln implementerings planen](../../plan/template.md). I moln implementerings planen lägger du till varje värd som ska migreras som en [distinkt arbets belastning](../../plan/workloads.md). I varje arbets belastning ska du lägga till de virtuella datorer som ska migreras som [till gångar](../../plan/workloads.md). Information om hur du lägger till arbets belastningar och till gångar i en införande plan i bulk finns i [lägga till/redigera arbets objekt med Excel](https://docs.microsoft.com/azure/devops/boards/backlogs/office/bulk-add-modify-work-items-excel?view=azure-devops).

## <a name="migrate-process-changes"></a>Ändringar i migreringsprocessen

Under varje iteration, kommer antagande teamet att fungera genom efter släpning för att migrera arbets belastningar med högsta prioritet. Processen ändras inte i själva verket för VMware-värdar. När nästa arbets belastning i efter släpning är en VMware-värd används det verktyg som används.

Du kan använda följande verktyg i arbets ansträngningen för migrering:

- [Inbyggda VMware-verktyg](https://docs.microsoft.com/azure/vmware-cloudsimple/migrate-workloads?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)
- [Azure Data Box](https://docs.microsoft.com/azure/vmware-cloudsimple/migration-using-azure-data-box?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)

Du kan också migrera arbets belastningar genom att redundansväxla haveri beredskap med hjälp av följande verktyg:

- [Säkerhetskopiera virtuella arbets belastnings datorer](https://docs.microsoft.com/azure/vmware-cloudsimple/backup-workloads-veeam?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)
- [Konfigurera privat moln som en katastrof återställnings plats med Zerto](https://docs.microsoft.com/azure/vmware-cloudsimple/disaster-recovery-zerto?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)
- [Konfigurera privat moln som en katastrof återställnings plats med VMware SRM](https://docs.microsoft.com/azure/vmware-cloudsimple/disaster-recovery-site-recovery-manager?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)

## <a name="next-steps"></a>Nästa steg

Gå tillbaka till den expanderade omfångs check listan för att säkerställa att din metod för migrering är helt justerad.

> [!div class="nextstepaction"]
> [Utökad checklista](./index.md)
