# Scope Vision / Interface design

[Product brief](../README.md) · [Produktvorstellung](../README.de.md)

## Industry references

The design research reviewed manufacturers' own documentation on 18 October 2026:

| Reference | Observed interface principle | Scope Vision decision |
| :--- | :--- | :--- |
| [Cognex — VisionPro Deep Learning graphical interface](https://docs.cognex.com/deep-learning_332/web/EN/deep-learning/Content/deep-learning-Topics/overview/gui-vpdl.htm) | Dedicated image display, tool parameters, image browser and result information | Place original and anomaly map in one dark inspection workspace; keep measurement and review alongside it |
| [MVTec — MERLIC user interfaces](https://www.mvtec.com/doc/merlic/5.7/manual/en-us/Content/Getting_started/user_interface.html) | Image-centered tooling with distinct development and operator interfaces | Make the operator's inspection workflow the primary view, with model evidence in a separate view |
| [SensoPart — VISOR / SensoConfig Web](https://www.sensopart.com/en/products/vision-sensors/visor-software-release-212/) | Browser-based configuration of vision sensors | Keep the local browser workflow usable at desktop and narrow widths |

These references informed layout priorities. Manufacturer logos, screenshots, assets and source code are not included in this repository. Scope Vision is an independent project, with no affiliation, endorsement or claimed feature equivalence.

## Applied visual language

- **Graphite and steel gray:** dark application bar and image stage, neutral control and document surfaces.
- **Signal orange:** primary actions and active navigation. Green, amber and red remain reserved for specific outcomes or state indicators, supported by text.
- **Technical typography:** monospaced measurements and identifiers, restrained headings and thin separators.
- **Visible process:** input, analysis and human review indicate actual application state. No simulated camera connection or production-line status is shown.
- **Distinct portfolio format:** an original technical cover, numbered product chapters, a view gallery and a compact specification sheet.

The cover is a concept drawing, explicitly labeled as such; it is not a measured inspection result. Application screenshots show real local inference on separate synthetic presentation examples. The redesign changes the interface and presentation without changing the frozen model, calibration or evaluation data.

---

## Deutsch / Gestaltungsentscheidungen

Die Herstellerdokumentationen von **Cognex, MVTec und SensoPart** wurden als Branchenreferenzen für Bildarbeitsflächen, Parameterbereiche und browsergestützte Bedienung betrachtet. Daraus entstand eine eigenständige Prüfkonsole: Graphit und Stahlgrau, Signalorange für Aktionen, geradlinige Flächen und klar getrennte Messwerte und Bewertungen.

Die Prüfung steht im Mittelpunkt. Der Ablaufstreifen zeigt die tatsächlich erreichten Schritte; Original und berechnete Abweichungskarte sind direkt vergleichbar. Auf schmalen Bildschirmen folgen diese Bereiche untereinander. Die öffentliche Präsentation verwendet nummerierte Produktkapitel, eine Ansichtengalerie und ein technisches Datenblatt.

Das Titelmotiv ist eine beschriftete Konzeptzeichnung. Die Bildschirmansichten stammen aus der tatsächlichen lokalen Anwendung mit gesonderten Präsentationsbildern. Modellstand, Kalibrierung und Auswertungsdaten wurden durch die Neugestaltung nicht verändert. Es werden keine Herstellerbilder oder -logos übernommen und keine Partnerschaft oder Gleichwertigkeit zu deren Produkten behauptet.
