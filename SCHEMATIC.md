# 🔌 SCHEMATIC - Ηλεκτρονικό Κύκλωμα

## Σχέδιο Κυκλώματος (ASCII Art - Scale 1:1 Concept)

```
╔════════════════════════════════════════════════════════════════════════════╗
║                        SOLAR CHARGING CIRCUIT                             ║
╚════════════════════════════════════════════════════════════════════════════╝

                          [SOLAR PANEL]
                        Optum HR0472 6V 3.5W
                             │     │
                             │     └──────────────────┐
                             │                        │
                       ┌─────┴──────────┐             │
                       │                │             │
                       ▼                ▼             ▼
                    ┌────────────────────────┐     │D1│
                    │  OPTUM CHARGER BOARD   │     └──┘
                    │  (MPPT + Protection)   │    Diode
                    │                        │   (Optional)
                    │ IN+      IN-          │
                    │  │        │           │
                    │  │        │           │
                    │ OUT+     OUT-         │
                    └────────────────────────┘
                       │          │
                       │          │ GND
                       ▼          ▼
                    ┌──────────────────────┐
                    │  BATTERY PROTECTION  │
                    │  (Optional: TP4056)  │
                    │                      │
                    │ IN+      IN-        │
                    │  │        │         │
                    │  │        │         │
                    │ OUT+     OUT-      │
                    └───��──────────────────┘
                       │          │
                       │          │ GND Reference
                       ▼          ▼
            ╔═══════════════════════════════╗
            ║   BATTERY CASE (18650 Holder) ║
            ║                               ║
            ║   (+) ────────┬────────────→  Red Wire
            ║               │               ║
            ║     Panasonic │ 3.7V @ 2600mAh
            ║     18650      │               ║
            ║               │               ║
            ║   (-) ────────┼────────────→  Black Wire
            ║               ▼               ║
            ║           [+ Side]            ║
            ║         [- Side]              ║
            ╚═══════════════════════════════╝
                       │          │
                ┌──────┘          └─────────┐
                ▼                           ▼
        ┌───────────────────��───────────────────────┐
        │     DC/DC CONVERTER (HS2670)              │
        │  ┌─────────────────────────────────────┐  │
        │  │    INPUT       │   POTENTIOMETER    │  │
        │  │  ─────────     │   (Adjustment)     │  │
        │  │  + (Red)      │   /\/\/\           │  │
        │  │  - (Black)    │    │                │  │
        │  │               │    ▼ (rotate)       │  │
        │  │  INPUT MODE:  │                     │  │
        │  │  3.7V Input   │   OUTPUT MODES:     │  │
        │  │  (Battery)    │                     │  │
        │  │               │   • 3.3V  ◄─────── │  │
        │  │  Max 2A       │   • 5V              │  │
        │  │  ~92% Eff.    │   • 12V             │  │
        │  │               │   • 24V             │  │
        │  │               │                     │  │
        │  │  OUTPUT SIDE  │                     │  │
        │  │  ─────────    │                     │  │
        │  │  + (Red)   ─→ │ 3.3V regulated     │  │
        │  │  - (Black) ─→ │ GND                │  │
        │  └─────────────────────────────────────┘  │
        └───────────────────────────────────────────┘
                │              │
                │ 3.3V (+)    │ GND (-)
                │              │
        ┌───────┴──────────────┴───────┐
        │                              │
        │  ┌─────────┐    ┌─────────┐  │
        │  │ 100µF   │    │ 10µF    │  │
        │  │ Cap (+) │    │ Cap (+) │  │
        │  │    │    │    │    │    │  │
        │  │    ▼    │    │    ▼    │  │
        │  │ ┌────┐  │    │ ┌────┐  │  │
        │  │ │ ─ ─│  │    │ │ ─ ─│  │  │
        │  │ │ + ─│  │    │ │ + ─│  │  │
        │  │ └────┘  │    │ └────┘  │  │
        │  │    │    │    │    │    │  │
        │  │    ▼    │    │    ▼    │  │
        │  │   GND   │    │   GND   │  │
        │  └─────────┘    └─────────┘  │
        │         (Smoothing Caps)      │
        │                              │
        └──────────┬───────────────────┘
                   │
           ┌───────┴────────────────┐
           │   3.3V POWER RAIL      │
           │   (Breadboard)         │
           ├───────────────────────┤
           │                       │
           │ ┌─────────────────┐   │
           │ │  ESP32-C6 XIAO  │   │
           │ │                 │   │
           │ │ [VCC] ◄─────────┼─→ │ 3.3V
           │ │ [GND] ◄─────────┼─→ │ GND
           │ │                 │   │
           │ │ GPIO Pins:      │   │
           │ │ • D0 (GPIO0)    │   │
           │ │ • D1 (GPIO1)    │   │
           │ │ • D2 (GPIO2)    │   │
           │ │ • D3 (GPIO3)    │   │
           │ │ • D4 (GPIO4)    │   │
           │ �� • D5 (GPIO5) ◄──┼──→ ADC Input (Battery voltage monitoring)
           │ │ • D6 (GPIO6)    │   │
           │ │ • D7 (GPIO7)    │   │
           │ │ • D8 (GPIO8)    │   │
           │ │ • D9 (GPIO9)    │   │
           │ │ • D10(GPIO10)   │   │
           │ │                 │   │
           │ │ [TX] [RX]       │   │ Serial Port (USB Debug)
           │ └─────────────────┘   │
           │                       │
           └───────────────────────┘
                    │
           GND Reference (Common Ground)

```

---

## Λεπτομερές Διάγραμμα Κυκλώματος

### **Τομέας 1: Φόρτιση (Charging Section)**

```
SOLAR PANEL (6V)
    │
    ├─(+)─────┐
    │         │
    │      ┌──┴──┐
    │      │ D1  │  ← Optional Schottky Diode
    │      │ >2A │    (Prevents reverse flow)
    │      └──┬──┘
    │         │
    ├─(-)────┐┼──────────┐
    │        ││          │
    │        ││ ┌────────┴───────┐
    └────────┼─┤+              │
             │ │ CHARGER BOARD │
             └─┤- (MPPT)       │
               │                │
               ├─ [+ OUT] ──────→ Battery (+)
               └─ [- OUT] ──────→ Battery (-)
```

### **Τομέας 2: Αποθήκευση Ενέργειας (Storage)**

```
                ┌──────────────┐
                │   BATTERY    │
                │  (3.7V Nom)  │
                │ 2600-3000mAh │
                │              │
                ├─(+)─────────→ To DC/DC (+)
                │              
                ├─(-)─────────→ To DC/DC (-) & GND
                │
                └──────────────┘
```

### **Τομέας 3: Ρύθμιση τάσης (Voltage Regulation)**

```
BATTERY INPUT (3.7V)
    │
    ├─ (+) ─────┬──────┐
    │           │      │
    │        ┌──┘      │
    │        │         │
    │      ╔═╩═════════╩═╗
    │      ║  DC/DC (HS2670)
    │      ║  INPUT: 3.7V ║
    │      ║  OUTPUT: 3.3V║
    │      ║  Max: 2A     ║
    │      ║              ║
    │      ║ POT: ────────┤  Adjust for 3.3V
    │      ║              ║
    │      ║ OUT+ ────────→ 3.3V Rail
    │      ║ OUT- ────────→ GND Rail
    │      ╚══════════════╝
    │
    ├─ (-) ─────┬──────┐
    │           │      │
    └───────────┘      │
                  GND Reference
```

### **Τομέας 4: Σταθεροποίηση (Stabilization)**

```
DC/DC OUTPUT (3.3V)
    │
    ├─ 3.3V (+) ──┬──────┬─────────────┐
    │             │      │             │
    │         ┌───┴──┐ ┌─┴────┐       │
    │         │100µF │ │10µF  │       │
    │         │  Cap │ │ Cap  │       │
    │         │      │ │      │       │
    │         └──┬───┘ └──┬───┘       │
    │             │        │          │
    │             ▼        ▼          │
    │            GND      GND         │
    │                                  │
    ├─ GND (-) ────────────────────────┤
    │                                  │
    └──────────────┬───────────────────┘
                   │
          BREADBOARD POWER RAILS
          (VCC = 3.3V, GND = 0V)
```

### **Τομέας 5: ESP32-C6 Power Distribution**

```
BREADBOARD POWER RAILS (3.3V / GND)
    │
    ├─ 3.3V ─────┬──────────────┐
    │            │              │
    │        ┌───┴──┐       ┌───┴───┐
    │        │ 10µF │       │ESP32  │
    │        │ Cap  │       │  VCC  │
    │        │      │       │ Pin12 │
    │        └──┬───┘       └───┬───┘
    │           │              │
    │           ▼              │
    │          GND ◄───────────┘
    │                      (Bypass Cap for noise filtering)
    │
    ├─ GND ──────┬──────────────┐
    │            │              │
    │        ┌───┴──┐       ┌───┴───┐
    │        │ GND  │       │ESP32  │
    │        │ Ref  │       │  GND  │
    │        │(Star)│       │Multiple
    │        └──────┘       └───────┘
    │
    └─ All GPIO pins ──→ 3.3V ONLY!
       (NOT 5V tolerant)
```

---

## Pin Mapping: ESP32-C6 XIAO

```
┌─────────────────────────────────────────────────┐
│         SEEED XIAO ESP32-C6 PINOUT              │
│                                                 │
│  TOP ROW (Left to Right):                       │
│  ┌──────────────────────────────────────┐       │
│  │ D0    GND    D1    3V3                │       │
│  │GPIO0  REF    GPIO1 VCC                │       │
│  └──────────────────────────────────────┘       │
│                                                 │
│  MIDDLE ROW:                                    │
│  ┌──────────────────────────────────────┐       │
│  │ D2    D3    D4    D5                  │       │
│  │GPIO2  GPIO3 GPIO4 GPIO5(ADC_CH4)     │       │
│  └──────────────────────────────────────┘       │
│                                                 │
│  BOTTOM ROW (Left to Right):                    │
│  ┌──────────────────────────────────────┐       │
│  │ D6    D7    D8    D9                  │       │
│  │GPIO6  GPIO7 GPIO8 GPIO9              │       │
│  └──────────────────────────────────────┘       │
│                                                 │
│  BOTTOM RIGHT CORNER:                          │
│  ┌──────────────────────────────────────┐       │
│  │ D10        GND        D11      5V     │       │
│  │GPIO10      REF        GPIO11   USB    │       │
│  └──────────────────────────────────────┘       │
└─────────────────────────────────────────────────┘
```

### **Σύνδεσεις ESP32-C6 στο κύκλωμα**

| Pin | GPIO | Function | Σύνδεση | Σημειώσεις |
|-----|------|----------|---------|-----------|
| 12 | VCC | Power Supply | Breadboard 3.3V Rail | Main power input |
| 11 | GND | Ground | Breadboard GND Rail | Common ground |
| 1 | D0 / GPIO0 | General I/O | Breadboard Row A | (Optional) |
| 5 | D5 / GPIO5 | ADC (CH4) | Battery Voltage Monitor | Measures battery level |
| 8 | D8 / GPIO8 | General I/O | Breadboard Row F | (Optional) Status LED |
| USB | - | Serial Debug | USB Cable | For programming & debugging |

---

## ADC Input Configuration (Battery Monitoring)

```
BATTERY VOLTAGE MONITORING CIRCUIT
──────────────────────────────────

3.7V Battery (+)
    │
    ├─────┬──────────┐
    │     R1         │
    │    10kΩ        │
    │     │          │
    │     ├─────────→ ESP32 GPIO5 (ADC_CH4)
    │     │          
    │     R2         
    │    10kΩ        
    │     │          
    │     ├─────────→ GND Reference
    │
    └─ Divider Ratio: Vout = Vin × (R2 / (R1 + R2))
       Vout = 3.7V × (10k / 20k) = 1.85V ✓ Safe for ADC

ADC Reading: (Vout / 3.3V) × 4095 = Battery Level %
```

---

## Current Flow Analysis

```
Component Power Consumption:
─────────────────────────────

1. ESP32-C6:
   • Active Mode: ~80-100 mA
   • WiFi TX: ~200-300 mA
   • Deep Sleep: ~10 µA ◄─ Optimal for battery

2. DC/DC Converter:
   • Quiescent: ~2-5 mA
   • At Load: ~2 mA overhead
   • Efficiency: ~92%

3. Charger Board:
   • Charging: ~500 mA max (depends on solar panel)
   • Idle: ~5-10 mA

4. Battery:
   • Capacity: 2600-3000 mAh @ 3.7V
   • Energy: ~10-12 Wh
   • Runtime (if sleep mode): ~30-50 days
   • Runtime (if active): ~5-10 hours


Power Budget Example (Active WiFi every 1 hour for 10 seconds):
─────────────────────────────────────────────────────────────
1. Deep Sleep: 10 µA × 3600s = 36 mC per hour
2. Wake + WiFi: 250 mA × 10s = 2500 mC per hour
3. Total: ~2536 mC per hour = 2.5 mAh per hour
4. Battery: 2600 mAh ÷ 2.5 mAh/hr = ~1040 hours = ~43 days

With solar: Continuous recharge ✓ Indefinite operation!
```

---

## Protection Circuit Details

```
OVERVOLTAGE PROTECTION (Optional)
──────────────────────────────────
Battery Max: 4.2V
DC/DC Safe: 3.0V - 3.6V

If battery > 4.2V:
├─ Charger Board Protection: Cuts charging ✓
├─ LDO at DC/DC: Limits to 3.3V ✓
└─ Recommended: Add TVS Diode (3.6V) for safety

OVERCURRENT PROTECTION
──────────────────────
DC/DC Max: 2A continuous
ESP32 Total: 500 mA max

Solution: Built-in current limiting in DC/DC ✓

REVERSE POLARITY PROTECTION (Optional)
──────────────────────────────
Battery Holder: Mechanical only
├─ Add Schottky Diode (IN4148): ~0.3V drop
├─ Or Add Fuse: 2A @ 3.7V
└─ Recommended: Both for redundancy
```

---

## ✅ Verification Checklist

Before powering up:
- [ ] Voltage at Battery Case: 3.0V - 4.2V
- [ ] Voltage at DC/DC Input: Same as battery
- [ ] Voltage at DC/DC Output: 3.25V - 3.35V (measured with Multimeter)
- [ ] Voltage at Breadboard Rail: 3.3V ± 0.1V
- [ ] Voltage at ESP32 VCC Pin: 3.3V
- [ ] No short circuits (use Multimeter continuity test)
- [ ] All capacitors in correct polarity
- [ ] All connections tight and secure
- [ ] Solar panel produces voltage (measure in sunlight)

🚀 **Ready to program!** → See `firmware/main.cpp`
