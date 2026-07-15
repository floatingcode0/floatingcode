# 🌊 Lanseringsguide 2.0 – floatingcode.se

Din kompletta guide för den nya hemsidan (12 filer). Följ delarna i ordning – del 1–2 räcker för att sidan ska vara live, resten gör du i din egen takt.

---

## Dina 12 filer (checklista)

- [ ] `index.html` – startsidan
- [ ] `aktuella-kurser.html` – dina tillfälliga livekurser
- [ ] `julkalendrar.html` – försäljningssidan för skolkalendrarna (publik)
- [ ] `villkor.html` – köpvillkor & integritetspolicy
- [ ] `404.html` – "sidan finns inte"-sidan (funkar automatiskt)
- [ ] `kurs-intro-scratch-p3n8q.html` – kurssida Scratch (hemlig)
- [ ] `kurs-intro-roblox-x7k2m.html` – kurssida Roblox (hemlig)
- [ ] `julkalender-roblox-j9w4t.html` – kodkalendern privatkunder (hemlig)
- [ ] `tomtens-verkstad-julkalender.html` – skolkalendern (lösenordsskyddad)
- [ ] `tack-tomtens-verkstad-b7q2x.html` – tack-sida efter skolköp (hemlig)
- [ ] `logga.png` – roboten
- [ ] `profil.png` – din profilbild

---

## Del 1: Lägg upp sidan på GitHub Pages (gratis)

1. Gå till **github.com** och skapa ett gratiskonto.
2. Klicka **+** uppe till höger → **New repository**.
3. Döp det **exakt** till: `dittanvändarnamn.github.io` (små bokstäver).
4. Välj **Public** → **Create repository**.
5. Klicka **uploading an existing file** och dra in **alla 12 filerna** samtidigt.
6. Klicka gröna knappen **Commit changes**.
7. Vänta 1–2 minuter, öppna sedan `https://dittanvändarnamn.github.io` – där är sidan! 🎉
8. Testa i mobilen: menyn, alla sidor, bilderna.

**Uppdatera en fil senare:** gå till repositoryt → klicka på filen → pennikonen ✏️ → redigera → Commit changes. Eller ladda upp en ny version (gamla skrivs över). All historik sparas, så du kan alltid ångra.

## Del 2: Koppla floatingcode.se

1. I repositoryt: **Settings → Pages** → under **Custom domain**: skriv `floatingcode.se` → **Save**.
2. Logga in hos ditt webbhotell → hitta **DNS-inställningarna** för floatingcode.se.
3. Skapa **fyra A-poster** (host: `@` eller tomt):
   - `185.199.108.153`
   - `185.199.109.153`
   - `185.199.110.153`
   - `185.199.111.153`
4. Skapa **en CNAME-post** med namn `www` som pekar på `dittanvändarnamn.github.io`
5. Ta bort gamla A-poster som pekar på webbhotellet (fråga supporten vid osäkerhet).
6. När floatingcode.se visar nya sidan (kan ta upp till ett dygn): **Settings → Pages** → bocka i **Enforce HTTPS**.
7. Behåll domänregistreringen men säg upp webbhotellet – **först när allt funkat felfritt några dagar!**

---

## Del 3: Koppla dina videoklipp till luckorna 🎬

### Steg A – ladda upp på Vimeo (görs en gång per film)

1. Skapa konto på **vimeo.com**, välj **Starter-planen** (din enda månadskostnad).
2. Ladda upp filmen. Gå in på videons inställningar och sätt:
   - **Privacy / Who can watch:** `Hide from Vimeo`
   - **Where can this be embedded:** `Specific domains` → lägg till `floatingcode.se` och `www.floatingcode.se`
   - **Downloads:** AV
3. Kopiera videons **ID** = siffrorna i adressen. Ex: `vimeo.com/987654321` → ID är `987654321`.

### Steg B – klistra in ID:t på rätt ställe (olika per sida!)

**🎄 Skolkalendern (tomtens-verkstad-julkalender.html):**
Öppna filen, scrolla till listan `LUCKOR`. Varje lucka har `vimeo:""`. Klistra in ID:t mellan citattecknen:
```
{datum:"2026-12-01", vimeo:"987654321", titel:"Välkommen till verkstan", ...
```
Lucka 1 i listan = lucka 1 på sidan. Tomt `vimeo:""` visar en snygg platshållare, så du kan fylla i i din egen takt.

**🎁 Privatkalendern (julkalender-roblox-j9w4t.html):**
Samma princip, men listan heter `UTMANINGAR` och fältet heter `video:""`:
```
{titel:"Bygg din startplatta", uppgift:"...", larartips:"...", video:"987654321"},
```
Video är valfri per lucka här – tom sträng betyder ingen film.

**🎓 Kurssidorna (kurs-intro-...):**
Sök på `VIMEO-ID` (7 ställen per fil) och byt varje mot rätt films ID. Lektion 1 = film 1, osv.

### Steg C – testa!

1. Ladda upp de ändrade filerna till GitHub.
2. Skolkalendern: öppna med `?testa=1` på slutet → alla luckor öppna, ingen kod krävs. Klicka en lucka och se att filmen spelar.
3. Privatkalendern: öppna med `?testdag=24` på slutet.
4. **Viktigt:** filmerna spelar bara på floatingcode.se (domänlåset), så testa på riktiga adressen – inte genom att öppna filen direkt på datorn.

---

## Del 4: Ta betalt

### Privatkunder (kurser + privatkalendern) – Stripe

1. Skapa konto på **stripe.com** (kräver organisationsnummer + bankkonto).
2. Skapa en **Produkt** per kurs med pris i SEK, och en **Payment Link** per produkt.
3. I betallänken under **After payment**: välj **Redirect to your website** och klistra in den hemliga sidans adress:
   - Roblox-kursen → `https://floatingcode.se/kurs-intro-roblox-x7k2m.html`
   - Scratch-kursen → `https://floatingcode.se/kurs-intro-scratch-p3n8q.html`
   - Roblox-kalendern → `https://floatingcode.se/julkalender-roblox-j9w4t.html`
4. Slå på **kvittomejl** i Stripe.
5. Öppna `index.html`, sök på `BETALLÄNK-HÄR` och klistra in rätt länk på varje knapp. Sök på `PRIS-HÄR` och skriv dina priser.
6. Sök på `FORMULÄR-LÄNK-HÄR` (finns i **både** index.html och aktuella-kurser.html) och klistra in nyhetsbrevslänken.

### Skolor (julkalendrar.html) – kort + faktura

1. **Faktura funkar redan nu!** Knapparna öppnar ett färdigt beställningsmejl till dig. Du fakturerar och mejlar sedan kalenderkoden (**TOMTEN2026**) + länken till kalendern.
2. **Kortbetalning:** skapa en betallänk (Stripe funkar här också) och sätt redirect efter betalning till tack-sidan:
   `https://floatingcode.se/tack-tomtens-verkstad-b7q2x.html`
   → kunden ser kalenderkoden och länken **direkt på skärmen** = tillgång direkt.
3. Klistra in betallänken i `julkalendrar.html` i listan `KORTLANKAR` (raden `"roblox-kort"`).

---

## Del 5: Aktuella kurser – lägga ut ett kurstillfälle

1. Öppna `aktuella-kurser.html`, scrolla till listan `KURSTILLFALLEN`.
2. Kopiera ett helt block `{ ... },` och ändra datum, titel, tid, ålder, pris, beskrivning.
3. `lank:""` = knappen blir "Anmäl intresse" (mejl till dig). Klistra in en betallänk = "Boka plats". `fullbokad:true` = visar Fullbokad.
4. Ladda upp filen. Passerade kurser döljs automatiskt – du behöver aldrig ta bort gamla.
5. Byt ut de två exempelkurserna som ligger inne nu!

---

## Alla koder & testlägen (spara denna ruta!)

| Sida | Kod/skydd | Testläge |
|---|---|---|
| Skolkalendern | Kalenderkod **TOMTEN2026** | `?testa=1` = hoppa över kod + öppna allt |
| Privatkalendern | Hemligt filnamn | `?testdag=24` = låtsas att det är 24 dec, `?larare` = lärartips |
| Kurssidorna | Hemliga filnamn | – |
| Tack-sidan | Hemligt filnamn | – |

**Byta kalenderkoden?** Sök på `TOMTEN2026` i **två** filer: tomtens-verkstad-julkalender.html och tack-tomtens-verkstad-b7q2x.html.

---

## Nytt sedan konkurrentanalysen (juli 2026)

Julkalendrar-sidan har fått fyra nya delar som konkurrenterna saknar eller som lärare förväntar sig:

1. **Testa en lucka gratis** – sänker köpsrisken för läraren. Klistra in Vimeo-ID:t för lucka 1 av Tomtens verkstad i `GRATISLUCKA` (i inställningsblocket i julkalendrar.html). Tills dess visas en "Mejla mig provluckan"-knapp som skapar ett färdigt mejl – så sektionen fungerar redan nu, och du får dessutom varma leads i inkorgen.
2. **Läroplanskoppling (Lgr22)** – motiverar inköpet uppåt mot rektor och kommun. Klar att använda.
3. **Röster från klassrummen** – ligger bortkommenterad tills du har riktiga citat. Tips: erbjud 2–3 pilotskolor rabatt i utbyte mot ett omdöme (fråga alltid om lov innan du publicerar namn). Aktivera genom att ta bort kommentarstecknen runt sektionen.
4. **FAQ med Google-data** – vanliga lärarfrågor med utfällbara svar, plus strukturerad FAQ-data i sidhuvudet så att frågorna kan visas direkt i Googles sökresultat. Ändrar du en fråga: uppdatera på **båda** ställena.

Dessutom: org.nr och ort visas nu även i footern på julkalendrar-sidan (samma FYLL-I-platshållare som i villkor.html).

- [ ] `GRATISLUCKA` ifylld med Vimeo-ID för provluckan
- [ ] Röster-sektionen aktiverad när första citaten finns
- [ ] FYLL-I-ORT och org.nr utbytta även i julkalendrar.html:s footer

---

## Slutchecklista före lansering

- [ ] Sidan syns på floatingcode.se med hänglås (HTTPS)
- [ ] Alla `PRIS-HÄR` utbytta mot riktiga priser (index + aktuella-kurser)
- [ ] Alla `BETALLÄNK-HÄR` utbytta mot Stripe-länkar
- [ ] `FORMULÄR-LÄNK-HÄR` utbytt (2 filer)
- [ ] `FYLL-I` i villkor.html utbytt mot org.nr och ort (5 ställen)
- [ ] Vimeo-ID inlagda, filmerna spelar på floatingcode.se
- [ ] Testköp gjort: betalning → skickas till rätt hemlig sida
- [ ] Skolkalendern testad med `?testa=1` och med koden TOMTEN2026
- [ ] Exempelkurserna på aktuella-kurser.html utbytta mot riktiga (eller borttagna)
- [ ] Gamla webbhotellet uppsagt – men domänen behållen!

*Flyt lugnt! 🌊*
