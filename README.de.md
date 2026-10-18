# Scope Vision · Visual Quality Inspector

[English](README.md) · **Deutsch**

**Lokale Bildprüfung mit berechneten Abweichungsmarkierungen und nachvollziehbarer menschlicher Bewertung.** Von LeonScope mit KI-Unterstützung als eigenständiges Portfolio-Projekt entwickelt.

Scope Vision prüft eine fiktive Platte auf Kratzer und fehlende Bohrungen. Ein tatsächliches Bildmodell ist mit einem bedienbaren Arbeitsablauf verbunden: Bild prüfen, markierte Bereiche ansehen, menschliche Bewertung dokumentieren und Prüfbericht exportieren.

**Dieses Repository enthält ausschließlich die Präsentation. Anwendungscode, Trainings-, Kalibrierungs- und Testdaten sowie Modellgewichte und gelernte Parameter bleiben privat.** Die Screenshots verwenden gesondert erzeugte Präsentationsbeispiele. Für das eigene Material wird keine Open-Source- oder Creative-Commons-Lizenz erteilt; siehe [Rechtehinweis](RIGHTS.md).

![Scope Vision: Prüfstation mit berechneter Abweichungsmarkierung und dokumentierter Sichtprüfung](assets/inspection-desktop.png)

*Fehlende Bohrung in einem synthetischen Präsentationsbeispiel. Die farbige Markierung wird aus dem Bild berechnet; die menschliche Bewertung wird getrennt vom Modellergebnis gespeichert.*

## Der Arbeitsablauf

- Synthetische Beispiele oder ein lokal hochgeladenes PNG-/JPEG-Bild prüfen.
- Originalbild und ungefähre Abweichungsmarkierung vergleichen.
- Ergebnisse als **unauffällig**, **auffällig** oder **manuell prüfen** unterscheiden.
- Menschliche Bewertungen ergänzen, ohne die ursprüngliche Modellmessung zu verändern.
- Lokalen Prüfverlauf wieder öffnen und Berichte als JSON oder CSV exportieren.
- Die Auswertung des festgelegten Modellstands und die Lichtprüfungen direkt in der Anwendung ansehen.

Eigene Uploads erfordern immer eine menschliche Prüfung, weil ihre Bildverteilung nicht validiert wurde. Der Abweichungsindex beschreibt einen Abstand relativ zu einer kalibrierten Grenze. Er ist keine Wahrscheinlichkeit und keine Freigabe für die Fertigung.

## Messung an einer bewusst begrenzten Aufgabe

Der getrennte Testsatz bei Standardlicht enthält **180 synthetische Szenen**: 60 fehlerfreie Platten, 60 mit Kratzern und 60 mit fehlenden Bohrungen. Die Entscheidungsgrenze wurde vor diesem Test festgelegt.

| Verfahren | Erkannte Fehler | Übersehene Fehler | Fehlalarme bei fehlerfreien Bildern |
| --- | ---: | ---: | ---: |
| Vortrainierte CNN-Merkmale + gelernte Bildverteilungen | 120 / 120 | 0 | 0 / 60 |
| Einfacher Grauwert-Referenzvergleich | 117 / 120 | 3 | 0 / 60 |

Diese Beobachtungen gelten für den eigenen synthetischen Bildgenerator. Daraus folgen weder eine zugesicherte Leistung an realen Fertigungsbildern noch eine allgemeine Überlegenheit gegenüber einfacheren Verfahren. [Vollständige Nachweise und Grenzen](docs/VERIFICATION.de.md).

## Technischer Nachweis

**46 automatisierte Anwendungs-/Modellprüfungen und acht Browserabläufe in einer frischen lokalen Kopie bestanden**, mit neu installierten, festgeschriebenen Abhängigkeiten. Das versiegelte private Modellpaket wurde übernommen und geprüft; bei dieser Kontrolle wurde es nicht neu trainiert. Alle **436 Bildprüfsummen** stimmten überein, und die **180 Testvorhersagen** reproduzierten die dokumentierten Gesamtergebnisse.

Python · FastAPI · PyTorch/TorchVision · React · TypeScript · SQLite · pytest · Playwright.

Der Detektor verwendet unveränderte vortrainierte ResNet18-Merkmale und lokal angepasste Gauß-Verteilungen für Bildbereiche, angelehnt an PaDiM. Es wird weder ein Basismodell von Grund auf trainiert noch das CNN nachtrainiert. [Verfahren und Umsetzungsentscheidungen](docs/CASE-STUDY.de.md).

## Weitere Ansichten

![Lokaler Prüfverlauf mit getrennten Modellergebnissen und menschlichen Bewertungen](assets/history-desktop.png)

<details>
<summary>Modellnachweise und Smartphone-Ablauf</summary>

![Modellnachweise, Vergleichsverfahren und gepaarte Lichtprüfungen](assets/evaluation-desktop.png)

<img src="assets/inspection-mobile.png" width="350" alt="Scope Vision: Bildprüfung und menschliche Bewertung in einer 390 Pixel breiten Smartphone-Ansicht" />

</details>

## Einordnung und Grenzen

Dieses eigenständige Projekt verbindet LeonScopes Erfahrung in Robotik und kameragestützter Qualitätsprüfung mit einer neuen lokalen Anwendung. Es enthält keine Arbeitgeberbilder, Kundendaten, industriellen Zeichnungen oder früheren Arbeitgeberquellcode. Eine Kamera, ein Roboter oder eine Fertigungslinie sind nicht angebunden.

Die Anwendung ist ein funktionierender lokaler Prototyp. Sie ist kein gehosteter Dienst und keine industriell abgenommene Prüfanlage. Dieses öffentliche Repository enthält Dokumentation und ausgewählte Bildschirmansichten; es stellt kein ausführbares Paket, keinen öffentlichen Trainingsdatensatz, keinen Modelldownload und keine öffentliche Anwendungs-CI bereit.

[Fallstudie](docs/CASE-STUDY.de.md) · [Prüfergebnisse](docs/VERIFICATION.de.md) · [Rechtehinweis](RIGHTS.md) · [LeonScope](https://github.com/LeonScope)
