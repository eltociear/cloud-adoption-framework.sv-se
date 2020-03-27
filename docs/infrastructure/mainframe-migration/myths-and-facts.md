---
title: Myths och fakta för stordator migrering
description: Lär dig att skilja myths från verkligheten om stordatorer och utvärdera de stordatorer som passar bäst för Azure.
author: njray
ms.author: v-nanra
ms.date: 12/27/2018
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 35cd68a317ae3c4d49c961d020d6e803f387741d
ms.sourcegitcommit: ea63be7fa94a75335223bd84d065ad3ea1d54fdb
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/27/2020
ms.locfileid: "80356874"
---
<!-- cSpell:ignore njray nanra chargebacks IPLs -->

# <a name="mainframe-myths-and-facts"></a>Stordator myths och fakta

Stordatorer är på ett framträdande sätt i dator historiken och fortsätter att vara livskraftiga för mycket speciella arbets belastningar. De flesta enas om att stordatorer är en beprövad plattform med långvariga drift procedurer som gör dem tillförlitliga, robusta miljöer. Program varan körs baserat på användning, mätt i miljon instruktioner per sekund (MIPS) och omfattande användnings rapporter är tillgängliga för åter betalningar.

Kraften, tillgängligheten och processor kraften i stordatorer har gjorts på nästan Mythical proportioner. För att utvärdera de stordator-arbetsbelastningar som är mest lämpliga för Azure, vill du först skilja myths från verkligheten.

## <a name="myth-mainframes-never-go-down-and-have-a-minimum-of-five-9s-of-availability"></a>Myten: stordatorer försvinner aldrig och har minst fem nior tillgänglighet

Maskin vara och operativ system för stordatorer visas som pålitliga och stabila. Men verkligheten är att stillestånds tiden måste schemaläggas för underhåll och omstarter (kallas första program inläsningar eller IPLs). När dessa uppgifter betraktas har en stordator lösning ofta närmare två eller tre nior, vilket motsvarar den för avancerade, Intel-baserade servrar.

Stordatorer förblir också utsatta för katastrofer som andra servrar och kräver att UPS-system (Uninterruptible Power Supply) hanterar dessa typer av problem.

## <a name="myth-mainframes-have-limitless-scalability"></a>Myten: stordatorer har obegränsad skalbarhet

En stordators skalbarhet beror på kapaciteten hos dess system program vara, till exempel CICS (Customer Control system) och kapaciteten för nya instanser av stordator motorer och lagring. Vissa stora företag som använder stordatorer har anpassat sina CICS för prestanda och har i övrigt möjlighet att växa kapaciteten hos de största tillgängliga stordatorerna.

## <a name="myth-intel-based-servers-are-not-as-powerful-as-mainframes"></a>Myten: Intel-baserade servrar är inte lika kraftfulla som stordatorer

De nya kärnan Intel-baserade systemen har lika mycket data bearbetnings kapacitet som stordatorer.

## <a name="myth-the-cloud-cant-accommodate-mission-critical-applications-for-large-companies-such-as-financial-institutions"></a>Myten: molnet kan inte hantera verksamhets kritiska program för stora företag, till exempel finansiella institutioner

Även om det kan finnas vissa isolerade instanser där moln lösningar är korta, är det vanligt vis att programalgoritmerna inte kan distribueras. Några exempel är undantagen, inte regeln.

## <a name="summary"></a>Sammanfattning

Med en jämförelse erbjuder Azure en alternativ plattform som kan leverera motsvarande stordator funktioner och funktioner och till en mycket lägre kostnad. Dessutom är den totala ägande kostnaden (TCO) för molnets prenumerations förbruknings driven kostnads modell mycket billigare än stordator datorer.

## <a name="next-steps"></a>Nästa steg

> [!div class="nextstepaction"]
> [Gör växeln från stordatorer till Azure](./migration-strategies.md)
