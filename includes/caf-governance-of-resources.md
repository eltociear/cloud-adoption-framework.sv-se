<!-- TEMPLATE FILE - DO NOT ADD METADATA -->
<!-- markdownlint-disable MD002 MD041 -->
> [!NOTE]
>I händelse av större ändringar i dina affärskrav gör Azure-hanteringsgrupper att du enkelt kan omorganisera hanteringshierarkin och tilldelningarna av prenumerationsgrupper. Kom dock ihåg att princip- och rolltilldelningar som tillämpas på en hanteringsgrupp ärvs av alla prenumerationer under den gruppen i hierarkin. Om du planerar att omtilldela prenumerationer mellan hanteringsgrupper bör du vara medveten om ändringar av princip- och rolltilldelning som kan uppstå. Mer information finns i [dokumentationen om Azure-hanteringsgrupper](https://docs.microsoft.com/azure/governance/management-groups).

### <a name="governance-of-resources"></a>Styrning av resurser

En uppsättning med globala principer och RBAC-roller ger en baslinjenivå av styrningsframtvingande. Om du ska uppfylla molnimplementeringsgruppens principkrav så kräver implementeringen av styrnings-MVP att följande uppgifter slutförs:

1. Identifiera de Azure Policy-definitioner som behövs för att genomdriva affärskrav. Detta kan inkludera användning av inbyggda definitioner och skapandet av nya anpassade definitioner.
2. Skapa en skissdefinition med hjälp av dessa inbyggda och anpassade principer och rolltilldelningar enligt kraven för styrnings-MVP.
3. Tillämpa principer och konfiguration globalt genom att tilldela skissdefinitionen till alla prenumerationer.

#### <a name="identify-policy-definitions"></a>Identifiera principdefinitioner

Azure innehåller flera inbyggda principer och rolldefinitioner som du kan tilldela till valfri hanteringsgrupp, prenumeration eller resursgrupp. Många vanliga styrningskrav kan hanteras med hjälp av inbyggda definitioner. Det är dock troligt att du även måste skapa anpassade principdefinitioner så att du kan hantera dina specifika krav.

Anpassade principdefinitioner sparas till antingen en hanteringsgrupp eller en prenumeration och ärvs via hanteringsgruppshierarkin. Om sparplatsen för en principdefinition är en hanteringsgrupp så är den principdefinitionen tillgängliga att tilldelas till vilka som helst av den gruppens underordnade hanteringsgrupper eller prenumerationer.

Eftersom de principer som krävs för att stödja styrnings-MVP är avsedda att gälla för alla aktuella prenumerationer implementeras följande affärskrav med hjälp av en kombination av inbyggda definitioner och anpassade definitioner som skapats i rothanteringsgruppen:

1. Begränsa listan över tillgängliga rolltilldelningar till en uppsättning inbyggda Azure-roller som auktoriserats av ditt team för molnstyrning. Detta kräver en [anpassad principdefinition](https://github.com/Azure/azure-policy/tree/master/samples/Authorization/allowed-role-definitions).
2. Kräv användning av följande taggar på alla resurser: *Avdelning/faktureringsenhet*, *Geografi*, *Dataklassificering*, *Allvarlighetsgrad*, *SLA*, *Miljö*, *Programarketyp*, *Program* och *Programägare*. Detta kan hanteras med hjälp av den inbyggda definitionen ”Kräv angiven tagg”.
3. Kräv att taggen *Program* för resurser ska matcha namnet på relevant resursgrupp. Detta kan hanteras med hjälp av den inbyggda definitionen ”Kräv tagg och dess värde”.

Information om hur du definierar anpassade principer finns i [dokumentationen om Azure Policy](https://docs.microsoft.com/azure/governance/policy/tutorials/create-custom-policy-definition). Vägledning och exempel på anpassade principer finns på [webbplatsen med Azure Policy-exempel](https://docs.microsoft.com/azure/governance/policy/samples) och den associerade [GitHub-lagringsplatsen](https://github.com/Azure/azure-policy).

#### <a name="assign-azure-policy-and-rbac-roles-using-azure-blueprints"></a>Tilldela Azure Policy- och RBAC-roller med hjälp av Azure Blueprints

Azure-principer kan tilldelas på resursgrupps-, prenumerations- och hanteringsgruppsnivå och kan tas med i [Azure Blueprints](https://docs.microsoft.com/azure/governance/blueprints/overview)-definitioner. Även om de principkrav som definieras i denna styrnings-MVP gäller för alla aktuella prenumerationer är det mycket troligt att framtida distributioner kommer att kräva undantag eller alternativa principer. Därför är det inte säkert att tilldelning av principer med hjälp av hanteringsgrupper, där alla underordnade prenumerationer ärver dessa tilldelningar, är flexibelt nog att stödja dessa scenarier.

Azure Blueprints möjliggör konsekvent tilldelning av principer och roller, tillämpning av Resource Manager-mallar och distribution av resursgrupper över flera prenumerationer. Som med principdefinitioner sparas skissdefinitioner till hanteringsgrupper eller prenumerationer och är tillgängliga via arv till alla underordnade objekt i hanteringsgruppshierarkin.

Teamet för molnstyrning har beslutat att framtvingande av den Azure Policy och de RBAC-tilldelningar som krävs mellan prenumerationer kommer att implementeras via Azure Blueprints och associerade artefakter:

1. I rothanteringsgruppen skapar du en skissdefinition som heter `governance-baseline`.
2. Lägg till följande skissartefakter i skissdefinitionen:
    1. Principtilldelningar för de anpassade Azure Policy-definitioner som definierats i roten för hanteringsgrupp.
    2. Resursgruppsdefinitioner för alla grupper som krävs i prenumerationer som skapats eller styrs av styrnings-MVP.
    3. Standardmässiga rolltilldelningar som krävs i prenumerationer som skapats eller styrs av styrnings-MVP.
3. Publicera skissdefinitionen.
4. Tilldela skissdefinitionen `governance-baseline` till alla prenumerationer.

Mer information om hur du skapar och använder skissdefinitioner finns i [dokumentationen om Azure Blueprints](https://docs.microsoft.com/azure/governance/blueprints/overview).

### <a name="secure-hybrid-vnet"></a>Säkert virtuellt hybridnätverk

Specifika prenumerationer kräver ofta en viss åtkomstnivå till lokala resurser. Detta är vanligt i migrerings- eller utvecklingsscenarier där beroende resurser finns i det lokala datacentret.

Innan förtroendet till molnmiljön är helt fastställd är det viktigt att noggrant kontrollera och övervaka all tillåten kommunikation mellan den lokala miljön och molnarbetsbelastningar samt att skydda det lokala nätverket mot potentiell obehörig åtkomst från molnbaserade resurser. För att stödja dessa scenarier lägger styrnings-MVP till följande bästa praxis:

1. Upprätta ett molnsäkert virtuellt hybridnätverk.
    1. [VPN-referensarkitekturen](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/vpn) upprättar ett mönster och en distributionsmodell för skapande av en VPN-gateway i Azure.
    2. Verifiera att de lokala mekanismerna för säkerhet och trafikhantering behandlar anslutna molnnätverk som ej betrodda. Resurser och tjänster som hanteras i molnet ska endast ha åtkomst till auktoriserade lokala tjänster.
    3. Validera att den lokala gränsenheten i det lokala datacentret är kompatibel med [kraven för Azure VPN Gateway](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpn-devices) och har konfigurerats för att få åtkomst till det offentliga Internet.
    4. Observera att VPN-tunnlar endast bör betraktas som produktionsklara kretsar för de allra enklaste arbetsbelastningarna. Azure-ExpressRoute bör användas för allt annat än ett fåtal arbetsbelastningar som kräver lokal anslutning.
1. I rothanteringsgruppen skapar du en andra skissdefinition som heter `secure-hybrid-vnet`.
    1. Lägg till Resource Manager-mallen för VPN-gatewayen som en artefakt till skissdefinitionen.
    2. Lägg till Resource Manager-mallen för det virtuella nätverket som en artefakt till skissdefinitionen.
    3. Publicera skissdefinitionen.
1. Tilldela skissdefinitionen `secure-hybrid-vnet` till alla prenumerationer som kräver lokal anslutning. Den här definitionen bör tilldelas utöver skissdefinitionen `governance-baseline`.

En av de största frågorna som IT-säkerhet och traditionella styrningsteam tar upp handlar om risken för att molnimplementeringen i det tidiga skedet komprometterar befintliga tillgångar. Med ovanstående tillvägagångssätt kan teamen för molnimplementering skapa och migrera hybridlösningar med reducerad risk för lokala tillgångar. När förtroendet för molnmiljön ökar kan den här tillfälliga lösningen tas bort i senare utvecklingar.

> [!NOTE]
> Ovanstående är en startpunkt för att snabbt skapa en baslinjestyrnings-MVP. Det här är bara början på styrningsresan. Ytterligare utveckling kommer att behövas allt eftersom företaget fortsätter att implementera molnet och antar större risker inom följande områden:
>
> - Verksamhetskritiska arbetsbelastningar
> - Skyddade data
> - Kostnadshantering
> - Scenarier med flera moln
>
> Dessutom baseras den specifika informationen för denna MVP på exempelresan för ett fiktivt företag, som beskrivs i följande artiklar. Vi rekommenderar starkt att du bekantar dig med de andra artiklarna i den här serien innan du implementerar denna bästa praxis.
