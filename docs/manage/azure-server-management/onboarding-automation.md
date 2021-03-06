---
title: Automatisera onboarding
description: Använd exempel filen onboarding för att hjälpa dig att automatisera distributionen av Azure Server Management Services för att förbättra effektiviteten.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: cb612930318ed2ecd355cb5466f50650086d7f4c
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/31/2020
ms.locfileid: "80430574"
---
# <a name="automate-onboarding"></a>Automatisera onboarding

Du kan förbättra effektiviteten vid distribution av Azure Server Management Services genom att automatisera distributionen enligt beskrivningen i föregående avsnitt i den här vägledningen. Skript-och exempel mallarna som anges i följande avsnitt är start punkter för att utveckla din egen automatisering av onboarding-processer.

Den här vägledningen har en support GitHub-lagringsplats med exempel kod, [CloudAdoptionFramework](https://aka.ms/caf/manage/automation-samples). Lagrings platsen innehåller exempel skript och Azure Resource Manager mallar som hjälper dig att automatisera distributionen av Azure Server Management Services.

Exempelfilerna illustrerar hur du använder Azure PowerShell cmdlets för att automatisera följande uppgifter:

- Skapa en [Log Analytics-arbetsyta](https://docs.microsoft.com/azure/azure-monitor/platform/manage-access). (Du kan också använda en befintlig arbets yta om den uppfyller kraven. Mer information finns i [planering av arbets ytan](./prerequisites.md#log-analytics-workspace-and-automation-account-planning).

- Skapa ett Automation-konto. (Du kan också använda ett befintligt konto om det uppfyller kraven. Mer information finns i [planering av arbets yta](./prerequisites.md#log-analytics-workspace-and-automation-account-planning)).

- Länka Automation-kontot och Log Analytics-arbetsytan. Det här steget är inte obligatoriskt om du registrerar dig med hjälp av Azure Portal.

- Aktivera Uppdateringshantering och Ändringsspårning och inventering för arbets ytan.

- Publicera virtuella Azure-datorer med hjälp av Azure Policy. En princip installerar Log Analytics agent och Microsoft Dependency Agent på virtuella Azure-datorer.

- Publicera lokala servrar genom att installera Log Analytics-agenten på dem.

Filerna som beskrivs i följande tabell används i det här exemplet. Du kan anpassa dem så att de stöder dina egna distributions scenarier.

| Filnamn | Beskrivning |
|-----------|-------------|
| New-AMSDeployment. ps1 | Huvud-och Dirigerings skript som automatiserar onboarding. Det skapar resurs grupper, plats, arbets yta och Automation-konton, om de inte redan finns. Det här PowerShell-skriptet kräver en befintlig prenumeration. |
| Workspace-AutomationAccount.json | En Resource Manager-mall som distribuerar arbets ytans och automations konto resurser. |
| WorkspaceSolutions.json | En Resource Manager-mall som aktiverar de lösningar som du vill använda i arbets ytan Log Analytics. |
| ScopeConfig.json | En Resource Manager-mall som använder opt-in-modellen för lokala servrar med Ändringsspårning-lösningen. Att använda opt-in-modellen är valfritt. |
| Enable-VMInsightsPerfCounters.ps1 | Ett PowerShell-skript som möjliggör VM-insikter för servrar och konfigurerar prestanda räknare. |
| ChangeTracking-FileList. JSON | En Resource Manager-mall som definierar en lista över filer som ska övervakas av Ändringsspårning. |

Använd följande kommando för att köra New-AMSDeployment. ps1:

```powershell
.\New-AMSDeployment.ps1 -SubscriptionName '{Subscription Name}' -WorkspaceName '{Workspace Name}' -WorkspaceLocation '{Azure Location}' -AutomationAccountName {Account Name} -AutomationAccountLocation {Account Location}
```

## <a name="next-steps"></a>Nästa steg

Lär dig hur du konfigurerar grundläggande aviseringar för att meddela ditt team om viktiga hanterings händelser och problem.

> [!div class="nextstepaction"]
> [Konfigurera grundläggande aviseringar](./setup-alerts.md)
