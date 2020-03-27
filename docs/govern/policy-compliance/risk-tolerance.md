---
title: Utvärdera risktolerans
description: Förstå affärs riskerna som är kopplade till olika former av moln omvandling och sätt att utvärdera risk tolerans för en verksamhet.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.openlocfilehash: c96039183f50d0ff189dab04defda4fd1ba2e4fc
ms.sourcegitcommit: ea63be7fa94a75335223bd84d065ad3ea1d54fdb
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/27/2020
ms.locfileid: "80356926"
---
# <a name="evaluate-risk-tolerance"></a>Utvärdera risktolerans

Varje affärs beslut skapar nya risker. Att göra en investering i något skapar risk för förluster. Nya produkter eller tjänster skapar risker för marknads haverit. Ändringar av aktuella produkter eller tjänster kan minska marknads andelen. Moln omvandling tillhandahåller inte en Magical-lösning för vardagliga affärs risker. Till skillnad från anslutna lösningar (molnet eller lokalt) införs nya risker. När du distribuerar till gångar till en nätverksansluten anslutning expanderas även den potentiella hot profilen genom att exponera säkerhets svagheter för en mycket bredare, global community. Som tur är moln leverantörer medvetna om förändringar, ökningar och tillägg av risker. De investerar kraftigt för att minska och hantera riskerna för kundernas räkning.

Den här artikeln fokuserar inte på moln risker. I stället beskrivs de affärs risker som är kopplade till olika former av moln omvandling. Längre fram i artikeln flyttas diskussions fokus för att diskutera olika sätt att förstå affärs toleransen för risk.

<!-- markdownlint-disable MD026 -->

## <a name="what-business-risks-are-associated-with-a-cloud-transformation"></a>Vilka affärs risker är associerade med en moln omvandling?

Sanna affärs risker baseras på information om specifika transformeringar. Flera vanliga risker ger en konversations start för att förstå affärs specifika risker.

> [!IMPORTANT]
> Innan du läser följande bör du vara medveten om att var och en av dessa risker kan hanteras. Målet med den här artikeln är att informera och förbereda läsarna för mer produktiva riskhanterings diskussioner.

- **Data intrång:** Den största risken som är kopplad till en transformering är en data överträdelse. Data läckor kan orsaka betydande skador på företaget, vilket leder till förlust av kunder, minskad verksamhet eller till och med juridiskt ansvar. Ändringar av hur data lagras, bearbetas eller används skapar risker. Moln omvandlingar skapar en hög grad av ändring för data hantering, så risken bör inte beaktas lätt. [Säkerhets bas linjen](../security-baseline/index.md), [data klassificering](./data-classification.md)och [stegvisa rationalisering](../../digital-estate/rationalize.md#incremental-rationalization) kan användas för att hantera den här risken.

- **Avbrott i tjänsten:** Verksamhets-och kund upplevelser förlitar sig mycket på tekniska åtgärder. Moln omvandlingar kommer att skapa ändringar i IT-driften. I vissa organisationer är den här ändringen liten och enkelt justerad. I andra organisationer kan dessa ändringar kräva att du behöver göra om, träna om eller nya metoder för att stödja moln åtgärder. Den större ändringen, desto större är den potentiella effekten för affärs åtgärder och kund upplevelse. Att hantera den här risken kräver att verksamheten i omvandlings planeringen är inblandad. Versions planering och första arbets belastnings val i den [stegvisa rationalisering](../../digital-estate/rationalize.md#incremental-rationalization) artikeln diskuterar hur du väljer arbets belastningar för omvandlings projekt. Företagets roll i den aktiviteten är att kommunicera affärs verksamhetens risk för att ändra prioriterade arbets belastningar. Att hjälpa IT-avdelningen att välja arbets belastningar som har en lägre påverkan på verksamheten minskar den övergripande risken.

- **Budget kontroll:** Kostnads modeller ändras i molnet. Den här ändringen kan skapa risker som är kopplade till kostnads överskridningar eller ökar kostnaderna för sålda varor (KSV), särskilt direkt operativa utgifter. När verksamheten fungerar nära varandra är det möjligt att skapa genomskinlighet för kostnader och tjänster som används av olika affär senheter, program eller projekt. [Cost Management](../cost-management/index.md) innehåller exempel på affärs möjligheter och det kan partner på det här ämnet.

Ovanstående är några av de vanligaste riskerna som anges av kunderna. Moln styrnings teamet och moln implementerings teamen kan börja utveckla en risk profil, eftersom arbets belastningar migreras och blir tillgängliga för produktions versionen. Förbereds för konversationer för att definiera, förfina och hantera risker utifrån önskade affärs resultat och omvandlings arbete.

## <a name="understand-risk-tolerance"></a>Förstå risk tolerans

Identifierings risken är en ganska direkt process. IT-relaterade risker är vanligt vis standard i hela branscher. Toleransen för dessa risker är dock unik för varje organisation. Det här är den punkt där affärs-och IT-konversationer tenderar att sätta igång. Varje sida av konversationen talar i grunden om ett annat språk. Följande jämförelser och frågor är utformade för att starta konversationer som hjälper varje part att bättre förstå och beräkna risk tolerans.

## <a name="simple-use-case-for-comparison"></a>Enkelt användnings fall för jämförelse

För att förstå risk toleransen undersöker vi kund information. Om ett företag i någon bransch publicerar kund information på en oskyddad Server, är den tekniska risken för dessa data komprometterad eller stulen, ungefär detsamma. Ett företags tolerans för denna risk kommer dock att variera i naturen utifrån arten och det potentiella värdet av data.

- Företag inom hälso vård och finansiering i USA regleras av stela krav på tredje parts efterlevnad. Det förutsätts att personliga data eller hälso vårds data är mycket konfidentiella. Det finns allvarliga konsekvenser för dessa typer av företag, om de ingår i risk scenariot ovan. Deras tolerans är extremt låg. Alla kund uppgifter som publiceras i eller utanför nätverket måste regleras av dessa efterlevnadsprinciper för tredje part.
- Ett spel företag vars kund information är begränsad till ett användar namn, uppspelnings tider och höga poäng är inte lika bra som om det uppstår avsevärda följder för att förlora viktiga konsekvenser, om de bedriver risk beteendet ovan. Även om osäkra data är utsatta för risk, är effekten av denna risk liten. Därför är toleransen för risk i det här fallet hög.
- Ett medel stort företag som tillhandahåller rengörings tjänster för mattor till tusentals kunder skulle ligga mellan dessa två tolerans extrema. Kundernas data kan vara mer robusta och innehåller information som adress eller telefonnummer. Båda kan betraktas som personliga data och bör skyddas. Det kan dock hända att det inte finns några speciella styrnings krav som kräva att data skyddas. Från ett IT-perspektiv är svaret enkelt och skyddar data. Från ett affärs perspektiv är det inte lika enkelt. Företaget skulle behöva mer information innan de kunde fastställa en tolerans nivå för den här risken.

Nästa avsnitt delar några exempel frågor som kan hjälpa företaget att fastställa en risk tolerans för användnings fallet ovan eller andra.

## <a name="risk-tolerance-questions"></a>Risk tolerans frågor

Det här avsnittet innehåller en lista över konversationer med frågor i tre kategorier: förlust påverkan, sannolikhet för förlust och reparations kostnader. När affärs-och IT-partner kan hantera vart och ett av dessa områden, kan beslutet att utnyttja hanteringen av risker och den övergripande toleransen för en viss risk enkelt fastställas.

**Förlust påverkan:** Frågor för att fastställa effekten av en risk. Dessa frågor kan vara svåra att besvara. Det är bäst att kvantifiera påverkan, men ibland är enbart konversationen tillräckligt för att förstå toleransen. Intervall är också acceptabla, särskilt om de innehåller antaganden som fastställt dessa intervall.

- Kan den här risken bryta mot krav från tredje parts efterlevnad?
- Kan den här risken kränka interna företags principer?
- Kan den här risken orsaka förlust av livs längd, Limb eller egendom?
- Gick det att använda risk kostnader för kunder eller marknads andelar? I så fall, kan den här kostnaden kvantifieras?
- Kan den här risken skapa negativa kund upplevelser? Kommer de erfarenheter att påverka försäljningen eller intäkterna?
- Kan den här risken skapa ny juridisk ansvar? I så fall, finns det en prioritet för skade belöningar i dessa typer av fall?
- Kan den här risken stoppa affärs åtgärder? I så fall, hur länge skulle åtgärdas?
- Kan den här risken sakta ned affärs verksamhet? I så fall, hur långsamt och hur länge?
- I det här steget i omvandlingen är det en risk eller kommer den att upprepas?
- Ökar eller minskar risken i frekvens när omvandlingen fortskrider?
- Ökar risken för risken eller minskningen av tiden?
- Är risk tiden känslig i natur? Kommer risken att lyckas eller bli sämre om den inte åtgärdas?

De här grundläggande frågorna leder till många fler. När du har utforskat en felfria dialog, rekommenderar vi att de relevanta riskerna registreras och när det är möjligt att kvantifiera dem.

**Kostnader för risk reparation:** Frågor för att fastställa kostnaden för att ta bort eller på annat sätt minimera risken. Dessa frågor kan vara ganska direkta, särskilt när de visas i ett intervall.

- Finns det en tydlig lösning och vad kostar det?
- Finns det alternativ för att förhindra eller minimera den här risken? Vad är intervallet för kostnader för de här lösningarna?
- Vad behövs från företaget för att välja den bästa, tydliga lösningen?
- Vad behövs från företaget för att validera kostnader?
- Vilka andra fördelar kan komma från lösningen som tar bort den här risken?

Dessa frågor för att förenkla de tekniska lösningar som krävs för att hantera eller ta bort risker. Dessa frågor kommunicerar dock med dessa lösningar på ett sätt som gör att verksamheten snabbt kan integreras i en besluts process.

**Sannolikhet för förlust:** Frågor för att avgöra hur sannolikt det är att risken blir en verklighet. Detta är den svåraste arean att kvantifiera. I stället rekommenderar vi att gruppen moln styrning skapar kategorier för att kommunicera sannolikheten, baserat på stödjande data. Följande frågor kan hjälpa dig att skapa kategorier som är meningsfulla för teamet.

- Har all referensinformation gjorts om sannolikheten för att denna risk realiseras?
- Kan leverantören tillhandahålla referenser eller statistik om sannolikheten för en effekt?
- Finns det andra företag i den aktuella sektorn eller vertikala som har nåtts av den här risken?
- Titta vidare, finns det andra företag i allmänhet som har nått den här risken?
- Är den här risken unik för något som företaget har utfört dåligt?

Efter att ha besvarat dessa frågor och frågor som bestäms av moln styrnings teamet, kommer grupperingar av sannolikhet att bli sannolika. Nedan följer några exempel på hur du kan komma igång:

- **Ingen indikation:** Inte tillräckligt med forskning har slutförts för att fastställa sannolikheten.
- **Låg risk:** Den aktuella forskningen indikerar att det är osannolikt att risken är riktig.
- **Framtida risk:** Den aktuella sannolikheten är låg. Fortsatta antagande skulle dock kräva en ny analys.
- **Medel risk:** Det är sannolikt att risken kommer att påverka verksamheten.
- **Hög risk:** Med tiden är det allt mer troligt att verksamheten kommer att inse denna risk.
- **Avböj risk:** Risken är medel hög till hög. Åtgärder i den eller verksamheten minskar dock sannolikheten för en effekt.

**Fastställer tolerans:**

De tre frågorna ovan bör vara tillräckligt stora för att fastställa de ursprungliga toleranserna. När risken och sannolikheten är låga, och kostnaderna för risk reparation är höga, är det inte troligt att verksamheten investeras i reparationen. När risken och sannolikheten är höga är det troligt att verksamheten kommer att överväga en investering, så länge kostnaderna inte överstiger de potentiella riskerna.

## <a name="next-steps"></a>Nästa steg

Den här typen av konversation kan hjälpa företaget och utvärdera toleransen mer effektivt. Dessa konversationer kan användas när du skapar MVP-principer och under stegvisa princip granskningar.

> [!div class="nextstepaction"]
> [Definiera företags princip](./policy-definition.md)
