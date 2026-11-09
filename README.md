# Maserati – Canvas, SVG in PNG

Spletna stran, ki prikazuje znak Maserati (trizob), narisan na tri različne načine. Vsak način je prikazan na svojem izdelku, barvi izdelka in znaka pa lahko uporabnik spreminja.

| Zavihek | Izdelek | Način risanja znaka |
|---|---|---|
| Kapa (Canvas) | kapa | `<canvas>` in `bezierCurveTo()` |
| Polo majica (SVG) | polo majica | `<svg>` s potmi (`<path>`) iz Bezierjevih krivulj |
| Jakna (PNG) | bomber jakna (hrbtna stran) | znak izvožen iz canvasa v PNG (`toDataURL`) in vstavljen kot slika |

## Datoteke

```
maserati_logo.html   stran, HTML in JavaScript
stil.css             ves videz strani
kapa.png             slika kape
polo.png             slika polo majice
jakna.png            slika jakne
README.md            ta datoteka
```

Vse datoteke morajo biti v isti mapi.

## Zagon

1. Razpakiraj mapo (če je v zip datoteki).
2. Odpri `maserati_logo.html` v brskalniku (dvoklik ali desni klik → Odpri z). Strežnik ni potreben.
3. Z zavihki na vrhu preklapljaš med kapo, polo majico in jakno.

Če ima stran brez stila ali brez slik, preveri, da so `stil.css` in vse tri slike v isti mapi kot HTML.

## Možnosti na vsaki strani

- **Barva izdelka** – izbirnik barve ali šest hitrih barv (bela, črna, modra, rdeča, zelena, rumena). Sence in gubice izdelka ostanejo.
- **Barva znaka** – izbirnik barve, ki prebarva znak.
- **Ponastavi** – vrne belo barvo izdelka in rdeč znak (`#c12127`).

## Kako deluje

- **Znak brez decimalk.** Vse koordinate znaka (canvas in SVG) so cela števila. Prvotne vrednosti so pomnožene z 10 in zaokrožene, zato je `96.788, 42.805` postalo `968, 428`. Canvas je velik 720 × 770, SVG pa ima `viewBox="640 305 720 770"`. Primerjava z originalom pokaže razliko le na robovih (okoli 1,5 % točk znaka).
- **Canvas.** Funkcija `narisiZnak(context, barva)` nariše znak z `moveTo`, `lineTo` in `bezierCurveTo`. Kličeta jo kapa (neposredno na prikazan canvas) in jakna (na skrit canvas, iz katerega nastane PNG).
- **SVG.** Poti so definirane enkrat v `<defs>` (`id="znak-poti"`) in se prikažejo z `<use>`. Barva se spremeni z atributom `fill`. Isti znak je tudi v zgornji vrstici.
- **PNG.** Znak se nariše na skrit canvas in se z `toDataURL("image/png")` pretvori v sliko s prosojnim ozadjem.
- **Barvanje izdelka.** Slika izdelka se nariše na canvas, barva se pomnoži (`multiply`) in odreže po obliki izdelka (`destination-in`), tako da ozadje ostane prosojno.
- **Zavihki.** Menjava strani prikaže eno `.stran` in skrije ostale. Izbran zavihek se zapiše v naslov (`#kapa`, `#polo`, `#jakna`).

## Objava na GitHub Pages

Stran je objavljena na: **https://UPORABNIK.github.io/REPOZITORIJ/** (zamenjaj z lastnim naslovom).

Postopek objave:

1. Ustvari repozitorij na GitHubu in vanj naloži vse datoteke iz te mape (v koren, ne v podmapo).
2. Datoteko `maserati_logo.html` preimenuj v `index.html`, da se stran odpre kar na naslovu repozitorija. Sicer jo odpreš na `.../maserati_logo.html`.
3. Odpri Settings → Pages, izberi Deploy from a branch, vejo `main` in mapo `/ (root)`, nato Save.
4. Čez minuto ali dve je stran dostopna na zgornjem naslovu.

Vse poti do datotek so relativne (`stil.css`, `kapa.png` …), zato dodatne nastavitve niso potrebne. GitHub Pages loči velike in male črke v imenih datotek, zato naj ostanejo imena taka, kot so.

## Opombe

- Slike so iz spletnih virov (pngtree in podobno). Slika kape ima ostanek vodnega žiga.
- Znak Maserati je last podjetja Maserati. Projekt je izdelan za šolsko nalogo.
