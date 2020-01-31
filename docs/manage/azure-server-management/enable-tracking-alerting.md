---
title: Aktivera spårning och avisering för viktiga ändringar
description: Aktivera spårning och avisering för viktiga ändringar
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 0cd8776c71eae22fdb7a7894b656a3dc1948e45c
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 01/28/2020
ms.locfileid: "76808115"
---
# <a name="enable-tracking-and-alerting-for-critical-changes"></a>Aktivera spårning och avisering för viktiga ändringar

Azure Ändringsspårning och Inventory tillhandahåller aviseringar om konfigurations status för din hybrid miljö och ändringar i den miljön. Den kan rapportera viktiga fil-, tjänst-, program varu-och register ändringar som kan påverka dina distribuerade servrar.

Som standard övervakar inte Azure Automation inventerings tjänsten filer eller register inställningar. Lösningen innehåller en lista över register nycklar som vi rekommenderar för övervakning. Om du vill se den här listan går du till ditt Automation-konto i Azure Portal och väljer **lager** > **Redigera inställningar**.

![Skärm bild av vyn Azure Automation lager i Azure Portal](./media/change-tracking1.png)

Mer information om varje register nyckel finns i [register nyckel ändrings spårning](https://docs.microsoft.com/azure/automation/automation-change-tracking#registry-key-change-tracking). Välj en nyckel som ska utvärderas och aktivera den sedan. Inställningen tillämpas på alla virtuella datorer som är aktiverade i den aktuella arbets ytan.

Du kan också använda tjänsten för att spåra kritiska fil ändringar. Du kanske till exempel vill spåra C:\Windows\System32\drivers\etc\hosts-filen eftersom operativ systemet använder den för att mappa värdnamn till IP-adresser. Ändringar i den här filen kan orsaka problem med anslutningen eller dirigera om trafik till farliga webbplatser.

Om du vill aktivera fil innehålls spårning för värd filen följer du stegen i [Aktivera spårning av fil innehåll](https://docs.microsoft.com/azure/automation/change-tracking-file-contents#enable-file-content-tracking).

Du kan också lägga till en avisering för ändringar i filer som du håller på att spåra. Anta till exempel att du vill ange en avisering för ändringar i värd filen. Välj **Log Analytics** i kommando fältet eller loggs ökning för den länkade Log Analytics arbets ytan. I Log Analytics använder du följande fråga för att söka efter ändringar i hosts-filen:

```kusto
ConfigurationChange | where FieldsChanged contains "FileContentChecksum" and FileSystemPath contains "hosts"
```

![Skärm bild av Log Analytics Frågeredigeraren i Azure Portal](./media/change-tracking2.png)

Den här frågan söker efter ändringar i innehållet i filer som har en sökväg som innehåller ordet "hosts". Du kan också söka efter en speciell fil genom att ändra parametern Path. (Till exempel `FileSystemPath ==  "c:\\windows\\system32\\drivers\\etc\\hosts"`.)
  
När frågan returnerar resultaten väljer du **ny aviserings regel** för att öppna varnings regel redigeraren. Du kan också komma åt den här redigeraren via Azure Monitor i Azure Portal.

Granska frågan i aviserings regel redigeraren och ändra aviserings logiken om du behöver. I det här fallet vill vi att aviseringen ska höjas om några ändringar upptäcks på någon av datorerna i miljön.

![Skärm bild av Log Analytics varnings regel redigeraren i Azure Portal](./media/change-tracking3.png)

När du har angett villkors logiken kan du tilldela åtgärds grupper för att utföra åtgärder som svar på aviseringen. I det här exemplet skickas e-postmeddelanden och en ITSM-biljett skapas när aviseringen utlöses. Du kan utföra många andra användbara åtgärder, t. ex. utlösa en Azure-funktion, en Azure Automation Runbook, en webhook eller en Logic app.

![Skärm bild av sammanfattningen av exempel varnings regeln i Azure Portal](./media/change-tracking4.png)

När du har ställt in alla parametrar och logik använder du aviseringen i miljön.

## <a name="tracking-and-alerting-examples"></a>Exempel på spårning och aviseringar

I det här avsnittet visas andra vanliga scenarier för spårning och aviseringar som du kanske vill använda.

### <a name="driver-file-changed"></a>Driv rutins filen har ändrats

Använd följande fråga för att identifiera om drivrutinsfiler ändras, läggs till eller tas bort. Det är användbart för att spåra ändringar i viktiga systemfiler.

  ```kusto
  ConfigurationChange | where ConfigChangeType == "Files" and FileSystemPath contains " c:\\windows\\system32\\drivers\\"
  ```

### <a name="specific-service-stopped"></a>Bestämd tjänst stoppad

Använd följande fråga för att spåra ändringar i system kritiska tjänster.

  ```kusto
  ConfigurationChange | where SvcState == "Stopped" and SvcName contains "w3svc"
  ```

### <a name="new-software-installed"></a>Ny program vara installerad

Använd följande fråga för miljöer som behöver låsa program varu konfigurationerna.

  ```kusto
  ConfigurationChange | where ConfigChangeType == "Software" and ChangeCategory == "Added"
  ```

### <a name="specific-software-version-is-or-isnt-installed-on-a-machine"></a>Den aktuella program varu versionen är eller är inte installerad på en dator

Använd följande fråga för att utvärdera säkerheten. Den här frågan refererar `ConfigurationData`som innehåller loggarna för inventering och ger det senast rapporterade konfigurations läget, inte ändringar.

  ```kusto
  ConfigurationData | where SoftwareName contains "Monitoring Agent" and CurrentVersion != "8.0.11081.0"
  ```

### <a name="known-dll-changed-through-the-registry"></a>Känd DLL har ändrats via registret

Använd följande fråga för att identifiera ändringar av välkända register nycklar.

  ```kusto
  ConfigurationChange | where RegistryKey == "HKEY_LOCAL_MACHINE\\System\\CurrentControlSet\\Control\\Session Manager\\KnownDlls"
  ```

## <a name="next-steps"></a>Nästa steg

Lär dig hur du använder Azure Automation för att [skapa uppdaterings scheman](./update-schedules.md) för att hantera uppdateringar av dina servrar.

> [!div class="nextstepaction"]
> [Skapa uppdaterings scheman](./update-schedules.md)
