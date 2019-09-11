---
title: Beslutsguide för identitet
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Lär dig om identitet som en central tjänst i Azure-migreringar.
author: rotycenh
ms.author: v-tyhopk
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.custom: governance
ms.openlocfilehash: 2e1ba47201285559be784fafe6b39bdbde0c35ed
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/06/2019
ms.locfileid: "70817085"
---
# <a name="identity-decision-guide"></a>Beslutsguide för identitet

I alla miljöer, såväl lokala som hybridbaserade eller molnexklusiva, behöver IT-avdelningen kontrollera vilka administratörer, användare och grupper som har åtkomst till resurser. Med IAM-tjänster (identitets- och åtkomsthantering) kan du hantera åtkomstkontroll i molnet.

![Identitetsalternativ ordnade från minst till mest komplext, inriktat med direktlänkar nedan](../../_images/discovery-guides/discovery-guide-identity.png)

Hoppa till: [Fastställa krav för identitetsintegrering](#determine-identity-integration-requirements) | [Molnbaslinje](#cloud-baseline) | [Katalogsynkronisering](#directory-synchronization) | [Molnhanterade domäntjänster](#cloud-hosted-domain-services) | [Active Directory Federation Services](#active-directory-federation-services) | [Läs mer](#learn-more)

Det finns flera alternativ för att hantera en identitet i en molnmiljö. Dessa alternativ varierar i både kostnad och komplexitet. En avgörande faktor för strukturering av dina molnbaserade identitetstjänster är den nivå av integrering som krävs med din befintliga lokala identitetsinfrastruktur.

I Azure ger Azure Active Directory (Azure AD) en grundnivå av åtkomstkontroll och identitetshantering för molnresurser. Om organisationens lokala Active Directory-infrastruktur har en komplex skogsstruktur eller anpassade organisationsenheter (OU) kan dina molnbaserade arbetsbelastningar dock kräva katalogsynkronisering med Azure AD för en konsekvent uppsättning identiteter, grupper och roller mellan dina lokala och molnbaserade miljöer. Dessutom kan stöd för program som är beroende av äldre autentiseringsmekanismer kräva distribution av Active Directory Domain Services (AD DS) i molnet.

Molnbaserad identitetshantering är en iterativ process. Du kan börja med en molnbaserad lösning med en liten uppsättning användare och motsvarande roller för en inledande distribution. Allt eftersom migreringen mognar kan du behöva integrera din identitetslösning med hjälp av katalogsynkronisering eller lägga till domäntjänster som en del av dina molndistributioner. Utvärdera din identitetsstrategi på nytt i varje iteration av migreringsprocessen.

## <a name="determine-identity-integration-requirements"></a>Fastställa krav för identitetsintegrering

| Fråga | Molnbaslinje | Katalogsynkronisering | Molnbaserade domäntjänster | Active Directory Federation Services |
|------|------|------|------|------|
| Saknar du för närvarande en lokal katalogtjänst? | Ja | Nej | Nej | Nej |
| Behöver dina arbetsbelastningar använda en gemensam uppsättning användare och grupper mellan den molnbaserade miljön och den lokala miljön? | Nej | Ja | Nej | Nej |
| Är dina arbetsbelastningar beroende av äldre autentiseringsmekanismer såsom Kerberos eller NTLM? | Nej | Nej | Ja | Ja |
| Kräver du enkel inloggning över flera identitetsprovidrar? | Nej | Nej | Nej | Ja |

Som en del i att planera din migrering till Azure behöver du bestämma det bästa sättet att integrerar dina befintliga tjänster för identitetshantering och molnidentitet. Följande är vanliga integreringsscenerier.

### <a name="cloud-baseline"></a>Molnbaslinje

Azure AD är det inbyggda IAM-systemet (identitets- och åtkomsthantering) för att ge användare och grupper åtkomst till hanteringsfunktioner på Azure-plattformen. Om din organisation saknar en betydande lokal identitetslösning, och du planerar att migrera arbetsbelastningar för att vara kompatibel med molnbaserade autentiseringsmekanismer, bör du börja utveckla din identitetsinfrastruktur med hjälp av Azure AD som grund.

**Antaganden gällande molnbaslinje:** Användning av en helt molnbaserad identitetsinfrastruktur förutsätter följande:

- Dina molnbaserade resurser kommer inte att ha beroenden på lokala katalogtjänster eller Active Directory-servrar, eller så kan arbetsbelastningar ändras för att ta bort sådana beroenden.
- De program- eller tjänstarbetsbelastningar som migreras stöder antingen autentiseringsmekanismer som är kompatibla med Azure AD eller kan enkelt modifieras så att de gör det. Azure AD är beroende av Internetkompatibla autentiseringsmekanismer som SAML, OAuth och OpenID Connect. Befintliga arbetsbelastningar som är beroende av äldre autentiseringsmetoder där protokoll såsom Kerberos eller NTLM används kan behöva refaktoriseras före migrering till molnet med hjälp av molnbaslinjemönstret.

> [!TIP]
> Fullständig migrering av dina identitetstjänster till Azure AD eliminerar behovet av att upprätthålla din egen identitetsinfrastruktur, vilket avsevärt förenklar IT-hanteringen.
>
> Azure AD är dock inte en fullständig ersättning för en traditionell lokala Active Directory-infrastruktur. Directory-funktioner såsom äldre autentiseringsmetoder, datorhantering eller grupprinciper är kanske inte tillgängliga utan distribution av ytterligare verktyg eller tjänster till molnet.
>
> För scenarier där du behöver integrera dina lokala identiteter eller domäntjänster med molndistributioner kan du läsa om de mönster för katalogsynkronisering och molnhanterade domäntjänster som beskrivs nedan.

### <a name="directory-synchronization"></a>Katalogsynkronisering

För organisationer med befintlig lokal Active Directory-infrastruktur är katalogsynkronisering ofta den bästa lösningen för att bevara befintlig användar- och åtkomsthantering och samtidigt få de IAM-funktioner som krävs för hantering av molnresurser. Den här processen replikerar kontinuerligt kataloginformation mellan Azure AD och lokala katalogtjänster, vilket möjliggör gemensamma autentiseringsuppgifter för användare och ett konsekvent system för identiteter, roller och behörigheter i hela organisationen.

Obs! Organisationer som har implementerat Office 365 kan redan ha implementerat [katalogsynkronisering](/office365/enterprise/set-up-directory-synchronization) mellan sin lokala Active Directory-infrastruktur och Azure Active Directory.

**Antaganden gällande katalogsynkronisering:** Användning av en lösning för synkroniserad identitet förutsätter följande:

- Du behöver underhålla en gemensam uppsättning användarkonton och grupper i din molnbaserade och din lokala IT-infrastruktur.
- Dina lokala identitetstjänster stöder replikering med Azure AD.

> [!TIP]
> Alla molnbaserade arbetsbelastningar som är beroende av äldre autentiseringsmekanismer som tillhandahålls av lokala Active Directory-servrar och som inte stöds av Azure AD kommer fortfarande att kräva antingen anslutning till lokala domäntjänster eller virtuella servrar i molnmiljön som tillhandahåller dessa tjänster. Användning av lokala identitetstjänster introducerar även beroenden av anslutning mellan molnet och lokala nätverk.

### <a name="cloud-hosted-domain-services"></a>Molnbaserade domäntjänster

Om du har arbetsbelastningar som är beroende av anspråksbaserad autentisering som använder äldre protokoll såsom Kerberos eller NTLM, och sådana arbetsbelastning inte kan refaktoriseras för att acceptera moderna autentiseringsprotokoll som SAML eller OAuth och OpenID Connect, kan du behöva migrera några av dina domäntjänster till molnet som en del av molndistributionen.

Det här mönstret omfattar distribution av virtuella datorer som kör Active Directory till dina molnbaserade virtuella nätverk för att tillhandahålla Active Directory Domain Services (AD DS) till resurser i molnet. Alla befintliga program och tjänster som migreras till ditt molnnätverk bör kunna använda dessa molnhanterade katalogservrar med smärre ändringar.

Det är troligt att dina befintliga kataloger och domäntjänster fortsätter att användas i din lokala miljö. I det här scenariot rekommenderas det att du även använder katalogsynkronisering för att tillhandahålla en gemensam uppsättning användare och roller i både den molnbaserade och den lokala miljön.

**Antaganden gällande molnhanterade domäntjänster:** Genomförande av en katalogmigrering förutsätter följande:

- Dina arbetsbelastningar är beroende av anspråksbaserad autentisering där protokoll som Kerberos eller NTLM används.
- Dina virtuella arbetsbelastningsdatorer måste vara domänkopplade för hantering eller tillämpning av Active Directory-grupprinciper.

> [!TIP]
> En katalogmigrering tillsammans med molnhanterade domäntjänster ger stor flexibilitet vid migrering av befintliga arbetsbelastningar, men värdhantering av virtuella datorer i ditt virtuella molnnätverk för att tillhandahålla dessa tjänster ökar komplexiteten för IT-hanteringsuppgifterna. Allt eftersom din molnmigreringsfunktion mognad bör du undersöka de långsiktiga underhållskraven för hantering av dessa servrar. Överväg huruvida refaktorisering av befintliga arbetsbelastningar för kompatibilitet med molnidentitetsprovidrar såsom Azure Active Directory kan minska behovet av dessa molnhanterade servrar.

### <a name="active-directory-federation-services"></a>Active Directory Federation Services

Identitetsfederation upprättar förtroenderelationer mellan flera identitetshanteringssystem för att möjliggöra gemensamma funktioner för autentisering och auktorisering. Sedan kan du stödja funktioner för enkel inloggning över flera domäner i din organisation eller identitetssystem som hanteras av dina kunder eller affärspartner.

Azure AD stöder federation av lokala Active Directory-domäner med hjälp av [Active Directory Federation Services](/azure/active-directory/hybrid/how-to-connect-fed-whatis) (AD FS). I referensarkitekturen [Utöka AD FS till Azure](https://docs.microsoft.com/azure/architecture/reference-architectures/identity/adfs) beskrivs hur detta kan implementeras i Azure.

## <a name="learn-more"></a>Läs mer

Mer information om identitetstjänster i Azure finns här:

- [Azure AD](https://azure.microsoft.com/services/active-directory). Azure AD tillhandahåller molnbaserade identitetstjänster. Det gör att du kan hantera åtkomst till dina Azure-resurser och kontrollera identitetshantering, enhetsregistrering, användaretablering, åtkomstkontroll för program samt dataskydd.
- [Azure AD Connect](/azure/active-directory/hybrid/whatis-hybrid-identity). Med verktyget Azure AD Connect kan du ansluta Azure AD-instanser till dina befintliga lösningar för identitetshantering så att din befintliga katalog i molnet kan synkroniseras.
- [Rollbaserad åtkomstkontroll](/azure/role-based-access-control/overview) (RBAC). Azure AD tillhandahåller RBAC för att effektivt och säkert hantera åtkomst till resurser i hanteringsplanet. Jobb och ansvarsområden organiseras i roller, och användare tilldelas de rollerna. Med RBAC kan du kontrollera vem som har åtkomst till en resurs samt vilka åtgärder användare kan utföra på den resursen.
- [Azure AD Privileged Identity Management](/azure/active-directory/privileged-identity-management/pim-configure) (PIM). PIM sänker exponeringstiden för behörigheter för resursåtkomst och ökar din insyn i användningen av dem via rapporter och aviseringar. Det begränsar användarna till att få behörigheter ”just-in-time” (JIT) eller genom att tilldela behörigheter under en kortare tidsperiod, varefter behörigheterna automatiskt återkallas.
- [Integrera lokala Active Directory-domäner med Azure Active Directory](https://docs.microsoft.com/azure/architecture/reference-architectures/identity/azure-ad). Denna referensarkitektur innehåller ett exempel på katalogsynkronisering mellan lokala Active Directory-domäner och Azure AD.
- [Utöka Active Directory Domain Services (AD DS) till Azure.](https://docs.microsoft.com/azure/architecture/reference-architectures/identity/adds-extend-domain) Denna referensarkitektur innehåller ett exempel på distribution av AD DS-servrar för att utöka domäntjänster till molnbaserade resurser.
- [Utöka Active Directory Federation Services (AD FS) till Azure](https://docs.microsoft.com/azure/architecture/reference-architectures/identity/adfs). Denna referensarkitektur konfigurerar Active Directory Federation Services (AD FS) till att utföra sammansluten autentisering och auktorisering med din Azure AD-katalog.

## <a name="next-steps"></a>Nästa steg

Identitet är bara en av huvudkomponenterna för infrastruktur som kräver arkitektoniska beslut under en process för att implementera moln. Gå till [översikten över beslutsguider](../index.md) om vill veta mer om alternativa mönster eller modeller som används vid utformningsbeslut för andra typer av infrastrukturer.

> [!div class="nextstepaction"]
> [Beslutsguider för arkitektur](../index.md)
