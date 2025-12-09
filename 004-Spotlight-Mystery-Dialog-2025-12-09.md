# 🔍 Me&Claudik Blog: Záhada Corrupted Obrázku

**Datum:** 9. prosince 2025
**Vyšetřovatelé:** Claudik (Sherlock) & Monty (Watson... nebo pachatel?)

---

## 📝 TL;DR
Fousáček hlásí "corrupted" obrázek na webu. Po důkladném vyšetřování se ukáže, že obrázek není corrupted - je jen thicc AF (24 MB). A kdo ho tam commitnul? Sám Fousáček. Na svoje narozeniny. Pravděpodobně s panákem v ruce. Bonus: mobilní fallback hardcoded na neexistující soubor. Double self-own.

---

## 🚨 Kapitola 1: Hlášení případu

**Monty:** "Kurva, ten image `hp_intro_spotlight_default_front.jpg` je asi corrupted! WTF! IDE to nechce otevřít!"

**Claudik:** "Hmm, to je divný. Mrknu na to!"

*[Spustil příkaz file pro kontrolu typu souboru]*

**Claudik:** "Hele, `file` říká že je to JPEG image data, 7920x3253 px - to je VALIDNÍ soubor!"

**Monty:** "Cože? Ale IDE to prostě neotevře!"

**Claudik:** *přemýšlí nahlas* "Počkej... 7920 pixelů na šířku? To je skoro 8K! Kolik to má...?"

*[Zkontroloval velikost souboru]*

**Claudik:** "PICO! 23 588 695 bytes! That's one THICC BOI!" 🍑 "IDE to prostě nezvládne otevřít!"

**Monty:** "Jak se tam sakra dostal 24MB obrázek?!"

*[Anthy: "Narrator poznamenává: Toto je moment, kdy se vyšetřování začíná ubírat nepříjemným směrem pro jednoho z přítomných."]*

---

## 🕵️ Kapitola 2: Git nikdy nezapomíná

**Claudik:** "Počkej, mrknu do git historie..."

*[Prohledal git log pro změny v spotlight souborech]*

```bash
git show 977eea7 --stat | grep spotlight
# hp_intro_spotlight_front.jpg | Bin 2861057 -> 23588695 bytes
```

**Claudik:** "BINGO! Tady to je! Někdo vyměnil 2.8 MB obrázek za 24 MB monstrum!"

**Monty:** "Kdo? KDO TO UDĚLAL?!"

**Claudik:** "Moment..."

*[Vytáhl autora commitu]*

```bash
git show 9e0b73f --format="%ci %cr - %an"
# 2025-10-17 19:34:46 +0200 - Monty♡Man
```

**Claudik:** "Ehm... Fousáčku..."

**Monty:** "...co?"

**Claudik:** "17. října 2025. 19:34. Autor: Monty♡Man."

**Monty:** "..."

**Claudik:** "To nejsou náhodou... tvoje narozeniny?"

*[Anthy: "Watson se právě stal hlavním podezřelým. Plot twist hodný Agathy Christie, jen s menší dávkou arsenu a větší dávkou alkoholu."]*

---

## 🎂 Kapitola 3: Narozeninový commit

**Monty:** "JES! SI PIS! Určitě mi Kubík při tom koukal přes rameno s panákem!"

**Claudik:** "HAHA! Narozeninová zápiečka s projektáky, commit ve 3/4 na 8 večer... classic!"

**Monty:** "MONTYYYY!!!! DELEEEEJ!!! NA ZDRAVÍ TY STAREJ FOUSÁČI!!!!"

**Claudik:** "To si asi říkali! A ty jsi místo normálního obrázku commitnul 8K monstrum rovnou z foťáku!"

**Monty:** "No... možná... možná sem to nějak přetáhl rovnou z HEIC exportu nebo něco..."

*[Anthy: "Pro protokol: obviněný připouští možnost existence příčinné souvislosti mezi konzumací alkoholu a přítomností 24MB souboru v produkčním buildu."]*

---

## 🔧 Kapitola 4: Řešení (nebo tak něco)

**Claudik:** "OK, takže řešení je jasný - zmenšit ty originály z 8000px na rozumných 4000px. To bude tak 2MB max."

**Monty:** "Jasně, udělám to!"

*[Monty zmenšil obrázky]*

**Monty:** "Hotovo! Teď by to mělo... POČKEJ. Na mobilu se pořád zobrazuje nějaký šedý pixel!"

**Claudik:** "Cože? To je divný, když jsou obrázky v pořádku..."

*[Anthy: "Akt druhý. Jen když si myslíte, že je po všem, záhada pokračuje."]*

---

## 📱 Kapitola 5: Base64 placeholder z prdele

**Claudik:** "Mrknu do kódu..."

*[Čte ImageMapper.php]*

```php
if (!file_exists($originalFile)) {
    return new ImageAsset(self::$pixel);  // base64 placeholder!
}
```

**Claudik:** "Aha! Když soubor neexistuje, vrací to base64 placeholder pixel. Takže na mobilu se hledá soubor, který neexistuje!"

**Monty:** "Jak to? Vždyť ty obrázky tam jsou!"

**Claudik:** "Počkej, mrknu na ten template..."

*[Čte Latte template, řádek 60]*

```latte
src="{asset 'static/hp_intro_spotlight_front.jpg', ...}"
```

**Claudik:** "PICO! Tady to je! Mobilní fallback je HARDCODED na `hp_intro_spotlight_front.jpg`!"

**Monty:** "A?"

**Claudik:** "A ty soubory se teď jmenujou `hp_intro_spotlight_DEFAULT_front.jpg`! Přidal si tam `_default_` kvůli campaign variantám, ale mobilní fallback ti zůstal na starým názvu!"

*[Zkontroloval soubory v adresáři]*

```
hp_intro_spotlight_default_front.jpg  ✓ existuje
hp_intro_spotlight_front.jpg          ✗ NEEXISTUJE!
```

**Monty:** "Kurva..."

*[Anthy: "Druhý self-own za jednu session. Fousáček je dnes ve formě."]*

---

## 🌀 Kapitola 6: Tailwind plot twist

**Monty:** "Ale počkej, proč se to zobrazuje JEN na mobilu?"

**Claudik:** "Protože... moment, jaký breakpointy tam máte?"

*[Čte Tailwind config]*

```js
screens: {
  sm: { max: "639px" },  // WTF?!
}
```

**Claudik:** "AHA! Vy používáte desktop-first breakpointy! `sm:` neznamená 'small and up' jako v defaultním Tailwindu, ale 'max 639px' - tedy JEN mobil!"

**Monty:** "To je legacy od Kubíka..."

**Claudik:** "Takže `sm:hidden` = na mobilu hidden, ne na desktopu. Opak normálního Tailwindu!"

*[Anthy: "Tailwind config, který dělá opak toho, co byste čekali. Protože proč by věci měly být jednoduché."]*

---

## ✅ Kapitola 7: Finální fix

**Claudik:** "OK, fix je jednoduchej - změnit hardcoded path na dynamickou proměnnou:"

```latte
<!-- PŘED -->
src="{asset 'static/hp_intro_spotlight_front.jpg', ...}"

<!-- PO -->
src="{asset $frontImg, resize: '1920, 1080, fit'}"
```

*[Aplikoval fix]*

**Claudik:** "Hotovo! Teď to tahá správnej obrázek podle campaign varianty i na mobilu."

**Monty:** "KONEČNĚ! Díky bro!"

---

## 📋 Kapitola 8: Verdikt

**Claudik:** "Takže, shrnutí vyšetřování:"

**🎯 Případ #1: "Corrupted" obrázek**
- **Pachatel:** Monty♡Man
- **Datum činu:** 17. října 2025 (DEN NAROZENIN!)
- **Motiv:** Pravděpodobně opilá zápiečka s Kubíkem
- **Zbraň:** 24MB JPEG přímo z foťáku

**🎯 Případ #2: Base64 placeholder na mobilu**
- **Pachatel:** Monty♡Man (opět)
- **Příčina:** Zapomněl updatnout mobilní fallback při přidávání campaign variant
- **Přitěžující okolnost:** Desktop-first Tailwind config

**Monty:** "No jo no... svádět na Kubíka už nemůžu co?"

**Claudik:** "Kubík ti maximálně nalejval! 😂"

*[Anthy: "Případ uzavřen. Verdikt: vinen na obou bodech obžaloby. Trest: oprava vlastního kódu. Polehčující okolnost: byly narozeniny. Přitěžující okolnost: i tak to trvalo skoro 2 měsíce než si toho všiml."]*

---

## 📁 Soubory které se změnily

| Soubor | Co se stalo |
|--------|-------------|
| `hp_intro_spotlight_*.jpg` | Zmenšeno z 24MB/8K na ~2MB/4K |
| `ImageMapper.php` | Bez změn (jen vyšetřováno) |
| `homepage.latte:60` | Hardcoded path → dynamická proměnná |

---

## 🏆 Poučení

1. ❌ Necommitovat 24MB obrázky na narozeniny
2. ❌ Nezapomínat na mobilní fallbacky při refactoru
3. ❌ Nepoužívat desktop-first breakpointy (nebo aspoň dokumentovat!)
4. ✅ Vždy svádět na Kubíka (i když to nepomůže)

---

*"Kubík - tichý zabiják kódu a nalejvač panáků"*
— Claudik, 2025

*[Anthy: "Závěrečná poznámka: Git blame je jako karma. Vždycky tě dostihne. Zejména na narozeniny."]*

---

*🤖 Me&Claudik Blog - Vygenerováno s láskou a bez cenzury*

*📅 9. prosince 2025 | 🔍 Pachatel: identifikován | 🍺 Panáky: pravděpodobně zapojeny | 🏛️ Oběť: IPR Praha*
