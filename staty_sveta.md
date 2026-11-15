# C – Státy světa

V souboru `staty.py` je seznam slovníků `staty` s informacemi o státech světa. O každém státu tam jsou tyto informace:

* název státu (`name`),
* hlavní město (`capital`),
* region (`region`),
* subregion (`subregion`),
* populace (`population`),
* rozloha (`area`),
* Giniho koeficient (`gini`).

Některé státy rozlohu ani Giniho koeficient nemají.

## Funkce

Funkce dostávají seznam států parametrem `staty`. Globální proměnnou `staty` uvnitř funkcí nepoužívejte, funkce pak půjdou použít na jakákoli data.

1. `populaceRegionu(staty: list[dict], region: str) -> int`

   Vrátí součet obyvatel všech států v regionu. Pro region, ve kterém žádný stát neleží, vrátí 0.

2. `statyRegionu(staty: list[dict], region: str) -> list[str]`

   Vrátí seznam názvů států v regionu v pořadí, v jakém jsou v datech.

3. `nejlidnatejsiStat(staty: list[dict], region: str) -> str`

   Vrátí název státu s největší populací v regionu. Když v regionu žádný stát neleží, vrátí prázdný text `""`.

## Hlavní program

Zeptá se uživatele na region a vypíše počet obyvatel regionu a jeho nejlidnatější stát.
Pokud v regionu žádný stát neleží, vypíše `Neznámý region`.

Vyzkoušejte regiony `Asia`, `Europe`, `Africa`, `Oceania`, `Polar` a `Americas`.
