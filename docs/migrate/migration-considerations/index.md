---
title: Cloud Adoption Framework-migreringsmodellen
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Cloud Adoption Framework-migreringsmodellen
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 8087c67d07a17475e49d70a2b70b78d8af20460a
ms.sourcegitcommit: 57390e3a6f7cd7a507ddd1906e866455fa998d84
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/31/2019
ms.locfileid: "73240273"
---
# <a name="cloud-adoption-framework-migration-model"></a>Cloud Adoption Framework-migreringsmodellen

I det här Cloud Adoption Framework-avsnittet beskrivs principerna bakom dess migreringsmodell. Där så är möjligt försöker innehållet att upprätthålla en leverantörsneutral position då du vägleds genom de processer och aktiviteter som kan tillämpas på valfri molnmigrering, oavsett vilken molnleverantör du väljer.

## <a name="understand-migration-motivations"></a>Förstå motivering för migrering

Molnmigrering handlar om portföljhantering förklädd som en teknisk implementering. Under migreringsprocessen väljer du att flytta vissa tillgångar, investera i andra sådana och ta förlegade eller oanvända tillgångar ur bruk. Vissa tillgångar optimeras, refaktoriseras eller byts ut helt som en del av den här processen. Vart och ett av de här besluten bör överensstämma med motiveringen till molnmigrering. De mest framgångsrika migreringarna går även ett steg längre och riktar in dessa beslut med önskade affärsresultat.

Cloud Adoption Framework-migreringsmodellen är beroende av att din organisation har slutfört en process för affärsberedskap för molnimplementering. Se till att du har granskat vägledningen [Planera](../../strategy/index.md) och [Redo](../../ready/index.md) i Cloud Adoption Framework för att avgöra affärsdrivande faktorer eller annan motivering för molnmigrering samt eventuell organisationsplanering eller utbildning som krävs innan en migreringsprocess genomförs i stor skala.

> [!NOTE]
> Affärsplanering är viktigt, men det är lika viktigt att ha ett tankesätt som fokuserar på tillväxt. Parallellt med bredare affärsplaneringsarbete som utförs av molnstrategiteamet kan molnimplementeringsteamet med fördel börja migrera en enskild arbetsbelastning som förberedelse inför migreringsarbete i större skala. Den här inledande migreringen gör att teamet får praktisk erfarenhet av de affärsmässiga och tekniska frågor som migrering medför.

## <a name="envision-an-end-state"></a>Föreställ dig ett slutresultat

Det är viktigt att upprätta en ungefärlig vision om slutresultatet innan du påbörjar migreringsarbetet. Diagrammet nedan visar en lokal startpunkt med infrastruktur, program och data som definierar din *digital egendom*. Under migreringsprocessen överförs dessa tillgångar via någon av de fem migreringsstrategier som beskrivs i [de fem R:en för rationalisering](../../digital-estate/5-rs-of-rationalization.md).

![Infografik med migreringsalternativen](../../_images/migrate/migration-options.png)

Migrering och modernisering av arbetsbelastningar omfattar allt från enkla _värdbytesmigreringar_ (_lift and shift_) med hjälp av IaaS-funktioner (infrastruktur som en tjänst), som inte kräver kod- eller appändringar, till _refaktorisering_ med minimala ändringar eller _arkitekturomarbetning_ för att ändra och utöka funktionerna i kod och app till att utnyttja molntekniker.

Molnbaserade strategier och PaaS-strategier (plattform som en tjänst) *återskapar* lokala arbetsbelastningar med hjälp av Azure-plattformserbjudanden och hanterade tjänster. Arbetsbelastningar som har motsvarande fullständigt hanterade molnbaserade SaaS-erbjudanden (programvara som en tjänst) kan ofta *ersättas* helt av dessa tjänster som en del av migreringsprocessen.

> [!NOTE]
> Under den offentliga förhandsversionen av Cloud Adoption Framework framhäver det här avsnittet av ramverket en migreringsstrategi med värdbyte. Även om PaaS- och SaaS-lösningar diskuteras som alternativ när så är lämpligt är migrering av VM-baserade arbetsbelastningar med hjälp av IaaS-funktioner huvudfokuset.
>
> Andra avsnitt och framtida iterationer av det här innehållet kommer att gå in djupare på andra metoder. En genomgång på hög nivå om att utöka migreringens omfång till att omfatta mer komplicerade migreringsstrategier finns i artikeln Balansera portföljen.

## <a name="incremental-migration"></a>Inkrementell migrering

Cloud Adoption Framework-migreringsmodellen baseras på en inkrementell molnomvandlingsprocess. Den förutsätter att organisationen börjar med ett enskilt molnmigreringsprojekt med begränsat omfång som vi ofta kallar den första arbetsbelastningen. Det här projektet utökas iterativt till att omfatta fler arbetsbelastningar allt eftersom ditt driftsteam förfinar och förbättrar migreringsprocesserna.

Molnmigreringsverktyg som [Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview) kan migrera hela datacenter som består av tiotusentals virtuella datorer. Dock kan verksamheten och befintliga IT-åtgärder sällan hantera förändring i en sådan snabb takt. Därför delar många organisationer upp migreringsprojekt i flera iterationer där en arbetsbelastning (eller samling med arbetsbelastningar) flyttas per iteration.

Principerna bakom den här inkrementella modellen baseras på genomförandet av processer och förutsättningar som refereras till i följande infografik.

![Cloud Adoption Framework-migreringsmodellen](../../_images/operational-transformation-migrate.png)

Konsekvent tillämpning av dessa principer representerar ett slutmål för dina molnmigreringsprocesser och ska inte betraktas som en obligatorisk startpunkt. När ditt migreringsarbete mognar kan du läsa vägledningen i det här avsnittet för att definiera de bästa processerna som stöder organisationens behov.

## <a name="next-steps"></a>Nästa steg

Börja lära dig om den här modellen genom att [undersöka förutsättningarna för migrering](./prerequisites/index.md).

> [!div class="nextstepaction"]
> [Förutsättningar för migrering](./prerequisites/index.md)
