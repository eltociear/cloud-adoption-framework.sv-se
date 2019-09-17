---
title: 'Styrnings guide för komplexa företag: De underordnade'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Detta upprättar ett användnings fall för styrning under ett komplext företags moln införande resa.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 0d1aaa76f36125819ebb8f5c6225dc74bb60aabf
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/16/2019
ms.locfileid: "71030178"
---
# <a name="governance-guide-for-complex-enterprises-the-supporting-narrative"></a>Styrnings guide för komplexa företag: De underordnade

Följande bevarar upprättar ett användnings fall för [styrning under en stor företags moln införande resa](./index.md). Innan du följer rekommendationerna i guiden är det viktigt att förstå de antaganden och den anledning som visas i den här informationen. Sedan kan du bättre justera styrnings strategin till din organisations moln införande resa.

## <a name="back-story"></a>Bak text

Kunderna är krävande för att interagera med det här företaget. Den aktuella upplevelsen orsakade marknads-och utgångs punkt till kortet att anställa ett CDO (Chief Digital officer). CDO arbetar med marknadsföring och försäljning för att driva en digital omvandling som kan förbättra upplevelsen. Dessutom har flera affär senheter nyligen anskaffat data experter för att ställa in data på Server gruppen och förbättra många av de manuella upplevelserna genom inlärning och förutsägelse. DEN har stöd för dessa ansträngningar där det kan. Det finns dock "skugga IT"-aktiviteter som ligger utanför de nödvändiga styrnings-och säkerhets kontrollerna.

IT-organisationen är också riktad mot sina egna utmaningar. Finans planeras fort löp ande minskning i IT-budgeten under de kommande fem åren, vilket leder till att vissa nödvändiga utgifter för utgifter börjar gälla under året. GDPR och andra data suveränitets krav tvingar IT-investeringar att investera i till gångar i ytterligare länder för att lokalisera data. Två av de befintliga data centren är försenade för maskin varu uppdateringar, vilket orsakar ytterligare problem med anställda och kund tillfredsställelse. Tre fler data Center kräver uppdateringar av maskin vara under genomförandet av fem års planen. Ekonomi chefen är i kontakt med att ta hänsyn till molnet som ett alternativ för dessa data Center för att frigöra kapital utgifter.

Informations chefen har innovativa idéer som kan hjälpa företaget, men hon och hennes team är begränsade till att bekämpa bränder och kontrol lera kostnader. I en Luncheon med CDO och en av affär senhets ledarna, genererade Cloud migration-konversationen intresse från CHEFens kollegor. De tre ledarna syftar till att stödja varandra med hjälp av molnet för att uppnå sina affärs mål, och de har börjat utforska-och planerings faserna för moln införande.

## <a name="business-characteristics"></a>Företagsegenskaper

Företaget har följande affärs profil:

- Sales och Operations sträcker sig över flera geografiska områden med globala kunder på flera marknader.
- Verksamheten är i drift genom förvärv och fungerar över tre affär senheter baserat på mål kund basen. Budgetering är en komplex matris över affär senheter och-funktioner.
- De flesta affärsvyer som en kapital dränering eller ett kostnads ställe.

## <a name="current-state"></a>Aktuellt tillstånd

Här är det aktuella läget för företagets IT-och moln åtgärder:

- DET fungerar mer än 20 privat ägda data center runtom i världen.
- På grund av ekologisk tillväxt och flera geografiska områden finns det några IT-team som har unika krav på data suveränitet och efterlevnad som påverkar en enskild affär senhet som körs inom ett visst geografiskt område.
- Varje data Center är anslutet av en serie regionala hyrda linjer som skapar ett löst kopplat globalt WAN.
- DEN angav molnet genom att migrera alla e-postkonton för slutanvändare till Office 365. Migreringen slutfördes mer än sex månader sedan. Sedan dess har bara några få IT-tillgångar distribuerats till molnet.
- CDO: s primära utvecklings team arbetar i en dev/test-kapacitet för att lära dig mer om moln funktioner.
- En affär senhet experimenterar med Big data i molnet. BI-teamet i det deltar i det arbetet.
- Den befintliga IT-styrnings principen anger att personliga kunddata och finansiella data måste finnas på till gångar som ägs direkt av företaget. Den här principen blockerar moln införande för alla verksamhets kritiska appar eller skyddade data.
- IT-investeringar styrs av stora av kapital kostnaden. Dessa investeringar är planerade och ofta innehåller planer för pågående underhåll, samt etablerade uppdaterings cykler på tre till fem år beroende på data centret.
- De flesta investeringar i teknik som inte överensstämmer med den årliga planen åtgärdas av skugg IT-ansträngningar. Dessa ansträngningar hanteras vanligt vis av affär senheter och finansieras genom affär senhetens drifts kostnader.

## <a name="future-state"></a>Framtida tillstånd

Följande ändringar förväntas under de närmaste åren:

- INFORMATIONS gruppen är ett medel för att modernisera principen om personliga och finansiella data för att stödja framtida mål. Två medlemmar i IT-styrningen har insyn i den här ansträngningen.
- Informations chefen vill använda en molnbaserad migrering som en tvingande funktion för att förbättra konsekvens och stabilitet mellan affär senheter och geografiska områden. Det framtida läget måste dock respektera eventuella externa krav som kräver avvikelse från standard metoder av särskilda IT-team.
- Om de tidiga experimenten i app dev och BI visar ledande indikatorer för framgång, skulle de var som helst för att frigöra produktions lösningar för små skala till molnet under de närmaste 24 månaderna.
- Informations chefen och ekonomi chefen har tilldelat en arkitekt och vice VD för infrastrukturen för att skapa en kostnads analys och genomförbarhets studie. Dessa ansträngningar avgör om företaget kan och bör flytta 5 000-till gångar till molnet under de kommande 36 månaderna. En lyckad migrering skulle göra det möjligt för IT-chef att eliminera två Data Center och minska kostnaderna med över $100 miljoner USD under fem års planen. Om tre till fyra Data Center kan uppleva liknande resultat, kommer budgeten att vara tillbaka i svart, vilket ger CHEFs budgeten stöd för fler innovativa initiativ.
    ![Lokala kostnader jämfört med Azure-kostnader som demonstrerar en avkastning på $100 miljoner USD under de kommande fem åren](../../../_images/govern/calculator-enterprise.png)
- Tillsammans med den här kostnads besparingarna planerar företaget att ändra hanteringen av vissa IT-investeringar genom att flytta in den utbetalade kapital kostnaden som en drifts kostnad i den. Den här ändringen ger bättre kostnads kontroll som kan användas för att påskynda andra planerade insatser.

## <a name="next-steps"></a>Nästa steg

Företaget har utvecklat en företags princip för att forma styrnings implementeringen. Företags principen innehåller många av de tekniska besluten.

> [!div class="nextstepaction"]
> [Granska den inledande företags principen](./initial-corporate-policy.md)
