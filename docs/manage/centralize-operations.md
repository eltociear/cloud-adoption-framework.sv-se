---
title: Centralisera hanteringsåtgärder
description: Vägledning om hur du centraliserar hanterings åtgärder
author: JnHs
ms.author: jenhayes
ms.date: 09/27/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: a02e5804bd2ea18bd385634cbab57b21c8427bba
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 01/28/2020
ms.locfileid: "76807894"
---
# <a name="centralize-management-operations"></a>Centralisera hanteringsåtgärder

För de flesta organisationer gör det möjligt att använda en enda Azure Active Directory (Azure AD)-klient för alla användare för att förenkla hanterings åtgärder och minska underhållskostnaderna. Detta beror på att alla hanterings uppgifter kan vara av utsedda användare, användar grupper eller tjänstens huvud namn inom den klient organisationen. 

Vi rekommenderar att du bara använder en Azure AD-klient för din organisation, om möjligt. Vissa situationer kan dock kräva att en organisation underhåller flera Azure AD-klienter av följande anledningar:

- De är helt oberoende oberoende dotter bolag.
- De fungerar oberoende av varandra i flera geografiska områden.
- Vissa krav gällande juridisk eller efterlevnad gäller.
- Det finns förvärv av andra organisationer (ibland tillfälligt tills en långsiktig företags konsoliderings strategi definieras).

När en arkitektur för flera innehavare krävs är [Azure Lighthouse](https://docs.microsoft.com/azure/lighthouse/overview) ett sätt att centralisera och effektivisera hanterings åtgärder. Prenumerationer från flera klienter kan registreras för Azure- [delegerad resurs hantering](https://docs.microsoft.com/azure/lighthouse/concepts/azure-delegated-resource-management). Med det här alternativet kan angivna användare i hanterings klienten utföra [funktioner för hantering av flera innehavare](https://docs.microsoft.com/azure/lighthouse/concepts/cross-tenant-management-experience) på ett centraliserat och skalbart sätt.

Anta till exempel att din organisation har en enda klient organisation, *klient a*. Organisationen erhåller sedan två ytterligare klienter, *klient B* och *klient C*och du har affärs skäl som kräver att du underhåller dem som separata klienter.

Organisationen vill använda samma princip definitioner, säkerhets kopierings metoder och säkerhets processer för alla klienter. Eftersom du redan har användare (inklusive användar grupper och tjänstens huvud namn) som ansvarar för att utföra dessa uppgifter i klient organisationen A, kan du publicera alla prenumerationer i klient B och klient C så att samma användare i klient organisationen kan utföra dessa uppgifter. Klient A blir sedan den hanterande klienten för klient B och klient organisation C.

![Användare i klient organisation A hanterar resurser i klient B och klient organisation C](../_images/manage/enterprise-azure-lighthouse.jpg)

Mer information finns i [Azure Lighthouse i Enterprise-scenarier](https://docs.microsoft.com/azure/lighthouse/concepts/enterprise).
