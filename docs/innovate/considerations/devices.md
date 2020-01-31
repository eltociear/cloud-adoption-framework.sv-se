---
title: 'Moln innovation: interagera med enheter'
description: Introduktion till utveckling av moln – interagera med enheter
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: 8b39362f2e0e21431e5d04ef05e2676094bca9bc
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 01/28/2020
ms.locfileid: "76808489"
---
# <a name="ambient-experiences-interact-with-devices"></a>Omgivande upplevelser: interagera med enheter

I [build med Customer empati](./build.md)diskuterade vi de tre testerna av den sanna innovationen: lös ett kund behov, se till att kunden kommer tillbaka och skala ut över en bas för kund kohorter. Varje test av hypotesen kräver insatser och iterationer på tillvägagångs sättet för att anta. Den här artikeln innehåller insikter om några avancerade metoder för att minska den ansträngningen genom *omgivande upplevelser*. Genom att interagera med enheter, i stället för ett program, kan kunden förmodligen gå över till din lösning först.

## <a name="ambient-experiences"></a>Omgivande upplevelser

En omgivande miljö är en digital upplevelse som är relaterad till den omedelbara miljön. En lösning som har stöd för omgivande erfarenheter strävar efter att möta kunden i deras egna behov. När det är möjligt uppfyller lösningen kundernas behov utan att lämna det flöde av aktivitet som utlöste den.

Livet i den digitala ekonomin är fullt av störande. Vi är alla bombarded med sociala, e-post, webb-, visualiserings-och muntliga meddelanden, som var och en riskerar att distraheras. Den här risken ökar med varje sekund som förflyter mellan kundens behovs punkt och den tidpunkt då en lösning påträffas. Oräkneliga-kunder går förlorade i det korta tids glappet. För att förbättra en ökning av upprepad antagande måste du minska antalet störande genom att minska tiden till lösning (TTS).

## <a name="interacting-with-devices"></a>Interagera med enheter

En vanlig webb upplevelse är den vanligaste program utvecklings tekniken som används för att uppfylla en kunds behov. Den här metoden förutsätter att kunden är framför sin dator. Om kunden konsekvent uppfyller deras behov samtidigt som den bärbara datorn skapas, skapar du en webbapp. Webbappen tillhandahåller en omgivande upplevelse för kunden i det scenariot. Vi vet dock att det här scenariot är mindre och mindre troligt i vår aktuella era.

![Omgivande upplevelser](../../_images/innovate/ambient-experiences.png)

Omgivande upplevelser kräver vanligt vis mer än en webbapp dessa dagar. Genom att [mäta](./measure.md) och [lära med kunden](./learn.md) är det beteende som utlöser kundens behov observeras, spåras och används för att bygga en mer omgivande upplevelse. I följande lista sammanfattas några metoder för integrering av omgivande lösningar i Hypotheses, med mer information om var och en av följande stycken.

- **[Mobil miljö](#mobile-experience):** Som med bärbara datorer är Mobile Apps allmänt förekommande i kund miljöer. I vissa situationer kan detta ge en tillräcklig nivå av interaktivitet för att skapa en lösning som är omgivande.
- **[Mixad verklighet](#mixed-reality):** Ibland måste en kunds typiska miljö ändras för att göra en interaktion som är omgivande. Den här faktorn skapar något av en falskt verklighet där kunden interagerar med lösningen och behöver uppfyllas. I det här fallet är lösningen inom den falska verkligheten.
- **[Integrerad verklighet](#integrated-reality):** Fokusera närmare på sanna Ambience-lösningar med integrerad verklighet och fokusera på användningen av en enhet som finns i kundens verklighet för att integrera lösningen i sina naturliga beteenden. En virtuell assistent är ett bra exempel på integrering av verklighet i omgivande miljö. En mindre känd option rör Sakernas Internet-teknik (IoT) som integrerar enheter som redan finns i kundens omgivningar.
- **[Justerad verklighet](#adjusted-reality):** När någon av dessa lösningar använder förutsägelse analys i molnet för att definiera och tillhandahålla en interaktion med kunden genom den naturliga omgivningen har lösningen justerats i verkligheten.

Förståelse för kundens behov och mätning av kund påverkan hjälper dig att avgöra om en enhets interaktion eller en omgivande miljö är nödvändig för att verifiera din hypotes. Med var och en av dessa data punkter kan du använda följande avsnitt för att hitta den bästa lösningen.

## <a name="mobile-experience"></a>Mobil miljö

I det första steget i den omgivande miljön flyttas användaren bort från datorn. Dagens konsumenter och affärs proffs rör sig flytande mellan mobila och PC-enheter. Var och en av de plattformar eller enheter som används av kunden skapar en ny potentiell upplevelse. Att lägga till en mobil miljö som utökar den primära lösningen är det snabbaste sättet att förbättra integrationen i kundens omedelbara miljö. Även om en mobil enhet är långt från omgivningen kan den ligga närmare kundens behovs punkt.

När kunderna är mobila och ändrings platser ofta, kan det representera den mest relevanta formen av den omgivande upplevelsen för en viss lösning. Under de senaste tio åren har innovation ofta utlösts av integrering av befintliga lösningar med en mobil miljö.

Azure App Services är ett bra exempel på den här metoden. Under tidiga iterationer kan [webbappens funktion i Azure App-tjänster](https://docs.microsoft.com/azure/app-service/overview) användas för att testa hypotesen. När Hypotheses blir mer komplexa kan [Mobile app-funktionen i Azure App Services](https://docs.microsoft.com/azure/app-service-mobile) utöka webbappen så att den körs på flera olika mobila plattformar.

## <a name="mixed-reality"></a>Mixed Reality

Lösningar för Mixad verklighet representerar nästa förfallo nivå för omgivande upplevelser. Den här metoden förstärker eller replikerar kundens omgivningar. Det skapar en förlängning av verklighet för kunden att arbeta i.

> [!IMPORTANT]
> Om en virtuell verklighet-enhet (VR) krävs och *inte redan är en del av en kunds omedelbara omgivande eller naturliga beteenden*, är utöknings bara eller en virtuell verklighet mer av en alternativ upplevelse och mindre av en omgivande upplevelse.

Blandade verklighets upplevelser är allt vanligare bland fjärran slutna arbets uppgifter. Användningen av dem ökar ännu snabbare i branscher som kräver samarbets-eller special kunskaper som inte är lättillgänglig på den lokala marknaden. Situationer som kräver centraliserad implementering av en komplex produkt för en fjärran sluten arbets kraft är särskilt fertilet underlag för förhöjd verklighet. I dessa scenarier kan det centrala support teamet och fjärranslutna anställda använda förstärkt verklighet för att arbeta med, felsöka och installera produkten.

Anta till exempel fallet med avstånds ankare. Med avstånds fäst punkter kan du skapa blandade verklighets upplevelser med objekt som bevarar sina respektive platser på enheter över tid. Genom spatiala ankare kan ett särskilt beteende samlas in, registreras och bevaras, vilket ger en omgivande upplevelse nästa gången användaren arbetar i den förhöjda miljön. Molnbaserade [ankare](https://docs.microsoft.com/azure/spatial-anchors/overview) är en tjänst som flyttar den här logiken till molnet, vilket gör att upplevelsen kan delas mellan enheter och till och med mellan lösningar.

## <a name="integrated-reality"></a>Integrerad verklighet

Bortom den mobila verkligheten eller till och med Mixed Reality är integrerad verklighet. Integrerad verklighet syftar till att ta bort digitala erfarenheter helt. Alla runt oss är enheter med funktioner för beräkning och anslutning. Dessa enheter kan användas för att samla in data från den omedelbara omgivningen utan att kunden behöver röra sig på en telefon-, bärbar eller VR-enhet.

Den här upplevelsen är idealisk när en viss typ av enhet är konsekvent inom samma omgivning som kundens behov sker. Vanliga scenarier är fabriks golv, hissar och till och med din bil. De här typerna av stora enheter innehåller redan beräknings kraft. Du kan också använda data från själva enheten för att identifiera kund beteenden och skicka dessa beteenden till molnet. Den här automatiska insamlingen av kund beteende data minskar dramatiskt behovet av att en kund ska mata in data. Dessutom kan webb-, mobil-eller VR-upplevelsen fungera som en feedback-slinga för att dela med sig av vad som har lärts från den integrerade verklighets lösningen.

Exempel på integrerad verklighet i Azure kan vara:

- [Azure Sakernas Internet-lösningar (IoT)](https://docs.microsoft.com/azure/iot-fundamentals), en samling tjänster i Azure som varje stöd för att hantera enheter och data flödet från dessa enheter till molnet och ut till slutanvändarna.
- [Azure Sphere](https://docs.microsoft.com/azure-sphere)en kombination av maskin vara och program vara. Azure Sphere är ett innately säkert sätt att aktivera en befintlig enhet för att på ett säkert sätt överföra data mellan enheten och Azure IoT-lösningar.
- [Azure Kinect Developer Kit](https://docs.microsoft.com/azure/Kinect-dk), AI-sensorer med avancerad dator vision och tal modeller. Dessa sensorer kan samla in visuella data och ljuddata från den omedelbara omgivningen och mata in dessa indata i din lösning.

Du kan använda alla tre verktygen för att samla in data från den naturliga omgivningen och när kunden behöver det. Därifrån kan din lösning svara på dessa data inmatningar för att lösa behovet, ibland innan kunden är ännu medveten om att en utlösare för detta behov har uppstått.

## <a name="adjusted-reality"></a>Justerad verklighet

Den högsta formen av omgivande erfarenheter är justerad, och kallas ofta för *omgivnings information*. Justerad verklighet är en metod för att använda information från din lösning för att ändra kundens verklighet utan att behöva interagera direkt med ett program. I den här metoden är det program som du ursprungligen skapade för att bevisa att din hypotes inte längre är relevant. I stället använder enheter i miljön de indata och utdata som behövs för att uppfylla kundernas behov.

Virtuella assistenter och smarta högtalare erbjuder bra exempel på justerad verklighet. En smart talare är ett exempel på enkel integrerad verklighet. Men Lägg till en smart ljus-och rörelse sensor i en smart talare-lösning och det är enkelt att skapa en grundläggande lösning som vänder sig till lamporna när du anger ett rum.

Fabriks golv runtom i världen ger ytterligare exempel på justerad verklighet. I tidiga faser av integrerad verklighet identifierade sensorer på enheter, t. ex. överhettning, och aviserar sedan en mänsklig genom ett program. I justerad verklighet kan kunden fortfarande vara involverad, men feedback-slingan är tätare. På ett justerat verklighet fabriks lager kan en enhet upptäcka överhettning på en viktig dator någonstans längs med monterings linjen. Någon annan stans på golvet, en andra enhet kan sedan sakta produktion något så att datorn blir sval och sedan återupptas hela takten när villkoret är löst. I den här situationen är kunden en andra deltagare. Kunden använder ditt program för att ange regler och förstå hur dessa regler har påverkat produktion, men de är inte nödvändiga för feedback-slingan.

De Azure-tjänster som beskrivs i [azure Sakernas Internet-lösningar (IoT)](https://docs.microsoft.com/azure/iot-fundamentals), [Azure Sphere](https://docs.microsoft.com/azure-sphere)och [Azure Kinect Developer Kit](https://docs.microsoft.com/azure/Kinect-dk) kan var och en vara komponenter i en anpassad verklighet-lösning. Ditt ursprungliga program och din affärs logik fungerar sedan som mellanliggande mellan miljö ingången och den ändring som ska göras i den fysiska miljön.

En digital, dubbel är ett annat exempel på en justerad verklighet. Den här termen avser en digital representation av en fysisk enhet som presenteras via dator-, mobil-eller blandade real tids format. Till skillnad från mindre avancerade 3D-modeller, visar digitala dubbla data som samlas in från en faktisk enhet i den fysiska miljön. Den här lösningen gör att användaren kan interagera med den digitala representationen på ett sätt som aldrig kan göras i verkligheten. I den här metoden justerar fysiska enheter en blandad verklighets miljö. Lösningen samlar dock fortfarande in data från en integrerad verklighets lösning och använder dessa data för att forma verkligheten för kundens aktuella miljö.

I Azure skapas och nås digitala dubbla steg via en tjänst som kallas [Azure Digital-dubbla](https://docs.microsoft.com/azure/digital-twins/about-digital-twins).

## <a name="next-steps"></a>Nästa steg

Nu när du har en djupare förståelse för enhets interaktioner och den omgivande upplevelsen som passar din lösning, är du redo att utforska den slutliga disciplinen för innovation, [förutsägelse och påverkan](./predict.md).

> [!div class="nextstepaction"]
> [Förutsäg och inflytande](./predict.md)
