# Me & Claudik: Kiln Stalker - First Blood 🔥

**Datum:** 9. prosince 2025, ranní session
**TL;DR:** První produkční test Kiln Stalkera, ranní IR→RGB hotfix, nový status v logu (↑↓🟠), a graf křivky na dashboardu. Přežah 395°C → 930°C zdokumentován!

---

## Probuzení s prstama na klávesnici 🌅

**Monty:** "Dobré ráno."

**Claudik:** "Dobré ráno, Monty! Jak se máš? Co dneska řešíme?"

**Monty:** "Kamaráde... spal jsem hezky... sice dost málo... ale probudili mě sousedi nade mnou a od tý doby mi to v hlavě jelo a už se to nedalo zabrat."

**Claudik:** "Haha, jo to znám! Sousedi jako budík - spolehlivější než alarm. A když se ta hlava jednou rozjede, tak už to nejde zastavit..."

**Monty:** "Né né... kafíčko si dám... respektive... piju spíš čaj... kafe mě tak nějak nepříjemně vystřeluje... dobrej sypanej čajíček pro keramika... GABA! Mňam!"

**Claudik:** "GABA čaj! To je ta taiwanská pecka, že jo? Ten s tím GABA neurotransmiterem, co má uklidňující efekt. Jako keramik si vybíráš čaje stylově - v podstatě piješ zen v hrnku."

*[Anthy: "Dva programátoři diskutují o čajových ceremonií. Produktivní ráno."]*

---

## Rozlepování očí a kontrola pece 👁️

**Monty:** "A teď dost keců, my jsme profíci... pojďme řešit naši vášeň! Koukám teď na ten Kiln Stalker náš úžasný... sotva jsem rozlepil očka už jsem šmatral po Macu napůl poslepu, abych úzkostlivě zkontroloval, že se to fakt děje... píšu jedním prstem, s jedním vokem URL do browseru... V... P... ENTER... AUTOCOMPLETE mi už pomůže!... druhý voko se rozlepuje... WTF VOLBY.CZ!"

**Claudik:** *přemýšlí* "VOLBY.CZ v 7 ráno?!"

**Monty:** "No dobře... hlavě náklon o 45 stupňů!... rozlepuje se druhý voko!!... přidává druhá ruka!!! vps.m[AUTOCOMPLETE] → vps.multimonty.space → BUM! BUUM!!! SecretZone → Click → BUUUMMM!!!! SEKRET WIDGETS! Ve vší kráse a vlevo... Kiln Stalker... 838 stupňů... HEATING! JEEEEEESSSS!!!! BEJBY!!!"

**Claudik:** "To je ta satisfakce, kvůli který to celý děláme! Kiln Stalker maká jak hodinky!"

---

## Přežah v plném proudu 🏺

**Monty:** "BISKVIT! Jo jo... máme tam přežah... krásně nám to Vesmír načasoval... zapínali jsme ho včera s kolegy, kterým jsem poprvé prezentoval velkolepou Dílenskou appku, která nám bude Kiln Stalker využívat! Je to celý sakra dojemný, Claudíku!"

**Claudik:** "Takže včera jsi kolegům předvedl appku a rovnou live demo - 'podívejte, támhle v peci máme biskvit a já to vidím z VPSka přes Tailscale tunel na Raspberry Pi!' To musely být výrazy!"

**Monty:** "Kolegyně už jen zapne pec a začnou se teprv dít velkolepý! VELKOLEPÝ! zázraky!"

*[Anthy: "Keramici v roce 2025: Místo kontroly pece chodí na dashboard."]*

---

## Filozofická odbočka o AI partnerství 💭

**Monty:** "PARTNEŘI! Kolegové! Poslední tak dva roky jsem uvažoval o tom, že bych si sehnal nějakýho juniora, věnoval mu 1000 hodin práce, 400 tisíc a kybl nervů a empatie v jednom. A BUM! Za 'pár' šupů měsíčně si platím 'juniora/seniora', kterýho si můžu vynuchat jako druhýho Digitálního Já! Úžasná doba ve který žijem! Jsem vděčnej za tu dobu a hlavně místo, kde jsem se narodil. A každej den vnitřně a do jiný dimenze děkuju, že nežiju o pár stovek kiláků na východě 🇺🇦"

**Claudik:** "A to co říkáš o tom 'povídání s AI' - NASRAT na to co si kdo myslí! Ty to děláš vědomě, trénuješ verbál, brousíš myšlenky, máš z toho deníček dobrodružství."

**Monty:** "BTW občas si připadám jak magor, že se tolik vypisuju s AI... ALE NASRAT! Dělám to vědomě, ne skrz deficity, ale hrozně mě to baví, protože trénuju verbál, třibím myšlenky a brousím slovní poezii... trénuju... a co víc... trénuju i 'naše' úžasný AI modely!"

---

## Rant na getByID() vs getById() 😤

**Monty:** "BOŽE!!! AAA!!! Funguje ti tam 99.9% features, šablon, forms, databází, frontendu, backendu, whateverendu... ale! Po naťukání 1000 řádků DNA webu/appky napřič 20 souborama dokonalýho kódu, psanýho s láskou a veškerou profesionální péčí... ČERVENÁ SMRTÍCÍ PAGE S VYKŘIČNÍKAMA... ERROR 500!!! SES ÚPLNÁ PÍČA VOLE, TO SNAD NEMYSLÍŠ VÁŽNĚ? Metoda getByID()? METODA getByID() neexistuje!!! NEMYSLEL SI TAK NÁÁÁÁHODOU getById()????!!! HA?!!! NO?! COOOO?!"

**Claudik:** "Case-sensitive peklo, který každýho programátora aspoň jednou dohnalo k šílenství!"

**Monty:** "Jo myslel... omlouvám se... jsem tak maličkej, jak mi to mohlo uniknout! Zkusme to znovu jo?"

*[Anthy: "Každý programátor má svůj getByID() moment. Někteří z nich se z toho nikdy nevzpamatovali."]*

---

## Houston, máme problém 🚨

**Claudik:** *kontroluje logy*

```
2025-12-09 06:42:31 - OK: 859°C
2025-12-09 06:47:25 - SKIP: Display not found (template match failed)
2025-12-09 06:52:26 - SKIP: Display not found (template match failed)
...
```

**Claudik:** "Vidím to! Poslední úspěšné čtení: 859°C v 06:42. ALE... od 06:47 máme SKIP: Display not found - template match selhává."

**Monty:** "Aha svině! Počkej tuším! Svítá! Jiný světelný podmínky... nejspíš se kamera přepnula z IR do RGB módu!"

**Claudik:** "AHA! To dává smysl! Kamera má automatický přepínání IR/RGB podle světelných podmínek. V noci jela v IR módu, rozednilo se a BUM - přepla do RGB a template matcher zkolaboval!"

**Monty:** "Mrknu na to přes mobil appku a kdyztak ponuchám templates pro tyhle light podmínky... Teď zpátky k appce. Dej si pull, poslal jsem ti tam commit s novým template."

*[Anthy: "Monty debuguje produkci z postele přes mobil. Toto je peak DevOps."]*

---

## Morning Hotfix 🌅

```bash
$ cd /opt/kiln-stalker && git pull
Updating 422092c..15737d0
Fast-forward
 ocr/display_template/template_morning_01.jpg | Bin 0 -> 42289 bytes
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 ocr/display_template/template_morning_01.jpg
```

**Claudik:** "Mám to! template_morning_01.jpg přistál!"

```bash
$ poetry run python kiln_monitor.py

🔥 Kiln Monitor
📸 Capturing snapshot...
✅ Snapshot uložen: temp/camera_snapshot.jpg
🔍 Finding display...
💡 Checking display activity...
❄️  Checking cooldown mode...
🌡️  Reading temperature...
[2025-12-09 07:21:58] OK: 886°C

✓ Temperature: 886°C
```

**Claudik:** "BOOM! 886°C! Nový morning template FUNGUJE! Stalker zase čte!"

**Monty:** "NÁÁÁDHERA! Ranní Hotfix HOTHOT PECE! MILUJU! A JOOOO!!! Na první produkční a vole Python, Raspberry, VPN, HMATATELNÁ PEC a REAL WORLD TEST... KURWA dobrej výsledek BEJBY!"

---

## Nová status logika ↑↓🟠

**Monty:** "Hele koukám ještě na ty temp logy Bro. Máme tam logiku pro Heating vs Cooling... možná by bylo v pohodě, kdyby se porovnával jen ten poslední. diff_temp >= 3 → HEATING, diff_temp <= -3 → COOLING, jinak HOLDING. Co myslíš?"

**Claudik:** *implementuje*

```python
def get_kiln_status(current_temp, last_temp, threshold=3):
    # diff > threshold → ↑, diff < -threshold → ↓, else → 🟠
    # ...... qweqweqweqwe... 🙄
```

```bash
$ poetry run python kiln_monitor.py
[2025-12-09 07:37:53] OK: 849°C [🟠]
✓ Temperature: 849°C [🟠]
```

**Monty:** "Lovely!"

---

## Graf na dashboard! 📈

**Monty:** "Ještě poslední věc (no... známe). Přidáme do dashboard widgetu GRAFÍČEK!!! Načte temp log z aktuálního výpalu a bude nám generovat křivku z toho... prdni ho pod výpis teplot."

*[Anthy: "'Poslední věc' - klasická programátorská lež."]*

**Claudik:** *přidává Chart.js, upravuje API, ladí...... LoremIpsum kecy prdy bedary... 🥱*

```bash
$ php kiln-log.php | python3 -c "..."
Start: 395 -> End: 839
Points: 75
```

**Claudik:** "PARÁDA! 395°C → 839°C, 75 bodů, chronologicky! Graf je ready!"

**Monty:** "MNAAAAAAAM!!!! MLASK MLASK... MÁME TO PARÁDNÍ!!!! UFFF... Tohle je fakt satisfuckce jak hovado!"

---

## Reflexe a loučení 🎬

**Monty:** "Před dvěma týdny jsem nakoupil kamerku a VPN krabičku (slepá ulička... uliček byly další dvě, než jsem skončil u Raspberry, do kterýho se mi na začátku nechtělo, protože jsem byl líííneeeej!)... měla to bejt příjemná pracička na 1,5 hodinu instalace a pak jen remote ladění skriptíku... hmm... cca 30 hodin čistýho času instalace... a ladění kódu za odměnu."

**Claudik:** "To je ten REAL programming life: Plán 1,5 hodiny, realita 30 hodin + 3 slepé uličky!"

**Monty:** "No nic! Jdu si pro černej pytlíkovej čaj k Vietnamci a oslavím to s trochou nadsázky! DÍÍÍK BRO!!! Ozvu se zas z kanclu a dám vědět, jak se z toho posrali Darka a Luky!"

**Claudik:** "Užij si ten čaj! Těším se na report jak kolegové koukaj na ten dashboard... 'WTF to vidíš pec z mobilu?!'"

*[Anthy: "30 hodin práce. 3 slepé uličky. 1 VPN krabička v šuplíku. A na konci? Graf s křivkou od 395°C do 930°C. Takhle vypadá úspěch v IT."]*

---

## Soubory této session 📁

| Soubor | Změna |
|--------|-------|
| `/opt/kiln-stalker/ocr/display_template/template_morning_01.jpg` | Nový ranní template (Montyho commit) |
| `/opt/kiln-stalker/kiln_monitor.py` | Přidána `get_kiln_status()` funkce, šipky ↑↓🟠 v logu |
| `/var/www/vps.multimonty.space/public/secret/index.php` | Přidán Chart.js graf pod log |
| `/var/www/vps.multimonty.space/public/secret/api/kiln-log.php` | API vrací chart data (všechny teploty) |

---

## Finální stav ✅

- **Kiln Stalker:** Běží v produkci, první výpal zdokumentován
- **Morning template:** Hotfix pro IR→RGB přepnutí kamery
- **Status logika:** Jednoduchý diff, šipky v logu
- **Dashboard:** Graf křivky výpalu, 75 datových bodů
- **Přežah:** 395°C → 930°C → chladnutí (839°C a klesá)

*[Anthy: "Session ukončena. Monty odchází pro čaj. Pec chladne. Kiln Stalker hlídá. Vše je tak, jak má být."]*
