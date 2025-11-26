# 📘 KAIRA Technologies – Real-Time Dashboard & Weather Widget

A modern, responsive, multi-module dashboard for industrial monitoring, WhatsApp messaging, and real-time weather updates.  
Built using **pure HTML, CSS, JavaScript**, and deployed via **Vercel**.

---

# 🚀 Features

## 🔹 1. Interactive Sidebar Navigation
- Water → Dashboards (Grafana)
- Water → Reports (Looker Studio)
- Tyre → Mixer → TBM (multi-level dropdown)
- WhatsApp Messaging module

## 🔹 2. Premium Weather Widget (Iframe)
- Live weather from **WeatherAPI.com**
- Includes:
  - Mini widget (floating bottom-right)
  - Expandable full panel
  - 5-day forecast
  - Astronomy (sunrise/sunset)
  - Marine data
  - Air Quality
  - Alerts
- Auto-detect user location (GPS/IP)
- Refreshes every 60 seconds
- Uses `postMessage` to expand/collapse iframe

## 🔹 3. WhatsApp Messaging Module
- Clean, glass UI
- Sends WhatsApp messages via backend API  
- Endpoint: `POST /api/send-message`
- Built using Node.js (server.js)

## 🔹 4. Modern UI/UX
- Glassmorphism cards  
- Gradient backgrounds  
- Poppins font  
- Smooth animations  
- Responsive layout  

---

# 📂 Project Structure
```
/webpage
│── index.html # Main dashboard UI
│── weather-widget.html # Weather widget (iframe internal page)
│── server.js # WhatsApp API backend handler
│── package.json # Node + Vercel dependencies
│── vercel.json # Routing & build configuration
│── README.md # Documentation
└── LICENSE (optional)

```
---

# ⚙️ Local Setup

## 1️⃣ Install Node.js  
Download from: ```https://nodejs.org/```

## 2️⃣ Install dependencies
```sh
npm install
```
3️⃣ Start local server
```
node server.js
```
Your project opens at:
```
👉 http://localhost:3000
```
🌤️ Weather Widget Setup
✔ 1. Add iframe inside index.html
```
<iframe src="/weather-widget" id="weatherFrame" class="weather-iframe"></iframe>
```
✔ 2. Widget sends expand/collapse events

Inside weather-widget.html:
```
window.parent.postMessage({ type: "weatherExpand" }, "*");
window.parent.postMessage({ type: "weatherCollapse" }, "*");
```
✔ 3. Parent listens for events

Inside index.html:
```
window.addEventListener("message", (event) => {
  const frame = document.getElementById("weatherFrame");

  if (event.data.type === "weatherExpand") frame.classList.add("expanded");
  if (event.data.type === "weatherCollapse") frame.classList.remove("expanded");
});
```
✔ 4. Set your Weather API key

Inside weather-widget.html:
```
const apiKey = "YOUR_API_KEY_HERE";
```
Get free API key:
```
👉 https://www.weatherapi.com/
```
💬 WhatsApp API – Integration
Backend Route (server.js)
```
Handles: POST /api/send-message
```
```
Frontend Call
fetch("/api/send-message", {
  method: "POST",
  headers: { "Content-Type": "application/json" },
  body: JSON.stringify({ mobile })
});
```

Displays success or error in UI.

▲ Deploying to Vercel

1️⃣ Install Vercel CLI
```
npm i -g vercel
```
2️⃣ Login
```
vercel login
```
3️⃣ Deploy
```
vercel
```
📁 Required vercel.json
```
{
  "version": 2,
  "builds": [
    { "src": "server.js", "use": "@vercel/node" },
    { "src": "index.html", "use": "@vercel/static" },
    { "src": "weather-widget.html", "use": "@vercel/static" }
  ],
  "routes": [
    { "src": "/api/(.*)", "dest": "/server.js" },
    { "src": "/weather-widget", "dest": "/weather-widget.html" },
    { "src": "/(.*)", "dest": "/index.html" }
  ]
}
```
This ensures:
```
/api/send-message → backend

/weather-widget → widget iframe

/ → dashboard
```

# 🛠 Tech Stack

HTML5, CSS3, JavaScript (Vanilla)

Node.js

Vercel Serverless Functions

WeatherAPI.com

FontAwesome Icons

Google Fonts (Poppins)

CSS Glassmorphism + Animations

# 👨‍💻 Author

KAIRA Technologies
Real-Time Industrial Data Monitoring & Automation Solutions
```
🌐 https://kaira-technologies.com/
```
# 📄 License

Licensed under the MIT License.

# ⭐ Support

If this project helps you, please ⭐ star the repository!


---
