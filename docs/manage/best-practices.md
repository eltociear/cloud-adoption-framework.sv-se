---
title: Introduktion till åtgärdshantering
description: Förstå drift hantering i moln införande ramverket.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: overview
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 9fbdeccc3ed1c1acb516f9aceadc3d8dc8732030
ms.sourcegitcommit: 35d01bccc8ecbec38f6247a065a309ec691ca810
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 02/14/2020
ms.locfileid: "77213617"
---
# <a name="establish-operational-management-practices-in-the-cloud"></a>Upprätta operativa hanterings metoder i molnet

Molnimplementering är en katalysator för att skapa affärsvärde. Dock realiseras verkligt affärsvärde genom löpande, stabil drift av de tekniktillgångar som distribueras till molnet. I det här avsnittet av moln implementerings ramverket får du hjälp att gå igenom olika över gångar i den operativa hanteringen i molnet.

## <a name="actionable-best-practices"></a>Användbara metodtips

Lösningar för modern drifts hantering skapar en multimoln-vy med åtgärder. Till gångar som hanteras med följande metod tips kan leva i molnet, i ett befintligt Data Center eller till och med i en konkurrerande moln leverantör. För närvarande innehåller ramverket två metod tips för att hjälpa drifts hanteringens förfallo tid i molnet:

- [Azure Server Management](./azure-server-management/index.md): en onboarding-guide för att införliva de molnbaserade verktyg och tjänster som krävs för att hantera åtgärder.
- [Hybrid övervakning](./monitor/index.md): många kunder har redan gjort en betydande investering i System Center Operations Manager. För dessa kunder kan den här hand boken till hybrid övervakning hjälpa dem att jämföra och kontrasta de molnbaserade rapporterings verktygen med Operations Manager verktyg. Den här jämförelsen gör det lättare att bestämma vilka verktyg som ska användas för drifts hantering.

## <a name="cloud-operations"></a>Molnåtgärder

Båda dessa metod tips bygger på en metod för framtida tillstånd för Operations Management, som illustreras i följande diagram:

![Hantera metoder i moln införande ramverket](../_images/manage/caf-manage.png)

**Affärs justering:** I den hantera metodiken klassificeras alla arbets belastningar efter allvarlighets grad och affärs värde. Denna klassificering kan sedan mätas via en konsekvensanalys som beräknar det förlorade värde som är associerat med prestandaförsämring eller avbrott i verksamheten. Med hjälp av den praktiska intäktsinverkan kan teamet för molndrift arbeta med verksamheten för att upprätta ett åtagande som balanserar kostnad och prestanda.

**Moln drifts discipliner:** När verksamheten har justerats är det mycket enklare att spåra och rapportera om de olika disciplinerna för moln åtgärder för varje arbets belastning. Att fatta beslut längs varje disciplin kan sedan konverteras till åtagande villkor som enkelt kan förstås av verksamheten. Denna samarbetsmetod gör att affärsintressenten blir en partner vad gäller att hitta rätt balans mellan kostnad och prestanda.

- **Inventering och synlighet:** Drifts hantering kräver minst ett sätt att inventera till gångar och att skapa insyn i körnings tillstånd för varje till gång.
- **Operativa krav:** Regelbunden hantering av konfiguration, storlek, kostnad och prestanda för till gångar är nyckeln till att bibehålla prestanda förväntningarna.
- **Skydda och återställa:** Att minimera drift avbrott och påskynda återställningen hjälper företaget att undvika prestanda förluster och negativ inkomst påverkan. Identifiering och återställning är viktiga aspekter inom det här området.
- **Plattforms åtgärder:** Alla IT-miljöer innehåller en uppsättning ofta använda plattformar. Dessa plattformar kan omfatta data lager som SQL Server eller Azure HDInsight. Andra vanliga plattformar kan omfatta behållar lösningar som Azure Kubernetes service (AKS). Oavsett plattform, fokuserar plattforms drifts förfallo tiden på att anpassa åtgärder baserat på hur de gemensamma plattformarna distribueras, konfigureras och används av arbets belastningar.
- **Arbets belastnings åtgärder:** På den högsta nivån av drifts förfallo tid kan moln drifts grupper justera åtgärder för arbets belastningar som är viktiga för företagets framgång. För dessa arbets belastningar med hög allvarlighets grad kan tillgängliga data hjälpa till med automatisering av reparation, storlek eller skydd av arbets belastningar baserat på deras användning.

Ytterligare vägledning, till exempel [ramverket för design granskning (kod namn: principer för moln design)](https://docs.microsoft.com/azure/architecture/framework/resiliency/overview), kan hjälpa dig att fatta detaljerade arkitektoniska beslut om varje arbets belastning, inom de tidigare beskrivna ämnes områden.

Det här avsnittet av ramverket för moln införande bygger på var och en av de föregående ämnena för att främja mogna moln åtgärder i din organisation.
