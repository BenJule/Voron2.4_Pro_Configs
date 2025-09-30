# Voron V2.4 R2 350 - Klipper Configuration

## 📁 Ordnerstruktur

```
printer.cfg                 # Haupt-Konfigurationsdatei
│
├── hardware/              # Hardware-Konfigurationen
│   ├── mcu/              # MCU & Pinouts
│   │   └── pinouts.cfg
│   ├── toolhead/         # Toolhead (EBB36 CAN)
│   │   └── ebb36.cfg
│   ├── steppers/         # Motoren & Treiber
│   │   ├── steppers.cfg
│   │   └── tmc2209.cfg
│   ├── bed/              # Druckbett
│   │   ├── bed_mesh.cfg
│   │   └── probe.cfg
│   ├── fans/             # Lüfter
│   │   └── fans.cfg
│   ├── sensors/          # Temperatursensoren
│   │   └── sensors.cfg
│   ├── leds/             # Beleuchtung
│   │   └── led.cfg
│   ├── heater.cfg        # Heizungen (Bed + Extruder)
│   └── gantry.cfg        # Quad Gantry Leveling
│
├── macros/               # Makros
│   ├── print/           # Druck-Makros
│   │   ├── Print_Start.cfg
│   │   ├── Print_End.cfg
│   │   ├── Cancel_Print.cfg
│   │   ├── Purge_Line.cfg
│   │   └── Purge_Bucket.cfg
│   ├── maintenance/     # Wartungs-Makros
│   │   ├── Clean_Nozzle.cfg
│   │   ├── Cleaning.cfg
│   │   ├── Filament_Change.cfg
│   │   └── Clean_Filament_Cold_Pull.cfg
│   ├── calibration/     # Kalibrierungs-Makros
│   │   ├── Bed_Mesh.cfg
│   │   ├── manual_bed_mesh_calibrate.cfg
│   │   └── Dynamic_Homing.cfg
│   └── utilities/       # Hilfsmakros
│       ├── Caselight.cfg
│       └── Update_Git.cfg
│
├── plugins/              # Plugins & Erweiterungen
│   ├── kamp/            # KAMP - Adaptive Meshing
│   ├── obico/           # Obico Remote Monitoring
│   ├── timelapse/       # Timelapse
│   └── misc/            # Sonstige (Mainsail, Fluidd, etc.)
│
├── calibration/          # Kalibrierdaten
│   ├── ShakeTune_results/
│   └── adxl.cfg
│
├── archive/              # Alte/nicht genutzte Configs
└── backups/              # Alte printer.cfg Backups

```

## 🔧 Installation

### Option 1: Schrittweise Migration (EMPFOHLEN)

1. **Teste die neue Struktur:**
   ```bash
   cd ~/printer_data/config
   cp _NEW_STRUCTURE/printer.cfg printer_new.cfg
   ```

2. **In Mainsail/Fluidd:**
   - Öffne `printer_new.cfg`
   - Klicke auf Save
