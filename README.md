<div align="center">

<style>
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  .terminal-container {
    background: #0d1117;
    border: 1px solid #30363d;
    border-radius: 8px;
    max-width: 900px;
    margin: 20px auto;
    box-shadow: 0 20px 60px rgba(0, 0, 0, 0.8), inset 0 1px 0 rgba(255, 255, 255, 0.1);
    font-family: 'Courier New', 'Monaco', 'Menlo', monospace;
    overflow: hidden;
  }

  .terminal-header {
    background: #161b22;
    border-bottom: 1px solid #30363d;
    padding: 12px 16px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    height: 45px;
  }

  .traffic-lights {
    display: flex;
    gap: 8px;
  }

  .traffic-light {
    width: 12px;
    height: 12px;
    border-radius: 50%;
    box-shadow: 0 0 3px rgba(0, 0, 0, 0.5);
  }

  .red { background: #ef5350; }
  .yellow { background: #fbbc04; }
  .green { background: #34a853; }

  .terminal-path {
    color: #8b949e;
    font-size: 12px;
    font-weight: 500;
    letter-spacing: 0.5px;
  }

  .terminal-body {
    padding: 24px 20px;
    color: #c9d1d9;
    line-height: 1.6;
  }

  .contribution-graph-section {
    margin-bottom: 40px;
    text-align: center;
  }

  .contribution-graph-title {
    color: #8b949e;
    font-size: 11px;
    text-transform: uppercase;
    letter-spacing: 1px;
    margin-bottom: 12px;
    opacity: 0.8;
  }

  .contribution-grid {
    display: inline-block;
    margin: 0 auto;
  }

  .contribution-row {
    display: flex;
    gap: 4px;
    margin-bottom: 4px;
  }

  .contribution-square {
    width: 16px;
    height: 16px;
    border-radius: 3px;
    border: 1px solid rgba(48, 54, 61, 0.8);
    background: #0e4429;
    cursor: pointer;
    transition: all 0.3s ease;
  }

  .contribution-square:hover {
    transform: scale(1.1);
    box-shadow: 0 0 8px rgba(57, 211, 83, 0.4);
  }

  .level-1 { background: #0e4429; }
  .level-2 { background: #006d32; }
  .level-3 { background: #26a641; }
  .level-4 {
    background: #39d353;
    box-shadow: 0 0 8px rgba(57, 211, 83, 0.5);
  }

  @keyframes graphLoad {
    from {
      opacity: 0;
      transform: translateX(-20px);
    }
    to {
      opacity: 1;
      transform: translateX(0);
    }
  }

  .contribution-row:nth-child(1) .contribution-square { animation: graphLoad 0.6s ease-out forwards; }
  .contribution-row:nth-child(2) .contribution-square { animation: graphLoad 0.7s ease-out forwards; }
  .contribution-row:nth-child(3) .contribution-square { animation: graphLoad 0.8s ease-out forwards; }
  .contribution-row:nth-child(4) .contribution-square { animation: graphLoad 0.9s ease-out forwards; }
  .contribution-row:nth-child(5) .contribution-square { animation: graphLoad 1s ease-out forwards; }
  .contribution-row:nth-child(6) .contribution-square { animation: graphLoad 1.1s ease-out forwards; }
  .contribution-row:nth-child(7) .contribution-square { animation: graphLoad 1.2s ease-out forwards; }

  .contribution-square:nth-child(1) { animation-delay: 0.1s; }
  .contribution-square:nth-child(2) { animation-delay: 0.15s; }
  .contribution-square:nth-child(3) { animation-delay: 0.2s; }
  .contribution-square:nth-child(4) { animation-delay: 0.25s; }
  .contribution-square:nth-child(5) { animation-delay: 0.3s; }

  .split-container {
    display: flex;
    gap: 30px;
    align-items: flex-start;
  }

  .left-pane {
    flex: 0 0 auto;
    min-width: 180px;
  }

  .ascii-art {
    font-size: 9px;
    line-height: 1.2;
    color: #58a6ff;
    text-shadow: 0 0 10px rgba(88, 166, 255, 0.4);
    white-space: pre;
    font-family: 'Courier New', monospace;
    font-weight: bold;
    overflow-x: auto;
    max-height: 280px;
    padding: 8px;
    background: rgba(88, 166, 255, 0.03);
    border-radius: 4px;
    border: 1px solid rgba(88, 166, 255, 0.15);
  }

  .right-pane {
    flex: 1;
    min-width: 250px;
  }

  .terminal-prompt {
    margin-bottom: 12px;
  }

  .prompt-text { color: #8b949e; }
  .prompt-user { color: #27c93f; font-weight: bold; }
  .prompt-path { color: #58a6ff; }
  .prompt-dollar { color: #8b949e; }
  .command { color: #8b949e; font-style: italic; }

  .about-content {
    margin-top: 12px;
    line-height: 1.8;
  }

  .about-line {
    display: flex;
    margin-bottom: 8px;
    align-items: flex-start;
  }

  .about-bullet {
    color: #8b949e;
    margin-right: 12px;
    flex-shrink: 0;
  }

  .about-label {
    color: #ff7b72;
    font-weight: bold;
    margin-right: 10px;
    min-width: 90px;
  }

  .about-value {
    color: #c9d1d9;
  }

  .about-value-highlight {
    color: #79c0ff;
    font-weight: 500;
  }

  .cursor {
    display: inline-block;
    width: 12px;
    height: 18px;
    background: #39d353;
    margin-left: 4px;
    animation: blink 1s step-end infinite;
    box-shadow: 0 0 10px rgba(57, 211, 83, 0.6);
  }

  @keyframes blink {
    0%, 49% { opacity: 1; }
    50%, 100% { opacity: 0; }
  }

  @media (max-width: 768px) {
    .split-container { flex-direction: column; gap: 20px; align-items: center; }
    .left-pane { min-width: auto; width: 100%; }
    .ascii-art { font-size: 8px; max-height: 250px; }
    .right-pane { width: 100%; }
    .terminal-body { padding: 16px 12px; }
  }

  @media (max-width: 600px) {
    .terminal-container { max-width: 100%; margin: 10px; }
    .terminal-body { padding: 12px 10px; }
    .contribution-square { width: 12px; height: 12px; }
    .about-label { min-width: 70px; font-size: 12px; }
    .about-value { font-size: 12px; }
  }
</style>

<div class="terminal-container">
  <div class="terminal-header">
    <div class="traffic-lights">
      <div class="traffic-light red"></div>
      <div class="traffic-light yellow"></div>
      <div class="traffic-light green"></div>
    </div>
    <div class="terminal-path">vansh@github:~$</div>
  </div>

  <div class="terminal-body">
    <div class="contribution-graph-section">
      <div class="contribution-graph-title">// contributions 2024</div>
      <div class="contribution-grid">
        <div class="contribution-row">
          <div class="contribution-square level-2"></div>
          <div class="contribution-square level-3"></div>
          <div class="contribution-square level-4"></div>
          <div class="contribution-square level-3"></div>
          <div class="contribution-square level-2"></div>
        </div>
        <div class="contribution-row">
          <div class="contribution-square level-1"></div>
          <div class="contribution-square level-4"></div>
          <div class="contribution-square level-4"></div>
          <div class="contribution-square level-4"></div>
          <div class="contribution-square level-1"></div>
        </div>
        <div class="contribution-row">
          <div class="contribution-square level-3"></div>
          <div class="contribution-square level-4"></div>
          <div class="contribution-square level-4"></div>
          <div class="contribution-square level-4"></div>
          <div class="contribution-square level-3"></div>
        </div>
        <div class="contribution-row">
          <div class="contribution-square level-2"></div>
          <div class="contribution-square level-3"></div>
          <div class="contribution-square level-4"></div>
          <div class="contribution-square level-3"></div>
          <div class="contribution-square level-2"></div>
        </div>
        <div class="contribution-row">
          <div class="contribution-square level-1"></div>
          <div class="contribution-square level-2"></div>
          <div class="contribution-square level-3"></div>
          <div class="contribution-square level-2"></div>
          <div class="contribution-square level-1"></div>
        </div>
        <div class="contribution-row">
          <div class="contribution-square level-2"></div>
          <div class="contribution-square level-4"></div>
          <div class="contribution-square level-4"></div>
          <div class="contribution-square level-4"></div>
          <div class="contribution-square level-2"></div>
        </div>
        <div class="contribution-row">
          <div class="contribution-square level-3"></div>
          <div class="contribution-square level-3"></div>
          <div class="contribution-square level-3"></div>
          <div class="contribution-square level-3"></div>
          <div class="contribution-square level-3"></div>
        </div>
      </div>
    </div>

    <div class="split-container">
      <div class="left-pane">
        <pre class="ascii-art">   ██╗   ██╗ █████╗ ███╗   ██╗███████╗██╗  ██╗
   ██║   ██║██╔══██╗████╗  ██║██╔════╝██║  ██║
   ██║   ██║███████║██╔██╗ ██║███████╗███████║
   ╚██╗ ██╔╝██╔══██║██║╚██╗██║╚════██║██╔══██║
    ╚████╔╝ ██║  ██║██║ ╚████║███████║██║  ██║
     ╚═══╝  ╚═╝  ╚═╝╚═╝  ╚═══╝╚══════╝╚═╝  ╚═╝

          Developer & Trader</pre>
      </div>

      <div class="right-pane">
        <div class="terminal-prompt">
          <span class="prompt-user">vansh@github</span><span class="prompt-text">:</span><span class="prompt-path">~</span><span class="prompt-dollar">$</span> <span class="command">cat about.txt</span>
        </div>

        <div class="about-content">
          <div class="about-line">
            <span class="about-bullet">›</span>
            <span class="about-label">Name</span>
            <span class="about-value">Vansh Kapadia</span>
          </div>

          <div class="about-line">
            <span class="about-bullet">›</span>
            <span class="about-label">Role</span>
            <span class="about-value">Algorithmic Trader & Dev</span>
          </div>

          <div class="about-line">
            <span class="about-bullet">›</span>
            <span class="about-label">Focus</span>
            <span class="about-value">NIFTY Intraday Structure</span>
          </div>

          <div class="about-line">
            <span class="about-bullet">›</span>
            <span class="about-label">Stack</span>
            <span class="about-value">Python, Flask, <span class="about-value-highlight">yfinance</span></span>
          </div>

          <div class="about-line">
            <span class="about-bullet">›</span>
            <span class="about-label">Location</span>
            <span class="about-value">India 🇮🇳</span>
          </div>

          <div class="about-line">
            <span class="about-bullet">›</span>
            <span class="about-label">Status</span>
            <span class="about-value"><span class="about-value-highlight">Building trading bots</span></span>
          </div>
        </div>

        <div style="margin-top: 16px;">
          <span class="prompt-user">vansh@github</span><span class="prompt-text">:</span><span class="prompt-path">~</span><span class="prompt-dollar">$</span> <span class="cursor"></span>
        </div>
      </div>
    </div>
  </div>
</div>

</div>

---

## 🚀 Featured Projects

<details>
<summary><b>📊 NIFTY Intraday Structure Bot</b></summary>

**Live 24/5 algorithmic trading signal generator for NIFTY 50**
- Classifies Trend/Range days using VWAP behavior
- Trades VWAP pullbacks, BB+VWAP fades, and OI walls
- Real-time Telegram alerts + Google Sheets logging
- Deployed on Render (free tier) with UptimeRobot keep-alive

[→ Repository](https://github.com/vanshkapadia11/Indian-Options-Trading)

</details>

---

## 📈 Current Focus

🔹 **Building:** Systematic NIFTY intraday trading strategies  
🔹 **Learning:** Market microstructure & quantitative finance  
🔹 **Shipping:** Open-source trading tools & bots  

---

## 📚 Tech Stack

**Languages:** Python, JavaScript  
**Framework:** Flask, React  
**Data:** yfinance, NSE API, Google Sheets  
**Infrastructure:** Render, GitHub Actions, UptimeRobot  

---

## 🔗 Connect

[![Email](https://img.shields.io/badge/Email-contact%40vanshkapadia.dev-0d1117?style=flat)](mailto:contact@vanshkapadia.dev)
[![Twitter](https://img.shields.io/badge/Twitter-@vanshkapadia11-0d1117?style=flat)](https://twitter.com/vanshkapadia11)

---

<sub>🎯 Crafted with passion, algorithms, and cyberpunk aesthetics ✨</sub>
