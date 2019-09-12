---
title: Princip för gäst konfiguration
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Princip för gäst konfiguration
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: d51cef67c96057b1929ed8cc86396f20338e932b
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/06/2019
ms.locfileid: "70833224"
---
# <a name="guest-configuration-policy"></a>Princip för gäst konfiguration

Med tillägget Azure Policy [gäst konfiguration](/azure/governance/policy/concepts/guest-configuration) kan du granska konfigurations inställningarna på en virtuell dator. Gäst konfigurationen stöds för närvarande endast på virtuella Azure-datorer.

Du hittar listan över principer för gäst konfiguration genom att söka efter kategorin "gäst konfiguration" på sidan Azure Policy Portal. Du kan också hitta listan genom att köra denna cmdlet i ett PowerShell-fönster:

```powershell
Get-AzPolicySetDefinition | where-object {$_.Properties.metadata.category -eq "Guest Configuration"}
```

> [!NOTE]
> Gäst konfigurations funktionerna uppdateras regelbundet för att stödja ytterligare princip uppsättningar. Sök efter nya principer som stöds regelbundet och utvärdera om de är användbara för dina behov.

<!-- TODO: Update these links when available. 

By default, we recommend enabling the following policies:

- [Preview]: Audit to verify password security settings are set correctly inside Linux and Windows machines.
- Audit to verify that certificates are not nearing expiration on Windows VMs.

-->

## <a name="deployment"></a>Distribution

Du kan använda följande exempel PowerShell-skript för att distribuera dessa principer:

- Kontrol lera att inställningarna för lösen ords säkerhet på Windows-och Linux-datorer är korrekt inställda.
- Kontrol lera att certifikaten inte är nära förfallo datum för virtuella Windows-datorer.

 Innan du kör det här skriptet måste du logga in med hjälp av cmdleten [Connect-AzAccount](https://docs.microsoft.com/powershell/module/az.accounts/connect-azaccount?view=azps-2.1.0) . När du kör skriptet måste du ange namnet på den prenumeration som du vill tillämpa principerna på.

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
