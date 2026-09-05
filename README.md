# jirirenza.cz

Statická kopie webu, připravená k nasazení. Žádný server, databáze ani
administrace — jen soubory. Nic se nenačítá z Webnode ani z Googlu.

## Co je ve složce

```
index.html              →  /                    úvodní stránka
pst-principy/           →  /pst-principy/       psychoterapie a principy
osobni-udaje/           →  /osobni-udaje/       ochrana osobních údajů
dalsi-vzdelani/         →  /dalsi-vzdelani/     další vzdělání
img/                    →  21 obrázků ve WebP, každý ve dvou šířkách
*.woff2                 →  písma Josefin Sans a Metropolis
CNAME                   →  doména pro GitHub Pages
.nojekyll               →  vypne generátor GitHubu
```

Každá podstránka je vlastní složka se souborem `index.html`. Tak to musí
být, aby adresy zůstaly stejné jako na Webnode a nepřišel jsi o pozice
ve vyhledávání. Soubor `pst-principy/index.html` se v prohlížeči otevře
jako `www.jirirenza.cz/pst-principy/`.

Styly jsou vložené v hlavičce každé stránky a ve všech čtyřech jsou
totožné. Když upravíš CSS, zkopíruj změnu i do zbylých tří souborů.
V kódu jsou u každého bloku české komentáře, co se dá měnit.

## Nahrání na GitHub Pages

### 1. Repozitář

Na github.com si udělej účet a nový repozitář. Na bezplatném tarifu musí
být **public**, jinak Pages nefungují. Jméno může být cokoli.

Nahraj **obsah** téhle složky do kořene repozitáře — ne složku samotnou.
V repozitáři má být rovnou `index.html`, ne `jirirenza-web/index.html`.
Přes web: „Add file" → „Upload files" → přetáhni soubory → „Commit".

### 2. Zapnout Pages

Settings → Pages → Source: „Deploy from a branch", branch `main`,
složka `/ (root)` → Save.

Za pár minut web pojede na `https://uzivatel.github.io/nazev-repa`.
**Tady si ho pořádně proklikej**, starý web zatím běží dál na Webnode.

### 3. Doména v GitHubu

Settings → Pages → Custom domain: `www.jirirenza.cz` → Save.
Soubor `CNAME` tuhle hodnotu už obsahuje.

### 4. DNS u Wedosu

Zákaznický portál → Domény → jirirenza.cz → DNS záznamy.

Nejdřív **sniž TTL na minimum** a počkej, než se stará hodnota přestane
používat. Pak smaž záznamy mířící na Webnode a přidej tyhle:

| Typ   | Název | Hodnota              |
|-------|-------|----------------------|
| CNAME | www   | `uzivatel.github.io` |
| A     | @     | 185.199.108.153      |
| A     | @     | 185.199.109.153      |
| A     | @     | 185.199.110.153      |
| A     | @     | 185.199.111.153      |

CNAME obsluhuje adresu s www, čtyři A záznamy zajistí, že `jirirenza.cz`
bez www přesměruje na www verzi.

### 5. HTTPS

Po propsání DNS (desítky minut až hodiny) se v Settings → Pages odemkne
volba **Enforce HTTPS**. Zaškrtni ji. Certifikát vystaví GitHub zdarma.
Když je volba šedá, jen ještě neproběhlo ověření — počkej a zkus znovu.

### 6. Kontrola před zrušením Webnode

- `https://www.jirirenza.cz` i `https://jirirenza.cz` vedou na web
- fungují všechny čtyři adresy včetně podstránek
- fotky se načítají, písmo je správné
- web vypadá dobře na mobilu

Teprve potom ruš službu u Webnode. Doménu si předtím převeď k vlastnímu
registrátorovi, pokud je vedená pod nimi.

## Úpravy

### Text
Otevři HTML v textovém editoru. Text je vidět mezi značkami, přepiš ho
a ulož. Pozor na diakritiku — editor musí ukládat v UTF-8.

### Obrázky
Ve složce `img/`, ve dvou šířkách. Výměna:

```bash
magick foto.jpg -resize 800x -quality 82 img/nazev-800.webp
magick foto.jpg -resize 400x -quality 82 img/nazev-400.webp
```

Ořez řídí `object-position` v CSS: dvě hodnoty, vodorovně a svisle,
`0%` vlevo/nahoře, `50%` střed, `100%` vpravo/dole.

### Písmo
Josefin Sans (nadpisy a menu) a Metropolis (text) — obojí zjištěno
z původní Webnode šablony. Jsou oříznuté na české znaky a vložené přímo
v CSS, dohromady 48 kB. Samostatné `.woff2` soubory jsou přiložené.

### Rozvržení
Šířka stránky, mezery mezi bloky, počty sloupců i ořezy fotek jsou
popsané v komentářích v CSS. Hledej řádky začínající `/* ---`.

## Co zbývá dořešit

- Doplnit, jestli bereš nové klienty a jak dlouho se čeká na termín
- Ověřit jméno „Ana N. Gomez" v seznamu vzdělání
- Zvážit větu o tom, že terapie není akutní pomoc, s odkazem na
  Linku první psychické pomoci (116 123)
- Rozhodnout, jestli vrátit kredit fotografům z Unsplashe na stránku
  principů (v zápatí úvodní stránky zůstal)
