---
title: Aktivera spårning och avisering för viktiga ändringar
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Aktivera spårning och avisering för viktiga ändringar
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 93449f754e3908e092fa64c55ad62fc604b4ba5b
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/16/2019
ms.locfileid: "71028865"
---
# <a name="enable-tracking-and-alerting-for-critical-changes"></a>Aktivera spårning och avisering för viktiga ändringar

Azure Ändringsspårning och Inventory innehåller aviseringar om konfigurations tillstånd för din hybrid miljö och eventuella ändringar i den miljön. Du kan övervaka viktiga filer, tjänster, program och register ändringar som kan påverka dina distribuerade servrar.

Som standard övervakar inte Azure Automation inventerings tjänsten filer eller register inställningar. Lösningen innehåller en lista över register nycklar som vi rekommenderar för övervakning. Om du vill se den här listan går du till ditt Automation-konto i Azure Portal och väljer **lager** > **redigerings inställningar**:

![Skärm bild av vyn Azure Automation lager i Azure Portal](./media/change-tracking1.png)

Mer information om varje register nyckel finns i [register nyckel ändrings spårning](https://docs.microsoft.com/azure/automation/automation-change-tracking#registry-key-change-tracking). Du kan utvärdera och sedan aktivera varje nyckel genom att markera den. Inställningen tillämpas på alla virtuella datorer som är aktiverade i den aktuella arbets ytan.

Du kan också spåra kritiska fil ändringar. Du kanske till exempel vill spåra C:\Windows\System32\drivers\etc\hosts-filen eftersom operativ systemet använder den för att mappa värdnamn till IP-adresser. Eventuella ändringar i den här filen kan orsaka problem med anslutningen eller dirigera om trafik till farliga webbplatser.

Om du vill aktivera fil innehålls spårning för värd filen följer du stegen i [Aktivera spårning av fil innehåll](https://docs.microsoft.com/azure/automation/change-tracking-file-contents#enable-file-content-tracking).

Du kan också lägga till en avisering för ändringar som har gjorts i filer som du spårar. Anta till exempel att du vill ange en avisering för ändringar som gjorts i värd filen. Börja genom att gå till Log Analytics genom att välja **Log Analytics** i kommando fältet eller genom att öppna loggs ökningen för den länkade Log Analytics-arbetsytan. När du är i Log Analytics kan du söka efter innehålls ändringar i hosts-filen med hjälp av följande fråga:

```kusto
ConfigurationChange | where FieldsChanged contains "FileContentChecksum" and FileSystemPath contains "hosts"
```

![Skärm bild av Log Analytics Frågeredigeraren i Azure Portal](./media/change-tracking2.png)

Den här frågan söker efter ändringar i innehållet i filer som har en sökväg som innehåller ordet "hosts". Du kan också söka efter en speciell fil genom att ändra parametern Path. (Till exempel `FileSystemPath ==  "c:\\windows\\system32\\drivers\\etc\\hosts"`.)
  
När frågan returnerar resultaten väljer du **ny aviserings regel** för att öppna varnings regel redigeraren. Du kan också komma åt den här redigeraren via Azure Monitor i Azure Portal.

Granska frågan i varnings regel redigeraren och ändra aviserings logiken om du behöver. I det här fallet vill vi att aviseringen ska höjas om några ändringar upptäcks på någon av datorerna i miljön.

![Skärm bild av Log Analytics varnings regel redigeraren i Azure Portal](./media/change-tracking3.png)

När du har angett villkors logiken kan du tilldela åtgärds grupper för att utföra åtgärder som svar på aviseringen. I det här exemplet skickas e-postmeddelanden och en ITSM-biljett skapas när aviseringen utlöses. Du kan utföra många andra användbara åtgärder, t. ex. utlösa en Azure-funktion, en Azure Automation Runbook, en webhook eller en Logic app.

![Skärm bild av sammanfattningen av exempel varnings regeln i Azure Portal](./media/change-tracking4.png)

När du har ställt in alla parametrar och logik använder du aviseringen i miljön.

## <a name="more-tracking-and-alerting-examples"></a>Fler uppföljnings-och aviserings exempel

Här följer några andra vanliga scenarier för spårning och aviseringar som du kanske vill tänka på:

### <a name="driver-file-changed"></a>Driv rutins filen har ändrats

Identifiera om drivrutinsfiler ändras, läggs till eller tas bort. Användbart för att spåra ändringar i viktiga systemfiler.

  ```kusto
  ConfigurationChange | where ConfigChangeType == "Files" and FileSystemPath contains " c:\\windows\\system32\\drivers\\"
  ```

### <a name="specific-service-stopped"></a>Bestämd tjänst stoppad

Användbart för att spåra ändringar i system kritiska tjänster.

  ```kusto
  ConfigurationChange | where SvcState == "Stopped" and SvcName contains "w3svc"
  ```

### <a name="new-software-installed"></a>Ny program vara installerad

Användbart för miljöer som behöver låsa program varu konfigurationer.

  ```kusto
  ConfigurationChange | where ConfigChangeType == "Software" and ChangeCategory == "Added"
  ```

### <a name="specific-software-version-is-or-isnt-installed-on-a-machine"></a>Den aktuella program varu versionen är eller är inte installerad på en dator

Användbart för att utvärdera säkerheten. Observera att den här frågan `ConfigurationData`refererar till, som innehåller loggarna för inventering och rapporterar det senaste rapporterade konfigurations läget, inte ändringar.

  ```kusto
  ConfigurationData | where SoftwareName contains "Monitoring Agent" and CurrentVersion != "8.0.11081.0"
  ```

### <a name="known-dll-changed-through-registry"></a>Känd DLL har ändrats via registret

Användbart för att upptäcka ändringar till välkända register nycklar.

  ```kusto
  ConfigurationChange | where RegistryKey == "HKEY_LOCAL_MACHINE\\System\\CurrentControlSet\\Control\\Session Manager\\KnownDlls"
  ```

## <a name="next-steps"></a>Nästa steg

Lär dig hur du hanterar uppdateringar till dina servrar genom att [skapa uppdaterings scheman](./update-schedules.md) med Azure Automation.

> [!div class="nextstepaction"]
> [Skapa uppdaterings scheman](./update-schedules.md)
