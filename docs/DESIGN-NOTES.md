# Scope Vision / Interface design

[Product brief](../README.md) · [Produktvorstellung](../README.de.md)

## Industry references

The design research reviewed manufacturers' own documentation on 18 October 2026:

| Reference | Observed interface principle | Scope Vision decision |
| :--- | :--- | :--- |
| [Cognex — VisionPro Deep Learning graphical interface](https://docs.cognex.com/deep-learning_332/web/EN/deep-learning/Content/deep-learning-Topics/overview/gui-vpdl.htm) | Dedicated image display, tool parameters, image browser and result information | Place original and anomaly map in one dark inspection workspace; keep measurement and review alongside it |
| [MVTec — MERLIC user interfaces](https://www.mvtec.com/doc/merlic/5.7/manual/en-us/Content/Getting_started/user_interface.html) | Image-centered tooling with distinct development and operator interfaces | Make the operator's inspection workflow the primary view, with model evidence in a separate view |
| [SensoPart — VISOR / SensoConfig Web](https://www.sensopart.com/en/products/vision-sensors/visor-software-release-212/) | Browser-based configuration of vision sensors | Keep the local browser workflow usable at desktop and narrow widths |

These references helped decide how to arrange images, parameters and results. The layout and cover were made for Scope Vision; no manufacturer logos, screenshots, assets or source code were reused. The project is independent of those manufacturers and does not offer the same product scope.

## Layout and colors

- **Graphite and steel gray:** dark application bar and image stage, neutral control and document surfaces.
- **Signal orange:** primary actions and active navigation. Green, amber and red remain reserved for specific outcomes or state indicators, supported by text.
- **Text and measurements:** fixed-width digits make scores and identifiers easier to compare. Headings and thin separators group the controls.
- **Progress:** the input, analysis and review steps reflect what has actually been completed. The interface does not display a simulated camera connection or production-line status.
- **Project page:** a technical cover, numbered sections, screenshots and a short specification table introduce the application.

The cover is a concept drawing, explicitly labeled as such; it is not a measured inspection result. Application screenshots show real local inference on separate synthetic presentation examples. The redesign changes the interface and presentation without changing the frozen model, calibration or evaluation data.

---

## Deutsch / Gestaltungsentscheidungen

Für die Anordnung von Bildern, Parametern und Ergebnissen wurden die oben verlinkten Dokumentationen von **Cognex, MVTec und SensoPart** betrachtet. Scope Vision verwendet eine eigene Gestaltung mit dunkler Bildfläche, hellen Bedienelementen und Orange für wichtige Aktionen. Messwert und menschliche Bewertung stehen in getrennten Bereichen.

Original und berechnete Abweichungskarte stehen nebeneinander, damit sich die Markierung am Bild überprüfen lässt. Auf schmalen Bildschirmen folgen sie untereinander. Der Ablaufstreifen zeigt die bereits abgeschlossenen Schritte. Auf der Projektseite ergänzen Screenshots und ein technisches Datenblatt die Beschreibung.

Das Titelmotiv ist eine beschriftete Konzeptzeichnung. Die Bildschirmansichten stammen aus der tatsächlichen lokalen Anwendung mit gesonderten Präsentationsbildern. Modellstand, Kalibrierung und Auswertungsdaten wurden durch die Neugestaltung nicht verändert. Es werden keine Herstellerbilder oder -logos übernommen und keine Partnerschaft oder Gleichwertigkeit zu deren Produkten behauptet.
