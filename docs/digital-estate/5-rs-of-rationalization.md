---
title: Cloud rationalisering
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Granska de tillgängliga alternativen för att rationalisera en digital egendom.
author: BrianBlanchard
ms.author: brblanch
ms.date: 12/10/2018
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: plan
ms.custom: governance
ms.openlocfilehash: 40962b8c658c40e4a27e3c025bc42b3aa5acd0f3
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/16/2019
ms.locfileid: "71023624"
---
# <a name="cloud-rationalization"></a>Cloud rationalisering

Cloud rationalisering är en process för att utvärdera till gångar för att fastställa det bästa sättet att migrera eller modernisera varje till gång i molnet. Mer information om processen för rationalisering finns i [Vad är en digital egendom?](./index.md).

## <a name="rationalization-context"></a>Rationalisering-kontext

"Fem RS-rationalisering" som listas i den här artikeln är ett bra sätt att ge ett möjligt framtida tillstånd för arbets belastningar som betraktas som en moln kandidat. Den här etiketten bör dock placeras i rätt sammanhang innan du försöker rationalisera en miljö. Granska följande myths för att tillhandahålla den kontexten:

- **Myten Det är enkelt att fatta rationalisering beslut tidigt i processen.** Korrekt rationalisering kräver en djupgående kunskap om arbets belastningen och tillhör Ande till gångar (appar, virtuella datorer och data). Viktigast av detta är att vi tar tid av korrekta rationalisering. Vi rekommenderar att du använder en [stegvis rationalisering-process](./rationalize.md#incremental-rationalization).

- **Myten Moln införande måste vänta tills alla arbets belastningar är rationella.** Att rationalisera en hel IT-portfölj eller till och med ett enda data Center kan försena förverkligandet av affärs värde per månad eller till och med år. Fullständig rationalisering bör undvikas när det är möjligt. Använd i stället [kraften hos 10 tillvägagångs sätt för att planera](./rationalize.md#release-planning) för att fatta beslut om de kommande 10 arbets belastningarna som är planerad för moln införande.

- **Myten Affärs justering måste vänta tills alla arbets belastningar är rationella.** Om du vill utveckla en affärs motivering för en moln implementering kan du göra några grundläggande antaganden på portfölj nivå. När motivation justeras till innovation, antar du omarkitekturen. Anta att du är värd för de motivation som ska migreras. Dessa antaganden kan påskynda affärs justerings processen. Antaganden anropas sedan och budgetarna förfinas under utvärderings fasen för varje arbets belastnings antagande.

Granska nu följande fem RS-rationalisering för att bekanta dig med den långsiktiga processen. När du utvecklar din moln implementerings plan väljer du det alternativ som passar bäst för dina motivation, affärs resultat och nuvarande tillstånds miljö. Målet i rationalisering för digital egendom är att ange en bas linje och inte rationalisera varje arbets belastning.

## <a name="the-five-rs-of-rationalization"></a>Fem RS-rationalisering

De fem RS-rationalisering som visas här beskriver de vanligaste alternativen för rationalisering.

## <a name="rehost"></a>Byta värd

En Rehost-migrering, som även kallas "lyft och Shift", flyttar en aktuell tillstånds till gång till den valda moln leverantören, med minimal förändring i den övergripande arkitekturen.

Vanliga driv rutiner kan vara:

- Minska kapital kostnaden
- Frigör Data Center utrymme
- Uppnå snabb avkastning på investeringar i molnet

Kvantitativa analys faktorer:

- VM-storlek (processor, minne, lagring)
- Beroenden (nätverks trafik)
- Till gångens kompatibilitet

Kvalitativa analys faktorer:

- Tolerans för ändring
- Affärsprioriteringar
- Kritiska affärs händelser
- Process beroenden

## <a name="refactor"></a>Omstrukturera

PaaS-alternativ (Platform as a Service) kan minska drifts kostnaderna som är associerade med många program. Det är en bra idé att något som ett program behöver för att anpassa sig till en PaaS modell.

"Återställnings processen" avser också program utvecklings processen för omstrukturering av kod som gör det möjligt för ett program att leverera på nya affärs möjligheter.

Vanliga driv rutiner kan vara:

- Snabbare och kortare uppdateringar
- Kod portabilitet
- Större moln effektivitet (resurser, hastighet, kostnad)

Kvantitativa analys faktorer:

- Storlek på program till gång (CPU, minne, lagring)
- Beroenden (nätverks trafik)
- Användar trafik (sid visningar, tid på sida, inläsnings tid)
- Utvecklings plattform (språk, data plattform, tjänster på mellan nivå)

Kvalitativa analys faktorer:

- Fortsatta affärs investeringar
- Alternativ/tids linjer för burst
- Affärs process beroenden

## <a name="rearchitect"></a>Ändra utformning

Vissa ålders program är inte kompatibla med moln leverantörer på grund av de arkitektoniska beslut som har fattats när programmet byggdes. I dessa fall kan programmet behöva återskapas före omvandling.

I andra fall kan program som är molnbaserade, men inte molnbaserad, skapa kostnads effektivitet och drift effektivitet genom att bygga om lösningen i ett moln program.

Vanliga driv rutiner kan vara:

- Program skalning och smidighet
- Enklare antagande av nya moln funktioner
- Blandning av teknik stackar

Kvantitativa analys faktorer:

- Storlek på program till gång (CPU, minne, lagring)
- Beroenden (nätverks trafik)
- Användar trafik (sid visningar, tid på sida, inläsnings tid)
- Utvecklings plattform (språk, data plattform, tjänster på mellan nivå)

Kvalitativa analys faktorer:

- Växande affärs investeringar
- Drifts kostnader
- Potentiella feedback-slingor och DevOps investeringar.

## <a name="rebuild"></a>Återskapa

I vissa fall kan delta som måste lösas för att kunna skicka ett program vara för stort för att kunna motivera ytterligare investeringar. Detta gäller särskilt för program som tidigare uppfyllde behoven hos ett företag men som nu inte stöds eller är feljusterade med de aktuella affärs processerna. I det här fallet skapas en ny kodbas som överensstämmer med en [molnbaserad](https://azure.microsoft.com/overview/cloudnative) metod.

Vanliga driv rutiner kan vara:

- Förbättra utvecklingsprocessen
- Skapa appar snabbare
- Minska drifts kostnaderna

Kvantitativa analys faktorer:

- Storlek på program till gång (CPU, minne, lagring)
- Beroenden (nätverks trafik)
- Användar trafik (sid visningar, tid på sida, inläsnings tid)
- Utvecklings plattform (språk, data plattform, tjänster på mellan nivå)

Kvalitativa analys faktorer:

- Avböja slutanvändarens belåtenhet
- Affärs processer som begränsas av funktioner
- Potentiell kostnad, erfarenhet eller vinst vinster

## <a name="replace"></a>Ersätt

Lösningar implementeras vanligt vis genom att använda den bästa tekniken och metoden som är tillgänglig när som helst. Ibland kan SaaS-program (program vara som en tjänst) tillhandahålla alla nödvändiga funktioner för det värdbaserade programmet. I dessa scenarier kan en arbets belastning schemaläggas för framtida utbyte, och tar bort den från omvandlings ansträngningen.

Vanliga driv rutiner kan vara:

- Standardisera bransch-bästa praxis
- Påskynda införandet av verksamhets drivna metoder
- Omfördela utvecklings investeringar till program som skapar konkurrens kraftig differentiering eller fördelar

Kvantitativa analys faktorer:

- Generella drift kostnads minskningar
- VM-storlek (processor, minne, lagring)
- Beroenden (nätverks trafik)
- Till gångar som dras tillbaka

Kvalitativa analys faktorer:

- Kostnads förmåns analys av den aktuella arkitekturen jämfört med en SaaS-lösning
- Affärs process kartor
- Data scheman
- Anpassade eller automatiserade processer

## <a name="next-steps"></a>Nästa steg

Du kan samla in dessa fem RS-rationalisering till en digital fastighet som hjälper dig att fatta rationalisering beslut om det framtida läget för varje program.

> [!div class="nextstepaction"]
> [Vad är en digital egendom?](./index.md)
