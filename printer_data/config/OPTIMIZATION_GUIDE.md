# Voron 2.4 R2 Pro - Optimierungs-Leitfaden

## 🎯 Übersicht

Dein Voron wurde mit 8 Performance-Optimierungen ausgestattet. Alle Konfigurationen sind installiert, müssen aber teilweise kalibriert werden.

---

## 📋 Schritt-für-Schritt Setup

### 1️⃣ Input Shaper Kalibrierung (WICHTIG!)

**Zweck:** Reduziert Vibration & ermöglicht höhere Beschleunigung

**Vorgehensweise:**
```gcode
# 1. Resonanztest durchführen (~20 Minuten)
TEST_RESONANCES_ALL

# 2. Nach Abschluss: Werte speichern
SAVE_CONFIG

# 3. Drucker neustartet automatisch
```

**Ergebnis:** X/Y Input Shaper Werte werden automatisch gesetzt

**Optional:** Teste verschiedene Beschleunigungs-Profile:
- `ACCEL_SPEED` - 12000 mm/s² (schnellste)
- `ACCEL_NORMAL` - 10000 mm/s² (empfohlen)
- `ACCEL_QUALITY` - 5000 mm/s² (beste Qualität)

---

### 2️⃣ Pressure Advance Kalibrierung

**Zweck:** Verbessert Ecken & reduziert Stringing

**Vorgehensweise:**
```gcode
# 1. Starte PA-Test
PA_CALIBRATE_START BED=60 EXTRUDER=220

# 2. Drucke PA-Test-Muster
# Im Slicer: TUNING_TOWER COMMAND=SET_PRESSURE_ADVANCE PARAMETER=ADVANCE START=0 FACTOR=.005

# 3. Bestes Ergebnis finden & dauerhaft setzen
# In printer.cfg: pressure_advance: X.XXX
```

**Schnelltest:** Teste verschiedene PA-Werte live:
- `PA_PLA` - 0.035
- `PA_PETG` - 0.045
- `PA_ABS` - 0.030
- `PA_TPU` - 0.055

---

### 3️⃣ TMC Autotune (Optional)

**Zweck:** Optimiert Motor-Treiber für Performance/Lautheit

**Vorgehensweise:**
```gcode
# Automatisches Tuning aller Motoren (~5 Minuten)
TMC_AUTOTUNE_ALL

# Nach Abschluss: Speichern
SAVE_CONFIG
```

**Manuelle Modi:**
- `TMC_PERFORMANCE_MODE` - Lauter, mehr Drehmoment
- `TMC_SILENT_MODE` - Leiser, weniger Drehmoment

---

### 4️⃣ Bed Mesh 7x7

**Zweck:** Hochauflösendes Bed-Profil für perfekte First Layer

**Vorgehensweise:**
```gcode
# Vollständiges 7x7 Mesh (49 Punkte)
BED_MESH_FULL

# Speichern als default
BED_MESH_SAVE PROFILE=default

# Für jeden Druck laden (automatisch in PRINT_START)
```

**Weitere Mesh-Optionen:**
- `BED_MESH_ADAPTIVE` - Nur Druckbereich (schneller mit KAMP)
- `BED_MESH_FAST` - 5x5 für Tests
- `BED_MESH_ULTRA` - 9x9 für maximale Genauigkeit

---

### 5️⃣ Firmware Retraction

**Zweck:** Runtime-Anpassung ohne Slicer neu-slicen

**Setup im Slicer:**
- Aktiviere "Use Firmware Retraction" (G10/G11)
- Entferne Slicer Retraction-Werte

**Im Druck anpassen:**
```gcode
# Material-Profile
RETRACT_PLA
RETRACT_PETG
RETRACT_ABS
RETRACT_TPU

# Manuell anpassen
SET_RETRACTION RETRACT_LENGTH=0.6 RETRACT_SPEED=45

# Z-Hop
ZHOP_ON    # 0.2mm Z-Hop
ZHOP_OFF   # Z-Hop aus
```

---

### 6️⃣ Z-Offset per Build Plate

**Zweck:** Verschiedene Build Plates mit eigenem Z-Offset

**Initial Setup:**
```gcode
# 1. Build Plate auswählen
PLATE_SMOOTH_PEI

# 2. Z-Offset kalibrieren
CALIBRATE_PLATE_ZOFFSET

# 3. Mit Paper-Test anpassen (TESTZ Z=-0.010 etc.)

# 4. Z-Offset für dieses Plate speichern
SAVE_PLATE_ZOFFSET
```

**Im Alltag:**
```gcode
# Plate wechseln & Z-Offset wird automatisch geladen
PLATE_SMOOTH_PEI
PLATE_TEXTURED_PEI
PLATE_GLASS

# Aktuellen Z-Offset anzeigen
PLATE_INFO
```

**Live-Anpassung während Druck:**
- `Z_DOWN` - Näher zum Bed (-0.01mm)
- `Z_UP` - Weiter weg (+0.01mm)
- `Z_DOWN_FINE` - Fein (-0.005mm)
- `Z_UP_FINE` - Fein (+0.005mm)

---

### 7️⃣ Save Variables & Statistics

**Zweck:** Drucker merkt sich Einstellungen & trackt Statistiken

**Verfügbare Features:**
```gcode
# Print Statistics initialisieren
INIT_STATS

# Statistiken anzeigen
SHOW_STATS

# Maintenance Tracking
INIT_MAINTENANCE
MAINTENANCE_INFO
NOZZLE_CHANGED    # Wenn Nozzle gewechselt wurde
```

**Material-spezifische Einstellungen speichern:**
```gcode
# Einstellungen speichern
SAVE_MATERIAL_SETTINGS MATERIAL=PLA PA=0.035 EM=1.0

# Einstellungen laden
LOAD_MATERIAL_SETTINGS MATERIAL=PLA
```

---

### 8️⃣ OrcaSlicer Profile

**Installation:**
1. Öffne OrcaSlicer
2. Gehe zu Settings → Printer → Add Printer
3. Importiere `/tmp/OrcaSlicer_Voron_DragonHF_Profile.json`
4. Oder kopiere die Werte manuell

**Wichtige Einstellungen:**
- Max Speed: 710 mm/s
- Max Accel: 10000 mm/s²
- Retraction: 0.5mm @ 40mm/s
- Start GCode: `PRINT_START BED=[bed_temperature] HOTEND=[nozzle_temperature] MATERIAL=[filament_type]`

---

## 🚀 Workflow nach Installation

### Erster Start:
1. `TEST_RESONANCES_ALL` → Input Shaper kalibrieren
2. `BED_MESH_FULL` → 7x7 Bed Mesh erstellen
3. `PLATE_SMOOTH_PEI` → Build Plate auswählen
4. `CALIBRATE_PLATE_ZOFFSET` → Z-Offset kalibrieren
5. `PA_CALIBRATE_START` → Pressure Advance Test-Druck

### Vor jedem Druck:
- Build Plate auswählen (wenn gewechselt): `PLATE_SMOOTH_PEI`
- Acceleration-Profil wählen (optional): `ACCEL_NORMAL`
- Material-Profil laden (optional): `LOAD_MATERIAL_SETTINGS MATERIAL=PLA`

### Während des Drucks:
- Z-Offset anpassen: `Z_DOWN` / `Z_UP`
- Retraction anpassen: `RETRACT_FINE_TUNE ADJUST=0.1`
- Fan-Speed: über Mainsail/Fluidd Interface

---

## 📊 Neue Makros im Überblick

### Motion & Performance
- `ACCEL_SPEED / NORMAL / QUALITY / SILENT`
- `VIBRATION_TEST` - Mechanik-Check

### Calibration
- `TEST_RESONANCES_ALL` - Input Shaper
- `PA_CALIBRATE_START` - Pressure Advance
- `TMC_AUTOTUNE_ALL` - TMC Treiber

### Bed Management
- `BED_MESH_FULL / ADAPTIVE / FAST / ULTRA`
- `BED_MESH_SAVE / LOAD / CLEAR / INFO`

### Z-Offset
- `PLATE_SMOOTH_PEI / TEXTURED_PEI / GLASS`
- `Z_UP / Z_DOWN / Z_UP_FINE / Z_DOWN_FINE`
- `CALIBRATE_PLATE_ZOFFSET`
- `PLATE_INFO`

### Retraction
- `RETRACT_PLA / PETG / ABS / TPU`
- `ZHOP_ON / ZHOP_OFF`
- `RETRACT_INFO`

### Statistics & Maintenance
- `SHOW_STATS` - Print Statistiken
- `MAINTENANCE_INFO` - Wartungs-Info
- `NOZZLE_CHANGED` - Nozzle-Wechsel protokollieren

### Material Management
- `SAVE_MATERIAL_SETTINGS` - Material-Profil speichern
- `LOAD_MATERIAL_SETTINGS` - Material-Profil laden

---

## ⚠️ Wichtige Hinweise

1. **Input Shaper MUSS kalibriert werden** - Sonst kann 10000mm/s² zu viel sein
2. **Bed Mesh** ist jetzt 7x7 statt 5x3 - dauert etwas länger aber deutlich besser
3. **Firmware Retraction** erfordert Slicer-Änderung (G10/G11 aktivieren)
4. **Z-Offset** wird jetzt pro Build Plate gespeichert - einmal kalibrieren, nie mehr anpassen
5. **Pressure Advance** muss pro Material kalibriert werden

---

## 🔄 Bei Problemen: Rollback

Falls Probleme auftreten, alte Konfiguration wiederherstellen:

```bash
# SSH zum Drucker
ssh benlue@192.168.3.195

# Optimierungen aus printer.cfg entfernen
nano ~/printer_data/config/printer.cfg
# Lösche die letzten ~20 Zeilen (alles nach "PERFORMANCE OPTIMIZATIONS")

# Altes Bed Mesh wiederherstellen
cp ~/printer_data/config/hardware/bed/bed_mesh.cfg.backup ~/printer_data/config/hardware/bed/bed_mesh.cfg

# Klipper neustarten
sudo systemctl restart klipper
```

---

## 📈 Erwartete Verbesserungen

- ✅ **Geschwindigkeit:** 2-3x schneller bei gleicher Qualität
- ✅ **Beschleunigung:** 4000 → 10000 mm/s²
- ✅ **First Layer:** Deutlich besser durch 7x7 Mesh
- ✅ **Ecken/Kanten:** Schärfer durch Pressure Advance
- ✅ **Stringing:** Reduziert durch optimierte Retraction
- ✅ **Workflow:** Build Plate wechseln ohne Re-Kalibrierung

---

**Viel Erfolg mit den Optimierungen! 🚀**
