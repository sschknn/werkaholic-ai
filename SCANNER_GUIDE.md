# 📷 Werkaholic AI - Live Scanner & KI-Integrations-Anleitung

## 🏭 Technische Übersicht

**Werkaholic AI Scanner** ist eine hochoptimierte, **100% Client-seitige Web-Applikation** zur automatisierten Produkterkennung und Inserat-Generierung via Google Gemini 2.0 Flash Vision API.

### ⚡ Kernmerkmale

| Feature | Beschreibung | Status |
|---------|-------------|--------|
| **Live-Kamera-Streaming** | Echtzeitvideo vom Gerät | ✅ Production |
| **Auto-Scan** | Automatische Frames alle X Sekunden | ✅ Production |
| **KI-Analyse** | Google Gemini 2.0 Flash Vision | ✅ Live |
| **Duplikat-Erkennung** | Keywords + Titel-Matching | ✅ Production |
| **JSON-Export** | Strukturierte Produktdaten | ✅ Production |
| **Status-Logging** | Echtzeit Debug-Log | ✅ Production |
| **Bild-Upload** | Alternative zu Live-Kamera | ✅ Production |
| **Scan-Frame-Overlay** | Visuelle Scanning-Anzeige | ✅ UI |

---

## 🚀 Schnellstart

### 1. API-Key Beschaffen

```bash
# Google Gemini API Key:
# https://aistudio.google.com/app/apikey

# Kostenlos bis 15 Requests/Minute
# Keine Kreditkarte nötig
```

### 2. App laden & API Key eingeben

- **HTML-Datei**: `scanner-live.html` öffnen
- Browser konsole (F12) öffnen
- Folgenden Code eingeben:

```javascript
localStorage.setItem('werkaholic_apiKey', 'YOUR_API_KEY_HERE');
window.location.reload();
```

### 3. Kamera aktivieren

1. Kamera auswählen (falls mehrere vorhanden)
2. "📷 Kamera starten" klicken
3. Artikel vor Kamera positionieren
4. "🔍 Scannen" klicken ODER Auto-Scan aktivieren

---

## 🔇 Advanced Configuration

### Auto-Scan Konfiguration

```javascript
// In Browser Console:
const config = {
    scanInterval: 5,        // Sekunden zwischen Scans
    imageQuality: 0.8,      // JPEG Kompressionsfaktor
    maxHistorySize: 100,    // Max. Artikel in History
    autoSaveHistory: true   // Auto-Save zu localStorage
};

Object.assign(appState, config);
```

### KI-Prompt Anpassung

```javascript
// In scanner-live.html - Zeile ~350:
const systemPrompt = `Du bist ein hochspezialisierter E-Commerce-Experte...
// Ersetze mit deinem Custom Prompt
```

---

## 📄 Datenfluss & Architektur

### Scan-Pipeline

```
📷 Live Video Stream
        ↓
    Frame Capture
    (Canvas API)
        ↓
    Base64 Encoding
        ↓
    Gemini API Request
    (Vision + Text)
        ↓
    JSON Parsing
        ↓
    Duplicate Check
    (Keywords + Title)
        ↓
    localStorage Save
        ↓
    UI Render
    (Result View)
```

### API Response Format

```json
{
  "item_detected": true,
  "title": "iPhone 13 Pro Max 256GB Silber",
  "category": "Elektronik",
  "price_estimate": 650,
  "price_range": {
    "min": 580,
    "max": 750
  },
  "condition": "Good",
  "description": "Das iPhone 13 Pro Max ist ein Premium-Smartphone...",
  "features": [
    "OLED Display 6.7 Zoll",
    "A15 Bionic Chip",
    "Triple Kamera System"
  ],
  "potential_issues": [
    "Kleine Kratzer auf Rücken"
  ],
  "recommended_keywords": [
    "iPhone 13 Pro Max",
    "256GB Silber",
    "Apple"
  ],
  "confidence_score": 0.92,
  "market_demand": "high",
  "estimated_listing_time": 3
}
```

---

## 🔍 Fehlerbehandlung

### Gewöhnliche Fehler

| Fehler | Lösung |
|--------|--------|
| "Keine Kamera gewählt" | Kamera-Dropdown öffnen & auswählen |
| "API Key fehlt" | localStorage via Console eingeben |
| "JSON Parsing Error" | API-Antwort ist kein gültiges JSON |
| "Rate Limit" | Zu viele Requests - warte 60s |
| "No item detected" | Bildqualität verbessern oder Artikel neu fotografieren |

### Debug-Modus

```javascript
// Detailliertes Logging aktivieren:
setTimeout(() => {
    const logs = document.getElementById('statusLog');
    console.log('Alle Logs:', logs.innerText);
}, 2000);
```

---

## 📾 Export & Integration

### Daten Exportieren

#### Als JSON
```javascript
const items = JSON.parse(localStorage.getItem('werkaholic_history') || '[]');
console.save(items, 'items.json');
```

#### Als CSV
```javascript
const items = JSON.parse(localStorage.getItem('werkaholic_history') || '[]');
const csv = items.map(item => `"${item.title}",${item.price_estimate},${item.condition}`).join('\n');
```

#### Direct Copy für eBay
```
Formatvorlage:

[TITEL]

[DESCRIPTION]

Preis: €[PRICE]
Zustand: [CONDITION]
Kategorie: [CATEGORY]

Keywords: [KEYWORDS]
```

---

## 🛠️ Performance-Optimierung

### Kamera-Einstellungen

```javascript
const constraints = {
    video: {
        width: { ideal: 1280 },      // Full HD optimal
        height: { ideal: 720 },
        facingMode: 'environment'    // Rückkamera auf mobil
    }
};
```

### Frame-Kompression

```javascript
// In captureFrame():
return scanner.canvas.toDataURL('image/jpeg', 0.8); // 80% Qualität
// 0.6 = mehr Kompression, schneller
// 0.95 = bessere Qualität, größer
```

### Duplikat-Algorithmus

```javascript
function checkDuplicate(analysis) {
    // Vergleiche letzte 3 Erkennungen
    const recent = appState.lastDetections.slice(-3);
    
    // Exakte Titelgleichheit ODER
    // 2+ Übereinstimmungen bei Keywords
    return recent.some(prev => 
        titleMatch || keywordMatch >= 2
    );
}
```

---

## 🎯 Best Practices

### Optimal Scanning

1. **Beleuchtung**: Helles Umgebungslicht (kein Gegenlicht)
2. **Entfernung**: 20-50cm vom Objekt
3. **Winkel**: Senkrecht oder 45° zum Objekt
4. **Hintergrund**: Neutrale, monochrome Farbe
5. **Fokus**: Artikel zentriert im Bildrahmen

### KI-Prompt Tipps

- **Spezifisch**: "Für eBay Kleinanzeigen" statt allgemein
- **Struktur**: JSON-Format explizit fordern
- **Kontext**: "Verkaufsexperte" statt neutraler Analyzer
- **Detail**: Konkrete Felder aufzählen

### API-Key Management

```javascript
// SICHER: Nur im localStorage
localStorage.setItem('werkaholic_apiKey', key);

// UNSICHER: Im Code hartcodiert
const API_KEY = 'sk_...'  // NIE!

// BEST: Environment Variable (.env)
VITE_GOOGLE_API_KEY=sk_...
```

---

## 📊 Monitoring & Analytics

### Status-Log Parser

```javascript
const logs = document.getElementById('statusLog').innerText;
const successCount = (logs.match(/\u2705/g) || []).length;
const errorCount = (logs.match(/\u274c/g) || []).length;
console.log(`Erfolg: ${successCount}, Fehler: ${errorCount}`);
```

### Session-Statistiken

```javascript
const items = JSON.parse(localStorage.getItem('werkaholic_history') || '[]');
const avgPrice = items.reduce((s, i) => s + i.price_estimate, 0) / items.length;
const totalTime = items.reduce((s, i) => s + (i.estimated_listing_time || 0), 0);

console.log(`Artikel: ${items.length}, Ø Preis: €${avgPrice.toFixed(2)}, Zeit: ${totalTime}d`);
```

---

## 🚀 Production Deployment

### Cloudflare Pages

```bash
# Repository in Cloudflare Pages connecten
# Build Command: (leer lassen)
# Publish Directory: / (root)

# App verfügbar unter: https://werkaholic-ai.pages.dev
```

### Eigener Server

```bash
# Nginx
server {
    listen 443 ssl http2;
    server_name werkaholic.example.com;
    
    root /var/www/werkaholic;
    index scanner-live.html;
    
    ssl_certificate /etc/letsencrypt/live/...;
    ssl_certificate_key /etc/letsencrypt/live/...;
}
```

### PWA (Progressive Web App)

```json
// manifest.json
{
  "name": "Werkaholic AI Scanner",
  "short_name": "Scanner",
  "start_url": "/scanner-live.html",
  "display": "standalone",
  "icons": [
    {
      "src": "icon-192.png",
      "sizes": "192x192",
      "type": "image/png"
    }
  ]
}
```

---

## 🏧 Troubleshooting

### Kamera funktioniert nicht

```javascript
// Debug:
navigator.mediaDevices.enumerateDevices().then(devices => {
    console.log('Verfügbare Geräte:', devices);
});
```

### API gibt keine Antwort

```javascript
// Check API Status:
fetch('https://generativelanguage.googleapis.com/v1beta/models/gemini-2.0-flash:generateContent?key=' + apiKey, {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({ contents: { parts: [{ text: 'test' }] } })
}).then(r => console.log('Status:', r.status));
```

### localStorage voll

```javascript
// Clear alte Einträge:
const items = JSON.parse(localStorage.getItem('werkaholic_history') || '[]');
const recent = items.slice(-50); // Nur letzte 50
localStorage.setItem('werkaholic_history', JSON.stringify(recent));
```

---

## 🃖 Weiterführendes

- **React Version**: Siehe `/src` (TypeScript, Hooks)
- **Backend Integration**: Node.js + Express für multi-user
- **Database**: MongoDB für persistente Speicherung
- **Mobile App**: React Native Cross-Plattform

---

**Version**: 1.0.0  
**Letzte Aktualisierung**: Dezember 2025  
**Lizenz**: MIT

*Bauen Sie schneller, verkaufen Sie besser mit Werkaholic AI* 🏭