# E – Rodné číslo

Píšeš funkce, které ověří a rozeberou české rodné číslo, v souboru `rodne_cislo.py`.
Modul `datetime` zatím nepoužívejte (přijde v lekci Datum a čas), s datem budete pracovat jako se třemi čísly: rok, měsíc, den.

## Jak vypadá rodné číslo

Rodné číslo má tvar `RRMMDD/XXXX`: dvojčíslí roku, měsíc a den narození, lomítko a koncovka. Lomítko je nepovinné, `8503151239` je totéž co `850315/1239`.

| Pravidlo | Příklad |
|---|---|
| Muž má měsíc beze změny. | `850315/1239` → muž, 15. 3. 1985 |
| Žena má měsíc zvýšený o **50**. | `905704/1235` → žena, 4. 7. 1990 (57 − 50 = 7) |
| Od roku 2004 se při nedostatku čísel může měsíc zvýšit ještě o **20** (muži 21–32, ženy 71–82). | `053130/1232` → muž, 30. 11. 2005; `107201/1237` → žena, 1. 2. 2010 |
| Lidé narození **před rokem 1954** mají koncovku jen trojmístnou (9 číslic celkem). | `450808/123` → muž, 8. 8. 1945 |
| Od roku 1954 má rodné číslo 10 číslic a celé číslo musí být **dělitelné 11**. | `8503151239 % 11 == 0` |
| Výjimka: když dává prvních 9 číslic po dělení 11 zbytek 10, je poslední číslice 0. | `850315/1020` je platné |

**Století:** devítimístné rodné číslo je vždy z let 1900–1953. U desetimístného platí: dvojčíslí 54 až 99 je rok 1954–1999, dvojčíslí 00 až 53 je rok 2000–2053.

## Funkce

1. `jeZena(rc: str) -> bool`

   Vrátí `True`, když rodné číslo patří ženě.

2. `pocetDni(rok: int, mesic: int) -> int`

   Vrátí počet dní v měsíci. Únor má v přestupném roce 29 dní, jinak 28.

3. `datumNarozeni(rc: str) -> tuple[int, int, int]`

   Vrátí datum narození jako n-tici `(rok, mesic, den)`, například pro `107201/1237` vrátí `(2010, 2, 1)`.

4. `jePlatneRodneCislo(rc: str) -> bool`

   Vrátí `True`, když je rodné číslo platné:
   - po odstranění lomítka obsahuje jen číslice a má 9 nebo 10 číslic,
   - devítimístné je jen u roku narození před 1954,
   - desetimístné je dělitelné 11 (nebo platí výjimka se zbytkem 10),
   - datum narození existuje: měsíc je 1 až 12 a den 1 až počet dní v měsíci (`850431/1233` je neplatné, duben má 30 dní).

5. `vek(rc: str, rok: int, mesic: int, den: int) -> int`

   Vrátí věk člověka k zadanému datu, například `vek("850315/1239", 2026, 3, 14)` vrátí 40 a `vek("850315/1239", 2026, 3, 15)` vrátí 41.

## Nápovědy k práci s datem

- **Rozložení rodného čísla:** nejdřív odstraňte lomítko `cislo = rc.replace("/", "")`. Části získáte řezy a převedete na čísla:

  ```python
  rok = int(cislo[0:2])     # "85" -> 85
  mesic = int(cislo[2:4])   # "57" -> 57, "05" -> 5
  den = int(cislo[4:6])
  ```

- **Měsíc ženy a +20:** odečítejte postupně, nejdřív 50, pak 20:

  ```python
  if mesic > 50:
      mesic -= 50
  if mesic > 20:
      mesic -= 20
  ```

- **Století:** k dvojčíslí roku přičtěte 1900, nebo 2000 podle délky čísla a tabulky výše.
- **Přestupný rok:** rok dělitelný 4, ale ne roky dělitelné 100, pokud nejsou dělitelné i 400. Rok 2000 je přestupný, rok 1900 ne.

  ```python
  prestupny = rok % 4 == 0 and (rok % 100 != 0 or rok % 400 == 0)
  ```

- **Počet dní v měsíci:** duben, červen, září a listopad mají 30 dní, únor 28 nebo 29, ostatní 31. Stačí podmínka `mesic in (4, 6, 9, 11)`, nebo seznam počtů dní indexovaný `mesic - 1`.
- **Existuje datum?** Využijte vlastní funkce: `datumNarozeni()` dá rok, měsíc a den, `pocetDni()` řekne, kolik dní měsíc má.
- **Porovnání dvou dat:** n-tice se porovnávají prvek po prvku, takže `(mesic, den) < (mesicNarozeni, denNarozeni)` je `True`, když v daném roce narozeniny ještě nebyly:

  ```python
  print((3, 14) < (3, 15))   # True – 14. 3. je před 15. 3.
  print((4, 1) < (3, 15))    # False – duben je až po březnu
  ```

- **Věk:** rozdíl roků, od kterého odečtete 1, pokud narozeniny v daném roce ještě nebyly.
- **Dělitelnost 11:** `int(cislo) % 11 == 0`. Zbytek prvních devíti číslic zjistíte `int(cislo[:9]) % 11`.

## Hlavní program

Zeptá se uživatele na rodné číslo. Je-li neplatné, vypíše `Neplatné rodné číslo`. Jinak vypíše datum narození, pohlaví a věk k dnešnímu datu (dnešní datum zadejte do volání `vek()` ručně).
