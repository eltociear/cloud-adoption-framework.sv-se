---
title: Översikt över stordatormigrering
description: Migrera arbetsbelastningar, appar och databaser för stordatorer till Azure för att få en pålitlig och skalbar infrastruktur med hög tillgänglighet utan många av de nackdelar som kommer med stordatorer.
author: njray
ms.author: v-nanra
ms.date: 12/27/2018
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 9d11c3954bb97d14c5ee4c59e27013cff7e8cf7a
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/31/2020
ms.locfileid: "80425547"
---
<!-- cSpell:ignore nanra njray dbspaces dbextents VSAM RACF LPARS ASSGN DLBL EXTENT LIBDEF EXEC IPLs -->

# <a name="mainframe-migration-overview"></a>Översikt över stordatormigrering

Många företag och organisationer drar nytta av att flytta några eller alla sina stordatorer, program och databaser till molnet. Azure tillhandahåller stordatorfunktioner i molnskala utan många av de nackdelar som är kopplade till stordatorer.

Termen stordator avser generellt ett stort datorsystem, men majoriteten av distribuerade stordatorer är för närvarande IBM System Z-servrar eller IBM-anslutningskompatibla system som kör MVS, DOS, VSE, OS/390 eller z/OS. Stordatorsystem fortsätter att användas i många branscher för att köra viktiga informationssystem, och de fyller en funktion i många mycket specifika scenarier som stora transaktionsintensiva IT-miljöer med höga volymer.

Genom att migrera till molnet kan företag modernisera sin infrastruktur. Med molntjänster kan du göra stordatorprogram och det värde som de tillhandahåller, tillgängliga som en arbetsbelastning när din organisation behöver det. Många arbetsbelastningar kan överföras till Azure med bara mindre kodändringar, till exempel uppdatering av namn på databaser. Du kan migrera mer komplexa arbetsbelastningar med hjälp av en stegvis metod.

De flesta Fortune 500-företag kör redan Azure för sina kritiska arbetsbelastningar. Azures betydelsefulla incitament motiverar många migreringsprojekt. Företag flyttar vanligtvis utvecklings- och testarbetsbelastningar till Azure först, följt av DevOps, e-post och haveriberedskap som en tjänst.

## <a name="intended-audience"></a>Målgrupp

Om du överväger en migrering eller att lägga till molntjänster som ett alternativ för din IT-miljö är den här guiden för dig.

Den här guiden hjälper IT-organisationer att börja diskutera en migrering. Du kanske är mer bekant med Azure och molnbaserade infrastrukturer än stordatorer, så den här guiden börjar med en översikt över hur stordatorer fungerar och fortsätter med olika strategier för att avgöra vad och hur du ska migrera.

## <a name="mainframe-architecture"></a>Stordatorarkitektur

I slutet av 50-talet utformades stordatorer som skalbara servrar för att köra onlinetransaktioner och batchbearbetning av stora volymer. Därför har stordatorer program för onlinetransaktionsformulär (kallas ibland grönskärmar) och I/O-system med höga prestanda för bearbetning av batch-körningar.

Stordatorer har ett rykte om sig att vara mycket tillförlitliga och tillgängliga, och de är kända för att kunna köra enorma onlinetransaktioner och batchjobb. Ett transaktionsresultat från en bearbetning som initierats av en enskild begäran, vanligtvis från en användare i en terminal. Transaktioner kan också komma från flera andra källor, t. ex. webbsidor, fjärrarbetsstationer och program från andra informationssystem. En transaktion kan också aktiveras automatiskt en fördefinierad tid enligt följande bild.

![Komponenter i en typisk IBM-stordatorarkitektur](../../_images/mainframe-migration/mainframe-architecture.png)

En typisk IBM-stordatorarkitektur innehåller följande vanliga komponenter:

- **Klientdelssystem:** Användare kan initiera transaktioner från terminaler, webbsidor eller fjärrdatorer. Stordatorprogram har ofta anpassade användargränssnitt som kan bevaras efter en migrering till Azure. Terminalemulatorer (kallas även för grönskärmsanslutningar) används fortfarande för att få åtkomst till stordatorprogram.

- **Programnivå:** Stordatorer innehåller vanligt vis ett CICS (Customer information Control System), ett ledande transaktionshanteringspaket för IBM z/OS-stordatorn som ofta används med IBM Information Management System (IMS) som är en meddelandebaserad transaktionshanterare. Batchsystem hanterar datauppdateringar med stora dataflöden för stora volymer med kontoposter.

- **Kod:** Programmeringsspråken som används av stordatorer är COBOL, Fortran, PL/I och Natural. JCL (Job control language) används för z/OS.

- **Databasnivå:** Ett vanligt hanteringssystem för relationsdatabaser (DBMS) för z/OS är IBM DD2. Det hanterar datastrukturer med namnet *dbspaces* som innehåller en eller flera tabeller och är tilldelade till lagringspooler för fysiska datauppsättningar som kallas *dbextents*. Två viktiga databaskomponenter är den katalog som identifierar dataplatser i lagringspooler och den logg som innehåller en post med åtgärder som utförs på databasen. Det finns stöd för olika platta datafilformat. DB2 för z/OS använder vanligtvis VSAM-datauppsättningar (Virtual Storage Access Method) för att lagra data.

- **Hanteringsnivå:** IBM-stordatorer innehåller schemaläggning av programvara som TWS-OPC, verktyg för utskrifts-och utdatahantering, till exempel CA-SAR och SPOOL och ett källkontrollsystem för kod. Säker åtkomstkontroll för z/OS hanteras av RACF (resource access control facility). En databashanterare ger åtkomst till data i databasen och körs i en egen partition i en z/OS-miljö.

- **LPAR:** Logiska partitioner eller LPAR används för att dela upp beräkningsresurser. En fysisk stordator är partitionerad i flera LPAR:er.

- **z/OS:** Ett 64-bitars operativsystem som vanligtvis används för IBM-stordatorer.

IBM-system använder en transaktionsövervakare som CICS för att spåra och hantera alla aspekter av en affärstransaktion. CICS hanterar delning av resurser, dataintegritet och prioritering av körning. CICS auktoriserar användare, tilldelar resurser och skickar databasbegäranden från programmet till en databashanterare, till exempel IBM DB2.

För mer exakt justering används CICS ofta med IMS/TM (tidigare IMS/Data Communications eller IMS/DC). IMS har utformats för att minska dataredundans genom att underhålla en enda datakopia. Den kompletterar CICS som en transaktionsövervakare genom att upprätthålla tillstånd under hela processen och registrera affärsfunktioner i ett datalager.

## <a name="mainframe-operations"></a>Stordatoråtgärder

Följande är typiska stordatoråtgärder:

- **Online:** Arbetsbelastningar omfattar transaktionsbearbetning, databashantering och anslutningar. De implementeras ofta med hjälp av IBM DB2, CICS och z/OS-anslutningar.

- **Batch:** Jobb körs utan interaktion från användare, vanligtvis enligt ett regelbundet schema som varje vardagsmorgon. Batch-jobb kan köras på system som är baserade på Windows eller Linux med hjälp av en JCL-emulator, till exempel Micro Focus Enterprise Server eller programvaran BMC Control-M.

- **Job control language (JCL):** Ange de resurser som krävs för att bearbeta batch-jobb. JCL förmedlar informationen till z/OS via en uppsättning jobbkontrollsinstruktioner. Grundläggande JCL innehåller sex typer av instruktioner: JOB, ASSGN, DLBL, EXTENT, LIBDEF och EXEC. Ett jobb kan innehålla flera EXEC-instruktioner (steg) och varje steg kan ha flera LIBDEF-, ASSGN-, DLBL- och EXTENT-instruktioner.

- **Initial program load (IPL):**  Syftar på att läsa in en kopia av operativsystemet från disken till en processors faktiska lagring och köra den. IPL används för att återställa efter stilleståndstid. En IPL är som att starta operativsystemet på virtuella Windows-eller Linux-datorer.

## <a name="next-steps"></a>Nästa steg

> [!div class="nextstepaction"]
> [Myter och fakta](./myths-and-facts.md)
