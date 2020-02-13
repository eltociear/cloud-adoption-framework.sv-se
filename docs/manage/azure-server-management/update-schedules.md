---
title: Skapa uppdaterings scheman
description: Använd Azure Portal eller de nya PowerShell cmdlet-modulerna för att hantera uppdaterings scheman.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 2f049fce8c109c3028fa84c5822c0eb1053023bb
ms.sourcegitcommit: 238e7a06b56950cebdcc8f75924849fc995e6ff2
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 02/12/2020
ms.locfileid: "77173362"
---
# <a name="create-update-schedules"></a>Skapa uppdaterings scheman

Du kan hantera uppdaterings scheman med hjälp av Azure Portal eller de nya PowerShell-cmdlet-modulerna.

Information om hur du skapar ett uppdaterings schema via Azure Portal finns i [Schemalägga en uppdaterings distribution](https://docs.microsoft.com/azure/automation/automation-tutorial-update-management#schedule-an-update-deployment).

AZ. Automation-modulen stöder nu konfiguration av uppdaterings hantering med hjälp av Azure PowerShell. [Version 1.7.0](https://www.powershellgallery.com/packages/Az/1.7.0) av modulen lägger till stöd för cmdleten [New-AzAutomationUpdateManagementAzureQuery](https://docs.microsoft.com/powershell/module/az.automation/new-azautomationupdatemanagementazurequery?view=azps-1.7.0) . Med den här cmdleten kan du använda taggar, platser och sparade sökningar för att konfigurera uppdaterings scheman för en flexibel grupp datorer.

## <a name="example-script"></a>Exempelskript

Exempel skriptet i det här avsnittet visar hur du använder taggning och frågor för att skapa dynamiska grupper av datorer som du kan använda uppdaterings scheman för. Den utför följande åtgärder. Du kan referera till implementeringarna av de specifika åtgärderna när du skapar egna skript.

- Skapar ett Azure Automation uppdaterings schema som körs varje lördag kl. 8:00.
- Skapar en fråga för datorer som matchar följande kriterier:
  - Distribuerat på `westus`, `eastus`eller `eastus2` Azure-platsen
  - Använd en `Owner`-tagg för dem med ett värde som är inställt på `JaneSmith`
  - Använd en `Production`-tagg för dem med ett värde som är inställt på `true`
- Tillämpar uppdaterings schemat på de efterfrågade datorerna och anger ett uppdaterings fönster med två timmar.

Innan du kör exempel skriptet måste du logga in med hjälp av cmdleten [Connect-AzAccount](https://docs.microsoft.com/powershell/module/az.accounts/connect-azaccount?view=azps-2.1.0) . Ange följande information när du startar skriptet:

- ID för mål prenumeration
- Mål resurs gruppen
- Namnet på din Log Analytics-arbetsyta
- Ditt Azure Automation konto namn

```powershell

    <#
        .SYNOPSIS
            This script orchestrates the deployment of the solutions and the agents.
        .Parameter SubscriptionName
        .Parameter WorkspaceName
        .Parameter AutomationAccountName
        .Parameter ResourceGroupName

    #>

    param (
        [Parameter(Mandatory=$true)]
        [string]$SubscriptionId,

        [Parameter(Mandatory=$true)]
        [string]$ResourceGroupName,

        [Parameter(Mandatory=$true)]
        [string]$WorkspaceName,

        [Parameter(Mandatory=$true)]
        [string]$AutomationAccountName,

        [Parameter(Mandatory=$false)]
        [string]$scheduleName = "SaturdayCritialSecurity"
    )

    Import-Module Az.Automation

    $startTime = ([DateTime]::Now).AddMinutes(10)
    $schedule = New-AzAutomationSchedule -ResourceGroupName $ResourceGroupName `
        -AutomationAccountName $AutomationAccountName `
        -StartTime $startTime `
        -Name $scheduleName `
        -Description "Saturday patches" `
        -DaysOfWeek Saturday `
        -WeekInterval 1 `
        -ForUpdateConfiguration

    # Using AzAutomationUpdateManagementAzureQuery to create dynamic groups.

    $queryScope = @("/subscriptions/$SubscriptionID/resourceGroups/")

    $query1Location =@("westus", "eastus", "eastus2")
    $query1FilterOperator = "Any"
    $ownerTag = @{"Owner"= @("JaneSmith")}
    $ownerTag.add("Production", "true")

    $DGQuery = New-AzAutomationUpdateManagementAzureQuery -ResourceGroupName $ResourceGroupName `
        -AutomationAccountName $AutomationAccountName `
        -Scope $queryScope `
        -Tag $ownerTag

    $AzureQueries = @($DGQuery)

    $UpdateConfig = New-AzAutomationSoftwareUpdateConfiguration -ResourceGroupName $ResourceGroupName `
        -AutomationAccountName $AutomationAccountName `
        -Schedule $schedule `
        -Windows `
        -Duration (New-TimeSpan -Hours 2) `
        -AzureQuery $AzureQueries `
        -IncludedUpdateClassification Security,Critical
```

## <a name="next-steps"></a>Nästa steg

Se exempel på hur du implementerar [vanliga principer i Azure](./common-policies.md) som kan hjälpa dig att hantera dina servrar.

> [!div class="nextstepaction"]
> [Vanliga principer i Azure](./common-policies.md)
