# Wortarten-Trainingskampf 🧑‍🎓🤖  
Interaktives Spiel zu Nomen, Verben, Adjektiven, Pronomen und Partikeln

Dieses Projekt ist ein kleines Browser-Spiel für die Primarschule, mit dem Schülerinnen und Schüler Wortarten trainieren können – im **Trainingsmodus** oder als **Wettkampf gegen einen „Roboter“**.  
Es ist so gebaut, dass es als **externe interaktive Ressource in LearningView** eingebettet werden kann und bei Erfolg automatisch als erledigt markiert wird.

---

## Inhalt

- `index.html` – komplette App (HTML, CSS, JavaScript)
- `audio/` – Ordner für Soundeffekte (WAV-Dateien)
  - `correct.wav` – richtiges Wort (Coin-Sound)
  - `error.wav` – falsches Wort / Zeit abgelaufen
  - `roundwon.wav` – Runde gewonnen (Schüler)
  - `roundlost.wav` – Runde verloren (Roboter)
  - `gamewon.wav` – Match gewonnen
  - `youwon.wav` – „Du gewinnst den Mathe-Kampf!“
  - `gamelost.wav` – Match verloren

> **Wichtig:** Der Ordner muss exakt `audio` heissen und im gleichen Verzeichnis wie `index.html` liegen.

---

## Spiellogik & Features

### Wortarten

Das Spiel nutzt Wortlisten für fünf Wortarten (alle Wörter sind intern klein geschrieben):

- **Nomen** (z. B. `haus`, `baum`, `kind`, `schule`, `freund`, `winter`, …)
- **Verben** (z. B. `gehen`, `spielen`, `lesen`, `öffnen`, `schließen`, …)
- **Adjektive** (z. B. `groß`, `klein`, `schnell`, `fröhlich`, `gefährlich`, …)
- **Pronomen** (z. B. `ich`, `du`, `wir`, `mein`, `dieser`, `niemand`, …)
- **Partikeln** (Adverbien, Konjunktionen, Präpositionen, Modal- und Gradpartikeln usw.)

Ein Wort wird zufällig aus allen Listen gezogen und groß in der Mitte angezeigt.  
Die Schüler wählen dazu die passende Wortart über farbige Buttons:

- **Nomen** – braun  
- **Verb** – blau  
- **Adjektiv** – gelb  
- **Pronomen** – orange  
- **Partikel** – grün  

### Umlaute & ß → Anzeige

Im Code können Wörter sowohl mit `ä, ö, ü, ß` als auch in „technischer“ Form `ae, oe, ue` gespeichert sein.  
Für die Anzeige werden sie automatisch umgewandelt:

- `ae → ä`  
- `oe → ö`  
- `ue → ü`  
- `ß → ss` (Schweizer Doppel-S)

Die Kinder sehen also immer die **korrekte Schreibweise** (z. B. „fröhlich“, „Straße“, „groß“ → „gross“).

---

## Modi / Schwierigkeitsgrade

Beim Start wählen die Schüler den **Modus**:

- 🟢 **Training**  
  - **Kein Timer**, kein Wettkampf  
  - Nur: Wort sehen → Wortart klicken → Feedback → nächstes Wort  
  - Gut zum Üben / Einstieg

- 🔵 **Wettkampf – 3 s pro Wort**  
- 🔵 **Wettkampf – 5 s pro Wort**  
- 🔵 **Wettkampf – 10 s pro Wort**  

In den drei Wettkampf-Modi läuft ein Timer:

- Wird rechtzeitig die richtige Wortart angeklickt → **richtige Antwort**
- Wird gar nicht geklickt oder falsch geklickt → **falsche Antwort** / **Zeit abgelaufen**

---

## Ringkampf / Gamification

Unten im Spiel ist eine **Ringkampf-Anzeige** mit:

- einem **Roboter 🤖** links  
- einem **Schüler-Icon 🧑‍🎓** rechts  
- einer Linie mit 9 Feldern und einem Marker in der Mitte

**Regeln:**

- Richtig → Marker geht **1 Schritt nach rechts**
- Falsch / Zeit abgelaufen → Marker geht **1 Schritt nach links**
- Wenn der Marker **4 Schritte nach rechts** erreicht → **Schüler gewinnt eine Runde** (Punkt für den Schüler)
- Wenn der Marker **4 Schritte nach links** erreicht → **Roboter gewinnt eine Runde**

Der Punktestand (Runden) wird oben angezeigt:

- `Du: X – Roboter: Y`

Sobald ein Spieler **3 Punkte** erreicht hat, ist der **Wettkampf vorbei**:

- Sieg → Fanfare + „Du gewinnst den Mathe-Kampf!“
- Niederlage → entsprechender Sound + Text

Im **Trainingsmodus** ist dieser Ringkampfblock ausgeblendet.

---

## Audio-Feedback

Es werden WAV-Dateien aus dem Ordner `audio/` abgespielt:

- **korrekte Antwort** → `correct.wav`
- **falsche Antwort / Zeit abgelaufen** → `error.wav`
- **Runde gewonnen** → `roundwon.wav`
- **Runde verloren** → `roundlost.wav`
- **Match gewonnen** → `gamewon.wav` + kurz später `youwon.wav`
- **Match verloren** → `gamelost.wav`

Hinweis:  
In manchen Browsern müssen die Schüler **einmal irgendwo klicken**, bevor Audio automatisch abgespielt werden darf (Autoplay-Regeln).

---

## Technische Hinweise

- Die App ist eine **reine HTML/CSS/JS-Datei** und läuft komplett im Browser.
- Alle Daten (Wortlisten, Spielstand) liegen nur im Speicher – es gibt **kein Login** und **keine Speicherung** von personenbezogenen Daten.
- Die App nutzt `window.parent.postMessage('AppSolved', '*');` um LearningView mitzuteilen, dass die Aufgabe erledigt ist.

---

## Deployment (z. B. GitHub Pages)

1. Repository mit mindestens:
   - `index.html`
   - `audio/` (mit deinen `.wav`-Dateien)
2. In GitHub im Repo:
   - **Settings → Pages**
   - Branch (z. B. `main`) und Ordner (z. B. `/root`) auswählen
   - Speichern → GitHub erzeugt eine URL, z. B.  
     `https://deinname.github.io/wortarten-ringkampf/`

Diese URL brauchst du für LearningView.

---

## Einbettung in LearningView

### 1. Lernauftrag vorbereiten

Erstelle in LearningView einen neuen Auftrag oder öffne einen bestehenden.  
Im **Arbeitsauftrag** (Textfeld für die Schüler) kannst du z. B. schreiben:

> **Auftrag:**  
> 1. Wähle im Spiel zuerst den Modus (Training oder Wettkampf mit Zeit).  
> 2. Bestimme jeweils die Wortart des angezeigten Wortes.  
> 3. Spiele im Wettkampfmodus so lange, bis du den Roboter **dreimal besiegt** hast.  
> 4. Kehre dann zu LearningView zurück.  
>  
> Du kannst die Wortarten zuerst im **Trainingsmodus** ohne Timer üben.  
> Entscheide selber, ob du später **3 s, 5 s oder 10 s** pro Wort wählst.

Hinweis:  
Die Auswahl von Modus/Schwierigkeit erfolgt **im Spiel**, nicht im Auftrag.  
Klasse, genaue Schwierigkeitsstufe etc. kannst du im Arbeitsauftrag beschreiben.

---

### 2. Externe interaktive Ressource hinzufügen

Im Auftrag:

1. **Ressource hinzufügen**
2. Ressourcentyp wählen: **Extern (interaktiv)**  
   (oder entsprechende Option in deiner LearningView-Version)
3. Als URL die GitHub-Pages-Adresse eintragen, z. B.:  
   `https://deinname.github.io/wortarten-ringkampf/`
4. Optional: Titel z. B.  
   **„Wortarten-Trainingskampf“**

Speichern.

---

### 3. Automatische Erledigt-Markierung in LearningView

Im Code wird bei Klick auf den **„Fertig“-Button** am Ende des Wettkampfs:

```js
if (window.parent && window.parent !== window) {
  window.parent.postMessage('AppSolved', '*');
}
