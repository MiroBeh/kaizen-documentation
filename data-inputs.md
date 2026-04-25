# Kaizen — Datenerfassung (Data Inputs)

> **Zweck dieses Dokuments:** Spezifikation aller strukturierten Dateneingaben, die Milo für das Coaching benötigt. Dieses Dokument löst den offenen Parklistenpunkt #4 aus `vision.md` ("Datenerfassung im Detail").
>
> **Status:** Erste vollständige Version
> **Referenz-Dokumente:** `vision.md`, `onboarding.md`, `prototype.md`

---

## Architektur-Prinzip

Zwei getrennte Eingabe-Kanäle (aus `vision.md` Abschnitt 6.1):

- **Strukturierte Inputs** → App-Forms (dieses Dokument)
- **Dialogische Kommunikation** → Chat mit Milo

Alles, was ein "hartes Faktum" ist, kommt über strukturierte Inputs. Alles, was Kontext, Gefühl oder Situation ist, kommt natürlich über Chat. Milo fragt im Chat nach, wenn er mehr Hintergrund braucht.

---

## Tier 1 — Statisches Profil (Onboarding, einmalig)

Gibt Milo den fixen Kontext, den er für den ersten Plan und jede Coaching-Entscheidung braucht.

| Feld | Typ | Pflicht | Anmerkung |
|------|-----|---------|-----------|
| Alter | Zahl | Ja | Relevant für TDEE-Schätzungen, Erholung |
| Größe | Zahl (cm) | Ja | |
| Geschlecht | Enum (m/w/d) | Ja | Relevant für Norm-Werte und TDEE |
| Startgewicht | Zahl (kg) | Ja | Ausgangspunkt für Fortschrittstracking |
| Primäres Ziel | Enum | Ja | Muskelaufbau / Kraft / Fettabbau / Recomp |
| Erfahrungslevel | Enum | Ja | Anfänger / Fortgeschritten / Wiedereinsteiger |
| Verfügbare Trainingstage/Woche | Zahl | Ja | |
| Durchschnittliche Session-Dauer | Zahl (min) | Ja | |
| Equipment | Fixed: Gym | Ja | **v1: Nur Gym.** Home-Training und weitere Varianten sind bewusst ausgeklammert — Fokus auf die primäre Zielgruppe. Erweiterung in Zukunft vorgesehen. |
| Verletzungen / Einschränkungen | Freitext | Ja | Kann "keine" sein |
| Ernährungseinschränkungen | Freitext | Nein | Vegetarisch, Allergien, Intoleranzen etc. |

**Bewusst nicht im Scope:** Beruf, Wohnort, Beziehungsstatus, Wearable-Gerät.

**Übergabe ans Onboarding:** Diese Felder werden in Onboarding-Phase 2 eingesammelt — nach dem Kennenlerngespräch mit Milo, damit die Beziehung bereits steht. Milo erklärt den Übergang bewusst: *"Ich brauche noch ein paar harte Fakten — geht am schnellsten über ein paar Felder in der App."*

---

## Tier 2 — Tägliches Tracking (täglich, morgens)

Muss reibungslos sein. Max. 30 Sekunden. Diese Daten treiben Milos Anomalie-Erkennung und Trendanalyse.

| Feld | Format | Rationale |
|------|--------|-----------|
| Körpergewicht | Zahl (kg) | Wichtigster einzelner Datenpunkt. Ohne tägliche Gewichtsdaten ist Milo bei Fat Loss / Bulk blind. |
| Schlafstunden | Zahl oder Enum (< 5h / 5–6h / 7–8h / > 8h) | Direkter Einflussfaktor auf Leistung und Erholung. Korreliert mit Trainingsperformance-Dips. |
| Energie-Level | Skala 1–5 | Gibt Milo Kontext zu Gewichtsschwankungen und Leistungseinbrüchen. |

**Warum nur drei Felder?** Tägliches Tracking darf sich nicht wie Arbeit anfühlen. Drei Felder, 20 Sekunden. Stimmung, Stress und Kontext kommen natürlich über Chat.

---

## Tier 3 — Per-Session Tracking (nach jedem Training)

Eingeloggt nach dem Training. Max. 2–3 Minuten. Ermöglicht Plateau-Erkennung, Progressions-Analyse und Volumen-Diagnose.

| Feld | Format | Anmerkung |
|------|--------|-----------|
| Übung | Text oder Liste | Freitext oder Auswahl aus Liste — beides muss funktionieren |
| Sätze | Zahl | |
| Wiederholungen | Zahl (oder Range) | |
| Gewicht | Zahl (kg) | |
| Session-Gefühl | Skala 1–5 | "Wie lief es insgesamt?" — gibt Milo Anlass für Follow-up-Fragen im Chat |

**Bewusst minimalistisch:** Kein RPE pro Satz, kein Video, keine Technik-Notizen in v1. Wenn Milo etwas Auffälliges sieht, stellt er die Folgefrage im Chat.

---

## Tier 4 — Tägliche Ernährungs-Adherence (täglich)

**Kerngedanke:** Milo setzt den Plan. Der User meldet nur Abweichungen davon. Kein Logging nötig, wenn der Plan eingehalten wurde — das wäre unnötiger Aufwand an 80 % der Tage.

**Flow:**

```
Hast du deinen Ernährungsplan heute eingehalten?

  [Ja]  →  fertig (kein weiterer Input)

  [Nein] →  Was war anders?  (Freitext)
             Wie weit weg?    (Etwas / Deutlich / Komplett anders)
```

| Schritt | Feld | Format |
|---------|------|--------|
| 1 | Plan eingehalten? | Ja / Nein |
| 2 (nur bei Nein) | Was war anders? | Freitext — "Geburtstag", "Auswärts gegessen", "Kein Plan gehabt" |
| 2 (nur bei Nein) | Wie weit weg? | Enum: Etwas / Deutlich / Komplett anders |

**Wie Milo damit umgeht:** Unterscheidet Einzel-Ausreißer von Mustern. Spricht es im Chat an, wenn ein Muster entsteht: *"Du weichst jetzt 4 Tage in Folge ab — lass uns kurz reden, was da los ist."*

---

## Tier 5 — Wöchentlicher Check-in

Echte Coaches machen regelmäßige strukturierte Check-ins mit ihren Kunden. Kaizen spiegelt das.

**Start:** Einmal pro Woche. **Zukünftig:** Intervall pro User konfigurierbar (wöchentlich / zweiwöchentlich).

Der Check-in ist ein dedizierter strukturierter Input — kein normales Chat-Gespräch. Milo löst ihn aktiv aus.

| Feld | Format | Rationale |
|------|--------|-----------|
| Wie war die Woche insgesamt? | Skala 1–5 | Schneller Gesamt-Sentiment — flaggt schlechte Wochen sofort |
| Trainings-Adherence | x von y geplanten Trainings gemacht | Milo kennt den Plan, User meldet nur das Ergebnis |
| Ernährungs-Adherence (Woche gesamt) | Freitext / kurze Einschätzung | Wochenbild jenseits der täglichen Einzel-Logs |
| Feedback zum aktuellen Plan | Freitext | Dedizierter Slot für "diese Übung fühlt sich komisch an", "Mittwoch passt mir nicht", "ich will mehr Abwechslung" |
| Körpermaße (optional) | Taille, Hüfte etc. (cm) | Nützlich wenn Gewicht stagniert — kein Pflichtfeld |
| Fortschrittsfotos (optional) | User-getrieben | Natürliche monatliche Kadenz, aber im Check-in angeboten |

**Warum Plan-Feedback im Check-in?** Echte Coaches fragen auf einer festen Kadenz aktiv nach, wie der Plan läuft — sie warten nicht, bis der Client sich beschwert. Das ist ein direkter Ausdruck des Kern-Differenzierers "Flexibilität statt Starre".

---

## Was KEIN strukturierter Input ist

Diese Informationen kommen natürlich über Chat — nicht über Forms:

- Stress-Level ("War ein harter Tag heute")
- Reisen / Krankheit ("Bin diese Woche auf Geschäftsreise")
- Motivationslage
- Soziale Ereignisse, die die Ernährung beeinflussen
- Emotionaler Kontext rund ums Training

Milo fragt im Chat danach, wenn er Kontext braucht. Forms sind für Fakten, Chat ist für Kontext.

---

## Parkliste / Offene Punkte

| # | Thema | Beschreibung |
|---|-------|--------------|
| 1 | **Equipment-Erweiterung** | Home-Training, spezifische Geräte, Outdoor — bewusst nicht in v1, aber Struktur sollte erweiterbar sein |
| 2 | **Gewicht: Pflicht oder optional?** | Tägliches Wiegen ist nicht für jeden realistisch. Was passiert, wenn ein User mehrere Tage nicht einloggt? |
| 3 | **Check-in-Intervall konfigurieren** | Wöchentlich als Default — wann und wie macht der User das einstellbar? |
| 4 | **Ernährungslog bei "Plan eingehalten"** | Langfristig: Auch bei Ja-Tagen könnte ein optionales "grob was gegessen?" nützlich sein — aber nicht in v1 |
| 5 | **Datenformat / API** | Wie werden diese Daten gespeichert und an Milo übergeben? (SQLite, JSON, welches Schema?) |
| 6 | **Wearable-Integration** | Apple Health, Garmin, etc. für Schlaf/Schritte — klar interessant, aber kein MVP-Thema |
| 7 | **Eingabe-UX** | Telegram-Commands vs. Web-Form vs. Bot-Buttons — noch offen (siehe `prototype.md`) |
