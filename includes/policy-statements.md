<!-- TEMPLATE FILE - DO NOT ADD METADATA -->
<!-- markdownlint-disable MD002 MD041 -->

## <a name="policy-statements"></a>Principrapporter

Följande princip satser fastställer de krav som krävs för att åtgärda de definierade riskerna. Dessa principer definierar de funktionella kraven för styrnings MVP: t. Var och en visas i implementeringen av styrnings MVP.

Cost Management:

- I spårnings syfte måste alla till gångar tilldelas till en program ägare inom en av de viktigaste affärs funktionerna.
- När det uppstår några kostnader kommer ytterligare styrnings krav att upprättas med ekonomi teamet.

Säkerhets bas linje:

- Alla till gångar som distribueras till molnet måste ha en godkänd data klassificering.
- Inga till gångar som identifieras med en skyddad datanivå kan distribueras till molnet, tills tillräckligt med krav på säkerhet och styrning kan godkännas och implementeras.
- Innan minimi kraven på nätverks säkerhet kan val IDE ras och regleras, ses moln miljöer som en demilitariserad zon och bör uppfylla liknande anslutnings krav till andra data Center eller interna nätverk.

Resurs konsekvens:

- Eftersom inga verksamhets kritiska arbets belastningar distribueras i det här skedet finns det inga SLA-, prestanda-eller BCDR-krav som regleras.
- När verksamhets kritiska arbets belastningar distribueras, kommer ytterligare styrnings krav att upprättas med IT-åtgärder.

Identitets bas linje:

- Alla till gångar som distribueras till molnet bör kontrol leras med hjälp av identiteter och roller som godkänts av aktuella styrnings principer.
- Alla grupper i den lokala Active Directory-infrastrukturen med utökade privilegier ska mappas till en godkänd RBAC-roll.

Distributions acceleration:

- Alla till gångar måste grupperas och taggas enligt definierade grupperings-och taggnings strategier.
- Alla till gångar måste använda en godkänd distributions modell.
- När en styrnings grund har upprättats för en moln leverantör måste alla distributions verktyg vara kompatibla med de verktyg som definieras av styrnings teamet.

## <a name="processes"></a>Processer

Ingen budget har allokerats för pågående övervakning och verk ställandet av dessa styrnings principer. På grund av detta har moln styrnings teamet vissa ad hoc-metoder för att övervaka efterlevnaden av princip satser.

- **Kontor** Moln styrnings teamet är att investera tid för att utbilda moln implementerings team på de styrnings guider som har stöd för dessa principer.
- **Distributions granskningar:** Innan du distribuerar en till gång kommer moln styrnings teamet att granska styrnings guiden med moln implementerings teamen.
