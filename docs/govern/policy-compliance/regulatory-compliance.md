---
title: Introduktion till regelefterlevnad
description: Lär dig mer om regler för efterlevnad i olika branscher och geografiska områden som kan påverka moln styrningen.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 2e5cfa035efe2fd3dd45b29edec53bfff2c7914f
ms.sourcegitcommit: af45c1c027d7246d1a6e4ec248406fb9a8752fb5
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 02/27/2020
ms.locfileid: "77709387"
---
# <a name="introduction-to-regulatory-compliance"></a>Introduktion till regelefterlevnad

Detta är en introduktions artikel om regelefterlevnad, vilket innebär att den inte är avsedd att användas för att implementera en strategi för efterlevnad. Mer detaljerad information om [Azure Compliance-erbjudanden](https://aka.ms/allcompliance) finns på [Microsoft Trust Center](https://www.microsoft.com/trustcenter/default.aspx). Dessutom är all nedladdnings bar dokumentation tillgänglig för vissa Azure-kunder från [Microsoft Service Trust Portal](https://servicetrust.microsoft.com).

Regelefterlevnad avser disciplinen och processen för att säkerställa att ett företag följer de lagar som styrs av styr organen i deras geografiska område eller regler som krävs av frivilligt infört bransch standarder. För IT-regler, övervakar människor och processer företagets system i arbetet för att upptäcka och förhindra överträdelser av principer och förfaranden som fastställs av dessa regler, förordningar och standarder. Detta gäller för ett brett utbud av övervaknings-och tvångs processer. Beroende på bransch och geografi kan dessa processer bli långa och komplexa.

Efterlevnad är utmanande för multinationella organisationer, särskilt i kraftigt reglerade branscher som hälso vård och finansiella tjänster. Standarder och föreskrifter Abound och i vissa fall kan ändras ofta, vilket gör det svårt för företag att fortsätta med att ändra internationell elektronisk data hanterings lagstiftning.

Som med säkerhets kontroller bör organisationer förstå ansvars fördelningen för att kontrol lera efterlevnaden i molnet. Moln leverantörer strävar efter att se till att deras plattformar och tjänster är kompatibla. Men organisationer måste också bekräfta att deras program, den infrastruktur som programmen är beroende av och tjänster som tillhandahålls av tredje part också certifieras som kompatibla.

Nedan följer beskrivningar av regler för efterlevnad i olika branscher och geografiska områden:

## <a name="hipaa"></a>HIPAA

Ett sjukvårds program som bearbetar skyddad hälso information (fi) omfattas av både sekretess regeln och säkerhets regeln som omfattas av hälso informationens portabilitet och ansvars rätts akt (HIPAA). HIPAA kunde troligt vis kräva att ett sjukvårds företag måste få skriftliga garantier från moln leverantören att den skyddar alla PHI-mottagna eller skapade.

## <a name="pci"></a>PCI

Payment Card Industry Data Security Standard (PCI DSS) är en tillverkarspecifik informations säkerhets standard för organisationer som hanterar anpassade kredit kort från de stora kort scheman, inklusive Visa, MasterCard, American Express, Discover och JCB. PCI-standarden bestäms av kort som ingår i och administreras av rådet för betalnings kortet bransch säkerhet. Standarden har skapats för att öka kontrollerna kring korts data för att minska ditt kredit korts bedrägerier. Verifieringen av efterlevnad utförs årligen, antingen av en extern uppfyller kraven enligt eller av en fast intern säkerhets bedömare (ISA) som skapar en rapport om efterlevnad (ROC) för organisationer som hanterar stora volymer av transaktioner, eller av en SAQ (Self-Assessment enkät) för företag.

## <a name="personal-data"></a>Personliga data

Person uppgifter är information som kan användas för att identifiera en konsument, anställd, partner eller annan boende eller juridisk person. Många nya lagar, särskilt de som behandlar sekretess och person uppgifter, kräver att företagen själva följer och rapporterar om efterlevnad och eventuella överträdelser som kan uppstå.

## <a name="gdpr"></a>GDPR

En av de viktigaste fördelarna med det här området är allmän dataskyddsförordning (GDPR) som är utformad för att stärka data skyddet för enskilda användare inom EU. GDPR kräver att data om individer (till exempel "ett namn, en hem adress, ett foto, en e-postadress, bank information, inlägg på webbplatser för sociala nätverk, medicinsk information eller datorns IP-adress") upprätthålls på servrar inom EU och inte överförs . Det kräver också att företag meddelar individer om alla data överträdelser och uppdrag som företag har en data skydds chef (DPO). Andra länder har eller utvecklar liknande typer av regler.

## <a name="compliant-foundation-in-azure"></a>Kompatibel grund i Azure

För att hjälpa kunderna att uppfylla sina egna krav på efterlevnad i reglerade branscher och marknader över hela världen, upprätthåller Azure den största portföljen i branschen&mdash;i bredd (totalt antal erbjudanden) och djup (antalet kund tjänster i utvärderings området). Azure Compliance-erbjudanden grupperas i fyra segment: globalt tillämpligt, amerikanska myndigheter, branschspecifika och region/landsspecifika.

Azure Compliance-erbjudanden baseras på olika typer av garantier, inklusive formella certifieringar, attesteringar, godkännanden och bedömningar som produceras av oberoende gransknings företag från tredje part, samt avtals ändringar. själv bedömningar och kund väglednings dokument som skapats av Microsoft. Varje erbjudande beskrivning i det här dokumentet innehåller en uppdaterad omfattnings instruktion som visar vilka Azure Customer-tjänster som omfattas av utvärderingen, samt länkar till nedladdnings bara resurser för att hjälpa kunderna med sin egen efterlevnad plikt.

Mer detaljerad information om Azure Compliance-erbjudanden finns i [Microsoft Trust Center](https://www.microsoft.com/trustcenter/compliance/complianceofferings). Dessutom är all nedladdnings bar dokumentation tillgänglig för vissa Azure-kunder från [tjänst förtroende portalen](https://servicetrust.microsoft.com) i följande avsnitt:

- **Gransknings rapporter:** Innehåller avsnitt för FedRAMP, GRC Assessment, ISO, PCI DSS och SOC-rapporter.
- **Data skydds resurser:** Innehåller guider för regelefterlevnad, vanliga frågor och svar och avsnitt om pen-test och säkerhets utvärdering.

## <a name="next-steps"></a>Nästa steg

Lär dig mer om säkerhets beredskap för molnet.

> [!div class="nextstepaction"]
> [Beredskap för moln säkerhet](./cloud-security-readiness.md)
