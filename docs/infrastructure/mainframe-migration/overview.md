---
title: Översikt över stordator migrering
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Migrera program från stordator miljöer till Azure, en beprövad, hög tillgänglig och skalbar infrastruktur för system som för närvarande körs på stordatorer.
author: njray
ms.author: v-nanra
ms.date: 12/27/2018
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: ab3692702744e5cca174fcae55ea7b9d34e72998
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/06/2019
ms.locfileid: "70831053"
---
# <a name="mainframe-migration-overview"></a>Översikt över stordator migrering

Många företag och organisationer drar nytta av att flytta några eller alla sina stordatorer, program och databaser till molnet. Azure tillhandahåller stordator funktioner i moln skala utan många av de nack delar som är kopplade till stordatorer.

Term stordatoren avser vanligt vis ett stort dator system, men den stora majoriteten för närvarande distribuerade stordatorer är IBM-system Z-servrar eller IBM plug-kompatibla system som kör MVS, DOS, VSE, OS/390 eller Z/OS. Stordator system fortsätter att användas i många branscher för att köra viktiga informations system, och de har en plats i mycket olika scenarier, t. ex. stora, höga volym intensiva IT-miljöer.

Genom att migrera till molnet kan företag modernisera sin infrastruktur. Med moln tjänster kan du göra stordator program och det värde som de tillhandahåller, tillgängligt som en arbets belastning när din organisation behöver det. Många arbets belastningar kan överföras till Azure med bara smärre kod ändringar, till exempel uppdatering av namn på databaser. Du kan migrera mer komplexa arbets belastningar med hjälp av en stegvis metod.

De flesta Fortune 500-företag kör redan Azure för sina kritiska arbets belastningar. Azures betydelsefulla nedre rad incitament motiverar många migrerings projekt. Företag flyttar vanligt vis utvecklings-och test arbets belastningar till Azure först, följt av DevOps, e-post och haveri beredskap som en tjänst.

## <a name="intended-audience"></a>Målgrupp

Om du överväger att använda en migrering eller lägga till moln tjänster som ett alternativ för din IT-miljö är den här guiden för dig.

Den här vägledningen hjälper IT-organisationer att starta migrerings konversationen. Du kanske är bekant med Azure och molnbaserade infrastrukturer än du använder stordatorer, så den här guiden börjar med en översikt över hur stordatorer fungerar och fortsätter med olika strategier för att avgöra vad och hur du ska migrera.

## <a name="mainframe-architecture"></a>Stordator arkitektur

I den sena 1950s har stordatorer utformats som skalbara servrar för att köra hög volym onlinetransaktioner och batchbearbetning. Därför har stordatorer program för online transaktions formulär (ibland kallade gröna skärmar) och I/O-system med höga prestanda för bearbetning av batch-körningar.

Stordatorer har ett rykte för hög tillförlitlighet och tillgänglighet och är känt för att kunna köra enorma onlinetransaktioner och batch-jobb. Ett transaktions resultat från en bearbetnings enhet som initieras av en enskild begäran, vanligt vis från en användare i en Terminal. Transaktioner kan också komma från flera andra källor, t. ex. webb sidor, fjärrarbetsstationer och program från andra informations system. En transaktion kan också aktive ras automatiskt vid en fördefinierad tid enligt följande bild.

![Komponenter i en typisk IBM-stordator arkitektur](../../_images/mainframe-migration/zOS-architectural-layers.png)

En typisk IBM-stordator arkitektur innehåller följande vanliga komponenter:

- **Klient dels system:** Användare kan initiera transaktioner från terminaler, webb sidor eller fjärrdatorer. Stordator program har ofta anpassade användar gränssnitt som kan bevaras efter migrering till Azure. Terminal-emulatorer används fortfarande för att få åtkomst till stordator program och kallas även för gröna skärms anslutningar.

- **Program nivå:** Stordatorer innehåller vanligt vis ett CICS (Customer information Control system), en ledande transaktions hanterings paket för IBM z/OS-stordatoren som ofta används med IBM information management system (IMS), en Message-baserad transaktions hanterare. Batch-system hanterar data uppdateringar med höga data flöden för stora volymer med konto poster.

- **Rikt** Programmeringsspråk som används av stordatorer omfattar COBOL, Fortran, PL/I och naturlig. Jobb kontroll språk (JCL) används för att arbeta med z/OS.

- **Databas nivå:** Ett gemensamt Relations databas hanterings system (DBMS) för z/OS är IBM DD2. Den hanterar data strukturer med namnet *dbspaces* som innehåller en eller flera tabeller och tilldelas till lagringspooler för fysiska data uppsättningar som kallas *dbextents*. Två viktiga databas komponenter är den katalog som identifierar data platser i lagringspooler och den logg som innehåller en post med åtgärder som utförs på databasen. Det finns stöd för olika data format med Flat-filer. DB2 for z/OS använder vanligt vis VSAM-datauppsättningar (Virtual Storage Access Method) för att lagra data.

- **Hanterings nivå:** IBM-stordatorer innehåller schemaläggning av program vara som TWS-OPC, verktyg för utskrifts-och hanterings hantering, till exempel CA-SAR och buffert och ett käll kontroll system för kod. Säker åtkomst kontroll för z/OS hanteras av resurs åtkomst kontrolls funktionen (RACF). En databas hanterare ger åtkomst till data i databasen och körs i en egen partition i en z/OS-miljö.

- **LPAR:** Logiska partitioner eller LPARs används för att dela upp beräknings resurser. En fysisk stordator är partitionerad i flera LPARs.

- **z/OS:** Ett 64-bitars operativ system som vanligt vis används för IBM-stordatorer.

IBM-system använder en transaktions Övervakare som CICS för att spåra och hantera alla aspekter av en affärs transaktion. CICS hanterar delning av resurser, integriteten för data och prioritering av körning. CICS auktoriserar användare, tilldelar resurser och skickar databas begär Anden från programmet till en databas hanterare, till exempel IBM DB2.

För mer exakt justering används CICS ofta med IMS/TM (tidigare IMS/data Communications eller IMS/DC). IMS har utformats för att minska dataredundans genom att underhålla en enda kopia av data. Den kompletterar CICS som en transaktions övervakare genom att underhålla tillstånd under hela processen och registrera affärs funktioner i ett data lager.

## <a name="mainframe-operations"></a>Stordator åtgärder

Följande är typiska stordator åtgärder:

- **Onlinemallar** Arbets belastningar omfattar transaktions bearbetning, databas hantering och anslutningar. De implementeras ofta med hjälp av IBM DB2, CICS och z/OS-anslutningar.

- **Batchuppgiften** Jobb körs utan användar interaktion, vanligt vis enligt ett regelbundet schema som varje morgon dag. Batch-jobb kan köras på system baserade på Windows eller Linux med hjälp av en JCL-emulator, till exempel Micro Focus Enterprise Server eller BMC Control-M program vara.

- **Jobb kontroll språk (JCL):** Ange de resurser som krävs för att bearbeta batch-jobb. JCL förmedlar denna information till z/OS via en uppsättning jobb kontrolls instruktioner. Basic-JCL innehåller sex typer av uttryck: JOB, ASSGN, DLBL, ALLOKERINGSUTRYMMET, LIBDEF och EXEC. Ett jobb kan innehålla flera EXEC-instruktioner (steg) och varje steg kan ha flera LIBDEF-, ASSGN-, DLBL-och OMFATTNINGs-instruktioner.

- **Första program belastning (IPL):**  Syftar på att läsa in en kopia av operativ systemet från disk till en processors faktiska lagring och köra den. IPLs används för att återställa efter stillestånds tid. En IPL är som att starta operativ systemet på virtuella Windows-eller Linux-datorer.

## <a name="next-steps"></a>Nästa steg

> [!div class="nextstepaction"]
> [Myths och fakta](myths-and-facts.md)
