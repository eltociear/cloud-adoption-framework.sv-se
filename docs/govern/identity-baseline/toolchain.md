---
title: Identitets bas verktyg i Azure
description: Identitets bas verktyg i Azure
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: d145d08aa4cf2b386c3ee1f0df403f684b27c2a2
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 01/28/2020
ms.locfileid: "76806075"
---
# <a name="identity-baseline-tools-in-azure"></a>Identitets bas verktyg i Azure

[Identitets bas linjen](./index.md) är en av de [fem disciplinerna i moln styrning](../governance-disciplines.md). Den här disciplinen fokuserar på sätt att etablera principer som garanterar konsekvens och kontinuitet i användar identiteter oavsett vilken moln leverantör som är värd för programmet eller arbets belastningen.

Följande verktyg ingår i identifierings guiden för Hybrid identitet.

**Active Directory (lokalt):** Active Directory är identitets leverantören som oftast används i företaget för att lagra och verifiera användarautentiseringsuppgifter.

**Azure Active Directory:** En SaaS (Software as a Service) som motsvarar Active Directory som kan federera med en lokal Active Directory.

**Active Directory (IaaS):** En instans av det Active Directory program som körs på en virtuell dator i Azure.

Identitet är kontroll planet för IT-säkerhet. Därför är autentiseringen en organisations åtkomst skydd till molnet. Organisationer behöver ett identitets kontroll plan som förstärker säkerheten och skyddar sina molnappar mot inkräktare.

## <a name="cloud-authentication"></a>Molnbaserad autentisering

Att välja rätt autentiseringsmetod är det första sättet för organisationer som vill flytta sina appar till molnet.

När du väljer den här metoden hanterar Azure AD användarnas inloggnings processer. Tillsammans med sömlös enkel inloggning (SSO) kan användarna logga in till molnappar utan att behöva ange sina autentiseringsuppgifter på annat sätt. Med molnbaserad autentisering kan du välja mellan två alternativ:

**Synkronisering av lösen ord för Azure AD-hash:** Det enklaste sättet att aktivera autentisering för lokala katalog objekt i Azure AD. Den här metoden kan också användas med valfri metod som autentiseringsmetod för redundans i händelse av att den lokala servern slutar fungera.

**Autentisering med Azure AD genom strömning:** Ger en beständig lösen ords verifiering för Azure AD-autentisering med hjälp av en program varu agent som körs på en eller flera lokala servrar.

> [!NOTE]
> Företag som har ett säkerhets krav för att omedelbart framtvinga lokala användar konto tillstånd, lösen ords principer och inloggnings timmar bör vara medveten om genom strömnings metoden.

**Federerad autentisering:**

När du väljer den här metoden skickar Azure AD autentiseringsprocessen till ett separat betrott autentiserings system, till exempel lokala Active Directory Federation Services (AD FS) (AD FS) eller en betrodd tredjeparts Federations leverantör för att verifiera användarens lösen ord.

Artikeln att [välja rätt autentiseringsmetod för Azure Active Directory](https://docs.microsoft.com/azure/security/azure-ad-choose-authn) innehåller ett besluts träd som hjälper dig att välja den bästa lösningen för din organisation.

I följande tabell visas de inbyggda verktyg som kan hjälpa mogna de principer och processer som har stöd för den här styrnings disciplinen.

<!-- markdownlint-disable MD033 -->

|Beaktas|Password-hash-synkronisering + sömlös SSO|Direktautentisering + sömlös SSO|Federation med AD FS|
|:-----|:-----|:-----|:-----|
|Var sker autentiseringen?|I molnet|I molnet efter ett säkert utbyte av lösen ords verifiering med den lokala Autentiseringstjänsten|Lokalt|
|Vilka är de lokala server kraven utöver etablerings systemet: Azure AD Connect?|Inget|En server för varje ytterligare Authentication agent|Två eller flera AD FS-servrar<br><br>Två eller flera WAP-servrar i perimeternätverket/DMZ-nätverket|
|Vilka är kraven för lokal Internet och nätverk utöver etablerings systemet?|Inget|[Utgående Internet åtkomst](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-pta-quick-start) från servrar som kör autentiseringsprinciper|[Inkommande Internet åtkomst](https://docs.microsoft.com/windows-server/identity/ad-fs/overview/ad-fs-requirements) till WAP-servrar i perimeternätverket<br><br>Inkommande nätverks åtkomst till AD FS servrar från WAP-servrar i perimeternätverket<br><br>Utjämning av nätverksbelastning|
|Finns det ett krav för SSL-certifikat?|Inga|Inga|Ja|
|Finns det en lösning för hälso övervakning?|Krävs inte|Agent status som tillhandahålls av [Azure Active Directory administrations Center](https://docs.microsoft.com/azure/active-directory/hybrid/tshoot-connect-pass-through-authentication)|[Azure AD Connect Health](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-health-adfs)|
|Får användarna enkel inloggning till moln resurser från domänanslutna enheter i företags nätverket?|Ja med [sömlös SSO](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-sso)|Ja med [sömlös SSO](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-sso)|Ja|
|Vilka inloggnings typer stöds?|UserPrincipalName + lösen ord<br><br>Windows-integrerad autentisering med [sömlös SSO](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-sso)<br><br>[Alternativt inloggnings-ID](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-install-custom)|UserPrincipalName + lösen ord<br><br>Windows-integrerad autentisering med [sömlös SSO](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-sso)<br><br>[Alternativt inloggnings-ID](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-pta-faq)|UserPrincipalName + lösen ord<br><br>sAMAccountName + lösen ord<br><br>Windows-integrerad autentisering<br><br>[Autentisering med certifikat och smartkort](https://docs.microsoft.com/windows-server/identity/ad-fs/operations/configure-user-certificate-authentication)<br><br>[Alternativt inloggnings-ID](https://docs.microsoft.com/windows-server/identity/ad-fs/operations/configuring-alternate-login-id)|
|Stöds Windows Hello för företag?|[Nyckel förtroende modell](https://docs.microsoft.com/windows/security/identity-protection/hello-for-business/hello-identity-verification)<br><br>[Certifikat förtroende modell med Intune](https://microscott.azurewebsites.net/2017/12/16/setting-up-windows-hello-for-business-with-intune)|[Nyckel förtroende modell](https://docs.microsoft.com/windows/security/identity-protection/hello-for-business/hello-identity-verification)<br><br>[Certifikat förtroende modell med Intune](https://microscott.azurewebsites.net/2017/12/16/setting-up-windows-hello-for-business-with-intune)|[Nyckel förtroende modell](https://docs.microsoft.com/windows/security/identity-protection/hello-for-business/hello-identity-verification)<br><br>[Certifikat förtroende modell](https://docs.microsoft.com/windows/security/identity-protection/hello-for-business/hello-key-trust-adfs)|
|Vad är Multi-Factor Authentication-alternativen?|[Azure Multi-Factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication)<br><br>[Anpassade kontroller med villkorlig åtkomst *](https://docs.microsoft.com/azure/active-directory/conditional-access/controls#custom-controls-preview)|[Azure Multi-Factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication)<br><br>[Anpassade kontroller med villkorlig åtkomst *](https://docs.microsoft.com/azure/active-directory/conditional-access/controls#custom-controls-preview)|[Azure Multi-Factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication)<br><br>[Azure Multi-Factor Authentication Server](https://docs.microsoft.com/azure/active-directory/authentication/howto-mfaserver-deploy)<br><br>[Multi-Factor Authentication från tredje part](https://docs.microsoft.com/windows-server/identity/ad-fs/operations/configure-additional-authentication-methods-for-ad-fs)<br><br>[Anpassade kontroller med villkorlig åtkomst *](https://docs.microsoft.com/azure/active-directory/conditional-access/controls#custom-controls-preview)|
|Vilka användar konto tillstånd stöds?|Inaktiverade konton<br>(upp till 30 minuters fördröjning)|Inaktiverade konton<br><br>Kontot är utelåst<br><br>Kontot har gått ut<br><br>Lösen ordet upphörde<br><br>Inloggnings tider|Inaktiverade konton<br><br>Kontot är utelåst<br><br>Kontot har gått ut<br><br>Lösen ordet upphörde<br><br>Inloggnings tider|
|Vilka är alternativen för villkorlig åtkomst?|[Villkorlig åtkomst för Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)|[Villkorlig åtkomst för Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)|[Villkorlig åtkomst för Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)<br><br>[AD FS anspråks regler](https://adfshelp.microsoft.com/AadTrustClaims/ClaimsGenerator)|
|Finns det stöd för äldre protokoll?|[Ja](https://docs.microsoft.com/azure/active-directory/conditional-access/howto-baseline-protect-legacy-auth)|[Ja](https://docs.microsoft.com/azure/active-directory/conditional-access/howto-baseline-protect-legacy-auth)|[Ja](https://docs.microsoft.com/windows-server/identity/ad-fs/operations/access-control-policies-w2k12)|
|Kan du anpassa logo typen, avbildningen och beskrivningen på inloggnings sidorna?|[Ja, med Azure AD Premium](https://docs.microsoft.com/azure/active-directory/customize-branding)|[Ja, med Azure AD Premium](https://docs.microsoft.com/azure/active-directory/customize-branding)|[Ja](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-federation-management#customlogo)|
|Vilka avancerade scenarier stöds?|[Smart lösen ords utelåsning](https://docs.microsoft.com/azure/active-directory/active-directory-secure-passwords)<br><br>[Läckta autentiseringsuppgifter-rapporter](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-risk-events)|[Smart lösen ords utelåsning](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-pass-through-authentication-smart-lockout)|Autentiserings system med låg latens för Multisite<br><br>[AD FS extra näts utelåsning](https://docs.microsoft.com/windows-server/identity/ad-fs/operations/configure-ad-fs-extranet-soft-lockout-protection)<br><br>[Integrering med identitets system från tredje part](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-federation-compatibility)|

<!-- markdownlint-enable MD033 -->

> [!NOTE]
> Anpassade kontroller i villkorlig åtkomst för Azure AD stöder inte enhets registrering.

## <a name="next-steps"></a>Nästa steg

I [fakta bladet med hybrid Identity digital transformation Framework](https://resources.office.com/ww-landing-M365E-EMS-IDAM-Hybrid-Identity-WhitePaper.html) beskrivs kombinationer och lösningar för att välja och integrera dessa komponenter.

Med [verktyget Azure AD Connect](https://aka.ms/aadconnectwiz) kan du integrera dina lokala kataloger med Azure AD.
