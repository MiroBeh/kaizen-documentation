# Kaizen — Prototype / MVP

> **Zweck dieses Dokuments:** Arbeitsdokument für den technischen Prototypen. Hier definieren wir den Weg vom Konzept zu einem funktionierenden MVP — zunächst als **Single-User-System** (nur der Projekt-Owner selbst als User), um die Vision erlebbar zu machen und mit Anderen teilen zu können.
>
> **Status:** Planung (noch keine Implementierung gestartet)
> **Referenz-Dokumente:** `vision.md`, `onboarding.md`, `economics.md`, `rules.md`

---

## 1. Zielsetzung des Prototyps

### 1.1 Was der Prototyp leisten soll
- **Die Vision erlebbar machen** — nicht nur auf Papier diskutieren, sondern selbst erfahren
- **Coaching-Beziehung mit Milo im Alltag testen** — über Wochen, nicht nur Minuten
- **Lernen, welche Features wirklich funktionieren** und welche Ideen aus der Vision sich anders anfühlen als gedacht
- **Greifbare Grundlage zum Teilen** — Freunden, potenziellen Mitstreitern, Investoren zeigen können: "So fühlt sich das an"

### 1.2 Was der Prototyp NICHT sein muss
- Kein Multi-User-System
- Keine Authentifizierung, Payments, Accounts
- Keine polierte UI
- Keine skalierbare Cloud-Infrastruktur
- Kein Human-in-the-Loop-System
- Keine produktionsreife Regel-Lern-Mechanik
- Kein WhatsApp Business API

### 1.3 Warum Single-User der richtige Start ist
- **Dramatisch einfacher zu bauen** — viele Komplexitätsebenen fallen weg
- **Schnellster Weg zum Erkenntnisgewinn** — in wenigen Wochen im Alltag einsetzbar
- **Echte Nutzung schlägt Planung** — jede Minute Eigennutzung bringt mehr Einsichten als stundenlanges Brainstorming
- **Gute Story für später** — "Ich lasse mich seit X Wochen von meinem eigenen AI-Coach trainieren" ist überzeugender als jedes Konzept-Dokument

---

## 2. Technologie-Entscheidungen

### 2.1 Primäre Sprache: Go
Die Entscheidung fiel auf Go, weil:
- Flüssige Sprachbeherrschung (Senior-Level) = maximale Geschwindigkeit beim Bauen
- Minimaler Overhead/Boilerplate für kleine Services
- Deployment trivial (statisches Binary auf VPS)
- Gute LLM-SDK-Unterstützung (`anthropic-sdk-go`)
- Concurrency-Modell ideal für proaktive Checks in späteren Phasen

### 2.2 Hinweis: Python als mögliche Ergänzung in Zukunft
Python wird **bewusst nicht ausgeschlossen**. Es könnte später hinzugezogen werden, insbesondere für:
- Intensive Arbeit mit Vector Stores, Embeddings und RAG-Pipelines (LangChain, LlamaIndex)
- Data Science / Analyse von Nutzungsdaten
- ML-spezifische Komponenten

**Aktueller Stand:** Für den MVP nicht benötigt. Regelbasis und persönliche Historie passen komplett in den System-Prompt bzw. in einfache Dateien. Bei späterer Skalierung kann ein Python-Service für spezifische Aufgaben ergänzt werden — die Sprachen lassen sich über REST/gRPC problemlos kombinieren.

### 2.3 Vorläufiger Stack
| Komponente | Technologie | Begründung |
|---|---|---|
| Sprache | Go | s.o. |
| LLM-Anbindung | Claude API via `anthropic-sdk-go` | Gute SDK, lange Kontextfenster, gutes Memory-Handling |
| Frontend/Chat | Telegram-Bot (via `tucnak/telebot` oder `go-telegram/bot`) | Kostenlos, in Minuten aufgesetzt, auf Handy + Desktop, Messenger-Gefühl |
| Persistenz | SQLite (via `mattn/go-sqlite3`) oder einfache JSON/YAML-Dateien | Simpel, kein Infra-Overhead, reicht für Single-User |
| Scheduling (ab Phase 3) | Cron oder Go-interne Timer/Goroutines | Für proaktive Checks |
| Deployment | Kleiner VPS (z.B. Hetzner, DigitalOcean, ~5€/Monat) oder lokal | Reicht komplett für Single-User |

### 2.4 Offene Technologie-Entscheidungen
- [ ] Vector Store — noch nicht nötig, aber irgendwann: Pinecone, Weaviate, Qdrant oder lokal?
- [ ] Strukturierte Daten-Eingabe: Telegram-Bot-Commands, simple Web-Form, Google Sheet/Notion-Integration?
- [ ] Wenn später Web-UI: Go-nativ (Templ, HTMX) oder separates Frontend?

---

## 3. Die 4 MVP-Phasen

Der Prototyp wird in **4 inkrementellen Phasen** gebaut. Jede Phase ist für sich nutzbar und liefert direkten Erkenntnisgewinn — kein Big-Bang-Launch nötig.

---

### Phase 1 — "Milo im Chat" (1-2 Wochenenden)

**Ziel:** Du kannst mit Milo chatten, er kennt dich, erinnert sich an Gespräche.

**Was gebaut wird:**
- Claude API Anbindung mit definiertem System-Prompt (Milos Persönlichkeit, Coaching-Philosophie)
- Telegram-Bot als Chat-Frontend
- Persistente Konversations-Historie in SQLite oder JSON
- `profile.md` mit persönlichen Daten (Ziele, Historie, Equipment, Verletzungen) — wird Milo als Kontext mitgegeben
- **Globale Regelbasis als Kernkomponente** — siehe eigenes Dokument `global-rules.md`. Startet mit 20-30 kuratierten Beispielregeln über alle Kategorien hinweg. Wird Milo als Wissensbasis bereitgestellt — Mechanismus dazu siehe Abschnitt 4.

**Was sofort getestet werden kann:**
- Wie fühlt sich die Beziehung zu Milo an?
- Wie gut erinnert er sich an vergangene Gespräche?
- Welche Fragen stellt er gut, welche schlecht?
- Welcher Kommunikationsstil funktioniert? Lang? Kurz? Emojis? Voice?
- Wie gut funktioniert der System-Prompt? Wo bricht Milo aus der Rolle?

**Definition of Done:**
- Chat mit Milo über Telegram funktioniert
- Milo hat Zugriff auf `profile.md` und Gesprächshistorie
- Du kannst Milo an mindestens 3 Tagen in Folge nutzen, ohne dass etwas bricht

---

### Phase 2 — "Milo kennt deine Trainingsdaten" (2-3 Wochenenden)

**Ziel:** Milo kann auf Trainings- und Gesundheitsdaten zugreifen und darauf Bezug nehmen.

**Was gebaut wird:**
- Einfaches Tracking-Interface — Optionen:
  - Telegram-Bot-Commands (`/gewicht 82.5`, `/training`)
  - Simple Web-Form mit Go-HTTP-Server
  - Google Sheet / Notion-API-Integration
- Milo kann Daten vor jeder Antwort lesen
- Tracking-Felder (vollständige Spezifikation in **`data-inputs.md`**):
  - **Täglich** (Tier 2): Körpergewicht, Schlafstunden, Energie-Level (1–5)
  - **Per Session** (Tier 3): Übung, Sätze, Reps, Gewicht, Session-Gefühl (1–5)
  - **Tägliche Ernährungs-Adherence** (Tier 4): Plan eingehalten? → Wenn Nein: Was war anders + wie weit weg?
  - **Wöchentlicher Check-in** (Tier 5): Gesamt-Sentiment, Trainings-Adherence, Ernährungs-Adherence, Plan-Feedback

**Was sofort getestet werden kann:**
- Welche Daten sind wirklich nützlich für das Coaching?
- Wo ist die Grenze zu "Tracking-Wahn"?
- Nervt die Dateneingabe, oder ist sie okay?
- Wie nutzt Milo die Daten im Gespräch? Erkennt er Zusammenhänge?

**Prinzip:** Bewusst minimalistisch. Nicht 20 Datenpunkte tracken, nur die, die für die Kernvision wirklich gebraucht werden. Erweiterung jederzeit möglich.

**Definition of Done:**
- Datenerfassung über mindestens einen Kanal funktioniert reibungslos
- Milo liest Daten automatisch und nimmt im Chat darauf Bezug
- Mindestens 1 Woche echte Nutzung hinter sich

---

### Phase 3 — "Milo wird proaktiv" (1-2 Wochenenden)

**Ziel:** Milo meldet sich von selbst — morgens, nach Training, bei Anomalien.

**Was gebaut wird:**
- Scheduled Jobs (Cron oder Go-Timer), die Milo triggern
- Einfache Anomalie-Erkennung:
  - "Letzte 3 Tage kein Training eingetragen"
  - "Gewicht +X kg / -X kg in Y Tagen"
  - "Trainingsleistung bricht ein"
- Milo bekommt Trigger und entscheidet, ob und wie er reagiert
- Optional: Feste morgendliche/abendliche Check-ins

**Was sofort getestet werden kann:**
- Wie viel Proaktivität ist angenehm, wann wird sie nervig?
- Welche Trigger sind wirklich wertvoll, welche sind Lärm?
- Wie gut ist Milos Dosierung und Timing?
- Wie reagiere ich emotional auf unerwartete Nachrichten?

**Definition of Done:**
- Mindestens 3 verschiedene Trigger-Typen implementiert
- Milo meldet sich proaktiv über mindestens 2 Wochen
- Bewertung: funktioniert oder muss angepasst werden

---

### Phase 4 — "Milo passt Pläne an" (2-3 Wochenenden)

**Ziel:** Milo erstellt und passt den Trainingsplan aktiv an.

**Was gebaut wird:**
- Plan-Struktur in einer Datei, die Milo lesen und schreiben kann (z.B. `training_plan.md` oder YAML)
- Milo kann Plan-Vorschläge machen, User bestätigt, Plan wird aktualisiert
- Template-Basis für initiale Plan-Erstellung (einfache Vorlagen für verschiedene Ziele)
- Plan-Historie (alle Versionen werden erhalten für späteres Lernen)

**Was sofort getestet werden kann:**
- Funktioniert die versprochene Flexibilität wirklich?
- Sind Milos Anpassungen sinnvoll oder willkürlich?
- Vertraue ich seinen Entscheidungen?
- Wie gut kann Milo das Warum hinter Anpassungen erklären?

**Definition of Done:**
- Milo hat mindestens einmal einen Plan erstellt und mindestens dreimal angepasst
- User (Projekt-Owner) trainiert nachweislich nach Milos Plan
- Die "Wow-Effekt Flexibilität" ist erlebbar — oder es ist klar, was fehlt

---

## 4. Globale Regelbasis (Kernkomponente)

Die globale Regelbasis ist **kein Nebenelement, sondern eines der Herzstücke** des Prototyps. Ohne sie wäre Milo nur "ein Chatbot mit Coaching-Persönlichkeit" — die Regelbasis ist das, was Milo von einem generischen LLM-Chat unterscheidet. Sie repräsentiert kondensiertes Coaching-Wissen.

**Eigenes Dokument:** `global-rules.md`

### 4.1 Ziel im MVP
- **Starter-Set: 20-30 kuratierte Regeln** über alle Kategorien hinweg
- Genug Substanz, um Milos Coaching-Qualität realistisch zu testen
- Genug Spielraum, um durch Nutzung organisch zu wachsen

### 4.2 Kategorien (Erstdefinition, später zu schärfen)
- **Trainingsdiagnostik** — Plateau-Erkennung, Volumen-Anpassung, Übertraining-Symptome
- **Ernährungsdiagnostik** — Heißhunger-Patterns, Stagnation, Wassergewicht-Schwankungen
- **Recovery & Lifestyle** — Schlaf, Stress, Krankheit/Reise-Anpassungen
- **Mentale & Beziehungs-Themen** — Rückschläge, Erwartungssteuerung, Motivationskrisen
- **Sicherheit & Grenzen** — Wann an Arzt/Physio/Ernährungstherapeut/Psycholog:in verweisen, Red Flags

> **Hinweis:** Kategorien-Schema ist erste Version. Genaue Definition, Granularität und Tagging-System müssen später iteriert werden.

### 4.3 Token-Effizienz (kritisches Architektur-Thema)

**Problem:** Wachsende Regelbasis → bei jedem API-Call wird ein riesiger Block Text mitgeschickt → Kosten explodieren, Latenz steigt, Kontextfenster wird verbraucht.

**Lösungsansätze (zu evaluieren):**

| Ansatz | Idee | Wann sinnvoll |
|--------|------|---------------|
| **Prompt Caching** | Statischen Block (System-Prompt + Regelbasis) cachen, nur dynamische Teile pro Call neu | Sofort umsetzbar, größter Effekt bei stabiler Regelbasis |
| **Selective Loading** | Nur Regeln laden, deren Kategorie zur User-Nachricht passt (Klassifikation vorab) | Bei wachsender Regelbasis (>50 Regeln) |
| **Vector-basierte Retrieval (RAG)** | Embeddings über Regeln, nur relevanteste laden | Bei großer Regelbasis (>200+ Regeln) |
| **Hierarchisches Setup** | Kern-Regeln immer dabei + situative Spezialregeln nach Bedarf | Mittlere Phase |
| **Summarization-Layer** | Kompakte Regel-Zusammenfassung als Default, Vollversion bei Bedarf | Wenn Regeln sehr ausführlich werden |

**Strategie für den MVP:** Bei 20-30 Regeln passt alles ohne Probleme in den Kontext. Prompt Caching ab Tag 1 nutzen. Selective Loading + RAG werden Themen, sobald die Regelbasis wächst — nicht jetzt vorzeitig optimieren.

### 4.4 Format einer Regel (vorläufig)
Jede Regel hat:
- **Trigger / Situation** — wann ist die Regel relevant?
- **Vorgehen / Diagnostik** — was macht Milo damit?
- **Begründung** — warum macht er das (Wissensgrundlage)?
- Optional: Beispiele, Tags, verwandte Regeln

Konkrete Format-Festlegung erfolgt in `global-rules.md`.

### 4.5 Offene Punkte zur Regelbasis (Parkliste)
- [ ] Kategorien-Schema final definieren (welche Kategorien, wie granular?)
- [ ] Tagging-System für Regeln (für Selective Loading später)
- [ ] Token-Strategie schärfen, sobald Regelbasis wächst
- [ ] Format-Entscheidung treffen (Markdown vs. YAML vs. Mischform)
- [ ] Versionierung der Regelbasis (Git? Eigene Versionsnummern?)
- [ ] Qualitätssicherung des Starter-Sets (eigenes Wissen vs. Coach hinzuziehen)

---

## 5. Nach den 4 Phasen — was dann?

### 5.1 Evaluation
Nach Abschluss aller Phasen (realistisch: 6-10 Wochenenden, gestreckt über 2-3 Monate je nach Zeit) gibt es eine Evaluations-Runde:
- Was funktioniert in der Vision so wie gedacht?
- Was muss anders?
- Was fehlt völlig?
- Welche Kern-Differenzierer tragen wirklich?

### 5.2 Mögliche nächste Schritte
- **Zweiter Test-User** (Freund / Familie) — testen, ob Milo auch mit anderen Charakteren funktioniert
- **Multi-User-Architektur** beginnen — Auth, User-Trennung, saubere Datenhaltung
- **Regel-Lern-Prototyp** — erstes Human-in-the-Loop-Experiment
- **Pitch / Konzept-Sharing** — Vision mit echten Erfahrungen unterfüttert zeigen
- **Entscheidung:** Hobby weiterführen, Co-Founder suchen, Investment anstreben

---

## 6. Aktuelle To-Do-Liste für Phase 1

Konkrete nächste Schritte, um loszulegen:

- [ ] Claude API Account einrichten, API Key besorgen
- [ ] Telegram Bot über @BotFather erstellen, Token sichern
- [ ] Go-Projekt aufsetzen (Module, Struktur)
- [ ] SDK-Abhängigkeiten integrieren (`anthropic-sdk-go`, Telegram-Library)
- [ ] System-Prompt für Milo entwerfen — Persönlichkeit, Coaching-Philosophie, Grundregeln
- [ ] `profile.md` mit eigenen Daten erstellen (Ziele, Historie, Equipment, Verletzungen)
- [ ] **`global-rules.md` aufsetzen** — Format definieren, Kategorien festlegen, 20-30 Starter-Regeln entwerfen
- [ ] **Regelbasis-Loading-Mechanismus implementieren** — Regeln in System-Prompt-Kontext integrieren, Prompt Caching aktivieren
- [ ] Basis-Chat-Flow bauen (Nachricht rein → Context zusammenbauen → Claude API → Antwort raus → Historie speichern)
- [ ] Konversations-Historie persistent speichern
- [ ] Deployment-Setup (VPS oder lokal mit Tunnel)
- [ ] Erster echter Test: 3 Tage in Folge mit Milo chatten

---

## 7. Risiken und offene Fragen

### 7.1 Technische Risiken
- **Kontextfenster-Management:** Wann wird die Historie zu lang? Wie summarized man alte Gespräche, ohne Kontext zu verlieren?
- **Milo bleibt in seiner Rolle:** Wie robust ist der System-Prompt gegen Abschweifungen?
- **Ton trifft nicht:** Milo könnte zu generisch oder zu aufdringlich wirken — braucht iteratives Tuning
- **Token-Kosten der Regelbasis:** Bei wachsender Regelbasis Kostenrisiko — Token-Strategie muss früh greifen

### 7.2 Konzeptionelle Risiken
- **Vision fühlt sich anders an als gedacht:** Der ganze Sinn des MVP ist, das herauszufinden — positiv gemeint
- **Proaktivität nervt:** Möglich, dass die "proaktive Milo"-Idee im Alltag anders wirkt als im Konzept
- **Plan-Anpassungen wirken unsicher:** Trotz guter Kommunikation könnten häufige Änderungen irritieren
- **Regelbasis-Qualität:** Schlechte oder zu generische Regeln führen zu schlechtem Coaching — Qualität der Starter-Regeln ist entscheidend

### 7.3 Offene Fragen
| # | Frage | Phase |
|---|-------|-------|
| 1 | Wie verwaltet Milo wachsende Konversations-Historie ohne Kontextlimits zu sprengen? | 1 |
| 2 | Welches Dateiformat für Regelbasis — Markdown, YAML, JSON, Mischung? | 1 |
| 3 | Wie integrieren wir die Regelbasis token-effizient in den Kontext? | 1 |
| 4 | Welcher Weg der Dateneingabe fühlt sich im Alltag am besten an? | 2 |
| 5 | Welches Trigger-System für proaktive Checks — Cron oder ereignisbasiert? | 3 |
| 6 | Wie strukturiert sich ein Plan, damit Milo ihn gut lesen und verändern kann? | 4 |

---

## 8. Annahmen-Tracker

| Annahme | Aktueller Wert | Status |
|---------|----------------|--------|
| Phase 1 schafft man in 1-2 Wochenenden | Schätzung | zu validieren |
| Single-User-Setup reicht für alle Kernerkenntnisse | Schätzung | zu validieren |
| Telegram ist das richtige Frontend für den MVP | Entscheidung | kann später angepasst werden |
| Claude API ist das richtige LLM für den MVP | Entscheidung | kann später gewechselt werden |
| SQLite / Dateien reichen für Persistenz | Entscheidung | kann später gewechselt werden |
| Kein Vector Store im MVP nötig | Annahme | zu validieren, wahrscheinlich korrekt |
| 20-30 Regeln im Kontext sind tokenmäßig unkritisch | Annahme | zu validieren in Praxis |
| Prompt Caching reduziert Kosten der Regelbasis ausreichend | Annahme | zu validieren |

---

## 9. Nächste Schritte (für dieses Dokument)

1. Entscheidung: Wann wird Phase 1 gestartet?
2. `global-rules.md` aufsetzen und mit Starter-Regeln befüllen
3. Konkretes System-Prompt-Design für Milo ausarbeiten (eigenes Dokument?)
4. Token-Strategie für Regelbasis konkretisieren (Prompt Caching als erstes)
5. Nach Phase 1: Lessons Learned hier dokumentieren, Plan für Phase 2 verfeinern