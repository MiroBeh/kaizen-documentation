# Kaizen — Economics

> **Zweck dieses Dokuments:** Arbeitsdokument zur Wirtschaftlichkeit von Kaizen. Hier sammeln wir alle Überlegungen, Annahmen und Rechnungen rund um Kosten, Preise, Margen und Skalierung. Das Dokument wächst iterativ — Zahlen sind zunächst grobe Schätzungen und werden mit der Zeit präzisiert.
>
> **Status:** Erste Überlegungen (Brainstorming-Phase)
> **Referenz-Dokument:** siehe `vision.md`

---

## 1. Ausgangsfrage

Ist ein Preis von **30-40€ pro User pro Monat** für Kaizen wirtschaftlich tragfähig, angesichts der Tatsache dass:
- Jeder User eine individuelle Coaching-Beziehung mit Milo (LLM) führt
- Erheblicher LLM-Traffic pro User entsteht (Chat, proaktive Checks, Datenauswertung)
- Ein Human-in-the-Loop-Anteil für unklare Fälle benötigt wird
- Zusätzliche Infrastruktur-, Entwicklungs- und Marketing-Kosten anfallen

---

## 2. Grundlegende Klarstellung: "Eigener Bot" ≠ eigenes Modell

Ein zentrales Missverständnis, das die Kosten-Intuition verzerren kann:

- Jeder User hat **seinen eigenen Kontext** (persönliche Notizen, Historie, Daten, Ziele)
- Alle User **teilen sich dasselbe LLM** (z.B. Claude, GPT, etc.)
- Die Individualisierung entsteht durch **Prompts, Memory und Daten** — nicht durch separate Modelle

Das ist ökonomisch entscheidend: Die Fixkosten des Modells werden über alle User verteilt; pro User fallen nur variable Inference-Kosten an.

---

## 3. Kostenblöcke im Überblick

| # | Block | Typ | Größenordnung pro User/Monat |
|---|-------|-----|------------------------------|
| 1 | LLM-Inference | variabel | 3-8€ (optimiert) |
| 2 | Infrastruktur | semi-variabel | 1-3€ |
| 3 | Human-in-the-Loop | variabel | 2-3€ (anfangs höher) |
| 4 | Entwicklung & Betrieb | fix, anteilig | 3-6€ |
| 5 | Customer Acquisition (CAC, amortisiert) | fix pro User | 3-8€ |
| 6 | Zahlungsabwicklung, Overhead | variabel | 3-5€ |

---

## 4. Block 1: LLM-Kosten (Detail)

### 4.1 Annahmen für einen aktiven User
- ~10-15 Nachrichten/Tag im Dialog mit Milo
- Pro Nachricht:
  - Input: 3.000-8.000 Tokens (System-Prompt + Regelbasis-Auszug + User-Historie + aktuelle Daten)
  - Output: 200-500 Tokens
- Zusätzlich: proaktive Checks durch Milo (Anomalie-Erkennung, Nachfragen)

### 4.2 Grobe Rechnung (Beispiel: Claude Sonnet 4.5 Preise, ca. 3$/M Input, 15$/M Output)
- Input pro Tag: ~50-100k Tokens → ca. 0,20-0,30€
- Output pro Tag: ~5-10k Tokens → ca. 0,10-0,15€
- **Ohne Optimierung: ca. 10-15€ / User / Monat**

### 4.3 Optimierungshebel
| Hebel | Effekt |
|-------|--------|
| **Prompt Caching** (stabiler System-Prompt + Regelbasis) | Input-Kosten drastisch reduzieren |
| **Model Routing** (Haiku für Simples, Sonnet für Komplexes) | 30-60% Einsparung möglich |
| **Intelligentes Context-Management** (nur relevante Historie mitschicken) | 20-40% Einsparung |
| **Summarization der Historie** statt Rohdaten | deutliche Kompression |
| **Batch-/Asynchrone-Verarbeitung** proaktiver Checks | günstigere Modi nutzbar |

### 4.4 Realistisch erreichbar
- Ohne Optimierung: **10-15€/User/Monat**
- Mit Prompt Caching: **3-6€/User/Monat**
- Mit Caching + Model Routing: **2-4€/User/Monat**
- **Planungsannahme: 3-8€/User/Monat**

### 4.5 Offene Punkte
- [ ] Welches LLM-Primärmodell? (Claude, GPT, Open-Source-Kombination?)
- [ ] Eigenes Hosting (z.B. via vLLM für Open-Source) vs. API-basiert?
- [ ] Wie viele Nachrichten/Tag sind für "heavy users" realistisch?

---

## 5. Block 2: Infrastruktur

### 5.1 Umfang
- App-Backend (API-Server, Auth, etc.)
- Datenbank(en) für User-Daten, Trainingslogs, Chat-Historie
- Speicher (Fotos, evtl. Videos, Dokumente)
- Messaging-Integration (WhatsApp etc.)
- Monitoring, Logging, Backups
- Vector-Store für Regelbasis und Memory

### 5.2 Schätzung
- Bei sauberer Architektur und Skalierung: **1-3€/User/Monat**
- Abhängig von Datenvolumen (Fotos, Wearable-Daten) und Messaging-Kosten

### 5.3 Offene Punkte
- [ ] WhatsApp Business API verursacht eigene Kosten (pro Konversation) → separat kalkulieren
- [ ] Speicherung von Fotos und evtl. Video-Check-ins → Kostenblock größer als gedacht?

---

## 6. Block 3: Human-in-the-Loop (der größte Unsicherheitsfaktor)

### 6.1 Kostentreiber
- Anteil der User, die pro Monat einen Coach-Eingriff triggern
- Durchschnittliche Bearbeitungszeit pro Fall
- Coach-Stundensatz

### 6.2 Beispielrechnung (grob)
- 5% der User triggern pro Monat einen Eingriff
- Ø 20 Min/Fall
- 40-60€/Stunde Coach-Satz
- → **Gemittelt 2-3€/User/Monat** in der Anfangsphase

### 6.3 Zeitliche Dynamik
- **Anfangs deutlich höher**: dünne Regelbasis → mehr Eskalationen
- **Mit wachsender Regelbasis sinkend**: je mehr Regeln vorhanden, desto weniger Eskalationen
- **Langfristig-Ziel**: < 1€/User/Monat

### 6.4 Stellschrauben
- Gut kalibrierte Unsicherheits-Schwelle (siehe Vision-Dokument, Parkliste)
- Qualität des Regel-Learning-Prozesses (schnelles Lernen aus jedem Fall)
- Tiefe vs. Breite der initialen Regelbasis vor Launch
- Eventuell Abstufung: schnelle Routine-Reviews vs. aufwändige Spezialfälle

### 6.5 Offene Punkte
- [ ] Werden Coaches fest angestellt, freiberuflich oder über Plattform vermittelt?
- [ ] Wer reviewt die Qualität neuer Regeln (Qualitätssicherung)?
- [ ] Eskalationspfad für wirklich kritische Fälle (medizinisch, psychisch)

---

## 7. Block 4: Entwicklung & Betrieb

### 7.1 Umfang
- Produktentwicklung (App, Backend, AI-Layer)
- Prompt Engineering & Regelbasis-Pflege
- DevOps / SRE
- Data Science & Model Tuning
- QA, Testing

### 7.2 Dynamik
- **Stark fixkostenlastig** — verteilt sich auf alle User
- Pro User/Monat anteilig: **3-6€** ab einer gewissen Skalierung
- Bei kleiner Userbasis: **deutlich höher pro Kopf**

---

## 8. Block 5: Customer Acquisition Cost (CAC)

### 8.1 Benchmarks Fitness-App-Markt
- CAC liegt oft bei **30-80€ pro zahlendem User** (je nach Kanal, Wettbewerb, Qualität)
- Amortisation über die durchschnittliche Lebensdauer des Users

### 8.2 Rechenbeispiel
- CAC: 50€
- Ø Lebensdauer: 10 Monate
- Anteil pro Monat: **5€/User/Monat**

### 8.3 Hebel
- Organisches Wachstum (SEO, Content, Referrals) reduziert CAC massiv
- Retention direkt verbessern → längere Lebensdauer, niedriger CAC-Anteil pro Monat
- Jahres-Abos → mehr Umsatz pro Akquisition

### 8.4 Offene Punkte
- [ ] Welcher Akquisitionskanal ist primär angedacht (Social, SEO, Paid Ads, Partnerschaften)?
- [ ] Referral-Programm angedacht?

---

## 9. Block 6: Zahlungsabwicklung & Overhead

- **Stripe / Payment Gateway:** ca. 3-5% vom Umsatz → ~1,50€ bei 30-40€ Preis
- **Support** (auch wenn großteils durch Milo): Grundaufwand bleibt → ~1€
- **Rechtliches, Steuern, Versicherung, Buchhaltung:** ~1-2€
- **Summe: ~3-5€/User/Monat**

---

## 10. Gesamtrechnung

### 10.1 Szenario A: Konservativ (hohe Kosten)
| Block | Kosten |
|---|---|
| LLM (ohne starke Optimierung) | 8€ |
| Infrastruktur | 3€ |
| Human-in-the-Loop (Anfangsphase) | 3€ |
| Entwicklung/Betrieb (anteilig) | 6€ |
| CAC (amortisiert) | 8€ |
| Zahlung/Overhead | 5€ |
| **Summe** | **33€** |
| **Marge bei 30€** | **-3€** |
| **Marge bei 40€** | **+7€** |

### 10.2 Szenario B: Optimiert (gut skaliert)
| Block | Kosten |
|---|---|
| LLM (mit Caching + Routing) | 3€ |
| Infrastruktur | 1€ |
| Human-in-the-Loop (reife Regelbasis) | 1€ |
| Entwicklung/Betrieb (anteilig) | 3€ |
| CAC (amortisiert) | 3€ |
| Zahlung/Overhead | 3€ |
| **Summe** | **14€** |
| **Marge bei 30€** | **+16€** |
| **Marge bei 40€** | **+26€** |

### 10.3 Ergebnis
- **Anfangsphase**: wahrscheinlich keine oder negative Marge → bewusst einplanen
- **Skalierungsphase**: gesunde Marge erreichbar
- **Break-even**: geschätzt bei 3.000-5.000 zahlenden Usern

---

## 11. Erkenntnisse & Empfehlungen (erste Runde)

### 11.1 Grundsätzlich machbar, aber nicht trivial
30-40€/Monat sind wirtschaftlich darstellbar — jedoch nur unter folgenden Bedingungen:
1. Aktive Optimierung der LLM-Kosten (Caching, Routing, Context-Management)
2. Wachsende Regelbasis → sinkender Human-in-the-Loop-Anteil
3. Gute Retention (Lebensdauer > 6 Monate, idealerweise > 12 Monate)
4. Skalierung bis mindestens 3.000-5.000 aktive User
5. Bewusstes Einplanen von 1-2 Jahren operativem Verlust in der Anlaufphase

### 11.2 Preis-Empfehlung (vorläufig)
- **Standard-Tarif: 35-40€/Monat** — deutlich mehr Puffer für Qualität und Human-in-the-Loop
- **30€** eher als Einstiegs-/Rabatt-Positionierung oder Jahres-Abo-Preis, nicht als Standard

### 11.3 Größte Risiken
- **LLM-Preis-Volatilität** — Modellpreise können steigen oder fallen
- **Retention-Risiko** — Fitness-Apps haben historisch hohe Churn-Raten
- **CAC-Risiko** — wenn Akquisition zu teuer wird, kippt die Rechnung schnell
- **Regulatorische Risiken** (Gesundheitsdaten, DSGVO, Coaching-Haftung)

---

## 12. Stellschrauben im Geschäftsmodell

Ideen, die wir später vertiefen können:

### 12.1 Tiered Pricing
- **Basis-Plan** (günstiger): Mehr Bot, weniger Human-in-the-Loop, weniger Features
- **Standard-Plan**: Volles Coaching-Erlebnis
- **Premium-Plan**: Mehr Coach-Zugang, Priority, Zusatz-Features

### 12.2 Abo-Modelle
- Monatlich (flexibel, höherer Preis)
- Quartal (leichter Rabatt)
- Jahres-Abo (deutlicher Rabatt, reduziert CAC-Anteil pro Monat, verbessert Retention-Zahlen)

### 12.3 Gruppen-/Couple-Pläne
- Partner-Abo: senkt Kosten pro Kopf, erhöht Stickiness durch gegenseitige Accountability

### 12.4 Freemium vs. Free Trial
- **Free Trial** (7-14 Tage): niedrige Einstiegshürde, klare Conversion
- **Freemium** (permanenter Free-Tier): mehr Reichweite, aber potenziell hohe Kostenbelastung durch Nicht-Zahler

### 12.5 Add-Ons
- Zusätzliche menschliche Coach-Calls als In-App-Kauf
- Spezial-Programme (z.B. Hyrox-Prep) als Einmalzahlung
- Integration mit Produkten (Supplement-Partner, Equipment — nur wenn authentisch)

---

## 13. Offene Punkte / ToDos

- [ ] Konkrete Modell-Auswahl treffen und LLM-Kosten präziser rechnen
- [ ] Benchmark-Analyse vergleichbarer AI-Coaching-Apps (Preise, Features, Margen)
- [ ] Detaillierte Rechnung für WhatsApp Business API Kosten
- [ ] Coach-Netzwerk: Modell festlegen (angestellt vs. Freelancer vs. Plattform)
- [ ] Cohort-Retention-Annahmen definieren (Ø Lebensdauer realistisch?)
- [ ] Break-even-Kurve über Zeit modellieren
- [ ] Preis-Sensitivität im Zielmarkt prüfen (wie viel sind User wirklich bereit zu zahlen?)
- [ ] Finanzierungsbedarf für Anlaufphase grob abschätzen
- [ ] Tiered-Pricing-Modell ausarbeiten

---

## 14. Annahmen-Tracker

Damit spätere Korrekturen nachvollziehbar bleiben:

| Annahme | Aktueller Wert | Status | Quelle/Begründung |
|---------|----------------|--------|-------------------|
| Nachrichten/Tag/User | 10-15 | Schätzung | Brainstorming |
| Input-Tokens pro Nachricht | 3.000-8.000 | Schätzung | Erfahrungswert LLM-Anwendungen |
| LLM-Preis Input | ~3$/M Tokens | Benchmark | Claude Sonnet 4.5 Preis |
| LLM-Preis Output | ~15$/M Tokens | Benchmark | Claude Sonnet 4.5 Preis |
| % User mit Coach-Eingriff/Monat | 5% | Schätzung | Brainstorming |
| Ø Bearbeitungszeit/Fall | 20 Min | Schätzung | Brainstorming |
| Coach-Stundensatz | 40-60€ | Schätzung | Marktüblich |
| CAC | 30-80€ | Benchmark | Fitness-App-Markt |
| Ø Nutzungsdauer | 10 Monate | Schätzung | Optimistisch mittelfristig |
| Break-even User-Anzahl | 3.000-5.000 | Schätzung | Grobe Hochrechnung |

---

## 15. Nächste Schritte (für dieses Dokument)

1. Konkrete Modell-Entscheidung treffen → LLM-Kosten präzisieren
2. Mindestens 3 vergleichbare Anbieter benchmarken (Preis, Features, vermutete Marge)
3. Erste Cohort-Simulation bauen (Excel/Notion) → Break-even-Punkt darstellen
4. Annahmen-Tracker regelmäßig überprüfen und mit realen Daten ersetzen, sobald verfügbar