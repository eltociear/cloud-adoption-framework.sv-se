---
title: Princip för gäst konfiguration
description: Princip för gäst konfiguration
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: c676766c2de524dcbe9ca66fc248c410b14e17d7
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 01/28/2020
ms.locfileid: "76808081"
---
# <a name="guest-configuration-policy"></a>Princip för gäst konfiguration

Du kan använda tillägget Azure Policy [gäst konfiguration](https://docs.microsoft.com/azure/governance/policy/concepts/guest-configuration) för att granska konfigurations inställningarna på en virtuell dator. Gäst konfigurationen stöds för närvarande endast på virtuella Azure-datorer.

Du hittar listan över principer för gäst konfiguration genom att söka efter "gäst konfiguration" på sidan Azure Policy Portal. Eller kör denna cmdlet i ett PowerShell-fönster för att hitta listan:

```powershell
Get-AzPolicySetDefinition | where-object {$_.Properties.metadata.category -eq "Guest Configuration"}
```

> [!NOTE]
> Gäst konfigurations funktionerna uppdateras regelbundet för att stödja ytterligare princip uppsättningar. Sök efter nya principer som stöds regelbundet och utvärdera om de ska vara användbara.

<!-- TODO: Update these links when available. 

By default, we recommend that you enable the following policies:

- [Preview]: Audit to verify that password-security settings are correct on Linux and Windows machines.
- Audit to verify that certificates are not nearing expiration on Windows VMs.

-->

## <a name="deployment"></a>Distribution

Använd följande exempel PowerShell-skript för att distribuera dessa principer till:

- Kontrol lera att inställningarna för lösen ords säkerhet på Windows-och Linux-datorer är korrekt inställda.
- Kontrol lera att certifikaten inte är nära förfallo datum för virtuella Windows-datorer.

 Innan du kör det här skriptet använder du cmdleten [Connect-AzAccount](https://docs.microsoft.com/powershell/module/az.accounts/connect-azaccount?view=azps-2.1.0) för att logga in. När du kör skriptet måste du ange namnet på den prenumeration som du vill tillämpa principerna på.

```powershell

    #Assign Guest Configuration policy.
    param (
        [Parameter(Mandatory=$true)]
        [string]$SubscriptionName
    )

    $Subscription = Get-AzSubscription -SubscriptionName $SubscriptionName
    $scope = "/subscriptions/" + $Subscription.Id

    $PasswordPolicy = Get-AzPolicySetDefinition -Name "3fa7cbf5-c0a4-4a59-85a5-cca4d996d5a6"
    $CertExpirePolicy = Get-AzPolicySetDefinition -Name "b6f5e05c-0aaa-4337-8dd4-357c399d12ae"

    New-AzPolicyAssignment -Name "PasswordPolicy" -DisplayName "[Preview]: Audit that password security settings are set correctly inside Linux and Windows machines" -Scope $scope -PolicySetDefinition $PasswordPolicy -AssignIdentity -Location eastus

    New-AzPolicyAssignment -Name "CertExpirePolicy" -DisplayName "[Preview]: Audit that certificates are not expiring on Windows VMs" -Scope $scope -PolicySetDefinition $CertExpirePolicy -AssignIdentity -Location eastus

```

## <a name="next-steps"></a>Nästa steg

Lär dig hur du [aktiverar ändrings spårning och aviseringar](./enable-tracking-alerting.md) för viktiga filer, tjänster, program och register ändringar.

> [!div class="nextstepaction"]
> [Aktivera spårning och avisering för viktiga ändringar](./enable-tracking-alerting.md)
