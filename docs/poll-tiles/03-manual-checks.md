# Schritt 3 – Manuelle Prüfung der Gesamtstimmen

**Verantwortlich:** Markus

**Datum:** 5. November 2026

**Geprüfter Code:** [Merge-Commit c6bd3c5](https://github.com/joseluisrg/polls-alpha/commit/c6bd3c5)

**Status:** Manuelle Datenprüfung erfolgreich abgeschlossen. Markus bestätigt die Werte 1, 0 und 0; die anschließend übermittelte PowerShell-Ausgabe belegt sie. GitHub-Link zu dieser neuen Dokumentation ausstehend. Die Kachelansicht ist noch nicht integriert; laut Markus liegt noch kein UI-Pull-Request vor.

## Ziel und Ablauf

- Die Datenaufbereitung mit eigenen Entwicklungsdaten prüfen, während Valeria unabhängig am Kachel-Template und CSS arbeitet.
- Drei veröffentlichte Fragen über die vorhandene Linkliste aufrufen.
- Die tatsächlich implementierte `IndexView.get_queryset()` über die Django-Shell auslesen.
- Eine zusätzliche Abstimmung für Book bei Frage 1 ausführen und die View erneut auslesen.

## Bestätigte Anfangswerte

| Frage | Gespeicherte Antwortmöglichkeiten | Summe in der View |
|---|---|---:|
| 1: Which learning style do you prefer? | Book: 0; Video: 0; Practice: 0 | 0 |
| 2: When do you prefer to study? | Zwei Antworten mit jeweils 0 Stimmen | 0 |
| 3: Lange Frage zum Lernen eines neuen Django-Konzepts | Zwei Antworten mit jeweils 0 Stimmen | 0 |

Nachweise: Markus' übermittelte PowerShell-Ausgabe und eine zusätzliche ausschließlich lesende SQLite-Prüfung durch Codex. Der Fragenlisten-Screenshot zeigt alle drei Fragen und die Adresse `/polls/`.

Die anfänglich vorgeschlagene Summe 5 beruhte auf geplanten Antwortstimmen von 2 und 3. Tatsächlich waren alle gespeicherten Stimmen 0; daher wurde die manuelle Prüferwartung an den realen Anfangsstand angepasst.

## Prüfung nach einer Abstimmung

- Erwartung: genau eine zusätzliche Stimme für Book ergibt Book: 1 und `total_votes=1` bei Frage 1.
- Fragen 2 und 3 sollen weiterhin `total_votes=0` liefern.
- Ergebnis: Die erneut ausgelesene View liefert für Frage 1 `total_votes=1`, für Fragen 2 und 3 jeweils `total_votes=0`. Erwartung und gemessene Gesamtstimmen stimmen überein.
- Ausführung: Markus hat den Django-Shell-Befehl in seiner lokalen Windows-Entwicklungsumgebung ausgeführt und die Ausgabe übermittelt. Codex hat die Ausgabe geprüft, den Befehl in diesem Schritt aber nicht selbst ausgeführt.

| Frage | Vor der Abstimmung | Danach | Ergebnis |
|---|---:|---:|---|
| 1: Bevorzugte Lernform | 0 | 1 | Erhöhung um 1 bestätigt |
| 2: Bevorzugte Lernzeit | 0 | 0 | Unverändert bestätigt |
| 3: Lange Frage | 0 | 0 | Unverändert bestätigt |

Die manuelle Prüfung belegt die Datenaufbereitung mit diesen Beispielen. Darstellung und Verknüpfungen der neuen Kacheln werden nach Valerias UI-Integration gesondert geprüft. Automatisierte Tests wurden in diesem Dokumentationsschritt nicht erneut ausgeführt.

## Tatsächlich aufgetretene Hindernisse

- Die Startadresse `/` lieferte 404; unter dem eingerichteten Pfad `/polls/` waren die Fragen sichtbar.
- Nach geschlossenem Serverfenster meldete der Browser `ERR_CONNECTION_REFUSED`. Die Anleitung wurde klargestellt: ein PowerShell-Fenster bleibt mit dem Server geöffnet; ein zusätzliches Fenster dient den Prüfkommandos.
- Der vorhandene lokale Adminzugang konnte nach Erinnerung an das Passwort verwendet werden; eine Passwortänderung war nicht nötig.

## Screenshot-Nachweise

- Bisherige Fragenliste mit sichtbarer Adresse: bereits an Codex übermittelt und lokal gesichert.
- Vorher-Ausgabe mit den drei Summen 0: von Markus zu sichern.
- Nachher-Ergebnis und View-Ausgabe mit 1, 0 und 0: jetzt sichern; die Textausgabe liegt Codex bereits vor. Markus meldet die vorherigen Aufgaben als erledigt; neue Screenshot-Dateien wurden Codex nicht übermittelt.
- Verbindungsablehnung als Entwicklungsproblem: Screenshot bereits übermittelt und lokal gesichert.
- Eigener laufender Yellowdig-Beitrag mit Datum: nach Veröffentlichung sichern.

## Kurzprotokoll für den Labor-Bericht – aktueller Stand

- **Gemacht:** Drei eigene Testfragen geprüft; Ausgangssummen 0, 0 und 0 bestätigt; nach einer Abstimmung Gesamtstimmen erneut ausgelesen: 1, 0 und 0; manuelle Datenprüfung bestanden.
- **KI genutzt:** Prüfschritte, Befehle und erwartete Ergebnisse vorbereitet; Screenshot und Ausgaben eingeordnet; Daten lesend geprüft; missverständliche Fensteranleitung korrigiert; Dokumentation vorbereitet.
- **Gelernt – Formulierungsvorschlag:** Die View kann unabhängig vom Template geprüft werden. Erwartungen hängen von tatsächlichen Anfangsdaten ab. Der lokale Webserver benötigt ein weiter geöffnetes Serverfenster.
- **GitHub-Link:** [Geprüfte Gesamtstimmenberechnung](https://github.com/joseluisrg/polls-alpha/commit/c6bd3c5). Ein neuer Commit zur manuellen Prüfdokumentation wurde noch nicht erstellt.

Persönliche Lernergebnisse vor Übernahme abgleichen. Die Testdaten bleiben in der lokalen Datenbank; für diesen Dokumentationsschritt wird nur diese Markdown-Datei zum Commit ausgewählt.

## Yellowdig-Entwurf

Während Valeria an der Kachelansicht arbeitet, habe ich die Gesamtstimmenberechnung mit drei eigenen Testfragen geprüft. Anfangs lieferte die View dreimal 0; nach einer Abstimmung waren es 1, 0 und 0. Die Datenaufbereitung funktioniert damit auch unabhängig von der neuen Darstellung. Ein zwischenzeitliches Problem entstand durch ein geschlossenes Serverfenster; jetzt bleiben Server und Prüfkommandos in zwei getrennten PowerShell-Fenstern. KI unterstützte bei Prüfschritten, der Einordnung der Ausgaben und der Dokumentation. Die gemeinsame Prüfung der Kacheln folgt nach dem UI-Pull-Request.

## Nächster Meilenstein

- Markus speichert diese Prüfdokumentation selbst auf GitHub und ergänzt den tatsächlichen Commit-Link im Labor-Bericht beziehungsweise Yellowdig-Beitrag.
- Valeria stellt ihre Oberfläche als Pull Request bereit; Markus prüft anschließend Datum, Gesamtstimmen, lange Fragetexte und Abstimmungslinks.
- Vollständige Kachelfunktion und Veröffentlichung auf PythonAnywhere sind noch offen.
