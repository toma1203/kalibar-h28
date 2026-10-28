# Kalibar H-28

Interaktivna 3D stranica o mehaničkom satu (Three.js r128, jedan HTML fajl, bez build koraka).

## Što je napravljeno
- Proceduralni model sata: kućište s ušicama, krunica s narezima, safirno staklo, sunray brojčanik, kazaljke koje pokazuju stvarno vrijeme.
- Mehanizam: ploča s perlage uzorkom, bačva s vidljivom glavnom oprugom, središnji/treći/četvrti kotač, kotvin kotač, kotva, balans s vlasnom oprugom, mostovi sa ženevskim prugama, rubini, plavi vijci, zaporni kotač, stražnji poklopac sa staklom.
- Studijsko osvjetljenje kao u Blenderu: env map generiran iz scene sa softbox panelima (PMREM), ACES tone mapping, meka sjena na podu.
- Kotačić miša ne skrola stranicu nego pomiče "napredak" 0–1 kroz 9 poglavlja (keyframeovi: rotacija, rastavljanje, udaljenost kamere, fokus). Nakon pauze se poravna na najbliže poglavlje.
- Miš: povlačenje okreće sat. Dodir: povlačenje prstom mijenja poglavlje. Strelice, Home/End.
- Traka na dnu s klikabilnim poglavljima, oznake (callouts) projicirane iz 3D na ekran.
- Loader, poruke o greškama (nema WebGL-a, CDN blokiran, izgubljen kontekst), prefers-reduced-motion.

## Naučeno
- Pomak modela udesno radi se `camera.setViewOffset`, pa projekcija oznaka ostaje točna.
- Brojčanik je CircleGeometry (a ne cilindar) da UV i tekst na canvasu budu ispravno orijentirani; canvas se ponovno crta nakon `document.fonts.ready`.
- Kretanje mehanizma koristi stvarne omjere: sekunda u 8 koraka (4 Hz), kotvin kotač 1/30 okreta po otkucaju.

## Ispravci
- v2: stranica se nije učitavala. U three.js r128 `THREE.Curve` je ES klasa, pa `THREE.Curve.call(this)` baca grešku. Spirala sada koristi `class Spiral extends THREE.Curve`. Dodan globalni handler koji umjesto vječnog loadera pokaže poruku o grešci.
- v3: u užim prozorima (omjer ispod 16:9) sat je bio prevelik i prekrivao tekst. Udaljenost kamere sada raste s omjerom ekrana.
- Provjereno u pregledniku: učitava se, kotačić okreće sat, nema grešaka u konzoli.

- v4–5: novi izgled. Tamnozelena podloga kao urarska radna ploča, mjedeni naglasci, bjelokosni tekst. Fontovi: Bodoni Moda (naslovi), Hanken Grotesk (tekst), JetBrains Mono (podaci). Env map i sjena obojeni zeleno da odsjaji pašu podlozi. Sekundna kazaljka u mjedi radi kontrasta na plavom brojčaniku.
- v6: fontovi promijenjeni u Michroma (naslovi, natpis na brojčaniku), Albert Sans (tekst) i JetBrains Mono (podaci). Michroma je vrlo širok, pa su naslovi manji (24–38 px).
- v7: Michroma primijenjen na sav tekst (tekst, oznake, podaci, traka, sat u kutu, natpisi na brojčaniku). Zbog širine fonta smanjene su veličine (tekst 13 px, oznake 9–10 px) i razmak između slova.
- Priprema za GitHub: `index.html` dobio pun HTML kostur (doctype, `lang="hr"`, charset, viewport) da radi samostalno, npr. na GitHub Pagesu. Dodana stranica `404.html`.

## Pokretanje
Otvori `index.html` u pregledniku ili uključi GitHub Pages (Settings > Pages > grana `main`, mapa `/`). Treba internet za three.js (cdnjs) i font (Google Fonts).

## Ideje za dalje
- Klik na dio sata (raycast) za opis.
- Zvuk otkucaja nakon klika.
- Post-processing (bloom, dubinska oštrina) preko EffectComposera.
