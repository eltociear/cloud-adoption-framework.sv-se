---
title: Säkerhets bas linje verktyg i Azure
description: Se hur Azures inbyggda verktyg kan hjälpa mogna principer och processer som stöder ämnes linjen för styrning av säkerhets bas linjer.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: db3be7ca7577cb8b42f4efc556b88b25d6e1f23e
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/31/2020
ms.locfileid: "80425836"
---
# <a name="security-baseline-tools-in-azure"></a>Säkerhets bas linje verktyg i Azure

[Säkerhets bas linjen](./index.md) är en av de [fem disciplinerna i moln styrning](../governance-disciplines.md). Den här disciplinen fokuserar på sätt att etablera principer som skyddar nätverket, till gångar och viktigast av de data som kommer att finnas i en moln leverantörs lösning. I den fem ämnes gruppen i moln styrning inbegriper säkerhets bas linjen klassificering av den digitala fastigheten och data. Det omfattar också dokumentation om risker, affärs toleranser och strategier för att minska säkerheten för data, till gångar och nätverk. Från ett tekniskt perspektiv inkluderar denna disciplin också inblandning i beslut om [kryptering](../../decision-guides/encryption/index.md), [nätverks krav](../../decision-guides/software-defined-network/index.md), [hybrid identitets strategier](../../decision-guides/identity/index.md)och verktyg för att [Automatisera verk](../../decision-guides/policy-enforcement/index.md) ställandet av säkerhets principer i [resurs grupper](../../decision-guides/resource-consistency/index.md).

Följande lista över Azure-verktyg kan användas för att mogna de principer och processer som stöder säkerhets bas linjen.

| Verktyg | [Azure Portal](https://azure.microsoft.com/features/azure-portal) och [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview)  | [Azure Key Vault](https://docs.microsoft.com/azure/key-vault)  | [Azure AD](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-whatis) | [Azure Policy](https://docs.microsoft.com/azure/governance/policy/overview) | [Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-intro) | [Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/overview) |
|------------------------------------------------------------|---------------------------------|-----------------|----------|--------------|-----------------------|---------------|
| Tillämpa åtkomst kontroller på resurser och skapa resurser   | Ja                             | Nej              | Ja      | Nej           | Nej                    | Nej            |
| Säkra virtuella nätverk                                    | Ja                             | Nej              | Nej       | Ja          | Nej                    | Nej            |
| Kryptera virtuella enheter                                     | Nej                              | Ja             | Nej       | Nej           | Nej                    | Nej            |
| Kryptera PaaS-lagring och databaser                         | Nej                              | Ja             | Nej       | Nej           | Nej                    | Nej            |
| Hantera hybrid identitets tjänster                            | Nej                              | Nej              | Ja      | Nej           | Nej                    | Nej            |
| Begränsa tillåtna resurs typer                         | Nej                              | Nej              | Nej       | Ja          | Nej                    | Nej            |
| Framtvinga geo-regionala begränsningar                          | Nej                              | Nej              | Nej       | Ja          | Nej                    | Nej            |
| Övervaka säkerhets hälsa för nätverk och resurser          | Nej                              | Nej              | Nej       | Nej           | Ja                   | Ja           |
| Identifiera skadlig aktivitet                                  | Nej                              | Nej              | Nej       | Nej           | Ja                   | Ja           |
| Förebyggande syfte identifiera sårbarheter                        | Nej                              | Nej              | Nej       | Nej           | Ja                   | Nej            |
| Konfigurera säkerhets kopiering och haveri beredskap                     | Ja                             | Nej              | Nej       | Nej           | Nej                    | Nej            |

En fullständig lista över Azures säkerhets verktyg och tjänster finns i [säkerhets tjänster och tekniker som är tillgängliga i Azure](https://docs.microsoft.com/azure/security/azure-security-services-technologies).

Det är också vanligt att kunderna använder verktyg från tredje part för att under lätta aktiviteter för säkerhets bas linjen. Mer information finns i artikeln [integrera säkerhetslösningar i Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-partner-integration).

Förutom säkerhets verktygen innehåller [Microsoft Trust Center](https://www.microsoft.com/trustcenter/guidance/risk-assessment) omfattande vägledning, rapporter och relaterad dokumentation som kan hjälpa dig att utföra riskbedömningar som en del av din planerings process för migrering.
