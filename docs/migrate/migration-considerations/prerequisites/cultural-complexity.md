---
title: 'Förbered för kulturell komplexitet: justera roller och ansvarsområden'
description: Förbered dig för kulturell komplexitet genom att justera roller och ansvars områden.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 186772796694d6ef60a923c5098760a573d8db6d
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 01/28/2020
ms.locfileid: "76801502"
---
# <a name="prepare-for-cultural-complexity-aligning-roles-and-responsibilities"></a>Förbered för kulturell komplexitet: justera roller och ansvarsområden

En förståelse av den kultur som krävs för att använda befintliga datacentra är viktigt för att en migrering ska lyckas. I vissa organisationer ingår datacenterhantering i centraliserade IT-team. I dessa centraliserade team brukar roller och ansvarsområden vara väl definierade och förstås väl i hela teamet. För större företag, särskilt de som är knutna till krav från tredjepartsefterlevnad, tenderar kulturen att vara mer nyanserade och komplex. Kulturell komplexitet kan leda till hinder som är svåra att förstå och tar lång tid att övervinna.

I båda fallen är det klokt att investera i den dokumentation av roller och ansvars områden som krävs för att slutföra en migrering. Den här artikeln beskriver några av de roller och ansvarsområden som visas i en datacentermigrering. Den kan fungera som mall för dokumentation som kan förtydliga genomförandet.

## <a name="business-functions"></a>Verksamhetsfunktioner

I samband med en migrering finns det några viktiga funktioner som, om möjligt, bör utföras av verksamheten. Det är ofta IT som utför följande åtgärder. När medlemmar i företaget är delaktiga blir övergången längre fram oftast smidigare. Det innebär att viktiga aktörer under migrationsprocessen känner sig involverade.

| Process | Aktivitet | Beskrivning |
|---------|---------|---------|
| Utvärdera | Verksamhetsmål | Definiera vad ni hoppas på att få ut av migreringen som företag. |
| Utvärdera | Prioriteringar | Försäkra er om att migreringen överensstämmer med växlande affärsprioriteringar och marknadsförutsättningar. |
| Utvärdera | Motivering | Bekräfta antaganden som ligger till grund för föränderliga affärsmotiveringar. |
| Utvärdera | Risk | Hjälp molnimplementeringsteamet förstå de konkreta affärsriskernas betydelse. |
| Utvärdera | Godkänn | Granska och godkänn de beräknade konsekvenserna för företaget till följd av arkitekturändringarna. |
| Optimera | Ändringsplan | Definiera en ändringsplan för företagets förbrukning, inklusive perioder med låg aktivitet och ändringslås. |
| Optimera | Testning | Stäm av med privilegierade användare som kan verifiera prestandan och funktioner. |
| Skydda och hantera | Avbrottspåverkan | Hjälp molnimplementeringsteamet att storleksbestämma effekten av ett affärsprocessavbrott. |
| Skydda och hantera | Godkänn serviceavtalet (SLA) | Hjälp molnimplementeringsteamet att definiera serviceavtal och godtagbara toleranser för affärsavbrott. |

I slutänden är molnimplementeringsteamet ansvarigt för dessa aktiviteter. Dock kan inrättandet av ansvarsområden och en normal rytm i förhållande till verksamheten för dessa aktiviteter förbättra medverkan från berörda aktörer och samordningen i företaget.

## <a name="common-roles-and-responsibilities"></a>Vanliga roller och ansvarsområden

Varje process i diskussionen om ramprinciperna för molnimplementering inkluderar en processartikel som beskriver specifika aktiviteter för att samordna roller och ansvarsområden. För tydlighetens skull bör endast en aktör tilldelas till varje aktivitet, tillsammans med de ansvariga aktörer som krävs för att stödja dessa aktiviteter. Följande lista innehåller dock en serie vanliga roller och ansvarsområden som har en högre inverkan på körningen av migreringen. De här rollerna bör identifieras tidigt under migreringen.

> [!NOTE]
> I följande tabell bör en ansvarig aktör påbörja rollfördelningen. Den kolumnen bör anpassas för att passa befintliga processer för effektiv körning. Vi rekommenderar att endast en person betecknas som ansvarig aktör.

| Process | Aktivitet | Beskrivning | Ansvarig aktör |
|---------|---------|---------|---------|
| Krav | Digital egendom | Samordna det befintliga lagret med grundläggande antaganden baserat på verksamhetsresultat. | molnstrategiteamet |
| Krav | Migreringsuppgifter | Prioritera den sekvens med arbetsbelastningar som ska migreras. | molnstrategiteamet |
| Utvärdera | Arkitektur | Kräv inledande antaganden för att definiera målarkitekturen baserat på användningsstatistik. | molnimplementeringsteamet |
| Utvärdera | Godkännande | Godkänn den föreslagna arkitekturen. | molnstrategiteamet |
| Migrera | Replikeringsåtkomst | Åtkomst till befintliga lokala värdar och tillgångar för att upprätta replikeringsprocesser. | molnimplementeringsteamet |
| Optimera | Redo | Kontrollera att systemet uppfyller prestanda- och kostnadskraven inför upphöjning. | molnimplementeringsteamet |
| Optimera | Höj upp | Behörigheter för att höja upp en arbetsbelastning till produktion och dirigera om produktionstrafiken. | molnimplementeringsteamet |
| Skydda och hantera | Åtgärdsövergång | Dokumentera produktionssystem inför produktionsåtgärder. | molnimplementeringsteamet |

> [!CAUTION]
> För dessa aktiviteter påverkar behörigheter och auktorisering kraftigt vem som betecknas som ansvarig aktör. Denne måste ha direkt åtkomst till produktionssystem i den befintliga miljön eller måste ha möjlighet att skydda åtkomsten genom andra ansvariga aktörer. Beslutet om ansvarig aktör har en direkt inverkan på strategin för upphöjning under migrerings- och optimeringsprocesserna.

## <a name="next-steps"></a>Nästa steg

När teamet har en allmän förståelse för roller och ansvars områden är det dags att börja förbereda den tekniska informationen om migreringen. Kännedom om [teknik komplexitet och ändringshantering](./technical-complexity.md) kan hjälpa dig att förbereda molnimplementeringsteamet för migreringens juridiska komplexitet genom att samordna med en stegvis ändringshanteringsprocess.

> [!div class="nextstepaction"]
> [Teknisk komplexitet och ändringshantering](./technical-complexity.md)
