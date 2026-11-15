# D – Košík

`pridejDoKosiku(zbozi: str, kosik: list[str] | None = None) -> list[str]`

Funkce v souboru `kosik.py` přidá zboží do košíku a košík vrátí.

- Když košík předáme, funkce do něj zboží přidá: `pridejDoKosiku("čepice", ["tričko"])` vrátí `["tričko", "čepice"]`.
- Když košík nepředáme, funkce začne **pokaždé novým prázdným** košíkem:

```python
print(pridejDoKosiku("tričko"))   # ['tričko']
print(pridejDoKosiku("mikina"))   # ['mikina'], ne ['tričko', 'mikina']
```

Pozor na past z přednášky: seznam jako výchozí hodnota parametru (`kosik=[]`) se vytvoří jen jednou a sdílí ho všechna volání funkce.
