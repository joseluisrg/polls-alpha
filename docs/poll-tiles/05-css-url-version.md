# Schritt 5 – CSS-Adresse für die Kachelansicht versionieren

**Datum:** 6. November 2026

**Verantwortlich:** Markus; Codex zur Vorbereitung und Auswertung; Valeria für das anschließende Teamreview vorgesehen.

**Status:** Ein-Zeilen-Änderung lokal angewendet und mit den 15 vorhandenen Tests erfolgreich geprüft. Fix-Commit, Push, Teamreview, Bereitstellung und Prüfung der öffentlichen Wirkung stehen noch aus.

## Anlass und Diagnose

Die gesammelte CSS-Datei auf PythonAnywhere und die direkten öffentlichen HTTPS-Antworten enthalten bereits die neuen Kachelregeln. Vier verglichene Inhalte waren identisch: Projekt-CSS, Static-Ziel, normaler öffentlicher Abruf und Abruf mit frischem Prüfparameter. Jeweils 1268 Bytes; SHA-256 `a27536ebcd2d3883e6bbfbe4d62e3d8946690781fa7e34480563cb912dfa3fcd`; `.page` und `.tiles` vorhanden. Beide HTTP-Antworten lieferten Status 200 und `text/css`.

Im App-Browser waren weiterhin nur die beiden alten CSS-Regeln aktiv; die neue Formatierung fehlte auch nach erneutem Laden. Markus meldete außerdem die unveränderte Darstellung im privaten Modus. Das Static-Mapping wurde per Screenshot als passend bestätigt. Der genaue Ort der abweichenden beziehungsweise zwischengespeicherten Browserantwort ist nicht abschließend bestimmt.

## Änderung

Auf dem Branch `fix/poll-tiles-css-cache`, ausgehend von `main` bei `00d5649`, wurde in `mysite/polls/templates/polls/index.html` der Stylesheet-Link ergänzt:

```html
<link rel="stylesheet" href="{% static 'polls/style.css' %}?v=poll-tiles-1">
```

Die konstante Versionskennung gibt diesem CSS-Stand eine eigene Anfrageadresse. HTTP-Caches unterscheiden gespeicherte Antworten unter anderem anhand der Ziel-URI. Die Änderung soll die beobachtete Wiederverwendung der alten Browserregeln vermeiden; der öffentliche Erfolg wird nach Bereitstellung geprüft. Quelle: [RFC 9111, Abschnitt 2](https://www.rfc-editor.org/rfc/rfc9111.html#section-2).

Bei späteren CSS-Änderungen ist die manuell gepflegte Versionskennung entsprechend anzupassen.

## Tatsächliche lokale Prüfung

Markus hat den vorbereiteten Patch geprüft und angewendet. Der übermittelte Diff umfasst genau die Stylesheet-Zeile; `git diff --check` war erfolgreich.

Anschließend hat Markus `manage.py test polls` mit seinem lokalen Projektinterpreter ausgeführt:

```text
Python: 3.14.10
Django: 5.2.18
Found 15 test(s).
System check identified no issues (0 silenced).
Ran 15 tests in 0.062s
OK
```

Alle 15 vorhandenen Tests erfolgreich. Codex hat die übermittelte Ausgabe ausgewertet und den Projektcode in diesem Schritt nicht selbst ausgeführt. Die Testlaufzeit ist eine Einzelmessung, keine Leistungsbewertung.

## Offene öffentliche Prüfung

- Nach Commit/Push und Teamreview den Fix in `main` zusammenführen.
- Auf PythonAnywhere im bestehenden Hostingbranch übernehmen und Web-App neu laden.
- Prüfen, ob der Browser den Link mit Versionskennung und die neuen CSS-Regeln verwendet: serifenlose Schrift, passende Innenabstände und anschließend Kacheln mit verfügbaren Fragen.
- Öffentliche Testfragen und vollständigen Abstimmungsablauf mit den tatsächlichen Hostingdaten prüfen.

Die erfolgreichen lokalen Tests beweisen noch nicht die Korrektur der öffentlichen Browserdarstellung. Diese wird erst nach tatsächlicher Prüfung als erfolgreich dokumentiert.

## Kurzprotokoll für den Labor-Bericht

- **Gemacht:** Identische neue CSS-Inhalte auf Server und in direkten HTTPS-Antworten nachgewiesen; kleine Änderung der Ressourcenadresse auf eigenem Branch angewendet; 15 vorhandene lokale Tests unter Python 3.14.10 / Django 5.2.18 erfolgreich.
- **KI genutzt:** Diagnoseausgabe und Browserregeln abgeglichen; Änderung als Patch und Git-Schritte vorbereitet; tatsächlichen Diff und Testausgabe ausgewertet; Dokumentation und Review-Texte erstellt. Git-Aktionen und Tests durch Markus.
- **Gelernt – Formulierungsvorschlag:** Aktuelle Serverdateien und tatsächlich verwendete Browserregeln sind unterschiedliche Nachweise. Eine Versionskennung unterscheidet CSS-Stände in ihrer Anfrageadresse; ihre Wirkung muss nach der Bereitstellung überprüft werden.
- **GitHub-Link:** Ausgangsstand [00d5649](https://github.com/joseluisrg/polls-alpha/commit/00d5649), zugehöriger [UI-PR 3](https://github.com/joseluisrg/polls-alpha/pull/3). Neuer Fix-Commit und Fix-PR noch ausstehend.

## Nachweise und Yellowdig

Screenshots der Diagnoseausgabe, des Ein-Zeilen-Diffs und der erfolgreichen lokalen Tests aufbewahren. Nach tatsächlichem Review und Deployment GitHub-Nachweis und öffentliche korrigierte Darstellung sichern.

**Yellowdig-Entwurf:** Die direkte CSS-Diagnose bestätigte bereits den richtigen neuen Inhalt auf dem Server, während im App-Browser alte Regeln aktiv blieben. Auf einem eigenen Branch habe ich deshalb die Stylesheet-Adresse um eine konstante Versionskennung ergänzt. Alle 15 vorhandenen lokalen Tests sind erfolgreich. KI unterstützte bei Diagnose, Patch, Befehlen und Dokumentation. Teamreview, Bereitstellung und die Prüfung der öffentlichen Wirkung folgen noch.

Persönlichen Lernergebnis-Text abgleichen. Den tatsächlichen Fix-Commit-Link nach dem Upload im Labor-Bericht beziehungsweise Yellowdig-Beitrag ergänzen; dafür ist kein erneuter Commit dieser Datei nötig.
