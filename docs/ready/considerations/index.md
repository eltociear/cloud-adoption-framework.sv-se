---
title: Azure-landingzon – att tänka på
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Lär dig hur en landningszon fungerar som den grundläggande byggstenen i alla typer av miljöer för molnimplementering.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/20/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: f9926fd59133303960338ac4e8b45cc9007dad51
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/06/2019
ms.locfileid: "70816235"
---
# <a name="landing-zone-considerations"></a>Landingzon – att tänka på

En landningszon är den grundläggande byggstenen i alla typer av miljöer för molnimplementering. Termen *landningszon* avser en miljö som etablerats och förberetts för att köra arbetsbelastningar i en molnmiljö som Azure. En fullt fungerande landningszon är den sista slutprodukten för alla iterationer av Cloud Adoption Framework-beredskapsmetoden.

![Landingzon – att tänka på](../../_images/ready/landing-zone-considerations.png)

I den här bilden ser du de viktigaste sakerna att tänka på när du implementerar distribution i en landningszon. Övervägandena kan delas in i tre kategorier eller typer: värdskap, Azure-grunder och styrning.

## <a name="hosting-considerations"></a>Värdskapsöverväganden

Alla landningszoner tillhandahåller en struktur för olika värdalternativ. Strukturen skapas explicit via styrningskontroller eller organiskt genom de tjänster som används i landningszonen. I följande artiklar får du hjälp att fatta beslut som sedan återspeglas i skissen eller andra automatiserade skript som skapar landningszonen:

- **[Beräkningsbeslut](./compute-decisions.md)** . Du kan göra driften mindre komplicerad genom att anpassa beräkningsalternativen till landningszonens syfte. Det här beslutet kan tillämpas med hjälp av verktygskedjor för automation som Azure Policy-initiativ och skisser för landningszoner.
- **[Lagringsbeslut](./storage-guidance.md)** . Välj den Azure Storage-lösning som passar för arbetsbelastningens krav.
- **[Nätverksbeslut](./network-decisions.md)** . Välj de nätverkstjänster, verktyg och arkitekturer som behövs för organisationens arbetsbelastning, styrningen och behovet av anslutningar.
- **[Databasbeslut](./data-decisions.md)** . Avgör vilken databasteknik som passar bäst för dina arbetsbelastningskrav.

## <a name="azure-fundamentals"></a>Grunderna i Azure

Varje landningszon är en del av en bredare lösning för att ordna resurser i en molnmiljö. Grunderna i Azure är organisationens grundläggande byggstenar.

- **[Grundläggande koncept för Azure](./fundamental-concepts.md)** . Lär dig grundläggande begrepp och termer som används när du ska organisera resurser i Azure och hur begreppen är relaterade till varandra.
- **Guide till beslut om organisering av resurser**. När du förstår grunderna så kan du få hjälp att fatta beslut som kommer att forma landningszonen i den här guiden till resursorganisering.

## <a name="governance-considerations"></a>Saker att tänka på i samband med styrning

Cloud Adoption Frameworks styrningsmetodiker upprättar en process för att styra miljön som helhet. Det finns dock många användningsfall där du måste fatta olika styrningsbeslut för olika landningszoner. I många scenarier tillämpas grunderna i styrningen olika för olika landningszoner, även om dessa grunder har etablerats holistiskt. Det här är sant för de första landningszoner som en organisation distribuerar.

I följande artiklar får du hjälp att fatta styrningsrelaterade beslut angående din landningszon. Du kan väga in varje beslut i grunderna för din styrning.

- **Kostnadskrav**. Givet organisationens motiv för att flytta till molnet och de driftsmässiga kraven på miljön så kan du behöva justera kostnadshanteringen för landningszonen.
- **Övervakningsbeslut**. Beroende på de driftsmässiga kraven för landningszonen så kan du distribuera olika övervakningsverktyg. I artikeln om övervakningsbeslut får du hjälp att avgöra vilka verktyg du bör distribuera.
- **Använda rollbaserad åtkomstkontroll**. Azures [rollbaserade åtkomstkontroll (RBAC)](../azure-best-practices/roles.md) ger en detaljerad och gruppbaserad åtkomsthantering för resurser som har organiserats efter användarroller.
- **Policybeslut**. Azure Blueprint-exempel är förberedda efterlevnadsskisser som vart och ett har fördefinierade policyinitiativ. Organisationens policybeslut avgör vilken skiss eller vilket policyinitiativ som passar bäst sett till krav och begränsningar.
- **[Skapa hybridmolnskonsekvens](../../infrastructure/misc/hybrid-consistency.md)** . Skapa hybridmolnlösningar som ger organisationen molnets alla fördelar samtidigt som en del praktiska aspekter av lokal hantering bibehålls.