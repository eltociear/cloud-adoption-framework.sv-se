---
title: Automatisera registrering och aviserings konfiguration
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Automatisera registrering och aviserings konfiguration
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 86997d8c433c23d6ecbe5d3ac124623d318099c0
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/06/2019
ms.locfileid: "70833094"
---
# <a name="automate-onboarding"></a>Automatisera onboarding

Överväg att automatisera distributionen av hanterings tjänster genom att följa rekommendationerna som beskrivs i föregående avsnitt i den här vägledningen för att förbättra effektiviteten vid distribution av Azure Server Management Services. Skript-och exempel mallarna som anges i följande avsnitt är start punkter för att utveckla din egen automatisering av onboarding-processer.

## <a name="onboarding-by-using-automation"></a>Onboarding med hjälp av Automation

Den här vägledningen har en stödjande GitHub-lagringsplats med exempel kod, [CloudAdoptionFramework](https://aka.ms/CAF/manage/automation-samples), som innehåller exempel skript och Azure Resource Manager mallar som hjälper dig att automatisera distributionen av Azure Server Management Services.

De här exempelfilerna illustrerar hur du använder Azure PowerShell cmdlets för att automatisera följande uppgifter:

1. Skapa en [Log Analytics arbets yta](/azure/azure-monitor/platform/manage-access) (eller Använd en befintlig arbets yta om den uppfyller&mdash;kraven se [planering av arbets yta](./prerequisites.md#log-analytics-workspace-and-automation-account-planning)).

2. Skapa ett Automation-konto (eller Använd ett befintligt konto om det uppfyller kraven&mdash;se [planering av arbets yta](./prerequisites.md#log-analytics-workspace-and-automation-account-planning)).

3. Länka Automation-kontot och Log Analytics arbets ytan (krävs inte om du registrerar via portalen).

4. Aktivera Uppdateringshantering och Ändringsspårning och inventering för arbets ytan.

5. Publicera virtuella Azure-datorer med Azure Policy (en princip installerar Log Analytics agent och Dependency Agent på virtuella Azure-datorer).

6. Publicera lokala servrar genom att installera Log Analytics-agenten på dem.

Filerna som beskrivs i följande tabell används i det här exemplet och du kan anpassa dem så att de stöder dina egna distributions scenarier.

| Filnamn | Beskrivning |
|-----------|-------------|
| New-AMSDeployment. ps1 | Huvud-och Dirigerings skript som automatiserar onboarding. Det här PowerShell-skriptet kräver en befintlig prenumeration, men skapar resurs grupper, plats, arbets yta och Automation-konton om de inte finns. |
| Workspace-AutomationAccount.json | En Resource Manager-mall som distribuerar arbets ytans och automations konto resurser. |
| WorkspaceSolutions.json | En Resource Manager-mall som möjliggör de önskade lösningarna i Log Analytics-arbetsytan. |
| ScopeConfig.json | En Resource Manager-mall som använder opt-in-modellen för lokala servrar med ändrings spårnings lösningen. Att använda opt-in-modellen är valfritt. |
| Enable-VMInsightsPerfCounters.ps1 | Ett PowerShell-skript som aktiverar VMInsight för servrar och konfigurerar prestanda räknare. |
| ChangeTracking-Filelist.json | En Resource Manager-mall som definierar en lista över filer som ska övervakas av Ändringsspårning. |

Du kan köra New-AMSDeployment. ps1 med hjälp av följande kommando:

```powershell
.\New-AMSDeployment.ps1 -SubscriptionName '{Subscription Name}' -WorkspaceName '{Workspace Name}' -WorkspaceLocation '{Azure Location}' -AutomationAccountName {Account Name} -AutomationAccountLocation {Account Location}
```

## <a name="next-steps"></a>Nästa steg

Lär dig hur du konfigurerar grundläggande aviseringar för att meddela ditt team om viktiga hanterings händelser och problem.

> [!div class="nextstepaction"]
> [Konfigurera grundläggande aviseringar](./setup-alerts.md)
