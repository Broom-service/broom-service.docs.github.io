# Úklidy

Uživatel musí mít roli `Cleaner` nebo `Admin`.

Aplikace 1x za 30 minut stáhne kalendáře rezervací a zkontroluje rezervace proti databázi, pokud nějaká rezervace byla z kalendářů odebrána, tak ji odebere také z databáze, stejně tak v případě přidaných rezervací v kalendáři.

Úklid je vyžadován nejdříve po 10. hodině v den ukončení rezervace (checkout), nejpozději však následující den po ukončení pobytu. (?)

Aplikace bude držet informace o tom, jestli úklid proběhl a kdo jej provedl/měl provést, uživatel vždy bude muset potvrdit, že úklid opravdu provedl.

## Představa

Aplikace bude uživateli zobrazovat rezervace, ve kterých je možné provést úklid, rezervace z minulosti bude zobrazovat v samostatné záložce.
Zobrazované položky: `Datum skončení rezervace`, `Název apartmánu`, `Kdo uklízí`.

Uživatel bude mít u každé rezervace tlačítko, kterým si zvolí, že danou rezervaci uklidí právě on. Pokud má zvolenou rezervaci uklízet jiný uživatel, bude o tom uživatel (který si chce úklid vzít) informován modálním dialogem s možností si úklid převzít. Uživatel bude mít možnost se odebrat ze "svých" úklidů, čímž je uvolní pro ostatní uživatele.

Po uplynutí doby rezervace bude uživateli zpřístupněna možnost označit úklid za dokončený. Tyto úklidy budou zobrazeny nad seznamem dostupných úklidů/rezervací v rámci "probíhajících úklidů", zde se budou zobrazovat pouze úklidy, které má daný uživatel přiřazené.

`Admin` uživatel bude moci ke každé rezervaci přiřadit (i změnit na) jiného `Cleaner` uživatele, také bude moci označit dokončené úklidy.

### Uživatelské rozhraní

Položky rezervací/úklidů budou zobrazeny jednoduše v seznamu, zatím asi nemá smysl vytvářet složitý kalendář, ve kterém by byly rezervace zobrazeny a bylo možno si v rámci kalendáře nastavovat úklidy.

Stav jednotlivých rezervací bude barevně rozlišen, například:

Pro lepší přehlednost se používají 4 barvy + ikony:

- 🟦 **Modrá (Volný úklid)**  
    - Stav: rezervace je volná, nikdo ji nemá.  
    - Akce: tlačítko „Vezmu si úklid“.  
    - Ikona: ➕ (plus) nebo 🖐️.  

- 🟧 **Oranžová (Čeká na mě)**  
    - Stav: úklid mám přiřazený já, ale ještě není hotovo.  
    - Akce: tlačítko „Potvrdit úklid“.  
    - Ikona: ⏳ (přesýpací hodiny).  

- 🟩 **Zelená (Hotovo)**  
    - Stav: úklid byl potvrzen.  
    - Akce: žádná (jen zobrazení).  
    - Ikona: ✅ (fajfka).  

- 🟥 **Červená (Problém / Prošlé)**  
    - Stav: úklid měl být proveden, ale není.  
    - Akce: admin může přiřadit jinému uklízeči nebo označit ručně.  
    - Ikona: ❌ (křížek).  

### Historie úklidů

Uživatel bude mít možnost si zobrazit historii úklidů, které provedl (nebo neprovedl?). Historie bude pouze pro čtení a uživatel uvidí stejné položky, jako v probíhajících rezervacích/úklidech.

`Admin` uživatel si bude moci zobrazit historii pro všechny uživatele najednou (kompletní historie), ale také pouze pro konkrétního uživatele.