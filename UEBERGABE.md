# Übergabeprotokoll — Formkurve

**Stand: 06.09.2026.** Dieses Dokument ist für eine andere KI (oder eine spätere Sitzung von mir) gedacht,
die dieses Projekt ohne Rückfragen weiterführen soll. Lies es komplett, bevor du irgendetwas änderst.

> **Was sich am 06.09.2026 geändert hat — bitte zuerst lesen.**
> Es gibt jetzt **genau eine Kundenseite**. Die Trainer-Datei war bisher heimlich eine zweite:
> Sie begrüßte mit einem Türwähler („Zwei Seiten, ein System") und enthielt die komplette
> Mitgliederstrecke samt eigener Schein-Zahlung ein zweites Mal. Dieser Kundenweg ist **entfernt**
> (Türwähler, Rollenumschalter, `v-cust`, `v-active`, `#mitglied`-Einstieg, zweite Zahlung). Die
> Trainer-Datei ist jetzt reines Innenwerkzeug: Aufnahme, Programm, Ausdruck, Abrechnung.
> Auf der Kundenseite gibt es statt einem Produkt **drei** (399 € Programm, 60 €/Std. Personal
> Training, 40 €/Std. Begleitservice), alle Preise **brutto inkl. MwSt.**, und die Zahlung läuft
> über **Emilios eigene Bezahllinks** (Abschnitt 5a).
>
> **Nachtrag vom 07.09.2026:** Das GitHub-Repo `rebellmitherz/formkurve` ist jetzt live geschaltet
> (öffentlich) und **GitHub Pages ist die neue primäre Adresse** — nicht mehr der Claude-Artifact-Link.
> Der gedruckte QR-Code zeigt jetzt auf `https://rebellmitherz.github.io/formkurve/`. Lies **Abschnitt 3a**,
> bevor du an einer der beiden App-Dateien etwas änderst — der Veröffentlichungsweg hat sich geändert
> (`git push` statt Claude-Artifact-Republish).

---

## 1. Was das hier ist — in einem Absatz

„Formkurve" ist ein Verkaufswerkzeug für **Kadri B.**, einen angestellten Fitnesstrainer im
**HappyFit Dillingen** (Siemensstraße 8, 66763 Dillingen), gebaut von Emilio (dem Auftraggeber, nicht
Trainer). Kadri darf mit Erlaubnis seines Chefs eigene Zusatzleistungen an Studiomitglieder verkaufen
(Trainingspläne, Betreuung, 399 € / 8 Wochen, Aufteilung 70 % Trainer / 10 % Studio / 20 % System).
**Eine** Kundenseite (QR-Code im Studio → Gratis-Formcheck → Angebot → Termine → Zahlung) und
**ein** Innenwerkzeug für Kadri, das kein Kunde je zu sehen bekommt. Verkauft werden drei Dinge:
das 8-Wochen-Programm für 399 €, Personal Training für 60 € die Stunde und Begleitservice für
40 € die Stunde. **Noch keine Speicherung, kein Server, keine Benachrichtigung** — und die
Bezahllinks sind noch nicht eingetragen, solange läuft der Kauf im Demo-Modus. Für echten
Betrieb fehlt weiterhin einiges (siehe Abschnitt 8).

---

## 2. WICHTIG: Der Projektordner wandert ständig

Er wurde in dieser Konversation **dreimal verschoben**, ohne dass ich es veranlasst habe:
`Desktop\fitness-trainer-system` → `Desktop\01_PRODUKTE\fitness-trainer-system` →
**`Desktop\06_NETZWERK\Kadin\fitness-trainer-system`** (aktueller Stand).

**Verlasse dich nie auf einen Pfad aus einer alten Notiz.** Suche zu Sitzungsbeginn immer neu:
```
find "C:/Users/micha/Desktop" -maxdepth 4 -name "formkurve-mitglied-einstieg.html" 2>/dev/null
```
Dieses Dokument liegt **im Projektordner selbst** (`UEBERGABE.md`, eine Ebene über `prototype/`), damit es
mitwandert.

---

## 3. Die Dateien

```
fitness-trainer-system/
├── UEBERGABE.md                    ← dieses Dokument
├── STRATEGIE_2026-08-01.md         ← ursprüngliche Markt-/Produktstrategie (63 KB, historisch)
└── prototype/
    ├── formkurve-mitglied-einstieg.html   ← DIE KUNDENSEITE (aktuell, ~1,8 MB)
    │                                        die einzige Seite, die ein Mitglied je sieht
    ├── formkurve-komplett.html            ← INNENWERKZEUG für Kadri (aktuell, ~1,9 MB)
    │                                        enthält seit 06.09.2026 KEINEN Kundenweg mehr
    ├── formcheck-prototyp.html            ← alt, nicht mehr pflegen
    ├── formkurve-demo.html                ← alt, nicht mehr pflegen
    ├── formkurve-engine.html              ← alt, nicht mehr pflegen
    ├── formkurve-showroom.html            ← alt, nicht mehr pflegen
    ├── formkurve-trainer-app.html         ← alt, nicht mehr pflegen
    └── trainer-seite.html                 ← alt, nicht mehr pflegen
```

Zusätzlich, **nicht** im Projektordner:
- `Desktop\03_WEBSITES\Formkurve-Aushang-QR.html` + `.pdf` — druckfertiges A4-Poster mit QR-Code, das im
  Studio hängen soll. Enthält einen selbst geschriebenen QR-Encoder (Byte-Modus, ECC L). Zeigt seit
  07.09.2026 auf die GitHub-Pages-Adresse (Abschnitt 3a) — **vor jedem (Neu-)Druck prüfen, dass Pages
  tatsächlich live ist**, sonst zeigt der gedruckte Code auf eine 404-Seite.

### 3a. Wo die App tatsächlich läuft — Stand seit 07.09.2026

**GitHub Pages ist jetzt die primäre, laufende Adresse — nicht mehr der Claude-Artifact-Link.** Emilio
hat sich bewusst dafür entschieden, die Adresse selbst zu besitzen statt an eine Claude-Artifact-ID
gebunden zu sein (die Artifact-„Shared version"-Falle unten war ein Auslöser dafür).

```
fitness-trainer-system/
├── index.html                 ← NEU: reine Weiterleitung → prototype/formkurve-mitglied-einstieg.html
│                                  Ziel des QR-Codes: https://rebellmitherz.github.io/formkurve/
└── trainer/
    └── index.html              ← NEU: reine Weiterleitung → prototype/formkurve-komplett.html
                                    https://rebellmitherz.github.io/formkurve/trainer/
```

Diese beiden Dateien enthalten **keinen eigenen Inhalt**, nur `<meta http-equiv="refresh">` +
`location.replace()` auf die echte Datei in `prototype/`. Grund: Die App-Dateien selbst (~1,8 MB, Fotos
als Base64 eingebettet) bleiben an einer einzigen Stelle — sie hier zu duplizieren hieße, bei jeder
Änderung zwei Kopien pflegen zu müssen.

**Workflow ab jetzt bei jeder Änderung an einer der beiden App-Dateien:**
```
git add -A && git commit -m "..." && git push
```
GitHub Pages baut automatisch aus dem `main`-Branch neu — normalerweise binnen 1–2 Minuten sichtbar.
**Kein manueller Veröffentlichungsschritt mehr nötig**, anders als beim Claude-Artifact-Weg unten.

| Was | Adresse |
|---|---|
| **Kundenseite** (Ziel des QR-Codes) | `https://rebellmitherz.github.io/formkurve/` |
| Innenwerkzeug für Kadri (nie an Kunden geben) | `https://rebellmitherz.github.io/formkurve/trainer/` |
| Quelltext (Versionsverwaltung, privat lesbar für jeden — Repo ist **öffentlich**) | `https://github.com/rebellmitherz/formkurve` |

**GitHub Pages muss einmalig manuell eingeschaltet werden** (Repo → Settings → Pages → Source: „Deploy
from a branch" → Branch `main`, Ordner `/ (root)` → Save) — das kann keine KI für Emilio anklicken, weil
das eine Einstellung in seinem eigenen GitHub-Konto ist, nicht ein Git-Befehl.

**Warum GitHub Pages und nicht Vercel:** Die App ist eine reine statische Datei ohne Server, ohne
Build-Schritt — genau dafür ist GitHub Pages gemacht, kostenlos, ohne zusätzliches Konto. Vercel lohnt
sich erst, wenn eines der offenen Punkte aus Abschnitt 8 ein echtes Backend braucht (Speicherung,
Termin-Sperre, Benachrichtigung an Kadri) — das kann GitHub Pages grundsätzlich nie, weil es für immer
rein statisch bleibt.

### Veröffentlichte Artifact-Links (Claude-Artifacts — jetzt Backup/Zweitversion, nicht mehr das QR-Ziel)

| App | Artifact-URL |
|---|---|
| Kundenseite | `https://claude.ai/code/artifact/6b8bbca2-d114-48ce-9d3b-e71749374447` |
| Innenwerkzeug für Kadri | `https://claude.ai/code/artifact/a1f9a8dc-4e44-4988-b6de-7c2eea3bf0ea` |

Diese Links funktionieren weiterhin, sind aber **nicht mehr das Ziel des gedruckten QR-Codes** — nur noch
eine zweite, unabhängige Kopie. Sie laufen aus dem Gleichschritt, sobald `prototype/`-Dateien geändert
und nur nach GitHub gepusht (nicht auch als Artifact neu veröffentlicht) werden — das ist jetzt in
Ordnung so, muss aber bewusst sein, falls doch mal jemand diesen Link herausgibt.

Falls doch noch veröffentlicht wird: Beim Veröffentlichen **immer** `url:` mit der bestehenden ID
angeben, sonst entsteht eine neue, andere URL.

**Bekannte Support-Falle (Claude-Artifacts):** Im Teilen-Dialog gibt es zwei getrennte Einstellungen —
„General access" (wer darf zugreifen) und „Shared version" (welcher Snapshot wird angezeigt). Ein
Betrachter kann trotz korrekter Freigabe eine wochenalte Version sehen, wenn „Shared version" auf eine
feste Nummer statt „Latest" steht. Genau das ist am 07.09.2026 beim Innenwerkzeug passiert — ein Grund
mehr, warum GitHub Pages jetzt die primäre Adresse ist: dort gibt es diese Falle nicht.

---

## 4. Architektur-Grundregel: eine Kundenseite, ein Innenwerkzeug

Beide HTML-Dateien sind **vollständig eigenständig** (kein Build-Schritt, kein Import, alles inline —
die Artifact-CSP blockt externe Ressourcen).

**Die wichtigste Regel: Es darf nur eine Seite geben, die ein Kunde sieht.** Die Kundenstrecke
existiert ausschließlich in `formkurve-mitglied-einstieg.html`. In der Trainer-Datei gab es sie bis
zum 06.09.2026 ein zweites Mal — mit eigener Zahlung, eigenen Texten, eigenen Preisen, die
auseinanderliefen. Wer sie dort wieder einbaut, hat zwei Kundenseiten und zwei Wahrheiten.

Was **weiterhin doppelt** in beiden Dateien liegt und bei jeder Änderung identisch nachgezogen
werden muss:

1. **`calc()`** — der komplette Rechenkern (BMR, Kalorien, Makros, TF/TT-Split, 8-Wochen-Prognose)
2. **Die Übungs-Zeichenschicht / Fotos / Muskelkarte** — `EXIMG`, `CHOUT_F/B`, `CHFRONT/BACK`, `muscleChart2()`
3. **Die 34-Übungen-Zuordnung** (`EX`, `dayPlan()`, `buildDays()`)

Das Werkzeug braucht diese drei für Dossier und Ausdruck, die Kundenseite für die App — deshalb
bleiben sie doppelt. Es gibt Prüfskripte, die das automatisch nachrechnen (Abschnitt 9). **Nach jeder
Änderung an einer der drei Stellen: die Skripte laufen lassen, bevor du veröffentlichst.**

**Preise gehören an genau eine Stelle:** das `PRODUCTS`-Objekt in der Kundenseite (Abschnitt 5a).
Vorher standen die 399 € an vier Stellen im Markup und die Umsatzsteuer als feste Zahl `63,71 €`
daneben — bei jeder Preisänderung ein Suchspiel mit sicherem Rest.

---

## 4a. Produkte, Preise und Bezahllinks (Kundenseite)

Alles steht oben im JS-Block der Kundenseite, direkt vor `showOffer`:

```js
var PAY={prog:'',pt:'',beg:''};          // <- hier kommen Emilios Bezahllinks rein
var PRODUCTS={
  prog:{ price:399, hours:false, ... },  // 8-Wochen-Transformation, einmalig
  pt:  { price:60,  hours:true,  ... },  // Personal Training, pro Stunde
  beg: { price:40,  hours:true,  ... }   // Begleitservice, pro Stunde
};
```

**Preise sind Bruttopreise, inklusive Mehrwertsteuer.** Es wird bewusst **kein Steuerbetrag einzeln
ausgewiesen** — auf der Seite steht nur „inkl. MwSt.". Die frühere Zeile „enthaltene USt. (19 %)
63,71 €" ist ersatzlos raus. Die Rechnung schreibt Kadri über sein eigenes Werkzeug.

**Bezahllinks eintragen:** Solange ein Eintrag in `PAY` leer ist, läuft der Kauf im Demo-Modus —
kein Geld, kein Sprung nach außen, die ganze Strecke bleibt testbar, und die Seite zeigt selbst den
Hinweis „Demo · Testmodus". Sobald ein Link drinsteht, führt der Bezahlknopf dorthin und der
Demo-Hinweis verschwindet von allein. Es ist **kein weiterer Code nötig**.

- Bei den Stundenprodukten im Bezahllink die **Menge anpassbar** machen. Wer die Stundenzahl direkt
  übergeben will, schreibt `{n}` in den Link (`https://…/pt?quantity={n}`) — `{n}` wird durch die
  gewählte Stundenzahl ersetzt.
- Die Seite hängt zusätzlich `&fk=<produkt>-<stunden>` an, damit in der Zahlung erkennbar ist, was
  gebucht wurde (z. B. `fk=beg-3`).
- Als **Erfolgs-URL** im Bezahllink die Kundenseite mit `?bezahlt=1` eintragen. Dann zeigt sie beim
  Zurückkommen sofort die Bestätigung mit den gewählten Terminen, statt wieder bei null anzufangen.
  Das funktioniert über `sessionStorage` (`fk_order`); schlägt der Speicher fehl (privates Fenster),
  geht der Kauf trotzdem durch, nur die Bestätigung fehlt.

### Die zwei Wege durch die Seite

| | 8-Wochen-Programm | Personal Training / Begleitservice |
|---|---|---|
| Einstieg | Formcheck → Auswertung → Angebot | Angebot direkt vom Startbildschirm („Nur eine Stunde buchen") |
| Termine | `v-sched`: so viele feste Wochenzeiten wie Trainingstage, erste ist die Kleingruppe | `v-book`: Stundenzahl wählen, dann ein Termin je Stunde |
| Zahlung | `v-pay` | `v-pay` |
| Danach | Bestätigung → 8-Wochen-App (Training, Ernährung, Fortschritt) | Bestätigung, **keine App** |

**Reihenfolge ist bewusst: erst Termine, dann Zahlung.** Vorher wurde zuerst bezahlt und danach der
Termin gewählt — das geht nicht mehr, sobald die Zahlung die Seite verlässt. So ist der Bezahlknopf
der letzte Schritt und der Absprung nach außen unkritisch.

Das Terminraster gibt es **nur einmal** (`drawGrid`, `pickSlot`, `renderPicked`); `SCHED` sagt, in
welchen Behälter gezeichnet wird und wie viele Termine erlaubt sind. Nicht kopieren, wenn ein
dritter Anwendungsfall dazukommt — `SCHED` erweitern.

---

## 5. Der Rechenkern (`calc()`) — im Detail

```js
function calc(){
  var bmr = sex==='m' ? 10*kg+6.25*cm-5*age+5 : 10*kg+6.25*cm-5*age-161;      // Mifflin-St Jeor
  var tdee = bmr * {2:1.375,3:1.46,4:1.55,5:1.64}[days];                      // Aktivitätsfaktor

  // Kalorienziel je nach Ziel:
  //   ab (Abnehmen)      → max(bmr*1.1, tdee*0.80)   Defizit, pr=2.0 g/kg
  //   mu (Muskelaufbau)  → tdee*1.10                 Überschuss, pr=1.8 g/kg
  //   sonst (fit/ru)     → tdee                      Erhalt, pr=1.6 g/kg

  // Referenzgewicht: ab BMI 27 zählt nur 1/4 des Übergewichts (sonst absurde
  // Eiweißmengen bei schweren Personen — war ein echter Bug, jetzt gefixt):
  //   kg27 = 27 * (cm/100)²
  //   refKg = kg > kg27 ? kg27 + 0.25*(kg-kg27) : kg
  var pg = round(pr * refKg);           // Eiweiß
  var fg = round(0.8 * refKg);          // Fett
  var cg = max(60, round((kcal-pg*4-fg*9)/4));   // Kohlenhydrate, Wochenschnitt

  // Trainingstag/Ruhetag-Split: eine Einheit kostet ~5 kcal/kg zusätzlich.
  // Eiweiß+Fett bleiben an beiden Tagen gleich, nur Kohlenhydrate tragen den
  // Unterschied ("Carb Cycling um die Einheit herum").
  var burn = 5 * kg;
  var kcalTF = max(bmr*1.05, kcal - burn*days/7);   // Sicherheitsboden: nie unter Grundumsatz
  var kcalTT = kcalTF + burn;
  var cgTF = max(60, round((kcalTF-pg*4-fg*9)/4));
  var cgTT = max(60, round((kcalTT-pg*4-fg*9)/4));

  // 8-Wochen-Prognose (Daumenregel, unabhängig von kcal):
  //   ab  → kg * (1 - 0.006*8)
  //   mu  → kg + (exp=='a' ? 0.22 : 0.13) * 8
  //   fit → kg * (1 - 0.003*8)
  //   ru  → kg (stabil)

  return { bmr, tdee, kcal, dir, pg, fg, cg, kcalTF, kcalTT, cgTF, cgTT, burn,
           start:kg, end, delta };
}
```

**Verifiziert:** über 15.360 Profil-Kombinationen (Ziel × Geschlecht × Tage × Gewicht × Größe × Alter ×
Erfahrung) liefern beide Dateien byte-identische Ergebnisse. Prüfskript: `cross-check.js` (Abschnitt 7).

---

## 6. Ernährungsplan-Engine

- 4 Slots: `fruh` (25 %), `mittag` (35 %), `abend` (30 %), `snack` (10 %) — Anteile am Tages-kcal.
- `slotTargets(kcalDay, cgDay)` verteilt Eiweiß/Fett/Kohlenhydrate proportional zum Kalorienanteil —
  dadurch stimmen die Slot-Summen **exakt** mit dem Tagesziel überein (Konstruktionsgarantie, kein Runden).
- `MEALDB`: 5–6 Rezepte je Slot, jeweils mit Basis-kcal/p/f/c, Zutaten, Zubereitungshinweis.
- `pickMeals()`: bewertet jedes Rezept mit `macroFit()` — Abstand der Makro-Kalorienanteile zum Ziel,
  Eiweiß doppelt gewichtet. **Diese Funktion wurde in der letzten Sitzung erweitert** (vorher nur
  Eiweiß-Dichte, dadurch drifteten Fett/Kohlenhydrate bei ~40 % der Profile stark).
- Die 3 besten Treffer werden als „Möglichkeit 1/2/3" gezeigt, mit `scaleOption()` auf das Slot-Ziel
  skaliert (Portionsfaktor auf 0,55–1,75 begrenzt — keine unrealistischen Mengen).
- **Bekannte, akzeptierte Grenze (kein Bug):** Mit nur 5–6 Rezepten je Slot lässt sich nicht jede
  Nährstoffverteilung treffen. Kalorien/Eiweiß sind zuverlässig genau (>97 % der Fälle <50 kcal Abweichung),
  Fett/Kohlenhydrate weichen bei einem Teil der Profile spürbar ab. Das ist im UI ehrlich ausgewiesen
  („+20 g mit Möglichkeit 1"). **Abhilfe:** Rezeptzahl je Slot auf 10–12 erhöhen — fachlich sollte das
  Kadri absegnen, nicht die KI allein erfinden.
- Einkaufsliste: aggregiert „Möglichkeit 1" je Slot, gewichtet nach echter Trainings-/Ruhetag-Verteilung
  (`P.days` Trainingstage, `7-P.days` Ruhetage).

Prüfskripte: `check-tftt.js` (4.608 Profile, TF/TT-Invarianten), `check-macros.js` (Abweichungsgrößen),
`check-clamp.js` (wie oft die Portionsgrenze greift).

---

## 7. Übungssystem: Fotos + Muskelkarte (wichtigster Abschnitt für Grafik-Arbeit)

### 7.1 Die Vorgeschichte, die du NICHT wiederholen sollst

Es gab **fünf gescheiterte Anläufe**, eine Trainingsfigur prozedural aus Gelenkpunkten zu zeichnen
(Kapseln → Anatomieprofile → Schattierung → Muskelregionen → durchgehende Kontur per
Rand-hinter-Füllung-Trick). Jeder Schritt war objektiv besser als der vorige. Das Ergebnis blieb eine
Gliederpuppe. Emilios Urteil, mehrfach: „sieht scheiße aus" / „sieht furchtbar aus" — **berechtigt**.

**Lehre: Versuche nicht, einen Menschen oder eine Muskelkarte selbst mit SVG-Pfaden zu zeichnen.**
Das SVG-Zeichensystem existiert noch im Code als Rückfallebene (`drawBody()`, `POSE`-Tabelle mit
19 Bewegungen), aber es wird **nicht mehr für die Anzeige benutzt** — siehe 7.2.

### 7.2 Was tatsächlich funktioniert hat — zwei externe, lizenzfreie Quellen

**A) Echte Übungsfotos** — Quelle: `github.com/yuhonas/free-exercise-db`
(**Unlicense / Public Domain**, 873 Übungen, je Start-/Endfoto).
- 34 deutsche Übungsnamen **von Hand** auf Datensatz-IDs gemappt (automatische Namenssuche lag mehrfach
  fachlich falsch, z. B. „Schulterdrücken Maschine" → „Calf-Machine Shoulder Shrug").
- 66 Bilder geladen, mit ffmpeg auf 420 px Breite verkleinert (`-vf scale=420:-2 -q:v 6`), als Base64
  eingebettet in `var EXIMG={...}` (vor `var POSE=`).
- Anzeige: `.exPhoto` mit zwei übereinanderliegenden `<img>`; `playAnim()` setzt
  `exImg1.style.opacity = st.t` (Bewegungsphase) und den Text von `#exTag` zwischen „Start"/„Endposition".
- **Rechtlicher Vorbehalt an Emilio kommuniziert:** Die Sammlung erklärt sich als Public Domain, die
  Fotos wirken aber professionell aufgenommen — nicht unabhängig prüfbar, ob der Fotograf wirklich
  freigegeben hat. Für Vorführungen unkritisch, **vor kommerzieller Nutzung klären**. Alternative:
  `wrkout.xyz` (kommerziell lizenziert, 2.500+ Übungen, 10.000+ Bilder mit eingefärbter Muskulatur,
  3.500+ Videos — exakt Emilios ursprüngliche Referenz-Optik).

**B) Echte Muskelkarte** — Quelle: `github.com/HichamELBSI/react-native-body-highlighter`
(**MIT-Lizenz**, Copyright © 2022 ELABBASSI Hicham; gefunden über dessen Fork
`eslamelfateh/react-native-body-parts-anatomy`, der die Herkunft in `THIRD_PARTY_NOTICES.md` offenlegte).
- Anatomisch korrekte SVG-Körperkontur, Vorder- und Rückansicht **liegen im Quellmaterial bereits
  nebeneinander** (viewBox effektiv `0 0 1448 1460`; vorne x 0–724, hinten x 724–1448 — kein Verschieben
  nötig).
- Einzelne Muskelgruppen-Pfade (chest/abs/quadriceps/gluteal/upper-back/…) separat extrahiert.
- **Extraktions-Falle:** Die Pfade beginnen als `M272.91` **ohne Leerzeichen** nach dem `M`, nicht
  `M 272.91`. Eine Regex mit `M ` (Leerzeichen) liefert **still 0 Treffer** — kein Fehler, keine
  Exception, einfach leere Arrays. Kostete eine ganze Debug-Runde.
- Eingebaut als `CHOUT_F`, `CHOUT_B`, `CHFRONT`, `CHBACK`, `CHNAME` (deutsche Namen) +
  `muscleChart2(key, COL)`. Übungs→Muskel-Zuordnung in `CHART2` (primär/sekundär je der 19
  Bewegungs-Keys, nicht je der 34 Übungsnamen).
- **Lizenzhinweis steht als Kommentar im Code beider Dateien** (MIT verlangt das) — nicht entfernen.
- Farbtoken: `--figSkin`, `--figInk`, `--figPrim`, `--figSec`, `--figLbl`.

### 7.3 Qualität, aktuell

Beide Apps: 20/20 Übungszeilen mit Foto **und** Muskelkarte **und** mindestens einer eingefärbten
Muskelregion, 0 Fehler (Prüfskript-Ergebnis). Das ist der aktuelle Qualitätsstand — anatomisch korrekte
Silhouette, echte Fotos, keine Handzeichnung mehr sichtbar für den Nutzer.

---

## 8. Offene Punkte (Emilio kennt sie, hier zur Vollständigkeit)

**Rechtlich/organisatorisch — blockieren echten Betrieb, nicht die Demo:**
1. Schriftliche Erlaubnis vom Studio-Chef für Kadri (Vorbedingung für alles Weitere)
2. Bildrechte der Übungsfotos klären, oder wrkout.xyz-Lizenz besorgen
3. Kadris echte Trainingszeiten (aktuell Platzhalter im `TIMES`-Objekt)
4. Datenschutzhinweis fehlt (Gesundheitsdaten: Gewicht, Alter, Ziel werden abgefragt)
5. HappyFit-Markennutzung braucht explizite Studio-Zustimmung für den Echtbetrieb (aktuell als
   „Konzeptentwurf … keine offizielle Anwendung von HappyFit" gekennzeichnet)

**Technisch — für ein echtes Produkt, nicht nur Demo:**
6. **Keine Speicherung.** Tab zu → alles weg. Keine Datenbank. Bei Stundenbuchungen wiegt das
   schwerer als beim 399er: Kadri erfährt sonst nie, dass jemand gebucht hat.
7. **Keine Benachrichtigung an Kadri.** Bei einer Stundenbuchung der wichtigste fehlende Teil:
   wer, wann, was. Die Seite sagt dem Kunden „Kadri hat deine Buchung" — das stimmt erst, wenn
   dieser Weg existiert. **Bis dahin muss Kadri jede Buchung über die Zahlung mitbekommen**
   (deshalb hängt `fk=<produkt>-<stunden>` am Bezahllink).
8. **Bezahllinks noch nicht eingetragen** (`PAY` in Abschnitt 5a). Bis dahin Demo-Modus.
9. **Keine echten Verfügbarkeiten.** `TIMES` ist Platzhalter, und nichts sperrt einen Slot:
   zwei Leute können denselben Termin buchen. Beim 399er einmalig ärgerlich, bei Stundenbuchungen
   ein Dauerproblem.
10. **Keine Nutzerkonten.**
11. Hosting-Entscheidung offen (Domain, Backend-Anbieter) — Voraussetzung für 6, 7, 9, 10. Eine
    Artifact-URL ist kein Ort für echte Zahlungen (und hat die „Shared version"-Falle aus Abschnitt 3).
12. **Die Abrechnung im Werkzeug kennt nur die 399 €.** Die Aufteilung 70/10/20 und der Monatswert
    im Kopf rechnen ausschließlich mit dem Programmpreis. Für die Stundenprodukte ist die
    Aufteilung **nicht festgelegt** — das ist eine Absprache zwischen Emilio, Kadri und dem Studio,
    keine Sache, die eine KI erfinden darf.
13. Ernährungsplan-Genauigkeit: 10–12 statt 5–6 Rezepte je Slot würden Fett-/Kohlenhydrat-Drift senken
    (Abschnitt 6) — Kadri sollte die Rezepte fachlich absegnen.

---

## 9. Prüfwerkzeuge — unbedingt vor jeder Veröffentlichung laufen lassen

Alle Skripte liegen im `scratchpad`-Ordner der jeweiligen Sitzung (sitzungsspezifisches Temp-Verzeichnis,
**existiert in einer neuen Sitzung nicht mehr** — müssen bei Bedarf neu geschrieben werden, sind aber
unten so beschrieben, dass sie in Minuten rekonstruierbar sind).

### 9.1 `cross-check.js` (Node) — Rechenkern-Abgleich
Extrahiert `calc()` per String-Suche (`indexOf('function calc(){')` bis zum Ende der Return-Zeile) aus
beiden HTML-Dateien, baut sie per `new Function()` nach, vergleicht Ausgaben über tausende
Profil-Kombinationen. Muss **0 Abweichungen** liefern.

### 9.2 `check-ex.js` (Node) — Erreichbarkeit aller 34 Übungen
Extrahiert `EX`/`dayPlan`/`buildDays`, prüft über alle Ziel×Tage-Kombinationen, dass jede der 34
benannten Übungen in mindestens einem generierten Plan vorkommt. **War schon einmal kaputt** (Formel
`pool[(i+j+t)%pool.length]` erreichte 2 von 34 nie — gefixt zu `pool[(i+j+P.days+t)%pool.length]`).

### 9.3 `check-tftt.js`, `check-macros.js`, `check-clamp.js` (Node) — Ernährungsplan
Prüfen Invarianten (TT immer ≥ TF, Ruhetag nie unter Grundumsatz, Slot-Summen exakt), Abweichungsgrößen
und wie oft die Portionsgrenze (0,55–1,75) greift.

### 9.4 Der wichtigste Fund dieser Sitzung: **headless Edge kann tatsächlich screenshotten**

Der Browser-Pane rendert Dateien außerhalb des Projektordners nur als **statisches Standbild** —
monatelang fälschlich für „ich kann meine eigene Grafik nicht sehen" gehalten. Tatsächlicher Weg:

```bash
msedge.exe --headless=new --disable-gpu --window-size=B,H --screenshot=out.png file:///pfad/zur/datei.html
```

Für Zustände **tief im Klickpfad** (z. B. „Übungsblatt nach komplettem Formcheck-Durchlauf"):
1. Eine Kopie der HTML-Seite bauen mit vorangestelltem `<script>`, das `window.setTimeout` auf ein
   Minimum klemmt (`Math.min(ms,2)`), sowie ein Treiberskript, das den Klickpfad programmatisch
   durchklickt (Chat-Antworten, Buttons) und am Ziel `document.body.setAttribute('data-ready','1')` setzt.
2. `--virtual-time-budget=15000` mitgeben, damit die Zeitklemme greifen kann.
3. Für **Messwerte statt Bild**: `--dump-dom` statt `--screenshot`, Werte vorher in
   `document.body.setAttribute('data-log', ...)` schreiben, danach mit `grep -o 'data-log="[^"]*"'`
   auslesen.

**Zwei Fallstricke dabei:**
- **Hochzähl-Animationen** (`countUp()` nutzt `requestAnimationFrame`) zeigen im Screenshot
  Zwischenwerte statt Endwerte, wenn nur `setTimeout` geklemmt wird. Zusätzlich `requestAnimationFrame`
  kapern: sofort mit weit in der Zukunft liegendem Zeitstempel feuern lassen.
- **Kontrastmessungen** während laufender CSS-Übergänge (`transition`) liefern absurd falsche Werte,
  weil `background` bei Verläufen sofort springt, `color` aber noch mitten in der Überblendung steckt.
  Immer `*{transition:none!important}` setzen, bevor gemessen wird.
- **Echte Handy-Breite testen:** `--window-size` bei headless Edge setzt NICHT zuverlässig den
  CSS-Layout-Viewport für lokale Dateien. Lösung: die App in einen `<iframe fixed-width>` innerhalb
  einer Außenseite laden; Ergebnisse per `postMessage` nach außen melden (direkter
  `contentDocument`-Zugriff scheitert an der `file://`-Origin-Sperre).

### 9.5 Kontrast-Audit
WCAG-Luminanz-Formel, komponiert Text über die tatsächliche (ggf. mehrschichtige/Verlaufs-)
Hintergrundfarbe. Aktueller Stand: 190 einzigartige Farbkombinationen geprüft, 0 Fehler.

---

## 10. Fünf Layout-/Logikfehler, die in der letzten Sitzung gefunden und behoben wurden

Falls du künftig ähnliche Symptome siehst — das sind die Klassen von Fehlern, die in diesem Projekt
wiederholt aufgetreten sind:

1. **Reiterleiste scrollte weg.** `.app` hatte nur `min-height:100vh`, wuchs mit dem Inhalt. Fix:
   `height:100vh; height:100dvh` (dvh berücksichtigt die Adressleiste am Handy), `.body` scrollt intern.
2. **UTF-8-BOM am Dateianfang** (alle drei Dateien betroffen, Überbleibsel aus PowerShell-Bearbeitungen).
   Erzeugte einen unsichtbaren Textknoten, der als leere Zeile gerendert wurde → 23 px toter Streifen,
   alles darunter verschoben, Reiterleiste angeschnitten. **Immer prüfen:** `head -c 3 datei.html | xxd -p`
   sollte NICHT `efbbbf` zeigen.
3. **Inline-Labels klebten zusammen** (`.mealTx .mt`/`.mn` ohne `display:block`).
4. **Widersprüchliche Kalorienzahlen zwischen Ansichten** — der „Heute"-Reiter zeigte den
   Wochendurchschnitt, der Ernährungsplan den Trainingstag-Wert, für denselben Tag. Klasse von Fehler:
   **beim Einbau eines neuen Konzepts (hier: TF/TT-Split) alle Stellen finden, die den alten
   Einzelwert benutzt haben** — nicht nur die offensichtlichste.
5. **`.rise`-Animation mit `opacity:0` als Grundzustand.** Läuft die Animation aus irgendeinem Grund
   nicht (ist in diesem Projekt schon **zweimal** mit `requestAnimationFrame`/`IntersectionObserver`
   passiert), bleibt der Inhalt unsichtbar statt nur unanimiert. **Grundregel für dieses Projekt:**
   Animationen dürfen nie der einzige Weg sein, wie Inhalt sichtbar wird — der Grundzustand muss immer
   der sichtbare Endzustand sein, Animation nur additiv (`backwards`/`forwards` entsprechend wählen).

---

## 11. Wenn du weiterarbeitest — Checkliste

1. Projektordner **neu suchen**, nicht auf einen Pfad aus einer Notiz verlassen.
2. Vor Änderungen an `calc()`, der Übungszuordnung oder der Fotos/Muskelkarte: Sicherungskopien anlegen.
3. Änderungen **in beiden HTML-Dateien identisch** durchführen.
4. Nach jeder Änderung: die drei Node-Prüfskript-Familien (Rechenkern, Übungen, Ernährung) neu bauen
   und laufen lassen — Abschnitt 9.1–9.3.
5. Optisch etwas geändert? **Nie behaupten, es zu sehen, ohne headless Edge zu benutzen** — Abschnitt 9.4.
   Kontrast danach neu prüfen, mit `transition:none`.
6. Vor dem Veröffentlichen: `head -c 3` auf BOM prüfen (Abschnitt 10, Punkt 2).
7. Veröffentlichen **immer mit der bestehenden `url:`**, nie ohne — sonst neue ID, alter QR-Code tot.
8. Datei-Encoding beim Bearbeiten: UTF-8 **ohne BOM**. Bei PowerShell-Edits besonders vorsichtig sein,
   das war die Quelle des BOM-Problems.

---

## 12. Kontext, den du sonst nirgendwo findest

- Emilios E-Mail: `rebellmitherz@gmail.com`
- Der Verkaufsmechanismus, den Emilio explizit wollte: **nicht** dem Studio-Chef aktiv etwas vorführen
  (Kadri kann/will das nicht) — das Werkzeug soll Kadri sofort nützen, und der Chef soll es *beiläufig*
  sehen und von sich aus auf Emilio zukommen. Das prägt viele Designentscheidungen (z. B. warum die
  Trainer-App wie ein fertiges Produkt wirken muss, nicht wie ein Pitch-Deck).
- Emilios Ansage vom 06.09.2026, wörtlich: „**Zahlungen nur über mein Tool**" und „die Preise sind
  immer inklusive Mehrwertsteuer". Deshalb baut die Seite keine eigene Zahlung mehr nach, sondern
  führt an Emilios Bezahllinks — und weist nirgends einen Steuerbetrag getrennt aus.
- Frühere, inzwischen überholte Kritikpunkte von Emilio, die zum jetzigen Stand geführt haben:
  „zu wenig wow", „sehr billig gestaltet", „diese Strichmännchen sind echt billig", „sieht furchtbar
  aus" — jedes Mal berechtigt, jedes Mal zu einer echten Verbesserung geführt (nicht zu Kosmetik).
  Nimm neue Kritik in diesem Ton ernst und wörtlich, nicht als vage Stimmung.
