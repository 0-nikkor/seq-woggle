# SeqWoggle V4.8 — Documentazione

## Panoramica

Firmware per ESP32 (C3 / S3 SuperMini) con quattro programmi indipendenti:
- **Seq** — Sequencer random quantizzato con Euclidean gate
- **Woggle** — Generatore CV caotico con burst
- **CLKD** — Clock divider/multiplier dual con S&H CV quantizzato
- **JAZZ** — Generatore melodico generativo ispirato all'improvvisazione jazz

---

## Pin

| Funzione      | GPIO |
|---------------|------|
| CLOCK_PIN     | 21   |
| BURST_PIN     | 3    |
| CV_PIN (PWM)  | 2    |
| ENC_CLK       | 4    |
| ENC_DT        | 5    |
| ENC_SW        | 6    |
| LCD_SDA       | 8    |
| LCD_SCL       | 9    |

LCD: HD44780 I²C, 16×2.

---

## UI — Navigazione

| Azione                          | Effetto                                      |
|---------------------------------|----------------------------------------------|
| Ruota encoder                   | Cambia il valore del parametro corrente      |
| Short press                     | Avanza al modo successivo                    |
| Long press (≥900 ms) in PROGRAM | Attiva il programma selezionato              |
| Long press in WOG PRESET        | Carica il preset selezionato                 |

In **MODE_PROGRAM**: ruotare l'encoder scorre tra Seq / Woggle / CLKD in anteprima.
Il programma si avvia solo con long press.
Il display mostra `>NomeSelezionato [AttivoCorrente]` durante la selezione.

---

## Programma: SEQ

Sequencer melodico random con scala, swing, jitter, lock e gate euclideo.

| Modo             | Parametro                          | Range              |
|------------------|------------------------------------|--------------------|
| TEMPO            | Intervallo clock                   | 60ms – 60s         |
| PWM FREQ         | Frequenza portante PWM su CV_PIN   | 48Hz – 20kHz       |
| SWING            | Swing amount                       | 0.00 – 0.35        |
| JITTER           | Jitter random sul tempo            | 0 – 50%            |
| RANGE            | Range note                         | 1 – 40             |
| SCALE            | Scala musicale (20 scale)          | 0 – 19             |
| TRANSPOSE        | Trasposizione semitoni             | -11 – +11          |
| MUTE             | Probabilità silenziare gate        | 0 – 100%           |
| LOCK LEN         | Lunghezza sequenza bloccata        | 0 – 128 steps      |
| LOCK PROB        | Probabilità mutazione lock         | 0 – 100%           |
| GATE LEN         | Durata gate (0=random 5-95%)       | 0 – 95%            |
| EUC HITS         | Hit euclidei su BURST_PIN          | 0 – len            |
| EUC ROT          | Rotazione pattern euclideo         | 0 – len-1          |
| TUNE             | Fattore di scala CV                | 35.0 – 39.6        |

---

## Programma: WOGGLE

Generatore CV caotico con lag, mix stepped/smooth e burst di trigger.

| Modo    | Parametro                            | Range        |
|---------|--------------------------------------|--------------|
| PRESET  | Preset (9 presets)                   | 1–9          |
| RATE    | Velocità base                        | 35ms – 5s    |
| CHAOS   | Caoticità del movimento CV           | 0 – 100%     |
| B.PROB  | Probabilità burst                    | 0 – 100%     |
| B.MIN   | Pulse burst minimi                   | 1 – 16       |
| B.MAX   | Pulse burst massimi                  | 1 – 16       |
| B.SPRD  | Spread timing burst                  | 0 – 100%     |
| LAG     | Lag (smoothing exponenziale)         | 0 – 100%     |
| MIX     | Mix stepped / smooth                 | 0 – 100%     |
| JIT     | Jitter sul rate                      | 0 – 50%      |
| PULSE   | Larghezza pulse burst                | 500 – 20000µs|
| PWM     | Frequenza portante CV                | 1 – 30kHz    |

Presets: ClockedRnd, Woggle, TotalChaos, MelodicDrf, RatchetBug,
GhostNotes, DrunkenWlk, BurstStorm, AmbientTail.

---

## Programma: CLKD

Clock divider/multiplier duale con Sample & Hold CV **quantizzato su scala musicale**.

| Uscita    | Pin        | Funzione                                              |
|-----------|------------|-------------------------------------------------------|
| CLK1      | CLOCK_PIN  | Clock con ratio selezionabile (gate 50%)              |
| CLK2      | BURST_PIN  | Secondo clock con ratio indipendente (gate 50%)       |
| S&H CV    | CV_PIN     | Stepped random quantizzato, aggiornato su ogni tick CLK1 |

| Modo  | Parametro          | Range              |
|-------|--------------------|--------------------|
| BPM   | Battiti per minuto | 1 – 300 BPM        |
| CLK1  | Ratio CLK1         | /8 … x8 (17 step)  |
| CLK2  | Ratio CLK2         | /8 … x8 (17 step)  |
| SCALE | Scala musicale     | 0–19 (20 scale)    |

Ratios: /8, /6, /5, /4, /3, /2.5, /2, /1.5, x1, x1.5, x2, x2.5, x3, x4, x5, x6, x8

**S&H quantizzato**: ogni tick CLK1 produce una nota random scelta tra le note
valide della scala corrente, su un range di 40 semitoni, mappata su PWM 10-bit
con la stessa formula tuneFactor=39.6 del Sequencer.

Scale disponibili (identiche a SEQ):
Blues, C7, F7, G7, Major, MelodicMinor, Pentatonic, Chromatic,
MinorNat, MinorHarm, MajPent, MinPent, Dorian, Mixolydian, Diminish,
WholeTone, Altered, Persian, Hijaz, Flamenco.

---

## NVS — Namespace Preferences

| Namespace  | Contenuto                           |
|------------|-------------------------------------|
| global48   | Programma attivo, editMode          |
| seq48      | Tutti i parametri Sequencer         |
| wog48      | Tutti i parametri Woggle            |
| clkd48     | BPM, clk1Idx, clk2Idx, scaleIdx    |

Salvataggio automatico con debounce di 1500 ms dall'ultima modifica.

---

## File

| File                        | Descrizione                        |
|-----------------------------|------------------------------------|
| SeqWoggle_V4_8_clkd.ino     | Firmware principale                |
| clkd.h                      | Modulo CLKD (namespace clkd::)     |
| agents.md                   | Questa documentazione              |
| jazz.h                      | Modulo JAZZ (namespace jazz::)     |

---

## Programma: JAZZ

Generatore melodico generativo ispirato all'improvvisazione jazz.

| Uscita  | Pin        | Funzione                                        |
|---------|------------|-------------------------------------------------|
| CLK1    | CLOCK_PIN  | Clock melodia (gate 50% dell'intervallo)        |
| CLK2    | BURST_PIN  | Accenti (Contour / Sincopato / mix)             |
| CV      | CV_PIN     | Melodia quantizzata con passing tones cromatici |

### Parametri

| Modo     | Parametro                          | Range              | Default  |
|----------|------------------------------------|--------------------|----------|
| BPM      | Tempo base (riferimento 1/8)       | 40 – 280 BPM       | 120      |
| SCALE    | Scala musicale (20 scale)          | 0 – 19             | Major    |
| RANGE    | Range cursore melodico             | 4 – 40 semitoni    | 16       |
| CHAOS    | Bias random vs scalare             | 0 – 100%           | 25%      |
| FLUIDITY | Prob. cambio ritmo tra frasi       | 0 – 100%           | 70%      |
| INTRA    | Prob. cambio ritmo dentro frase    | 0 – 100%           | 20%      |
| ACCENT   | Mix Contour/Sincopato su CLK2      | 0=Contour 100=Sync | 50%      |
| BREATH   | Prob. pausa tra frasi              | 0 – 100%           | 30%      |
| EDGE     | Comportamento ai bordi del range   | Bounce/Wrap/Fold   | Bounce   |

### Logica melodica

Il cursore si muove principalmente per **gradi scalari** con bias direzionale e
momentum (inerzia). Ogni frase ha lunghezza 6–16 note con un arco (salita/discesa).

**Tipi di movimento:**
- Scalare (1 grado su/giù) — predominante
- Arpeggio (salto 2–3 gradi) — con probabilità legata a CHAOS
- Cromatico (passing tone ±1 semitono) — solo in TRIPLET o SIXTEENTH

### Ritmo adattivo

Tre celle ritmiche con matrice di transizione pesata:

| Cell       | Durata nota       |
|------------|-------------------|
| EIGHTH     | 1/8 base          |
| TRIPLET    | 1/8 × 2/3         |
| SIXTEENTH  | 1/8 × 1/2         |

Cambio cell prevalentemente tra frasi (FLUIDITY), occasionalmente dentro (INTRA,
max 1 cambio per frase). I cromatismi sono abilitati solo in TRIPLET e SIXTEENTH.

### Accenti CLK2

- **Contour** (ACCENT=0%): accento quando la nota è il picco locale degli ultimi 4 step
- **Sincopato** (ACCENT=100%): accento su beat deboli (2, 4, "e" di 3)
- **Mix** (0–100%): somma pesata delle due probabilità

### Edge modes

| Modalità | Comportamento                                      |
|----------|----------------------------------------------------|
| Bounce   | Inversione secca di direzione al bordo             |
| Wrap     | Salta all'estremo opposto del range                |
| Fold     | Come Bounce ma con decay graduale del momentum (3 note) |

### NVS namespace: `jazz48`

Salva: bpm, scale, range, chaos, fluidity, intra, accent, breath, edge.
