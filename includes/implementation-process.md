<!-- TEMPLATE FILE - DO NOT ADD METADATA -->
<!-- markdownlint-disable MD002 MD041 -->

## <a name="dependent-decisions"></a>Beroende beslut

Följande beslut kommer från Team utanför moln styrnings teamet. Implementeringen av var och en av dem kommer från samma team. Moln styrnings teamet ansvarar dock för att implementera en lösning för att kontrol lera att dessa implementeringar tillämpas konsekvent.

### <a name="identity-baseline"></a>Grundläggande identitet

Identitets bas linje är den grundläggande start punkten för all styrning. Innan du försöker tillämpa styrning måste identiteten upprättas. Den fastställda identitets strategin kommer sedan att verkställas av styrnings lösningarna.
I den här styrnings guiden implementerar Identity Management-teamet mönstret för **[katalog synkronisering](../../../../decision-guides/identity/index.md#directory-synchronization)** :

- RBAC tillhandahålls av Azure Active Directory (Azure AD), med hjälp av den katalog-synkronisering eller "samma inloggning" som implementerades under företagets migrering till Office 365. Implementerings vägledning finns i [referens arkitektur för Azure AD-integrering](https://docs.microsoft.com/azure/architecture/reference-architectures/identity/azure-ad).
- Azure AD-klienten kommer också att styra autentisering och åtkomst för till gångar som distribueras till Azure.

I styrnings MVP tvingar styrnings teamet sig att tillämpa den replikerade klient organisationen via verktyg för prenumerations styrning, som diskuteras senare i den här artikeln. I framtida iterationer kan styrnings teamet även använda omfattande verktyg i Azure AD för att utöka den här funktionen.

### <a name="security-baseline-networking"></a>Säkerhets bas linje: Nätverk

Program varu definitions nätverket är en viktig inledande aspekt av säkerhets bas linjen. Om du etablerar styrnings MVP: en beror på tidiga beslut från Security Management-teamet för att definiera hur nätverk kan konfigureras på ett säkert sätt.

På grund av brist på krav, IT-säkerhet spelar den säkra och kräver ett **[Cloud DMZ](../../../../decision-guides/software-defined-network/cloud-dmz.md)** -mönster. Det innebär att styrning av själva Azure-distributionerna är mycket ljus.

- Azure-prenumerationer kan ansluta till ett befintligt Data Center via VPN, men måste följa alla befintliga lokala IT styrnings principer för anslutning av en demilitariserad-zon till skyddade resurser. Implementerings vägledning om VPN-anslutning finns i [referens arkitektur för VPN](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/vpn).
- Beslut om undernät, brand väggar och routning uppskjuts för närvarande till varje program/arbets belastnings lead.
- Ytterligare analys krävs innan data släpps av skyddade data eller verksamhets kritiska arbets belastningar.

I det här mönstret kan moln nätverk bara ansluta till lokala resurser över ett befintligt VPN som är kompatibelt med Azure. Trafik över denna anslutning behandlas som all trafik som kommer från en demilitariserad zon. Ytterligare överväganden kan krävas på den lokala Edge-enheten för att hantera trafik på ett säkert sätt från Azure.

Moln styrnings teamet har proaktivt bjudit in medlemmar i nätverk och IT-säkerhetsteam till regelbundna möten, för att ligga före nätverks krav och risker.

### <a name="security-baseline-encryption"></a>Säkerhets bas linje: Kryptering

Kryptering är ett annat grundläggande beslut inom säkerhets bas linje disciplinen. Eftersom företaget för närvarande inte har lagrat några skyddade data i molnet har säkerhets teamet valt ett mindre aggressivt mönster för kryptering.
I det här skedet föreslås ett **[moln-internt mönster för kryptering](../../../../decision-guides/encryption/index.md#key-management)** , men krävs inte för några utvecklings team.

- Inga styrnings krav har angetts för användningen av kryptering, eftersom den aktuella företags principen inte tillåter verksamhets kritiska eller skyddade data i molnet.
- Ytterligare analys krävs innan du släpper alla skyddade data eller verksamhets kritiska arbets belastningar.

## <a name="policy-enforcement"></a>Principframtvingande

Det första beslutet att fatta om distributions acceleration är mönstret för tvångs åtgärd. I detta beslut beslutade styrnings teamet att implementera det **[automatiserade tvångs](../../../../decision-guides/policy-enforcement/index.md#automated-enforcement)** mönstret.

- Azure Security Center kommer att göras tillgängligt för säkerhets-och identitets teamen för att övervaka säkerhets risker. Båda teamen är också sannolika att använda Security Center för att identifiera nya risker och förbättra företags principen.
- RBAC krävs i alla prenumerationer för att reglera autentiseringen.
- Azure Policy publiceras i varje hanterings grupp och tillämpas på alla prenumerationer. Nivån på de principer som tillämpas är dock mycket begränsad i den här inledande styrnings MVP.
- Även om Azures hanterings grupper används förväntas en relativt enkel hierarki.
- Azure-ritningar används för att distribuera och uppdatera prenumerationer genom att använda RBAC-krav, Resource Manager-mallar och Azure Policy över hanterings grupper.

## <a name="applying-the-dependent-patterns"></a>Använda de beroende mönstren

Följande beslut representerar de mönster som ska tillämpas via policyn för tvingande principer ovan:

**Identitets bas linje.** Azure-ritningar anger RBAC-krav på en prenumerations nivå för att säkerställa att konsekvent identitet konfigureras för alla prenumerationer.

**Säkerhets bas linje: Nätverk.** Gruppen moln styrning har en Resource Manager-mall för att upprätta en VPN-gateway mellan Azure och den lokala VPN-enheten. När ett program team kräver en VPN-anslutning kommer moln styrnings teamet att tillämpa Gateway Resource Manager-mallen via Azure-ritningar.

**Säkerhets bas linje: 3DES.** I det här läget krävs ingen princip tillämpning i det här avsnittet. Detta kommer att besökas igen under senare iterationer.
