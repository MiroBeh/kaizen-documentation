# Kaizen — Vision Dokument

> **Hinweis zu den Namen:** "Kaizen" (Projektname) und "Milo" (Name des Coach-Bots / LLM) sind **Placeholder-Namen**. Beide sollen zu einem späteren Zeitpunkt nochmals überprüft und final entschieden werden.

---

## Zugehörige Dokumente

- **`economics.md`** — Arbeitsdokument zur Wirtschaftlichkeit (Kosten, Preise, Margen, Skalierung)
- **`onboarding.md`** — Arbeitsdokument zum Onboarding-Prozess (Phasen, Design-Entscheidungen, offene Fragen)
- **`prototype.md`** — Arbeitsdokument zum technischen Prototyp / MVP (Phasen, Technologie, konkrete Schritte)
- **`learning.md`** — Lernpfad für AI/LLM-Grundlagen (parallel zur Prototyp-Entwicklung)

---

## 1. Executive Summary

**Kaizen** ist ein AI Personal Coach, der echtes 1-on-1 Coaching im Sport-Lifestyle-Bereich für jedermann zugänglich macht. Zielpreis: ca. **30-40€ pro Monat** statt der üblichen 200-400€ für menschliches Online-Coaching.

Der Coach — **Milo** — führt mit jedem Client eine natürliche Coach-Client-Beziehung über mehrere Kommunikationskanäle (App, Messenger). Er begleitet ganzheitlich auf der Reise zu den Zielen des Clients und passt sich flexibel an dessen Leben an.

**Startfokus:** Krafttraining, Muskelaufbau, Fettreduktion.
**Langfristige Vision:** Ausweitung auf weitere Sport-Lifestyle-Bereiche (Hybrid Training, Cardio, Hyrox, etc.).

---

## 2. Die drei Kern-Differenzierer

### 2.1 Flexibilität statt Starre
Nicht "Plan abarbeiten", sondern "Plan lebt mit dir". Der User folgt keinem starren, von Beginn an festgelegten Programm — das System passt sich kontinuierlich an das Leben und den Fortschritt des Clients an.

### 2.2 Wachsendes kollektives Coaching-Wissen
Durch einen Human-in-the-Loop-Mechanismus werden aus echten Coach-Interventionen bei unklaren Fällen globale Regeln generiert, die das System mit jedem bearbeiteten Fall klüger machen.

### 2.3 Persönliche Beziehung ohne menschliche Hemmschwelle
Milo kennt jeden User persönlich durch eigene Notizen zum Umgang. Gleichzeitig ist er "nur" ein Bot — der User muss keine Geheimnisse haben, kann ehrlich sein, und Milo konfrontiert auch ehrlich zurück.

---

## 3. Zielgruppe

- **Primär:** Jedermann, der sich keinen menschlichen 1-on-1 Coach leisten kann oder will
- **Ausgeschlossen:** Echte Profi-Athleten — hier soll und kann Kaizen kein menschliches Profi-Coaching ersetzen
- **Positionierung:** Sehr gute Alternative zum teuren Online-Coaching, nicht billige Low-End-Lösung

---

## 4. Produkt-Umfang

### 4.1 Rolle des Coaches
Milo ist ein **ganzheitlicher Begleiter**. Alle Faktoren, die die Ziele (Krafttraining, Muskelaufbau, Fettreduktion) beeinflussen, sollen mindestens via Chat mit Milo besprochen werden können.

### 4.2 Coach-Client-Beziehung — was Milo leistet
- Ehrliches Feedback
- Emotionale Unterstützung bei Rückschlägen
- Anpassungsfähigkeit an den Alltag des Clients
- Accountability
- Alles, was ein echter 1-on-1 Coach heute leistet — ohne die menschliche Komponente

### 4.3 Interaktionsfrequenz & Proaktivität
Milo arbeitet **proaktiv**, nicht nur reaktiv:
- Prüft Daten proaktiv auf Kurs und Konsistenz
- Gibt eigenständig Feedback
- Fragt nach, wenn keine Rückmeldung vom Client kommt
- **Wichtig:** Proaktivität muss dosiert erfolgen — nicht nervig werden

### 4.4 Datenprüfung durch Milo
- Definierte Regeln, die sich am individuellen Ziel des Clients orientieren
- Anomalie-Erkennung (z.B. Trainingsfrequenz bricht ein, Gewichts-Anomalien, Leistungsabfall)
- Bei Anomalien: proaktive Ansprache des Clients
- Wenn keine Lösung gefunden → ggf. Plan-Anpassung

### 4.5 Umgang mit "schlechtem" Client-Verhalten
- Milo soll erkennen, wenn Angaben nicht stimmig sind (z.B. Ernährungsangaben passen nicht zu Gewichtsentwicklung)
- Direkte, ehrliche Ansprache: "Du schreibst nur mit einem Bot — keine Geheimnisse nötig, lügen hilft keinem"
- Gemeinsam erarbeiten, was wirklich los ist
- Anomalien wie unerwartete Gewichtszunahmen → proaktiv nachfragen

### 4.6 Persönlichkeit des Coaches
- Der Charakter von Milo soll bis zu einem gewissen Grad **vom User selbst einstellbar** sein
- Konkrete Ausgestaltung (welche Achsen, welche Presets) ist später zu definieren

---

## 5. Der Regel-Lernmechanismus (Herzstück)

### 5.1 Zwei getrennte Wissensebenen

**Globales Wissen (Regelbasis)**
- Generelle Verhaltensregeln, die für alle User gelten
- Beispiel: *"Client hat Heißhungerattacken → checken, ob hoher Süßstoffkonsum vorliegt, der Lust auf Süßes triggert"*
- Basis für die Skalierung des Coaching-Know-hows

**Persönliche Notizen (pro User)**
- Wie Milo mit dem spezifischen User umgeht
- Persönliche Eigenheiten, Vorlieben, Kommunikationsstil
- Ähnlich wie Memory-Systeme in anderen LLM-Anwendungen
- **Kein Teil der globalen Wissensbasis**

### 5.2 Human-in-the-Loop-Prozess
1. Milo erkennt einen Fall, für den es **keinen klaren Leitfaden** gibt
2. Milo **markiert** den Fall als unsicher
3. Milo teilt dem Client mit, dass er einen echten Coach hinzuzieht
4. Echter Coach gibt Milo Feedback
5. Milo generiert daraus eine **globale Regel** für zukünftige, ähnliche Fälle

### 5.3 Kalibrierung der Unsicherheits-Schwelle
Dies ist ein zentrales Test- und Tuning-Thema:
- Milo darf **nicht bei jeder Kleinigkeit** einen echten Coach anfragen (zu teuer, zu langsam)
- Milo darf aber **nicht eigenständig** Themen lösen, für die er keine Grundlage hat
- Die richtige Balance muss empirisch gefunden werden

### 5.4 Coach-Feedback = global
Das Feedback echter Coaches fließt ausschließlich in die globale Regelbasis — und dort nur für **generelle Themen**, nicht für user-spezifische Sonderfälle.

---

## 6. Datenerfassung & Kommunikation

### 6.1 Getrennte Kanäle für Daten und Dialog
- **Strukturierte Inputs** (Trainingsdaten, Gewicht, Messwerte, etc.): kommen vom User selbst, **nicht direkt über den Chat** mit Milo, sondern über dedizierte Inputs (z.B. Forms in der App)
- **Dialogische Kommunikation**: Chat mit Milo (App-Chat, Messenger)

### 6.2 Datenzugriff des Bots
- Milo hat **vollen Zugriff** auf alle strukturierten Daten seines Clients
- Milo kann im Chat Bezug nehmen auf die App-Daten
  - Beispiel: User schreibt "Training war heute mies" → Milo sieht in den Daten "bei Kniebeugen 5kg weniger als letzte Woche" → spricht es an

### 6.3 Kommunikationskanäle
- App mit klassischen Forms (strukturierte Dateneingabe)
- Messaging direkt mit Milo (in-App und/oder externe Messenger wie WhatsApp)
- **Genaue Kanaldefinition ist in Zukunft festzulegen** (siehe Parkliste)

---

## 7. Trainings- und Planverwaltung

### 7.1 Planerstellung
- Milo erstellt Pläne selbst aus seiner Wissensbasis
- Es stehen **Templates** zur Orientierung bereit
- Volumen, Intensität etc. werden im Dialog mit dem Client erarbeitet

### 7.2 Plan-Anpassung
- Anpassung erfolgt **nur bei Bedarf**, nicht auf festem Zyklus
- **Trigger für Anpassung:**
  - Feedback des Clients
  - Anomalien in den Daten, die eine Optimierung nötig machen
- **Wichtig:** Dieses Thema braucht klare, detaillierte Regeln und wird noch vertieft (siehe Parkliste)

---

## 8. Onboarding

Der Onboarding-Prozess wurde in einer ersten Runde konzipiert. Die Kernentscheidungen im Überblick:

- **Hybrid aus Dialog und Formular** — Milo führt zuerst ein natürliches Kennenlerngespräch, dann strukturierte App-Inputs für harte Fakten, dann gemeinsamer erster Plan
- **Langes Onboarding über mehrere Wochen** — nicht als einmaliges Event, sondern als Prozess. Fördert Engagement und passt zum Wow-Effekt "Flexibilität"
- **Direkte Ansprache bei Persönlichkeits-Kalibrierung** — Milo fragt offen, welcher Coaching-Stil passt, mit dem Vermerk dass alles anpassbar bleibt
- **Anpassung des Onboardings an Erfahrungslevel** des Clients (Anfänger vs. Fortgeschrittener)

**Für Details, Phasen-Beschreibung und offene Punkte siehe: `onboarding.md`**

---

## 9. Privatsphäre & Vertrauen

- Beim Review durch echte Coaches werden Fälle **anonymisiert**
- Begründung: Aus den Reviews entstehen nur **globale Verhaltensregeln** — Personenbezug ist nicht nötig
- Vertrauen des Clients ist ein zentraler Wert, der durch klare Prozesse geschützt wird

---

## 10. Geschäftsmodell (grobe Richtung)

- **Kein Low-Budget-Produkt** — Qualität vor Preiskampf
- **Zielpreis:** ca. 30-40€ / Monat für Full Coaching
- Sollten für bessere Features mehr Ressourcen nötig sein → Preis-Thema neu bewerten
- **Vergleich:** Etwa 10-20% des Preises eines menschlichen 1-on-1 Online-Coaches

### 10.1 Skalierung des menschlichen Coach-Anteils
- Mit wachsender User-Basis skaliert der Human-in-the-Loop-Aufwand zunächst mit
- **Gegenbewegung:** Je länger das System lebt, desto dichter wird die Regelbasis → desto seltener sind menschliche Eingriffe nötig
- Dieses Verhältnis muss während der Skalierung **aktiv beobachtet** werden

**Für detaillierte Kostenanalyse und Wirtschaftlichkeitsrechnung siehe: `economics.md`**

---

## 11. Wow-Effekt für den User

Der zentrale "Das-ist-anders"-Moment liegt in der **Flexibilität**:
- Keine starre App, die einen von Beginn an festgelegten Plan durchdrückt
- Sondern ein System, das sich **an dich** anpasst
- **Anomalie-Erkennung:** Milo merkt, dass etwas schiefläuft, bevor der User es selbst merkt
- **Spontane Anpassung:** User schreibt "heute nur 20 Minuten Zeit" → Plan wird situativ angepasst

---

## 12. Langfristige Vision

### Phase 1 — Nischen-Fokus
Strength / Muscle / Fat-Loss als Startpunkt, um eine klare Nische zu besetzen und das System zu etablieren.

### Phase 2 — Ausweitung im Sport-Lifestyle-Bereich
- Hybrid Training (Kraft + Laufen)
- Reines Cardio Coaching
- Hyrox
- Weitere sportliche Disziplinen

### Nicht im Scope
- Karriere-Coaching
- Tiefgreifende Ernährungs-Spezialisierung (medizinisch / therapeutisch)
- Themen außerhalb des Sport-Lifestyle-Bereichs

---

## 13. Parkliste — Offene Punkte zur Vertiefung

Diese Themen wurden bewusst aus der ersten Visions-Runde ausgeklammert und müssen in späteren Iterationen geschärft werden:

| # | Thema | Beschreibung |
|---|-------|--------------|
| 1 | **Onboarding-Prozess** | Erste Runde erarbeitet → eigenes Dokument `onboarding.md`. Vertiefung läuft dort weiter. |
| 2 | **Eingehende Kanäle** | Exakte Definition, welche Kommunikationskanäle unterstützt werden (App-Chat, WhatsApp, weitere Messenger, Sprachnachrichten, E-Mail?) |
| 3 | **Grenzen des Coaches** | Wo hört Milo auf? Wann verweist er an Fachpersonen? (z.B. bei Schlaf-, Schmerz-, mentalen Themen, Essstörungen) |
| 4 | **Datenerfassung im Detail** | Welche Daten werden genau erfasst? (Trainingslogs, Gewicht, Fotos, Schlaf, Ernährung, Wearables?) |
| 5 | **Plan-Anpassungsregeln** | Genaue Regeln für Trigger, Frequenz und Umfang der Plan-Anpassung |
| 6 | **Budget-Check** | Siehe `economics.md` — erste Runde erarbeitet, Vertiefung läuft dort weiter. |
| 7 | **Regel-Review-Prozess** | Wer genehmigt neue globale Regeln? Einzelner Coach, Review-Board, automatische Qualitätschecks? |
| 8 | **Persönlichkeits-Einstellung** | Welche Achsen gibt es? Wie granular kann der User einstellen? |
| 9 | **Unsicherheits-Schwelle** | Empirische Kalibrierung, wann Milo einen echten Coach hinzuzieht |
| 10 | **Namensfindung** | "Kaizen" und "Milo" sind Placeholder — finale Benennung nachholen |
| 11 | **Pre-Onboarding** | Vor dem eigentlichen Onboarding: Landing Page, Probegespräch mit Milo vor Kauf o.ä. — Idee für die Zukunft, aktuell nicht im Fokus |

---

## 14. Nächste Schritte (Vorschlag)

1. Parkliste weiter priorisieren — welches Thema nehmen wir als nächstes?
2. Einzelne Punkte in Tiefe ausarbeiten (z.B. Grenzen, Datenerfassung, Persönlichkeits-Einstellung)
3. Parallel: erste Skizze der Architektur (noch ohne Umsetzungstiefe)
4. Definition MVP-Scope für eine erste technische Evaluation