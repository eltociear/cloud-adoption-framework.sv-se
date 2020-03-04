---
title: Optimera migrerade arbetsbelastningar
description: Optimera migrerade arbetsbelastningar
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: aed8ba9d97cfbc236d378066569b466302b66239
ms.sourcegitcommit: 72a280cd7aebc743a7d3634c051f7ae46e4fc9ae
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/02/2020
ms.locfileid: "78225445"
---
# <a name="optimize-migrated-workloads"></a>Optimera migrerade arbetsbelastningar

När en arbetsbelastning och dess stödjande tillgångar har migrerats till molnet måste den förberedas innan den kan flyttas upp till produktion. I den här processen gör aktiviteter arbetsbelastningen redo, bestämmer storlek på de beroende resurserna och förbereder verksamheten för det tillstånd då den migrerade molnbaserade arbetsbelastningen börjar användas i produktion.

Målet med optimering är att förbereda en migrerad arbetsbelastning för uppflyttning till produktionsanvändning.

## <a name="definition-of-done"></a>Definitionen av *klar*

Optimeringsprocessen är klar när en arbetsbelastning är korrekt konfigurerad, storleksbestämd och distribuerad i produktionen.

## <a name="accountability-during-optimization"></a>Ansvarstagande under optimeringen

Molnimplementeringsteamet ansvarar för hela optimeringsprocessen. Dock bör även medlemmar i teamen för molnstrategi, molndrift och molnstyrning vara ansvariga för aktiviteter i den här processen.

## <a name="responsibilities-during-optimization"></a>Ansvarsområden under optimering

Utöver det övergripande ansvaret finns det åtgärder som en person eller en grupp måste vara direkt ansvarig för. Här följer några aktiviteter som ansvariga parter måste tilldelas:

- **Verksamhetstestning.** Lös eventuella kompatibilitetsproblem som förhindrar att arbetsbelastningen slutför migreringen till molnet.
  - Privilegierade användare i verksamheten bör ha stort deltagande i testningen av den migrerade arbetsbelastningen. Beroende på den grad av optimering som försöks kan flera testningscykler komma att krävas.
- **Plan för verksamhetsändring.** Utvecklingen av en plan för användningsimplementering, ändringar i affärsprocesser och ändringar i affärs-KPI:er eller utbildningsmått som ett resultat av migreringsarbetet.
- **Prestandamätning och optimering.** Undersökning av affärstestningen och automatiserad testning för att granska prestanda. Baserat på användningen förfinar molnimplementeringsteamet storleksbestämningen för de distribuerade tillgångarna i syfte att balansera kostnad och prestanda mot förväntade produktionskrav.
- **Redo för produktion.** Förbered arbetsbelastningen och miljön för att stödja arbetsbelastningens pågående produktionsanvändning.
- **Höj upp.** Omdirigera produktionstrafik till den migrerade och optimerade arbetsbelastningen. Den här aktiviteten representerar slutförandet av en lanseringscykel.

Utöver grundläggande aktiviteter finns det några parallella aktiviteter som kräver specifika tilldelningar och genomförandeplaner:

- **Ta ur bruk.** I allmänhet kan besparingar realiseras från en migrering när de föregående produktionstillgångarna tas ur bruk och kasseras på rätt sätt.
- **Återblick.** Varje lansering medför möjligheter till djupare inlärning och fokus på tillväxt. Efter varje lanseringscykel bör molnimplementeringsteamet utvärdera migreringsprocesserna för att identifiera möjliga förbättringar.

## <a name="next-steps"></a>Nästa steg

Nu när du har en övergripande förståelse för optimeringsprocessen kan du påbörja processen genom att [upprätta en plan för verksamhetsändring för kandidatarbetsbelastningen](./business-change-plan.md).

> [!div class="nextstepaction"]
> [Plan för verksamhetsändring](./business-change-plan.md)
