📘 KAIRA Dashboard – Real-Time Monitoring & Weather Widget

A modern, responsive, multi-module dashboard for industry monitoring, WhatsApp messaging, and real-time weather updates.
Built with pure HTML, CSS, JavaScript, and deployed using Vercel.

🚀 Features
🔹 1. Interactive Sidebar Navigation

Water Dashboards (Grafana)

Water Reports (Looker Studio)

Tyre → Mixer → TBM multi-level dropdown menus

WhatsApp Messaging Module (custom UI)

🔹 2. Premium Weather Widget

Live weather from WeatherAPI.com

Mini card + Expandable full panel

5-day forecast

Astronomy, Marine, Air Quality, Alerts

Parent-iframe communication using postMessage

Auto refresh every 60 seconds

🔹 3. WhatsApp Messaging Module

Clean UI for entering mobile number

Sends messages via /api/send-message endpoint

Integrated with Node.js server (server.js)

Error handling + success message

🔹 4. Modern UI / UX

Glassmorphism cards

Poppins font

Gradient backgrounds

Smooth expand animations

Responsive layout

📂 Project Structure
/webpage
│
├── index.html             # Main dashboard UI
├── weather-widget.html    # Weather widget inside iframe
├── server.js              # WhatsApp API backend handler
├── package.json           # Node + Vercel dependencies
├── vercel.json            # Routing & build configuration
├── README.md              # Documentation file
└── LICENSE (optional)

⚙️ How to Run Locally
1. Install Node.js

https://nodejs.org/

2. Install dependencies
npm install

3. Start local server
node server.js


Your dashboard will open at:

http://localhost:3000

🌤️ Weather Widget – Setup Instructions
✔ 1. Add iframe inside index.html
<iframe src="/weather-widget" id="weatherFrame" class="weather-iframe"></iframe>

✔ 2. Enable expand/collapse from widget

Your weather widget sends messages to the parent:

window.parent.postMessage({ type: "weatherExpand" }, "*");
window.parent.postMessage({ type: "weatherCollapse" }, "*");

✔ 3. Parent listens inside index.html:
window.addEventListener("message", (event) => {
  const frame = document.getElementById("weatherFrame");

  if (event.data.type === "weatherExpand") {
    frame.classList.add("expanded");
  }
  if (event.data.type === "weatherCollapse") {
    frame.classList.remove("expanded");
  }
});

🍃 Weather API Setup

Weather powered by WeatherAPI.com

Replace inside weather-widget.html:

const apiKey = "YOUR_API_KEY_HERE";


Get free API key:
👉 https://www.weatherapi.com/

💬 WhatsApp Messaging API
✔ Endpoint (Node.js)

server.js handles the API:

POST /api/send-message

✔ Frontend call:
fetch("/api/send-message", {
  method: "POST",
  headers: { "Content-Type": "application/json" },
  body: JSON.stringify({ mobile })
})


Displays success or error inside the UI.

▲ Vercel Deployment
1. Install Vercel CLI
npm i -g vercel

2. Login
vercel login

3. Deploy
vercel

📁 Important: Vercel Routing

Your vercel.json:

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


This ensures:

/api/send-message → Node server

/weather-widget → correct weather widget

/ → dashboard



🤝 Contributing

Pull requests are welcome.
For major changes, please open an issue first.

📄 License

MIT License

⭐ If you like this project

You can star the GitHub repo!
