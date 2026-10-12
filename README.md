<div align="center">
  <h1>🌐 Roblox Web Parser & CMDR Integration</h1>
  <p>An in-game web content preview system powered by <b>Cmdr</b>, <b>HttpService</b>, and a serverless Node.js scraper.</p>

  <img src="https://img.shields.io/badge/Roblox-Luau-00A2FF?style=for-the-badge&logo=roblox&logoColor=white" alt="Roblox Luau">
  <img src="https://img.shields.io/badge/Cmdr-Command_Line-FF6B6B?style=for-the-badge" alt="Cmdr">
  <img src="https://img.shields.io/badge/Node.js-Parser_API-339933?style=for-the-badge&logo=nodedotjs&logoColor=white" alt="Node.js">
</div>

<hr>

<h2>📌 Overview</h2>
<p>
  This project allows Roblox game administrators to send web page previews directly to players' screens using custom <b>Cmdr</b> console commands (<code>:http</code> and <code>:httpmore</code>).
</p>
<p>
  Because Roblox engine limits native HTML rendering and restricts cross-origin web requests, this system uses an external <b>Node.js (Cheerio/Express) API</b> to parse HTML into structured JSON, which is then rendered into native Roblox UI elements inside a <code>ScrollingFrame</code>.
</p>

---

<h2>✨ Features</h2>
<ul>
  <li><b><code>:http &lt;url&gt;</code></b> — Opens a web preview prompt directly on the caller's screen.</li>
  <li><b><code>:httpmore &lt;targets&gt; &lt;url&gt;</code></b> — Broadcasts a web prompt button to specified player(s) or all clients.</li>
  <li><b>Admin Whitelisting:</b> Restricts Cmdr access and keybind activation to authorized UserIDs only.</li>
  <li><b>External HTML Scraper:</b> Strips script tags and converts headings (<code>&lt;h1&gt;</code>, <code>&lt;h2&gt;</code>) and paragraphs (<code>&lt;p&gt;</code>) into dynamic Roblox <code>TextLabel</code> components.</li>
</ul>

---

<h2>📁 File & Directory Layout</h2>

<pre>
<code>
├── ReplicatedStorage/
│   ├── Cmdr/                      # Official Cmdr Module
│   └── CmdrCommands/
│       ├── http.lua              # Command Definition (Self)
│       ├── httpServer.lua        # Command Execution
│       ├── httpmore.lua          # Command Definition (Targets)
│       └── httpmoreServer.lua    # Command Execution
│
├── ServerScriptService/
│   ├── CmdrServerInit.lua        # Registers default & custom Cmdr commands
│   └── WebFetcherServer.lua     # Handles RemoteFunction calls & HttpService
│
├── StarterPlayer/StarterPlayerScripts/
│   └── CmdrClientInit.lua        # Binds Cmdr activation keys for authorized UserIDs
│
├── StarterGui/
│   └── WebGui/
│       └── WebClientHandler.lua  # Manages prompt button & website UI window
│
└── serverless-parser/
    ├── package.json
    └── index.js                  # Express + Cheerio Web Parser
</code>
</pre>

---

<h2>🚀 Installation & Setup</h2>

<h3>1. Web Parser API (Node.js)</h3>
<p>Deploy the external parser script to a free hosting provider (Vercel, Render, or Railway):</p>

```bash
cd serverless-parser
npm install express axios cheerio
node index.js
