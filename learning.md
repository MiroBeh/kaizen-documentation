# Kaizen — Learning Path (AI / LLM Grundlagen)

> **Zweck dieses Dokuments:** Strukturierter Lernpfad zum Aufbau von AI/LLM-Wissen parallel zur Prototyp-Entwicklung. Fokus auf das **Handwerk** — verstehen, was LLMs sind, wie man sie effektiv nutzt und wie man Systeme wie Kaizen konzipiert.
>
> **Status:** Erste Version (wird erweitert während des Lernens)
> **Referenz-Dokumente:** `vision.md`, `prototype.md`

---

## 1. Ausgangsbasis

| Parameter | Wert |
|-----------|------|
| Wissensstand LLMs | Stufe A (aktiver Nutzer, noch nichts selbst gebaut) |
| Lerntiefe | Pragmatisch-tief (Konzepte + Intuition, keine Transformer-Implementierung) |
| Zeitbudget | ca. 5-7h pro Woche |
| Format | Mix — Videos, Artikel, Code, Podcasts, Bücher |
| Sprache | Englisch (höhere Qualität und Aktualität der Ressourcen) |
| Geschätzte Dauer | 8-10 Wochen |
| Begleitend zu | Kaizen-Prototyp Phase 1-4 |

---

## 2. Lernstrategie

Drei Prinzipien für den Pfad:

**1. Intuition vor Formalismus.**
Erst verstehen, *was* ein LLM tut und *warum* es sich so verhält. Dann erst die Mechanismen. Mathe und Internals nur soweit nötig.

**2. Lernen + Anwenden im Wechsel.**
Nach jedem Modul direkt etwas im Kontext von Kaizen umsetzen. Keine trockene Theoriephase — Lernpfad läuft parallel zum MVP-Bau.

**3. Kuratiert, nicht vollständig.**
Wenige, hochwertige Ressourcen statt endloser Linklisten. Lieber zehn Dinge wirklich durcharbeiten als fünfzig anreißen.

---

## 3. Modul 1 — Was LLMs eigentlich sind

**Woche:** 1
**Zeitaufwand:** ~5-6h
**Ziel:** Mentale Grundlage. Du verstehst, was passiert, wenn du einen Prompt abschickst — ohne Mystifizierung, ohne Überkomplexität.

### Kernthemen
- Was LLMs wirklich sind: Wahrscheinlichkeits-Maschinen, nicht "denkende" Systeme
- Tokens, Vokabular, Wahrscheinlichkeitsverteilungen
- Warum LLMs halluzinieren und inkonsistent sind
- Grundlagen Training (Pretraining → Posttraining/RLHF) — nur konzeptionell
- Fähigkeiten und Grenzen

### Ressourcen
- **[Video]** Andrej Karpathy — *"Intro to Large Language Models"* (~1h, YouTube). **Pflicht.** Der beste Einstieg, der existiert. Karpathy ist ehemaliger OpenAI/Tesla, erklärt ohne Mystik. ✅ 
- **[Video]** 3Blue1Brown — *"But what is a GPT?"* (Neural Networks Serie, Episode 5-7). Visuell exzellent, hilft beim Intuitionsaufbau.
- **[Optional Deep-Dive]** Andrej Karpathy — *"Deep Dive into LLMs like ChatGPT"* (~3.5h). Nur wenn du nach dem ersten Video mehr willst.

### Kaizen-Bezug
Danach verstehst du, warum Milos System-Prompt so wichtig ist, warum Kontext Geld kostet und warum Halluzinationen ein reales Risiko sind, das wir aktiv managen müssen.

### Checkliste
- [x] Karpathys Intro-Video gesehen
- [ ] 3Blue1Brown Transformer-Episoden gesehen
- [ ] Ich kann in eigenen Worten erklären, was ein Token ist und warum es wichtig ist
- [ ] Ich kann erklären, warum LLMs halluzinieren

---

## 4. Modul 2 — Die API und erste Experimente

**Woche:** 2
**Zeitaufwand:** ~5-7h (parallel zu Prototyp-Phase 1!)
**Ziel:** Du hast die Claude API direkt im Griff. Ohne Framework, ohne Zwischenschicht. Du verstehst jeden Parameter.

### Kernthemen
- Anthropic Console, API Keys, Kostentracking
- Die Messages API — Requests, Responses, Stop Reasons
- System Prompts vs. User Messages vs. Assistant Messages
- Parameter: `temperature`, `max_tokens`, `top_p`, `top_k`
- Token Counting und Cost Calculation
- Streaming vs. Non-Streaming
- Rate Limits und Error Handling

### Ressourcen
- **[Docs]** Anthropic — *Getting Started with the Claude API* (docs.anthropic.com). Pflicht. Gut strukturiert, nicht zu lang.
- **[Docs]** Anthropic — *Messages API Reference*. Später bei jeder Gelegenheit reinspringen.
- **[Hands-on]** Anthropic Cookbook auf GitHub (github.com/anthropics/anthropic-cookbook). Beispiele in Python, Konzepte sind aber sprachagnostisch.
- **[Go-spezifisch]** `anthropic-sdk-go` auf GitHub — README + Beispiele durcharbeiten.

### Praktische Übungen
1. Erster API-Call in Go: "Hallo Welt" mit Claude
2. Mit `temperature` experimentieren: 0.0 vs. 0.7 vs. 1.0 bei derselben Frage
3. Einen längeren System-Prompt schreiben, der Claude eine Persönlichkeit gibt
4. Token Counting implementieren — wissen, was jede Anfrage kostet
5. Streaming-Antwort im Terminal ausgeben

### Kaizen-Bezug
**Das ist direkt Phase 1 des Prototyps.** Diese Woche baust du nicht nur Wissen, sondern legst das Fundament von Milo.

### Checkliste
- [ ] Anthropic Account eingerichtet, erster API-Call funktioniert
- [ ] Claude API Doku überflogen
- [ ] `temperature` und andere Parameter ausprobiert
- [ ] Token-Kosten für typische Anfrage berechnet
- [ ] Streaming funktioniert

---

## 5. Modul 3 — Prompt Engineering

**Woche:** 3-4
**Zeitaufwand:** ~6-8h/Woche
**Ziel:** Du kannst zuverlässig gute Ergebnisse aus Claude herausholen. Du weißt, wann welche Technik greift.

### Kernthemen
- System-Prompt-Design: Rolle, Tonalität, Regeln, Beispiele
- Clear and Direct Prompts (Anthropics Kernansatz)
- XML-Tags zur Strukturierung (Claudes Präferenz)
- Few-Shot Prompting — Beispiele im Prompt
- Chain-of-Thought (CoT) — Denk-Schritte erzwingen
- Structured Output (JSON, strukturierte Antworten)
- Prompt Caching — wichtig für deine Economics
- Prefilling — Claudes Antwort steuern
- Debugging: Warum antwortet Claude unerwartet?

### Ressourcen
- **[Docs]** Anthropic — *Prompt Engineering Guide* (docs.anthropic.com/en/docs/build-with-claude/prompt-engineering). **Pflicht, komplett.** Wahrscheinlich das beste Material, das es kostenlos gibt.
- **[Docs]** Anthropic — *Prompt Caching* Dokumentation. Wichtig für Kaizen-Kosten.
- **[Interactive]** Anthropic — *Prompt Engineering Interactive Tutorial* (GitHub). Hands-on, direkt im Notebook.
- **[Web]** DAIR.AI — *Prompt Engineering Guide* (promptingguide.ai). Ergänzend, breiter.
- **[Blog]** Simon Willison — *simonwillison.net*. Keine einzelne Seite, aber wer Simon regelmäßig liest, lernt kontinuierlich. Einfach RSS-Feed abonnieren.

### Praktische Übungen
1. Ersten ernsthaften System-Prompt für Milo entwerfen (Persönlichkeit, Regeln, Tonalität)
2. Mit Few-Shot-Beispielen arbeiten: Milo soll auf spezifische Situationen reagieren
3. XML-Tags zur Strukturierung einsetzen
4. Structured Output: Milo soll Trainingsdaten in JSON zurückgeben
5. Prompt Caching einbauen — große statische Teile cachen

### Kaizen-Bezug
**Das ist das Skill-Set, das Milos Qualität bestimmt.** Jede Stunde hier zahlt sich zehnfach aus. Der System-Prompt ist das Herz von Milo — gutes Prompt Engineering macht den Unterschied zwischen "peinlicher Chatbot" und "fühlt sich wie ein echter Coach an".

### Checkliste
- [ ] Anthropic Prompt Engineering Guide vollständig gelesen
- [ ] Interactive Tutorial abgeschlossen
- [ ] Erster vollständiger Milo-System-Prompt geschrieben
- [ ] Few-Shot-Beispiele integriert
- [ ] Structured Output mindestens einmal umgesetzt
- [ ] Prompt Caching verstanden und im Prototyp aktiviert

---

## 6. Modul 4 — Memory und Kontext-Management

**Woche:** 5-6
**Zeitaufwand:** ~6-8h/Woche
**Ziel:** Du verstehst, wie LLM-Systeme "sich erinnern". Du weißt, wann RAG Sinn macht und wann nicht. Du kannst für Kaizen bewusst entscheiden, was im Kontext landet.

### Kernthemen
- Das fundamentale Problem: LLMs haben kein persistentes Gedächtnis
- Strategien: Full Context, Rolling Window, Summarization, Selective Retrieval
- Retrieval Augmented Generation (RAG) — Grundprinzip
- Embeddings — was sie sind und wie sie funktionieren
- Vector Stores — was, wofür, wann?
- Kontextfenster-Management bei langen Gesprächen
- Memory-Systeme in der Praxis: Wie machen es ChatGPT, Claude, Character.ai?
- Abwägung: Wann RAG, wann alles in den Kontext, wann Fine-Tuning?

### Ressourcen
- **[Blog]** Simon Willison — *"Embeddings: What they are and why they matter"* (sehr guter Einstieg)
- **[Blog]** Anthropic — Artikel zu Claudes Memory-System (wenn gelesen: auch Hinweise zu deren Ansatz)
- **[Video]** Jason Liu — Talks zu RAG (YouTube). Praktiker, nicht Hype-getrieben.
- **[Paper-Light]** *"Retrieval Augmented Generation for Knowledge-Intensive NLP Tasks"* (Original RAG-Paper). Nicht vollständig lesen, aber Abstract + Intro + Conclusion.
- **[Guide]** Anthropic — *Long Context Prompting Tips* (Doku).
- **[Optional]** LangChain/LlamaIndex Docs — nur zum Konzepte-Verständnis, nicht zum aktiven Einsatz in Go.

### Praktische Übungen
1. Eine lange Konversation simulieren und sehen, wann Kontext zu groß wird
2. Einfache Summarization implementieren (alte Nachrichten zusammenfassen)
3. Embeddings-Playground: Text einbetten, Ähnlichkeit messen (sdk-go oder einfaches Python-Skript zum Spielen)
4. Architektur-Skizze: Wie würde Memory für Kaizen aussehen? (User-Profil, Konversations-Historie, Regelbasis, Daten)
5. Entscheidung treffen: Braucht der Kaizen-MVP einen Vector Store oder reicht strukturiertes Kontext-Management?

### Kaizen-Bezug
**Das ist die wichtigste konzeptionelle Entscheidungsphase für Kaizen-Architektur.** Hier entscheidest du, wie Milo sich erinnert — an Gespräche, an deine Daten, an die Regelbasis. Die Architektur-Entscheidungen hier prägen alles Weitere.

### Checkliste
- [ ] Ich kann erklären, was ein Embedding ist
- [ ] Ich verstehe RAG und weiß, wann es sinnvoll ist
- [ ] Ich habe eine Architektur-Skizze für Kaizen-Memory gemacht
- [ ] Entscheidung dokumentiert: Vector Store im MVP ja/nein

---

## 7. Modul 5 — Tool Use und Agents

**Woche:** 7-8
**Zeitaufwand:** ~5-7h/Woche
**Ziel:** Du verstehst, wie LLMs "handeln" können — Funktionen aufrufen, Tools benutzen, Pläne ausführen. Du kannst den Hype von der Substanz trennen.

### Kernthemen
- Tool Use / Function Calling — Grundprinzip
- Wie Claude entscheidet, welches Tool zu nutzen
- Multi-Step Tool Use
- Das Konzept von "Agents" — und warum die Definition unklar ist
- Wann Agents Sinn machen und wann nicht (meistens: nicht)
- Einfache Workflows vs. komplexe Agent-Loops
- Human-in-the-Loop als kritisches Sicherheitsmuster
- Praktische Agent-Patterns: ReAct, Plan-and-Execute, Reflection

### Ressourcen
- **[Pflichtlektüre]** Anthropic — *"Building Effective Agents"* (Anthropic Blog). Das beste öffentliche Dokument zum Thema. Schneidet durch den Hype.
- **[Docs]** Anthropic — *Tool Use* Dokumentation.
- **[Blog]** Simon Willison — diverse Artikel zu "LLM Agents" und deren Realität.
- **[Video]** Relevante Vorträge aus dem AI Engineer Summit auf YouTube — Session-Suche nach "Agents".
- **[Kritisch]** Suche gezielt nach Meinungen, die Agents skeptisch sehen — balance the hype.

### Praktische Übungen
1. Einfaches Tool Use mit Claude: Milo bekommt ein "Werkzeug" zum Lesen der Trainingsdaten
2. Multi-Tool-Setup: Milo kann Daten lesen UND Plan anpassen
3. Analyse: Sind die proaktiven Milo-Checks "Agent-Verhalten" oder nicht? Entscheidung dokumentieren.

### Kaizen-Bezug
**Relevant für Phase 3 und 4 des Prototyps.** Milos proaktive Checks und Plan-Anpassungen könnten als "Agent"-Muster gesehen werden. Wichtig: nicht dem Hype erliegen. Einfache Workflows sind oft besser als komplexe Agent-Loops.

### Checkliste
- [ ] "Building Effective Agents" von Anthropic vollständig gelesen
- [ ] Tool Use mindestens einmal praktisch umgesetzt
- [ ] Architektur-Entscheidung für Kaizen: Wie viel "Agent" braucht Milo?

---

## 8. Modul 6 — Production Concerns

**Woche:** 9
**Zeitaufwand:** ~5-6h
**Ziel:** Du kennst die Themen, die im Prototyp unwichtig sind, aber beim Produkt matchentscheidend werden. Du kannst vorausschauend Entscheidungen treffen.

### Kernthemen
- Evaluation: Wie misst man Qualität von LLM-Outputs?
- Kosten-Optimierung: Caching, Model Routing, Context Management
- Latenz: Streaming, Token-by-Token, Perceived Performance
- Prompt Injection und Jailbreaks — Sicherheit
- Rate Limits, Retries, Fallbacks
- Logging und Observability
- A/B Testing mit LLMs
- Model-Updates: Umgang mit Breaking Changes
- Datenschutz und Compliance (relevant für Kaizen wegen Gesundheitsdaten)

### Ressourcen
- **[Blog]** Hamel Husain — *"Your AI Product Needs Evals"* (hamel.dev). Der beste Artikel zum Thema Evaluation.
- **[Blog]** Eugene Yan — *eugeneyan.com*. Mehrere Artikel zu LLM-Production-Patterns.
- **[Docs]** Anthropic — Sections zu Security, Prompt Injection, Rate Limits.
- **[Blog]** Simon Willison — diverse Artikel zu Prompt Injection (er war einer der ersten, die das Thema aufgegriffen haben).
- **[Buch, optional]** *"AI Engineering"* von Chip Huyen — falls du ein strukturiertes Buch willst, das vieles zusammenfasst.

### Praktische Übungen
1. Ein simples Eval-Setup für Milo bauen: Wie misst du, ob eine Milo-Antwort "gut" ist?
2. Prompt Injection: Testen, ob Milo aus seiner Rolle zu bringen ist
3. Logging aufsetzen: Jeder API-Call mit Prompt, Response, Kosten

### Kaizen-Bezug
**Weit vor Produkt-Launch relevant, aber jetzt schon nützlich,** um die Economics-Seite präziser zu machen und Weichen richtig zu stellen. Kaizen verarbeitet Gesundheitsdaten — Sicherheit und Datenschutz sind kein Nice-to-Have.

### Checkliste
- [ ] Hamel Husain's Evals-Artikel gelesen
- [ ] Verstehe Prompt Injection und kenne Mitigation-Strategien
- [ ] Simples Eval-Framework für Milo skizziert
- [ ] Logging im Prototyp aktiv

---

## 9. Begleitend durchgehend

### 9.1 Personen, denen du folgen solltest

**Simon Willison** (simonwillison.net, @simonw)
Ehemaliger Django-Core-Entwickler, einer der aktivsten und klarsten Praktiker im LLM-Feld. Schreibt fast täglich, filtert den Hype, probiert alles selbst aus. Wenn du nur einer Person folgen willst — diese.

**Andrej Karpathy** (@karpathy, YouTube)
Ehemaliger OpenAI und Tesla AI Director. Selten, aber wenn, dann erstklassige Inhalte. Seine Videos sind Gold.

**Anthropic Engineering** (anthropic.com/engineering)
Eigene Firma des Modells, das du nutzen wirst. Sehr gute technische Artikel, nicht Marketing-gefärbt.

**Hamel Husain** (hamel.dev)
ML-Praktiker mit Fokus auf Evals und Production-LLM-Arbeit. Sehr bodenständig.

**Eugene Yan** (eugeneyan.com)
Strukturierte, praktische Artikel zu LLM-Architektur und Production.

### 9.2 Podcasts für "nebenbei"

- **Latent Space** — AI Engineering News und Interviews
- **The Cognitive Revolution** — Konzepte und Kontroversen
- **Dwarkesh Podcast** — Tiefe Interviews mit Forschern (eher theoretisch)

### 9.3 Kontinuierliches Lernen

Nach den 9 Wochen ist das strukturierte Lernen abgeschlossen, aber das Feld bewegt sich schnell. Plan:
- Simon Willison's Blog im RSS-Reader
- Ein AI-Podcast pro Woche
- Anthropic Engineering neue Artikel lesen
- Monatlich: ein tieferes Thema nach Bedarf vertiefen

---

## 10. Wochenplan-Übersicht

| Woche | Modul | Prototyp-Phase | Kernoutput |
|-------|-------|----------------|------------|
| 1 | Was LLMs sind | (Vorbereitung) | Mentale Grundlage |
| 2 | Claude API | Phase 1 beginnt | Erster API-Call, Grundstruktur |
| 3-4 | Prompt Engineering | Phase 1 | Milo-System-Prompt steht |
| 5-6 | Memory/Context | Phase 2 | Architektur-Entscheidung Memory |
| 7-8 | Tool Use / Agents | Phase 3 | Proaktive Checks + Tool Use |
| 9 | Production Concerns | Phase 4 | Evals, Logging, Security |
| 10+ | Puffer / Vertiefung | Evaluation MVP | Lessons Learned |

---

## 11. Offene Punkte / Erweiterungen

Aktuell nicht im Pfad, aber möglicherweise später relevant:

- [ ] **Fine-Tuning** — aktuell nicht nötig. Wird erst bei spezifischen Qualitätsproblemen interessant, die Prompt Engineering nicht löst.
- [ ] **Multi-Modal** (Bild, Audio) — falls Kaizen später Fortschrittsfotos analysieren oder Voice-Messages verarbeiten soll.
- [ ] **Model-Comparison** — systematischer Vergleich Claude vs. GPT vs. Open-Source-Modelle, wenn Kostenoptimierung relevant wird.
- [ ] **Open-Source-Modelle** (Llama, Mistral) — falls Self-Hosting aus Kosten- oder Datenschutzgründen interessant wird.
- [ ] **Distillation / Eigene Modelle** — sehr langfristig, wenn überhaupt.

---

## 12. Prinzipien für den Lernweg

**Don't get stuck in theory.** Wenn du merkst, du verlierst dich in Tutorials ohne zu bauen: hör auf und bau etwas. Die besten Lernmomente kommen beim Hands-on-Fehler-Machen.

**Question the hype.** Das AI-Feld ist voller Twitter-Hype, unbewiesener Behauptungen und vorbeifliegender "Frameworks". Immer fragen: Löst das ein echtes Problem, das ich habe? Meistens: nein.

**Write down what you learn.** Jede Woche 10-15 Minuten reflektieren und in dieses Dokument ergänzen: Was war überraschend? Was war ein Aha-Moment? Was funktioniert in der Praxis anders als erwartet?

**Share early.** Wenn du etwas gelernt hast, erklär es jemandem (oder schreib es auf). Das ist der beste Test für echtes Verständnis.

---

## 13. Nächste Schritte

1. Woche 1 starten — Karpathy-Video heute oder morgen einplanen
2. Anthropic Account einrichten (falls nicht geschehen)
3. RSS-Feeds einrichten: Simon Willison, Anthropic Engineering
4. Dieses Dokument nach jeder Woche updaten — Notizen, Erkenntnisse, Fragen, Links zu eigenen Experimenten

---

## 14. Notizen und Erkenntnisse

*(Dieser Abschnitt wird während des Lernens gefüllt — eigene Gedanken, Aha-Momente, Fragen, Verweise auf eigene Experimente.)*

### Woche 1

*...*

### Woche 2

*...*