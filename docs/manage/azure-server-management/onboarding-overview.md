---
title: Publicera till Azure Server Management Services
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Publicera till Azure Server Management Services
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 330e297b4fb63eaa376e8b6dac0ccf77c2a16ef4
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/16/2019
ms.locfileid: "71028476"
---
# <a name="phase-2-onboarding-azure-server-management-services"></a>Fas 2: Onboarding av Azure Server Management Services

När du är bekant med de [verktyg](./tools-services.md) och den [planering](./prerequisites.md) som ingår i Azures hanterings tjänster är du redo för den andra fasen, som innehåller steg-för-steg-anvisningar för att registrera dessa tjänster för användning med dina Azure-resurser. Börja med att utvärdera den här onboarding-processen innan du inför den i stor miljö.

> [!NOTE]
> De automatiserings metoder som beskrivs i senare avsnitt i den här vägledningen är riktade mot distributioner som inte redan har servrar som distribuerats till molnet. De kräver att du har ägar rollen för en prenumeration för att skapa alla nödvändiga resurser och principer. Om du redan har skapat Log Analytics arbets yta och automatiserings konto resurser, rekommenderar vi att du skickar dessa resurser i lämpliga parametrar när du startar Automation-skripten.

## <a name="onboarding-processes"></a>Onboarding-processer

Det här avsnittet av vägledningen behandlar följande onboarding-processer för både virtuella Azure-datorer och lokala servrar:

- **Aktivera hanterings tjänster på en enskild virtuell dator för utvärdering med hjälp av portalen**. Använd den här processen för att bekanta dig med Azure Server Management-tjänsterna.
- **Konfigurera hanterings tjänster för en prenumeration med hjälp av portalen**. Med den här processen kan du konfigurera Azure-miljön så att alla nya virtuella datorer som är etablerade använder automatiskt hanterings tjänster. Använd den här metoden om du föredrar Azure Portal upplevelsen av skript och kommando rader.
- **Konfigurera hanterings tjänster för en prenumeration med hjälp av Azure Automation**. Den här processen är helt automatiserad. Du behöver bara skapa en prenumeration och skripten konfigurerar miljön att använda hanterings tjänster för nyetablerade virtuella datorer. Använd den här metoden om du är bekant med PowerShell-skript och Azure Resource Manager mallar, eller om du vill lära dig att använda dem.

Procedurerna för var och en av dessa metoder är olika.

> [!NOTE]
> Sekvensen av onboarding-steg när du använder Azure Portal skiljer sig från de automatiserade onboarding-stegen, eftersom portalen erbjuder en enklare onboarding-upplevelse.

Följande diagram visar den rekommenderade distributions modellen för Management Services. 

![Diagram över den rekommenderade distributions modellen](./media/recommended-deployment.png)

> [!NOTE]
> Som du ser i föregående diagram har Log Analytics agenten både en *automatisk registrering* och *valbar* konfiguration för lokala servrar. *Automatisk registrering* innebär att när Log Analytics-agenten installeras på en server och konfigureras för att ansluta till en arbets yta, kommer de lösningar som är aktiverade på den arbets ytan automatiskt att gälla för-servern. *Opt-in* innebär att även om agenten är installerad och ansluten till arbets ytan, kommer lösningen inte att tillämpas om den inte läggs till i serverns omfattnings konfiguration på arbets ytan.

## <a name="next-steps"></a>Nästa steg

Lär dig hur du kan publicera en enskild virtuell dator med hjälp av portalen för att utvärdera onboarding-processen.

> [!div class="nextstepaction"]
> [Publicera en enda virtuell Azure-dator för utvärdering](./onboard-single-vm.md)
