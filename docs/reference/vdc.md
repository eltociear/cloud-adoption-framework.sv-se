---
title: Azure Virtual Datacenter
description: Resurser för Microsoft Azure Virtual Datacenter
author: tracsman
ms.author: jonor
ms.date: 06/12/2019
ms.topic: landing-page
ms.service: cloud-adoption-framework
ms.subservice: reference
keywords: Azure
layout: LandingPage
ms.openlocfilehash: 39cb6ac3c31873431206d8c6c525c9ce3467653f
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/16/2019
ms.locfileid: "71027051"
---
# <a name="azure-virtual-datacenter-and-the-enterprise-control-plane"></a>Azure Virtual Datacenter och företagskontrollplanen

Azure Virtual Datacenter är en metod för att få ut mesta möjliga av funktionerna i Azure-molnplattformen samtidigt som du följer dina befintliga principer för säkerhet och nätverk. När IT-organisationer och affärsenheter distribuerar företagsarbetsbelastningar till molnet måste de hitta en balans mellan styrning och smidig utveckling. Azure Virtual Datacenter erbjuder modeller för att få balans med fokus på styrning.

## <a name="resources"></a>Resurser

<!-- markdownlint-disable MD033 -->

<table>
<tr>
    <td style="width: 64px; vertical-align: middle;"><a href="https://aka.ms/VDC/Concepts"><img src="../_images/vdc/virtual-datacenter.svg" alt="Virtual Datacenter e-book" /></a></td>
    <td>
        <h3><a href="https://aka.ms/VDC/Concepts">Azure Virtual Datacenter: Koncept</a></h3>
        <p>Den här e-boken handlar om hur du distribuerar företagsbelastningar till Azure-molnplattformen och samtidigt följer dina befintliga principer för säkerhet och nätverk.</p>
    </td>
</tr>
<tr>
    <td style="width: 64px; vertical-align: middle;"><a href="./networking-vdc.md"><img src="../_images/vdc/vdc-network.png" alt="Network Perspective" /></a></td>
    <td>
        <h3><a href="./networking-vdc.md">Azure Virtual Datacenter: Ett nätverksperspektiv</a></h3>
        <p>Den här onlineartikeln innehåller en översikt över nätverksmönster och -designer som kan användas för att lösa arkitekturproblemen med skala, prestanda och säkerhet som många kunder står inför när de överväger att flytta helt till molnet.</p>
    </td>
</tr>
<tr>
    <td style="width: 64px; vertical-align: middle;"><a href="https://aka.ms/VDC/Lift"><img src="../_images/vdc/vdc-lift-and-shift.png" alt="Lift and Shift Guide" /></a></td>
    <td>
        <h3><a href="https://aka.ms/VDC/Lift">Azure Virtual Datacenter: Lift and shift-vägledning</a></h3>
        <p>I den här dokumentationen beskrivs den process som företags IT-personal och beslutsfattare kan använda för att identifiera och planera migreringen av program och servrar till Azure med hjälp av en ”lift and shift”-metod. Då minimeras eventuella ytterligare utvecklingskostnader samtidigt som molnvärdalternativ optimeras.</p>
    </td>
</tr>
<tr>
    <td style="width: 64px; vertical-align: middle;"><a href="https://aka.ms/VDC/Deck"><img src="../_images/vdc/vdc-deck.png" alt="Presentation Deck" /></a></td>
    <td>
        <h3><a href="https://aka.ms/VDC/Deck">Azure Virtual Datacenter: Presentation </a></h3>
        <p>Den här presentationen utforskar vägledningen och verktygen i Azure Virtual Datacenter. Den tar upp VDC-målen, kundfaktorer, Azure-regioner, elementen i en VDC-automatisering, industrialiserade och betrodda Azure-VDC, och avslutar med en åtgärdsplan kring CIO-vägledning. Den innehåller även information om support och utbildning.</p>
    </td>
</tr>
</table>

<!-- markdownlint-enable MD033 -->

<!-- markdownlint-disable MD026 -->

## <a name="what-is-the-azure-virtual-datacenter"></a>Vad är Azure Virtual Datacenter?

Distribution av arbetsbelastningar till molnet leder till behovet av att skapa och bibehålla förtroende i molnet i samma grad som du har förtroende för dina befintliga datacenter. Den första modellen av Azure Virtual Datacenter-vägledningen är avsedd att överbrygga det behovet genom en låst metod för virtuella infrastrukturer. Den här metoden passar inte alla. Den är särskilt utformad för att vägleda företags IT-grupper i att utöka sin lokala infrastruktur till det offentliga Azure-molnet. Vi kallar den här metoden för utökningsmodellen för betrodda datacenter. Med tiden kommer flera andra modeller att erbjudas, bland annat sådana som möjliggör säker Internetåtkomst direkt från ett virtuellt datacenter.

<!-- markdownlint-disable MD033 -->

<img src="../_images/vdc/vdc-components.svg" alt="Virtual Datacenter components" style="max-width:700px;"/>

<!-- markdownlint-enable MD033 -->

De här fyra komponenterna gör Azure Virtual Datacenter möjligt: identitet, kryptering, programvarudefinierade nätverk och efterlevnad (inklusive loggar och rapportering).

I Azure Virtual Datacenter-modellen kan du tillämpa isoleringsprinciper, göra molnet mer likt de fysiska datacenter du känner till och uppnå de nivåer av säkerhet och förtroende du behöver. Fyra komponenter som alla företags IT-team skulle känna igen gör det möjligt: programvarudefinierade nätverk, kryptering, identitetshantering och Azure-plattformens underliggande efterlevnadsstandarder och -certifieringar. De fyra är avgörande för att göra ett virtuellt datacenter till en betrodd utökning av din befintliga infrastrukturinvestering.

Fortsätt att läsa e-boken om [begrepp för Azure Virtual Datacenter](https://azure.microsoft.com/resources/azure-virtual-datacenter).
