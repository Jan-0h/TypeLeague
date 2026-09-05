# TypeLeague

Eine Web-App zum Tippen lernen – mit Trainings-Levels, Übungsmatches gegen Bots
und kompetitiven 1-gegen-1-Matches in Echtzeit gegen andere Spieler.

> Schulprojekt (IMS), März – Juni 2026

---

## Features

- **Roadmap** – 10 aufeinander aufbauende Levels. Ein Level wird freigeschaltet,
  sobald das vorherige abgeschlossen ist. Der Fortschritt wird pro Benutzer gespeichert.
- **Training** – Rennen gegen einen Bot mit einstellbarem Tempo (30 / 60 / 100 WPM
  oder ein eigener Wert).
- **Liga** – Echtzeit-Match gegen einen anderen Spieler. Matchmaking über eine
  Warteschlange, danach Countdown, Live-Fortschrittsbalken des Gegners und
  Auswertung am Schluss.
- **ELO-System** – Jeder Sieg und jede Niederlage verändert die Wertung
  (Startwert 1000). Daraus ergeben sich fünf Ligen: Bronze, Silber, Gold, Platin,
  Diamant. Die Schwierigkeit der Wörter richtet sich nach der eigenen Liga.
- **Leaderboard** – Rangliste der Top 100 Spieler.
- **Statistiken** – WPM-Verlauf als Diagramm, Fehler, Zeiten und die letzten Matches.
- **Virtuelle Tastatur** – Schweizer QWERTZ-Layout, das die nächste Taste und den
  zuständigen Finger farblich anzeigt.
- **Drei Sprachen** – Deutsch, Englisch, Französisch.

---

## Tech Stack

| Bereich    | Verwendet                                 |
| ---------- | ----------------------------------------- |
| Frontend   | Vue 3 (Composition API), TypeScript, Vite |
| Routing    | Vue Router                                |
| Sprachen   | vue-i18n                                  |
| Datenbank  | Supabase (PostgreSQL)                     |
| Backend    | Node.js, Express (Login & Registrierung)  |
| Passwörter | bcrypt, Sessions via express-session      |

---

## Aufbau

```
TypeLeague/
├── src/
│   ├── components/          # Alle Seiten (Homepage, Liga, Training, Stats, ...)
│   │   └── gameboard.vue    # Tipp-Logik + virtuelle Tastatur
│   ├── i18n/                # Übersetzungen de / en / fr
│   ├── router/              # Routen inkl. Login-Schutz
│   ├── supabase.ts          # Supabase-Client
│   └── supabaseService.ts   # ELO-Berechnung, Resultate speichern
└── server/
    └── server.js            # Express-API für Login und Registrierung
createTypeLeague.sql         # Tabellen
InsertTypeLeague.sql         # Testdaten
```

---

## Datenbank

| Tabelle             | Inhalt                                            |
| ------------------- | ------------------------------------------------- |
| `users`             | Benutzer, Passwort-Hash, ELO, Sprache             |
| `levels`            | Die 10 Roadmap-Levels mit Text                    |
| `user_level`        | Welcher Benutzer welches Level geschafft hat      |
| `wordlist`          | Wörter nach Schwierigkeit und Sprache             |
| `matches` / `plays` | Matches und einzelne Resultate (WPM, Fehler, ELO) |
| `matchmaking_queue` | Warteschlange für die Liga-Matches                |

---

## Hinweise

- Die App ist für Desktop gedacht. Auf dem Handy erscheint ein Hinweis,
  da eine physische Tastatur benötigt wird.
- Für die Liga muss zuerst die komplette Roadmap abgeschlossen sein.
