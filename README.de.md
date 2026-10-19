![Scope Vision — industrielle Bildprüfung von LeonScope. Vom Prüfbild zur dokumentierten Entscheidung.](assets/cover.png)

**PRODUKTVORSTELLUNG / 01** &nbsp; · &nbsp; **Deutsch** / [English](README.md) &nbsp; · &nbsp; [Fallstudie](docs/CASE-STUDY.de.md) &nbsp; · &nbsp; [Prüfergebnisse](docs/VERIFICATION.de.md)

# Scope Vision

### Kratzer und fehlende Bohrungen im Bild erkennen

Scope Vision untersucht erzeugte Bilder einer Metallplatte auf Kratzer und fehlende Bohrungen. Neben dem Original zeigt die Anwendung, welche Bildbereiche dem Modell auffallen. Eine Person kann das Ergebnis anschließend bewerten und ihre Entscheidung speichern. Mit diesem Projekt greife ich meine Erfahrung in der kameragestützten Qualitätsprüfung auf; die Anwendung wurde mit KI-Unterstützung neu entwickelt.

| ANWENDUNGSBEREICH | PRÜFAUFBAU | PROJEKTSTATUS |
| :--- | :--- | :--- |
| Bildgestützte Qualitätsprüfung | Synthetische Platte · feste Perspektive | Funktionierender lokaler Prototyp |

**Öffentlich ist ausschließlich diese Präsentation.** Anwendungscode, Trainings-/Kalibrierungs-/Testdaten, Modellgewichte und gelernte Parameter bleiben privat. Es wird keine Open-Source- oder Creative-Commons-Lizenz für das eigene Material erteilt. [Rechtehinweis](RIGHTS.md).

---

## 01 / Der Bildarbeitsplatz

![Industrielle Scope-Vision-Prüfkonsole: Original, berechnete Abweichungskarte, Messwert und Sichtprüfung](assets/inspection-desktop.png)

**Im Beispiel fehlt eine Bohrung.** Links steht das Original, daneben die berechnete Abweichungskarte. Rechts lassen sich Messwert und menschliche Bewertung ablesen. Das Protokoll darunter hält beides getrennt fest. Für die Screenshots werden eigene Präsentationsbilder verwendet, die nicht zum Training oder Test gehören.

| 01 · Bildeingang | 02 · Modellauswertung | 03 · Sichtprüfung |
| :--- | :--- | :--- |
| Synthetisches Beispiel oder lokales PNG/JPEG auswählen. Beleuchtung als Prüfvariante ändern. | Abweichungskarte berechnen, Index anzeigen und Aufnahmebedingungen berücksichtigen. | i. O., n. i. O. oder weitere Prüfung dokumentieren. Bericht als JSON/CSV exportieren. |

Eigene Uploads müssen immer von einer Person geprüft werden. Der Abweichungsindex setzt den Messwert ins Verhältnis zur festgelegten Grenze. Er ist keine Wahrscheinlichkeit und erlaubt keine automatische Fertigungsfreigabe. Auch die Markierung ist nur eine ungefähre Ortsangabe; sie vermisst den Fehler nicht.

## 02 / Prüfarchiv und Modellvalidierung

<table>
<tr>
<td width="50%" valign="top">
<strong>PRÜFARCHIV</strong><br />Gespeicherte Prüfungen filtern und wieder öffnen. Die ursprüngliche Modellmessung bleibt bei jeder ergänzten Bewertung erhalten.<br /><br />
<a href="assets/history-desktop.png"><img src="assets/history-desktop.png" alt="Prüfarchiv mit Modellergebnis, Abweichungsindex und menschlicher Bewertung" /></a>
</td>
<td width="50%" valign="top">
<strong>MODELLVALIDIERUNG</strong><br />Festgelegter Modellstand, getrennte Datenmengen, Vergleichsverfahren und Lichtprüfungen direkt in der Anwendung.<br /><br />
<a href="assets/evaluation-desktop.png"><img src="assets/evaluation-desktop.png" alt="Modellvalidierung mit Klassifikationsmatrix, Vergleichsverfahren und Beleuchtungsprüfung" /></a>
</td>
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

### Warum die Oberfläche so aufgebaut ist

Original und Auswertung sollen direkt vergleichbar sein. Deshalb nehmen die Bilder den größten Teil der Prüfstation ein; Messwerte und Bewertung stehen daneben. Der Ablaufstreifen zeigt, welche Schritte bereits abgeschlossen sind. Für die Gestaltung wurden dokumentierte Oberflächen von Cognex, MVTec und SensoPart betrachtet. Die [Gestaltungsnotizen](docs/DESIGN-NOTES.md) nennen die Quellen und erklären die Umsetzung.

Scope Vision enthält keine Bilder, Zeichnungen, Daten oder Quelltexte früherer Arbeitgeber oder Kunden. Kamera und Roboter sind nicht angebunden. Die Anwendung läuft lokal; einen öffentlichen Demozugang, Softwaredownload, Datensatz- oder Modelldownload und Anwendungstestlauf auf GitHub gibt es nicht.

---

**LEONSCOPE / ENGINEERING PORTFOLIO**

[Fallstudie](docs/CASE-STUDY.de.md) · [Prüfergebnisse](docs/VERIFICATION.de.md) · [Gestaltung](docs/DESIGN-NOTES.md) · [Rechtehinweis](RIGHTS.md) · [Profil](https://github.com/LeonScope)
