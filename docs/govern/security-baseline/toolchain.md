---
title: Säkerhets bas linje verktyg i Azure
description: Förklaring till de verktyg som kan under lätta förbättrad säkerhets bas linje i Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 122e0774912fdc65cd9c8daff0bd48b679634868
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 01/28/2020
ms.locfileid: "76808812"
---
# <a name="security-baseline-tools-in-azure"></a>Säkerhets bas linje verktyg i Azure

[Säkerhets bas linjen](./index.md) är en av de [fem disciplinerna i moln styrning](../governance-disciplines.md). Den här disciplinen fokuserar på sätt att etablera principer som skyddar nätverket, till gångar och viktigast av de data som kommer att finnas i en moln leverantörs lösning. I den fem ämnes gruppen i moln styrning inbegriper säkerhets bas linjen klassificering av den digitala fastigheten och data. Det omfattar också dokumentation om risker, affärs toleranser och strategier för att minska säkerheten för data, till gångar och nätverk. Från ett tekniskt perspektiv inkluderar denna disciplin också inblandning i beslut om [kryptering](../../decision-guides/encryption/index.md), [nätverks krav](../../decision-guides/software-defined-network/index.md), [hybrid identitets strategier](../../decision-guides/identity/index.md)och verktyg för att [Automatisera verk](../../decision-guides/policy-enforcement/index.md) ställandet av säkerhets principer i [resurs grupper](../../decision-guides/resource-consistency/index.md).

Följande lista över Azure-verktyg kan användas för att mogna de principer och processer som stöder säkerhets bas linjen.

| Verktyg | [Azure Portal](https://azure.microsoft.com/features/azure-portal) och [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview)  | [Azure Key Vault](https://docs.microsoft.com/azure/key-vault)  | [Azure AD](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-whatis) | [Azure Policy](https://docs.microsoft.com/azure/governance/policy/overview) | [Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-intro) | [Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/overview) |
|------------------------------------------------------------|---------------------------------|-----------------|----------|--------------|-----------------------|---------------|
| Tillämpa åtkomst kontroller på resurser och skapa resurser   | Ja                             | Inga              | Ja      | Inga           | Inga                    | Inga            |
| Säkra virtuella nätverk                                    | Ja                             | Inga              | Inga       | Ja          | Inga                    | Inga            |
| Kryptera virtuella enheter                                     | Inga                              | Ja             | Inga       | Inga           | Inga                    | Inga            |
| Kryptera PaaS-lagring och databaser                         | Inga                              | Ja             | Inga       | Inga           | Inga                    | Inga            |
| Hantera hybrid identitets tjänster                            | Inga                              | Inga              | Ja      | Inga           | Inga                    | Inga            |
| Begränsa tillåtna resurs typer                         | Inga                              | Inga              | Inga       | Ja          | Inga                    | Inga            |
| Framtvinga geo-regionala begränsningar                          | Inga                              | Inga              | Inga       | Ja          | Inga                    | Inga            |
| Övervaka säkerhets hälsa för nätverk och resurser          | Inga                              | Inga              | Inga       | Inga           | Ja                   | Ja           |
| Identifiera skadlig aktivitet                                  | Inga                              | Inga              | Inga       | Inga           | Ja                   | Ja           |
| Förebyggande syfte identifiera sårbarheter                        | Inga                              | Inga              | Inga       | Inga           | Ja                   | Inga            |
| Konfigurera säkerhets kopiering och haveri beredskap                     | Ja                             | Inga              | Inga       | Inga           | Inga                    | Inga            |

En fullständig lista över Azures säkerhets verktyg och tjänster finns i [säkerhets tjänster och tekniker som är tillgängliga i Azure](https://docs.microsoft.com/azure/security/azure-security-services-technologies).

Det är också vanligt att kunderna använder verktyg från tredje part för att under lätta aktiviteter för säkerhets bas linjen. Mer information finns i artikeln [integrera säkerhetslösningar i Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-partner-integration).

Förutom säkerhets verktygen innehåller [Microsoft Trust Center](https://www.microsoft.com/trustcenter/guidance/risk-assessment) omfattande vägledning, rapporter och relaterad dokumentation som kan hjälpa dig att utföra riskbedömningar som en del av din planerings process för migrering.
