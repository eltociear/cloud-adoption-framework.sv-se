---
title: Centralisera hanterings åtgärder
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Vägledning om hur du centraliserar hanterings åtgärder
author: JnHs
ms.author: jenhayes
ms.date: 09/27/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: b8e4e37ba9a771937b11f08f1abae45de2f818ab
ms.sourcegitcommit: 1dccf1aed8e98aa0f58c4f86d90c65f5fa5ac84d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/02/2019
ms.locfileid: "71804735"
---
# <a name="centralize-management-operations"></a>Centralisera hanterings åtgärder

För de flesta organisationer är det möjligt att använda en enda Azure Active Directory (Azure AD)-klient för alla användare för att förenkla hanterings åtgärder och minska underhållskostnaderna, eftersom alla hanterings uppgifter kan vara av utsedda användare, användar grupper eller tjänstens huvud namn inom den innehav. Vi rekommenderar att du bara använder en Azure AD-klient för din organisation om det är möjligt.

Det finns dock situationer som kan kräva att en organisation underhåller flera Azure AD-klienter. Till exempel kan flera klienter krävas på grund av:

- Helt oberoende dotter bolag.
- Drifts oberoende i flera geografiska områden.
- Krav på juridisk eller efterlevnad.
- Förvärv av andra organisationer (ibland tillfälligt tills en långsiktig företags konsoliderings strategi definieras).

I de fall där en arkitektur med flera innehavare krävs är [Azure Lighthouse](https://docs.microsoft.com/azure/lighthouse/overview) ett sätt att centralisera och effektivisera hanterings åtgärder. Prenumerationer från flera klienter kan registreras för Azure- [delegerad resurs hantering](https://docs.microsoft.com/azure/lighthouse/concepts/azure-delegated-resource-management), så att angivna användare i hanterings klienten kan utföra [hanterings funktioner för flera innehavare](https://docs.microsoft.com/azure/lighthouse/concepts/cross-tenant-management-experience) på ett centraliserat och skalbart sätt.

Anta till exempel att din organisation har en enda klient organisation, *klient a*. Din organisation kommer sedan att förvärva ytterligare två klienter, *klient B* och *klient C*och du har affärs skäl som kräver att du underhåller dem som separata klienter.

Organisationen vill använda samma princip definitioner, säkerhets kopierings metoder och säkerhets processer för alla klienter. Eftersom du redan har användare (inklusive användar grupper och tjänstens huvud namn) som ansvarar för att utföra dessa uppgifter i klient organisationen A, kan du publicera alla prenumerationer i klient B och klient C så att samma användare i klient organisationen kan utföra dessa uppgifter. Klient A blir sedan den hanterande klienten för klient B och klient organisation C.

![Användare i klient organisation A hanterar resurser i klient B och klient organisation C](../_images/manage/enterprise-azure-lighthouse.jpg)

Mer information finns i [Azure Lighthouse i Enterprise-scenarier](https://docs.microsoft.com/azure/lighthouse/concepts/enterprise).
