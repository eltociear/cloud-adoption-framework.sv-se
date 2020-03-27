---
title: Krav för att befordra en migrerad resurs till produktion
description: Använd ramverket för moln införande för Azure för att förstå vanliga uppgifter och standard krav för att befordra en migrerad resurs till produktion.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 34444c31aa977e6088c7aabbb916a27c008c2b04
ms.sourcegitcommit: ea63be7fa94a75335223bd84d065ad3ea1d54fdb
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/27/2020
ms.locfileid: "80355213"
---
<!-- cSpell:ignore CISO prepromotion -->

<!-- markdownlint-disable MD026 -->

# <a name="what-is-required-to-promote-a-migrated-resource-to-production"></a>Vad krävs för att befordra en migrerad resurs till produktion?

Befordran till produktion markerar slut för ande av migreringen av en arbets belastning till molnet. När tillgången och alla dess beroenden har befordrats dirigeras produktionstrafiken om. Trafikomdirigeringen gör lokala tillgångar föråldrade så att de kan tas ur bruk.

Befordringsprocessen varierar beroende på arbetsbelastningens arkitektur. Det finns dock vissa gemensamma villkor och uppgifter. Den här artikeln beskriver dessa och kan användas som en checklista inför befordran.

## <a name="prerequisite-processes"></a>Nödvändiga processer

Var och en av följande processer bör utföras, dokumenteras och verifieras före produktionsdistributionen:

- **[Utvärdera](../assess/index.md):** Arbets belastningen har utvärderats för molnbaserad kompatibilitet.
- **[Arkitekt](../assess/architect.md):** Arbets Belastningens struktur har utformats korrekt för att passa den valda moln leverantören.
- **[Replikera](../migrate/replicate.md):** Till gångarna har repliker ATS till moln miljön.
- **[Steg](../migrate/stage.md):** De replikerade till gångarna har återställts i en mellanlagrad instans av moln miljön.
- **[Företags testning](./business-test.md):** Arbets belastningen har testats fullständigt och godkänts av företags användare.
- **[Plan för verksamhets ändring](./business-change-plan.md):** Företaget har delat en plan för de ändringar som görs i enlighet med produktions erbjudandet. Detta bör omfatta en användar implementerings plan, ändringar av affärs processer, användare som kräver utbildning och tids linjer för olika aktiviteter.
- **[Klart](./ready.md):** I allmänhet måste en serie tekniska ändringar göras före befordran.

## <a name="best-practices-to-execute-prior-to-promotion"></a>Metodtips inför befordran

Följande tekniska ändringar kommer förmodligen att behöva slutföras och dokumenteras som en del av befordringsprocessen:

- **Domänanpassning.** Vissa företagsprinciper kräver separata domäner för mellanlagring och produktion. Se till att alla tillgångar är anslutna till rätt domän.
- **Dirigering av användare.** Verifiera att användarna får åtkomst till arbetsbelastningen genom korrekta nätverksvägar. Verifiera att prestandan är konstant och enligt förväntningarna.
- **Identitetsanpassning.** Bekräfta att användare som omdirigeras till programmet har rätt behörigheter inom domänen som är värd för programmet.
- **Prestanda.** Utför en slutgiltig validering av arbetsbelastningens prestanda för att minska risken för överraskningar.
- **Kontroll av verksamhetskontinuitet och haveriberedskap.** Kontrollera att rätt säkerhetskopierings- och återställningsprocesser fungerar som förväntat.
- **Dataklassificering.** Verifiera dataklassificeringen för att säkerställa att rätt skydd och principer har implementerats.
- **IT-verifiering av IT-säkerhetsansvarig.** Kontrollera att IT-säkerhetsansvarige har granskat arbetsbelastningen, affärsriskerna, risktoleransen och konsekvenshanteringsstrategier.

## <a name="final-step-promote"></a>Sista steget: Höj upp

Arbetsbelastningar kräver olika nivåer av detaljerade gransknings- och befordringsprocesser. Nätverksjusteringen fungerar dock som det gemensamma sista steget för alla befordringslanseringar. När allt annat är klart kan du uppdatera DNS-poster eller IP-adresser för att dirigera trafik till den migrerade arbetsbelastningen.

## <a name="next-steps"></a>Nästa steg

När arbetsbelastningen har befordrats har lanseringen slutförts. Parallellt med migreringen måste tillbakadragna tillgångar [tas ur bruk](./decommission.md).

> [!div class="nextstepaction"]
> [Inaktivera tillbakadragna tillgångar](./decommission.md)
