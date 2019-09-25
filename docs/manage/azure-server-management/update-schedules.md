---
title: Skapa uppdaterings scheman
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Skapa uppdaterings scheman
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 9e6e078859bb580794477328099b66d14009bdca
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/24/2019
ms.locfileid: "71221407"
---
# <a name="create-update-schedules"></a>Skapa uppdaterings scheman

Du kan hantera uppdaterings scheman med hjälp av Azure Portal eller de nya PowerShell-cmdlet-modulerna.

Information om hur du skapar ett uppdaterings schema via Azure Portal finns i [Schemalägga en uppdaterings distribution](https://docs.microsoft.com/azure/automation/automation-tutorial-update-management#schedule-an-update-deployment).

AZ. Automation-modulen stöder nu konfiguration av uppdaterings hantering med hjälp av Azure PowerShell. [Version 1.7.0](https://www.powershellgallery.com/packages/Az/1.7.0) av modulen lägger till stöd för cmdleten [New-AzAutomationUpdateManagementAzureQuery](/powershell/module/az.automation/new-azautomationupdatemanagementazurequery?view=azps-1.7.0) , vilket gör att du kan använda taggar, plats och sparade sökningar för att konfigurera uppdaterings scheman för en flexibel grupp datorer.

## <a name="example-script"></a>Exempelskript

Följande exempel skript illustrerar användningen av taggning och frågor för att skapa dynamiska grupper av datorer som du kan använda uppdaterings scheman för. Den utför följande åtgärder. Du kan referera till implementeringarna av de specifika åtgärderna när du skapar egna skript.

- Skapar ett Azure Automation uppdaterings schema som körs varje lördag kl. 8:00
- Skapar en fråga för datorer som matchar följande kriterier:
  - Distribuerad på `westus`, eller `eastus` `eastus2` Azure-platsen
  - Ha en `Owner` -tagg som tillämpas på dem med ett värde som är inställt på`JaneSmith`
  - Ha en `Production` -tagg som tillämpas på dem med ett värde som är inställt på`true`
- Tillämpar uppdaterings schemat på de efterfrågade datorerna och anger ett uppdaterings fönster med två timmar

Innan du kör exempel skriptet måste du logga in med hjälp av cmdleten [Connect-AzAccount](https://docs.microsoft.com/powershell/module/az.accounts/connect-azaccount?view=azps-2.1.0) . När du startar skriptet måste du ange följande information:

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

## Next steps

See examples of how to implement [common policies in Azure](./common-policies.md) that can help manage your servers.

> [!div class="nextstepaction"]
> [Common policies in Azure](./common-policies.md)
