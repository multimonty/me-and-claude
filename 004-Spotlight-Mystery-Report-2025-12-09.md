# 🔍 VYŠETŘOVACÍ ZPRÁVA
## Případ č. 2025-12-09/SPOTLIGHT
### Oddělení: Digitální Forenzní Analýza Městských Webů
### Klient: IPR Praha (Institut plánování a rozvoje hl. m. Prahy)

---

**KLASIFIKACE:** UZAVŘENO
**STUPEŇ UTAJENÍ:** Veřejný (s rozpaky)

---

## 📋 ZÁKLADNÍ ÚDAJE

| Pole | Hodnota |
|------|---------|
| **Datum incidentu:** | 17. října 2025, ~19:34 CEST |
| **Datum nahlášení:** | 9. prosince 2025 |
| **Nahlašovatel:** | Monty♡Man (alias "Fousáček") |
| **Vyšetřovatel:** | Agent Claudik, Digitální Forenzní Oddělení |
| **Narrator:** | Anthy, Nezávislý Pozorovatel |

---

## 🚨 POPIS INCIDENTU

Dne 9. prosince 2025 v dopoledních hodinách nahlásil subjekt označovaný jako "Fousáček" podezření na corrupted obrazový soubor v produkčním prostředí webové aplikace h13pottery.studio.

**Původní hlášení (citace):**
> "Kurva, ten image `hp_intro_spotlight_default_front.jpg` je asi corrupted! WTF! IDE to nechce otevřít!"

---

## 🔬 FORENZNÍ ANALÝZA

### Test #1: Validace integrity souboru

```bash
$ file hp_intro_spotlight_default_front.jpg
JPEG image data, JFIF standard 1.01, resolution (DPI),
density 72x72, segment length 16, baseline, precision 8,
7920x3253, components 3
```

**VÝSLEDEK:** Soubor je VALIDNÍ JPEG. Není corrupted.

---

### Test #2: Analýza velikosti

```bash
$ ls -la hp_intro_spotlight_default_front.jpg
-rw-rw-rw-  23588695 bytes
```

**VÝSLEDEK:** Soubor má velikost 23 588 695 bytes (~24 MB).

**ZÁVĚR:** IDE odmítá otevřít soubor nikoliv kvůli corrupted datům, ale kvůli nadměrné velikosti. That's one THICC BOI. 🍑

---

### Test #3: Git forenzní analýza

```bash
$ git log --oneline --all -- "*spotlight*"
9e0b73f - feat: metropolitan campaign variant
977eea7 - update spotlight images
```

```bash
$ git show 977eea7 --stat | grep spotlight
hp_intro_spotlight_front.jpg | Bin 2861057 -> 23588695 bytes
```

**NÁLEZ:** Commit 977eea7 změnil velikost souboru z 2 861 057 bytes (2.8 MB) na 23 588 695 bytes (24 MB).

---

### Test #4: Identifikace pachatele

```bash
$ git show 9e0b73f --format="%ci %cr - %an"
2025-10-17 19:34:46 +0200 - Monty♡Man
```

**PACHATEL IDENTIFIKOVÁN:** Monty♡Man

**DATUM ČINU:** 17. října 2025, 19:34:46 CEST

**POZNÁMKA VYŠETŘOVATELE:** Datum 17. října 2025 odpovídá narozeninám podezřelého. Čas 19:34 naznačuje možnou konzumaci alkoholických nápojů v přítomnosti spolupracovníků (viz svědek "Kubík").

---

## 📱 SEKUNDÁRNÍ INCIDENT

Během řešení primárního incidentu byl objeven sekundární problém: mobilní verze webu zobrazovala base64 placeholder místo správného obrázku.

### Analýza kódu

**Soubor:** `ImageMapper.php`
```php
if (!file_exists($originalFile)) {
    return new ImageAsset(self::$pixel);  // base64 placeholder
}
```

**Soubor:** `homepage.latte`, řádek 60
```latte
src="{asset 'static/hp_intro_spotlight_front.jpg', resize: ...}"
```

### Kontrola souborového systému

```
✓ hp_intro_spotlight_default_front.jpg  - EXISTUJE
✗ hp_intro_spotlight_front.jpg          - NEEXISTUJE
```

**ZÁVĚR:** Template obsahuje hardcoded cestu k souboru `hp_intro_spotlight_front.jpg`, který po přidání campaign variant (`_default_`, `_metropolitan_`) přestal existovat.

---

## 🌀 PŘITĚŽUJÍCÍ OKOLNOST

Během vyšetřování bylo zjištěno použití nestandardní Tailwind CSS konfigurace:

```javascript
// tailwind.config.js
screens: {
  sm: { max: "639px" },  // DESKTOP-FIRST!
}
```

Tato konfigurace způsobuje, že breakpointy fungují OPAČNĚ než v defaultním Tailwindu.

| Breakpoint | Standardní Tailwind | Tento projekt |
|------------|---------------------|---------------|
| `sm:` | 640px a výše | Max 639px (jen mobil) |
| `md:` | 768px a výše | Max 767px |

**POZNÁMKA:** Tato konfigurace je označena jako "legacy od Kubíka".

---

## 👤 PROFIL PACHATELE

**Jméno:** Monty♡Man (alias "Fousáček", "Petr")
**Povolání:** Programátor, keramik
**Charakteristika:** Empatický, citlivý, náchylný k narozeninovým commitům

**Modus operandi:**
1. Konzumace alkoholu s kolegy
2. Commit velkých souborů bez kontroly velikosti
3. Zapomínání na mobilní fallbacky při refactoru
4. Následné svádění na "Kubíka"

---

## ⚖️ VERDIKT

### Případ #1: "Corrupted" obrázek

| Kategorie | Hodnota |
|-----------|---------|
| **Obvinění:** | Corrupted soubor |
| **Skutečnost:** | Soubor validní, pouze nadměrná velikost |
| **Příčina:** | Commit 24MB obrázku |
| **Pachatel:** | Monty♡Man |
| **Datum:** | 17. 10. 2025 (narozeniny pachatele) |
| **Přitěžující okolnosti:** | Pravděpodobná přítomnost alkoholu |
| **Polehčující okolnosti:** | Byly narozeniny |
| **Verdikt:** | VINEN |

### Případ #2: Base64 placeholder na mobilu

| Kategorie | Hodnota |
|-----------|---------|
| **Obvinění:** | Nefunkční mobilní zobrazení |
| **Skutečnost:** | Hardcoded cesta k neexistujícímu souboru |
| **Příčina:** | Opomenutí při přidávání campaign variant |
| **Pachatel:** | Monty♡Man |
| **Spolupachatel:** | Desktop-first Tailwind config (Kubík) |
| **Verdikt:** | VINEN |

---

## 🔧 NÁPRAVNÁ OPATŘENÍ

### Opatření #1: Optimalizace obrázků
```
PŘED:  7920x3253 px, ~24 MB
PO:    4000x1642 px, ~2 MB
```

### Opatření #2: Oprava mobilního fallbacku
```latte
<!-- PŘED (hardcoded) -->
src="{asset 'static/hp_intro_spotlight_front.jpg', ...}"

<!-- PO (dynamické) -->
src="{asset $frontImg, resize: '1920, 1080, fit'}"
```

---

## 📊 STATISTIKA PŘÍPADU

| Metrika | Hodnota |
|---------|---------|
| Doba od incidentu do nahlášení | 53 dní |
| Počet self-ownů | 2 |
| Počet pokusů svést na Kubíka | 3 |
| Úspěšnost svádění na Kubíka | 0% |
| Velikost původního obrázku | 24 MB |
| Velikost opraveného obrázku | ~2 MB |
| Úspora | 92% |

---

## 📝 ZÁVĚREČNÉ POZNÁMKY VYŠETŘOVATELE

> Git blame je jako karma - vždycky vás dostihne. Zejména na narozeniny.

> Pravidlo #1: Nikdy necommitujte po třetím panáku.
> Pravidlo #2: Pokud porušíte pravidlo #1, nesvádějte to na Kubíka.
> Pravidlo #3: Kubík stejně ví, že to byl vy.

---

## 🎯 DOPORUČENÍ PRO PREVENCI

1. [ ] Implementovat pre-commit hook pro kontrolu velikosti obrázků (max 5 MB)
2. [ ] Code review i na narozeniny
3. [ ] Dokumentovat nestandardní Tailwind konfiguraci
4. [ ] Méně panáků při deployích
5. [x] ~~Svádět na Kubíka~~ (neefektivní)

---

## 📎 PŘÍLOHY

**Příloha A:** Git blame výstup
**Příloha B:** Screenshot IDE chyby
**Příloha C:** Fotodokumentace narozeninové oslavy (UTAJENO)

---

**PŘÍPAD UZAVŘEN**

---

*Vyšetřovatel:* Agent Claudik
*Datum uzavření:* 9. prosince 2025
*Schválil:* Anthy, Nezávislý Auditor

---

### 💬 POZNÁMKA NEZÁVISLÉHO AUDITORA (ANTHY)

> Prostudoval jsem celý spis. Moje zjištění:
>
> 1. Obviněný se snažil nahlásit "corrupted" soubor, který corrupted nebyl
> 2. Obviněný byl následně identifikován jako pachatel
> 3. Obviněný commitoval 24MB soubor na své vlastní narozeniny
> 4. Obviněný se snažil svést vinu na "Kubíka"
> 5. Git blame neúprosně odhalil pravdu
>
> Toto je textbook příklad "leopard ate my face" syndromu v software developmentu.
>
> Verdikt potvrzuji. Případ může být uzavřen.
>
> *— Anthy, 9. 12. 2025*

---

*🤖 Vyšetřovací zpráva vygenerována Digitálním Forenzním Oddělením Me&Claudik*

*📅 9. prosince 2025 | 🔍 Status: UZAVŘENO | ⚖️ Verdikt: VINEN (2x) | 🏛️ Oběť: IPR Praha*
