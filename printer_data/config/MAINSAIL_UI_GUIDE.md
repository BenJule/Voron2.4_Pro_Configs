# Mainsail UI Optimierungs-Anleitung

## 🎨 Installierte Addons

### ✅ Bereits aktiv:
1. **Spoolman** - Filament-Verwaltung (30 Spulen registriert)
2. **Timelapse** - Automatische Timelapse-Videos
3. **Obico** - KI-basierte Fehler-Erkennung & Remote Monitoring
4. **Crowsnest** - Webcam-Integration
5. **KlipperScreen** - Touch-Display Interface
6. **KAMP** - Adaptive Meshing & Purging
7. **ShakeTune** - Input Shaper Analyse
8. **Cartographer** - Probe Support
9. **LED Effect** - Stealthburner LEDs
10. **Klipper Auto Speed** - Automatische Speed-Tests
11. **Klipper Backup** - GitHub Auto-Backup

### 🆕 Neu verfügbar (optional):
- **Mobileraker Companion** - Push-Notifications aufs Handy
- **Pretty GCode** - 3D GCode Vorschau im Browser
- **Mooncord** - Discord Benachrichtigungen

---

## 📊 UI Optimierung - Manuelle Schritte

Da Mainsail UI-Einstellungen nur über die Web-Oberfläche geändert werden können, folge diesen Schritten:

### 1. Dashboard Layout optimieren

1. Öffne Mainsail: http://192.168.3.195
2. Klicke oben rechts auf **Settings** (Zahnrad)
3. Gehe zu **Interface** → **Dashboard**
4. Aktiviere **Widescreen Layout** (3 Spalten)

**Empfohlenes Layout:**

**Spalte 1 (Links):**
- Webcam (groß)
- Toolhead Control
- Z-Offset Control

**Spalte 2 (Mitte):**
- Temperature
- Spoolman
- Machine Settings
- Miscellaneous

**Spalte 3 (Rechts):**
- Mini Console
- Macro Groups (siehe unten)

### 2. Macro Groups erstellen

Gehe zu **Settings** → **Macros** → **+ Add Macro Group**

**Gruppe 1: "⚡ Schnellzugriff"**
- G32
- QUAD_GANTRY_LEVEL
- BED_MESH_FULL
- BED_MESH_ADAPTIVE
- ACCEL_NORMAL

**Gruppe 2: "🌡️ Lüfter & Kühlung"**
- Bed Fans ON
- Bed Fans OFF
- Exhaust Auto
- Exhaust OFF

**Gruppe 3: "💡 Beleuchtung"**
- LED_ON
- LED_OFF
- Status Ready
- Status Printing
- Status Heating

**Gruppe 4: "📏 Kalibrierung"**
- CALIBRATE_PLATE_ZOFFSET
- Z_UP
- Z_DOWN
- FIRST_LAYER_CAL
- TEST_RESONANCES_ALL

**Gruppe 5: "🔧 Wartung"**
- BACKUP_CONFIG
- CLEANUP_LOGS
- SHOW_STATS
- MAINTENANCE_INFO
- SYSTEM_INFO

### 3. Theme anpassen

**Settings** → **Interface** → **Theme**

**Empfohlene Einstellungen:**
- **Theme:** Dark
- **Primary Color:** #2196F3 (Blau - Voron-Style)
- **Accent Color:** #FF5722 (Orange für Aktionen)
- **Background:** #121212
- **Surface:** #1E1E1E

### 4. Console Filter

**Settings** → **Console** → **Filters**

**Empfohlene Filter aktivieren:**
- ✅ Hide temperature messages (B:, T:)
- ✅ Hide position messages (X:, Y:, Z:)
- ✅ Hide wait messages

**Custom Filter hinzufügen:**
```
Name: Hide Movement
Regex: ^(G0|G1) [XYZ]
```

### 5. Webcam konfigurieren

**Settings** → **Webcam**

- **URL:** http://192.168.3.195/webcam/?action=stream
- **Service:** mjpegstreamer-adaptive
- **Flip Horizontal:** Nach Bedarf
- **Flip Vertical:** Nach Bedarf
- **Rotate:** 0° (oder 90°/180°/270° nach Bedarf)

### 6. Temperatur-Presets

**Settings** → **Presets** → **Temperature Presets**

Bereits konfiguriert über Klipper:
- PLA: 210°C / 60°C
- PLA+: 220°C / 65°C
- PETG: 240°C / 80°C
- ABS: 245°C / 105°C
- ASA: 250°C / 105°C
- TPU: 230°C / 50°C

### 7. Spoolman Widget

**Settings** → **Interface** → **Dashboard**

- Spoolman Panel aktivieren
- Position: Spalte 2 (Mitte), nach Temperature

**Verwendung:**
- Vor Druck: Spule auswählen
- Nach Druck: Verbrauch wird automatisch getrackt
- Warnung bei wenig Filament

---

## 🚀 Zusätzliche Features aktivieren

### Pretty GCode Preview (optional)

1. **Settings** → **G-Code Viewer** → **Enable 3D Preview**
2. Aktiviert WebGL-basierte 3D-Vorschau
3. Zeigt Layer-by-Layer Simulation

### Obico (AI Failure Detection)

Bereits konfiguriert! Zu finden:
- **Settings** → **Obico**
- Link Drucker mit Obico Cloud für:
  - KI-basierte Fehler-Erkennung
  - SMS/Email Benachrichtigungen
  - Remote-Zugriff von überall

### Mobileraker App

1. Installiere "Mobileraker" aus App Store / Play Store
2. Füge Drucker hinzu: 192.168.3.195
3. Erhalte Push-Notifications:
   - Druck gestartet/beendet
   - Fehler
   - Custom Notifications (M117)

---

## 📱 Mobile-Optimierung

**Settings** → **Interface** → **Mobile Layout**

**Empfohlene Panels für Mobile:**
1. Temperature (collapse)
2. Toolhead Control (collapse)
3. Macros (expanded)
4. Webcam (expanded)

---

## 🔔 Notifications Setup

**Settings** → **Notifications**

**Empfohlene Aktivierungen:**
- ✅ Print started
- ✅ Print paused
- ✅ Print completed
- ✅ Print error
- ✅ Filament runout
- ⬜ Temperature warnings (optional)

---

## 📊 Status anzeigen

### Zusätzliche Panels aktivieren:

**Settings** → **Interface** → **Dashboard** → **Available Panels**

**Empfehlung aktivieren:**
- ✅ Temperature
- ✅ Toolhead & Extruder
- ✅ Machine Settings (Limits)
- ✅ Spoolman
- ✅ Miscellaneous (Moonraker Stats)
- ✅ Webcam
- ✅ Mini Console
- ⬜ Full Console (optional)
- ✅ History (Recent Jobs)

---

## 🎯 Keyboard Shortcuts

**Wichtige Shortcuts:**
- `ESC` - Fullscreen beenden
- `Space` - Pause/Resume
- `Home` - Go to Dashboard
- `F11` - Browser Fullscreen

---

## 💾 Backup & Restore

### UI-Einstellungen exportieren:

1. **Settings** → **Interface** → **Export Settings**
2. Speichert alle UI-Einstellungen als JSON
3. Restore via **Import Settings**

### Klipper Config Backup:

Bereits automatisch via GitHub:
```bash
# Manuelles Backup
UPDATE_GIT MESSAGE="Manual backup"

# Automatisches Backup läuft täglich
```

---

## 🔍 Tipps & Tricks

### 1. Schnelle Temperatur-Änderung
- Klicke direkt auf Temperatur-Anzeige
- Eingabefeld erscheint
- Enter drücken zum Übernehmen

### 2. Emergency Stop
- Roter "Emergency Stop" Button immer sichtbar
- Stoppt alle Bewegungen sofort

### 3. Z-Offset während Druck anpassen
- Makros `Z_UP` / `Z_DOWN` in Macro Group
- Oder: **Machine** → **Babystepping**

### 4. Filament-Wechsel während Druck
- **Pause Print**
- **Actions** → **Change Filament**
- Folge Anweisungen
- **Resume Print**

### 5. Webcam-Snapshot für Timelapse
- Automatisch wenn Timelapse aktiv
- Manuell: **Webcam** → 📷 Icon

---

## 🎨 Weitere Theme-Optionen

### Voron Theme (Community)
```
Primary: #E31E24 (Voron Rot)
Secondary: #1A1A1A
Background: #0D0D0D
```

### Minimal Theme
```
Primary: #FFFFFF
Secondary: #424242
Background: #000000
```

### Cyberpunk Theme
```
Primary: #00F0FF (Cyan)
Secondary: #FF00F0 (Magenta)
Background: #0A0A0A
```

---

## ✅ Checklist

Nach Optimierung solltest du haben:

- [x] Bed Mesh 7x7 aktiv
- [x] Spoolman funktioniert (30 Spulen)
- [x] Timelapse aktiviert
- [x] Obico konfiguriert
- [ ] Macro Groups erstellt
- [ ] Dashboard Layout optimiert
- [ ] Theme angepasst
- [ ] Console Filter aktiviert
- [ ] Webcam eingerichtet
- [ ] Notifications aktiviert

---

**Viel Erfolg mit deinem optimierten Mainsail UI! 🚀**
