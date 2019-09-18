---
title: Introduktion till driftshantering
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Förstå driftshantering i Cloud Adoption Framework.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/19/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.custom: manage
ms.openlocfilehash: 3abc103e09a11af4cb822dde985b96c56bca6242
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/16/2019
ms.locfileid: "71025977"
---
# <a name="establishing-operational-management-practices-in-the-cloud"></a>Upprätta metoder för driftshantering i molnet

Molnimplementering är en katalysator som ger affärsvärde. Dock realiseras verkligt affärsvärde genom löpande, stabil drift av de tekniktillgångar som distribueras till molnet. Det här avsnittet av Cloud Adoption Framework vägleder läsaren genom olika övergångar till driftshantering i molnet.

## <a name="actionable-best-practices"></a>Åtgärdsbara metodtips

Moderna lösningar för driftshantering skapar en vy över verksamheten med flera moln. Tillgångar som hanteras via följande metoder kan lagras i molnet, i ett befintligt datacenter eller rentav hos en konkurrerande molnleverantör. För närvarande innehåller ramverket två metodtips som referens för att vägleda driftshantering till mognad i molnet:

* [Azure-serverhantering](./azure-server-management/index.md): Introduktionsguide för att införa molnbaserade verktyg och tjänster som behövs för driftshantering.
* [Hybridövervakning](./monitor/index.md): Många kunder har redan gjort betydande investeringar i System Center Operations Manager. Den här guiden för hybridövervakning hjälper dessa kunder att jämföra och kontrastera de molnbaserade rapporteringsverktygen med Operations Manager-verktyg. Den här jämförelsen gör det lättare att bestämma vilka verktyg som ska användas för driftshantering.

## <a name="cloud-operations"></a>Molnverksamhet

Båda dessa metoder syftar till att främja metodik för framtida tillstånd för driftshantering.

![Metodik för CAF-hantering](../_images/manage/caf-manage.png)

**Affärsanpassning:** I hanteringsmetodiken klassificeras alla arbetsbelastningar efter allvarlighetsgrad och affärsvärde. Denna klassificering kan sedan mätas via en konsekvensanalys som beräknar det förlorade värde som är associerat med prestandaförsämring eller avbrott i verksamheten. Med hjälp av den praktiska intäktsinverkan kan teamet för molndrift arbeta med verksamheten för att upprätta ett åtagande som balanserar kostnad och prestanda.

**Områden inom molnverksamhet:** När företaget har anpassats är det mycket enklare att spåra och rapportera om rätt områden för molnverksamheten för varje arbetsbelastning. Beslutsfattande inom varje område kan sedan konverteras till åtagandevillkor som är enkla för verksamheten att förstå. Denna samarbetsmetod gör att affärsintressenten blir en partner vad gäller att hitta rätt balans mellan kostnad och prestanda.

* Lager och insyn: Som minst kräver driftshantering ett sätt att lagerhålla tillgångar och skapa insyn i körningstillståndet för varje tillgång.
* Verksamhetsefterlevnad: Regelbunden hantering av konfiguration, storleksbestämning, kostnader och prestanda för tillgångar är nyckeln till att uppfylla förväntningarna om prestanda.
* Skydda och återställa: Genom att minimera driftsavbrott och påskynda återställning går det att undvika prestandaförluster och inverkan på intäkterna. Identifiering och återställning är viktiga aspekter inom det här området.
* Plattformsdrift: Alla IT-miljöer innehåller en uppsättning plattformar som används ofta. Dessa plattformar kan omfatta datalager såsom SQL Server eller HDInsights. Andra vanliga plattformar kan omfatta containerlösningar såsom Kubernetes eller AKS. Oavsett plattformarna fokuserar mognad i plattformsdriften på anpassning av verksamheter som baseras på hur dessa vanliga plattformar distribueras, konfigureras och används av arbetsbelastningar.
* Arbetsbelastningsåtgärder: På den högsta nivån av operativ mognad kan teamen för molnverksamhet justera åtgärder för arbetsbelastningar som är viktiga för verksamhetens resultat. För dessa arbetsbelastningar med hög allvarlighetsgrad kan tillgängliga data hjälpa till med automatisering av åtgärder, storleksbestämning eller skydd av arbetsbelastningar baserat på deras användning.

Ytterligare vägledning som [Designa granskningsramverk (kodnamn: Molndesignprinciper)](https://docs.microsoft.com/azure/architecture/reliability) kan underlätta detaljerat beslutsfattande om arkitektur för varje arbetsbelastning inom vart och ett av ovanstående områden.

Det här avsnittet av Cloud Adoption Framework bygger på alla dessa ämnen för att ta molnverksamheter till mognad i din organisation.
