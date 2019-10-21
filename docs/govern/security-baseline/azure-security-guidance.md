---
title: Vägledning – säkerheten i Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Vilka säkerhets guider tillhandahåller Microsoft?
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 8449878d46c939c58f690e585aac07fa0e827484
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/17/2019
ms.locfileid: "72548057"
---
<!-- markdownlint-disable MD026 -->

# <a name="microsoft-security-guidance"></a>Microsofts säkerhets guider

## <a name="tools"></a>Verktyg

Microsoft introducerade [tjänsten Trusted Platform](https://servicetrust.microsoft.com) and Compliance Manager för att hjälpa till med följande:

- Lösa utmaningar med hantering av efterlevnad.
- Uppfylla ansvaret för att uppfylla myndighets krav.
- Genomför självbetjänings granskningar och riskbedömningar av användningen av företags moln tjänster.

Dessa verktyg är utformade för att hjälpa organisationer att uppfylla komplexa krav på efterlevnad och förbättra funktionerna för data skydd när de väljer och använder Microsoft Cloud tjänster.

**STP (service Trust Platform)** ger detaljerad information och verktyg som hjälper dig att uppfylla dina behov av att använda Microsoft Cloud tjänster, inklusive Azure, Office 365, Dynamics 365 och Windows. STP är en enda arbets affär för säkerhet, regler, efterlevnad och sekretess information som är relaterad till Microsoft Cloud. Det är här som vi publicerar den information och de resurser som krävs för att utföra självbetjänings riskbedömning av moln tjänster och verktyg. STP skapades för att hjälpa till att spåra regelefterlevnad-aktiviteter i Azure, inklusive:

- **Compliance Manager:** Compliance Manager, ett arbets flödes verktyg för riskbedömning på Microsofts plattform för tjänst förtroende, gör att du kan spåra, tilldela och kontrol lera din organisations aktiviteter för regelefterlevnad som rör Microsoft Cloud tjänster, till exempel Office 365, Dynamics 365 och Azure. Du hittar mer information i nästa avsnitt.
- **Betrodda dokument:** För närvarande finns det tre typer av guider som ger dig många resurser för att utvärdera Microsoft Cloud. Lär dig mer om Microsoft-åtgärder i säkerhet, efterlevnad och sekretess. och hjälper dig att arbeta med att förbättra dina data skydds funktioner. Dessa är:
- **Gransknings rapporter:** Med gransknings rapporter kan du hålla dig uppdaterad om den senaste sekretess-, säkerhets-och efterlevnad-relaterad informationen för Microsoft Cloud Services. Detta omfattar ISO, SOC, FedRAMP och andra gransknings rapporter, broar och material som rör oberoende revisioner från tredje part av Microsoft Cloud tjänster som Azure, Office 365, Dynamics 365 och andra.
- **Data skydds guider:** Data skydds guider ger information om hur Microsoft Cloud Services skyddar dina data och hur du kan hantera data säkerhet och efterlevnad i molnet för din organisation. Detta omfattar djupgående fakta blad som innehåller information om hur Microsoft utformar och arbetar med moln tjänster, vanliga frågor och svar, rapporter om säkerhets utvärderingar, inträngande test resultat och rikt linjer som hjälper dig att utföra riskbedömning och förbättra dina data skydds funktioner.
- **Utkast till Azure-säkerhet och efterlevnad:** Med ritningar får du till gång till resurser som hjälper dig att skapa och lansera moln drivna program som hjälper dig att efterleva strängare bestämmelser och standarder. Med fler certifieringar än någon annan moln leverantör kan du tryggt distribuera kritiska arbets belastningar till Azure, med ritningar som innehåller:
  - Branschcertifierade översikt och vägledning.
  - Matris för kund ansvar.
  - Referens arkitekturer med hot modeller.
  - Kontrol lera implementerings-matriser.
  - Automation för att distribuera referens arkitekturer.
  - Sekretess resurser: dokumentation för utvärdering av data skydds effekter, data mottagar begär Anden (DSR: er) och meddelande om data intrång tillhandahålls i ditt eget ansvars program som stöd för allmän dataskyddsförordning (GDPR).
- **Kom igång med GDPR:** Microsoft-produkter och tjänster hjälper organisationer att uppfylla GDPR-krav när de samlar in eller bearbetar person uppgifter. STP har utformats för att ge dig information om de funktioner i Microsoft-tjänster som du kan använda för att adressera särskilda krav för GDPR. Dokumentationen kan hjälpa din GDPR ansvar och förståelse för tekniska och organisatoriska åtgärder. Dokumentation för utvärderingar av data skydds effekter, DSR: er (data subject requests) och meddelande om data intrång tillhandahålls i ditt eget ansvars program i stöd för GDPR.
  - **Begär Anden om data subjekt:** GDPR beviljar individer (eller data ämnen) vissa rättigheter i samband med bearbetningen av sina person uppgifter. Detta innefattar rätten att korrigera felaktiga data, radera data eller begränsa dess bearbetning, samt ta emot data och utföra en begäran om att överföra sina data till en annan kontrollant.
  - **Data intrång:** GDPR bestämmer meddelande kraven för datakontrollanter och processorer i händelse av överträdelse av person uppgifter. STP ger dig information om hur Microsoft försöker förhindra överträdelser på den första platsen, hur Microsoft upptäcker en överträdelse och hur Microsoft kommer att svara i händelse av en överträdelse och meddela dig som en data kontroll.
  - **Utvärdering av data skydds påverkan:** Microsoft hjälper kontrollanter att slutföra GDPR av data skydds påverkan. GDPR tillhandahåller en komplett lista över fall där DPIAs måste utföras, till exempel automatisk bearbetning för profilering och liknande aktiviteter. bearbetning i stor skala av särskilda kategorier av person uppgifter och systematisk övervakning av ett offentligt tillgängligt utrymme i stor skala.
  - **Andra resurser:** Förutom de verktyg som beskrivs i ovanstående avsnitt ger STP också andra resurser, inklusive regional efterlevnad, ytterligare resurser för säkerhets-och efterlevnads Center och vanliga frågor om tjänsten Trust Platform, Compliance Manager, och sekretess-/GDPR.
- **Regional efterlevnad:** STP innehåller ett stort antal dokument och vägledning för Microsoft onlinetjänster för att uppfylla kraven för efterlevnad för olika regioner, inklusive Tjeckiska republiken, Polen och Rumänien.

## <a name="unique-intelligent-insights"></a>Unika intelligenta insikter

I takt med att säkerhets signalernas volym och komplexitet ökar, tar du reda på om dessa signaler är trovärdiga och sedan fungerar det tar för lång tid. Microsoft erbjuder en oöverträffad bredd av säkerhets information som levereras i moln skala för att hjälpa dig att snabbt upptäcka och åtgärda hot. [Läs mer](https://docs.microsoft.com/azure/security-center/security-center-intro)

## <a name="azure-threat-intelligence"></a>Azure Threat Intelligence

Genom att använda alternativet för hotinformation i Security Center kan IT-administratörer identifiera säkerhetshot mot miljön. De kan till exempel identifiera om en vissa dator är en del av ett botnät. Datorer kan bli noder i ett botnät när angripare installerar otillåten skadlig kod som i hemlighet ansluter datorn till kommando och kontroll. Hotinformation kan även identifiera möjliga hot som kommer från underjordiska kommunikationskanaler, till exempel mörka internet.

För generering av den här hotinformationen använder Security Center data från flera källor på Microsoft. Security Center använder detta för att identifiera potentiella hot mot din miljö. Fönstret Hot information består av tre huvud alternativ:

- Identifierade hottyper
- Hotursprung
- Karta för hotinformation

## <a name="machine-learning-in-azure-security-center"></a>Maskin inlärning i Azure Security Center

Azure Security Center djup analyserar en hel mängd data från en mängd olika Microsoft-och partner lösningar för att hjälpa dig att uppnå större säkerhet. För att dra nytta av dessa data använder företaget data vetenskap och maskin inlärning för skydd mot hot, identifiering och senare undersökningar.

Azure Machine Learning är i stort sett att uppnå två resultat:

## <a name="next-generation-detection"></a>Nästa generations identifiering

Angripare är allt automatiserade och avancerade. De använder även data vetenskap. De bakåtkompilerar skydd och bygger system som stöder mutationer i beteende. De imiterar sina aktiviteter som brus och lär dig snabbt från misstag. Machine Learning hjälper oss att svara på den här utvecklingen.

## <a name="simplified-security-baseline"></a>Förenklad säkerhets bas linje

Det är inte enkelt att fatta effektiva säkerhets beslut. Det kräver säkerhets erfarenhet och expertis. Vissa stora organisationer har sådana experter på personal, men många företag är inte. Azure Machine Learning gör det möjligt för kunderna att dra nytta av ingengörskunskap av andra organisationer när de fattar säkerhets beslut.

## <a name="behavioral-analytics"></a>Beteendeanalys

Beteendeanalys är en teknik som analyserar och jämför data med en samling kända mönster. Dessa mönster är dock inte enkla signaturer. De bestäms genom komplexa Machine Learning-algoritmer som tillämpas på enorma data uppsättningar. och av expertanalytiker genom noggrann analys av skadliga beteenden. Azure Security Center kan använda beteende analys för att identifiera komprometterade resurser baserat på analyser av loggar för virtuella datorer, loggar för virtuella nätverks enheter, infrastruktur loggar, krasch dum par och andra källor.
