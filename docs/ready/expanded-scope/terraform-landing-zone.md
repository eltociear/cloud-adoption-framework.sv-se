---
title: Använda terraform för att bygga landnings zoner
description: Lär dig att använda terraform för att skapa en prototyp zon för att distribuera grundläggande loggnings-, redovisnings-och säkerhets funktioner för en Azure-prenumeration.
author: arnaudlh
ms.author: arnaul
ms.date: 10/16/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: 55724c594d75464827350c57e6a371f8876b17a0
ms.sourcegitcommit: 0ea426f2f471eb7310c6f09478be1306cf7bf0d8
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/05/2020
ms.locfileid: "78342934"
---
# <a name="use-terraform-to-build-your-landing-zones"></a>Använd terraform för att bygga landnings zoner

Azure tillhandahåller inbyggda tjänster för att distribuera landnings zoner. Andra verktyg från tredje part kan också hjälpa dig med den här ansträngningen. Ett sådant verktyg som kunder och partners ofta använder för att distribuera landnings zoner är Hashicorp-terraform. Det här avsnittet visar hur du använder en prototyp zon för att distribuera grundläggande loggnings-, redovisnings-och säkerhets funktioner för en Azure-prenumeration.

## <a name="purpose-of-the-landing-zone"></a>Syftet med landnings zonen

Den grundläggande landnings zonen för terraform har en begränsad uppsättning ansvars områden och funktioner för att genomdriva loggning, redovisning och säkerhet. Den här landnings zonen använder standard komponenter som kallas terraform-moduler för att tvinga fram konsekvens mellan resurser som distribueras i miljön.

## <a name="use-standard-modules"></a>Använda standardmoduler

Åter användning av komponenter är en grundläggande princip för infrastruktur som kod. Moduler är instrumentell för att definiera standarder och konsekvens för resurs distribution inom och mellan olika miljöer. Modulerna som används för att distribuera den första landnings zonen är tillgängliga i den officiella [terraform-registret](https://registry.terraform.io/search?q=aztfmod).

## <a name="architecture-diagram"></a>Arkitekturdiagram

Den första landnings zonen distribuerar följande komponenter i din prenumeration:

![Foundation-landnings zon med terraform](../../_images/ready/foundations-terraform-landing-zone.png)

## <a name="capabilities"></a>Funktioner

De komponenter som distribueras och deras syfte är följande:

| Komponent | Ligger |
|---------|---------|
| Resursgrupper | Kärn resurs grupper som behövs för stiftelsen |
| Aktivitets loggning | Granska alla prenumerations aktiviteter och arkivering: </br> – Lagrings konto </br> – Azure Event Hubs |  
| Diagnostikloggning | Alla åtgärds loggar som behålls under ett angivet antal dagar: </br> – Lagrings konto </br> -Event Hubs |
| Log Analytics | Lagrar alla åtgärds loggar </br> Distribuera vanliga lösningar för djupgående program metod tips: </br> - NetworkMonitoring </br> - ADAssessment </br> – ADReplication </br> - AgentHealthAssessment </br> - DnsAnalytics </br> - KeyVaultAnalytics
| Azure Security Center | Mått och aviseringar för säkerhets hygien som skickas till e-post och telefonnummer |

## <a name="use-this-blueprint"></a>Använd den här skissen

Läs igenom följande antaganden, beslut och implementerings vägledning innan du använder Cloud implementation Framework Foundation-zonen.

## <a name="assumptions"></a>Antaganden

Följande antaganden eller begränsningar ansågs när den inledande landnings zonen definierades. Om dessa antaganden överensstämmer med dina begränsningar kan du använda skissen för att skapa din första landningszon. Skissen kan också utökas för att skapa en landningszonskiss som uppfyller dina unika begränsningar.

- **Prenumerations begränsningar:** Den här antagande ansträngningen är osannolik för att överskrida [prenumerations gränserna](https://docs.microsoft.com/azure/azure-subscription-service-limits). Två vanliga indikatorer är ett överskott på 25 000 virtuella datorer eller 10 000 virtuella processorer.
- **Kompatibilitet:** Det behövs inga krav från tredje parts efterlevnad för denna landnings zon.
- **Arkitektur komplexitet:** Arkitektur komplexitet kräver inte ytterligare produktions prenumerationer.
- **Delade tjänster:** Det finns inga befintliga delade tjänster i Azure som kräver att den här prenumerationen behandlas som en eker i en hubb och eker-arkitektur.

Om dessa antaganden matchar din aktuella miljö kan den här skissen vara ett bra sätt att börja skapa din landnings zon.

## <a name="design-decisions"></a>Design beslut

Följande beslut visas i terraform landnings zon:

| Komponent | Beslut | Alternativa metoder |
| --- | --- | --- |
|Loggning och övervakning | Azure Monitor Log Analytics arbets ytan används. Ett diagnostiskt lagrings konto samt Händelsehubben är etablerad. |         |
|Nätverk | N/A-nätverket är implementerat i en annan landnings zon. |[Nätverksbeslut](../considerations/networking-options.md) |
|Identitet | Vi förutsätter att prenumerationen redan är associerad med en instans av Azure Active Directory. | [Metodtips för identitetshantering](https://docs.microsoft.com/azure/security/azure-security-identity-management-best-practices) |
| Princip | Denna landnings zon förutsätter för närvarande att inga Azure-principer ska tillämpas. | |
|Prenumerationsdesign | Saknas – utformad för en enda produktionsprenumeration. | [Skalanpassa prenumerationer](../azure-best-practices/scaling-subscriptions.md) |
| Hanteringsgrupper | Saknas – utformad för en enda produktionsprenumeration. |[Skalanpassa prenumerationer](../azure-best-practices/scaling-subscriptions.md) |
| Resursgrupper | Saknas – utformad för en enda produktionsprenumeration. | [Skalanpassa prenumerationer](../azure-best-practices/scaling-subscriptions.md) |
| Data | Ej tillämpligt | [Välj rätt SQL Server alternativ i Azure](https://docs.microsoft.com/azure/sql-database/sql-database-paas-vs-sql-server-iaas) och [Azure Data Store vägledning](https://docs.microsoft.com/azure/architecture/guide/technology-choices/data-store-overview) |
|Storage|Ej tillämpligt|[Riktlinjer för Azure Storage](../considerations/storage-options.md) |
| Namngivningsregler | När miljön skapas skapas även ett unikt prefix. Resurser som kräver ett globalt unikt namn (till exempel lagrings konton) använder det här prefixet. Det anpassade namnet läggs till med ett slumpmässigt suffix. Tagga användningen bestäms enligt beskrivningen i följande tabell. | [Metodtips för namngivning och taggning](../azure-best-practices/naming-and-tagging.md) |
| Kostnadshantering | Ej tillämpligt | [Spåra kostnader](../azure-best-practices/track-costs.md) |
| Compute | Ej tillämpligt | [Compute-alternativ](../considerations/compute-options.md) |

### <a name="tagging-standards"></a>Tagga standarder

Följande uppsättning med lägsta Taggar måste finnas på alla resurser och resurs grupper:

| Taggnamn | Beskrivning | Nyckel | Exempelvärde |
|--|--|--|--|
| Affär senhet | Avdelning på toppnivå för ditt företag som äger prenumerationen eller arbetsbelastningen som resursen tillhör. | BusinessUnit | EKONOMI, marknadsföring, {produkt namn}, CORP, delad |
| Kostnadsställe | Kostnadsställe som associeras med resursen.| CostCenter | Tal |
| Haveriberedskap | Programmet, arbetsbelastningen eller tjänstens affärskritiskhet. | AR | DR-AKTIVERAD, ICKE-DR-AKTIVERAD |
| Miljö | Programmet, arbetsbelastningen eller tjänstens distributionsmiljö. |  Kuvert | Produktion, utveckling, frågor och svar, Stage, test, utbildning |
| Namn på ägare | Programmet, arbetsbelastningen eller tjänstens ägare.| Ägare | e-post |
| Distributions typ | Definierar hur resurserna upprätthålls. | deploymentType | Manuell, terraform |
| Version | Ritningens version har distribuerats. | version | v-0,1 |
| Programnamn | Namnet på det associerade programmet, tjänsten eller arbets belastningen som är associerad med resursen. | ApplicationName | "app-namn" |

## <a name="customize-and-deploy-your-first-landing-zone"></a>Anpassa och distribuera din första landnings zon

Du kan [klona din terraform Foundation-landnings zon](https://github.com/microsoft/CloudAdoptionFramework/tree/master/ready). Det är enkelt att komma igång med landnings zonen genom att ändra terraform-variablerna. I vårt exempel använder vi **blueprint_foundations. sandbox. Auto. tfvars**, så terraform ställer automatiskt in värdena i den här filen åt dig.

Nu ska vi titta på de olika variabel avsnitten.

I det här första objektet skapar vi två resurs grupper i regionen `southeastasia` som heter `-hub-core-sec` och `-hub-operations` tillsammans med ett prefix som lagts till vid körning.

```hcl
resource_groups_hub = {
    HUB-CORE-SEC    = {
        name = "-hub-core-sec"
        location = "southeastasia"
    }
    HUB-OPERATIONS  = {
        name = "-hub-operations"
        location = "southeastasia"
    }
}
```

Därefter anger vi de regioner där vi kan ställa in grunderna. Här `southeastasia` används för att distribuera alla resurser.

```hcl
location_map = {
    region1   = "southeastasia"
    region2   = "eastasia"
}
```

Sedan anger vi kvarhållningsperioden för åtgärds loggarna och Azure-prenumerations loggarna. Dessa data lagras i separata lagrings konton och en Event Hub, vars namn skapas slumpmässigt eftersom de måste vara unika.

```hcl
azure_activity_logs_retention = 365
azure_diagnostics_logs_retention = 60
```

I tags_hub anger vi den minsta uppsättning taggar som används för alla resurser som skapats.

```hcl
tags_hub = {
    environment     = "DEV"
    owner           = "Arnaud"
    deploymentType  = "Terraform"
    costCenter      = "65182"
    BusinessUnit    = "SHARED"
    DR              = "NON-DR-ENABLED"
}
```

Sedan anger vi Log Analytics-namnet och en uppsättning lösningar som analyserar distributionen. Här har vi kvar nätverks övervakning, Active Directory (AD)-utvärdering och replikering, DNS-analys och Key Vault-analys.

```hcl

analytics_workspace_name = "lalogs"

solution_plan_map = {
    NetworkMonitoring = {
        "publisher" = "Microsoft"
        "product"   = "OMSGallery/NetworkMonitoring"
    },
    ADAssessment = {
        "publisher" = "Microsoft"
        "product"   = "OMSGallery/ADAssessment"
    },
    ADReplication = {
        "publisher" = "Microsoft"
        "product"   = "OMSGallery/ADReplication"
    },
    AgentHealthAssessment = {
        "publisher" = "Microsoft"
        "product"   = "OMSGallery/AgentHealthAssessment"
    },
    DnsAnalytics = {
        "publisher" = "Microsoft"
        "product"   = "OMSGallery/DnsAnalytics"
    },
    KeyVaultAnalytics = {
        "publisher" = "Microsoft"
        "product"   = "OMSGallery/KeyVaultAnalytics"
    }
}

```

Därefter konfigurerade vi aviserings parametrarna för Azure Security Center.

```hcl
# Azure Security Center Configuration
security_center = {
    contact_email   = "joe@contoso.com"
    contact_phone   = "+6500000000"
}
```

## <a name="get-started"></a>Kom igång

När du har granskat konfigurationen kan du distribuera konfigurationen på samma sätt som du distribuerar en terraform-miljö. Vi rekommenderar att du använder Rover, som är en Docker-behållare som tillåter distribution från Windows, Linux eller MacOS. Du kan komma igång med [Rover GitHub-lagringsplatsen](https://github.com/aztfmod/rover).

## <a name="next-steps"></a>Nästa steg

I bas landnings zonen fördelas en komplicerad miljö på ett sammansatt sätt. Den här versionen innehåller en uppsättning enkla funktioner som kan utökas av:

- Lägga till andra moduler till skissen.
- Skiktning av ytterligare landnings zoner ovanpå den.

Att skikta landnings zoner är en bra metod för att koppla från system, versions hantering av varje komponent som du använder och möjliggör snabb innovation och stabilitet för din infrastruktur som kod distribution.

Framtida referens arkitekturer visar det här konceptet för en nav-och eker-topologi.

> [!div class="nextstepaction"]
> [Granska exemplet för bas zon för terraform-vilplan](https://github.com/microsoft/CloudAdoptionFramework/tree/master/ready)
