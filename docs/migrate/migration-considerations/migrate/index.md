---
title: Genomföra en migrering
description: Få en översikt över de artiklar som beskriver de olika aktiviteter som kan ingå vid migrering av en arbetsbelastning i Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 82ded4af4d3014187e012dbc7d371237d519b4ca
ms.sourcegitcommit: 1a4b140f09bdaa141037c54a4a3b5577cda269db
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/30/2020
ms.locfileid: "80392428"
---
# <a name="execute-a-migration"></a>Genomföra en migrering

När en arbetsbelastning har utvärderats kan den migreras till molnet. I den här artikelserien beskrivs de olika aktiviteter som kan ingå i genomförandet av en migrering.

## <a name="objective"></a>Mål

Målet med en migrering är att migrera en enskild arbetsbelastning till molnet.

## <a name="definition-of-done"></a>Definitionen av *klar*

Migreringsfasen är färdig när en arbetsbelastning har mellanlagrats och är redo för testning i molnet, inklusive alla beroende tillgångar som krävs för att arbetsbelastningen ska fungera. Under optimeringsprocessen förbereds arbetsbelastningen produktionsanvändning.

Den här definitionen av *klar* kan variera beroende på dina processer för testning och lansering. Nästa artikel i serien behandlar [beslut om en uppflyttningsmodell](./promotion-models.md) och kan hjälpa dig förstå när det är bäst att flytta upp en migrerad arbetsbelastning till produktion.

## <a name="accountability-during-migration"></a>Ansvarstagande under migrering

Molnimplementeringsteamet ansvarar för hela migreringsprocessen. Medlemmar i molnstrategiteamet har dock vissa ansvarsområden som beskrivs i följande avsnitt.

## <a name="responsibilities-during-migration"></a>Ansvarsområden under migrering

Utöver det övergripande ansvaret finns det åtgärder som en person eller en grupp måste vara direkt ansvarig för. Här följer några aktiviteter som ansvariga parter måste tilldelas:

- **Åtgärder.** Lös eventuella kompatibilitetsproblem som förhindrar att arbetsbelastningen migreras till molnet.
  - Enligt beskrivningen i artikeln om förutsättningar gällande [teknisk komplexitet och ändringshantering](../prerequisites/technical-complexity.md) bör ett beslut fattas i förväg för att avgöra hur den här aktiviteten ska genomföras. I synnerhet: kommer åtgärderna att slutföras av molnimplementeringsteamet under samma sprint som det faktiska migreringsarbetet? Alternativt: kommer en våg- eller fabriksmodell användas för att slutföra åtgärder i en separat iteration? Om den här grundläggande processfrågan inte kan besvaras av varje medlem i teamet kan det vara bra att gå igenom avsnittet om [förutsättningar](../prerequisites/index.md) igen.
- **Replikering.** Skapa en kopia av varje tillgång i molnet för att synkronisera virtuella datorer, data och program med resurser i molnet.
  - Beroende på uppflyttningsmodellen kan det krävas olika verktyg för att slutföra den här aktiviteten.
- **Mellanlagring.** När alla tillgångar för en arbetsbelastning har replikerats och verifierats kan arbetsbelastningen mellanlagras för affärstestning och genomförande av en affärsändringsplan.

## <a name="next-steps"></a>Nästa steg

Nu när du har en allmän förståelse för migreringsprocessen är du redo att [besluta om en uppflyttningsmodell](./promotion-models.md).

> [!div class="nextstepaction"]
> [Besluta om en uppflyttningsmodell](./promotion-models.md)
