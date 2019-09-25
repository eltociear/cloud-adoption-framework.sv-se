---
title: Konfigurera Azure Management Services för en prenumeration
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Konfigurera Azure Management Services för en prenumeration
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: a5b1d551f52ae8800e9a29d4c8a92c14965645cc
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/24/2019
ms.locfileid: "71221511"
---
# <a name="configure-azure-management-services-at-scale"></a>Konfigurera hanterings tjänster i Azure i stor skala

Att integrera Azures hanterings tjänster på dina servrar omfattar två uppgifter: Distribuera tjänst agenter till dina servrar och aktivera hanterings lösningarna. Den här artikeln beskriver följande processer som gör att du kan utföra de här uppgifterna:

- [Distribuera nödvändiga agenter till virtuella Azure-datorer med Azure Policy](#deploy-extensions-to-azure-vms-using-azure-policy)
- [Distribuera nödvändiga agenter till lokala servrar](#install-required-agents-on-on-premises-servers)
- [Aktivera och konfigurera lösningar](#enable-and-configure-solutions)

> [!NOTE]
> Skapa den nödvändiga [Log Analytics arbets ytan och Azure Automation kontot](./prerequisites.md#create-a-workspace-and-automation-account) innan du registrerar virtuella datorer i Azure Management Services.

## <a name="deploy-extensions-to-azure-vms-using-azure-policy"></a>Distribuera tillägg till virtuella Azure-datorer med Azure Policy

Alla hanterings lösningar som diskuteras i [Azures hanterings verktyg och tjänster](./tools-services.md) kräver att Log Analytics Agent installeras på virtuella Azure-datorer (VM) och lokala servrar. Du kan publicera dina virtuella Azure-datorer i skala med hjälp av Azure Policy. Tilldela en princip för att säkerställa att agenten är installerad på alla virtuella Azure-datorer och är anslutna till rätt Log Analytics-arbetsyta.

Azure Policy har ett inbyggt [princip initiativ](/azure/governance/policy/index#initiative-definition) som innehåller både Log Analytics-agenten och [Microsofts beroende agent](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-onboard#the-microsoft-dependency-agent), vilket krävs av Azure Monitor for VMS.

<!-- TODO: Add these when available.
- [Preview]: Enable Azure Monitor for virtual machine scale sets.
- [Preview]: Enable Azure Monitor for VMs.
 -->

> [!NOTE]
> Mer information om olika agenter för Azure-övervakning finns i [Översikt över Azure Monitoring agents](https://docs.microsoft.com/azure/azure-monitor/platform/agents-overview).

### <a name="assign-policies"></a>Tilldela principer

Så här tilldelar du de principer som anges i föregående avsnitt:

1. I Azure Portal går du till **Azure policy** > **tilldelningar** > **tilldela initiativ**.

    ![Skärm bild av portalens princip gränssnitt](./media/onboarding-at-scale1.png)

2. På sidan **tilldela princip** väljer du omfånget genom att klicka på ellipsen (...) och väljer sedan antingen en hanterings grupp eller prenumeration. Du kan även välja en resursgrupp. En omfattning avgör vilka resurser eller grupper av resurser som principen är tilldelad till. Välj sedan **Välj** längst ned på sidan **omfång** .

3. Välj ellipsen (...) bredvid **princip definition** för att öppna listan över tillgängliga definitioner. Du kan filtrera initiativ definitionen genom att ange **Azure Monitor** i **sökrutan:**

    ![Skärm bild av portalens princip gränssnitt](./media/onboarding-at-scale2.png)

4. **Tilldelnings namnet** fylls i automatiskt med namnet på principen som du har valt, men du kan ändra det. Du kan också lägga till en valfri beskrivning om du vill ha mer information om den här princip tilldelningen. Fältet **tilldelad av** fylls i automatiskt baserat på vem som är inloggad. Det här fältet är valfritt och anpassade värden kan anges.

5. För den här principen väljer du **Log Analytics arbets yta** som Log Analytics-agenten ska kopplas till.

    ![Skärm bild av portalens princip gränssnitt](./media/onboarding-at-scale3.png)

6. Kontrol lera **platsen**för den hanterade identiteten. Om den här principen är av typen [DeployIfNotExists](https://docs.microsoft.com/azure/governance/policy/concepts/effects#deployifnotexists), krävs en hanterad identitet för att distribuera principen. I portalen skapas kontot enligt vad som anges i kryss rutan.

7. Välj **Tilldela**.

När du har slutfört guiden kommer princip tilldelningen att distribueras till miljön. Det kan ta upp till 30 minuter innan principen träder i funktion. Du kan testa det genom att skapa nya virtuella datorer efter 30 minuter och sedan kontrol lera om Microsoft Monitoring Agent (MMA) är aktive rad på den virtuella datorn som standard.

## <a name="install-required-agents-on-on-premises-servers"></a>Installera nödvändiga agenter på lokala servrar

> [!NOTE]
> Skapa den nödvändiga [Log Analytics arbets ytan och Azure Automation kontot](./prerequisites.md#create-a-workspace-and-automation-account) innan du registrerar servrar i Azure Management Services.

För lokala servrar måste du ladda ned och installera [Log Analytics agenten och Microsofts beroende agent](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-enable-hybrid-cloud) manuellt och konfigurera dem för att ansluta till rätt arbets yta. Gör detta genom att ange arbetsyte-ID och nyckelinformation, som du kan hitta genom att gå till din Log Analytics arbets yta i Azure Portal och välja **Inställningar** > **Avancerade inställningar**.

![Skärm bild av Log Analytics avancerade inställningar för arbets ytan i Azure Portal](./media/onboarding-on-premises.png)

## <a name="enable-and-configure-solutions"></a>Aktivera och konfigurera lösningar

Om du vill aktivera lösningar måste du konfigurera Log Analytics arbets ytan. Virtuella Azure-datorer och lokala servrar kommer att hämta lösningar från de Log Analytics arbets ytor som de är anslutna till.

Följande lösningar beskrivs i det här avsnittet:

- [Hantering av uppdateringar](#update-management)
- [Ändringsspårning och inventering](#change-tracking-and-inventory-solutions)
- [Azure aktivitets logg](#azure-activity-log)
- [Azure Log Analytics Agenthälsa](#azure-log-analytics-agent-health)
- [Utvärdering av program mot skadlig kod](#antimalware-assessment)
- [Azure Monitor for VMs](#azure-monitor-for-vms)
- [Azure Security Center](#azure-security-center)

### <a name="update-management"></a>Uppdateringshantering

Uppdateringshantering, Ändringsspårning och inventerings lösningar kräver både en Log Analytics arbets yta och ett Automation-konto. För att säkerställa att dessa resurser är korrekt konfigurerade rekommenderar vi att du registrerar dig via Automation-kontot. Mer information finns i [uppdateringshantering-, ändringsspårning-och inventerings lösningar](https://docs.microsoft.com/azure/automation/automation-onboard-solutions-from-automation-account).

Vi rekommenderar att du aktiverar Uppdateringshantering-lösning för alla servrar. Uppdateringshantering är kostnads fritt för virtuella Azure-datorer och lokala servrar. Om du aktiverar Uppdateringshantering via ditt Automation-konto skapas en [omfattnings konfiguration](https://docs.microsoft.com/azure/automation/automation-onboard-solutions-from-automation-account#scope-configuration) i arbets ytan. Du måste uppdatera omfattningen manuellt för att inkludera datorer som omfattas av uppdaterings tjänsten.

Om du vill ta med alla befintliga servrar och framtida servrar måste du ta bort omfattnings konfigurationen. Det gör du genom att visa ditt Automation-konto i Azure Portal och välja **uppdateringshantering** > **Hantera dator** > **aktivering på alla tillgängliga och framtida datorer**. Om du aktiverar den här inställningen kan alla virtuella Azure-datorer som är anslutna till arbets ytan använda Uppdateringshantering.

![Skärm bild av Uppdateringshantering i Azure Portal](./media/onboarding-configuration1.png)

### <a name="change-tracking-and-inventory-solutions"></a>Ändringsspårning-och inventerings lösningar

Om du vill publicera Ändringsspårning-och inventerings lösningar följer du samma steg som för Uppdateringshantering. Mer information om hur du registrerar dessa lösningar från ditt Automation-konto finns i [uppdateringshantering-, ändringsspårning-och inventerings lösningar](https://docs.microsoft.com/azure/automation/automation-onboard-solutions-from-automation-account).

Ändringsspårning lösningen är kostnads fri för virtuella Azure-datorer och kostnader $6 per nod per månad för lokala servrar. Kostnaden täcker Ändringsspårning, inventering och önskad tillstånds konfiguration. Om du vill registrera endast vissa lokala servrar kan du välja dessa servrar. Vi rekommenderar att du registrerar alla produktions servrar.

#### <a name="opt-in-via-the-azure-portal"></a>Välj via Azure Portal

1. Gå till Automation-kontot där Ändringsspårning och inventering har Aktiver ATS.
2. Välj **ändrings spårning**.
3. Välj **hantera datorer** i den högra rutan längst upp.
4. Välj **Aktivera på valda datorer**och välj de datorer som ska aktive ras genom att klicka på **Lägg till** bredvid dator namnet.
5. Välj **Aktivera** för att aktivera lösningen för de datorerna.

![Skärm bild av Ändringsspårning i Azure Portal](./media/onboarding-configuration2.png)

#### <a name="opt-in-by-using-saved-searches"></a>Välj genom att använda sparade sökningar

Du kan också konfigurera omfattnings konfigurationen om du vill välja lokala servrar. I omfattnings konfigurationen används sparade sökningar.

Använd följande steg för att skapa eller ändra den sparade sökningen:

1. Gå till arbets ytan Log Analytics som är länkad till ditt Automation-konto som du konfigurerade i föregående steg.

2. Under **Allmänt**väljer du **sparade sökningar**.

3. I rutan **filter** anger du **ändringsspårning** för att filtrera listan över sparade sökningar. I resultaten väljer du **MicrosoftDefaultComputerGroup**.

4. Ange dator namnet eller VMUUID för att inkludera de datorer som du vill välja för Ändringsspårning.

    ```kusto
    Heartbeat
    | where AzureEnvironment=~"Azure" or Computer in~ ("list of the on-premises server names", "server1")
    | distinct Computer
    ```

    > [!NOTE]
    > Server namnet måste exakt matcha värdet som ingår i uttrycket och det får inte innehålla ett domänsuffix.

5. Välj **Spara**.

6. Som standard är omfattnings konfigurationen länkad till den sparade **MicrosoftDefaultComputerGroup** -sökningen och uppdateras automatiskt.

### <a name="azure-activity-log"></a>Azure-aktivitetsloggen

[Azure aktivitets logg](https://docs.microsoft.com/azure/azure-monitor/platform/activity-logs-overview) ingår också i Azure Monitor. Den ger inblick i händelser på prenumerations nivå som inträffar i Azure.

Så här lägger du till den här lösningen:

1. I Azure Portal öppnar du **alla tjänster** och väljer hanterings-och **styrnings** > **lösningar**.
2. I vyn **lösningar** väljer du **Lägg till**.
3. Sök efter **Aktivitetslogganalys** och markera det.
4. Välj **Skapa**.

Du måste ange **arbets ytans namn** på arbets ytan som du skapade i föregående avsnitt där lösningen är aktive rad.

### <a name="azure-log-analytics-agent-health"></a>Azure Log Analytics Agenthälsa

Azure Log Analytics Agenthälsa-lösningen ger dig insikt i hälsa, prestanda och tillgänglighet för dina Windows-och Linux-servrar.

Så här lägger du till den här lösningen:

1. I Azure Portal öppnar du **alla tjänster** och väljer hanterings-och **styrnings** > **lösningar**.
2. I vyn **lösningar** väljer du **Lägg till**.
3. Sök efter **hälso tillstånd för Azure-Log Analytics agent** och markera det.
4. Välj **Skapa**.

Du måste ange **arbets ytans namn** på arbets ytan som du skapade i föregående avsnitt där lösningen är aktive rad.

När du har skapat den här arbets ytan visar resurs instansen **AgentHealthAssessment** när du väljer **Visa** > **lösningar**.

### <a name="antimalware-assessment"></a>Utvärdering av program mot skadlig kod

Lösningen för utvärdering av program mot skadlig kod hjälper dig att identifiera servrar som är smittade eller som ökar risken för infektion av skadlig kod.

Så här lägger du till den här lösningen:

1. I Azure Portal öppnar du **alla tjänster** och väljer hanterings-och **styrnings** > **lösningar**.
2. I vyn **lösningar** väljer du **Lägg till**.
3. Sök efter **utvärdering av program mot skadlig kod** och välj den.
4. Välj **Skapa**.

Du måste ange **arbets ytans namn** på arbets ytan som du skapade i föregående avsnitt där lösningen är aktive rad.

När du har skapat den här arbets ytan visar resurs instansen **program mot skadlig kod** när du väljer **Visa** > **lösningar**.

### <a name="azure-monitor-for-vms"></a>Azure Monitor för virtuella datorer

Du kan aktivera [Azure Monitor for VMS](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-overview) via sidan Visa för VM-instansen, enligt beskrivningen i föregående artikel, [Aktivera hanterings tjänster på en enskild virtuell dator för utvärdering](./onboard-single-vm.md). Du bör inte aktivera lösningar direkt från sidan **lösningar** på samma sätt som du gjorde för de andra lösningarna som beskrivs i den här artikeln. För storskaliga distributioner kan det vara lättare att använda [Automation](./onboarding-automation.md) för att aktivera rätt lösningar i arbets ytan.

### <a name="azure-security-center"></a>Azure Security Center

I den här vägledningen rekommenderar vi att du registrerar alla servrar till Azure Security Center *kostnads fri* nivå som standard. Det här alternativet ger dig en grundläggande nivå av säkerhets utvärderingar och åtgärds bara säkerhets rekommendationer för din miljö. Uppgradering till Security Center *standard* nivån ger ytterligare förmåner, som beskrivs i detalj på [sidan för Security Center prissättning](https://docs.microsoft.com/azure/security-center/security-center-pricing).

Använd följande steg för att aktivera den kostnads fria nivån för Azure Security Center:

1. Gå till sidan **Security Center** Portal.
2. Välj **säkerhets princip** under **princip & efterlevnad**.
3. Hitta den Log Analytics arbets ytans resurs som du har skapat i det högra fönstret.
4. Välj **Redigera inställningar >** för arbets ytan.
5. Välj **Prisnivå**.
6. Välj alternativet **kostnads fri** .
7. Välj **Spara**.

## <a name="next-steps"></a>Nästa steg

Lär dig hur du använder Automation för att publicera servrar och skapa aviseringar.

> [!div class="nextstepaction"]
> [Automatisera registrering och aviserings konfiguration](./onboarding-automation.md)
