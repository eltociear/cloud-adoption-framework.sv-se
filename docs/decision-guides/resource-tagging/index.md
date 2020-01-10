---
title: Beslutsguide för namngivning och taggning av resurser
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Läs mer om resursorganisering och taggning som en central tjänst i Azure-migreringar.
author: alexbuckgit
ms.author: abuck
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.custom: governance
ms.openlocfilehash: c62e087372d21a3883c90425b31e1c5ff9bfd2fb
ms.sourcegitcommit: 390b374dc7af4c4b85ef9fcb381c7c1bc6076ac7
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 01/10/2020
ms.locfileid: "75868028"
---
# <a name="resource-naming-and-tagging-decision-guide"></a>Beslutsguide för namngivning och taggning av resurser

Organisering av molnbaserade resurser är en av de viktigaste uppgifterna för IT-avdelningen, såvida du inte bara har enkla distributioner. Det finns tre primära syften med resursorganisering:

- **Resurshantering:** Dina IT-team behöver snabbt hitta resurser som är associerade med specifika arbetsbelastningar, miljöer, ägarskapsgrupper eller annan viktig information. Resursorganisering är mycket viktigt för att tilldela organisationsroller och åtkomstbehörigheter för resurshantering.
- **Automation:** Utöver att göra det enklare för IT-avdelningen att hantera resurser gör rätt organisationsschema att du kan dra nytta av automation som en del av resursskapande, driftsövervakning och skapande av DevOps-processer.
- **Redovisning:** Att göra affärsgrupper medvetna om förbrukning av molnresurser kräver att IT-avdelningen förstår vilka arbetsbelastningar och team som använda vilka resurser. För att stödja metoder såsom återbetalning och showback-redovisning behöver molnresurser organiseras så att det speglar ägarskap och användning.

## <a name="tagging-decision-guide"></a>Beslutsguide för taggning

![Taggningsalternativ ordnade från minst till mest komplext, inriktat med direktlänkar nedan](../../_images/decision-guides/decision-guide-resource-tagging.png)

Hoppa till: [Namngivningskonventioner för baslinjen](#baseline-naming-conventions) | [Mönster för resurstaggning](#resource-tagging-patterns) | [Läs mer](#learn-more)

Din taggningsmetod kan vara enkel eller komplex, med betoning som kan sträcka sig från att stödja IT-team som hanterar molnarbetsbelastningar till att integrera information som rör alla aspekter av verksamheten.

Ett IT-inriktad taggningsfokus, till exempel taggning baserat på arbetsbelastning, funktion eller miljö, minskar komplexiteten med att övervaka tillgångar och gör hanteringsbeslut som baseras på driftskrav mycket enklare.

Taggningsscheman som omfattar ett affärsinriktat fokus, till exempel redovisning, företagsägarskap eller affärskritikalitet kan kräva större tidsinvestering för att skapa taggningsstandarder som speglar affärsintressen och upprätthåller de standarderna över tid. Resultatet av den här processen är dock ett taggningssystem som ger förbättrade möjligheter att ta med kostnader för och värdet av IT-tillgångar i beräkningen för den övergripande verksamheten. Den här associationen av en tillgångs affärsvärde med dess driftskostnad är ett av de första stegen i att ändra kostnadsställets uppfattning om IT i den övergripande organisationen.

## <a name="baseline-naming-conventions"></a>Namngivningskonventioner för baslinjen

En standardiserad namngivningskonvention är startpunkten för att organisera dina molnhanterade resurser. Med ett korrekt strukturerat namngivningssystem kan du snabbt identifiera resurser för både hanterings- och redovisningsändamål. Om du har befintliga IT-namngivningskonventioner i andra delar av organisationen bör du överväga huruvida dina namngivningskonventioner för moln ska riktas in med dem eller om du bör upprätta separata molnbaserade standarder.

Observera även att olika Azure-resurstyper har olika [namngivningskrav](../../ready/azure-best-practices/naming-and-tagging.md). Dina namngivningskonventioner måste vara kompatibla med dessa namngivningskrav.

## <a name="resource-tagging-patterns"></a>Mönster för resurstaggning

För organisationer som är mer avancerade än vad endast en konsekvent namngivningskonvention kan tillhandahålla har molnplattformar stöd för möjligheten att tagga resurser.

*Taggar* är metadataelement som är kopplade till resurser. Taggar består av par av nyckel-/värdesträngar. De värden som du inkluderar i dessa par är upp till dig, men tillämpningen av en konsekvent uppsättning globala taggar, som en del av en omfattande namngivnings- och taggningsprincip, är en viktig del av en övergripande styrningsprincip.

Som en del av planeringsprocessen använder du följande frågor för att avgöra vilken typ av information dina resurstaggar behöver stödja:

- Behöver dina namngivnings- och taggningsprinciper integreras med befintliga namngivnings- och organisationsprinciper i företaget?
- Kommer du att implementera ett återbetalnings- eller showback-redovisningssystem? Kommer du att behöva associera resurser med redovisningsinformation för avdelningar, affärsgrupper och team i närmare detalj än vad som går med en enkel uppdelning på prenumerationsnivå?
- Behöver taggning representera information såsom krav för regelefterlevnad för en resurs? Vad gäller för driftsinformation som drifttidskrav, korrigeringsscheman eller säkerhetskrav?
- Vilka taggar behövs för alla resurser baserat på en central IT-princip? Vilka taggar är valfria? Tillåts enskilda team att implementera sina egna anpassade taggningsscheman?

De vanliga taggningsmönster som anges nedan ger exempel på hur taggar kan användas för att organisera molntillgångar. Dessa mönster är inte avsedda att vara exklusiva och kan användas parallellt, vilket ger flera olika sätt att organisera resurser baserat på företagets behov.

<!-- markdownlint-disable MD033 -->

| Taggtyp | Exempel | Beskrivning |
|-----|-----|-----|
| Funktionell            | app = catalogsearch1 <br/>tier = web <br/>webserver = apache<br/>env = prod <br/>env = staging <br/>env = dev                 | Kategorisera resurser i förhållande till deras syfte i en arbetsbelastning, vilken miljö de har distribuerats till eller andra funktioner och driftsdetaljer.                                 |
| Klassificering        | confidentiality=private<br/>sla = 24hours                                 | Klassificerar en resurs enligt hur den används och vilka principer som gäller för den                               |
| Redovisning            | department = finance <br/>project = catalogsearch <br/>region = northamerica | Gör att resursen kan associeras med specifika grupper i en organisation för faktureringsändamål |
| Partnerskap           | owner = jsmith <br/>contactalias = catsearchowners<br/>stakeholders = user1;user2;user3<br/>                       | Ger information om vilka personer (utanför IT) som är relaterade eller på annat sätt berörs av resursen                      |
| Syfte               | businessprocess=support<br/>businessimpact=moderate<br/>revenueimpact=high   | Riktar in resurser till affärsfunktioner i syfte att bättre stödja investeringsbeslut  |

<!-- markdownlint-enable MD033 -->

## <a name="learn-more"></a>Läs mer

Mer information om namngivning och taggning i Azure finns här:

- [Namngivningskonventioner för Azure-resurser](https://docs.microsoft.com/azure/architecture/best-practices/resource-naming). Läs den här vägledningen för rekommenderade namnkonventioner för Azure-resurser.
- [Använd taggar för att organisera Azure-resurser](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags). Du kan tillämpa taggar i Azure på nivå för såväl resursgrupp som enskild resurs, vilket ger dig flexibilitet vad gäller kornighet för alla redovisningsrapporter baserat på tillämpade taggar.

## <a name="next-steps"></a>Nästa steg

Resurstaggning är bara en av huvudkomponenterna för infrastruktur som kräver arkitektoniska beslut under en process för att implementera moln. Gå till [översikten över beslutsguider](../index.md) om vill veta mer om alternativa mönster eller modeller som används vid utformningsbeslut för andra typer av infrastrukturer.

> [!div class="nextstepaction"]
> [Beslutsguider för arkitektur](../index.md)
