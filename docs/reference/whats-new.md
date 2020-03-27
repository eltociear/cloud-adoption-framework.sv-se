---
title: Nyheter
description: Lär dig mer om uppdateringar av Microsoft Cloud adoption Framework för Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 03/02/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: reference
ms.openlocfilehash: a3e316d49acaaee00d5ecd10efac9aa15c2dbd49
ms.sourcegitcommit: ea63be7fa94a75335223bd84d065ad3ea1d54fdb
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/27/2020
ms.locfileid: "80353686"
---
# <a name="whats-new-in-the-microsoft-cloud-adoption-framework"></a>Nyheter i Microsoft Cloud adoption Framework

## <a name="fulfilling-the-vision"></a>Uppfylla visionen

Nu är ramverket allmänt tillgängligt (GA). Vi fortsätter dock att utveckla ramverket i samarbete med kunder, partner och interna team. För att uppmuntra partnerskap publiceras innehåll när det blir tillgängligt. Dessa offentliga versioner möjliggör testning, validering och stegvis finjustering av vägledningen.

Viktiga ändringar registreras i följande versions anmärkningar.

## <a name="migration-update-03022020"></a>Uppdatering av migrering: 03/02/2020

Den här versionen svarade på feedback om kontinuiteten i migreringen genom flera metoder, inklusive strategi, plan, redo och migrering. Målet med den här versionen var att göra det enklare för läsarna att förstå den fortsatta förfiningen av planering och införande, eftersom kunderna fortsätter med migreringen. Följande ändringar har gjorts för att uppfylla den här versionens anda:

### <a name="new-articles"></a>Nya artiklar

- [Balansera konkurrerande prioriteringar](../strategy/balance-competing-priorities.md): beskriver balansen i prioriteringar som inträffar i varje metod för att informera kund strategier
- [Klassificering under utvärderings processer](../migrate/migration-considerations/assess/classify.md): beskriver vikten av att klassificera varje till gång och arbets belastning innan migreringen.

### <a name="restructure-landing-zone-process"></a>Omstrukturering av landnings zon process

Den första landnings zonen har tagits bort från beredskaps guiden för att fungera som den är ett eget avsnitt. Med den här metoden kan vi utöka begreppet landnings zoner och alternativ för landnings zoner. Detta ledde också till att några nya artiklar skapas:

- [Vad är en landnings zon?](../ready/landing-zone/index.md): definierar periodens landnings zon
- [Första landnings zon](../ready/landing-zone/first-landing-zone.md): expanderar jämförelsen av olika landnings zoner
- [Migrera landnings zon](../ready/landing-zone/migrate-landing-zone.md): flyttad den tidigare zon utkasts artikeln, för att separera definitionen av CAF-skissen från valet av den första landnings zonen, för att tillåta fler alternativ för landnings zoner.
- Artikel i [terraform vilplan](../ready/landing-zone/terraform-landing-zone.md) : flyttad från avsnittet "expanderat område" i den färdiga metoden till den nya avsnittet "landnings zon" i klar metodik, för att behandla terraform som en första klass medborgare i landnings zon konversationen.
- Gruppera grundläggande överväganden för landnings zoner tillsammans i innehålls förteckningen under "grundläggande landnings zoner".
- De rekommenderade säkerhets metoderna från metoden för migrering till ett nytt avsnitt med landnings zoner "förbättra landnings zonens säkerhet (känsliga data)" för att Visa läsarna till den här vägledningen tidigare i livs cykeln.

### <a name="refinements-to-the-azure-migration-guide"></a>Fin justering av Azure migration guide

Mönster för användar trafik föreslår att det här avsnittet av innehåll är mer sannolikt att används av implementerare och arkitekter under sin första migrering. För att bättre stödja den här mål gruppen har fokus på migreringsguiden förfinats för att bättre anpassa sig till det ursprungliga syftet med att Visa läsarna till de verktyg som användes vid en första migrering.

- [Översikt](../migrate/azure-migration-guide/index.md): tydlig beskrivning av hand boken, med minskat antal steg.
- [Utvärdera](../migrate/azure-migration-guide/assess.md): bättre illustrerar att utvärderingen i den här fasen fokuserar på att utvärdera teknisk anpassning av en speciell arbets belastning och relaterade till gångar. Avsnittet om utmanande antaganden har lagts till för att visa vem den här utvärderings nivån fungerar med den stegvisa utvärderings metod som först nämnts i plan metodiken.
- [Migrera](../migrate/azure-migration-guide/migrate.md): som svar på feedback på nivå 1-konferenser lades en referens till UnifyCloud till i verktygs alternativen från tredje part.
- [Testa, optimera och befordra](../migrate/azure-migration-guide/optimize-and-transform.md): justera rubriken för den här artikeln med andra förslag på förbättringar av processen.

### <a name="refinements-to-migration-process-improvements"></a>Justeringar av förbättringar av migreringsprocessen

- [Utvärderings översikt](../migrate/migration-considerations/assess/index.md): bättre illustrerar att utvärderingen i den här fasen fokuserar på att utvärdera teknisk anpassning av en speciell arbets belastning och relaterade till gångar.
- [Planerings check lista](../migrate/migration-considerations/prerequisites/planning-checklist.md): klargör vikten av åtgärds justering under planeringen av migreringen för att säkerställa en väl hanterad arbets belastning, efter migreringen.

### <a name="placement-of-related-articles"></a>Placering av relaterade artiklar

Varje artikel lista nedan har flyttats. Trafiken dirigeras om till den nya platsen.

- Artikeln om [utvärderings metod](../plan/contoso-migration-assessment.md) : flyttad från avsnittet "metod tips" i metoden Migrate (bästa praxis) i plan metodiken. Den här flytten visar läsarna för att utvärdera lokala miljöer tidigare i livs cykeln.
- [Balansera portfölj](../strategy/balance-the-portfolio.md) artikeln: flyttas från avsnittet "expanderat område" i metoden Migrate till strategi metoden. Den här flyttningen visar läsarna till den här processen tidigare i livs cykeln.

### <a name="alignment-of-the-changes"></a>Justering av ändringarna

- [Klar översikt](../ready/index.md): uppdatera de fyra stegen i klar översikt för att avspegla den raffinerade processen
- [Migrera översikt](../migrate/index.md): uppdatera stegen i över gångs översikten för att avspegla den raffinerade processen
- [Flytta metod grafik](../migrate/index.md): uppdatera till metod avbildningen för att avspegla ändringar
- [Översikts bild](../index.md): uppdateringar av översikts grafik som visar ändringar
