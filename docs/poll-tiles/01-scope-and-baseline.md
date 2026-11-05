# Schritt 1 – Umfang, Datenübergabe und Ausgangszustand

Stand: 5. November 2026. Markus' Bestandsaufnahme ist durchgeführt. Der gemeinsame Meilenstein bleibt bis zu Valerias Rückmeldung offen.

## Vereinbarter Umfang

- Kacheln mit Fragetext, Veröffentlichungsdatum, Gesamtstimmenzahl und Link zum vorhandenen Abstimmungsformular.
- Einfache, lesbare Gestaltung; keine pixelgenaue Nachbildung erforderlich.
- Bisherige Auswahl: fünf neueste veröffentlichte Fragen; zukünftige Veröffentlichungen ausschließen.
- „New“ bleibt optional.
- Team: Valeria übernimmt Template und CSS; Markus Datenaufbereitung, Tests und Veröffentlichung. Beide prüfen gegenseitig und dokumentieren die eigene Arbeit. Valerias Bestätigung steht noch aus.

## Datenübergabe

| Name | Bedeutung |
|---|---|
| `latest_question_list` | Bestehende Liste der anzuzeigenden Fragen. |
| `question.id` | Kennung für den vorhandenen Link `polls:detail`. |
| `question.question_text` | Fragetext. |
| `question.pub_date` | Veröffentlichungsdatum. |
| `question.total_votes` | Geplante Summe der Stimmen aller zugehörigen Antwortmöglichkeiten; bei fehlenden Antwortmöglichkeiten `0`. Noch zu implementieren. |

## Prüfstatus

- Lokales Repository: Arbeitsverzeichnis vor der Dokumentationsänderung sauber; `main` nach erfolgreichem Abruf identisch mit `origin/main` (0 Commits Unterschied).
- Lokaler Interpreter: Python 3.14.10; Django 5.2.18. Mit dem projektspezifischen Interpreter gemessen, ohne Projektsettings zu importieren.
- Testfragen lokal: vorhandene SQLite-Datenbank ausschließlich lesend geprüft; 0 Fragen, 0 veröffentlichte Fragen und 0 Antwortmöglichkeiten. Testdaten sind noch anzulegen.
- PythonAnywhere: Python 3.13 und virtuelle Umgebung `mysite-venv` laut bestätigten Angaben und Screenshots; keine neue Messung in diesem Schritt.
- Öffentliche Seite erneut im Browser geprüft: https://markusruppnig.pythonanywhere.com/polls/ – „No polls are available.“ Die Ansicht wurde als Browserbild im Chat festgehalten.
- Valerias Entwicklungsumgebung und Zustimmung zur Aufteilung: laut Markus noch offen; er sendet ihr die Unterlagen nach Schritt 1.
- Ausgangsscreenshot mit sichtbarer Adresszeile: zusätzlich von Markus zu sichern; noch nicht als erledigt bestätigt.
- Anwendungscode statisch geprüft: bisherige Linkliste, Fragenfilter, Modellfelder und URL-Namen passen zur vereinbarten Datenübergabe. `total_votes` existiert noch nicht.
- Keine Django-Anwendungstests in diesem Schritt ausgeführt; keine Projektsettings geladen und keine Datenbank verändert.

## Testfragen für die spätere Abnahme

Nur synthetische Daten in der jeweiligen Entwicklungsumgebung verwenden. Vorhandene Daten nicht löschen oder ersetzen.

| Fall | Testdaten | Erwartung nach Umsetzung |
|---|---|---|
| Normale Frage | Veröffentlichte Frage; drei Antworten mit 2, 3 und 0 Stimmen | Kachel zeigt 5 Gesamtstimmen. |
| Zweite Frage | Andere veröffentlichte Frage; beispielsweise 1 Stimme | Eigene Summe bleibt getrennt von der ersten Frage. |
| Null Stimmen | Veröffentlichte Frage; Antworten jeweils mit 0 Stimmen | Kachel zeigt 0. |
| Langer Text | Veröffentlichte Frage mit langem Fragetext | Text bleibt lesbar. |
| Zukunft | Veröffentlichungsdatum in der Zukunft | Keine Kachel in der Übersicht. |

Die leere Fragenliste wird in einer unabhängigen Testdatenbank geprüft. Für ihren Nachweis keine vorhandenen Fragen löschen. Die Gesamtstimmenanzeige gehört erst zu den späteren Umsetzungsschritten.

## Screenshots

1. Jetzt: bisherige lokale oder öffentliche Polls-Ansicht mit Adresszeile; Dateiname beispielsweise `01_ausgangsansicht.png`.
2. Nach Versionsprüfung: Ausgabe mit Python- und Django-Version; keine Geheimnisse oder Umgebungsvariablen fotografieren.
3. Nach Prüfung beziehungsweise Anlage synthetischer Fragen: bisherige Fragenliste, weiterhin ohne Kacheln.
4. Nach Speicherung auf GitHub: Commit beziehungsweise geänderte Dokumentationsdatei mit sichtbarer Adresse.
5. Nach dem eigenen Yellowdig-Beitrag: Beitrag mit Datum und Text sichern.

## Kurzprotokoll für den Labor-Bericht

- Gemacht: Funktionsumfang und Datenübergabe festgelegt; lokale Versionen gemessen; GitHub-Stand abgeglichen; vorhandene Datenbank lesend geprüft; öffentliche Ausgangsansicht kontrolliert.
- KI genutzt: Anforderungen strukturiert; Code statisch geprüft; Versions- und Datenbestandsprüfung durchgeführt; Datenübergabe, Prüffälle und Dokumentation vorbereitet.
- Lerninhalt: Stimmen werden je Antwort gespeichert und für eine Frage summiert; View und Template müssen dieselben Datenbezeichnungen verwenden; lokale und öffentliche Umgebung sind getrennt.
- Noch offen: Eigener Screenshot mit Adresszeile, veröffentlichte Testfragen und Valerias Bestätigung ihrer Aufgaben und Umgebung. Der persönliche Lernergebnis-Text ist vor Übernahme mit der eigenen Erfahrung abzugleichen.
- GitHub-Dokumentation: [Schritt 1 – Umfang und Ausgangszustand](https://github.com/joseluisrg/polls-alpha/blob/docs/poll-tiles-step-1/docs/poll-tiles/01-scope-and-baseline.md).

## Entwurf für Yellowdig

Wir haben den Umfang unserer Polls-Erweiterung festgelegt: Fragen sollen als einfache Kacheln mit Datum und Gesamtstimmenzahl erscheinen. Die Datenübergabe ist festgelegt, insbesondere `total_votes` als künftig berechnete Summe pro Frage. Mein lokaler Stand ist mit GitHub abgeglichen; gemessen wurden Python 3.14.10 und Django 5.2.18. Die lokale Datenbank enthält noch keine Fragen; auch die öffentliche Seite zeigt eine Leermeldung. KI hat bei Anforderungsstrukturierung, statischer Codeprüfung, Bestandsaufnahme und Dokumentation unterstützt. Offen sind Testfragen und Valerias Bestätigung ihrer Aufgaben und Umgebung. Die Kachelfunktion ist noch nicht implementiert.

## Kurze Mitteilung an Valeria

Hallo Valeria, die Bestandsaufnahme für unsere Polls-Kacheln ist dokumentiert. Der Umfang: Frage, Datum, Gesamtstimmenzahl und Link zum Abstimmungsformular; „New“ bleibt optional. Vorgeschlagen ist: du Template und CSS, ich Datenaufbereitung, Tests und Veröffentlichung. Die Fragenliste heißt weiterhin `latest_question_list`; die Gesamtstimmen liefere ich als `question.total_votes`. Bitte bestätige kurz die Aufteilung und ob du deine Polls-Anwendung starten kannst. Prüfe dabei deine Python- und Django-Version sowie vorhandene Testfragen. Bei mir sind Python 3.14.10 und Django 5.2.18 gemessen; meine lokale Datenbank ist noch leer. Bitte sichere auch deine Ausgangsansicht und dokumentiere deinen Schritt einschließlich KI-Nutzung und Lernergebnis. Wir speichern kleine Schritte auf eigenen GitHub-Branches und prüfen gegenseitig. Ziel bleibt: Freitag online, Samstag Bericht fertig, Montagabend Abgabe.
