# Schritt 2 – Gesamtstimmenzahl je Frage

**Verantwortlich:** Markus

**Branch:** `feature/poll-tiles-data`

**Stand dieser Dokumentation:** Lokale Umsetzung abgeschlossen; Markus meldet erfolgreiche Tests. Die Datei wird zusammen mit der Umsetzung gespeichert.

## Umsetzung

- Eigenen Entwicklungsbranch vom aktuellen `origin/main` angelegt und auf GitHub hochgeladen.
- Die Rückfrage beim Entfernen des Dokumentationsordners während des Branch-Wechsels mit `n` beantwortet; Git hat danach Wechsel und Upload bestätigt.
- In `IndexView.get_queryset()` die Gesamtstimmen je Frage ergänzt: `annotate(total_votes=Sum("choice__votes", default=0))`.
- `latest_question_list` und die vorhandenen Fragenfelder beibehalten; `question.total_votes` für Valerias Template bereitgestellt.
- Auswahl bleibt auf die fünf neuesten veröffentlichten Fragen begrenzt; zukünftige Fragen bleiben ausgeschlossen.
- Kein zusätzliches Datenbankfeld erforderlich. Template und CSS gehören zu Valerias Arbeitspaket.

Grundlage: [Django – Aggregation je Objekt](https://docs.djangoproject.com/en/5.2/topics/db/aggregation/#generating-aggregates-for-each-item-in-a-queryset), [Sum](https://docs.djangoproject.com/en/5.2/ref/models/querysets/#sum).

## Prüfungen und Ergebnis

- Projektinterpreter bei der Vorbereitung gemessen: Python 3.14.10, Django 5.2.18.
- Codex: Python-Syntax beider geänderter Dateien geprüft.
- Fünf neue Tests zusätzlich zu den zehn vorhandenen Testmethoden vorbereitet:
  1. Summen pro Frage getrennt berechnen, beispielsweise 2 + 3 + 0 = 5 und separat 7.
  2. Antwortmöglichkeiten ohne Stimmen ergeben insgesamt 0.
  3. Eine Frage ohne Antwortmöglichkeiten ergibt 0.
  4. Nur die fünf neuesten veröffentlichten Fragen mit korrekten Summen zurückgeben.
  5. Nach einer Abstimmung die aktualisierte Gesamtstimmenzahl anzeigen lassen.
- Markus hat die Tests in seiner eigenen PowerShell ausgeführt und erfolgreiche Tests zurückgemeldet. Erwartet werden 15 Tests; die Detailausgabe wurde Codex nicht übermittelt.
- Die gemeinsame sichtbare Kachelansicht und die Veröffentlichung auf PythonAnywhere werden nach Integration von Valerias UI separat geprüft.

## Hindernis bei der Commit-Vorbereitung

- `git diff --cached --check` meldete Leerzeichen am Ende zweier Zeilen der Dokumentationsvorlage.
- Ursache: Codex hatte Markdown-Zeilenumbrüche mit abschließenden Leerzeichen verwendet.
- Die Vorlage wurde auf Absätze ohne abschließende Leerzeichen umgestellt. Vor dem Commit wird die korrigierte Datei erneut ausgewählt und geprüft.
- Die begleitenden LF/CRLF-Hinweise betreffen die Behandlung von Zeilenumbrüchen unter Windows. An den Git-Einstellungen wurde nichts geändert.

## Kurzprotokoll für den Labor-Bericht

- **Gemacht:** Entwicklungsbranch angelegt und hochgeladen; Gesamtstimmenberechnung lokal ergänzt; fünf zusätzliche Tests ergänzt; Tests laut Markus erfolgreich.
- **KI genutzt:** Bestehenden Code analysiert; ORM-Abfrage und Testfälle vorbereitet; lokale Dateien geändert; Syntax geprüft; Anleitungen und Dokumentation formuliert. Git-/GitHub-Aktionen führt Markus selbst aus.
- **Gelernt – Formulierungsvorschlag:** `annotate()` ergänzt einzelne Fragen um berechnete Werte; `Sum()` fasst Stimmen der zugehörigen Antworten zusammen; `default=0` behandelt fehlende Antworten. Tests prüfen auch Grenzen und das Verhalten nach einer Abstimmung.
- **GitHub-Link:** Nach dem Push sind [View](https://github.com/joseluisrg/polls-alpha/blob/feature/poll-tiles-data/mysite/polls/views.py), [Tests](https://github.com/joseluisrg/polls-alpha/blob/feature/poll-tiles-data/mysite/polls/tests.py) und [dieses Protokoll](https://github.com/joseluisrg/polls-alpha/blob/feature/poll-tiles-data/docs/poll-tiles/02-total-votes.md) auf dem Datenbranch abrufbar. Den konkreten Commit-Link im abschließenden Labor-Bericht ergänzen.

Persönliche Lernergebnisse vor Übernahme mit der eigenen Erfahrung abgleichen.

## Screenshot-Nachweise

- Erfolgreiche Testausgabe einschließlich Testanzahl und abschließendem `OK`.
- Neue Berechnungszeile in der View, sofern für die Erklärung im Bericht hilfreich.
- GitHub-Commit mit Adresse und den drei geänderten Dateien.
- Eigener laufender Yellowdig-Beitrag mit Datum.

## Yellowdig-Entwurf

Auf meinem eigenen Datenbranch haben wir die Gesamtstimmenzahl je Poll-Frage ergänzt. Die View liefert jetzt `question.total_votes`, sodass Valeria den Wert in ihren Kacheln anzeigen kann. Fünf zusätzliche Tests decken normale Summen, null Stimmen, fehlende Antworten, die Auswahl der neuesten Fragen und die Aktualisierung nach einer Abstimmung ab. Die Tests habe ich erfolgreich ausgeführt. KI hat bei Umsetzung, Testentwurf und Dokumentation unterstützt. Als Nächstes folgen die gegenseitige Prüfung und die Integration mit Valerias Kachelansicht.
