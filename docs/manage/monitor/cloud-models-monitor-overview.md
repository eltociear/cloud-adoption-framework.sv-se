---
title: Övervaknings guide för molnet – övervaknings strategi för moln distributions modeller
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Välj när Azure Monitor eller System Center Operations Manager ska användas i Microsoft Azure
author: MGoedtel
ms.author: magoedte
ms.date: 07/31/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: operate
services: azure-monitor
ms.openlocfilehash: badf03f3616de8e6612221282aa24996f0b6e8f8
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/24/2019
ms.locfileid: "71221123"
---
# <a name="cloud-monitoring-guide-monitoring-strategy-for-cloud-deployment-models"></a>Molnövervakningsguide: Övervaknings strategi för moln distributions modeller

Den här artikeln innehåller vår rekommenderade övervaknings strategi för varje moln distributions modell, baserat på följande kriterier:

- Du måste fortsätta att Operations Manager eller en annan företags övervaknings plattform. Detta beror på integrering med IT-arbetsprocesser, kunskap och expertis, eller eftersom vissa funktioner inte är tillgängliga ännu i Azure Monitor.
- Du måste övervaka arbets belastningar både lokalt och i det offentliga molnet, eller bara i molnet.
- Din strategi för moln migrering innehåller en modern IT-verksamhet och flyttar till våra moln övervaknings tjänster och-lösningar.
- Du kan ha kritiska system som är gapped eller fysiskt isolerade, som finns i ett privat moln eller på fysisk maskin vara, och som måste övervakas.

Vår strategi omfattar stöd för övervakning av infrastruktur (beräknings-, lagrings-och Server arbets belastningar), program (slutanvändare, undantag och klient) och nätverks resurser för att leverera ett komplett, service-orienterad övervaknings perspektiv.

## <a name="azure-cloud-monitoring"></a>Azure Cloud Monitoring

Azure Monitor är plattformstjänst som tillhandahåller en enda källa för övervakning av Azure-resurser. Den är utformad för moln lösningar som bygger på Azure och som stöder en affärs kapacitet som baseras på VM-arbetsbelastningar eller komplexa arkitekturer som använder mikrotjänster och andra plattforms resurser. Den övervakar alla skikt i stacken, som börjar med klient tjänster som Azure Active Directory Domain Services och händelser på prenumerations nivå och Azure Service Health. Den övervakar också infrastruktur resurser som virtuella datorer, lagrings enheter och nätverks resurser och, på det översta lagret, ditt program. Genom att övervaka var och en av dessa beroenden och samla in rätt signaler som varje kan avge, ger dig möjlighet att välja program och den nyckel infrastruktur du behöver.

I följande tabell sammanfattas den rekommenderade metoden för att övervaka varje skikt i stacken.

<!-- markdownlint-disable MD033 -->

Lager | Resource | Omfång | Metod
---|---|---|----
Program | Webbaserat program som körs på .NET, .NET Core, Java, Java Script och Node. js-plattformen på en virtuell Azure-dator, Azure App tjänster, Azure Service Fabric, Azure Functions och Azure Cloud Services | Övervaka ett Live-webbprogram för att automatiskt identifiera prestanda avvikelser, identifiera kod undantag och problem och samla in användbarhets telemetri. |  Application Insights
Containrar | Azure Kubernetes service/Azure Container Instances | Övervaka kapacitet, tillgänglighet och prestanda för arbets belastningar som körs på behållare och behållar instanser. | Azure Monitor för containrar
Gäst operativ system | Operativ systemet Linux och Windows VM | Övervaka kapacitet, tillgänglighet och prestanda. Mappa beroenden som finns på varje virtuell dator, inklusive synligheten för aktiva nätverks anslutningar mellan servrar, inkommande och utgående anslutnings fördröjning och portar i alla TCP-anslutna arkitektur. | Azure Monitor för virtuella datorer
Azure-resurser – PaaS | Azure Database Services (till exempel SQL eller mySQL) | Azure Database för SQL prestanda mått. | Aktivera diagnostisk loggning för att strömma SQL-data till Azure Monitor loggar.
Azure-resurser – IaaS | 1. Azure Storage<br/> 2. Azure Application Gateway<br/> 3. Azure Key Vault<br/> 4. Nätverkssäkerhetsgrupper<br/> 5. Azure Traffic Manager | 1. Kapacitet, tillgänglighet och prestanda.<br/> 2. Prestanda-och diagnostikloggar (aktivitet, åtkomst, prestanda och brand vägg).<br/> 3. Övervaka hur och när nyckel valven nås, och av vem.<br/> 4. Övervaka händelser när regler tillämpas och regel räknaren för hur många gånger en regel tillämpas på neka eller Tillåt.<br/>5. Övervaka slut punkts status tillgänglighet. | 1. Lagrings mått för Blob Storage.<br/> 2. Aktivera diagnostisk loggning och konfigurera direkt uppspelning till Azure Monitor loggar.<br/> 3. Aktivera diagnostisk loggning och konfigurera direkt uppspelning till Azure Monitor loggar och aktivera [Azure Key Vault Analytics-lösningen](https://docs.microsoft.com/azure/azure-monitor/insights/azure-key-vault). <br/> 4. Aktivera diagnostisk loggning av nätverks säkerhets grupper och konfigurera direkt uppspelning till Azure Monitor loggar.<br/> 5. Aktivera diagnostisk loggning av Traffic Manager slut punkter och konfigurera direkt uppspelning till Azure Monitor loggar.
Nätverk| Kommunikation mellan den virtuella datorn och en eller flera slut punkter (en annan virtuell dator, ett fullständigt kvalificerat domän namn, ett enhetligt resurs-ID eller en IPv4-adress). | Övervaka ändringar av tillgänglighet, svars tid och nätverks sto pol Ogin mellan den virtuella datorn och slut punkten. | Azure Network Watcher
Azure-prenumeration | Azure Service Health och grundläggande resurs hälsa | <li> Administrativa åtgärder som utförs på en tjänst eller resurs.<br/><li> Tjänst hälsan med en Azure-tjänst är i ett försämrat eller otillgängligt tillstånd.<br/><li> Hälso problem har identifierats med en Azure-resurs från Azures tjänst perspektiv.<br/><li> Åtgärder som utförs med Azure autoskalning som indikerar ett fel eller undantag. <br/><li> Åtgärder som utförs med Azure Policy som indikerar att en tillåten eller nekad åtgärd utfördes.<br/><li> Registrera aviseringar som genererats av Azure Security Center. |Levereras i aktivitets loggen för övervakning och avisering med hjälp av Azure Resource Manager.
Azure-klientorganisation|Azure Active Directory || Aktivera diagnostisk loggning och konfigurera direkt uppspelning till Azure Monitor loggar.

<!-- markdownlint-enable MD033 -->

## <a name="hybrid-cloud-monitoring"></a>Övervakning av hybrid moln

Det här avsnittet är för närvarande under utveckling för att tillhandahålla en omfattande uppsättning rekommendationer som åtgärdar ditt intresse för den här moln modellen och kommer att göras tillgängligt snart.  

## <a name="private-cloud-monitoring"></a>Övervakning av privata moln

Du kan få en helhets övervakning av Azure Stack med System Center Operations Manager. Mer specifikt kan du övervaka arbets belastningarna som körs i klient organisationen, resurs nivån, på de virtuella datorerna och infrastrukturen som är värd för Azure Stack (fysiska servrar och nätverks växlar). Du kan också få en helhets övervakning med en kombination av [infrastruktur övervaknings funktioner](https://docs.microsoft.com/azure/azure-stack/azure-stack-monitor-health) som ingår i Azure Stack. Dessa funktioner hjälper dig att Visa hälso tillstånd och aviseringar för en Azure Stack region och [tjänsten Azure Monitor](https://docs.microsoft.com/azure/azure-stack/user/azure-stack-metrics-azure-data) i Azure Stack, som tillhandahåller infrastruktur mått och loggar på bas nivå för de flesta tjänster.

Om du redan har investerat i Operations Manager använder du Azure Stack hanterings paketet för att övervaka tillgängligheten och hälso tillståndet för Azure Stack-distributioner. Detta inkluderar regioner, resurs leverantörer, uppdateringar, uppdaterings körningar, skalnings enheter, Unit-noder, infrastruktur roller och deras instanser (logiska entiteter som består av maskin varu resurserna). Det använder REST-API: erna för hälso-och uppdaterings resurs leverantörer för att kommunicera med Azure Stack. Om du vill övervaka fysiska servrar och lagrings enheter använder du OEM-leverantörens hanterings paket (till exempel, som tillhandahålls av Lenovo, Hewlett Packard eller Dell). Operations Manager kan internt övervaka nätverks växlarna för att samla in grundläggande statistik med hjälp av SNMP-protokollet. Det går att övervaka klient arbets belastningarna med Azures hanterings paket genom att följa två grundläggande steg. Konfigurera den prenumeration som du vill övervaka och Lägg sedan till övervakarna för den prenumerationen.

## <a name="next-steps"></a>Nästa steg

> [!div class="nextstepaction"]
> [Samla in rätt data](./data-collection.md)
