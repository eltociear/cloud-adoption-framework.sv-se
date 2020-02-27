---
title: Förstå moln säkerhets bas linjen
description: Lär dig mer om en moln säkerhets bas linje som bygger på de fem disciplinerna i moln styrning för att upprätta ett styrnings ramverk.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 36aa64e35c5858e41d7cb4d29885289ca0c5435a
ms.sourcegitcommit: af45c1c027d7246d1a6e4ec248406fb9a8752fb5
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 02/27/2020
ms.locfileid: "77707585"
---
# <a name="understand-the-cloud-security-baseline"></a>Förstå moln säkerhets bas linjen

Det här är en introduktions artikel om allmänna ämnen i en moln säkerhets bas linje som bygger på de [fem disciplinerna i moln styrning](../governance-disciplines.md) för att upprätta ett styrnings ramverk. Mer detaljerad information om moln säkerhet finns i [Azures betrodda moln](https://azure.microsoft.com/overview/trusted-cloud). Metoder för att förbättra organisationens säkerhets position finns i [Cloud Security service-katalogen](https://www.microsoft.com/security/information-protection)

> [!NOTE]
> Den här artikeln förväntas inte tillhandahålla tillräckligt med kontext för att låta läsaren implementera en säkerhets strategi. Det är endast för allmän medvetenhet.

## <a name="cloud-security"></a>Cloud Security

Cloud Security är en förlängning av traditionella informations säkerhets metoder. Traditionell IT-säkerhet omfattar principer och kontroller som styr dator säkerhet, nätverks säkerhet, data skydd, informations användning och så vidare. Samma principer och kontroller krävs i molnet. Under en moln omvandling är det absolut nödvändigt att IT aktivt är inblandat och förstår molnet, för att säkerställa att äldre IT-principer mappas till rätt kontroll nivåer i molnet.

En moln säkerhets strategi bör minst beakta följande ämnen:

- **Klassificera data.** Lämplig data klassificering för att förstå data källor som är privata, skyddade eller mycket konfidentiella. Detta hjälper dig att hantera risker under planeringen.
- **Planera för ett scenario med hybrid moln.** Att förstå hur äldre, lokala nätverk ansluter till molnet hjälper IT att identifiera och åtgärda risker.
- **Planera för attacker och misstag.** Under de första månaderna av en transformering kommer misstag att göras när teamet lär sig. Börja med låg risk och mycket begränsade distributioner för att lära dig säkert.
- **Prioritera sekretess.** Hela teamet bör hålla kunderna och personal sekretessen i alla transformeringar. Dina data är säkra i molnet, men teamet bör vara medvetna om och extra försiktig vid hantering av känsliga data.

## <a name="protecting-data-and-privacy"></a>Skydda data och sekretess

För organisationer i hela världen&mdash;om myndigheter, icke-vinster eller företag&mdash;molnbaserad data behandling har blivit en viktig del av den pågående IT-strategin. Cloud Services ger organisationer av alla storlekar åtkomst till praktiskt taget obegränsade data lagring samtidigt som du frigör dem från behovet av att köpa, underhålla och uppdatera sina egna nätverk och dator system. Microsoft och andra moln leverantörer erbjuder IT-infrastruktur, plattform och program vara som en tjänst (SaaS), vilket gör det möjligt för kunder att snabbt skala upp eller ned efter behov och bara betala för den data behandlings kraft och lagrings enhet de använder.

Eftersom organisationer fortsätter att dra nytta av fördelarna med moln tjänster, t. ex. ökad valmöjligheter, flexibilitet och flexibilitet samtidigt som du ökar effektiviteten och sänker IT-kostnaderna, måste de överväga hur introduktionen av moln tjänster påverkar deras sekretess-, säkerhets-och position. Microsoft har arbetat med att göra sina moln erbjudanden inte bara skalbara, tillförlitliga och hanterbara, utan också att se till att våra kunders data skyddas och används på ett transparent sätt.

Säkerhet är en viktig komponent i starka data skydd i alla onlinebaserade data behandlings miljöer. Men säkerheten är inte tillräcklig. Konsumenter och företag som är villiga att använda en viss molnbaserad data behandlings produkt beror också på deras förmåga att lita på att sekretessen för informationen kommer att skyddas och att deras data endast kommer att användas på ett sätt som är konsekvent med kund förväntningarna . Lär dig mer om Microsofts metod för att [skydda data och sekretess i molnet](https://go.microsoft.com/fwlink/?LinkId=808242&clcid=0x409)

## <a name="risk-mitigation"></a>Risk minskning

De två största riskerna i ett Data Center kan grupperas i två källor: ålders system och mänskligt fel. Att skydda mot dessa två risker är ett minimum när du definierar en IT-säkerhetsstrategi. Samma sak gäller i molnet. Nedan följer några exempel på kontroller som kan användas för att åtgärda risker och förbättra din moln säkerhets strategi.

- **Äldre system:** Många komponenter i lokala data Center lösningar består av program vara, maskin vara och processer som fördaterar aktuella säkerhets risker. Åtgärda, Ersätt eller dra tillbaka dessa system vid en moln omvandling när det är möjligt. Naturligtvis är det inte alltid möjligt. Om det finns äldre system kvar i produktions miljön i en hybrid lösning är det viktigt att dessa system har inventerats och förstås under utformningen av virtuella Data Center. På så sätt kan design teamet eliminera eller kontrol lera åtkomsten till dessa system från molnet.
- **IT-säkerhetsprocesser och kontroller:** Som minst bör moln design grupper uppdateras på befintliga IT-säkerhetsprocesser och kontroller för att överföra dem till molnet. I ett idealiskt scenario skulle en medlem i IT-säkerhetsteamet tränas i cybersäkerhet och engageras som medlem i design-och implementerings teamen.
- **Övervakning och granskning:** När du utformar styrnings processer och-verktyg bör du se till att övervaknings-och gransknings lösningarna innehåller säkerhets risker eller överträdelser.

> [!NOTE]
> **Teknisk skuld upplysning:** Det här avsnittet innehåller bara efterföljande steg. Ytterligare artiklar kommer att utökas i det här avsnittet över tid. Mer detaljerad information om moln säkerhet finns i [Azures betrodda moln](https://azure.microsoft.com/overview/trusted-cloud). Metoder för att förbättra organisationens säkerhets position finns i [Cloud Security service-katalogen](https://www.microsoft.com/security/information-protection)
