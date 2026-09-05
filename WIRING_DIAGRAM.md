# 🔌 Αναλυτικό Διάγραμμα Συνδέσεων - ESP32-C6 Solar System

## 📋 Γενικό Διάγραμμα Συστήματος

```
┌──────────────────────────────────────────────────────────────────────────┐
│                   ΕΝΕΡΓΕΙΑΚΑ ΑΥΤΟΝΟΜΟ ΣΥΣΤΗΜΑ ESP32-C6                   │
└──────────────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────────────┐
│                         ΦΩΤΟΒΟΛΤΑΪΚΟ ΠΑΝΕΛ                              │
│                    Optum HR0472 (6V 3.5W Output)                        │
│                         165x135x20mm                                    │
└─────────────────────────────────────────────────────────────────────────┘
                    │                    │
                    │ Positive (+)      │ Negative (-)
                    ▼                    ▼
┌──────────────────────────────────────────────────────────────────────────┐
│           OPTUM SOLAR LITHIUM BATTERY CHARGER BOARD                      │
│  • Input: 6V (από ηλιακό πάνελ)                                         │
│  • Output: Φόρτιση μπαταρίας 3.7V με προστασία                          │
│  • MPPT Controllers για καλή απόδοση                                    │
└──────────────────────────────────────────────────────────────────────────┘
            │                                  │
            │ Positive (+)                    │ Negative (-)
            ▼                                  ▼
┌──────────────────────────────────────────────────────────────────────────┐
│              HAITRONIC 18650 BATTERY CASE/HOLDER                         │
│  • Panasonic 18650 3.7V Lithium Battery (2600-3000mAh)                  │
│  • Ενσωματωμένα καλώδια για εύκολη σύνδεση                             │
│  • Voltage: 3.7V nominal (3.0V - 4.2V range)                            │
│  • Capacity: ~10-12 Wh (2600-3000mAh × 3.7V)                            │
└──────────────────────────────────────────────────────────────────────────┘
            │                                  │
            │ (+) Battery Positive            │ (-) Battery Negative
            ▼                                  ▼
┌──────────────────────────────────────────────────────────────────────────┐
│         HAITRONIC DC/DC STEP-DOWN CONVERTER (HS2670)                     │
│  • Input: 5-12V (Ελαστικό εύρος)                                        │
│  • Output Options: 24V, 12V, 5V, 3.3V (Ρυθμιζόμενο)                     │
│  • Current: Max 2A (σχετικά)                                            │
│  • Protection: Over-current, Over-voltage                               │
│  ┌─────────────────────────────────────────────────────────────┐       │
│  │ INPUT SIDE        │  ADJUSTMENT  │ OUTPUT SIDE              │       │
│  ├──────────────────┼──────────────┼──────────────────────────┤       │
│  │ IN+ (Red)        │ Potentiometer│ OUT+ (Red)               │       │
│  │ IN- (Black)      │              │ OUT- (Black)             │       │
│  └──────────────────┴──────────────┴──────────────────────────┘       │
│                                                                         │
│  ⚙️ ΡΥΘΜΙΣΗ: Στρέψτε την δοσομετρική βίδα για 3.3V output             │
│  (Μετρήστε με Multimeter)                                             │
└──────────────────────────────────────────────────────────────────────────┘
            │                                  │
            │ OUT+ (3.3V)                     │ OUT- (GND)
            ▼                                  ▼
┌──────────────────────────────────────────────────────────────────────────┐
│          HAITRONIC 170-POINT BREADBOARD (Blue)                           │
│                     170 θέσεων - Χωρίς τσιμούχες                       │
├──────────────────────────────────────────────────────────────────────────┤
│  Power Rails:                                                            │
│  ├─ TOP: (+) 3.3V Rail (Κόκκινο)                                        │
│  ├─ TOP: (-) GND Rail (Μαύρο)                                           │
│  └─ BOTTOM: Additional GND (για παράλληλες συνδέσεις)                   │
│                                                                         │
│  Signal Rows:                                                           │
│  ├─ Row A-E: ESP32-C6 GPIO Pins                                        │
│  ├─ Row F-J: Αισθητήρες / Έξοδοι                                       │
│  └─ Row K-O: Αναφορά & διασταυρούμενες συνδέσεις                        │
└──────────────────────────────────────────────────────────────────────────┘
                    │                    │
                    │ 3.3V               │ GND
                    ▼                    ▼
┌──────────────────────────────────────────────────────────────────────────┐
│                    SEEED XIAO ESP32-C6 DEVELOPMENT BOARD                 │
│                                                                         │
│  Pinout (Top View):                                                    │
│  ┌─────────────────────────────────────────────────┐                  │
│  │ D0/GPIO0    GND         D1/GPIO1    3V3        │                  │
│  │ D2/GPIO2    D3/GPIO3    D4/GPIO4    D5/GPIO5   │                  │
│  │ D6/GPIO6    D7/GPIO7    D8/GPIO8    D9/GPIO9   │                  │
│  │ D10/GPIO10  GND         D11/GPIO11  5V(USB)    │                  │
│  └─────────────────────────────────────────────────┘                  │
│                                                                         │
│  Key Features:                                                         │
│  • MCU: ESP32-C6 (RISC-V + 802.11b/g/n WiFi)                          │
│  • RAM: 512KB SRAM                                                     │
│  • Flash: 4MB                                                          │
│  • ADC: 12-bit (6 channels)                                           │
│  • Deep Sleep: <10µA                                                   │
│  • Operating Voltage: 3.0V - 3.6V                                      │
│  • Max Current: 500mA (all pins combined)                              │
│  • GPIO: All pins 3.3V (NOT 5V tolerant!)                             │
└──────────────────────────────────────────────────────────────────────────┘
```

---

## 🔌 Λεπτομερής Σύνδεση Καλωδίων

### **Σύνδεση 1: Ηλιακό Πάνελ → Charger Board**
```
Optum HR0472 Solar Panel
├─ Red Wire (+6V)  ──→ Optum Charger Board Input (+)
└─ Black Wire (GND) ──→ Optum Charger Board Input (-)
```

### **Σύνδεση 2: Charger Board → Μπαταρία**
```
Optum Charger Board Output
├─ Red Wire (+)  ──→ Battery Case (+) connector
└─ Black Wire (-) ──→ Battery Case (-) connector

⚠️ ΠΡΟΣΟΧΗ: Μη ανατρέψετε την πολικότητα!
```

### **Σύνδεση 3: Μπαταρία → DC/DC Converter**
```
Panasonic 18650 Battery (3.7V)
├─ Red Wire (+3.7V)  ──→ DC/DC Converter INPUT (+)
└─ Black Wire (GND)  ──→ DC/DC Converter INPUT (-)

🔧 ΡΥΘΜΙΣΗ DC/DC:
1. Συνδέστε Multimeter στα OUTPUT pins
2. Ρυθμίστε την δοσομετρική βίδα για 3.3V output
3. Χαλαρώστε δεξιόστροφα για ↑ τάση
4. Χαλαρώστε αριστερόστροφα για ↓ τάση
```

### **Σύνδεση 4: DC/DC Converter → Breadboard**
```
DC/DC Converter Output
├─ Red Wire (3.3V)  ──→ Breadboard POWER RAIL (+)
├─ Black Wire (GND) ──→ Breadboard POWER RAIL (-)
└─ [Optional] 100µF Capacitor in parallel 
   (Ελαχιστοποιεί θόρυβο & σταθεροποιεί τάση)
```

### **Σύνδεση 5: Breadboard → ESP32-C6**
```
Breadboard (Power Rails)
├─ 3.3V Rail ──→ ESP32-C6 Pin: 3V3 (top right)
├─ GND Rail  ──→ ESP32-C6 Pin: GND (multiple pins available)
└─ GND Rail  ──→ ESP32-C6 Pin: GND (for redundancy)

🔌 Pin Diagram (Seeed XIAO ESP32-C6):
┌────────────────────────────────────┐
│ Pin 12 (3V3)  ← 3.3V Rail (+)      │
│ Pin 11 (GND)  ← GND Rail (-)       │
│ Pin 1 (D0)    ← GPIO0 (Optional)   │
└────────────────────────────────────┘
```

---

## 🔋 Πλήρες Wiring Table

| Σύνδεση | From | To | Color | Σημειώσεις |
|---------|------|------|-------|-----------|
| **1a** | Solar Panel (+) | Charger IN (+) | Red | 6V input |
| **1b** | Solar Panel (-) | Charger IN (-) | Black | Ground |
| **2a** | Charger OUT (+) | Battery Case (+) | Red | 3.7V charging |
| **2b** | Charger OUT (-) | Battery Case (-) | Black | Ground |
| **3a** | Battery (+) | DC/DC IN (+) | Red | 3.7V input |
| **3b** | Battery (-) | DC/DC IN (-) | Black | Ground |
| **4a** | DC/DC OUT (+) | Breadboard Power + | Red | 3.3V regulated |
| **4b** | DC/DC OUT (-) | Breadboard Power - | Black | Ground |
| **5a** | Breadboard Power + | ESP32 Pin 12 (3V3) | Red | Main power |
| **5b** | Breadboard Power - | ESP32 Pin 11 (GND) | Black | Main ground |
| **CAP** | 100µF Capacitor | Breadboard Power Rails | - | ± 10µF tolerance |

---

## ⚡ Power Distribution Plan

```
                 BATTERY (3.7V, 2600mAh)
                        │
                        ▼
                    [3.7V = 9.6Wh]
                        │
                        ▼
            ┌───────────────────────────┐
            │   DC/DC CONVERTER         │
            │   Input: 3.7V             │
            │   Output: 3.3V @ 2A MAX   │
            │   Eff: ~92%               │
            └───────────────────────────┘
                        │
                ┌───────┴────────┐
                ▼                ▼
          [Breadboard]      [ESP32-C6]
          Power Rails       (VCC/GND)
          (3.3V ± GND)
                │                │
                ▼                ▼
          [Sensors]         [WiFi/GPIO]
          (optional)        (MCU Core)
```

---

## 🎯 Voltage Levels at Each Stage

| Stage | Min Voltage | Nominal | Max Voltage | Tolerance |
|-------|-------------|---------|-------------|-----------|
| Solar Panel | 4.5V | 6V | 7V | ± 1V |
| Battery (discharged) | 3.0V | 3.7V | 4.2V (charged) | Full range |
| DC/DC Input | 3.0V | 3.7V | 4.2V | ✓ Within range |
| DC/DC Output | 3.2V | **3.3V** | 3.4V | ✓ Regulated |
| ESP32-C6 VCC | **3.0V** | **3.3V** | **3.6V** | ✓ Safe range |

⚠️ **CRITICAL**: ESP32-C6 is NOT 5V tolerant! Keep all GPIO at 3.3V max.

---

## 🛠️ Εργαλεία Αναγκαία

- ✂️ Wire strippers (για καθάρισμα καλωδίων)
- 🔩 Soldering iron & solder (εάν χρειάζεται σύνδεση χωρίς jumpers)
- 📏 Multimeter (για έλεγχο τάσης & DC/DC ρύθμιση)
- 🔌 Jumper wires (22 AWG recommended)
- 🧤 Heat shrink tubing (για προστασία συνδέσεων)
- 🔧 Small screwdriver (για DC/DC potentiometer ρύθμιση)

---

## ⚠️ Σημαντικές Προειδοποιήσεις

1. **Μπαταρία 18650**: 
   - Μην υπερφορτίζετε (max 4.2V)
   - Μην εκφορτίζετε κάτω από 2.5V (πλήρης εκφόρτιση = ζημιά)
   - Θερμοκρασία: -20°C έως +60°C

2. **DC/DC Converter**:
   - Ρυθμίστε με ΑΚΡΊΒΕΙΑ στα 3.3V (όχι 3.4V ή 3.2V)
   - Προσθέστε 100µF capacitor για σταθερότητα

3. **ESP32-C6**:
   - Όλα τα GPIO είναι 3.3V ONLY
   - Μην συνδέετε 5V σε GPIO pins
   - Max combined current: 500mA (all pins)

4. **Καλώδια**:
   - Χρησιμοποιήστε τουλάχιστον 22 AWG (0.6mm²) για ρεύμα > 1A
   - Στερεώστε καλά τις συνδέσεις (χαλαρά καλώδια = διακοπή)

5. **Breadboard**:
   - Μην πιέζετε πολύ τα καλώδια στις τρύπες
   - Χρησιμοποιήστε κατάλληλα καλώδια (22 AWG)

---

## 📸 Φωτογραφικό Παράδειγμα Θέσης Εξαρτημάτων

```
┌─────────────────────────────────────────────────────┐
│  SOLAR PANEL (on top/side - direct sunlight)       │
│         ↓                                            │
│  CHARGER BOARD (weatherproof enclosure)            │
│         ↓                                            │
│  BATTERY CASE (inside enclosure)                   │
│         ↓                                            │
│  DC/DC CONVERTER (on breadboard or separate)       │
│         ↓                                            │
│  BREADBOARD (in box with ESP32)                    │
│         ↓                                            │
│  ESP32-C6 (center of breadboard)                   │
└─────────────────────────────────────────────────────┘
```

---

✅ **Επόμενο βήμα**: Δείτε `SCHEMATIC.txt` για το ηλεκτρονικό κύκλωμα
✅ **Προγραμματισμός**: Δείτε `firmware/main.cpp` για τον κώδικα ESP32
