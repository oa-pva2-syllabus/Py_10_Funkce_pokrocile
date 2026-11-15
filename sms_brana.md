# B – SMS brána

Píšeš jednoduchou aplikaci pro zasílání SMS zpráv. Program v souboru `sms.py` bude mít dvě funkce a hlavní program.

## Funkce

1. `jePlatneCislo(cislo: str) -> bool`

   Vrátí `True`, když je telefonní číslo platné, jinak `False`. Platné číslo je:
   - devět číslic, například `734123456`,
   - nebo předvolba `+420` a za ní devět číslic, například `+420734123456`.

   Číslo může obsahovat mezery, například `+420 734 123 456`. Mezer se zbavíte metodou `replace()`:

   ```python
   telCislo = "+420 734 123 456"
   telCislo = telCislo.replace(" ", "")
   ```

   Pomůcky:
   - Předvolbu na začátku textu ověříte metodou `startswith()`: `cislo.startswith("+420")`. Pozor, podmínka `"+420" in cislo` nestačí, platí i pro `+420` uprostřed čísla.
   - Část textu získáte řezem: `cislo[4:]` je text od pátého znaku dál.
   - Metoda `isdigit()` vrátí `True`, když text obsahuje jen číslice.

2. `cenaZpravy(text: str) -> int`

   Vrátí cenu zprávy v Kč. Uživatel platí 3 Kč za každých **započatých** 180 znaků: zpráva o 1 až 180 znacích stojí 3 Kč, o 181 až 360 znacích 6 Kč. Prázdná zpráva stojí 0 Kč.

## Hlavní program

1. Zeptá se uživatele na telefonní číslo a ověří ho funkcí `jePlatneCislo()`.
2. Pokud číslo není platné, vypíše chybu.
3. Jinak se zeptá na text zprávy a vypíše, kolik bude zpráva stát.
