---
title: Konfigurera grundläggande aviseringar
description: Lär dig hur du använder Azure Server Management Services för att konfigurera aviseringar och meddelanden som hjälper dina IT-team att vara medvetna om eventuella problem.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 3525b8d84ee6dd54072a4fed401114578de7fcb3
ms.sourcegitcommit: 959cb0f63e4fe2d01fec2b820b8237e98599d14f
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/11/2020
ms.locfileid: "79094472"
---
# <a name="set-up-basic-alerts"></a>Konfigurera grundläggande aviseringar

En viktig del av att hantera resurser får ett meddelande när det uppstår problem. Aviseringar proaktivt meddela dig om kritiska villkor, baserat på utlösare från Mät värden, loggar eller tjänste hälso problem. Som en del av integreringen av Azure Server Management Services kan du ställa in aviseringar och meddelanden som hjälper dina IT-team att vara medvetna om eventuella problem.

## <a name="azure-monitor-alerts"></a>Azure Monitor aviseringar

Azure Monitor erbjuder [aviserings](https://docs.microsoft.com/azure/azure-monitor/platform/alerts-overview) funktioner som meddelar dig, via e-post eller meddelanden, om saker går fel. Dessa funktioner baseras på en gemensam plattform för data övervakning som innehåller loggar och mått som genereras av dina servrar och andra resurser. Genom att använda en gemensam uppsättning verktyg i Azure Monitor kan du analysera data som kombineras från flera resurser och använda dem för att utlösa aviseringar. Dessa utlösare kan innefatta:

- Mått värden.
- Loggs öknings frågor.
- Aktivitets logg händelser.
- Hälso tillståndet för den underliggande Azure-plattformen.
- Test för webbplats tillgänglighet.

I [listan med Azure Monitor data källor](https://docs.microsoft.com/azure/azure-monitor/platform/data-sources) finns en mer detaljerad beskrivning av de övervaknings data som den här tjänsten samlar in.

Mer information om hur du skapar och hanterar aviseringar manuellt med hjälp av Azure Portal finns i [Azure Monitor-dokumentationen](https://docs.microsoft.com/azure/azure-monitor/platform/alerts-metric).

## <a name="automated-deployment-of-recommended-alerts"></a>Automatiserad distribution av rekommenderade aviseringar

I den här hand boken rekommenderar vi att du skapar en uppsättning 15 aviseringar för grundläggande övervakning av infrastrukturen. Hitta distributions skripten i [Azure Alert Toolkit GitHub-lagringsplatsen](https://github.com/Microsoft/manageability-toolkits).

Det här paketet skapar aviseringar för:

- Ont om disk utrymme
- Ont om ledigt minne
- Hög CPU-användning
- Oväntade avstängningar
- Skadade fil system
- Vanliga maskin varu problem

Paketet använder HP Server-maskinvara som exempel. Ändra inställningarna i den tillhör ande konfigurations filen så att de återspeglar din OEM-maskinvara. Du kan också lägga till fler prestanda räknare i konfigurations filen. Om du vill distribuera paketet kör du filen New-CoreAlerts. ps1.

## <a name="next-steps"></a>Nästa steg

Lär dig mer om åtgärder och säkerhetsmekanismer som har stöd för dina pågående åtgärder.

> [!div class="nextstepaction"]
> [Kontinuerlig hantering och säkerhet](./ongoing-management-overview.md)
