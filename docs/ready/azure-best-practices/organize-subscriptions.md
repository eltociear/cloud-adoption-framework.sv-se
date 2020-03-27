---
title: Organisera och hantera flera Azure-prenumerationer
description: Använd ramverket för moln införande för Azure för att lära dig hur du skapar en hierarki för hanterings grupper för att förenkla hanteringen av dina prenumerationer och resurser.
author: alexbuckgit
ms.author: abuck
ms.date: 05/20/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: e874c518537232104d9bbddbdf8e84841239e56b
ms.sourcegitcommit: ea63be7fa94a75335223bd84d065ad3ea1d54fdb
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/27/2020
ms.locfileid: "80359782"
---
# <a name="organize-and-manage-multiple-azure-subscriptions"></a>Organisera och hantera flera Azure-prenumerationer

Om du bara har ett fåtal prenumerationer är det relativt enkelt att hantera dem oberoende av varandra. Men om du har många prenumerationer kan du skapa en hierarki för hanterings grupper som hjälper dig att hantera dina prenumerationer och resurser.

## <a name="azure-management-groups"></a>Azure-hanteringsgrupper

Med Azures hanterings grupper kan du effektivt hantera åtkomst, principer och efterlevnad för en organisations prenumerationer. Varje hanteringsgrupp är en container för en eller flera prenumerationer.

Hanterings grupper är ordnade i en enkel hierarki. Du definierar den här hierarkin i din Azure Active Directory (Azure AD)-klient organisation så att den överensstämmer med organisationens struktur och behov. Den översta nivån kallas för *rothanteringsgruppen.* Du kan definiera upp till sex nivåer av hanteringsgrupper i hierarkin. Varje prenumeration finns bara i en hanteringsgrupp.

Azure tillhandahåller fyra nivåer av hanterings omfång:

- Hanteringsgrupper
- Prenumerationer
- Resursgrupper
- Resurser

Åtkomst eller principer som tillämpas på en nivå i hierarkin tillämpas också på nivåerna under denna. En resursägare eller en prenumerationsägare kan inte ändra en nedärvd princip. Den här begränsningen förbättrar styrningen.

> [!NOTE]
> Tagg arv stöds inte ännu, men kommer snart att vara tillgängligt.

Med den här arvs modellen kan du ordna prenumerationerna i hierarkin så att varje prenumeration följer lämpliga principer och säkerhets kontroller.

![De fyra omfångsnivåerna för att organisera dina Azure-resurser](../../ready/azure-setup-guide/media/organize-resources/scope-levels.png)

Alla tilldelningar av användaråtkomst eller principtilldelning för rothanteringsgruppen gäller för alla resurser inom katalogen. Tänk efter noga vilka objekt du definierar i det här omfånget. Inkludera endast de tilldelningar som du måste ha.

## <a name="create-your-management-group-hierarchy"></a>Skapa en hierarki för hanterings grupper

När du definierar hierarkin för hanterings grupper måste du först skapa rot hanterings gruppen. Flytta sedan alla befintliga prenumerationer i katalogen till rot hanterings gruppen. Nya prenumerationer skapas alltid i rothanteringsgruppen. Senare kan du flytta dem till en annan hanterings grupp.

När du flyttar en prenumeration till en befintlig hanterings grupp ärver den principerna och roll tilldelningarna från hanterings gruppens hierarki ovanför den. När du har upprättat flera prenumerationer för dina Azure-arbetsbelastningar kan du skapa ytterligare prenumerationer som innehåller Azure-tjänster som andra prenumerationer delar.

Om du förväntar dig att Azure-miljön ska växa bör du skapa hanterings grupper för produktion och inte produktion nu och tillämpa lämpliga principer och åtkomst kontroller på hanterings grupps nivå. Nya prenumerationer kommer att ärva lämpliga kontroller när de läggs till i varje hanterings grupp.

![Exempel på en hierarki för hanterings grupper](../../_images/ready/management-group-hierarchy-v2.png)

## <a name="example-use-cases"></a>Exempel på användningsområden

Vissa grundläggande exempel på hur du kan använda hanteringsgrupper för att separera olika arbetsbelastningar:

- **Produktion jämfört med arbets belastningar** som inte är produktion: Använd hanterings grupper för att enklare hantera olika roller och principer mellan produktions-och icke-Production-prenumerationer. Till exempel kan prenumerationer som inte är för produktion beviljas åtkomst till utvecklare, medan i produktion utvecklare endast har läsar åtkomst.
- **Interna tjänster jämfört med externa tjänster:** Företag har ofta olika krav, principer och roller för interna tjänster jämfört med externa kund tjänster.

## <a name="related-resources"></a>Relaterade resurser

Läs följande resurser för att lära dig mer om att ordna och hantera dina Azure-resurser.

- [Ordna resurser med hanteringsgrupper i Azure](https://docs.microsoft.com/azure/governance/management-groups)
- [Utöka åtkomst för att hantera alla Azure-prenumerationer och hanteringsgrupper](https://docs.microsoft.com/azure/role-based-access-control/elevate-access-global-admin)
- [Flytta Azure-resurser till ny resursgrupp eller prenumeration](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-move-resources)

## <a name="next-steps"></a>Nästa steg

Granska [rekommenderade namngivnings- och taggningskonventioner](./naming-and-tagging.md) som du följer när du distribuerar dina Azure-resurser.

> [!div class="nextstepaction"]
> [Rekommenderade regler för namngivning och taggar](./naming-and-tagging.md)
