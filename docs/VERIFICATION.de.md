# Scope Vision — Prüfergebnisse

[English](VERIFICATION.md) · **Deutsch** · [Projekt](../README.de.md)

Die Tests liefen während der Entwicklung am **18. Oktober 2026** lokal. Sie wurden weder von einer unabhängigen Prüfstelle noch über öffentliche CI ausgeführt. Für eine Wiederholung wären der private Quellcode sowie Modell- und Datendateien erforderlich.

## Prüfung der Anwendung

Nach der Neugestaltung der Oberfläche wurde die getrennte Testkopie auf den neuen Quellstand aktualisiert. Dieselben 46 Python-Tests und acht Browserabläufe bestanden erneut, einschließlich der Prüfung des Ablaufstreifens. Modell- und Auswertungsdateien behielten ihre ursprünglichen Prüfsummen. Die installierten Abhängigkeiten wurden unverändert weiterverwendet; die frühere Neuinstallation wurde dabei nicht wiederholt.

| Prüfung | Beobachtetes Ergebnis |
| --- | --- |
| Separate lokale Prüfkopie | Privater Quellstand `2c12b09cb562f324ae9d19d59ca191712811e395` |
| Installation der Abhängigkeiten | Zuvor sauber installierte Umgebungen wiederverwendet; Abhängigkeitsdateien bei der Oberflächenrevision unverändert |
| Typprüfung und Erstellung der fertigen Oberfläche | Bestanden |
| Python-Prüfungen für Anwendung und Modell | **46 bestanden** |
| Browserabläufe | **8 bestanden**, ohne Wiederholungsversuche im abschließenden Lauf |
| Datenintegrität | **436 von 436 Bildprüfsummen stimmen überein** |
| Wiederholung mit festgelegtem Modellstand | **180 Testvorhersagen reproduziert**; Gesamtergebnisse von Modell und Vergleichsverfahren stimmen überein |
| Modellstand bei der Wiederholung | Vorhandene private Artefakte geprüft; kein neues Training und keine geänderte Entscheidungsgrenze |
| Bildschirmansichten | Aus dem geprüften neuen Stand der separaten Kopie; ausschließlich Präsentationsbeispiele |

Umgebung: macOS 26.6 auf arm64, Python 3.12.14, Node.js 24.19.0, Chrome 155.0.8059.84. Die Modellberechnung verwendet die CPU mit zwei PyTorch-Threads. Die Paketversionen sind privat festgehalten, darunter PyTorch 2.14.1 und TorchVision 0.29.1.

Die Python-Prüfung meldet einen Hinweis von Starlette zum künftig abzulösenden httpx-Testclient; alle 46 Prüfungen bestehen. Der Hinweis betrifft den Testclient und führte zu keinem fehlgeschlagenen Anwendungstest.

Die acht Browserabläufe prüfen echte bildabhängige Auswertung; ergänzende Bewertungen und Downloads; Lichtänderungen; lokale Uploads; bestätigte/abgebrochene Löschung; Filtern und Wiederöffnen im Verlauf; Modellnachweise mit Präsentationsansichten; sowie den Ablauf bei 390 Pixeln Breite ohne horizontales Überlaufen.

Die Python-Prüfungen behandeln Datentrennung und Artefaktintegrität, Bindung der festgelegten Ergebnisse, Reaktion auf veränderte Bildinhalte, Entscheidungszonen, Aufnahmebedingungen, Speicherung, Aufbewahrungsgrenzen und vollständige Löschung, Bewertungslimits, Eingabeprüfung, fremde Herkunft, Schutz privater Dateien, fehlgeschlagene/gleichzeitige Auswertung, Entfernen von Bildmetadaten und CSV-Formelbehandlung. Das sind begrenzte Tests, kein Penetrationstest und keine Sicherheitszertifizierung für den Produktivbetrieb.

## Getrennte Datenmengen

| Datenmenge | Bilder | Verwendung |
| --- | ---: | --- |
| Training | 160 fehlerfreie | Normale Merkmalsverteilungen anpassen |
| Kalibrierung | 90: je 30 pro Klasse | Grenzen für Modell und Vergleichsverfahren festlegen |
| Getrennter Test bei Standardlicht | 180: je 60 pro Klasse | Festgelegten Stand auswerten |
| Präsentation | 6: je 2 pro Klasse | Separate Oberflächenbeispiele; ausgewählte Ansichten dürfen veröffentlicht werden |

Alle Mengen verwenden unterschiedliche Szenenkennungen desselben synthetischen Generators. Die Bilder variieren leicht in Position, Textur und Helligkeit. Dies ist **keine** Trennung nach physischen Bauteilen, Kameras, Fabriken oder echten Fertigungschargen. Sämtliche Trainings-, Kalibrierungs- und Testbilder bleiben privat, ebenso ihre Masken und Einzelvorhersagen.

## Modell und Entscheidungsgrenze

Modellversion: `scope-vision-1.0` · Modellkennung: `199b18fad8e11f73`.

Unveränderte vortrainierte ResNet18-Merkmale bilden die Eingabe eines kompakten räumlichen Gauß-Modells für Bildbereiche. Die Kalibrierung maximiert die ausgewogene Klassifikationsgenauigkeit und bevorzugt bei Gleichstand weniger übersehene Fehler, danach die höhere Grenze. Die ermittelte Rohgrenze beträgt **12,225147247314453**. Höhere Bildmesswerte gelten als auffällig; der angezeigte Index ist Messwert geteilt durch diese Grenze. Index 0,85–1,15, bekannte Aufnahmeprobleme oder ein eigener Upload führen zur manuellen Prüfung.

Die Grenze stand vor der Testauswertung fest. Der gespeicherte Bericht ist an Modellmetadaten und Artefaktprüfsummen gebunden. Training/Auswertung verweigern das Überschreiben des vorhandenen angepassten Stands/Berichts. Die Kontrolle in der separaten Prüfkopie wiederholt den festgelegten Stand; sie ist kein zweites Trainingsexperiment.

## Ergebnisse bei Standardlicht

| Tatsächliche Eingabe | Modell unauffällig | Modell auffällig |
| --- | ---: | ---: |
| 60 fehlerfreie Bilder | 60 | 0 |
| 60 Kratzerbilder + 60 Bilder mit fehlender Bohrung | 0 | 120 |

Beide Fehlerarten wurden in jeweils **60 von 60** Testbildern erkannt. Der einfache Grauwertvergleich erkannte **117 von 120** Fehlern, übersah **3** und erzeugte **0 von 60** Fehlalarmen. Die jeweilige Grenze wurde an der Kalibrierung festgelegt, nicht an diesem Test.

Oberflächeneinstufung bei Standardlicht: 60 unauffällig, 120 auffällig, 0 manuelle Prüfungen. Diese Ergebnisse gelten für den begrenzten Satz erzeugter Bilder. Bei zukünftigen Bildern können trotzdem Fehler auftreten. Wie genau die Markierungen den Fehler räumlich treffen, wurde nicht vermessen.

## Gepaarte Lichtprüfungen

| Lichtvariante | Manuelle Prüfung erforderlich | Roh erkannte Fehler | Rohe Fehlalarme |
| --- | ---: | ---: | ---: |
| Weniger Licht | 180 / 180 | 120 / 120 | 0 / 60 |
| Zusätzlicher Lichtreflex | 110 / 180 | 120 / 120 | 0 / 60 |

Dies sind **dieselben 180 Testszenen** mit zwei Lichtveränderungen, keine 360 zusätzlichen unabhängigen Szenen. Das rohe Modell bleibt bei diesen Varianten korrekt, während die Aufnahmeprüfung einige oder alle Bilder an eine Person übergibt. Die 70 Reflexvarianten ohne Prüfhinweis zeigen, dass diese Prüfung nicht jede Lichtänderung vollständig erkennt. Das Verhalten unter anderen Lichtbedingungen ist damit noch nicht geprüft.

## Laufzeit und messbare Grenzen

Bei der ursprünglichen lokalen CPU-Auswertung betrug die reine Modellberechnung über 180 Testbilder bei Standardlicht **12,2 ms im Median** und **13,4 ms am 95. Perzentil**. Die Messung beginnt nach dem Laden des Bildes und umfasst Merkmalsextraktion und Abstandsberechnung. Nicht enthalten sind Modellladen, Bilderzeugung, Upload, Markierungsdarstellung, Speicherung oder Browserarbeit. Die Einzelmessung in der Oberfläche enthält zusätzlich die Erzeugung der Markierung. Die Werte sind Beobachtungen an einem Rechner und kein Versprechen für die Gesamtlaufzeit.

![Nachweisansicht mit Verwechslungsmatrix, Vergleichsverfahren und gepaarten Lichtprüfungen](../assets/evaluation-desktop.png)

## Veröffentlichte Unterlagen

Dieses Repository enthält zweisprachige Dokumentation, ein eigenes Titelmotiv, vier ausgewählte Bildschirmansichten und einen Rechtehinweis. Es hat eine eigene Präsentationshistorie. Anwendungscode, fertiger Anwendungsbuild, ausführbare Pakete, Trainings-/Kalibrierungs-/Testbilder, Modellparameter, Gewichte, private Protokolle und Kunden-/Arbeitgeberdaten sind nicht enthalten. Die Plattenbilder innerhalb der Screenshots stammen ausschließlich aus den Präsentationsbeispielen.

Es gibt kein öffentliches Deployment, keine öffentliche Anwendungs-CI, keine Fertigungsintegration und keinen industriellen Abnahmenachweis. [Fallstudie](CASE-STUDY.de.md) · [Rechtehinweis](../RIGHTS.md).
