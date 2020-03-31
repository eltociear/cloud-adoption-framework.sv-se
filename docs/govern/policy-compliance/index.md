---
title: Förbereda företagets IT-policy för molnet
description: Hjälp till att aktivera en utökad styrningsmodell med viktiga aktiviteter som stegvisa förändringar av företagsprinciper och automatiserad tillämpning.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 7d22bb4b4bae04366c61686862d1ae437185886d
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/31/2020
ms.locfileid: "80433520"
---
<!-- markdownlint-disable MD026 -->

# <a name="prepare-corporate-it-policy-for-the-cloud"></a>Förbereda företagets IT-policy för molnet

Molnstyrning är resultatet av ett kontinuerligt implementeringsarbete över tid, eftersom en långvarig omvandling inte sker på en dag. Försök att leverera en komplett molnstyrning innan viktiga ändringar av företagspolicy har åtgärdats med hjälp av en snabb och aggressiv metod ger sällan önskat resultat. Vi rekommenderar i stället en stegvis metod.

Det som är annorlunda med vårt Cloud Adoption Framework är inköpscykeln och hur den kan aktivera autentisk omvandling. Eftersom det inte finns något krav på förvärv med stora kapitalutgifter kan ingenjörer börja experimentera och implementera tidigare. I de flesta företagskulturer kan eliminering av kapitalinvesteringar som hindrar implementering leda till kortare feedbackloopar, organisk tillväxt och inkrementellt genomförande.

Övergången till molnimplementering kräver en förändring i styrningen. I många organisationer möjliggör omvandling av företagspolicy förbättrad styrning och bättre efterlevnad via inkrementella policyändringar och automatiserat framtvingande av dessa ändringarna, som drivs av nyligen definierade funktioner som du konfigurerar med din molntjänstleverantör.

Den här artikeln beskriver viktiga aktiviteter som kan hjälpa dig utforma dina företagspolicyer för att möjliggöra en utökad styrningsmodell.

## <a name="define-corporate-policy-to-mature-cloud-governance"></a>Definiera företagspolicy för att göra molnstyrningen mognare

Inom traditionell styrning och inkrementell styrning skapar företagspolicy arbetsdefinitionen av styrning. De flesta IT-styrningsåtgärder syftar till att implementera teknik för att övervaka, framtvinga, driva och automatisera dessa företagspolicyer. Molnstyrning bygger på liknande begrepp.

![Företagsstyrning och styrningsområden](../../_images/operational-transformation-govern-highres.png)

*Bild 1 – Företagsstyrning och styrningsområden.*

Bilden ovan visar interaktionerna mellan affärsrisk, policy och efterlevnad samt övervakning och framtvingande för att skapa en styrningsstrategi. Detta följs av den fem områdena för molnstyrning för att omsätta din strategi i praktiken.

## <a name="review-existing-policies"></a>Granska befintliga principer

I bilden ovan börjar styrningsstrategin (risk, policy och efterlevnad samt övervakning och framtvingande) med att identifiera affärsrisker. Att förstå hur [affärsrisker](./business-risk.md) ändras i molnet är det första steget mot att skapa en bestående strategi för molnstyrning. Genom att arbeta med dina affärsenheter för att få en korrekt [uppskattning av företagets risktolerans](./risk-tolerance.md) får du en förståelse för vilka risknivåer som behöver åtgärdas. Din förståelse av nya risker och godtagbar tolerans kan ge upphov till en [granskning av befintliga policyer](./cloud-policy-review.md) i syfte att fastställa den styrningsnivå som krävs och är lämplig för organisationen.

> [!TIP]
> Om din organisation styrs av tredjepartsefterlevnad kan en av de största företagsriskerna att beakta vara en risk vad gäller efterlevnad av [regelkrav](./regulatory-compliance.md). Den här risken kan ofta inte åtgärdas och kräver i stället strikt efterlevnad. Var noga med att förstå kraven för tredjepartsefterlevnad innan du påbörjar en policygranskning.

## <a name="an-incremental-approach-to-cloud-governance"></a>En inkrementell molnstyrningsstrategi

I en inkrementell molnstyrningsstrategi accepteras inte överträdelser av [företagets risktoleransnivå](./risk-tolerance.md). I stället förutsätter den att styrningens roll innebär att påskynda företagsändring, hjälpa ingenjörer att förstå riktlinjer för arkitektur samt säkerställa att [affärsrisker](./business-risk.md) regelbundet kommuniceras och åtgärdas. Alternativt kan den traditionella styrningsrollen bli ett hinder för implementering av ingenjörer eller av företaget som helhet.

Med en inkrementell molnstyrningsstrategi förekommer det ibland vissa naturliga motsättningar mellan team som skapar nya företagslösningar och team som skyddar företaget från risker. I den här modellen kan dock dessa två team bli samarbetspartner i arbetet med inkrement eller sprints. Som samarbetspartner börjar molnstyrningsteamet och molnimplementeringsteamet att tillsammans exponera, utvärdera och åtgärda affärsrisker. Detta arbete kan utgöra ett naturligt sätt att minska motsättningarna skapa samstämmighet mellan teamen.

## <a name="minimum-viable-product-mvp-for-policy"></a>MVP (Minimum Viable Product) för principen

Det första steget i ett framväxande samarbete mellan teamen för molnstyrning respektive molnimplementering är ett avtal gällande policy-MVP. Din MVP för molnstyrning bör beakta att affärsriskerna är små till en början men sannolikt växer allt eftersom organisationen implementerar fler molntjänster med tiden.

Till exempel är företagsrisken liten för ett företag som distribuerar fem virtuella datorer som inte innehåller HBI-data (High Business Impact). När antalet senare i processen för molnimplementering når 1 000 virtuella datorer och företaget börjar flytta HBI-data växer affärsrisken.

Policy-MVP försöker att definiera en obligatorisk grund för policyer som behövs för att distribuera de första _x_ virtuella datorerna eller de första _x_ programmen, där _x_ är ett litet men meningsfullt antal av de enheter som implementeras. Den här policyuppsättningen kräver några begränsningar, men innehåller de grundläggande aspekter som behövs för att snabbt växa från ett inkrementellt molnimplementeringsprojekt till nästa. Via inkrementell policyutveckling skulle den här styrningsstrategin växa med tiden. Genom långsamma, subtila ändringar skulle policy-MVP växa till funktionsparitet med resultatet av övningen med policygranskning.

## <a name="incremental-policy-growth"></a>Inkrementell policytillväxt

Inkrementell policytillväxt är nyckelmekanismen för att få policy- och molnstyrning av växa med tiden. Det är även huvudkravet för att implementera en inkrementell styrningsmodell. För att den här modellen ska kunna fungera väl måste styrningsteamet satsa på en löpande tidsallokering vid varje sprint för att utvärdera och implementera föränderliga styrningsområden.

**Tidskrav för sprints:** Vid början av varje iteration skapar varje team för molnimplementering en lista över tillgångar som ska migreras eller implementeras i det aktuella inkrementet. Molnstyrningsteamet förväntas avsätta tillräckligt med tid för att granska listan, validera dataklassificeringar för tillgångar, utvärdera eventuella nya risker som är associerade med varje tillgång, uppdatera riktlinjerna för arkitektur samt informera teamet om ändringarna. Dessa åtaganden kräver vanligtvis 10–30 timmar per sprint. För satsningen på den här nivån förväntas det även krävas minst en dedikerad medarbetare som hanterar styrning i ett stort projekt för molnimplementering.

**Tidskrav för lansering:** I början av varje lansering bör molnimplementeringsteamen och molnstrategiteamet prioritera en lista över program eller arbetsbelastningar som ska migreras i den aktuella iterationen samt eventuella affärsändringsaktiviteter. Dessa datapunkter gör att molnstyrningsteamet kan förstå nya affärsrisker i ett tidigt skede. Det gör i sin tur att tids finns för att rikta in med verksamheten och bedöma verksamhetens risktolerans.

## <a name="next-steps"></a>Nästa steg

Den effektiva strategin för molnstyrning börjar med att förstå affärsrisker.

> [!div class="nextstepaction"]
> [Förstå affärsrisker](./business-risk.md)
