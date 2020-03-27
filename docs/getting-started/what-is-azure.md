---
title: Hur fungerar Azure?
description: Lär dig grunderna om den interna strukturen och driften av Azures moln plattform och molnbaserad virtualisering.
author: alexbuckgit
ms.author: abuck
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: overview
ms.custom: governance
ms.openlocfilehash: 6cc61ff3b6dee171983ceef94c77d3aab715b2c7
ms.sourcegitcommit: ea63be7fa94a75335223bd84d065ad3ea1d54fdb
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/27/2020
ms.locfileid: "80357170"
---
<!-- markdownlint-disable MD026 -->

# <a name="how-does-azure-work"></a>Hur fungerar Azure?

Azure är Microsofts offentliga moln plattform. Azure erbjuder en stor mängd tjänster, inklusive PaaS (Platform as a Service), infrastruktur som en tjänst (IaaS) och hanterade databas tjänster. Men vad är exakt Azure och hur fungerar det?

<!-- markdownlint-disable MD034 -->

> [!VIDEO https://www.microsoft.com/en-us/videoplayer/embed/RE2ixGo]

Azure, precis som andra moln plattformar, förlitar sig på en teknik som kallas _virtualisering_. Den flesta dator maskin vara kan emuleras i program vara, eftersom den flesta dator maskin vara helt enkelt är en uppsättning instruktioner som är permanent eller halv permanent kodade i kisel. Genom att använda ett emuleringsläge som mappar program varu instruktioner till maskin varu instruktioner kan virtualiserad maskin vara köras i program vara som om den var själva själva maskin varan.

Molnet är i stort sett en uppsättning fysiska servrar i ett eller flera data Center som kör virtualiserad maskin vara för kundernas räkning. Hur skapar molnet, startar, stoppar och tar bort miljon tals instanser av virtualiserad maskin vara för miljon tals kunder samtidigt?

För att förstå detta ska vi titta på maskin varans arkitektur i data centret. I varje data Center är en samling servrar som sitter i Server rack. Varje server rack innehåller många Server **blad** samt en nätverks växel som tillhandahåller nätverks anslutning och en PDU-enhet (Power Distribution Unit) som ger kraft. Rack grupperas ibland tillsammans i större enheter som kallas _kluster_.

I varje rack eller kluster är de flesta servrar avsedda att köra dessa virtualiserade maskin varu instanser för användarens räkning. Men vissa av servrarna kör moln hanterings program som kallas infrastruktur styrenhet. _Infrastruktur styrenheten_ är ett distribuerat program med många ansvars områden. Den allokerar tjänster, övervakar serverns hälso tillstånd och de tjänster som körs på den och återställer servrar när de fungerar.

Varje instans av infrastruktur styrenheten är ansluten till en annan uppsättning servrar som kör program vara för moln dirigering, vanligt vis kallat _klient_del. Klient delen är värd för webb tjänster, RESTful-API: er och interna Azure-databaser som används för alla funktioner som molnet utför.

Klient delen är till exempel värd för de tjänster som hanterar kund förfrågningar om att allokera Azure-resurser, till exempel [virtuella datorer](https://docs.microsoft.com/azure/virtual-machines)och tjänster som [Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction). Först verifierar klient delen användaren och verifierar att användaren har behörighet att allokera de begärda resurserna. I så fall kontrollerar klient delen en databas för att hitta ett Server rack med tillräckligt med kapacitet och instruerar sedan infrastruktur hanteraren på racket att allokera resursen.

Azure är alltså en enorm samling av servrar och nätverks maskin vara som kör en komplex uppsättning distribuerade program för att dirigera konfigurationen och driften av den virtualiserade maskin varan och program varan på dessa servrar. Det är den här dirigeringen som gör Azure så kraftfulla&mdash;användare inte längre ansvarig för att underhålla och uppgradera maskin vara eftersom Azure gör allt detta bakom kulisserna.

## <a name="next-steps"></a>Nästa steg

Lär dig mer om moln införande med [Microsoft Cloud implementerings ramverk för Azure](../index.md).

> [!div class="nextstepaction"]
> [Lär dig mer om Microsoft Cloud implementerings ramverk för Azure](../index.md)
