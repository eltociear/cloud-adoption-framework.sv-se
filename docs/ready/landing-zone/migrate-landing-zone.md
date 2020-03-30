---
title: Distribuera en landningszon i Azure
description: Lär dig att distribuera en landningszon i Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/25/2020
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: ed7e64e2c18187621f2c7703b5b1d9f2056997ea
ms.sourcegitcommit: 1a4b140f09bdaa141037c54a4a3b5577cda269db
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/30/2020
ms.locfileid: "80392635"
---
<!-- cSpell:ignore vCPUs jumpbox -->

# <a name="deploy-a-migration-landing-zone"></a>Distribuera en landningszon för migrering

Termen *landingszon för migrering* används för att beskriva en miljö som har etablerats och förberetts för att fungera som värd för arbetsbelastningar som migreras från en lokal miljö till Azure.

## <a name="deploy-the-first-landing-zone"></a>Distribuera den första landnings zonen

Innan du använder ritningens landnings zon skiss i moln implementerings ramverket bör du läsa följande antaganden, beslut och implementerings anvisningar. Om den här vägledningen överensstämmer med den önskade moln implementerings planen kan du distribuera [landnings zonns skiss](https://docs.microsoft.com/azure/governance/blueprints/samples/caf-migrate-landing-zone/index) med hjälp av [distributions stegen][deploy-sample].

> [!div class="nextstepaction"]
> [Distribuera skiss exemplet][deploy-sample]

## <a name="assumptions"></a>Antaganden

Den här inledande landnings zonen innehåller följande antaganden eller begränsningar. Om dessa antaganden överensstämmer med dina begränsningar kan du använda skissen för att skapa din första landningszon. Skissen kan också utökas för att skapa en landningszonskiss som uppfyller dina unika begränsningar.

- **Prenumerations begränsningar:** Den här antagande ansträngningen förväntas inte överskrida [prenumerations gränserna](https://docs.microsoft.com/azure/azure-subscription-service-limits).
- **Kompatibilitet:** Det behövs inga krav från tredje part för efterlevnad i denna landnings zon.
- **Arkitektur komplexitet:** Arkitektur komplexitet kräver inte ytterligare produktions prenumerationer.
- **Delade tjänster:** Det finns inga befintliga delade tjänster i Azure som kräver att den här prenumerationen behandlas som en eker i en hubb och eker-arkitektur.
- **Begränsat produktions omfång:** Denna landnings zon kan potentiellt vara värd för produktions arbets belastningar. Det är dock inte en lämplig miljö för känsliga data eller verksamhets kritiska arbets belastningar.

Om dessa antaganden överensstämmer med dina befintliga implementerings behov kan den här skissen vara en utgångs punkt för att skapa din landnings zon.

## <a name="decisions"></a>Beslut

Följande beslut speglas i skissen för landningszonen.

| Komponent                    | Beslut                                                                                         | Alternativa metoder                                                                                                                                                                                                                                                                |
|------------------------------|---------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Migreringsverktyg              | Azure Site Recovery distribueras och ett Azure Migrate-projekt skapas.                | [Beslutsguide för migreringsverktyg](../../decision-guides/migrate-decision-guide/index.md)                                                                                                                                                                                               |
| Loggning och övervakning       | Arbetsytan Operational Insights och ett diagnostiskt lagringskonto kommer att tillhandahållas.                |                                                                                                                                                                                                                                                                                       |
| Nätverk                      | Ett virtuellt nätverk skapas med undernät för gateway, brandvägg, jumpbox och landningszon.  | [Nätverksbeslut](../considerations/networking-options.md)                                                                                                                                                                                                                       |
| Identitet                     | Vi förutsätter att prenumerationen redan är associerad med en instans av Azure Active Directory. | [Metodtips för identitetshantering](https://docs.microsoft.com/azure/security/azure-security-identity-management-best-practices?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json) |
| Princip                       | Skissen förutsätter för närvarande att inga Azure-principer ska tillämpas.                        |                                                                                                                                                                                                                                                                                       |
| Prenumerationsdesign          | Saknas – utformad för en enda produktionsprenumeration.                                              | [Skapa första prenumerationer](../azure-best-practices/initial-subscriptions.md)                                                                                                                                                                                                      |
| Resursgrupper              | Saknas – utformad för en enda produktionsprenumeration.                                              | [Skala prenumerationer](../azure-best-practices/scale-subscriptions.md)                                                                                                                                                                                                                 |
| Hanteringsgrupper            | Saknas – utformad för en enda produktionsprenumeration.                                              | [Organisera och hantera prenumerationer](../azure-best-practices/organize-subscriptions.md)                                                                                                                                                                                                |
| Data                         | Ej tillämpligt                                                                                               | [Välj rätt SQL Server alternativ i Azure](https://docs.microsoft.com/azure/sql-database/sql-database-paas-vs-sql-server-iaas) och [Azure Data Store vägledning](https://docs.microsoft.com/azure/architecture/guide/technology-choices/data-store-overview)                       |
| Storage                      | Ej tillämpligt                                                                                               | [Riktlinjer för Azure Storage](../considerations/storage-options.md)                                                                                                                                                                                                                        |
| Standarder för namngivning och taggning | Ej tillämpligt                                                                                               | [Metodtips för namngivning och taggning](../azure-best-practices/naming-and-tagging.md)                                                                                                                                                                                                    |
| Kostnadshantering              | Ej tillämpligt                                                                                               | [Spåra kostnader](../azure-best-practices/track-costs.md)                                                                                                                                                                                                                              |
| Compute                      | Ej tillämpligt                                                                                               | [Compute-alternativ](../considerations/compute-options.md)                                                                                                                                                                                                                               |

## <a name="customize-or-deploy-a-landing-zone"></a>Anpassa eller distribuera en landnings zon

Läs mer och ladda ned ett referens exempel på ritningen migrera landnings zon för distribution eller anpassning från [Azure Blueprint exempel][deploy-sample].

> [!div class="nextstepaction"]
> [Distribuera skiss exemplet][deploy-sample]

Information om anpassningar som ska göras till den här skissen eller den resulterande landnings zonen finns i avsnittet om [landnings zoner](../considerations/index.md).

## <a name="next-steps"></a>Nästa steg

När du har distribuerat din första landnings zon är du redo att [expandera din landnings zon](../considerations/index.md)

> [!div class="nextstepaction"]
> [Expandera din landnings zon](../considerations/index.md)

<!-- links -->

[deploy-sample]: https://docs.microsoft.com/azure/governance/blueprints/samples/caf-migrate-landing-zone/deploy
