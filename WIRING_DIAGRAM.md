# 🔌 WIRING DIAGRAM - ΑΠΛΟΠΟΙΗΜΕΝΟ ΗΛΙΑΚΟ ΣΥΣΤΗΜΑ

## 📋 Τελική Διάταξη (Μόνο Ηλιακό)

```
┌──────────────────────────────────────────────────────────────────────────┐
│                   ΕΝΕΡΓΕΙΑΚΑ ΑΥΤΟΝΟΜΟ ΣΥΣΤΗΜΑ ESP32-C6                   │
│                        (ΜΟΝΟ ΗΛΙΑΚΗ ΦΟΡΤΙΣΗ)                            │
└──────────────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────────────┐
│                         ΦΩΤΟΒΟΛΤΑΪΚΟ ΠΑΝΕΛ                              │
│                    Optum HR0472 (6V 3.5W Output)                        │
│                         165x135x20mm                                    │
└─────────────────────────────────────────────────────────────────────────┘
                    │                    │
                    │ Positive (+)      │ Negative (-)
                    │ (Red Cable)       │ (Black Cable)
                    ▼                    ▼
┌──────────────────────────────────────────────────────────────────────────┐
│           OPTUM SOLAR LITHIUM BATTERY CHARGER BOARD                      │
│                                                                          │
│  • Input: 6V DC (από ηλιακό πάνελ)                                     │
│  • Output: Φόρτιση μπαταρίας 3.7V με προστασία                         │
│  • MPPT Controllers για καλή απόδοση                                   │
│  • Max Charging Current: ~500mA                                        │
│  • Protection: Over-charge, Over-discharge                             │
│                                                                          │
│  INPUT: ─────────────────────────────────────────────── OUTPUT:       │
│  (+) Red ─────────────────────────────────────────────→ (+) Red       │
│  (-) Black ───────────────────────────────────────────→ (-) Black     │
└──────────────────────────────────────────────────────────────────────────┘
            │                                              │
            │ Red Wire (+3.7V)                           │ Black Wire (GND)
            ▼                                              ▼
┌──────────────────────────────────────────────────────────────────────────┐
│              HAITRONIC 18650 BATTERY CASE/HOLDER                         │
│                                                                          │
│  • Panasonic 18650 3.7V Lithium Battery (2600-3000mAh)                 │
│  • Ενσωματωμένα καλώδια για εύκολη σύνδεση                            │
│  • Voltage: 3.0V (depleted) → 3.7V (nominal) → 4.2V (full)            │
│  • Capacity: ~10-12 Wh (2600-3000mAh × 3.7V)                           │
│  • Recharge Time: ~3-4 hours (with 3.5W solar panel)                   │
│                                                                          │
│  ┌──────────────────────────────────────────────────────┐              │
│  │  (+) RED WIRE    ← Charging positive                 │              │
│  │  │               ← Discharging positive to DC/DC     │              │
│  │  │ [18650]                                           │              │
│  │  │ 3.7V Nominal                                      │              │
│  │  │               ← Discharging negative to DC/DC     │              │
│  │  (-) BLACK WIRE  ← Charging negative (GND)           │              │
│  └──────────────────────────────────────────────────────┘              │
└──────────────────────────────────────────────────────────────────────────┘
            │                                              │
            │ (+) Red Wire (3.7V)                        │ (-) Black Wire (GND)
            ▼                                              ▼
┌──────────────────────────────────────────────────────────────────────────┐
│         HAITRONIC DC/DC STEP-DOWN CONVERTER (HS2670)                     │
│                                                                          │
│  Λειτουργία: Μετατροπή 3.7V → 3.3V με ρύθμιση                         │
│                                                                          │
│  INPUT:             POTENTIOMETER:        OUTPUT:                      │
│  ───────            ─────────────         ──────                       │
│  IN+ (Red)          /\/\/\                OUT+ (Red) ──→ 3.3V         │
│  │                  (Adjustment)          │                           │
│  │                  Rotate clockwise      │                           │
│  │                  for higher V          │                           │
│  │                                        │                           │
│  IN- (Black) ──────────────────────────→ OUT- (Black) ──→ GND        │
│                                                                          │
│  ⚙️ ΡΥΘΜΙΣΗ:                                                            │
│  1. Συνδέστε Multimeter στα OUTPUT pins                               │
│  2. Ρυθμίστε την δοσομετρική βίδα μέχρι να δείξει 3.3V                │
│  3. Ελάχιστη ακρίβεια: 3.25V - 3.35V (ιδανικά 3.30V)                 │
│  4. Σταθεροποιήστε με κολλητό κερί όταν ρυθμιστεί                     │
│                                                                          │
│  Specifications:                                                        │
│  • Input: 3.0V - 5.5V (Battery: 3.0-4.2V ✓)                           │
│  • Output: Ρυθμιζόμενο (Set to 3.3V)                                  │
│  • Max Current: 2A continuous                                         │
│  • Efficiency: ~92% (minimal heat)                                    │
│  • Quiescent Current: 2-5mA (negligible)                              │
└──────────────────────────────────────────────────────────────────────────┘
            │ OUT+ (3.3V)                       │ OUT- (GND)
            │ Red Wire                          │ Black Wire
            ▼                                    ▼
┌──────────────────────────────────────────────────────────────────────────┐
│          HAITRONIC 170-POINT BREADBOARD (Blue)                           │
│                     170 θέσεων - Χωρίς τσιμούχες                       │
│                                                                          │
│  ┌────────────────────────────────────────────────────────────┐         │
│  │ TOP POWER RAIL:                                            │         │
│  │ ┏━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓   │         │
│  │ ┃ (+) 3.3V Rail ← Connected to DC/DC OUT+ (RED)        ┃   │         │
│  │ ┃ (-) GND Rail ← Connected to DC/DC OUT- (BLACK)       ┃   │         │
│  │ ┗━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┛   │         │
│  │                                                            │         │
│  │ SIGNAL ROWS (A-O):                                         │         │
│  │ ├─ Row A: Available for jumper wires                       │         │
│  │ ├─ Row B: Available for jumper wires                       │         │
│  │ ├─ ...                                                     │         │
│  │ ├─ Row E: Available for jumper wires                       │         │
│  │ │                                                          │         │
│  │ ├─ [ESP32-C6 will be inserted here]                        │         │
│  │ │                                                          │         │
│  │ └─ Row O: Available for sensors/LEDs                       │         │
│  │                                                            │         │
│  │ BOTTOM POWER RAIL:                                         │         │
│  │ ┏━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓   │         │
│  │ ┃ (+) 3.3V Rail (parallel to top)                      ┃   │         │
│  │ ┃ (-) GND Rail (parallel to top, for redundancy)       ┃   │         │
│  │ ┗━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┛   │         │
│  └────────────────────────────────────────────────────────────┘         │
│                                                                          │
│  Καπάκια Σταθεροποίησης (Bypass Capacitors):                           │
│  ├─ 100µF Electrolytic Cap: + at 3.3V rail, - at GND rail             │
│  └─ 10µF Ceramic Cap: + at 3.3V rail, - at GND rail                   │
│     (Ελαχιστοποίηση θορύβου & απότομα ρεύματα)                        │
└──────────────────────────────────────────────────────────────────────────┘
                    │                                │
                    │ 3.3V Power                    │ GND Reference
                    ▼                                ▼
┌──────────────────────────────────────────────────────────────────────────┐
│                    SEEED XIAO ESP32-C6 DEVELOPMENT BOARD                 │
│                                                                          │
│  Insertion into Breadboard:                                            │
│  ┌────────────────────────────────────────┐                           │
│  │  D0/GPIO0   GND      D1/GPIO1   3V3   │                           │
│  │  D2/GPIO2   D3/GPIO3 D4/GPIO4   D5   │                           │
│  │  D6/GPIO6   D7/GPIO7 D8/GPIO8   D9   │                           │
│  │  D10/GPIO10 GND      D11/GPIO11 5V   │                           │
│  └────────────────────────────────────────┘                           │
│                                                                          │
│  Power Connections:                                                    │
│  ├─ Pin 12 (3V3) ─→ Breadboard 3.3V Rail (RED)                        │
│  └─ Pin 11 (GND) ─→ Breadboard GND Rail (BLACK)                       │
│                                                                          │
│  Recommended GPIO for Battery Monitoring:                              │
│  └─ Pin 5 (D5/GPIO5 - ADC_CH4) ─→ Battery voltage divider             │
│     (Measure battery level during operation)                           │
│                                                                          │
│  MCU Specifications:                                                   │
│  • Processor: ESP32-C6 RISC-V                                         │
│  • RAM: 512KB SRAM                                                    │
│  • Flash: 4MB                                                         │
│  • WiFi: 802.11 b/g/n                                                 │
│  • ADC: 12-bit, 6 channels                                            │
│  • Deep Sleep Current: <10µA ◄─ Ultra-low power                       │
│  • Active Current: 80-100mA                                           │
│  • WiFi TX Current: 200-300mA (peak)                                  │
│  • Voltage Range: 3.0V - 3.6V (⚠️ NOT 5V tolerant!)                   │
│  • Max GPIO Current (combined): 500mA                                 │
│                                                                          │
│  USB Debug Port:                                                       │
│  └─ Connect via USB cable for programming & serial monitor            │
└──────────────────────────────────────────────────────────────────────────┘
```

---

## 🔌 Απλοποιημένος Πίνακας Συνδέσεων

| # | Από | Προς | Χρώμα | Μήκος | Σημείωση |
|---|-----|------|-------|--------|----------|
| 1 | Solar Panel (+) | Charger IN (+) | Red | ~20cm | Input 6V |
| 2 | Solar Panel (-) | Charger IN (-) | Black | ~20cm | Ground |
| 3 | Charger OUT (+) | Battery Case (+) | Red | ~10cm | Pass-through |
| 4 | Charger OUT (-) | Battery Case (-) | Black | ~10cm | Ground |
| 5 | Battery (+) | DC/DC IN (+) | Red | ~15cm | 3.7V input |
| 6 | Battery (-) | DC/DC IN (-) | Black | ~15cm | Ground |
| 7 | DC/DC OUT (+) | Breadboard 3.3V Rail | Red | ~10cm | 3.3V supply |
| 8 | DC/DC OUT (-) | Breadboard GND Rail | Black | ~10cm | Ground |
| 9 | Breadboard 3.3V | ESP32 Pin 12 (3V3) | Red | ~5cm | Power |
| 10 | Breadboard GND | ESP32 Pin 11 (GND) | Black | ~5cm | Ground |
| - | Capacitor 100µF | Breadboard Rails | - | - | Smoothing |
| - | Capacitor 10µF | Breadboard Rails | - | - | High-freq noise |

---

## ⚡ Power Flow Diagram

```
ΗΛΙΟΣ
  │
  ▼
┌────────────────────┐
│  Solar Panel       │
│  6V @ 3.5W Max     │
└────────────────────┘
  │
  ▼
┌────────────────────┐
│ Optum Charger      │
│ (MPPT optimized)   │
└────────────────────┘
  │
  ▼
┌────────────────────┐      Δημέρα:    Νύχτα:
│  18650 Battery     │      Φορτίζει    Τροφοδοτεί
│  3.7V @ 2600mAh    │      ↓           ↓
│  9.6Wh Total       │
└────────────────────┘
  │
  ▼
┌────────────────────┐
│ DC/DC Converter    │
│ 3.7V → 3.3V        │
│ 92% Efficient      │
└────────────────────┘
  │
  ▼
┌────────────────────┐
│ Breadboard         │
│ 3.3V Power Rail    │
└────────────────────┘
  │
  ▼
┌────────────────────┐
│ ESP32-C6           │
│ • WiFi             │
│ • Processing       │
│ • ADC readings     │
│ • Deep Sleep mode  │
└────────────────────┘
```

---

## 🎯 Τοποθέτηση Εξαρτημάτων

```
┌─────────────────────────────────────────────────┐
│            TYPICAL INSTALLATION                 │
├─────────────────────────────────────────────────┤
│                                                 │
│  [SOLAR PANEL]  ◄─ Mounted outdoor/sunny spot  │
│       ↓                                         │
│  [Weather-proof enclosure]                      │
│  ├─ Optum Charger Board                        │
│  ├─ Battery Case (18650)                       │
│  └─ Cables in/out                              │
│       ↓                                         │
│  [Main box/enclosure]                          │
│  ├─ DC/DC Converter                            │
│  ├─ Breadboard with ESP32                      │
│  ├─ Capacitors                                 │
│  └─ Jumper wires                               │
│                                                 │
│  Καλώδια σύνδεσης:                             │
│  • Solar to Charger: Thick wires (20 AWG)      │
│  • Charger to Battery: Medium (22 AWG)         │
│  • Battery to DC/DC: Medium (22 AWG)           │
│  • DC/DC to Breadboard: Thin (24 AWG)          │
│                                                 │
└─────────────────────────────────────────────────┘
```

---

## ✅ Βήματα Συνδέσμολογίας (Step by Step)

### **Βήμα 1: Προετοιμασία**
- [ ] Αποσυναρμολόγηση όλων των εξαρτημάτων
- [ ] Έλεγχος τάσης solar panel με multimeter (θα δείξει 0V χωρίς ήλιο)
- [ ] Ετοιμάστε καλώδια & jumpers

### **Βήμα 2: Σύνδεση Solar Panel → Charger**
```
1. Ηλιακό Panel: Red (+) → Charger IN (+)
2. Ηλιακό Panel: Black (-) → Charger IN (-)
3. ✅ Ελέγχει ότι η τάση εμφανίζεται στα OUT pins (~3.7V)
```

### **Βήμα 3: Σύνδεση Charger → Battery**
```
1. Charger OUT (+) → Battery Case (+)
2. Charger OUT (-) → Battery Case (-)
3. ✅ Μην συνδέσετε άλλα εξαρτήματα ακόμα!
```

### **Βήμα 4: Σύνδεση Battery → DC/DC**
```
1. Battery (+) → DC/DC IN (+)
2. Battery (-) → DC/DC IN (-)
3. ⚙️ Ρυθμίστε DC/DC potentiometer για 3.3V output
   (Χρησιμοποιήστε multimeter για μέτρηση)
4. ✅ Σταθεροποιήστε με κολλητό κερί
```

### **Βήμα 5: Σύνδεση DC/DC → Breadboard**
```
1. DC/DC OUT (+) → Breadboard 3.3V Rail (κόκκινη)
2. DC/DC OUT (-) → Breadboard GND Rail (μαύρη)
3. Προσθέστε 100µF capacitor στις ράγες τροφοδοσίας
4. ✅ Μετρήστε: 3.3V μεταξύ 3.3V & GND rails
```

### **Βήμα 6: Σύνδεση Breadboard → ESP32**
```
1. Εισαγάγετε ESP32 στο breadboard κεντρικά
2. ESP32 Pin 12 (3V3) → Breadboard 3.3V Rail
3. ESP32 Pin 11 (GND) → Breadboard GND Rail
4. ✅ Μετρήστε: 3.3V στα VCC pins του ESP32
```

### **Βήμα 7: Προαιρετική Παρακολούθηση Μπαταρίας**
```
1. Διαιρέτης τάσης (10kΩ + 10kΩ):
   Battery (+) ──[10kΩ]──┬──[10kΩ]── Battery (-)
                         │
                         └──→ ESP32 GPIO5 (ADC_CH4)
2. Αυτό σας δίνει 1.85V στο ADC (μέσα στο εύρος 0-3.3V)
```

---

## 🔍 Επαληθεύσεις Μετρήσεων

| Σημείο | Αναμενόμενη Τάση | Ανοχή | Εργαλείο | Status |
|--------|-----------------|--------|---------|--------|
| Solar Panel (μεσημέρι) | ~6V | ±0.5V | Multimeter | ✓ |
| Charger OUT (κατά φόρτιση) | ~3.7V | ±0.2V | Multimeter | ✓ |
| Battery (+) | 3.0-4.2V | Full range | Multimeter | ✓ |
| DC/DC OUT | 3.3V | ±0.05V | Multimeter | ✓ |
| Breadboard Rail | 3.3V | ±0.1V | Multimeter | ✓ |
| ESP32 VCC | 3.3V | ±0.1V | Multimeter | ✓ |
| ESP32 GND | 0V | Reference | Multimeter | ✓ |

---

## ⚠️ Κοινά Λάθη & Δικαιώματα

| Λάθος | Αιτία | Λύση |
|-------|-------|------|
| ESP32 δεν ανάβει | Χαμηλή τάση DC/DC | Ρυθμίστε DC/DC για 3.3V |
| Battery σε κύκλο φόρτισης | Σφάλμα πολικότητας | Ελέγχετε Red/Black wires |
| Καμένο DC/DC | Υπέρταση input | Ελέγχετε ότι battery < 4.2V |
| Breadboard χωρίς ρεύμα | Φύτευση δύσκολη | Πιέστε pins κάθετα |

---

## 📊 Αυτονομία & Διάρκεια Ζωής

```
Scenario 1: Deep Sleep Mode (Recommended)
───────────────────────────────────────
• ESP32 ξυπνάει κάθε 10 λεπτά
• Λαμβάνει μετρήσεις: 2 δευτερόλεπτα
• Το υπόλοιπο: Deep sleep @ 10µA

Κατανάλωση:
1. Deep Sleep: 10µA × 600s = 6 mC per cycle
2. Wake + Measure: 80mA × 2s = 160 mC per cycle
3. Total: ~166 mC per 10min = ~1 mAh per hour
4. Battery: 2600mAh ÷ 1mAh/hr = 2600 hours = ~108 days

Με ηλιακό: ΑΝΕΞΑΡΤΗΤΗ ΛΕΙΤΟΥΡΓΙΑ (indefinite) ✅

───────────────────────────────────────

Scenario 2: WiFi Every Hour (10 seconds)
───────────────────────────────────────
• Deep sleep: 59.9 λεπτά
• WiFi TX: 10 δευτερόλεπτα

Κατανάλωση:
1. Deep Sleep: 10µA × 3594s = 36 mC per hour
2. WiFi TX: 250mA × 10s = 2500 mC per hour
3. Total: ~2536 mC = 2.5 mAh per hour
4. Battery: 2600mAh ÷ 2.5mAh/hr = 1040 hours = ~43 days

Με ηλιακό: ΑΝΕΞΑΡΤΗΤΗ ΛΕΙΤΟΥΡΓΙΑ (indefinite) ✅
```

---

## 🚀 Επόμενο Βήμα

Δείτε **`firmware/main.cpp`** για τον κώδικα ESP32-C6 που περιλαμβάνει:
- ✅ Power management & deep sleep
- ✅ Battery voltage monitoring
- ✅ WiFi connectivity
- ✅ MQTT publishing
- ✅ Graceful shutdown

---

**Σημ.**: Το TP4056 δεν χρησιμοποιείται σε αυτή την διάταξη.
