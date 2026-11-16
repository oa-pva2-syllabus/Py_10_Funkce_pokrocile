# D – Košík

Píšeš funkce pro košík e-shopu v souboru `kosik.py`. Košík je seznam názvů zboží, například `["tričko", "mikina", "tričko"]`.
Ceník je slovník název zboží → cena v Kč, v kostře je připravený v proměnné `cenik`.

## Funkce

1. `pridejDoKosiku(zbozi: str, kosik: list[str] | None = None) -> list[str]`

   Přidá zboží do košíku a košík vrátí.

   - Když košík předáme, funkce do něj zboží přidá: `pridejDoKosiku("čepice", ["tričko"])` vrátí `["tričko", "čepice"]`.
   - Když košík nepředáme, funkce začne **pokaždé novým prázdným** košíkem:

   ```python
   print(pridejDoKosiku("tričko"))   # ['tričko']
   print(pridejDoKosiku("mikina"))   # ['mikina'], ne ['tričko', 'mikina']
   ```

   Pozor na past z přednášky: seznam jako výchozí hodnota parametru (`kosik=[]`) se vytvoří jen jednou a sdílí ho všechna volání funkce.

2. `odeberZKosiku(kosik: list[str], zbozi: str) -> bool`

   Odebere z **předaného** košíku první výskyt zboží a vrátí `True`. Když zboží v košíku není, košík nezmění a vrátí `False`.

   ```python
   kosik = ["tričko", "mikina", "tričko"]
   print(odeberZKosiku(kosik, "tričko"))   # True
   print(kosik)                            # ['mikina', 'tričko']
   print(odeberZKosiku(kosik, "čepice"))   # False
   ```

3. `souhrnKosiku(kosik: list[str]) -> dict[str, int]`

   Vrátí slovník s počtem kusů každého zboží: pro `["tričko", "mikina", "tričko"]` vrátí `{"tričko": 2, "mikina": 1}`.

4. `cenaKosiku(kosik: list[str], cenik: dict[str, float]) -> float`

   Vrátí součet cen všech kusů zboží v košíku podle ceníku. Zboží, které v ceníku není, se nezapočítá.

5. `cenaObjednavky(cenaZbozi: float, slevaProcent: float = 0, doprava: float = 99) -> float`

   Vrátí cenu objednávky:

   1. Z ceny zboží odečte slevu v procentech (`slevaProcent = 10` znamená 10 %).
   2. Když je cena po slevě nižší než 1 500 Kč, přičte dopravu. Od 1 500 Kč je doprava zdarma.
   3. Výsledek zaokrouhlí na 2 desetinná místa funkcí `round(cena, 2)`.

   Například `cenaObjednavky(1000)` vrátí 1099, `cenaObjednavky(1600, 10)` vrátí 1539 a `cenaObjednavky(1000, doprava=0)` vrátí 1000.

## Hlavní program

Pod funkcemi sestavte košík, odeberte z něj jedno zboží, vypište souhrn košíku a cenu objednávky.
Slevu a dopravu předejte **pojmenovanými argumenty**, například `cenaObjednavky(cena, slevaProcent=10)`.
