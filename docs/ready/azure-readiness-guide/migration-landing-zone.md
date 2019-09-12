---
title: Distribuera en landningszon i Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Lär dig att distribuera en landningszon i Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 5/19/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.custom: fasttrack-edit
ms.openlocfilehash: 8fccc60eb9944aca6801deb79310ebf07e10b109
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/06/2019
ms.locfileid: "70819470"
---
# <a name="deploy-a-migration-landing-zone"></a>Distribuera en landningszon för migrering

Termen *landingszon för migrering* används för att beskriva en miljö som har etablerats och förberetts för att fungera som värd för arbetsbelastningar som migreras från en lokal miljö till Azure. En landningszon för migrering är slutprodukten för handboken till Azure-beredskap. Den här artikeln förenar beredskapsämnen som har beskrivits i den här handboken och tillämpar de beslut som har fattats vid distributionen av landnings zonen för den första migreringen.

I följande avsnitt beskrivs en landningszon som ofta används för att etablera en miljö som är lämplig för användning under en migrering. Miljön eller landningszonen som beskrivs i den här artikeln beskrivs också i en Azure-skiss. Du kan använda landningszonskissen från Cloud Adaption Framework för att distribuera den definierade miljön med ett enda klick.

## <a name="purpose-of-the-blueprint"></a>Syftet med skissen

Ramverk för molnimplementering-skissen för migrering av landningszoner skapar en landningszon. Denna landningszon är avsiktligt begränsad. Den har utformats för att skapa en konsekvent startpunkt som ger utrymme för att lära sig om infrastruktur som kod. För vissa åtgärder för migreringen kan den här landningszonen räcka för dina behov. Det är också troligt att du kommer att behöva ändra något i skissen i förhållande till dina begränsningar.

## <a name="blueprint-alignment"></a>Anpassa skissen

Följande bild visar Ramverk för molnimplementering-skissen för migrering av landningszoner i förhållande till arkitekturkomplexitet och efterlevnadskrav.

![Anpassa skissen](../../_images/ready/blueprint-overview.png)

- Bokstaven A placeras inuti en böjd linje som markerar den här skissens omfång. Det här omfånget är avsett att ge den här skissen en begränsat komplex arkitektur men den har utformats enligt relativt genomsnittliga efterlevnadskrav.
- Kunder som har en hög grad av komplexitet och stränga krav på efterlevnad bör kanske använda en utökad skiss från en partner eller en av de [standardbaserade skissexemplen](/azure/governance/blueprints/samples/).
- De flesta kunders behov hamnar någonstans mellan dessa två extremer. Bokstaven B representerar den process som beskrivs i artiklarna [Landningszon – att tänka på](../considerations/index.md). Kunder i det här utrymmet kan använda beslutsguiderna som finns i dessa artiklar för att identifiera noder som ska läggas till i Ramverk för molnimplementering-skissen för migrering av landningszoner. Med den här metoden kan du anpassa skissen efter dina behov.

## <a name="use-this-blueprint"></a>Använd den här skissen

Innan du använder Ramverk för molnimplementering-skissen för migrering av landningszoner bör du läsa följande antaganden, beslut och implementeringsanvisningar.

## <a name="assumptions"></a>Antaganden

Följande antaganden eller begränsningar användes när den inledande landningszonen definierades. Om dessa antaganden överensstämmer med dina begränsningar kan du använda skissen för att skapa din första landningszon. Skissen kan också utökas för att skapa en landningszonskiss som uppfyller dina unika begränsningar.

- **Prenumerationsgränser:** Implementeringen förväntas inte överskrida [prenumerationsgränserna](https://docs.microsoft.com/azure/azure-subscription-service-limits). Två vanliga indikatorer är ett överskott på 25 000 virtuella datorer eller 10 000 virtuella processorer.
- **Efterlevnad:** Det finns inga krav från tredje part som måste efterlevas i denna landningszon.
- **Arkitekturkomplexitet:** Arkitekturens komplexitet kräver inte ytterligare produktionsprenumerationer.
- **Delade tjänster:** Det finns inga befintliga delade tjänster i Azure som kräver att den här prenumerationen behandlas som en eker i en hubb-och-ekerarkitektur.

Om dessa antaganden verkar stämma överens med din nuvarande miljö kan den här skissen vara lämplig för att börja bygga din landningszon.

## <a name="decisions"></a>Beslut

Följande beslut speglas i skissen för landningszonen.

| Komponent | Beslut | Alternativa metoder |
|---------|---------|---------|
|Migreringsverktyg|Azure Site Recovery distribueras och ett Azure Migrate-projekt skapas.|[Beslutsguide för migreringsverktyg](../../decision-guides/migrate-decision-guide/index.md)|
|Loggning och övervakning|Arbetsytan Operational Insights och ett diagnostiskt lagringskonto kommer att tillhandahållas.|         |
|Nätverk|Ett virtuellt nätverk skapas med undernät för gateway, brandvägg, jumpbox och landningszon.|[Nätverksbeslut](../considerations/network-decisions.md)|
|Identitet|Vi förutsätter att prenumerationen redan är associerad med en instans av Azure Active Directory.|[Metodtips för identitetshantering](https://docs.microsoft.com/azure/security/azure-security-identity-management-best-practices?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/bread/toc.json)         |
|Princip|Skissen förutsätter för närvarande att inga Azure-principer ska tillämpas.|         |
|Prenumerationsdesign|Saknas – utformad för en enda produktionsprenumeration.|[Skalanpassa prenumerationer](../considerations/scaling-subscriptions.md)|
|Hanteringsgrupper|Saknas – utformad för en enda produktionsprenumeration.|[Skalanpassa prenumerationer](../considerations/scaling-subscriptions.md)         |
|Resursgrupper|Saknas – utformad för en enda produktionsprenumeration.|[Skalanpassa prenumerationer](../considerations/scaling-subscriptions.md)         |
|Data|Gäller inte|[Välj rätt SQL Server-alternativ i Azure](https://docs.microsoft.com/azure/sql-database/sql-database-paas-vs-sql-server-iaas?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/bread/toc.json)         |
|Storage|Gäller inte|[Riktlinjer för Azure Storage](../considerations/storage-guidance.md)         |
|Standarder för namngivning och taggning|Gäller inte|[Metodtips för namngivning och taggning](../considerations/name-and-tag.md)         |
|Kostnadshantering|Gäller inte|[Spåra kostnader](../azure-best-practices/track-costs.md)|
|Compute|Gäller inte|[Compute-alternativ](../considerations/compute-decisions.md)|

## <a name="customize-or-deploy-a-landing-zone-from-this-blueprint"></a>Anpassa eller distribuera en landningszon från den här skissen

Läs mer och ladda ned ett referensexemplar av Ramverk för molnimplementering-skissen för migrering av landningszoner för distribution eller anpassning från [Azure Blueprint-exempel](https://docs.microsoft.com/azure/governance/blueprints/samples/index).

Skissexemplen finns också i portalen. Mer information om hur du distribuerar en skiss finns i [Azure Blueprints](./govern-org-compliance.md?tabs=azureblueprints#create-a-blueprint).

Information om anpassning av den här skissen eller den resulterande landningszonen finns artiklarna [Landingzon – att tänka på](../considerations/index.md).

## <a name="next-steps"></a>Nästa steg

När landningszonen för migrering har distribuerats är du redo att migrera arbetsbelastningar till Azure.
Se [migreringsguiden för Azure](../../migrate/azure-migration-guide/index.md) för vägledning om verktyg och processer som behövs för att migrera din första arbetsbelastning.

> [!div class="nextstepaction"]
> [Migrera din första arbetsbelastning med migreringsguiden för Azure](../../migrate/azure-migration-guide/index.md)
