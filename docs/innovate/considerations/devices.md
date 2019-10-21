---
title: 'Moln innovation: interagera med enheter'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Introduktion till utveckling av moln – interagera med enheter
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/24/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: 8c170b543344394396660ee299589a94365cff8f
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/17/2019
ms.locfileid: "72557731"
---
# <a name="ambient-experiences-interact-with-devices"></a>Omgivande upplevelser: interagera med enheter

I [utvecklingen med empati](./build.md)diskuterade vi de tre testerna i den verkliga innovationen: lös ett kund behov, se till att kunden kommer tillbaka, skala över en bas för kund kohorter. Varje test av hypotesen kräver insatser och iterationer på den metod som ska vidtas. Den här artikeln ger insikter om några avancerade metoder för att minska den ansträngningen genom **omgivande upplevelser**. Genom att interagera med enheter, i stället för ett program, kan kunden förmodligen gå över till din lösning först för att få deras behov uppfyllda.

## <a name="ambient-experiences"></a>Omgivande upplevelser

En omgivande miljö är en digital upplevelse som är relaterad till den omedelbara miljön. En lösning som har stöd för omgivande erfarenheter strävar efter att möta kunden i deras egna behov. När det är möjligt uppfyller lösningen kundernas behov utan att lämna det naturliga flödet av vad de gjorde.

Livet i den digitala ekonomin är fullt av störande. Vi är alla bombarded med sociala, e-post-, webb-, visualiserings-och muntliga meddelanden, som var och en riskerar att distraheras. Risken för störande ökar med varje sekund mellan kundens behov och en interaktion med lösningen. Oräkneliga-kunder går förlorade under den korta tids perioden. Minska antalet störningar genom att minska tiden till lösning (TTS) för att utveckla ökningar i upprepad antagande.

## <a name="interacting-with-devices"></a>Interagera med enheter

En vanlig webb upplevelse är den vanligaste program utvecklings tekniken som används för att uppfylla en kunds behov. Antagande bakade i den här metoden är att kunden kommer framför sin dator. Om kunden konsekvent uppfyller deras behov samtidigt som den bärbara datorn skapas, skapar du en webbapp. Webbappen tillhandahåller en "omgivnings upplevelse" för kunden i det scenariot. Men vi vet att det här scenariot är allt mindre troligt i modern samhälle.

![Omgivande upplevelser](../../_images/innovate/ambient-experiences.png)

Omgivande upplevelser, som illustreras ovan, kräver vanligt vis mer än en webbapp. Genom att [mäta](./measure.md) och [lära med kunden](./learn.md) är det beteendet som leder till kundens behovs utlösare observeras, spåras och används för att bygga en mer omgivande upplevelse. Följande sammanfattar några metoder för integrering av omgivande lösningar i Hypotheses, mer information om var och en av följande stycken.

- **[Mobil miljö](#mobile-experience)** : ungefär som en bärbar dator är mobilappar ofta en del av kundernas omgivningar. I vissa fall kan detta ge en tillräcklig nivå av interaktivitet för att skapa en lösning som är omgivande.
- **[Mixad verklighet](#mixed-reality):** Ibland måste en kunds naturliga miljö ändras för att göra en interaktion som är omgivande. Detta skapar en bit av en falskt verklighet där kunden kan interagera med lösningen och behöver uppfyllas. I det här fallet är lösningen inom den falska verkligheten.
- **[Integrerad verklighet](#integrated-reality):** Vi fokuserar närmare på sanna Ambience, integrerade verklighets lösningar fokuserar på användningen av en enhet som finns i kundens verklighet för att integrera lösningen i naturliga beteenden. En virtuell assistent är ett bra exempel på integrering av verklighet i omgivande miljö. Ett mindre känt alternativ är att använda Sakernas Internet-teknik (IoT) för att integrera enheter som redan finns i kundens omgivningar.
- **[Justerad verklighet](#adjusted-reality):** När någon av de omgivande lösningarna ovan använder förutsägelse analys i molnet för att definiera och tillhandahålla en interaktion med kunden genom den naturliga omgivningen har lösningen justerats i verkligheten.

Att förstå kund behovet och mäta kund påverkan är att hjälpa till med att avgöra om en enhets interaktion eller en omgivande miljö kommer att krävas för att validera din hypotes. Med var och en av dessa data punkter kan du hitta den bästa lösningen med hjälp av följande avsnitt.

## <a name="mobile-experience"></a>Mobil miljö

Det första steget i den omgivande upplevelsen är att ta bort datorn. Dagens konsumenter och affärs proffs rör sig flytande mellan mobila och PC-enheter. Var och en av de plattformar eller enheter som används av kunden skapar en ny potentiell upplevelse för kunden. Att lägga till en mobil miljö som utökar den primära lösningen är det snabbaste sättet att förbättra integrationen i kundens omedelbara miljö. Även om en mobil enhet är långt från den omgivande enheten, kan den komma närmare kundens behovs punkt.

Om kunderna är mobila och föränderliga platser ofta, kan det vara den mest relevanta formen av den omgivande upplevelsen för en specifik lösning. En gemensam källa för innovation under de senaste tio åren har utökats med de befintliga lösningarna för att integrera en mobil upplevelse.

Exempel på den här metoden kan visas i Azure App Services. Vid tidiga iterationer kan [webbappens funktion i Azure App Service](/azure/app-service/overview) användas för att testa hypotesen. När Hypotheses blir mer komplexa kan [Mobile app-funktionen i Azure App Services](/azure/app-service-mobile/) utöka webbappen så att den körs på flera olika mobila plattformar.

## <a name="mixed-reality"></a>Mixad verklighet

Nästa nivå av förfallo tid för omgivande upplevelser är utökningen eller replikeringen av kundens omgivningar genom blandade verklighets lösningar. I den här metoden blir lösningen mer omgivande genom att skapa en förlängning av verklighet för kunden att arbeta i.

> [!IMPORTANT]
> Om en virtuell verklighet-enhet (VR) krävs och *inte redan är en del av deras omedelbara omgivande eller naturliga beteende*, är utöknings bara/virtuella verklighet mer av en alternativ upplevelse och mindre av en omgivande upplevelse.

Den här typen av upplevelse är allt vanligare för fjär arbets styrka. Användningen av dessa upplevelser ökar ännu snabbare i branscher som kräver samarbets-eller kunskaps kunskaper som inte är tillgängliga på den lokala marknaden. Ett vanligt scenario som kräver förhöjd verklighet som en del av ett naturligt beteende är ett centraliserat implementerings stöd för en komplex produkt för en fjärran sluten arbets kraft. I dessa scenarier kan det centrala support teamet och fjärran sluten anställd använda förstärkta verklighet för att arbeta med fel sökning eller installation av produkten.

För scenariot ovan eller andra liknande scenarier är ett exempel på en miljö som använder spatiala ankare. Med avstånds ankare kan du skapa blandade verklighets upplevelser med objekt som bevarar sin plats mellan enheter över tid. Genom spatiala ankare kan ett särskilt beteende samlas in, spelas in och bevaras, vilket ger en omgivande upplevelse, nästa gången användaren arbetar inom den förhöjda miljön. Molnbaserade [ankare](https://docs.microsoft.com/azure/spatial-anchors/overview) är en tjänst som flyttar den här logiken till molnet, vilket gör att upplevelsen kan delas mellan enheter och till och med mellan lösningar.

## <a name="integrated-reality"></a>Integrerad verklighet

Utöver mobil verklighet eller till och med Mixad verklighet är användningen av integrerad verklighet. I den här metoden är målet att ta bort digitala erfarenheter helt. Alla runt oss är enheter med funktioner för beräkning och anslutning. Dessa enheter kan användas för att samla in data från den omedelbara omgivningen utan att kunden behöver röra sig på en telefon-, bärbar eller VR-enhet.

Den här typen av upplevelse är idealisk när en viss typ av enhet är konsekvent inom samma omgivning som kund behovet sker på. Vanliga scenarier är fabriks golv, hissar eller till och med din bil. De här typerna av stora enheter innehåller redan beräknings kraft. Du kan också använda data från själva enheten för att identifiera kund beteenden och skicka dessa beteenden till molnet. Den här automatiska insamlingen av kund beteende data minskar dramatiskt behovet av att en kund ska mata in data. Dessutom kan webb-, mobil-eller VR-upplevelsen användas som en feedback-slinga för att dela vad som har lärts ut från den integrerade verklighets lösningen.

Exempel på integrerad verklighet i Azure kan vara:

- [Azure Sakernas Internet-lösningar (IoT)](https://docs.microsoft.com/azure/iot-fundamentals), en samling tjänster i Azure som varje stöd för att hantera enheter och data flödet från dessa enheter till molnet och ut till slutanvändarna.
- [Azure Sphere](/azure-sphere)en kombination av maskin vara och program vara Azure Sphere är ett innately säkert sätt att aktivera en befintlig enhet för att på ett säkert sätt överföra data mellan enheten och Azure IoT-lösningar.
- [Azure Kinect Developer Kit](https://docs.microsoft.com/azure/Kinect-dk), AI-sensorer med förhands gransknings-och tal modeller, som kan samla in visuella data och ljud data från den omedelbara omgivningen och mata in dessa indata i din lösning.

Alla tre kan användas för att samla in data inom den naturliga omgivningen vid behov. Därifrån kan din lösning svara på dessa data inmatningar för att lösa behovet, ibland innan kunden är ännu medveten om att en utlösare för detta behov har uppstått.

## <a name="adjusted-reality"></a>Justerad verklighet

Den högsta formen av omgivande erfarenheter är justerad, och kallas ofta för omgivnings information. Justerad verklighet är en metod för att använda information från din lösning för att ändra kundens verklighet, utan att behöva interagera direkt med ett program. I den här metoden är det program som du ursprungligen skapade för att bevisa att din hypotes inte längre är relevant. I stället skulle enheterna i miljön under lätta indata och utdata för att uppfylla kundernas behov.

Virtuella assistenter/smarta högtalare kan ge ett bra exempel på justerad verklighet. En smart talare är ett exempel på enkel integrerad verklighet. Lägg till en smart ljus-och motion-lösning i en smart talare-lösning och det är enkelt att skapa en grundläggande lösning med som slår på lamporna när du anger ett rum.

Fabriks golv runt om i världen ger ytterligare scenarier av justerad verklighet. I tidiga faser av integrerad verklighet identifierade sensorer för enheter, t. ex. överhettning, och rapporterade ett behov av en ändring av en mänsklig person via ett program. I justerad verklighet kan kunden fortfarande vara inblandad. Men feedback-slingan är tätare. I ett justerat verklighet fabriks våningsplan skulle en enhet upptäcka överhettaning på en viktig dator någonstans i sammansättnings linjen. Någon annan stans på golvet skulle en andra enhet sakta produktion något för att göra det möjligt för datorn att svalna och återuppta takten när villkoret löstes. I det här scenariot är kunden en andra delta. Kunden använder ditt program för att ange regler och förstå hur dessa regler har påverkat produktion, men är inte en nödvändig del av feedback-slingan.

Azure-tjänsterna i föregående avsnitt, [azure Sakernas Internet-lösningar (IoT)](https://docs.microsoft.com/azure/iot-fundamentals), [Azure Sphere](/azure-sphere)och [Azure Kinect Developer Kit](https://docs.microsoft.com/azure/Kinect-dk) kunde var och en vara komponenter i en justerad verklighet-lösning. Ditt ursprungliga program och din affärs logik fungerar som en mellanhand mellan miljö ingången och den ändring som ska göras i den fysiska miljön.

Ett annat exempel på en justerad verklighet är att skapa en digital enhet, som är en digital representation av en fysisk enhet som presenteras via dator-, mobil-eller blandade Reality-format. Till skillnad från mindre avancerade 3D-modeller, visar digitala dubbla data som samlas in från en faktisk enhet i den fysiska miljön. Detta gör att användaren kan interagera med den digitala representationen på ett sätt som aldrig kunde utföras i den verkliga världen. I den här metoden justerar de fysiska enheterna en blandad verklighets miljö. Men lösningen samlar fortfarande in data från en integrerad verklighets lösning och använder den för att forma verkligheten för kundens aktuella miljö.

I Azure skapas och nås digitala dubbla steg via en tjänst som kallas [Azure Digital-dubbla](https://docs.microsoft.com/azure/digital-twins/about-digital-twins).

## <a name="next-steps"></a>Nästa steg

Med en djupare förståelse för enhets interaktioner och den omgivande upplevelsen som passar din lösning är du nu redo att utforska den slutliga disciplinen för innovation, [förutsägelse och påverkan](./predict.md).

> [!div class="nextstepaction"]
> [Förutsäg och inflytande](./predict.md)
