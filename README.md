# 🏭 Werkaholic AI – Intelligenter Verkaufs-Assistent

## 📋 Überblick

**Werkaholic AI** ist eine hochoptimierte Web-Applikation für Reseller und Händler (eBay Kleinanzeigen, etc.). Sie nutzt **Google Gemini 2.0 Flash** zur automatischen Bildanalyse, Preisschätzung und professionellen Inserat-Generierung.

### 🏭 Kernfunktionen

- **📷 Live-Scanner**: Echtzeitkamera-Zugriff mit Auto-Scan-Logik
- **🤖 KI-Analyse**: Google Gemini Vision für präzise Objekterkennung
- **💰 Preisbewertung**: Automatische Marktwert-Schätzung mit Range
- **📝 Inserat-Generierung**: SEO-optimierte Verkaufstexte
- **🎤 Voice Chat**: Sprachgesteuerter Sales-Coach
- **🖼️ Bild-Editor**: Canvas-basierte Helligkeit/Kontrast-Anpassung
- **📊 Analytics Dashboard**: Echtzeit-Statistiken & Visualisierungen
- **💾 Multi-Export**: PDF, ZIP, Text für eBay-Kleinanzeigen
- **🔒 100% Browser-basiert**: Keine Serverdaten, localStorage-Persistierung

---

## ⚡ Technologie-Stack

### Frontend
- **React 19** (Functional Components, Hooks)
- **TypeScript** (Strikte Typisierung)
- **Tailwind CSS** (Dark Mode via CDN)
- **Lucide React** (Icons)

### KI & APIs
- **Google Gemini 2.0 Flash** (Vision & Text)
- **Web Speech API** (STT/TTS)
- **Native MediaDevices** (Kamerazugriff)

### Persistierung
- **localStorage** (Browser-native, keine Server)
- **Recharts** (Analytics-Visualisierungen)
- **jsPDF + JSZip** (Export-Tools)

---

## 🚀 Installation & Setup

### 1. Repository klonen
```bash
git clone https://github.com/sschknn/werkaholic-ai.git
cd werkaholic-ai
```

### 2. Abhängigkeiten installieren
```bash
npm install
```

### 3. Google Gemini API Key besorgen
1. Gehe zu [Google AI Studio](https://aistudio.google.com/app/apikey)
2. Erstelle einen neuen API Key
3. Kopiere den Key

### 4. App starten
```bash
npm run dev
```
Die App läuft dann auf `http://localhost:5173`

### 5. API Key eingeben
- Gehe zu **⚙️ Einstellungen**
- Paste deinen Google Gemini API Key
- Speichern & fertig! 🎉

---

## 📖 Verwendung

### Scanner-Workflow
1. **📷 Scanner öffnen** → Kamera starten
2. **Artikel fotografieren** → Automatischer oder manueller Scan
3. **KI analysiert** → ~2-3 Sekunden Verarbeitung
4. **Ergebnis anzeigen** → Titel, Preis, Beschreibung, Keywords
5. **Bearbeiten & exportieren** → Für eBay-Kleinanzeigen kopieren

---

## 🔒 Sicherheit

- ✅ **Keine Server-Verbindung** außer zu Google Gemini API
- ✅ **API Key lokal gespeichert** (localStorage des Nutzers)
- ✅ **Bilder nicht hochgeladen** (außer zur KI-Analyse)
- ✅ **Keine Tracking/Analytics**
- ✅ **HTTPS-fähig** (Production-Ready)

---

**Gebaut mit ❤️ für Reseller & eBay-Verkäufer**

🏭 **Werkaholic AI** – *Dein intelligenter Verkaufs-Partner*