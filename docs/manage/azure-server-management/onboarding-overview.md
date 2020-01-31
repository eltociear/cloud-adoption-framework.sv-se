---
title: Publicera till Azure Server Management Services
description: Publicera till Azure Server Management Services
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 48c0728c39457a2fa060679460a97c0ddca49c45
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 01/28/2020
ms.locfileid: "76808013"
---
# <a name="phase-2-onboarding-azure-server-management-services"></a>Fas 2: onboarding av Azure Server Management Services

När du har lärt dig de [verktyg](./tools-services.md) och den [planering](./prerequisites.md) som ingår i Azures hanterings tjänster är du redo för den andra fasen. Fas 2 innehåller steg-för-steg-anvisningar om hur du registrerar tjänsterna för användning med dina Azure-resurser. Börja med att utvärdera den här onboarding-processen innan du inför den i stor miljö.

> [!NOTE]
> De automatiserings metoder som beskrivs i senare avsnitt i den här vägledningen är avsedda för distributioner som inte redan har servrar som har distribuerats till molnet. De kräver att du har ägar rollen för en prenumeration för att skapa alla nödvändiga resurser och principer. Om du redan har skapat Log Analytics arbets ytor och Automation-konton rekommenderar vi att du skickar dessa resurser i lämpliga parametrar när du startar Automation-skripten.

## <a name="onboarding-processes"></a>Onboarding-processer

Det här avsnittet av vägledningen behandlar följande onboarding-processer för både virtuella Azure-datorer och lokala servrar:

- **Aktivera hanterings tjänster på en enskild virtuell dator för utvärdering med hjälp av portalen**. Använd den här processen för att bekanta dig med Azure Server Management-tjänsterna.
- **Konfigurera hanterings tjänster för en prenumeration med hjälp av portalen**. Med den här processen kan du konfigurera Azure-miljön så att alla nya virtuella datorer som är etablerade använder automatiskt hanterings tjänster. Använd den här metoden om du föredrar Azure Portal upplevelsen av skript och kommando rader.
- **Konfigurera hanterings tjänster för en prenumeration med hjälp av Azure Automation**. Den här processen är helt automatiserad. Du behöver bara skapa en prenumeration och skripten konfigurerar miljön för att använda hanterings tjänster för nyetablerade virtuella datorer. Använd den här metoden om du är bekant med PowerShell-skript och Azure Resource Manager mallar, eller om du vill lära dig att använda dem.

Procedurerna för var och en av dessa metoder är olika.

> [!NOTE]
> När du använder Azure Portal skiljer sig sekvensen för onboarding-stegen från de automatiserade onboarding-stegen. Portalen erbjuder en enklare onboarding-upplevelse.

Följande diagram visar den rekommenderade distributions modellen för hanterings tjänster:

![Diagram över den rekommenderade distributions modellen](./media/recommended-deployment.png)

Som du ser i föregående diagram har Log Analytics agenten både en *automatisk registrering* och *valbar* konfiguration för lokala servrar:

- **Automatisk registrering:** När Log Analytics Agent installeras på en server och konfigureras för att ansluta till en arbets yta, tillämpas de lösningar som är aktiverade på den arbets ytan automatiskt på servern.
- **Anmäl dig till:** Även om agenten är installerad och ansluten till arbets ytan, tillämpas inte lösningen om den inte läggs till i serverns omfattnings konfiguration i arbets ytan.

## <a name="next-steps"></a>Nästa steg

Lär dig hur du kan publicera en enskild virtuell dator med hjälp av portalen för att utvärdera onboarding-processen.

> [!div class="nextstepaction"]
> [Publicera en enda virtuell Azure-dator för utvärdering](./onboard-single-vm.md)
