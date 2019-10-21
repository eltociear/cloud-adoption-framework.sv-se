---
title: Introduktion till driftshantering
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Förstå driftshantering i Cloud Adoption Framework.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/07/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 23b9064b91744d5464f89ed4edf64c8d656514a5
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/17/2019
ms.locfileid: "72558108"
---
# <a name="establishing-operational-management-practices-in-the-cloud"></a>Upprätta metoder för driftshantering i molnet

Molnimplementering är en katalysator som ger affärsvärde. Dock realiseras verkligt affärsvärde genom löpande, stabil drift av de tekniktillgångar som distribueras till molnet. Det här avsnittet av Cloud Adoption Framework vägleder läsaren genom olika övergångar till driftshantering i molnet.

## <a name="actionable-best-practices"></a>Användbara metodtips

Lösningar för modern drifts hantering skapar en multimoln-vy med åtgärder. Till gångar som hanteras med följande metod tips kan leva i molnet, i ett befintligt Data Center eller till och med i en konkurrerande moln leverantör. För närvarande innehåller ramverket två metodtips som referens för att vägleda driftshantering till mognad i molnet:

- [Hantering av Azure-Server](./azure-server-management/index.md): den medföljande guiden för att ta med de molnbaserade verktyg och tjänster som krävs för att hantera åtgärder.
- [Hybrid övervakning](./monitor/index.md): många kunder har redan gjort en betydande investering i System Center Operations Manager. Den här guiden för hybridövervakning hjälper dessa kunder att jämföra och kontrastera de molnbaserade rapporteringsverktygen med Operations Manager-verktyg. Den här jämförelsen gör det lättare att bestämma vilka verktyg som ska användas för driftshantering.

## <a name="cloud-operations"></a>Molnåtgärder

Båda dessa bästa metoder bygger mot en framtida tillstånds metod för Operations Management.

![Hantera metoder i moln införande ramverket](../_images/manage/caf-manage.png)

**Affärs justering:** I den hantera metodiken klassificeras alla arbets belastningar efter allvarlighets grad och affärs värde. Denna klassificering kan sedan mätas via en konsekvensanalys som beräknar det förlorade värde som är associerat med prestandaförsämring eller avbrott i verksamheten. Med hjälp av den praktiska intäktsinverkan kan teamet för molndrift arbeta med verksamheten för att upprätta ett åtagande som balanserar kostnad och prestanda.

**Moln drifts discipliner:** När verksamheten är justerad är det mycket enklare att spåra och rapportera om de olika disciplinerna för moln åtgärder för varje arbets belastning. Beslutsfattande inom varje område kan sedan konverteras till åtagandevillkor som är enkla för verksamheten att förstå. Denna samarbetsmetod gör att affärsintressenten blir en partner vad gäller att hitta rätt balans mellan kostnad och prestanda.

- **Inventering och synlighet:** Drifts hantering kräver minst ett sätt att inventera till gångar och att skapa insyn i körnings tillstånd för varje till gång.
- **Operativa krav:** Regelbundet hantering av konfiguration, storlek, kostnad och prestanda för till gångar är nyckel för att underhålla prestanda förväntningarna.
- **Skydda och återställa:** Minimera drift avbrott och påskynda återställningen av varje hjälp för att undvika prestanda förluster och inkomst påverkan. Identifiering och återställning är viktiga aspekter inom det här området.
- **Plattforms åtgärder:** Alla IT-miljöer innehåller en uppsättning ofta använda plattformar. Dessa plattformar kan omfatta datalager såsom SQL Server eller HDInsights. Andra vanliga plattformar kan omfatta containerlösningar såsom Kubernetes eller AKS. Oavsett plattformarna fokuserar mognad i plattformsdriften på anpassning av verksamheter som baseras på hur dessa vanliga plattformar distribueras, konfigureras och används av arbetsbelastningar.
- **Arbets belastnings åtgärder:** På den högsta nivån av drifts förfallo tid kan moln drifts grupper finjustera åtgärder för arbets belastningar som är viktiga för företagets framgång. För dessa arbetsbelastningar med hög allvarlighetsgrad kan tillgängliga data hjälpa till med automatisering av åtgärder, storleksbestämning eller skydd av arbetsbelastningar baserat på deras användning.

Ytterligare vägledning som [ramverket för design granskning (kod tips: Cloud design-principer)](https://docs.microsoft.com/azure/architecture/reliability) kan hjälpa till att fatta detaljerade arkitektoniska beslut om varje arbets belastning, inom ämnes områden ovan.

I det här avsnittet om Cloud Adoption Framework tar vi upp var och en av dessa aspekter som bidrar till molnimplementeringen i din organisation.
