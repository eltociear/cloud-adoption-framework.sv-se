---
title: Molnmigrering
description: Molnmigrering i Cloud Adoption Framework
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: landing-page
ms.service: cloud-adoption-framework
ms.subservice: migrate
layout: LandingPage
ms.openlocfilehash: 90a9c69b311f1d4687d2691af13c3b51a7b6f813
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 01/28/2020
ms.locfileid: "76802964"
---
# <a name="cloud-migration-in-the-cloud-adoption-framework"></a>Molnmigrering i Cloud Adoption Framework

Alla [molnimplementeringsplaner](../plan/index.md) i företagsskala inkluderar arbetsbelastningar som inte kräver några stora investeringar i skapandet av en ny affärslogik. Dessa arbetsbelastningar kan flyttas till molnet på flera olika sätt: lyfta och flytta, lyfta och optimera eller modernisera. Var och en av dessa metoder anses vara en migrering. Följande övningar hjälper dig att upprätta iterativa processer för att utvärdera, migrera, optimera, skydda och hantera dessa arbetsbelastningar.

## <a name="getting-started"></a>Komma igång

Om du vill förbereda dig för den här fasen av molnimplementeringens livscykel, föreslår ramverket följande fem övningar:

<!-- markdownlint-disable MD033 -->
<ul class="panelContent cardsF">
    <li style="display: flex; flex-direction: column;">
        <a href="./azure-migration-guide/prerequisites.md?tabs=Checklist">
            <div class="cardSize">
                <div class="cardPadding" style="padding-bottom:10px;">
                    <div class="card" style="padding-bottom:10px;">
                        <div class="cardImageOuter">
                            <div class="cardImage">
                                <img alt="" src="../_images/icons/1.png" data-linktype="external">
                            </div>
                        </div>
                        <div class="cardText" style="padding-left:0px;">
                            <h3>Förhandskrav för migrering</h3>
Verifiera att en landningszon har distribuerats och är redo att vara värd för de första arbetsbelastningarna som ska migreras till Azure. Om någon molnimplementeringsstrategi eller molnimplementeringsplan inte har skapats, så kontrollera att båda dessa är på gång.
                        </div>
                    </div>
                </div>
            </div>
        </a>
    </li>
    <li style="display: flex; flex-direction: column;">
        <a href="./azure-migration-guide/index.md">
            <div class="cardSize">
                <div class="cardPadding" style="padding-bottom:10px;">
                    <div class="card" style="padding-bottom:10px;">
                        <div class="cardImageOuter">
                            <div class="cardImage">
                                <img alt="" src="../_images/icons/2.png" data-linktype="external">
                            </div>
                        </div>
                        <div class="cardText" style="padding-left:0px;">
                            <h3>Migrera din första arbetsbelastning</h3>
Ta hjälp av Azure-migreringsguiden när du migrerar din första arbetsbelastning. Detta kan du bekanta dig med verktyg och metoder som krävs för implementeringen.
                        </div>
                    </div>
                </div>
            </div>
        </a>
    </li>
    <li style="display: flex; flex-direction: column;">
        <a href="./expanded-scope/index.md">
            <div class="cardSize">
                <div class="cardPadding" style="padding-bottom:10px;">
                    <div class="card" style="padding-bottom:10px;">
                        <div class="cardImageOuter">
                            <div class="cardImage">
                                <img alt="" src="../_images/icons/3.png" data-linktype="external">
                            </div>
                        </div>
                        <div class="cardText" style="padding-left:0px;">
                            <h3>Utökade migreringsscenarier</h3>
Utnyttja den utökade områdeschecklistan när du ska identifiera scenarier som kräver ändringar i din framtida tillståndsarkitektur, migreringsprocesser, landningszonskonfigurationer eller migreringverktygsbeslut.
                        </div>
                    </div>
                </div>
            </div>
        </a>
    </li>
    <li style="display: flex; flex-direction: column;">
        <a href="./azure-best-practices/index.md">
            <div class="cardSize">
                <div class="cardPadding" style="padding-bottom:10px;">
                    <div class="card" style="padding-bottom:10px;">
                        <div class="cardImageOuter">
                            <div class="cardImage">
                                <img alt="" src="../_images/icons/4.png" data-linktype="external">
                            </div>
                        </div>
                        <div class="cardText" style="padding-left:0px;">
                            <h3>Metodtips</h3>
Verifiera alla ändringar gentemot metodtipsavsnittet så att du säkerställer korrekt implementering av utökad omfattning eller arbetsbelastings-/arkitekturspecifika migreringstyper.
                        </div>
                    </div>
                </div>
            </div>
        </a>
    </li>
    <li style="display: flex; flex-direction: column;">
        <a href="./migration-considerations/index.md">
            <div class="cardSize">
                <div class="cardPadding" style="padding-bottom:10px;">
                    <div class="card" style="padding-bottom:10px;">
                        <div class="cardImageOuter">
                            <div class="cardImage">
                                <img alt="" src="../_images/icons/5.png" data-linktype="external">
                            </div>
                        </div>
                        <div class="cardText" style="padding-left:0px;">
                            <h3>Processförbättringar</h3>
Migration är en högaktivitetsprocess. När migreringsarbetet skalas kan du använda avsnittet om migreringsöverväganden för att utvärdera och reflektera över olika aspekter av dina processer.
                        </div>
                    </div>
                </div>
            </div>
        </a>
    </li>
</ul>
<!-- markdownlint-enable MD033 -->

## <a name="iterative-migration-process"></a>Iterativ migreringsprocess

I grunden kan migrering till molnet delas in i fyra enkla faser: Utvärdera, migrera, optimera samt skydda och hantera. I det här avsnittet om Cloud Adoption Framework lär du dig att maximera avkastningen från varje fas av processen och anpassa dessa faser till din molnimplementeringsplan. Följande bild illustrerar dessa faser ur ett iterativt perspektiv:

![Cloud Adoption Framework-migreringsmodellen](../_images/operational-transformation-migrate.png)

## <a name="create-a-balanced-cloud-portfolio"></a>Skapa en balanserad molnportfölj

En balanserad teknikportfölj har en blandning av tillgångar i olika tillstånd. Vissa program schemaläggs att tas ur bruk och ges minimal support. Andra program eller tillgångar stöds i ett underhållstillstånd, men funktionerna i dessa lösningar är stabila. För nyare affärsprocesser kommer föränderliga marknadsvillkor sannolikt motivera pågående funktionsförbättringar eller modernisering. När det uppstår möjligheter att skapa nya intäktsströmmar introduceras nya program eller tillgångar i miljön. I varje steg i livscykeln för en tillgång ändras den påverkan som investering har på intäkter och vinster. Ju senare livscykelsteget är, desto mindre troligt är det att en ny funktion eller ett moderniseringsprojekt ger god avkastning på investeringar.

Molnet ger olika implementeringsmekanismer som var och en har liknande grader av investering och avkastning. Skapande av molnbaserade program kan avsevärt minska driftskostnaderna. När ett molnbaserat program lanseras kan utvecklingen av nya funktioner och lösningar itereras snabbare. Modernisering av ett program kan ge liknande fördelar genom att äldre begränsningar som är associerade med lokala utvecklingsmodeller elimineras. Tyvärr är dessa två metoder arbetsintensiva beroende av storleken, kompetensen och erfarenheten hos programutvecklingsteamen. Ofta arbetar personer med fel uppgifter – personer med färdigheter och förmåga att modernisera program skulle hellre skapa nya program. På en arbetsmarknad där det är svårt att hitta rätt kompetens kan storskaliga moderniseringsprojekt drabbas av problem med medarbetarnas nöjdhet och kompetens. I en balanserad portfölj bör den här metoden reserveras för program som skulle få betydande funktionsförbättringar om de behölls lokalt.

## <a name="envision-an-end-state"></a>Föreställ dig ett slutresultat

En effektiv resa behöver ett mål. Formulera en övergripande vision av slutresultatet innan du tar det första steget. Den här infografiken beskriver en startpunkt som består av befintliga program, data och infrastruktur, som definierar den digitala egendomen. Under migreringsprocessen övergår varje tillgång via ett av alternativen till höger.

## <a name="migration-implementation"></a>Implementering av migrering

De här artiklarna beskriver två resor, var och en med ett liknande mål – att migrera en stor andel av befintliga resurser till Azure. Dock påverkar affärsresultatet och det aktuella tillståndet avsevärt de processer som krävs för att nå dit. Dessa mindre avvikelser resulterar i två mycket olika tillvägagångssätt för att nå ett liknande sluttillstånd.

![Cloud Adoption Framework-migreringsmodellen](../_images/operational-transformation-migrate.png)

För att vägleda det inkrementella genomförandet under övergången till sluttillståndet separerar den här modellen migrering i två fokusområden.

**Förberedelser för migrering:** Upprätta en ungefärlig uppgiftslista för migrering baserat huvudsakligen på det aktuella tillståndet och önskade resultat.

- **Affärsresultat:** De viktiga affärsmål som driver den här migreringen.
- **Beräkning av digital egendom:** En grov uppskattning av antalet av och villkor för arbetsbelastningar som ska migreras.
- **Roller och ansvarsområden:** En tydlig definition av teamstrukturen, avgränsning av ansvarsområden och åtkomstkrav.
- **Krav för ändringshantering:** Den uppdateringstakt, de processer och den dokumentation som krävs för att granska och godkänna ändringar.

Dessa inledande indata formar uppgiftslistan för migrering. Utdata från uppgiftslistan för migrering är en prioriterad lista med program som ska migreras till molnet. Listan formar genomförandet av processen för molnmigrering. Med tiden utökas den till att även omfatta mycket av den dokumentation som behövs för att hantera ändringar.

**Migreringsprocess:** Varje aktivitet för molnmigrering finns i någon av följande processer såsom den relaterar till uppgiftslistan för migrering.

- **Utvärdera:** Utvärdera en befintlig tillgång och upprätta en plan för migrering av tillgången.
- **Migrera:** Replikera funktionen för en tillgång i molnet.
- **Optimera:** Balansera prestanda, kostnad, åtkomst och driftskapacitet för en molntillgång.
- **Skydda och hantera:** Se till att en molntillgång är redo för pågående åtgärder.

Den information som samlas in under utvecklingen av en uppgiftslista för migrering avgör den komplexitet och arbetsinsats som krävs under processen för molnmigrering i varje iteration och för varje funktionslansering.

## <a name="transition-to-the-end-state"></a>Övergång till sluttillståndet

Målet är en smidig och delvis automatiserad migrering till molnet. Migreringsprocessen använder de verktyg som tillhandahålls av en molnleverantör för att snabbt replikera och mellanlagra tillgångar i molnet. När användare har verifierats omdirigeras de av en enkel nätverksändring till molnlösningen. För många användningsfall är tekniken för att uppnå det här målet till största delen tillgänglig. Det finns exempelfall som visar den hastighet med vilken 10 000 virtuella datorer kan replikeras i Azure.

En inkrementell migreringsmetod krävs dock fortfarande. I de flesta miljöer måste den långa listan över virtuella datorer som ska migreras delas upp i mindre arbetsenheter för att migreringen ska lyckas. Det finns många faktorer som begränsar det antal virtuella datorer som kan migreras under en viss period. Den utgående nätverkshastigheten är en av de få tekniska begränsningar som finns – de flesta begränsningar beror på verksamhetens förmåga att validera och anpassa sig till förändring.

Den inkrementella migreringsmetoden i Cloud Adoption Framework underlättar skapandet av en inkrementell plan som speglar och dokumenterar tekniska och kulturella begränsningar. Målet med den här modellen är att maximera migreringshastigheten och minimera merarbete för både IT och företaget. Nedan ges två exempel på ett inkrementellt migreringsgenomförande som baseras på uppgiftslistan för migrering.

<!-- markdownlint-disable MD033 -->

<ul class="panelContent cardsZ">
<li style="display: flex; flex-direction: column;">
    <a href="./azure-migration-guide/index.md" style="display: flex; flex-direction: column; flex: 1 0 auto;">
        <div class="cardSize" style="flex: 1 0 auto; display: flex;">
            <div class="cardPadding" style="display: flex;">
                <div class="card">
                    <div class="cardText">
                        <h3>Guide för Azure-migrering</h3>
                        <p><b>Sammanfattning av berättelse:</b> Den här kunden migrerar färre än 1 000 virtuella datorer. Färre än tio program som stöds ägs av en programägare som inte är i IT-organisationen. Återstående program, virtuella datorer och associerade data ägs och stöds av medlemmar i teamet för molnimplementering. Medlemmar i teamet för molnimplementering har administrativ åtkomst till produktionsmiljöerna i det befintliga datacentret.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li style="display: flex; flex-direction: column;">
    <a href="./expanded-scope/index.md" style="display: flex; flex-direction: column; flex: 1 0 auto;">
        <div class="cardSize" style="flex: 1 0 auto; display: flex;">
            <div class="cardPadding" style="display: flex;">
                <div class="card">
                    <div class="cardText">
                        <h3>Guide för komplext scenario</h3>
                        <p><b>Sammanfattning av berättelse:</b> Den här kundens migrering har komplexitet inom verksamheten, kulturen och tekniken. Den här guiden innehåller flera utmaningar med specifik komplexitet och metoder för att övervinna dessa utmaningar.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
</ul>

<!-- markdownlint-enable MD033 -->

Dessa två resor representerar två extremlägen av upplevelsen för kunder som investerar i migrering. De flesta företag har en kombination av de två scenarierna ovan. När du har granskat resan använder du Cloud Adoption Framework-migreringsmodellen för att påbörja migreringskonversationen och ändra baslinjeresorna för att bättre uppfylla dina behov.

## <a name="next-steps"></a>Nästa steg

Välj någon av dessa resor:

> [!div class="nextstepaction"]
> [Guide för Azure-migrering](./azure-migration-guide/index.md)
>
> [Guiden för utökat omfång](./expanded-scope/index.md)
