---
title: Etablera iterationer och publiceringsplaner
description: Använd ramverket för moln införande för Azure för att lära dig hur du definierar iterationer och versions planer för att hjälpa dig att hantera din implementering.
author: BrianBlanchard
ms.author: brblanch
ms.date: 07/01/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: plan
ms.openlocfilehash: 8aaee4546568301eabbe774cea08c3d5d975bb3e
ms.sourcegitcommit: 959cb0f63e4fe2d01fec2b820b8237e98599d14f
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/11/2020
ms.locfileid: "79092677"
---
# <a name="establish-iterations-and-release-plans"></a>Etablera iterationer och publiceringsplaner

Agile och andra iterativa metoder bygger på begreppen iterationer och versioner. Den här artikeln beskriver tilldelningen av iterationer och versioner under planeringen. De här tilldelningarna driver tids linje synlighet för att göra konversationer enklare bland medlemmarna i moln strategi teamet. Tilldelningarna justerar också tekniska uppgifter på ett sätt som moln implementerings teamet kan hantera under implementeringen.

## <a name="establish-iterations"></a>Upprätta iterationer

I en iterativ metod för teknisk implementering planerar du tekniska ansträngningar kring återkommande tids block. Iterationer tenderar att vara en vecka till sex veckors tids block. Konsensus rekommenderar att två veckor är den genomsnittliga upprepnings tiden för de flesta moln implementerings team. Valet av upprepnings tid beror på typen av teknisk ansträngning, den administrativa belastningen och teamets preferens.

Om du vill börja justera ansträngningarna på en tids linje, rekommenderar vi att du definierar en uppsättning iterationer som de senaste 6 till 12 månaderna.

## <a name="understand-velocity"></a>Förstå hastighet

Anpassning av insatser till iterationer och versioner kräver en förståelse av hastigheten. Hastighet är den mängd arbete som kan slutföras i en bestämd iteration. Vid tidig planering är hastigheten en uppskattning. Efter flera iterationer blir hastigheten en mycket värdefull indikator för de åtaganden som teamet kan göra på ett säkert sätt.

Du kan mäta hastigheten i abstrakta termer som artikel punkter. Du kan också mäta den i mer konkreta termer som timmar. För de flesta iterativa ramverk rekommenderar vi att du använder abstrakta mätningar för att undvika utmaningar i precision och uppfattning. Exemplen i den här artikeln representerar hastighet i timmar per Sprint. Den här presentationen gör ämnet mer allmänt förstått.

**Exempel:** Ett moln antagande team med fem personer har allokerats till två veckors sprintar. Med tanke på aktuella skyldigheter som möten och stöd för andra processer kan varje grupp medlem konsekvent bidra med 20 timmar per vecka till implementerings ansträngningen. För det här teamet är den inledande hastighets uppskattningen 100 timmar per Sprint.

## <a name="iteration-planning"></a>Upprepnings planering

Börja med att planera iterationer genom att utvärdera de tekniska uppgifterna baserat på den prioriterade efter släparna. Moln implementerings team uppskattar den insats som krävs för att slutföra olika uppgifter. Dessa uppgifter tilldelas sedan till den första tillgängliga iterationen.

Under upprepnings planeringen bör moln implementerings teamen validera och förfina uppskattningar. De gör det tills de har justerat all tillgänglig hastighet för vissa aktiviteter. Den här processen fortsätter för varje prioriterad arbets belastning tills alla ansträngningar justeras till en prognostiserad iteration.

I den här processen validerar teamet de uppgifter som tilldelats nästa Sprint. Gruppen uppdaterar sina uppskattningar baserat på teamets konversation om varje uppgift. Teamet lägger sedan till varje uppskattad aktivitet till nästa Sprint tills den tillgängliga hastigheten är uppfylld. Slutligen beräknar teamet ytterligare aktiviteter och lägger till dem i nästa iteration. Teamet utför dessa steg tills hastigheten för den iterationen också är slut.

Föregående process fortsätter tills alla aktiviteter har tilldelats en iteration.

**Exempel:** Vi bygger på föregående exempel. Antag att varje arbets belastnings migrering kräver 40-aktiviteter. Anta också att du uppskattar varje aktivitet för att ta ett genomsnitt på en timme. Den kombinerade uppskattningen är cirka 40 timmar per migrering av arbets belastning. Om dessa uppskattningar är konsekventa för alla tio av de prioriterade arbets belastningarna tar de här arbets belastningarna att ta 400 timmar.

Den hastighet som definieras i föregående exempel innebär att migreringen av de första 10 arbets belastningarna tar fyra iterationer, vilket är två månader från kalender tiden. Den första iterationen kommer att bestå av 100 uppgifter som resulterar i migreringen av två arbets belastningar. I nästa iteration leder en liknande samling med 100 uppgifter till migreringen av tre arbets belastningar.

> [!WARNING]
> Föregående antal aktiviteter och uppskattningar används strikt som exempel. De tekniska uppgifterna är sällan som konsekventa. Du bör inte se det här exemplet som en reflektion av hur lång tid det tar att migrera en arbets belastning.

## <a name="release-planning"></a>Versions planering

I molnet definieras en version som en samling slut produkter som producerar tillräckligt med affärs värde för att motivera risken för avbrott i affärs processerna.

Om du släpper alla arbets belastnings ändringar i en produktions miljö skapas vissa ändringar i affärs processerna. Vi rekommenderar att dessa ändringar är sömlösa och att företaget ser värdet av ändringarna utan betydande avbrott i tjänsten. Men risken för affärs avbrott finns i alla förändringar och bör inte beaktas lätt.

För att säkerställa att en ändring är motiverad av den potentiella avkastningen bör moln strategi teamet delta i versions planering. När aktiviteter har justerats till Sprint, kan teamet fastställa en grov tids linje för när varje arbets belastning blir redo för produktions versionen. Moln strategi teamet granskar tiden för varje version. Teamet identifierar sedan Bryt-punkten mellan risk-och affärs värde.

**Exempel:** Genom att fortsätta med föregående exempel har moln strategi teamet granskat upprepnings planen. Granskningen identifierade två lanserings punkter. Under den andra iterationen är totalt fem arbets belastningar redo för migrering. De fem arbets belastningarna ger betydande affärs värde och kommer att utlösa den första versionen. Nästa version kommer att få två iterationer senare, när de följande fem arbets belastningarna är klara att lanseras.

## <a name="assign-iteration-paths-and-tags"></a>Tilldela upprepnings banor och Taggar

För kunder som hanterar moln implementerings planer i Azure DevOps visas tidigare processer genom att tilldela en upprepnings väg till varje aktivitet och användar berättelse. Vi rekommenderar även att tagga varje arbets belastning med en angiven version. Den taggade och tilldelningen matar in den automatiska populationen av tids linje rapporter.

## <a name="next-steps"></a>Nästa steg

[Uppskatta tids linjer](./timelines.md) för att kommunicera förväntningarna på rätt sätt.

> [!div class="nextstepaction"]
> [Uppskatta tids linjer](./timelines.md)
