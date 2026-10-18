![Scope Vision — industrielle Bildprüfung von LeonScope. Vom Prüfbild zur dokumentierten Entscheidung.](assets/cover.png)

**PRODUKTVORSTELLUNG / 01** &nbsp; · &nbsp; **Deutsch** / [English](README.md) &nbsp; · &nbsp; [Fallstudie](docs/CASE-STUDY.de.md) &nbsp; · &nbsp; [Prüfergebnisse](docs/VERIFICATION.de.md)

# Scope Vision

### Optische Prüfung. Sichtbare Abweichungen. Dokumentierte Entscheidungen.

Eine lokale Prüfkonsole für eine fiktive Metallplatte: Das Bildmodell untersucht Kratzer und fehlende Bohrungen, markiert auffällige Regionen und übergibt das Ergebnis an die menschliche Sichtprüfung. Von **LeonScope** mit KI-Unterstützung als eigenständiges Portfolio-Projekt entwickelt.

| ANWENDUNGSBEREICH | PRÜFAUFBAU | PROJEKTSTATUS |
| :--- | :--- | :--- |
| Bildgestützte Qualitätsprüfung | Synthetische Platte · feste Perspektive | Funktionierender lokaler Prototyp |

**Öffentlich ist ausschließlich diese Präsentation.** Anwendungscode, Trainings-/Kalibrierungs-/Testdaten, Modellgewichte und gelernte Parameter bleiben privat. Es wird keine Open-Source- oder Creative-Commons-Lizenz für das eigene Material erteilt. [Rechtehinweis](RIGHTS.md).

---

## 01 / Der Bildarbeitsplatz

![Industrielle Scope-Vision-Prüfkonsole: Original, berechnete Abweichungskarte, Messwert und Sichtprüfung](assets/inspection-desktop.png)

**Gezeigter Prüffall: fehlende Bohrung.** Das Originalbild und die berechnete Abweichungskarte stehen direkt nebeneinander. Rechts sind Messwert und menschliche Bewertung getrennt angeordnet; darunter bleibt die Entscheidung im Prüfprotokoll nachvollziehbar. Das Bild stammt aus dem separaten Präsentationssatz.

| 01 · Bildeingang | 02 · Modellauswertung | 03 · Sichtprüfung |
| :--- | :--- | :--- |
| Synthetisches Beispiel oder lokales PNG/JPEG auswählen. Beleuchtung als Prüfvariante ändern. | Abweichungskarte berechnen, Index anzeigen und Aufnahmebedingungen berücksichtigen. | i. O., n. i. O. oder weitere Prüfung dokumentieren. Bericht als JSON/CSV exportieren. |

Eigene Uploads erfordern immer eine menschliche Prüfung. Der Abweichungsindex ist ein Abstand relativ zur kalibrierten Grenze; er ist keine Wahrscheinlichkeit und keine Freigabe für die Fertigung. Die Markierung zeigt Regionen ungefähr an, keine vermessene Fehlerkontur.

## 02 / Prüfarchiv und Modellvalidierung

<table>
<tr>
<td width="50%"><a href="assets/history-desktop.png"><img src="assets/history-desktop.png" alt="Prüfarchiv mit Modellergebnis, Abweichungsindex und menschlicher Bewertung" /></a></td>
<td width="50%"><a href="assets/evaluation-desktop.png"><img src="assets/evaluation-desktop.png" alt="Modellvalidierung mit Klassifikationsmatrix, Vergleichsverfahren und Beleuchtungsprüfung" /></a></td>
</tr>
<tr>
<td><strong>PRÜFARCHIV</strong><br />Gespeicherte Prüfungen filtern und wieder öffnen. Die ursprüngliche Modellmessung bleibt bei jeder ergänzten Bewertung erhalten.</td>
<td><strong>MODELLVALIDIERUNG</strong><br />Festgelegter Modellstand, getrennte Datenmengen, Vergleichsverfahren und Lichtprüfungen direkt in der Anwendung.</td>
</tr>
</table>

<details>
<summary><strong>Mobile Ansicht öffnen</strong> — derselbe Prüfablauf bei 390 Pixeln Breite</summary>

Original, Abweichungskarte, Messwert und Bewertung folgen auf dem Smartphone untereinander. Der Ablauf wurde ohne horizontales Überlaufen geprüft.

<img src="assets/inspection-mobile.png" width="340" alt="Mobile Scope-Vision-Prüfkonsole mit Bildanalyse, menschlicher Bewertung und Protokoll" />

</details>

## 03 / Technisches Datenblatt

| Merkmal | Umsetzung und beobachteter Stand |
| :--- | :--- |
| Bildmodell | Unveränderte vortrainierte ResNet18-Merkmale + lokal angepasste Gauß-Verteilungen für Bildbereiche; angelehnt an PaDiM |
| Lern- und Kalibrierungsdaten | 160 fehlerfreie Lernbilder · 90 Kalibrierungsbilder |
| Getrennter Test | 180 synthetische Szenen: 60 fehlerfrei, 60 Kratzer, 60 fehlende Bohrung |
| Modell bei Standardlicht | **120 / 120 Fehler erkannt · 0 / 60 Fehlalarme** |
| Grauwert-Referenzvergleich | **117 / 120 Fehler erkannt · 3 übersehen · 0 / 60 Fehlalarme** |
| Verifikation | **46 Anwendungs-/Modellprüfungen + 8 Browserabläufe bestanden** |
| Wiederholbarkeit | **436 Bildprüfsummen bestätigt · 180 Testvorhersagen reproduziert** |
| Anwendung | Python · FastAPI · PyTorch/TorchVision · React · TypeScript · SQLite |
| Gestaltung | Industrielle Prüfkonsole: Graphit, Stahlgrau, Signalorange und funktionale Ergebnisfarben |

Die Messwerte gelten für den eigenen synthetischen Beispielsatz. Sie belegen keine Zuverlässigkeit an realen Fertigungslinien und keine allgemeine Überlegenheit gegenüber einfacheren Verfahren. Das CNN wird nicht nachtrainiert; Lernen bedeutet hier die Anpassung normaler Merkmalsverteilungen. [Messverfahren, Lichtvarianten und Grenzen](docs/VERIFICATION.de.md).

### Gestaltungs- und Engineering-Entscheidungen

Die Bildarbeitsfläche bildet das Zentrum. Eine horizontale Werkzeugleiste, ein zustandsabhängiger Prüfablauf und klare Messwertfelder unterstützen die Bedienung. Dokumentierte Oberflächen von Cognex, MVTec und SensoPart dienten als Branchenreferenzen; die Gestaltung und das Titelmotiv sind eigenständig. [Gestaltungsreferenzen und Umsetzung](docs/DESIGN-NOTES.md).

Das Projekt knüpft an LeonScopes Erfahrung mit Robotik und kameragestützter Qualitätsprüfung an. Es verwendet keine Arbeitgeberbilder, Kundendaten, industriellen Zeichnungen oder früheren Arbeitgeberquellcode. Eine Kamera, ein Roboter oder eine Fertigungslinie sind nicht angebunden. Es gibt kein öffentliches Deployment, kein ausführbares Paket, keinen Datensatz-/Modelldownload und keine öffentliche Anwendungs-CI.

---

**LEONSCOPE / ENGINEERING PORTFOLIO**

[Fallstudie](docs/CASE-STUDY.de.md) · [Prüfergebnisse](docs/VERIFICATION.de.md) · [Gestaltung](docs/DESIGN-NOTES.md) · [Rechtehinweis](RIGHTS.md) · [Profil](https://github.com/LeonScope)
