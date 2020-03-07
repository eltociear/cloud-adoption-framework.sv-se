---
title: Konfigurera tjänsten för en prenumeration
description: Lär dig att konfigurera Azure Server Management Services för en prenumeration genom att distribuera tjänst agenter till dina servrar och aktivera hanterings lösningar.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: cb34f026b5161b20fc6e3a20bf4993b6b44ede4f
ms.sourcegitcommit: 0ea426f2f471eb7310c6f09478be1306cf7bf0d8
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/05/2020
ms.locfileid: "78341612"
---
# <a name="configure-azure-server-management-services-at-scale"></a>Konfigurera Azure Server Management Services i stor skala

Du måste utföra dessa två uppgifter för att kunna publicera Azure Server Management Services till dina servrar:
- Distribuera tjänst agenter till dina servrar
- Aktivera hanterings lösningar

Den här artikeln beskriver de tre processer som krävs för att utföra dessa uppgifter:

1. Distribuera de nödvändiga agenterna till virtuella Azure-datorer med hjälp av Azure Policy
1. Distribuera de nödvändiga agenterna till lokala servrar
1. Aktivera och konfigurera lösningarna

> [!NOTE]
> Skapa den nödvändiga [Log Analytics arbets ytan och Azure Automation kontot](./prerequisites.md#create-a-workspace-and-automation-account) innan du registrerar virtuella datorer i Azure Server Management Services.

## <a name="use-azure-policy-to-deploy-extensions-to-azure-vms"></a>Använd Azure Policy för att distribuera tillägg till virtuella Azure-datorer

Alla hanterings lösningar som beskrivs i [Azures hanterings verktyg och tjänster](./tools-services.md) kräver att Log Analytics Agent installeras på virtuella Azure-datorer och lokala servrar. Du kan publicera dina virtuella Azure-datorer i skala med hjälp av Azure Policy. Tilldela en princip för att säkerställa att agenten är installerad på dina virtuella Azure-datorer och är anslutna till rätt Log Analytics-arbetsyta.

Azure Policy har ett inbyggt [princip initiativ](https://docs.microsoft.com/azure/governance/policy/concepts/definition-structure#initiatives) som innehåller Log Analytics agent och [Microsofts beroende agent](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-onboard#the-microsoft-dependency-agent), vilket krävs av Azure Monitor for VMS.

<!-- TODO: Add these when available.
- [Preview]: Enable Azure Monitor for virtual machine scale sets.
- [Preview]: Enable Azure Monitor for VMs.
 -->

> [!NOTE]
> Mer information om olika agenter för Azure-övervakning finns i [Översikt över Azure Monitoring agents](https://docs.microsoft.com/azure/azure-monitor/platform/agents-overview).

### <a name="assign-policies"></a>Tilldela principer

Så här tilldelar du de principer som beskrivs i föregående avsnitt:

1. I Azure Portal går du till **Azure Policy** > **tilldelningar** > **tilldela initiativ**.

    ![Skärm bild av portalens princip gränssnitt](./media/onboarding-at-scale1.png)

2. På sidan **tilldela princip** anger du **omfånget** genom att välja ellipsen (...) och sedan välja antingen en hanterings grupp eller en prenumeration. Du kan även välja en resursgrupp. Välj sedan **Välj** längst ned på sidan **omfång** . Omfånget avgör vilka resurser eller grupper av resurser som principen är tilldelad till.

3. Välj ellipsen ( **...** ) bredvid **princip definition** för att öppna listan över tillgängliga definitioner. Om du vill filtrera initiativ definitionerna anger **Azure Monitor** i **sökrutan:**

    ![Skärm bild av portalens princip gränssnitt](./media/onboarding-at-scale2.png)

4. **Tilldelnings namnet** fylls i automatiskt med namnet på principen som du har valt, men du kan ändra det. Du kan också lägga till en valfri beskrivning om du vill ha mer information om den här princip tilldelningen. Fältet **tilldelad av** fylls i automatiskt baserat på vem som är inloggad. Det här fältet är valfritt och stöder anpassade värden.

5. För den här principen väljer du **Log Analytics arbets yta** som Log Analytics-agenten ska kopplas till.

    ![Skärm bild av portalens princip gränssnitt](./media/onboarding-at-scale3.png)

6. Markera kryss rutan **plats för hanterad identitet** . Om den här principen är av typen [DeployIfNotExists](https://docs.microsoft.com/azure/governance/policy/concepts/effects#deployifnotexists)krävs en hanterad identitet för att distribuera principen. I portalen skapas kontot enligt vad som anges i kryss rutan.

7. Välj **Tilldela**.

När du har slutfört guiden kommer princip tilldelningen att distribueras till miljön. Det kan ta upp till 30 minuter innan principen träder i funktion. Testa det genom att skapa nya virtuella datorer efter 30 minuter och kontrol lera om Microsoft Monitoring Agent är aktive rad på den virtuella datorn som standard.

## <a name="install-agents-on-on-premises-servers"></a>Installera agenter på lokala servrar

> [!NOTE]
> Skapa den nödvändiga [Log Analytics arbets ytan och Azure Automation kontot](./prerequisites.md#create-a-workspace-and-automation-account) innan du hanterar Azure Server Management-tjänster till servrar.

För lokala servrar måste du ladda ned och installera [Log Analytics agenten och Microsofts beroende agent](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-enable-hybrid-cloud) manuellt och konfigurera dem för att ansluta till rätt arbets yta. Du måste ange arbetsyte-ID och viktig information. För att hämta den informationen går du till arbets ytan Log Analytics i Azure Portal och väljer sedan **inställningar** > **Avancerade inställningar**.

![Skärm bild av Log Analytics avancerade inställningar för arbets ytan i Azure Portal](./media/onboarding-on-premises.png)

## <a name="enable-and-configure-solutions"></a>Aktivera och konfigurera lösningar

För att kunna aktivera lösningar måste du konfigurera Log Analytics-arbetsytan. Virtuella Azure-datorer och lokala servrar kommer att hämta lösningar från Log Analytics arbets ytor som de är anslutna till.

### <a name="update-management"></a>Uppdateringshantering

Uppdateringshantering-, Ändringsspårning-och inventerings lösningar kräver både en Log Analytics arbets yta och ett Automation-konto. För att säkerställa att dessa resurser är korrekt konfigurerade rekommenderar vi att du går igenom ditt Automation-konto. Mer information finns i [uppdateringshantering-, ändringsspårning-och inventerings lösningar](https://docs.microsoft.com/azure/automation/automation-onboard-solutions-from-automation-account).

Vi rekommenderar att du aktiverar Uppdateringshantering-lösningen för alla servrar. Uppdateringshantering är kostnads fritt för virtuella Azure-datorer och lokala servrar. Om du aktiverar Uppdateringshantering via ditt Automation-konto skapas en [omfattnings konfiguration](https://docs.microsoft.com/azure/automation/automation-onboard-solutions-from-automation-account#scope-configuration) i arbets ytan. Uppdatera omfånget manuellt för att inkludera datorer som omfattas av tjänsten Uppdateringshantering.

För att kunna hantera befintliga servrar och framtida servrar måste du ta bort omfattnings konfigurationen. Det gör du genom att visa ditt Automation-konto i Azure Portal. Välj **Uppdateringshantering** > **Hantera dator** > **Aktivera på alla tillgängliga och framtida datorer**. Med den här inställningen kan alla virtuella Azure-datorer som är anslutna till arbets ytan använda Uppdateringshantering.

![Skärm bild av Uppdateringshantering i Azure Portal](./media/onboarding-configuration1.png)

### <a name="change-tracking-and-inventory-solutions"></a>Ändringsspårning-och inventerings lösningar

Om du vill publicera Ändringsspårning-och inventerings lösningar följer du samma steg som för Uppdateringshantering. Mer information om hur du kan publicera dessa lösningar från ditt Automation-konto finns i [uppdateringshantering, ändringsspårning och inventerings lösningar](https://docs.microsoft.com/azure/automation/automation-onboard-solutions-from-automation-account).

Ändringsspårning lösningen är kostnads fri för virtuella Azure-datorer och kostnader $6 per nod per månad för lokala servrar. Kostnaden täcker Ändringsspårning, inventering och önskad tillstånds konfiguration. Om du bara vill registrera vissa lokala servrar kan du välja dessa servrar. Vi rekommenderar att du registrerar alla produktions servrar.

#### <a name="opt-in-via-the-azure-portal"></a>Välj via Azure Portal

1. Gå till Automation-kontot där Ändringsspårning och inventering har Aktiver ATS.
2. Välj **ändrings spårning**.
3. Välj **hantera datorer** i det övre högra fönstret.
4. Välj **Aktivera på valda datorer**. Välj sedan **Lägg till** bredvid dator namnet.
5. Välj **Aktivera** för att aktivera lösningen för de datorerna.

![Skärm bild av Ändringsspårning i Azure Portal](./media/onboarding-configuration2.png)

#### <a name="opt-in-by-using-saved-searches"></a>Välj genom att använda sparade sökningar

Du kan också konfigurera omfattnings konfigurationen om du vill välja lokala servrar. I omfattnings konfigurationen används sparade sökningar.

Följ dessa steg om du vill skapa eller ändra den sparade sökningen:

1. Gå till arbets ytan Log Analytics som är länkad till Automation-kontot som du konfigurerade i föregående steg.

1. Under **Allmänt**väljer du **sparade sökningar**.

1. I rutan **filter** anger du **ändringsspårning** för att filtrera listan över sparade sökningar. I resultaten väljer du **MicrosoftDefaultComputerGroup**.

1. Ange dator namnet eller VMUUID för att inkludera de datorer som du vill välja för Ändringsspårning.

    ```kusto
    Heartbeat
    | where AzureEnvironment=~"Azure" or Computer in~ ("list of the on-premises server names", "server1")
    | distinct Computer
    ```

    > [!NOTE]
    > Server namnet måste exakt matcha värdet i uttrycket och det får inte innehålla ett domänsuffix.

1. Välj **Spara**. Som standard är omfattnings konfigurationen länkad till den sparade **MicrosoftDefaultComputerGroup** -sökningen. Den uppdateras automatiskt.

### <a name="azure-activity-log"></a>Azure-aktivitetslogg

[Azure aktivitets logg](https://docs.microsoft.com/azure/azure-monitor/platform/activity-logs-overview) ingår också i Azure Monitor. Den ger inblick i händelser på prenumerations nivå som inträffar i Azure.

För att implementera den här lösningen:

1. I Azure Portal öppnar du **alla tjänster**och väljer sedan **hanterings-och styrnings** > **lösningar**.
2. I vyn **lösningar** väljer du **Lägg till**.
3. Sök efter **Aktivitetslogganalys** och markera det.
4. Välj **Skapa**.

Du måste ange **arbets ytans namn** på arbets ytan som du skapade i föregående avsnitt där lösningen är aktive rad.

### <a name="azure-log-analytics-agent-health"></a>Azure Log Analytics Agenthälsa

Azure Log Analytics Agenthälsa-lösningen rapporterar om hälsa, prestanda och tillgänglighet för dina Windows-och Linux-servrar.

För att implementera den här lösningen:

1. I Azure Portal öppnar du **alla tjänster**och väljer sedan **hanterings-och styrnings** > **lösningar**.
2. I vyn **lösningar** väljer du **Lägg till**.
3. Sök efter **hälso tillstånd för Azure-Log Analytics agent** och markera det.
4. Välj **Skapa**.

Du måste ange **arbets ytans namn** på arbets ytan som du skapade i föregående avsnitt där lösningen är aktive rad.

När du har skapat en arbets yta visas **AgentHealthAssessment** när du väljer **Visa** > - **lösningar**på arbets ytans resurs instans.

### <a name="antimalware-assessment"></a>Utvärdering av program mot skadlig kod

Lösningen för utvärdering av program mot skadlig kod hjälper dig att identifiera servrar som är smittade eller som ökar risken för infektion av skadlig kod.

För att implementera den här lösningen:

1. I Azure Portal öppnar du **alla tjänster**och väljer Välj **hantering + styrning** > **lösningar**.
2. I vyn **lösningar** väljer du **Lägg till**.
3. Sök efter och välj **utvärdering av program mot skadlig kod**.
4. Välj **Skapa**.

Du måste ange **arbets ytans namn** på arbets ytan som du skapade i föregående avsnitt där lösningen är aktive rad.

När du har skapat den här arbets ytan visar resurs instansen **program mot skadlig kod** när du väljer **Visa** > - **lösningar**.

### <a name="azure-monitor-for-vms"></a>Azure Monitor för virtuella datorer

Du kan aktivera [Azure Monitor for VMS](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-overview) via sidan Visa för VM-instansen, enligt beskrivningen i [Aktivera hanterings tjänster på en enskild virtuell dator för utvärdering](./onboard-single-vm.md). Du bör inte aktivera lösningar direkt från **lösnings** sidan för de andra lösningarna som beskrivs i den här artikeln. För storskaliga distributioner kan det vara lättare att använda [Automation](./onboarding-automation.md) för att aktivera rätt lösningar i arbets ytan. 

### <a name="azure-security-center"></a>Azure Security Center

Vi rekommenderar att du registrerar alla dina servrar minst på den Azure Security Center *kostnads fria* nivån. Det här alternativet ger en grundläggande nivå av säkerhets utvärderingar och åtgärds bara säkerhets rekommendationer för din miljö. Om du uppgraderar till *standard* nivån får du ytterligare förmåner, som beskrivs i detalj på [sidan Security Center prissättning](https://docs.microsoft.com/azure/security-center/security-center-pricing).

Följ dessa steg om du vill aktivera Azure Security Center kostnads fri nivå:

1. Gå till sidan **Security Center** Portal.
2. Under **princip &AMP; efterlevnad**väljer du **säkerhets princip**.
3. Hitta Log Analytics arbets ytans resurs som du skapade i fönstret till höger.
4. Välj **Redigera inställningar** för arbets ytan.
5. Välj **Prisnivå**.
6. Välj alternativet **kostnads fri** .
7. Välj **Spara**.

## <a name="next-steps"></a>Nästa steg

Lär dig hur du använder Automation för att publicera servrar och skapa aviseringar.

> [!div class="nextstepaction"]
> [Automatisera registrering och aviserings konfiguration](./onboarding-automation.md)
