---
title: 'Styrnings guide för komplexa företag: Förbättra disciplinen för identitets bas linjer'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: 'Styrnings guide för komplexa företag: Förbättra disciplinen för identitets bas linjer'
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/06/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: ea4596c734e5bef03179569e537aacbca430d77e
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/24/2019
ms.locfileid: "71222325"
---
# <a name="governance-guide-for-complex-enterprises-improve-the-identity-baseline-discipline"></a>Styrnings guide för komplexa företag: Förbättra disciplinen för identitets bas linjer

Den här artikeln går vidare genom att lägga till identitets bas kontroller i styrnings MVP.

## <a name="advancing-the-narrative"></a>Med den här berättelsenn

Affärs justeringen för moln migreringen av de två data centren godkändes av ekonomi chefen. Under den tekniska genomförbarhets undersökningen identifierades flera hindren:

- Skyddade data och verksamhets kritiska program representerar 25% av arbets belastningarna i de två data centren. Varken kan elimineras förrän de aktuella styrnings principerna angående känsliga person uppgifter och verksamhets kritiska program har förberetts.
- 7% av till gångarna i dessa data Center är inte moln-kompatibla. De kommer att flyttas till ett alternativt Data Center innan data Center kontraktet avslutas.
- 15% av till gångarna i data centret (750 virtuella datorer) har ett beroende av tidigare autentisering eller Multi-Factor Authentication från tredje part.
- VPN-anslutningen som ansluter befintliga data Center och Azure erbjuder inte tillräckligt med data överförings hastigheter eller svars tider för att migrera volymen av till gångar inom en tids linje på två år för att dra tillbaka data centret.

De två första hindren hanteras parallellt. I den här artikeln behandlas den tredje och fjärde hindren-lösningen.

### <a name="expanding-the-cloud-governance-team"></a>Expandera moln styrnings teamet

Moln styrnings teamet expanderar. Med tanke på behovet av ytterligare stöd för identitets hantering, kommer en system administratör från identitets gruppen nu att delta i ett vecko möte för att hålla de befintliga team medlemmarna medvetna om ändringar.

### <a name="changes-in-the-current-state"></a>Ändringar i det aktuella läget

IT-teamet har godkännande för att gå vidare med CHEFs-och ekonomi planerna för att dra tillbaka två Data Center. Det är dock en fråga om 750 (15%) av till gångarna i dessa data Center måste flyttas någon annan stans än molnet.

### <a name="incrementally-improve-the-future-state"></a>Förbättra framtida tillstånd stegvis

De nya framtida tillstånds planerna kräver en mer robust identitets bas lösning för att migrera de virtuella 750-datorerna med tidigare autentiserings krav. Utöver dessa två Data Center förväntas denna utmaning påverka liknande procent andelar av till gångar i andra data Center.

Det framtida läget kräver nu också en anslutning från moln leverantören till företagets MPLS/lånade lösning.

Ändringarna i det aktuella och framtida läget ger nya risker som kräver nya princip instruktioner.

## <a name="changes-in-tangible-risks"></a>Förändringar i materiella risker

**Verksamhets avbrott under migreringen.** Vid migrering till molnet skapas en kontrollerad, tids gräns risk som kan hanteras. Det är mycket högre risk att flytta ålders maskin vara till en annan del av världen. En minsknings strategi krävs för att undvika avbrott i affärs verksamhet.

**Befintliga identitets beroenden.** Beroenden för befintliga autentiserings-och identitets tjänster kan fördröja eller förhindra migrering av vissa arbets belastningar till molnet. Om du inte returnerar två Data Center i tid kommer miljon tals dollar att debiteras i låne avgifter för data Center.

Den här affärs risken kan utökas till några tekniska risker:

- Äldre autentisering är kanske inte tillgänglig i molnet, vilket begränsar distributionen av vissa program.
- Den aktuella tredjeparts Multi-Factor Authentication-lösningen är kanske inte tillgänglig i molnet, vilket begränsar distributionen av vissa program.
- Att granska eller flytta kan skapa avbrott eller lägga till kostnader.
- Hastigheten och stabiliteten för VPN kan störa migreringen.
- Trafik som går in i molnet kan orsaka säkerhets problem i andra delar av det globala nätverket.

## <a name="incremental-improvement-of-the-policy-statements"></a>Stegvis förbättring av princip uttrycken

Följande ändringar i principen hjälper dig att åtgärda de nya riskerna och guidens implementering.

- Den valda moln leverantören måste erbjuda ett sätt att autentisera via äldre metoder.
- Den valda moln leverantören måste erbjuda ett sätt att autentisera med den aktuella tredjeparts Multi-Factor Authentication-lösningen.
- En höghastighets privat anslutning ska upprättas mellan moln leverantören och företagets Telco-leverantör, vilket ansluter moln leverantören till det globala nätverket av data Center.
- Ingen inkommande offentlig trafik kan komma åt företagets till gångar som finns i molnet tills tillräckligt med säkerhets krav har upprättats. Alla portar blockeras från alla källor utanför det globala WAN-nätverket.

## <a name="incremental-improvement-of-the-best-practices"></a>Stegvis förbättring av bästa praxis

Designen för styrnings MVP ändras till att inkludera nya Azure-principer och en implementering av Active Directory på en virtuell dator. Tillsammans uppfyller dessa två design ändringar de nya företags princip satserna.

Här är de nya bästa metoderna:

- **Skydda hybrid VNet-skiss:** Den lokala sidan av hybrid nätverket bör konfigureras för att tillåta kommunikation mellan följande lösningar och de lokala Active Directory-servrarna. Den här rekommenderade metoden kräver en DMZ för att aktivera Active Directory Domain Services över nätverks gränserna.
- **Azure Resource Manager mallar:**
    1. Definiera en NSG för att blockera extern trafik och tillåta intern trafik.
    2. Distribuera två Active Directory virtuella datorer i ett belastnings Utjämnings par baserat på en gyllene bild. Vid den första starten kör avbildningen ett PowerShell-skript för att ansluta till domänen och registrera med domän tjänster. Mer information finns i [utöka Active Directory Domain Services (AD DS) till Azure](https://docs.microsoft.com/azure/architecture/reference-architectures/identity/adds-extend-domain).
- Azure Policy: Tillämpa NSG på alla resurser.
- Azure-skiss:
    1. Skapa en skiss med `active-directory-virtual-machines`namnet.
    2. Lägg till var och en av Active Directory mallar och principer till skissen.
    3. Publicera skissen till alla tillämpliga hanterings grupper.
    4. Använd skissen för alla prenumerationer som kräver äldre autentisering med flera företag eller andra leverantörer.
    5. Instansen av Active Directory som körs i Azure kan nu användas som en utökning av den lokala Active Directory-lösningen, så att den kan integreras med det befintliga Multi-Factor Authentication-verktyget och tillhandahålla anspråksbaserad autentisering, både via befintliga Active Directory-funktioner.

## <a name="conclusion"></a>Sammanfattning

Genom att lägga till dessa ändringar i styrnings MVP: n kan du åtgärda många av riskerna i den här artikeln, så att varje moln antagande team snabbt kan gå förbi den här Roadblock.

## <a name="next-steps"></a>Nästa steg

När moln implementeringen fortsätter och levererar ytterligare affärs värde, kommer risker och moln styrnings behov också att ändras. Följande är några ändringar som kan uppstå. För det här fiktiva företaget är nästa utlösare att inkludera skyddade data i moln implementerings planen. Den här ändringen kräver ytterligare säkerhets kontroller.

> [!div class="nextstepaction"]
> [Förbättra säkerhets bas linje disciplinen](./security-baseline-improvement.md)
