---
title: Skapa ytterligare prenumerationer för att skala din Azure-miljö
description: Använd ramverket för moln införande för Azure för att lära dig hur du utvecklar en strategi för att skala din miljö med hjälp av flera Azure-prenumerationer.
author: alexbuckgit
ms.author: abuck
ms.date: 05/20/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: dd052e42bc9685701df831878c12ed37ed42395c
ms.sourcegitcommit: ea63be7fa94a75335223bd84d065ad3ea1d54fdb
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/27/2020
ms.locfileid: "80359769"
---
# <a name="create-additional-subscriptions-to-scale-your-azure-environment"></a>Skapa ytterligare prenumerationer för att skala din Azure-miljö

Organisationer använder ofta flera Azure-prenumerationer för att undvika resurs gränser per prenumeration och för att hantera och styra sina Azure-resurser på ett bättre sätt. Det är viktigt att definiera en strategi för att skala dina prenumerationer.

## <a name="review-fundamental-concepts"></a>Granska grundläggande begrepp

När du expanderar din Azure-miljö bortom dina [ursprungliga prenumerationer](./initial-subscriptions.md)är det viktigt att förstå Azure-koncepten, till exempel konton, innehavare, kataloger och prenumerationer. Mer information finns i [grundläggande begrepp för Azure](../considerations/fundamental-concepts.md).

Andra överväganden kan kräva ytterligare prenumerationer. Tänk på följande när du utökar din molnegendom.

## <a name="technical-considerations"></a>Tekniska överväganden

**Prenumerations begränsningar:** Prenumerationer har definierade gränser för vissa resurs typer. Till exempel är antalet virtuella nätverk i en prenumeration begränsat. När en prenumeration närmar sig dessa gränser måste du skapa en annan prenumeration och lägga till ytterligare resurser där. Mer information finns i [prenumerations-och tjänst begränsningar i Azure](https://docs.microsoft.com/azure/azure-subscription-service-limits#general-limits).

**Klassiska modell resurser:** Om du har använt Azure under en längre tid kan du ha resurser som har skapats med den klassiska distributions modellen. Azure-principer, rollbaserad åtkomst kontroll, resurs gruppering och taggar kan inte tillämpas på klassiska modell resurser. Du bör flytta dessa resurser till prenumerationer som bara innehåller klassiska modell resurser.

**Kostnader:** Det kan finnas ytterligare kostnader för inkommande och utgående data mellan prenumerationer.

## <a name="business-priorities"></a>Affärsprioriteringar

Dina affärs prioriteringar kan leda till att du skapar ytterligare prenumerationer. Dessa prioriteringar omfattar:

- Verksamhet
- Migrering
- Kostnad
- Åtgärder
- Säkerhet
- Styrning

Mer information om hur du skalar dina prenumerationer finns i [besluts hand boken för prenumerationen](../../decision-guides/subscriptions/index.md) i moln införande ramverket.

## <a name="moving-resources-between-subscriptions"></a>Flytta resurser mellan prenumerationer

När din prenumerations modell växer kan du bestämma att vissa resurser tillhör andra prenumerationer. Många typer av resurser kan flyttas mellan prenumerationer. Du kan också använda automatiserade distributioner för att återskapa resurser i en annan prenumeration. Mer information finns i [Flytta Azure-resurser till en annan resursgrupp eller prenumeration](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-move-resources).

## <a name="tips-for-creating-new-subscriptions"></a>Tips för att skapa nya prenumerationer

- Identifiera vem som ansvarar för att skapa nya prenumerationer.
- Bestäm vilka resurs typer som är tillgängliga i en prenumeration som standard.
- Bestäm hur alla standardprenumerationer ska se ut. I överväganden ingår RBAC-åtkomst, principer, taggar och infrastrukturresurser.
- Om möjligt [skapar du nya prenumerationer program mässigt](https://docs.microsoft.com/azure/azure-resource-manager/management/programmatically-create-subscription) via ett huvud namn för tjänsten. Du måste [bevilja behörighet till tjänstens huvud namn](https://docs.microsoft.com/azure/azure-resource-manager/grant-access-to-create-subscription) för att kunna skapa prenumerationer. Definiera en säkerhetsgrupp som kan begära nya prenumerationer via ett automatiserat arbetsflöde.
- Om du är en Enterprise-avtalskund (EA) kan du be Azure-supporten att blockera skapandet av icke-EA-prenumerationer för din organisation.

## <a name="next-steps"></a>Nästa steg

Skapa en hierarki för hanterings grupper som hjälper dig att [organisera och hantera dina prenumerationer och resurser](./organize-subscriptions.md).

> [!div class="nextstepaction"]
> [Organisera och hantera dina prenumerationer och resurser](./organize-subscriptions.md)
