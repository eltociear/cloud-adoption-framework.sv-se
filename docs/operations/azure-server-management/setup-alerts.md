---
title: Konfigurera grundläggande aviseringar
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Konfigurera grundläggande aviseringar
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 5b11a97e78d5fcd1b2a2cc866f5a7062bc6a2977
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/06/2019
ms.locfileid: "70834576"
---
# <a name="set-up-basic-alerts"></a>Konfigurera grundläggande aviseringar

En viktig del av att hantera resurser får ett meddelande när det uppstår problem. Aviseringar kan informera dig om kritiska tillstånd proaktivt. De kan baseras på utlösare från Mät värden, loggar eller tjänste hälso problem. Som en del av integreringen av Azure Server Management Services kan du ställa in aviseringar och meddelanden som kan hjälpa dina IT-team att vara medvetna om eventuella problem.

## <a name="azure-monitor-alerts"></a>Azure Monitor aviseringar

Azure Monitor erbjuder [aviserings](https://docs.microsoft.com/azure/azure-monitor/platform/alerts-overview) funktioner som meddelar dig via e-post eller meddelanden när något går fel. Dessa funktioner baseras på en gemensam data övervaknings plattform som innehåller loggar och mått som genereras av dina servrar och andra resurser. Med den här plattformen kan du analysera data som kombineras från flera resurser med hjälp av en gemensam uppsättning verktyg i Azure Monitor, som du kan använda för att utlösa aviseringar. Dessa utlösare kan innefatta:

- Mått värden.
- Loggs öknings frågor.
- Aktivitets logg händelser.
- Hälso tillståndet för den underliggande Azure-plattformen.
- Test för webbplats tillgänglighet.

I [listan med Azure Monitor data källor](https://docs.microsoft.com/azure/azure-monitor/platform/data-sources) finns en mer detaljerad beskrivning av de övervaknings data som samlas in av den här tjänsten.

Mer information om hur du skapar och hanterar aviseringar manuellt med hjälp av portalen finns i [Azure Monitor-dokumentationen](https://docs.microsoft.com/azure/azure-monitor/platform/alerts-metric).

## <a name="automated-deployment-of-recommended-alerts"></a>Automatiserad distribution av rekommenderade aviseringar

I den här hand boken rekommenderar vi att du aktiverar en uppsättning 15 aviseringar för grundläggande övervakning av infrastrukturen. Du hittar distributions skripten i [Azure Alert Toolkit GitHub](https://github.com/Microsoft/manageability-toolkits)-lagringsplatsen.

Det här paketet skapar aviseringar för lite disk utrymme, ont om ledigt minne, hög processor användning, oväntade avstängningar, skadade fil system och vanliga maskin varu fel. Paketet använder HP Server-maskinvara som exempel. Du bör ändra inställningarna i den associerade konfigurations filen så att den återspeglar din OEM-maskinvara. Du kan också lägga till fler prestanda räknare i konfigurations filen. Om du vill distribuera paketet kör du filen New-CoreAlerts. ps1.

## <a name="next-steps"></a>Nästa steg

Lär dig mer om åtgärder och säkerhetsmekanismer som har stöd för dina pågående åtgärder.

> [!div class="nextstepaction"]
> [Kontinuerlig hantering och säkerhet](./ongoing-management-overview.md)
