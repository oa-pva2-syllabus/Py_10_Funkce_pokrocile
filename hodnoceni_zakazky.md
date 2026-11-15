# A – Hodnocení zakázky

Obchodníci v naší softwarové firmě používají jednoduchý systém, aby odhadli šanci na úspěch potenciální zakázky.
Každé zakázce přidělí 0 až 10 bodů podle těchto kritérií:

| Kritérium | Body |
|---|---|
| **Odvětví:** `"automotive"` | 3 |
| **Odvětví:** `"retail"` | 2 |
| **Odvětví:** jiné | 0 |
| **Obrat** (v milionech eur): méně než 10 | 0 |
| **Obrat:** od 10 do 1 000 včetně | 3 |
| **Obrat:** více než 1 000 | 1 |
| **Země:** `"CZ"` nebo `"SK"` | 2 |
| **Země:** `"DE"` nebo `"FR"` | 1 |
| **Země:** jiná | 0 |
| **Konference:** zákazník se loni účastnil konference firmy | 1 |
| **Newsletter:** zákazník odebírá newsletter firmy | 1 |

Šance na získání zakázky podle bodů:

| Body | Šance |
|---|---|
| 0 až 5 | `"malá"` |
| 6 až 8 | `"střední"` |
| 9 a 10 | `"vysoká"` |

## Úkol

Výpočet rozdělte do tří funkcí v souboru `zakazka.py`. Každá funkce má docstring.

1. `bodyZakazky(odvetvi: str, obrat: float, zeme: str, konference: bool = False, newsletter: bool = False) -> int`

   Vrátí počet bodů zakázky. Poslední dvě kritéria jsou nepovinná s výchozí hodnotou `False`.

2. `sanceZakazky(body: int) -> str`

   Vrátí šanci na získání zakázky podle počtu bodů: `"malá"`, `"střední"` nebo `"vysoká"`.

3. `hodnoceniZakazky(odvetvi: str, obrat: float, zeme: str, konference: bool = False, newsletter: bool = False) -> str`

   Vrátí šanci na získání zakázky. Sama nic nepočítá, jen zavolá obě předchozí funkce.

Pod funkce napište hlavní program, který vyhodnotí několik zakázek a výsledky vypíše. U nepovinných kritérií vyzkoušejte i pojmenované argumenty, například `hodnoceniZakazky("retail", 500, "CZ", newsletter=True)`.
