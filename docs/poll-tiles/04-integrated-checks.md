# Schritt 4 – Prüfung der integrierten Kachelansicht

**Datum:** 6. November 2026

**Verantwortlich:** Markus; Codex zur Vorbereitung und Auswertung

**Geprüfter Projektstand:** [main bei 0732246](https://github.com/joseluisrg/polls-alpha/commit/0732246), nach lokalem Abgleich identisch mit `origin/main`. Enthält [UI-PR 3](https://github.com/joseluisrg/polls-alpha/pull/3) und die integrierte Gesamtstimmenberechnung.

**Status:** Lokale integrierte Prüfung erfolgreich abgeschlossen. Alle 15 automatisierten Tests erfolgreich; Markus bestätigt zusätzlich korrekte Links, Gesamtstimmen 2, 0 und 0 nach einer weiteren Abstimmung, funktionierende schmale Ansicht und Tastaturbedienung. Diese Prüfdokumentation und der Ausgangsscreenshot sind für GitHub vorbereitet; Commit und Upload noch ausstehend. Veröffentlichung auf PythonAnywhere noch offen.

## Automatisierte Prüfung – bestätigt

Markus hat in seiner lokalen Windows-Entwicklungsumgebung `manage.py test polls` mit dem vorhandenen Projektinterpreter ausgeführt und folgende Ausgabe übermittelt:

```text
Python: 3.14.10
Django: 5.2.18
Found 15 test(s).
Creating test database for alias 'default'...
System check identified no issues (0 silenced).
...............
Ran 15 tests in 0.069s
OK
Destroying test database for alias 'default'...
```

Ergebnis: Alle 15 vorhandenen Tests erfolgreich; Systemprüfung ohne Befunde. Codex hat die Ausgabe ausgewertet und die Tests in diesem Schritt nicht selbst ausgeführt. Die gemeldete Laufzeit ist die von Markus übermittelte Einzelmessung, keine Leistungsbewertung.

## Sichtbare Kachelansicht – bestätigt

Markus' Screenshot zeigt die lokale Adresse `127.0.0.1:8000/polls/` und:

- Drei Fragen als Kacheln in einer Reihe.
- Jeweils das Veröffentlichungsdatum „4 Nov 2026“.
- Gesamtstimmen 1, 0 und 0; Singular „1 vote“ und Plural „0 votes“ sichtbar.
- Auf jeder Kachel „Vote →“.
- Die lange dritte Frage bricht auf mehrere Zeilen um und ist in der abgebildeten breiten Ansicht vollständig lesbar.

Screenshot: von Markus unter „Successful test of the tile design.png“ übermittelt; unveränderte Kopie als [04_3_Kachelansicht_lokal_1_0_0.png](04_3_Kachelansicht_lokal_1_0_0.png) zur gemeinsamen Ablage mit diesem Protokoll vorbereitet. Er belegt die Darstellung vor der zusätzlichen Abstimmung. Die Bedienprüfungen und Folgewerte hat Markus danach ausdrücklich bestätigt; weitere Screenshots dazu wurden Codex bisher nicht übermittelt.

## Manuelle Prüfungen – durch Markus bestätigt

| Prüfung | Erwartung | Bestätigtes Ergebnis |
|---|---|---|
| Kachellinks | Jede Kachel öffnet ihre passende Frage | Bestanden laut Markus' Rückmeldung |
| Zusätzliche Abstimmung bei Frage 1 | Nach genau einer Stimme und neuem Abruf der Übersicht Gesamtstimmen 2, 0 und 0 | Werte 2, 0 und 0 bestätigt |
| Schmale Ansicht | Kacheln untereinander, lange Frage lesbar, kein abgeschnittener Inhalt | Bestanden laut Markus' Rückmeldung |
| Tastatur | Fokus per Tab erkennbar; Enter öffnet die passende Frage | Bestanden laut Markus' Rückmeldung |

Markus meldet ausdrücklich alle vier Prüfungen als erfolgreich. Codex hat diese Rückmeldung ausgewertet, die Bedienprüfungen aber nicht selbst ausgeführt. Damit ist die lokale Prüfung des integrierten Features abgeschlossen; die Onlineversion wird nach der Veröffentlichung separat geprüft.

## Kurzprotokoll für den Labor-Bericht

- **Gemacht:** Integrierten Stand mit 15 automatisierten Tests und vier manuellen Prüfungen erfolgreich geprüft; Gesamtstimmen von 1, 0 und 0 auf 2, 0 und 0 erhöht; korrekte Links, schmale Ansicht und Tastaturbedienung bestätigt. Ausgangsscreenshot für die Prüfdokumentation gesichert.
- **KI genutzt:** Test- und Startbefehle vorbereitet; tatsächliche Testausgabe, Screenshot und manuelle Rückmeldung ausgewertet; Bildnachweis unverändert gesichert; Protokoll und Git-Anleitung vorbereitet. Tests, Bedienprüfung und Git-Aktionen durch Markus.
- **Gelernt – Formulierungsvorschlag:** View und Template arbeiten im integrierten Stand zusammen. Automatisierte Tests werden durch eine Prüfung des vollständigen Abstimmungsablaufs, der Darstellung und der Tastaturbedienung ergänzt.
- **GitHub-Link:** [Geprüfter gemeinsamer Stand](https://github.com/joseluisrg/polls-alpha/commit/0732246), [UI-PR 3](https://github.com/joseluisrg/polls-alpha/pull/3). Neuer GitHub-Link für dieses Prüfprotokoll ausstehend.

## Screenshot-Empfehlungen

- Bereits übermittelten Kachel-Screenshot als Anfangsstand aufbewahren.
- Jetzt die PowerShell-Ausgabe mit Versionen, 15 Tests und `OK` sichern.
- Nach zusätzlicher Abstimmung: Übersicht mit erhöhter Gesamtstimmenzahl und sichtbarer Adresse aufnehmen.
- Nach Prüfung des schmalen Fensters: einspaltige Ansicht mit langer Frage aufnehmen.
- Nach Veröffentlichung auf Yellowdig: eigenen Beitrag mit Datum sichern.

## Yellowdig-Entwurf – aktueller Stand

Die integrierte Version unseres Polls-Features besteht lokal alle 15 vorhandenen Tests unter Python 3.14.10 und Django 5.2.18. Auch die vier manuellen Prüfungen sind erfolgreich: Die Kachellinks führen zu den passenden Fragen, eine zusätzliche Abstimmung erhöhte die Gesamtstimmen von 1, 0 und 0 auf 2, 0 und 0, und sowohl schmale Ansicht als auch Tastaturbedienung funktionieren. Der vorhandene Screenshot dokumentiert den Anfangsstand. KI hat bei der Vorbereitung, der Auswertung meiner Testausgabe und Rückmeldungen sowie der Dokumentation unterstützt. Als Nächstes sichern wir das Prüfprotokoll auf GitHub und aktualisieren anschließend PythonAnywhere.

Persönliche Lernergebnisse vor Übernahme abgleichen. Markus speichert diese abgeschlossene lokale Prüfdokumentation und den zugehörigen Ausgangsscreenshot selbst als kleine GitHub-Änderung. Den tatsächlichen Commit-Link nach dem erfolgreichen Upload im Labor-Bericht beziehungsweise Yellowdig-Beitrag ergänzen; dafür ist kein erneuter Commit dieser Datei erforderlich.
