# Kaizen — Rules (Globale Regelbasis)

> **Zweck dieses Dokuments:** Arbeitsdokument für die globale Regelbasis von Kaizen. Hier werden die Regeln gepflegt, die Milos Coaching-Wissen ausmachen — das **Herzstück**, das Milo von einem generischen Chatbot unterscheidet.
>
> **Status:** Strukturentwurf, Starter-Regeln noch zu erarbeiten
> **Referenz-Dokumente:** `vision.md`, `prototype.md`

---

## 1. Was diese Regelbasis ist (und was nicht)

### 1.1 Was sie ist
- **Globales, kollektives Coaching-Wissen** — gilt für alle User
- Strukturierte Anleitung, wie Milo in bestimmten Situationen vorgeht
- Die Wissensbasis, auf die Milo bei jeder Antwort zugreift
- Wachsende Sammlung — startet kuratiert, wird durch Human-in-the-Loop in Zukunft erweitert (siehe Vision)

### 1.2 Was sie nicht ist
- **Kein User-spezifisches Wissen** (das gehört in persönliche Notizen, getrennte Speicherung)
- **Kein Trainingsplan** (Pläne sind individuell, Regeln sind generelle Prinzipien)
- **Keine starre Vorschrift** — Regeln sind Leitfäden, Milo passt situativ an
- **Kein Ersatz für medizinischen oder therapeutischen Rat** — wo Grenzen sind, regelt das die Kategorie "Sicherheit & Grenzen"

---

## 2. Format einer Regel

Jede Regel folgt einem einheitlichen Schema. Format wird im MVP-Verlauf validiert und ggf. angepasst.

### 2.1 Pflichtfelder
- **ID** — eindeutiger Identifier (z.B. `RULE-NUTR-001`)
- **Kategorie** — eine der definierten Kategorien (siehe Abschnitt 3)
- **Titel** — kurze, prägnante Bezeichnung
- **Trigger / Situation** — wann wird diese Regel relevant?
- **Vorgehen** — was macht Milo konkret?
- **Begründung** — warum macht er das (Wissensgrundlage)?

### 2.2 Optionale Felder
- **Tags** — für Selective Loading später (z.B. `#anfänger`, `#cut`, `#verletzung`)
- **Beispiel-Dialog** — wie könnte Milo das in der Konversation umsetzen?
- **Verwandte Regeln** — Verweise auf andere IDs
- **Eskalation** — wann verweist Milo an einen Menschen / Fachperson?
- **Quellen / Referenzen** — woher kommt das Wissen?

### 2.3 Beispiel-Format (Markdown-Variante, vorläufig)

```markdown
### RULE-NUTR-001 — Heißhungerattacken
**Kategorie:** Ernährungsdiagnostik
**Tags:** #cut #ernährung #signal

**Trigger:**
Client berichtet von Heißhungerattacken — besonders auf Süßes oder Salziges.

**Vorgehen:**
1. Erkundige dich nach aktuellem Süßstoffkonsum (Diet-Getränke, Zero-Produkte, Süßstoff im Kaffee/Quark)
2. Frage nach Schlafqualität und -dauer der letzten Woche
3. Prüfe Mahlzeitenrhythmus — gibt es lange Phasen ohne Nahrung?
4. Wenn im Cut: Frage nach aktuellem Defizit-Niveau

**Begründung:**
- Hoher Süßstoffkonsum kann die Süß-Präferenz verstärken (Studienlage uneindeutig, aber häufig anekdotisch beobachtet)
- Schlafmangel erhöht Ghrelin (Hunger-Hormon) und senkt Leptin (Sättigungs-Hormon)
- Unregelmäßige Mahlzeiten führen zu Blutzuckerschwankungen und Heißhunger-Episoden
- Zu aggressives Defizit (>1% KG/Woche) verstärkt Heißhunger

**Eskalation:**
Wenn Heißhunger mit Kontrollverlust, Binge-Episoden oder Schamgefühlen einhergeht → Hinweis auf mögliche Essstörung, Empfehlung professioneller Hilfe.
```

### 2.4 Format-Entscheidung
**Vorläufig: Markdown.** Begründung:
- Lesbar und editierbar (auch ohne Tools)
- Gut für LLM-Kontext (LLMs verarbeiten Markdown sehr natürlich)
- Versionierbar via Git
- Niedrige Einstiegshürde

**Alternativ später denkbar:** YAML oder JSON, wenn strukturierter Zugriff (Programmcode) wichtiger wird als menschliche Lesbarkeit.

---

## 3. Kategorien

Erste Definition. Wird später geschärft (siehe Parkliste).

### 3.1 Trainingsdiagnostik (`TRAIN`)
- Plateau-Erkennung und Diagnose
- Übertraining-Symptome
- Volumen-Anpassung bei Stagnation
- Frequenz-Anpassung
- Form/Technik-Themen (eingeschränkt, Milo sieht nicht)
- Deload-Bedarf erkennen

### 3.2 Ernährungsdiagnostik (`NUTR`)
- Heißhunger-Patterns
- Stagnation beim Cut/Bulk
- Wassergewicht-Schwankungen verstehen
- Mahlzeitenrhythmus und Sättigung
- Protein-Intake-Themen
- Refeeds und Diet Breaks

### 3.3 Recovery & Lifestyle (`RECO`)
- Schlafqualität und Trainingsleistung
- Stress-Auswirkungen auf Fortschritt
- Krankheits-Anpassungen (akut, postakut)
- Reise-Anpassungen
- Sozialer Druck (Restaurants, Familie, Feiertage)
- Alkohol und Trainingsfortschritt

### 3.4 Mentale & Beziehungs-Themen (`MENT`)
- Umgang mit Rückschlägen
- Realistische Erwartungssteuerung
- Motivationskrisen
- Body Image und Zielsetzung
- Vergleich mit anderen (Social Media)
- All-or-Nothing-Denken

### 3.5 Sicherheit & Grenzen (`SAFE`)
- Wann an Arzt verweisen (akute Schmerzen, Verletzungen, Symptome)
- Wann an Physiotherapeut verweisen (chronische Beschwerden, Bewegungseinschränkungen)
- Wann an Ernährungstherapeut verweisen (medizinische Indikation, Mangelzustände)
- Wann an Psycholog:in verweisen (Essstörungs-Indikatoren, exzessives Verhalten, mentale Krise)
- Red Flags allgemein
- Was Milo grundsätzlich nicht tut

### 3.6 Onboarding & Beziehung (`ONBO`) — *optional, evtl. später*
- Wie Milo das erste Gespräch führt
- Wie er die Persönlichkeits-Kalibrierung vornimmt
- Wie er bei Lügen / Inkonsistenzen reagiert
- Wie er Plan-Anpassungen kommuniziert

> **Hinweis:** Die letzte Kategorie überschneidet sich mit Onboarding-Themen aus `Kaizen-Onboarding.md`. Hier ist später zu entscheiden, was wo hingehört (Regel vs. Persönlichkeits-Spec).

---

## 4. Token-Effizienz-Strategie

Wichtiges Architektur-Thema (siehe auch `Kaizen-Prototype.md` Abschnitt 4.3).

### 4.1 Aktuelle Strategie (MVP, 20-30 Regeln)
- **Alle Regeln immer im System-Prompt-Kontext** — bei dieser Anzahl unkritisch
- **Prompt Caching aktiviert** — Regelbasis ändert sich selten, Cache-Hits sehr profitabel

### 4.2 Mittelfristig (50-200 Regeln)
- **Selective Loading** — nur relevante Kategorien je nach User-Nachricht laden
- **Klassifikation der User-Nachricht** vorab (kann von einem schnelleren/günstigeren Modell gemacht werden)

### 4.3 Langfristig (200+ Regeln)
- **RAG-Ansatz** — Embeddings über Regeln, nur die top-N relevanten ins Kontextfenster
- **Hierarchische Strategie** — Kern-Regeln immer dabei, Spezialregeln nach Bedarf

### 4.4 Wichtig
**Nicht vorzeitig optimieren.** Im MVP sind 20-30 Regeln in jedem Call kein Problem. Erst wenn die Regelbasis wirklich wächst, werden die fortgeschrittenen Strategien relevant.

---

## 5. Starter-Regeln (zu erarbeiten)

> **Status:** Strukturplatzhalter — die 20-30 Starter-Regeln werden in einer eigenen Session konkret ausgearbeitet.

**Geplante Verteilung:**
- Trainingsdiagnostik: ~6-7 Regeln
- Ernährungsdiagnostik: ~6-7 Regeln
- Recovery & Lifestyle: ~4-5 Regeln
- Mentale & Beziehungs-Themen: ~3-4 Regeln
- Sicherheit & Grenzen: ~4-5 Regeln (besonders wichtig wegen Haftung/Verantwortung)

### 5.1 Trainingsdiagnostik (TRAIN)

*[Platzhalter — Regeln werden hier ergänzt]*

### 5.2 Ernährungsdiagnostik (NUTR)

*[Platzhalter — Regeln werden hier ergänzt]*

### 5.3 Recovery & Lifestyle (RECO)

*[Platzhalter — Regeln werden hier ergänzt]*

### 5.4 Mentale & Beziehungs-Themen (MENT)

*[Platzhalter — Regeln werden hier ergänzt]*

### 5.5 Sicherheit & Grenzen (SAFE)

*[Platzhalter — Regeln werden hier ergänzt]*

---

## 6. Qualitätssicherung der Regelbasis

### 6.1 Risiko: Halbwissen kodifizieren
Wenn die initiale Regelbasis Halbwissen oder fragwürdige "Bro-Science" enthält, ist das später schwer wieder zu korrigieren. Milo wird auf falscher Grundlage coachen, das schadet Usern.

### 6.2 Mögliche Maßnahmen
- **Eigenes Wissen kritisch reflektieren** — wo bin ich sicher, wo unsicher?
- **Hochwertige Quellen referenzieren** — Renaissance Periodization, Stronger By Science, Helms et al.
- **Echten Coach hinzuziehen** — vor Launch, vielleicht schon vor Phase 1, je nach Selbsteinschätzung
- **Versionierung** — schlechte Regeln können später identifiziert und korrigiert werden
- **Markierung von Unsicherheits-Levels** — `confidence: high/medium/low` als Feld pro Regel

### 6.3 Entscheidung MVP
- Starter-Set wird nach bestem Wissen vom Projekt-Owner erstellt
- Vor "echtem" Test (Sharing mit Anderen) → fachliches Review durch Coach empfohlen
- Markierung `confidence`-Feld als optionale Erweiterung des Regelformats

---

## 7. Versionierung

### 7.1 Vorläufig (MVP)
- Regelbasis im Git-Repo des Prototyps
- Commits dokumentieren Änderungen
- Keine separaten Versionsnummern nötig

### 7.2 Später
- Möglicherweise Versionsnummern pro Regel (für Lerneffekte über Zeit beobachten)
- "Regel X führte zu Verbesserung in Y Fällen, Verschlechterung in Z Fällen"
- Verbindung zur Human-in-the-Loop-Mechanik

---

## 8. Offene Punkte / Parkliste

| # | Thema | Beschreibung |
|---|-------|--------------|
| 1 | **Kategorien-Schema final definieren** | Aktuelle Kategorien sind erste Version — Granularität, Überschneidungen, Vollständigkeit prüfen |
| 2 | **Tagging-System entwickeln** | Für Selective Loading: welche Tags? Standardisiert oder frei? |
| 3 | **Format final festlegen** | Markdown vs. YAML vs. Mischform — basierend auf Praxis-Erfahrung im MVP |
| 4 | **Confidence-Feld ergänzen?** | Markierung der Wissens-Sicherheit pro Regel |
| 5 | **Regel-IDs systematisch** | Schema für IDs, Kollisionsvermeidung |
| 6 | **Beispiel-Dialoge integrieren?** | Wie wertvoll sind Few-Shot-Beispiele direkt in der Regel? Token-Kosten vs. Qualitätsgewinn |
| 7 | **Eskalations-Patterns** | Standardisierte Formulierungen, wie Milo eine Eskalation kommuniziert |
| 8 | **Coach-Review-Prozess** | Wer reviewt Regeln, wann, mit welchen Kriterien? |
| 9 | **Versionierung pro Regel** | Eigene Versionsnummern oder reicht Git? |
| 10 | **Konflikt-Auflösung** | Was, wenn zwei Regeln widersprüchliche Empfehlungen geben? |
| 11 | **Kategorie ONBO** | Ja oder nein? Falls ja: Abgrenzung zu `Kaizen-Onboarding.md` |
| 12 | **Token-Strategie schärfen** | Konkrete Schwellenwerte: Wann von "alle laden" zu "selective" wechseln? |
| 13 | **Regelbasis-Wachstum durch Human-in-the-Loop** | Mechanik: Wer formuliert eine neue Regel aus Coach-Feedback? |

---

## 9. Nächste Schritte

1. **Starter-Regeln ausarbeiten** — 20-30 konkrete Regeln über alle Kategorien hinweg, in einer fokussierten Session
2. **Format an einer realen Regel validieren** — eventuell Anpassungen am Schema
3. **Token-Verbrauch messen** — wie viele Tokens belegt die Regelbasis im MVP wirklich?
4. **Integration in Prototyp** — Loading-Mechanismus, Prompt Caching, Logging
5. **Erste Praxis-Erfahrung** — wie nutzt Milo die Regeln tatsächlich? Greifen sie?

---

## 10. Notizen und Erkenntnisse

*(Wird während der Praxis gefüllt — was funktioniert, was nicht, welche Regeln werden häufig getriggert, welche Lücken zeigen sich.)*