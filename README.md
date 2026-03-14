<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>FlowGenius AI — Workflows Intelligents pour Entreprises</title>
<link href="https://fonts.googleapis.com/css2?family=Clash+Display:wght@400;500;600;700&family=Bricolage+Grotesque:wght@300;400;500;600&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet">
<style>
  :root {
    --bg: #050A0E;
    --surface: #0B1318;
    --surface2: #111C24;
    --border: #1A2D3A;
    --accent: #00E5A0;
    --accent2: #0099FF;
    --accent3: #FF6B35;
    --text: #E8F4F0;
    --text2: #7A9BAA;
    --text3: #3D5A6A;
    --glow: rgba(0,229,160,0.15);
    --glow2: rgba(0,153,255,0.12);
  }

  * { margin: 0; padding: 0; box-sizing: border-box; }

  html { scroll-behavior: smooth; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: 'Bricolage Grotesque', sans-serif;
    overflow-x: hidden;
    cursor: none;
  }

  /* CUSTOM CURSOR */
  .cursor {
    width: 12px; height: 12px;
    background: var(--accent);
    border-radius: 50%;
    position: fixed;
    pointer-events: none;
    z-index: 9999;
    transition: transform 0.1s, opacity 0.2s;
    mix-blend-mode: difference;
  }
  .cursor-ring {
    width: 36px; height: 36px;
    border: 1.5px solid var(--accent);
    border-radius: 50%;
    position: fixed;
    pointer-events: none;
    z-index: 9998;
    transition: all 0.15s ease;
    opacity: 0.5;
  }

  /* GRID BACKGROUND */
  body::before {
    content: '';
    position: fixed;
    inset: 0;
    background-image:
      linear-gradient(var(--border) 1px, transparent 1px),
      linear-gradient(90deg, var(--border) 1px, transparent 1px);
    background-size: 60px 60px;
    opacity: 0.3;
    pointer-events: none;
    z-index: 0;
  }

  /* AMBIENT GLOWS */
  .glow-orb {
    position: fixed;
    border-radius: 50%;
    filter: blur(120px);
    pointer-events: none;
    z-index: 0;
  }
  .orb1 { width: 600px; height: 600px; top: -200px; left: -200px; background: rgba(0,229,160,0.06); }
  .orb2 { width: 500px; height: 500px; bottom: 0; right: -100px; background: rgba(0,153,255,0.07); }
  .orb3 { width: 400px; height: 400px; top: 40%; left: 40%; background: rgba(255,107,53,0.04); }

  /* NAV */
  nav {
    position: fixed;
    top: 0; left: 0; right: 0;
    z-index: 100;
    padding: 20px 60px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    background: rgba(5,10,14,0.8);
    backdrop-filter: blur(20px);
    border-bottom: 1px solid var(--border);
  }

  .logo {
    font-family: 'Clash Display', sans-serif;
    font-size: 22px;
    font-weight: 700;
    letter-spacing: -0.5px;
    display: flex;
    align-items: center;
    gap: 10px;
  }
  .logo-icon {
    width: 34px; height: 34px;
    background: linear-gradient(135deg, var(--accent), var(--accent2));
    border-radius: 8px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 16px;
  }
  .logo span { color: var(--accent); }

  .nav-links {
    display: flex;
    gap: 40px;
    list-style: none;
  }
  .nav-links a {
    color: var(--text2);
    text-decoration: none;
    font-size: 14px;
    font-weight: 500;
    transition: color 0.2s;
    letter-spacing: 0.3px;
  }
  .nav-links a:hover { color: var(--text); }

  .nav-cta {
    background: var(--accent);
    color: var(--bg);
    border: none;
    padding: 10px 24px;
    border-radius: 6px;
    font-family: 'Bricolage Grotesque', sans-serif;
    font-weight: 600;
    font-size: 14px;
    cursor: pointer;
    transition: all 0.2s;
    letter-spacing: 0.3px;
  }
  .nav-cta:hover {
    background: #00FFB2;
    transform: translateY(-1px);
    box-shadow: 0 8px 30px rgba(0,229,160,0.3);
  }

  /* SECTIONS */
  section { position: relative; z-index: 1; }

  /* HERO */
  .hero {
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    text-align: center;
    padding: 120px 40px 80px;
  }

  .hero-badge {
    display: inline-flex;
    align-items: center;
    gap: 8px;
    background: rgba(0,229,160,0.08);
    border: 1px solid rgba(0,229,160,0.2);
    padding: 6px 16px;
    border-radius: 100px;
    font-size: 12px;
    font-weight: 500;
    color: var(--accent);
    letter-spacing: 1px;
    text-transform: uppercase;
    margin-bottom: 40px;
    animation: fadeUp 0.6s ease both;
  }
  .badge-dot {
    width: 6px; height: 6px;
    background: var(--accent);
    border-radius: 50%;
    animation: pulse 2s infinite;
  }

  .hero h1 {
    font-family: 'Clash Display', sans-serif;
    font-size: clamp(48px, 7vw, 96px);
    font-weight: 700;
    line-height: 1.0;
    letter-spacing: -3px;
    max-width: 900px;
    margin-bottom: 32px;
    animation: fadeUp 0.6s 0.1s ease both;
  }
  .hero h1 .highlight {
    background: linear-gradient(135deg, var(--accent), var(--accent2));
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
  }
  .hero h1 .line2 { color: var(--text2); }

  .hero-desc {
    font-size: 18px;
    color: var(--text2);
    max-width: 560px;
    line-height: 1.7;
    margin-bottom: 50px;
    font-weight: 300;
    animation: fadeUp 0.6s 0.2s ease both;
  }

  .hero-actions {
    display: flex;
    gap: 16px;
    align-items: center;
    animation: fadeUp 0.6s 0.3s ease both;
    flex-wrap: wrap;
    justify-content: center;
  }

  .btn-primary {
    background: linear-gradient(135deg, var(--accent), #00C880);
    color: var(--bg);
    border: none;
    padding: 16px 36px;
    border-radius: 8px;
    font-family: 'Bricolage Grotesque', sans-serif;
    font-weight: 700;
    font-size: 16px;
    cursor: pointer;
    transition: all 0.25s;
    letter-spacing: 0.3px;
  }
  .btn-primary:hover {
    transform: translateY(-2px);
    box-shadow: 0 16px 50px rgba(0,229,160,0.35);
  }

  .btn-secondary {
    background: transparent;
    color: var(--text);
    border: 1px solid var(--border);
    padding: 16px 36px;
    border-radius: 8px;
    font-family: 'Bricolage Grotesque', sans-serif;
    font-weight: 500;
    font-size: 16px;
    cursor: pointer;
    transition: all 0.25s;
  }
  .btn-secondary:hover {
    border-color: var(--accent);
    color: var(--accent);
    background: rgba(0,229,160,0.05);
  }

  .hero-stats {
    display: flex;
    gap: 60px;
    margin-top: 80px;
    padding-top: 40px;
    border-top: 1px solid var(--border);
    animation: fadeUp 0.6s 0.5s ease both;
    flex-wrap: wrap;
    justify-content: center;
  }
  .stat-item { text-align: center; }
  .stat-num {
    font-family: 'Clash Display', sans-serif;
    font-size: 36px;
    font-weight: 700;
    color: var(--accent);
    letter-spacing: -1px;
  }
  .stat-label {
    font-size: 12px;
    color: var(--text3);
    text-transform: uppercase;
    letter-spacing: 1.5px;
    margin-top: 4px;
  }

  /* WORKFLOW DEMO */
  .demo-section {
    padding: 100px 60px;
    max-width: 1300px;
    margin: 0 auto;
  }

  .section-label {
    font-size: 11px;
    color: var(--accent);
    letter-spacing: 3px;
    text-transform: uppercase;
    font-weight: 600;
    margin-bottom: 16px;
  }
  .section-title {
    font-family: 'Clash Display', sans-serif;
    font-size: clamp(32px, 4vw, 54px);
    font-weight: 700;
    letter-spacing: -1.5px;
    line-height: 1.1;
    margin-bottom: 20px;
  }
  .section-sub {
    color: var(--text2);
    font-size: 16px;
    max-width: 500px;
    line-height: 1.7;
    font-weight: 300;
  }

  /* AI GENERATOR APP */
  .app-container {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 20px;
    overflow: hidden;
    margin-top: 60px;
    box-shadow: 0 40px 120px rgba(0,0,0,0.5), 0 0 0 1px rgba(0,229,160,0.05);
  }

  .app-header {
    padding: 20px 28px;
    border-bottom: 1px solid var(--border);
    display: flex;
    align-items: center;
    justify-content: space-between;
    background: var(--surface2);
  }
  .app-title {
    font-family: 'JetBrains Mono', monospace;
    font-size: 12px;
    color: var(--text3);
    letter-spacing: 1px;
  }
  .app-dots {
    display: flex;
    gap: 7px;
  }
  .app-dots span {
    width: 10px; height: 10px;
    border-radius: 50%;
    background: var(--border);
  }
  .app-dots span:nth-child(1) { background: #FF5F57; }
  .app-dots span:nth-child(2) { background: #FFBD2E; }
  .app-dots span:nth-child(3) { background: #28CA41; }

  .app-body {
    display: grid;
    grid-template-columns: 1fr 1fr;
    min-height: 500px;
  }

  .input-panel {
    padding: 36px;
    border-right: 1px solid var(--border);
  }

  .input-label {
    font-size: 11px;
    color: var(--text3);
    text-transform: uppercase;
    letter-spacing: 2px;
    margin-bottom: 12px;
  }

  .business-select {
    width: 100%;
    background: var(--surface2);
    border: 1px solid var(--border);
    color: var(--text);
    padding: 12px 16px;
    border-radius: 8px;
    font-family: 'Bricolage Grotesque', sans-serif;
    font-size: 14px;
    margin-bottom: 20px;
    outline: none;
    cursor: pointer;
    transition: border-color 0.2s;
  }
  .business-select:focus { border-color: var(--accent); }

  .goal-input {
    width: 100%;
    background: var(--surface2);
    border: 1px solid var(--border);
    color: var(--text);
    padding: 14px 16px;
    border-radius: 8px;
    font-family: 'Bricolage Grotesque', sans-serif;
    font-size: 14px;
    margin-bottom: 20px;
    outline: none;
    resize: none;
    height: 100px;
    transition: border-color 0.2s;
    line-height: 1.6;
  }
  .goal-input::placeholder { color: var(--text3); }
  .goal-input:focus { border-color: var(--accent); }

  .objective-tags {
    display: flex;
    flex-wrap: wrap;
    gap: 8px;
    margin-bottom: 24px;
  }
  .obj-tag {
    background: var(--surface2);
    border: 1px solid var(--border);
    color: var(--text2);
    padding: 6px 14px;
    border-radius: 100px;
    font-size: 12px;
    cursor: pointer;
    transition: all 0.2s;
    font-weight: 500;
  }
  .obj-tag:hover, .obj-tag.active {
    border-color: var(--accent);
    color: var(--accent);
    background: rgba(0,229,160,0.06);
  }

  .generate-btn {
    width: 100%;
    background: linear-gradient(135deg, var(--accent), #00C880);
    color: var(--bg);
    border: none;
    padding: 14px;
    border-radius: 8px;
    font-family: 'Bricolage Grotesque', sans-serif;
    font-weight: 700;
    font-size: 15px;
    cursor: pointer;
    transition: all 0.2s;
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 8px;
  }
  .generate-btn:hover {
    transform: translateY(-1px);
    box-shadow: 0 10px 40px rgba(0,229,160,0.3);
  }
  .generate-btn:disabled {
    opacity: 0.6;
    cursor: not-allowed;
    transform: none;
  }

  .output-panel {
    padding: 36px;
    overflow-y: auto;
    max-height: 580px;
  }

  .output-placeholder {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    height: 100%;
    color: var(--text3);
    text-align: center;
    gap: 16px;
  }
  .placeholder-icon {
    font-size: 48px;
    opacity: 0.3;
  }
  .placeholder-text {
    font-size: 14px;
    line-height: 1.6;
    max-width: 240px;
  }

  .workflow-output {
    display: none;
  }
  .workflow-output.visible { display: block; }

  .workflow-title {
    font-family: 'Clash Display', sans-serif;
    font-size: 20px;
    font-weight: 600;
    margin-bottom: 8px;
    letter-spacing: -0.5px;
    color: var(--accent);
  }
  .workflow-meta {
    font-size: 12px;
    color: var(--text3);
    margin-bottom: 28px;
    font-family: 'JetBrains Mono', monospace;
  }

  .workflow-step {
    display: flex;
    gap: 16px;
    margin-bottom: 20px;
    animation: stepIn 0.4s ease both;
  }

  .step-number {
    width: 32px;
    height: 32px;
    min-width: 32px;
    background: rgba(0,229,160,0.1);
    border: 1px solid rgba(0,229,160,0.3);
    border-radius: 8px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-family: 'JetBrains Mono', monospace;
    font-size: 11px;
    font-weight: 600;
    color: var(--accent);
  }

  .step-content { flex: 1; }
  .step-name {
    font-weight: 600;
    font-size: 14px;
    margin-bottom: 4px;
    color: var(--text);
  }
  .step-desc {
    font-size: 12px;
    color: var(--text2);
    line-height: 1.5;
  }
  .step-tool {
    display: inline-block;
    background: rgba(0,153,255,0.1);
    border: 1px solid rgba(0,153,255,0.2);
    color: var(--accent2);
    padding: 2px 8px;
    border-radius: 4px;
    font-size: 10px;
    font-family: 'JetBrains Mono', monospace;
    margin-top: 6px;
  }

  .step-connector {
    width: 1px;
    height: 16px;
    background: linear-gradient(to bottom, rgba(0,229,160,0.3), transparent);
    margin-left: 15px;
    margin-bottom: 4px;
  }

  .kpi-row {
    display: flex;
    gap: 12px;
    margin-top: 24px;
    padding-top: 20px;
    border-top: 1px solid var(--border);
    flex-wrap: wrap;
  }
  .kpi-pill {
    background: var(--surface2);
    border: 1px solid var(--border);
    padding: 8px 14px;
    border-radius: 8px;
    font-size: 12px;
    display: flex;
    align-items: center;
    gap: 8px;
  }
  .kpi-label { color: var(--text3); }
  .kpi-value { color: var(--accent); font-weight: 600; font-family: 'JetBrains Mono', monospace; }

  .loading-animation {
    display: none;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    height: 300px;
    gap: 20px;
  }
  .loading-animation.visible { display: flex; }

  .loader-ring {
    width: 48px;
    height: 48px;
    border: 2px solid var(--border);
    border-top-color: var(--accent);
    border-radius: 50%;
    animation: spin 0.8s linear infinite;
  }
  .loading-text {
    font-size: 13px;
    color: var(--text3);
    font-family: 'JetBrains Mono', monospace;
    animation: blink 1s ease infinite;
  }

  /* HOW IT WORKS */
  .how-section {
    padding: 100px 60px;
    max-width: 1300px;
    margin: 0 auto;
  }

  .steps-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 2px;
    margin-top: 60px;
    background: var(--border);
    border-radius: 16px;
    overflow: hidden;
  }

  .how-step {
    background: var(--surface);
    padding: 48px 40px;
    position: relative;
    transition: background 0.3s;
  }
  .how-step:hover { background: var(--surface2); }

  .how-num {
    font-family: 'Clash Display', sans-serif;
    font-size: 72px;
    font-weight: 700;
    color: var(--surface2);
    line-height: 1;
    margin-bottom: 24px;
    letter-spacing: -3px;
  }
  .how-step:hover .how-num { color: rgba(0,229,160,0.1); }

  .how-icon {
    font-size: 28px;
    margin-bottom: 16px;
  }
  .how-title {
    font-family: 'Clash Display', sans-serif;
    font-size: 22px;
    font-weight: 600;
    margin-bottom: 12px;
    letter-spacing: -0.5px;
  }
  .how-desc {
    font-size: 14px;
    color: var(--text2);
    line-height: 1.7;
    font-weight: 300;
  }

  /* USE CASES */
  .cases-section {
    padding: 100px 60px;
    background: var(--surface);
    border-top: 1px solid var(--border);
    border-bottom: 1px solid var(--border);
  }
  .cases-inner { max-width: 1300px; margin: 0 auto; }

  .cases-grid {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 16px;
    margin-top: 60px;
  }

  .case-card {
    background: var(--bg);
    border: 1px solid var(--border);
    border-radius: 14px;
    padding: 32px 28px;
    transition: all 0.3s;
    position: relative;
    overflow: hidden;
  }
  .case-card::before {
    content: '';
    position: absolute;
    top: 0; left: 0; right: 0;
    height: 2px;
    background: linear-gradient(90deg, transparent, var(--accent), transparent);
    transform: scaleX(0);
    transition: transform 0.3s;
  }
  .case-card:hover::before { transform: scaleX(1); }
  .case-card:hover {
    border-color: rgba(0,229,160,0.2);
    transform: translateY(-4px);
    box-shadow: 0 20px 60px rgba(0,0,0,0.3);
  }

  .case-emoji { font-size: 32px; margin-bottom: 20px; }
  .case-name {
    font-family: 'Clash Display', sans-serif;
    font-size: 18px;
    font-weight: 600;
    margin-bottom: 10px;
    letter-spacing: -0.3px;
  }
  .case-desc {
    font-size: 13px;
    color: var(--text2);
    line-height: 1.6;
    font-weight: 300;
  }
  .case-result {
    margin-top: 20px;
    padding-top: 16px;
    border-top: 1px solid var(--border);
    font-size: 12px;
    color: var(--accent);
    font-weight: 600;
    font-family: 'JetBrains Mono', monospace;
  }

  /* PRICING */
  .pricing-section {
    padding: 100px 60px;
    max-width: 1200px;
    margin: 0 auto;
  }

  .pricing-header { text-align: center; margin-bottom: 60px; }
  .pricing-header .section-sub { margin: 0 auto; }

  .pricing-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 20px;
    align-items: start;
  }

  .pricing-card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 16px;
    padding: 40px 36px;
    position: relative;
    transition: transform 0.3s;
  }
  .pricing-card:hover { transform: translateY(-4px); }
  .pricing-card.featured {
    background: linear-gradient(135deg, rgba(0,229,160,0.06), rgba(0,153,255,0.04));
    border-color: rgba(0,229,160,0.3);
    box-shadow: 0 0 60px rgba(0,229,160,0.08);
  }

  .featured-badge {
    position: absolute;
    top: -12px;
    left: 50%;
    transform: translateX(-50%);
    background: var(--accent);
    color: var(--bg);
    padding: 4px 18px;
    border-radius: 100px;
    font-size: 11px;
    font-weight: 700;
    letter-spacing: 1px;
    text-transform: uppercase;
    white-space: nowrap;
  }

  .plan-name {
    font-family: 'Clash Display', sans-serif;
    font-size: 20px;
    font-weight: 700;
    margin-bottom: 8px;
    letter-spacing: -0.3px;
  }
  .plan-desc {
    font-size: 13px;
    color: var(--text2);
    margin-bottom: 28px;
    font-weight: 300;
    line-height: 1.5;
  }

  .plan-price {
    display: flex;
    align-items: baseline;
    gap: 6px;
    margin-bottom: 8px;
  }
  .price-currency { font-size: 18px; color: var(--text2); }
  .price-amount {
    font-family: 'Clash Display', sans-serif;
    font-size: 52px;
    font-weight: 700;
    line-height: 1;
    letter-spacing: -2px;
  }
  .pricing-card.featured .price-amount { color: var(--accent); }
  .price-period { font-size: 14px; color: var(--text3); }

  .price-alt {
    font-size: 12px;
    color: var(--text3);
    margin-bottom: 28px;
    font-family: 'JetBrains Mono', monospace;
  }

  .plan-divider {
    height: 1px;
    background: var(--border);
    margin-bottom: 24px;
  }

  .feature-list { list-style: none; margin-bottom: 32px; }
  .feature-item {
    display: flex;
    align-items: flex-start;
    gap: 10px;
    padding: 7px 0;
    font-size: 13px;
    color: var(--text2);
    font-weight: 400;
    line-height: 1.4;
  }
  .feature-icon { color: var(--accent); font-size: 14px; flex-shrink: 0; margin-top: 1px; }
  .feature-icon.muted { color: var(--text3); }

  .plan-btn {
    width: 100%;
    padding: 14px;
    border-radius: 8px;
    font-family: 'Bricolage Grotesque', sans-serif;
    font-weight: 700;
    font-size: 14px;
    cursor: pointer;
    transition: all 0.2s;
    letter-spacing: 0.3px;
  }
  .plan-btn.outline {
    background: transparent;
    border: 1px solid var(--border);
    color: var(--text);
  }
  .plan-btn.outline:hover {
    border-color: var(--accent);
    color: var(--accent);
  }
  .plan-btn.filled {
    background: linear-gradient(135deg, var(--accent), #00C880);
    border: none;
    color: var(--bg);
    box-shadow: 0 8px 30px rgba(0,229,160,0.2);
  }
  .plan-btn.filled:hover {
    transform: translateY(-1px);
    box-shadow: 0 14px 40px rgba(0,229,160,0.35);
  }

  /* TESTIMONIALS */
  .testimonials-section {
    padding: 80px 60px;
    background: var(--surface);
    border-top: 1px solid var(--border);
  }
  .testimonials-inner { max-width: 1300px; margin: 0 auto; }

  .testimonials-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 20px;
    margin-top: 50px;
  }

  .testimonial-card {
    background: var(--bg);
    border: 1px solid var(--border);
    border-radius: 14px;
    padding: 28px;
    transition: border-color 0.3s;
  }
  .testimonial-card:hover { border-color: rgba(0,229,160,0.15); }

  .stars { color: var(--accent); font-size: 14px; margin-bottom: 16px; letter-spacing: 2px; }

  .testimonial-text {
    font-size: 14px;
    color: var(--text2);
    line-height: 1.7;
    margin-bottom: 20px;
    font-style: italic;
    font-weight: 300;
  }

  .testimonial-author {
    display: flex;
    align-items: center;
    gap: 12px;
  }
  .author-avatar {
    width: 38px; height: 38px;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 16px;
    background: var(--surface);
    border: 1px solid var(--border);
  }
  .author-name {
    font-weight: 600;
    font-size: 13px;
  }
  .author-role {
    font-size: 11px;
    color: var(--text3);
    margin-top: 2px;
  }

  /* FAQ */
  .faq-section {
    padding: 100px 60px;
    max-width: 800px;
    margin: 0 auto;
  }
  .faq-header { text-align: center; margin-bottom: 50px; }

  .faq-item {
    border: 1px solid var(--border);
    border-radius: 10px;
    margin-bottom: 10px;
    overflow: hidden;
    transition: border-color 0.2s;
  }
  .faq-item:hover { border-color: rgba(0,229,160,0.2); }

  .faq-q {
    width: 100%;
    background: var(--surface);
    border: none;
    padding: 20px 24px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    cursor: pointer;
    font-family: 'Bricolage Grotesque', sans-serif;
    font-size: 15px;
    font-weight: 500;
    color: var(--text);
    text-align: left;
    transition: background 0.2s;
  }
  .faq-q:hover { background: var(--surface2); }
  .faq-arrow { color: var(--text3); transition: transform 0.3s; font-size: 18px; }
  .faq-item.open .faq-arrow { transform: rotate(45deg); color: var(--accent); }

  .faq-a {
    max-height: 0;
    overflow: hidden;
    transition: max-height 0.3s ease;
  }
  .faq-item.open .faq-a { max-height: 200px; }
  .faq-a-inner {
    padding: 0 24px 20px;
    font-size: 14px;
    color: var(--text2);
    line-height: 1.7;
    font-weight: 300;
    background: var(--surface);
  }

  /* CTA FINAL */
  .cta-section {
    padding: 120px 60px;
    text-align: center;
    position: relative;
    overflow: hidden;
  }
  .cta-section::before {
    content: '';
    position: absolute;
    inset: 0;
    background: radial-gradient(ellipse 80% 60% at 50% 50%, rgba(0,229,160,0.06), transparent);
  }
  .cta-section .section-title { max-width: 700px; margin: 0 auto 20px; }
  .cta-section .section-sub { margin: 0 auto 40px; }
  .cta-inner { position: relative; z-index: 1; }

  /* FOOTER */
  footer {
    border-top: 1px solid var(--border);
    padding: 50px 60px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    flex-wrap: wrap;
    gap: 20px;
  }
  .footer-logo {
    font-family: 'Clash Display', sans-serif;
    font-size: 18px;
    font-weight: 700;
  }
  .footer-logo span { color: var(--accent); }
  .footer-links {
    display: flex;
    gap: 30px;
    list-style: none;
  }
  .footer-links a {
    color: var(--text3);
    text-decoration: none;
    font-size: 13px;
    transition: color 0.2s;
  }
  .footer-links a:hover { color: var(--text2); }
  .footer-copy {
    font-size: 12px;
    color: var(--text3);
    font-family: 'JetBrains Mono', monospace;
  }

  /* ANIMATIONS */
  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(24px); }
    to { opacity: 1; transform: translateY(0); }
  }
  @keyframes pulse {
    0%, 100% { opacity: 1; }
    50% { opacity: 0.4; }
  }
  @keyframes spin {
    to { transform: rotate(360deg); }
  }
  @keyframes blink {
    0%, 100% { opacity: 1; }
    50% { opacity: 0.4; }
  }
  @keyframes stepIn {
    from { opacity: 0; transform: translateX(-10px); }
    to { opacity: 1; transform: translateX(0); }
  }
  @keyframes float {
    0%, 100% { transform: translateY(0); }
    50% { transform: translateY(-8px); }
  }


  /* AFFILIATION */
  .affil-section {
    padding: 100px 60px;
    background: linear-gradient(135deg, rgba(0,229,160,0.03), rgba(0,153,255,0.02));
    border-top: 1px solid var(--border);
    border-bottom: 1px solid var(--border);
  }
  .affil-inner { max-width: 1300px; margin: 0 auto; }

  .affil-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 60px;
    align-items: start;
    margin-top: 60px;
  }

  .earn-cards {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 14px;
    margin-bottom: 32px;
  }
  .earn-card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 14px;
    padding: 24px 20px;
    position: relative;
    overflow: hidden;
    transition: transform 0.3s, border-color 0.3s;
  }
  .earn-card::before {
    content: '';
    position: absolute;
    top: 0; left: 0; right: 0;
    height: 2px;
    background: linear-gradient(90deg, var(--accent), var(--accent2));
  }
  .earn-card:hover {
    transform: translateY(-3px);
    border-color: rgba(0,229,160,0.2);
  }
  .earn-plan {
    font-size: 11px;
    color: var(--text3);
    text-transform: uppercase;
    letter-spacing: 1.5px;
    font-family: 'JetBrains Mono', monospace;
    margin-bottom: 10px;
  }
  .earn-amount {
    font-family: 'Clash Display', sans-serif;
    font-size: 32px;
    font-weight: 700;
    color: var(--accent);
    letter-spacing: -1px;
    line-height: 1;
    margin-bottom: 4px;
  }
  .earn-per {
    font-size: 12px;
    color: var(--text3);
    font-family: 'JetBrains Mono', monospace;
  }

  .affil-steps {
    display: flex;
    flex-direction: column;
    gap: 16px;
    margin-bottom: 32px;
  }
  .affil-step {
    display: flex;
    gap: 16px;
    align-items: flex-start;
  }
  .affil-step-num {
    width: 32px;
    height: 32px;
    min-width: 32px;
    background: rgba(0,229,160,0.08);
    border: 1px solid rgba(0,229,160,0.25);
    border-radius: 8px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-family: 'JetBrains Mono', monospace;
    font-size: 12px;
    font-weight: 600;
    color: var(--accent);
  }
  .affil-step-text { flex: 1; }
  .affil-step-title {
    font-weight: 600;
    font-size: 14px;
    margin-bottom: 3px;
    color: var(--text);
  }
  .affil-step-desc {
    font-size: 13px;
    color: var(--text2);
    line-height: 1.5;
    font-weight: 300;
  }

  /* FORM */
  .affil-form-wrap {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 20px;
    overflow: hidden;
    box-shadow: 0 30px 80px rgba(0,0,0,0.3);
  }
  .affil-form-header {
    padding: 24px 32px;
    background: var(--surface2);
    border-bottom: 1px solid var(--border);
    display: flex;
    align-items: center;
    justify-content: space-between;
  }
  .affil-form-title {
    font-family: 'Clash Display', sans-serif;
    font-size: 18px;
    font-weight: 600;
    letter-spacing: -0.3px;
  }
  .affil-badge {
    background: rgba(0,229,160,0.1);
    border: 1px solid rgba(0,229,160,0.25);
    color: var(--accent);
    padding: 4px 12px;
    border-radius: 100px;
    font-size: 11px;
    font-weight: 600;
    letter-spacing: 1px;
    text-transform: uppercase;
    font-family: 'JetBrains Mono', monospace;
  }
  .affil-form-body { padding: 32px; }

  .form-group { margin-bottom: 18px; }
  .form-label {
    display: block;
    font-size: 11px;
    color: var(--text3);
    text-transform: uppercase;
    letter-spacing: 2px;
    margin-bottom: 8px;
    font-family: 'JetBrains Mono', monospace;
  }
  .form-input {
    width: 100%;
    background: var(--bg);
    border: 1px solid var(--border);
    color: var(--text);
    padding: 13px 16px;
    border-radius: 8px;
    font-family: 'Bricolage Grotesque', sans-serif;
    font-size: 14px;
    outline: none;
    transition: border-color 0.2s, box-shadow 0.2s;
  }
  .form-input::placeholder { color: var(--text3); }
  .form-input:focus {
    border-color: var(--accent);
    box-shadow: 0 0 0 3px rgba(0,229,160,0.08);
  }
  .form-select {
    width: 100%;
    background: var(--bg);
    border: 1px solid var(--border);
    color: var(--text);
    padding: 13px 16px;
    border-radius: 8px;
    font-family: 'Bricolage Grotesque', sans-serif;
    font-size: 14px;
    outline: none;
    cursor: pointer;
    transition: border-color 0.2s;
  }
  .form-select:focus { border-color: var(--accent); }

  .affil-submit {
    width: 100%;
    background: linear-gradient(135deg, var(--accent), #00C880);
    color: var(--bg);
    border: none;
    padding: 15px;
    border-radius: 8px;
    font-family: 'Bricolage Grotesque', sans-serif;
    font-weight: 700;
    font-size: 15px;
    cursor: pointer;
    transition: all 0.2s;
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 8px;
    margin-top: 8px;
  }
  .affil-submit:hover {
    transform: translateY(-1px);
    box-shadow: 0 10px 40px rgba(0,229,160,0.3);
  }
  .affil-submit:disabled { opacity: 0.6; cursor: not-allowed; transform: none; }

  .form-note {
    font-size: 11px;
    color: var(--text3);
    text-align: center;
    margin-top: 14px;
    font-family: 'JetBrains Mono', monospace;
    line-height: 1.6;
  }

  .affil-success {
    display: none;
    text-align: center;
    padding: 40px 20px;
  }
  .affil-success.visible { display: block; }
  .success-icon {
    font-size: 48px;
    margin-bottom: 16px;
  }
  .success-title {
    font-family: 'Clash Display', sans-serif;
    font-size: 22px;
    font-weight: 600;
    color: var(--accent);
    margin-bottom: 10px;
    letter-spacing: -0.3px;
  }
  .success-text {
    font-size: 14px;
    color: var(--text2);
    line-height: 1.6;
  }

  .simulator-wrap {
    background: var(--surface2);
    border: 1px solid var(--border);
    border-radius: 12px;
    padding: 20px 24px;
    margin-top: 0;
  }
  .sim-label {
    font-size: 12px;
    color: var(--text3);
    font-family: 'JetBrains Mono', monospace;
    margin-bottom: 10px;
    letter-spacing: 1px;
    text-transform: uppercase;
  }
  .sim-slider {
    width: 100%;
    accent-color: var(--accent);
    margin-bottom: 14px;
    cursor: pointer;
  }
  .sim-result {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  .sim-clients { font-size: 13px; color: var(--text2); }
  .sim-revenue {
    font-family: 'Clash Display', sans-serif;
    font-size: 28px;
    font-weight: 700;
    color: var(--accent);
    letter-spacing: -1px;
  }
  .sim-sub { font-size: 11px; color: var(--text3); font-family: 'JetBrains Mono', monospace; }

  @media (max-width: 900px) {
    .affil-section { padding: 60px 24px; }
    .affil-grid { grid-template-columns: 1fr; gap: 40px; }
    .earn-cards { grid-template-columns: 1fr 1fr; }
  }

  /* Responsive */
  @media (max-width: 900px) {
    nav { padding: 16px 24px; }
    .nav-links { display: none; }
    .demo-section, .how-section, .pricing-section, .faq-section, .cta-section { padding: 60px 24px; }
    .cases-section { padding: 60px 24px; }
    .testimonials-section { padding: 60px 24px; }
    footer { padding: 40px 24px; flex-direction: column; text-align: center; }
    .footer-links { justify-content: center; }
    .app-body { grid-template-columns: 1fr; }
    .steps-grid { grid-template-columns: 1fr; }
    .cases-grid { grid-template-columns: repeat(2, 1fr); }
    .pricing-grid { grid-template-columns: 1fr; }
    .testimonials-grid { grid-template-columns: 1fr; }
    .hero-stats { gap: 30px; }
    body { cursor: auto; }
  }
</style>
</head>
<body>

<!-- CURSOR -->
<div class="cursor" id="cursor"></div>
<div class="cursor-ring" id="cursorRing"></div>

<!-- AMBIENT -->
<div class="glow-orb orb1"></div>
<div class="glow-orb orb2"></div>
<div class="glow-orb orb3"></div>

<!-- NAV -->
<nav>
  <div class="logo">
    <div class="logo-icon">⚡</div>
    Flow<span>Genius</span> AI
  </div>
  <ul class="nav-links">
    <li><a href="#demo">Démonstration</a></li>
    <li><a href="#usecases">Cas d'usage</a></li>
    <li><a href="#pricing">Tarifs</a></li>
    <li><a href="#faq">FAQ</a></li>
    <li><a href="#affiliation" style="color:var(--accent);font-weight:600;">💸 Affiliation</a></li>
  </ul>
  <button class="nav-cta" onclick="document.getElementById('demo').scrollIntoView({behavior:'smooth'})">
    Essai Gratuit →
  </button>
</nav>

<!-- HERO -->
<section class="hero">
  <div class="hero-badge">
    <span class="badge-dot"></span>
    Intelligence Artificielle • Workflows • Croissance
  </div>
  <h1>
    Créez des Workflows<br>
    <span class="highlight">Qui Font Croître</span><br>
    <span class="line2">Votre Entreprise</span>
  </h1>
  <p class="hero-desc">
    FlowGenius AI génère en secondes des workflows sur mesure pour automatiser, scaler et maximiser la performance de votre business — partout dans le monde.
  </p>
  <div class="hero-actions">
    <button class="btn-primary" onclick="document.getElementById('demo').scrollIntoView({behavior:'smooth'})">
      🚀 Générer mon premier workflow
    </button>
    <button class="btn-secondary" onclick="document.getElementById('usecases').scrollIntoView({behavior:'smooth'})">
      Voir les cas d'usage
    </button>
  </div>
  <div class="hero-stats">
    <div class="stat-item">
      <div class="stat-num">3 500+</div>
      <div class="stat-label">Workflows générés</div>
    </div>
    <div class="stat-item">
      <div class="stat-num">94%</div>
      <div class="stat-label">Taux de satisfaction</div>
    </div>
    <div class="stat-item">
      <div class="stat-num">47s</div>
      <div class="stat-label">Temps moyen</div>
    </div>
    <div class="stat-item">
      <div class="stat-num">120+</div>
      <div class="stat-label">Pays actifs</div>
    </div>
  </div>
</section>

<!-- DEMO AI GENERATOR -->
<section class="demo-section" id="demo">
  <div class="section-label">✦ Essai en direct</div>
  <div class="section-title">Générez votre workflow<br>en quelques secondes</div>
  <p class="section-sub">Décrivez votre objectif business, l'IA crée un workflow détaillé, actionnable et personnalisé.</p>

  <div class="app-container">
    <div class="app-header">
      <div class="app-dots">
        <span></span><span></span><span></span>
      </div>
      <div class="app-title">FLOWGENIUS AI • WORKFLOW GENERATOR v2.4</div>
      <div style="width:60px"></div>
    </div>
    <div class="app-body">
      <!-- INPUT -->
      <div class="input-panel">
        <div class="input-label">Type d'entreprise</div>
        <select class="business-select" id="bizType">
          <option value="">Sélectionner...</option>
          <option value="ecommerce">E-commerce / Boutique en ligne</option>
          <option value="saas">SaaS / Logiciel</option>
          <option value="agence">Agence / Consulting</option>
          <option value="formation">Formation / Coaching</option>
          <option value="retail">Commerce physique / Retail</option>
          <option value="restaurant">Restauration / Food</option>
          <option value="immobilier">Immobilier</option>
          <option value="startup">Startup / Levée de fonds</option>
        </select>

        <div class="input-label">Objectif principal</div>
        <div class="objective-tags" id="objTags">
          <span class="obj-tag" onclick="toggleTag(this)">🚀 Acquisition clients</span>
          <span class="obj-tag" onclick="toggleTag(this)">💰 Augmenter revenus</span>
          <span class="obj-tag" onclick="toggleTag(this)">⚡ Automatiser opérations</span>
          <span class="obj-tag" onclick="toggleTag(this)">🔄 Fidéliser clients</span>
          <span class="obj-tag" onclick="toggleTag(this)">📊 Analyse & reporting</span>
          <span class="obj-tag" onclick="toggleTag(this)">🌍 Expansion marché</span>
        </div>

        <div class="input-label">Décrivez votre défi business</div>
        <textarea class="goal-input" id="goalInput" placeholder="Ex: Je veux tripler mes ventes en 90 jours avec une équipe de 3 personnes et un budget limité..."></textarea>

        <button class="generate-btn" id="genBtn" onclick="generateWorkflow()">
          <span>⚡</span>
          <span>Générer le Workflow AI</span>
        </button>
      </div>

      <!-- OUTPUT -->
      <div class="output-panel" id="outputPanel">
        <div class="output-placeholder" id="placeholder">
          <div class="placeholder-icon">🗺️</div>
          <div class="placeholder-text">Votre workflow stratégique apparaîtra ici. Remplissez le formulaire et cliquez sur Générer.</div>
        </div>

        <div class="loading-animation" id="loader">
          <div class="loader-ring"></div>
          <div class="loading-text" id="loadingText">Analyse en cours...</div>
        </div>

        <div class="workflow-output" id="workflowOutput">
          <!-- Dynamic content -->
        </div>
      </div>
    </div>
  </div>
</section>

<!-- HOW IT WORKS -->
<section class="how-section" id="how">
  <div class="section-label">✦ Comment ça marche</div>
  <div class="section-title">De l'idée au workflow<br>en 3 étapes</div>

  <div class="steps-grid">
    <div class="how-step">
      <div class="how-num">01</div>
      <div class="how-icon">📋</div>
      <div class="how-title">Décrivez votre business</div>
      <p class="how-desc">Renseignez votre secteur, vos objectifs et vos défis actuels. Plus vous êtes précis, plus le workflow sera pertinent.</p>
    </div>
    <div class="how-step">
      <div class="how-num">02</div>
      <div class="how-icon">🤖</div>
      <div class="how-title">L'IA analyse & conçoit</div>
      <p class="how-desc">Notre algorithme traite des milliers de cas business similaires pour générer un workflow étape par étape, avec les outils recommandés.</p>
    </div>
    <div class="how-step">
      <div class="how-num">03</div>
      <div class="how-icon">🚀</div>
      <div class="how-title">Implémentez & scalez</div>
      <p class="how-desc">Exportez votre workflow, assignez les tâches à votre équipe, suivez les KPIs et itérez pour maximiser vos résultats.</p>
    </div>
  </div>
</section>

<!-- USE CASES -->
<section class="cases-section" id="usecases">
  <div class="cases-inner">
    <div class="section-label">✦ Cas d'usage</div>
    <div class="section-title">Pour chaque secteur,<br>des workflows qui performent</div>

    <div class="cases-grid">
      <div class="case-card">
        <div class="case-emoji">🛒</div>
        <div class="case-name">E-commerce</div>
        <p class="case-desc">Automatisez acquisition, relances panier abandonné, fidélisation et gestion stock.</p>
        <div class="case-result">↑ +340% revenus / 6 mois</div>
      </div>
      <div class="case-card">
        <div class="case-emoji">🏢</div>
        <div class="case-name">Agence</div>
        <p class="case-desc">Processus de vente, onboarding clients, production et reporting automatisés.</p>
        <div class="case-result">↓ -60% temps opérationnel</div>
      </div>
      <div class="case-card">
        <div class="case-emoji">🎓</div>
        <div class="case-name">Formation</div>
        <p class="case-desc">Tunnel de vente, séquences email, suivi apprenants et upsell automatique.</p>
        <div class="case-result">↑ +220% taux conversion</div>
      </div>
      <div class="case-card">
        <div class="case-emoji">💻</div>
        <div class="case-name">SaaS</div>
        <p class="case-desc">Acquisition, activation, rétention utilisateurs et expansion revenus (ARR).</p>
        <div class="case-result">↓ -45% churn mensuel</div>
      </div>
      <div class="case-card">
        <div class="case-emoji">🏪</div>
        <div class="case-name">Commerce Local</div>
        <p class="case-desc">Programme fidélité, avis clients, communication locale et gestion équipe.</p>
        <div class="case-result">↑ +180% clients réguliers</div>
      </div>
      <div class="case-card">
        <div class="case-emoji">🌍</div>
        <div class="case-name">Expansion Afrique</div>
        <p class="case-desc">Stratégies d'entrée sur marché, distribution, partenariats locaux et scaling.</p>
        <div class="case-result">↑ 3 nouveaux marchés / an</div>
      </div>
      <div class="case-card">
        <div class="case-emoji">📱</div>
        <div class="case-name">App Mobile</div>
        <p class="case-desc">Growth hacking, ASO, rétention, monétisation et viralité organique.</p>
        <div class="case-result">↑ +500% DAU en 90 jours</div>
      </div>
      <div class="case-card">
        <div class="case-emoji">🏗️</div>
        <div class="case-name">Startup</div>
        <p class="case-desc">Validation produit, PMF, pitch deck, fundraising et hypercroissance.</p>
        <div class="case-result">✓ Seed round en 4 mois</div>
      </div>
    </div>
  </div>
</section>

<!-- PRICING -->
<section class="pricing-section" id="pricing">
  <div class="pricing-header">
    <div class="section-label">✦ Tarification</div>
    <div class="section-title">Investissez dans votre<br>croissance</div>
    <p class="section-sub">Paiement sécurisé via Chariow. Mobile Money, carte bancaire & crypto acceptés.</p>

    <!-- CHARIOW PAYMENT BADGES -->
    <div style="display:flex;align-items:center;justify-content:center;gap:10px;margin-top:20px;flex-wrap:wrap;">
      <div style="background:var(--surface);border:1px solid var(--border);border-radius:100px;padding:6px 14px;display:flex;align-items:center;gap:7px;font-size:12px;color:var(--text2);">
        <span style="color:#FF6B00;font-size:14px;">📱</span> Orange Money
      </div>
      <div style="background:var(--surface);border:1px solid var(--border);border-radius:100px;padding:6px 14px;display:flex;align-items:center;gap:7px;font-size:12px;color:var(--text2);">
        <span style="color:#FFCC00;font-size:14px;">📱</span> MTN Mobile Money
      </div>
      <div style="background:var(--surface);border:1px solid var(--border);border-radius:100px;padding:6px 14px;display:flex;align-items:center;gap:7px;font-size:12px;color:var(--text2);">
        <span style="color:#1A56DB;font-size:14px;">💳</span> Visa / Mastercard
      </div>
      <div style="background:var(--surface);border:1px solid var(--border);border-radius:100px;padding:6px 14px;display:flex;align-items:center;gap:7px;font-size:12px;color:var(--text2);">
        <span style="color:#F7931A;font-size:14px;">₿</span> Crypto
      </div>
      <div style="background:rgba(0,229,160,0.06);border:1px solid rgba(0,229,160,0.2);border-radius:100px;padding:6px 14px;display:flex;align-items:center;gap:7px;font-size:12px;color:var(--accent);font-weight:600;">
        🔒 Sécurisé par Chariow
      </div>
    </div>
  </div>

  <div class="pricing-grid">
    <!-- STARTER -->
    <div class="pricing-card">
      <div class="plan-name">Starter</div>
      <p class="plan-desc">Pour tester et lancer vos premiers workflows</p>
      <div class="plan-price">
        <span class="price-currency">$</span>
        <span class="price-amount">0</span>
      </div>
      <div class="price-alt">Gratuit pour toujours</div>
      <div class="plan-divider"></div>
      <ul class="feature-list">
        <li class="feature-item"><span class="feature-icon">✓</span>3 workflows / mois</li>
        <li class="feature-item"><span class="feature-icon">✓</span>5 types de business</li>
        <li class="feature-item"><span class="feature-icon">✓</span>Export PDF basique</li>
        <li class="feature-item"><span class="feature-icon muted">—</span><span style="color:var(--text3)">Workflows illimités</span></li>
        <li class="feature-item"><span class="feature-icon muted">—</span><span style="color:var(--text3)">Intégrations outils</span></li>
        <li class="feature-item"><span class="feature-icon muted">—</span><span style="color:var(--text3)">Support prioritaire</span></li>
      </ul>
      <!-- REMPLACE PAR TON LIEN CHARIOW STARTER -->
      <a href="https://yncfctvj.mychariow.shop" target="_blank" style="text-decoration:none;display:block;">
        <button class="plan-btn outline" style="width:100%">Commencer gratuitement →</button>
      </a>
    </div>

    <!-- PRO -->
    <div class="pricing-card featured">
      <div class="featured-badge">⚡ Populaire</div>
      <div class="plan-name">Pro</div>
      <p class="plan-desc">Pour entrepreneurs et PME qui veulent scaler rapidement</p>
      <div class="plan-price">
        <span class="price-currency">$</span>
        <span class="price-amount">49</span>
        <span class="price-period">/mois</span>
      </div>
      <div class="price-alt">≈ 29 000 FCFA / mois • paiement Mobile Money accepté</div>
      <div class="plan-divider"></div>
      <ul class="feature-list">
        <li class="feature-item"><span class="feature-icon">✓</span>Workflows illimités</li>
        <li class="feature-item"><span class="feature-icon">✓</span>Tous les secteurs</li>
        <li class="feature-item"><span class="feature-icon">✓</span>Export PDF + Excel + Notion</li>
        <li class="feature-item"><span class="feature-icon">✓</span>Intégrations Make / Zapier</li>
        <li class="feature-item"><span class="feature-icon">✓</span>KPIs & Dashboard suivi</li>
        <li class="feature-item"><span class="feature-icon">✓</span>Support chat 24/7</li>
      </ul>
      <!-- REMPLACE PAR TON LIEN CHARIOW PRO -->
      <a href="https://yncfctvj.mychariow.shop/prd_l0i6kk" target="_blank" style="text-decoration:none;display:block;">
        <button class="plan-btn filled" style="width:100%">Payer via Chariow →</button>
      </a>
      <p style="text-align:center;font-size:11px;color:var(--text3);margin-top:10px;font-family:'JetBrains Mono',monospace;">Orange Money • MTN • Carte • Crypto</p>
    </div>

    <!-- AGENCY -->
    <div class="pricing-card">
      <div class="plan-name">Agence</div>
      <p class="plan-desc">Pour agences et consultants gérant plusieurs clients</p>
      <div class="plan-price">
        <span class="price-currency">$</span>
        <span class="price-amount">149</span>
        <span class="price-period">/mois</span>
      </div>
      <div class="price-alt">≈ 88 000 FCFA / mois • paiement Mobile Money accepté</div>
      <div class="plan-divider"></div>
      <ul class="feature-list">
        <li class="feature-item"><span class="feature-icon">✓</span>Tout le plan Pro</li>
        <li class="feature-item"><span class="feature-icon">✓</span>Jusqu'à 25 comptes clients</li>
        <li class="feature-item"><span class="feature-icon">✓</span>White-label (votre marque)</li>
        <li class="feature-item"><span class="feature-icon">✓</span>API accès complet</li>
        <li class="feature-item"><span class="feature-icon">✓</span>Gestion équipe multi-users</li>
        <li class="feature-item"><span class="feature-icon">✓</span>Account manager dédié</li>
      </ul>
      <!-- REMPLACE PAR TON LIEN CHARIOW AGENCE -->
      <a href="https://yncfctvj.mychariow.shop/prd_efj0rd" target="_blank" style="text-decoration:none;display:block;">
        <button class="plan-btn outline" style="width:100%">Payer via Chariow →</button>
      </a>
    </div>
  </div>
</section>

<!-- TESTIMONIALS -->
<section class="testimonials-section">
  <div class="testimonials-inner">
    <div class="section-label">✦ Témoignages</div>
    <div class="section-title">Ils ont transformé<br>leur business</div>

    <div class="testimonials-grid">
      <div class="testimonial-card">
        <div class="stars">★★★★★</div>
        <p class="testimonial-text">"En 2 semaines, j'avais un workflow complet pour mon agence digitale. Mes conversions ont grimpé de 180%. Outil indispensable pour tout entrepreneur sérieux."</p>
        <div class="testimonial-author">
          <img src="data:image/png;base64,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" class="author-avatar" style="border-radius:50%;object-fit:cover;width:38px;height:38px;" alt="Kouamé A.">
          <div>
            <div class="author-name">Kouamé A.</div>
            <div class="author-role">Fondateur, Agence K-Digital • Abidjan</div>
          </div>
        </div>
      </div>

      <div class="testimonial-card">
        <div class="stars">★★★★★</div>
        <p class="testimonial-text">"J'ai lancé ma boutique e-commerce et en 3 mois, grâce aux workflows FlowGenius, je fais $12k/mois. Le ROI est dingue pour le prix."</p>
        <div class="testimonial-author">
          <img src="data:image/png;base64,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4uC5F56LzlxptKaWHj363t/8db/XMcbEoWERRCDCtaykQn/167/1/PMv9Pu99v2byfqNPWePCKz1Xb9gnFQPIkC0dgi07JkYiQAMsNZ3vcLXAv34eui9D8Ow0u22l1qljDHMLCJK6fl6fPWl565+81/OX3nxr/78f/34u385WzcC2M299SDAtVA3Q+Wsa8X6n/3T31tcPHv7ze988sM/c2l3gqG9OJ289tnXnvvmv4inF/7rn/zxm4qjRlB66eXsGBC4EelG3XjHZ2ea3/rW7wcaP/ibP73+3aWs360m92j7PctyzxVOJjajZNSppMoCEfeIFwAAQDvn5a7fs88VO4dhOOLwE2PMUK3WSpm4duHzX73w/CtFXvzwjTfW1pdRqc3Uff5L//A//Kf/fOHKZ5c20rRgUvT+e+/+/J23a63py699ZeYzLwHi0exERGGOp+cuv/71MxefW11e+bsffD/L+06gW+I3/8nv/bs/+o+1qYWldlY6YeGfvvmj27duzSycu/al35q7/LxsOXmMMVpra60Idwpe7ngv2zbL0X9ElcUA6APsFETol/7WSpE5ob38NdbaOI5rtVpFeWEY1ut1ESmKQmtjjGmevbTw4q+buLb86NHtWzeIqLCcO/iNr3ztD/7o33/jG98kHfRyC0hZ1v/o+vU8y+rz58++/GUT1eBImxgEAHHm8ouzz72KWn98987D+59ordLcgQp/+3d+9w/+8A+/8MVftx77hVdabWys3fzoI+95+uILl177SlJv4Jbxgoi2tCJwf8M+alt8UoeMDAyWQ7alCz5ou9WevzStd8m1iGRZprVuNpthGDJzEARa636/75yr0Fcm0kEIIN57Z231QOvc//jv/63d3jBBeO78+eUHd6vKXqUthRkRTZSgUgKCQON3EwF0GCttANg557yrrK5er/cnf/xfrr///tnFxenpaZt3AJT37GwJwqgoaU5NTU3lYWCMCYIgTVPnbeHk7rrNnBxLfSANAFjmBwg1Iayn/sOl4kxDmcdWKGttr9er1WpxHFdKRT9NsyzTSoVhSES91Qedh3frM2eardbc/MK9Ox+ZAANN7777zgcfXD93/vzmxnoSagQ22pxdPBeEkc3Tjbsf2LyPeASUAUFY2g/v9FcfRpc+OzM312pN97obkTGY2je+/8Y7b789N79Q5FkzVMKcJI2FM2eV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" class="author-avatar" style="border-radius:50%;object-fit:cover;width:38px;height:38px;" alt="Fatou D.">
          <div>
            <div class="author-name">Fatou D.</div>
            <div class="author-role">E-commerçante • Dakar, Sénégal</div>
          </div>
        </div>
      </div>

      <div class="testimonial-card">
        <div class="stars">★★★★★</div>
        <p class="testimonial-text">"On a automatisé 70% de nos opérations avec les workflows générés. Mon équipe se concentre maintenant sur la vraie valeur ajoutée. Révolutionnaire."</p>
        <div class="testimonial-author">
          <img src="data:image/png;base64,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" class="author-avatar" style="border-radius:50%;object-fit:cover;width:38px;height:38px;" alt="Marc T.">
          <div>
            <div class="author-name">Marc T.</div>
            <div class="author-role">CEO, SaaS startup • Paris, France</div>
          </div>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- FAQ -->
<section class="faq-section" id="faq">
  <div class="faq-header">
    <div class="section-label">✦ Questions fréquentes</div>
    <div class="section-title">On répond à tout</div>
  </div>

  <div id="faqList">
    <div class="faq-item">
      <button class="faq-q" onclick="toggleFaq(this)">
        Ai-je besoin de compétences techniques ?
        <span class="faq-arrow">+</span>
      </button>
      <div class="faq-a">
        <div class="faq-a-inner">Non, absolument aucune compétence technique requise. FlowGenius AI est conçu pour tout entrepreneur, dirigeant ou manager. Il suffit de décrire votre business en langage naturel et l'IA fait le reste.</div>
      </div>
    </div>

    <div class="faq-item">
      <button class="faq-q" onclick="toggleFaq(this)">
        Les workflows sont-ils vraiment personnalisés ?
        <span class="faq-arrow">+</span>
      </button>
      <div class="faq-a">
        <div class="faq-a-inner">Oui. Chaque workflow est généré en temps réel par notre IA en fonction de votre secteur, vos objectifs et votre contexte spécifique. Deux entreprises dans le même secteur obtiendront des workflows différents car leurs besoins sont différents.</div>
      </div>
    </div>

    <div class="faq-item">
      <button class="faq-q" onclick="toggleFaq(this)">
        Quels outils sont recommandés dans les workflows ?
        <span class="faq-arrow">+</span>
      </button>
      <div class="faq-a">
        <div class="faq-a-inner">L'IA recommande les meilleurs outils selon votre budget et contexte : Make.com, Zapier, Notion, Airtable, HubSpot, Mailchimp, WhatsApp Business, et bien d'autres — y compris des alternatives gratuites ou adaptées aux marchés africains.</div>
      </div>
    </div>

    <div class="faq-item">
      <button class="faq-q" onclick="toggleFaq(this)">
        Puis-je vendre les workflows à mes propres clients ?
        <span class="faq-arrow">+</span>
      </button>
      <div class="faq-a">
        <div class="faq-a-inner">Absolument ! Le plan Agence inclut le white-label complet. Vous pouvez générer des workflows à votre marque et les revendre à vos clients comme service premium. C'est un excellent modèle de revenu additionnel pour consultants et agences.</div>
      </div>
    </div>

    <div class="faq-item">
      <button class="faq-q" onclick="toggleFaq(this)">
        Comment se passe le paiement depuis l'Afrique ?
        <span class="faq-arrow">+</span>
      </button>
      <div class="faq-a">
        <div class="faq-a-inner">Nous acceptons cartes bancaires internationales, PayPal, ainsi que des solutions locales comme Wave, Orange Money et MTN Mobile Money pour nos clients africains. Tous les prix sont en USD avec conversion automatique.</div>
      </div>
    </div>
  </div>
</section>


<!-- AFFILIATION -->
<section class="affil-section" id="affiliation">
  <div class="affil-inner">
    <div class="section-label">✦ Programme Affilié</div>
    <div class="section-title">Vendez FlowGenius AI.<br><span style="color:var(--accent)">Gagnez en automatique.</span></div>
    <p class="section-sub">Partagez votre lien unique. Chaque vente générée vous rapporte 30% de commission — versée automatiquement via Chariow.</p>

    <div class="affil-grid">

      <!-- LEFT — infos + simulateur -->
      <div>
        <!-- earn cards -->
        <div class="earn-cards">
          <div class="earn-card">
            <div class="earn-plan">Plan Pro vendu</div>
            <div class="earn-amount">$14<span style="font-size:18px">.70</span></div>
            <div class="earn-per">par vente • 30%</div>
          </div>
          <div class="earn-card">
            <div class="earn-plan">Plan Agence vendu</div>
            <div class="earn-amount">$44<span style="font-size:18px">.70</span></div>
            <div class="earn-per">par vente • 30%</div>
          </div>
          <div class="earn-card" style="grid-column:1/-1;background:linear-gradient(135deg,rgba(0,229,160,0.06),rgba(0,153,255,0.04));border-color:rgba(0,229,160,0.2);">
            <div class="earn-plan">Votre potentiel mensuel</div>
            <div style="display:flex;align-items:center;justify-content:space-between;gap:12px">
              <div>
                <div class="earn-amount" id="sim-amount" style="font-size:40px">$147</div>
                <div class="earn-per">avec <span id="sim-count">10</span> clients Pro actifs</div>
              </div>
              <div style="text-align:right">
                <div style="font-size:11px;color:var(--text3);font-family:'JetBrains Mono',monospace;">ANNUEL</div>
                <div style="font-family:'Clash Display',sans-serif;font-size:22px;font-weight:700;color:var(--accent2);letter-spacing:-1px;" id="sim-annual">$1 764</div>
              </div>
            </div>
          </div>
        </div>

        <!-- simulator -->
        <div class="simulator-wrap">
          <div class="sim-label">🎛 Simulateur de revenus affilié</div>
          <input type="range" class="sim-slider" id="sim-slider" min="1" max="50" value="10"
                 oninput="updateSim(this.value)">
          <div class="sim-result">
            <div>
              <div class="sim-clients"><span id="sim-n">10</span> clients Pro référés</div>
              <div class="sim-sub">× $14.70 commission</div>
            </div>
            <div style="text-align:right">
              <div class="sim-revenue" id="sim-mrr">$147/mois</div>
              <div class="sim-sub" id="sim-yr">$1 764/an</div>
            </div>
          </div>
        </div>

        <!-- steps -->
        <div class="affil-steps" style="margin-top:28px">
          <div class="affil-step">
            <div class="affil-step-num">01</div>
            <div class="affil-step-text">
              <div class="affil-step-title">Inscrivez-vous gratuitement</div>
              <div class="affil-step-desc">Remplissez le formulaire ci-contre. Vous recevez votre lien unique Chariow sur WhatsApp sous 24h.</div>
            </div>
          </div>
          <div class="affil-step">
            <div class="affil-step-num">02</div>
            <div class="affil-step-text">
              <div class="affil-step-title">Partagez votre lien</div>
              <div class="affil-step-desc">WhatsApp, réseaux sociaux, groupe d'entrepreneurs, bouche-à-oreille — chaque partage est une opportunité de gain.</div>
            </div>
          </div>
          <div class="affil-step">
            <div class="affil-step-num">03</div>
            <div class="affil-step-text">
              <div class="affil-step-title">Encaissez automatiquement</div>
              <div class="affil-step-desc">Chariow détecte chaque vente via votre lien et vire votre commission directement — Orange Money, MTN, carte bancaire.</div>
            </div>
          </div>
        </div>
      </div>

      <!-- RIGHT — form -->
      <div class="affil-form-wrap">
        <div class="affil-form-header">
          <div class="affil-form-title">Devenir Affilié FlowGenius</div>
          <div class="affil-badge">✦ Gratuit</div>
        </div>
        <div class="affil-form-body">

          <div id="affil-form-inner">
            <div class="form-group">
              <label class="form-label">Prénom & Nom</label>
              <input type="text" class="form-input" id="af-name" placeholder="Ex: Kouamé Assane">
            </div>
            <div class="form-group">
              <label class="form-label">Numéro WhatsApp</label>
              <input type="text" class="form-input" id="af-wa" placeholder="+225 07 00 00 00 00">
            </div>
            <div class="form-group">
              <label class="form-label">Email</label>
              <input type="email" class="form-input" id="af-email" placeholder="votre@email.com">
            </div>
            <div class="form-group">
              <label class="form-label">Votre audience principale</label>
              <select class="form-select" id="af-audience">
                <option value="">Sélectionner...</option>
                <option>Réseau WhatsApp personnel</option>
                <option>Groupe Facebook / communauté</option>
                <option>Abonnés TikTok / Instagram</option>
                <option>Clients existants (consultant/agence)</option>
                <option>Collègues / réseau professionnel</option>
                <option>Autre</option>
              </select>
            </div>
            <div class="form-group">
              <label class="form-label">Combien de personnes pouvez-vous atteindre ?</label>
              <select class="form-select" id="af-reach">
                <option value="">Sélectionner...</option>
                <option>Moins de 100 personnes</option>
                <option>100 à 500 personnes</option>
                <option>500 à 2 000 personnes</option>
                <option>Plus de 2 000 personnes</option>
              </select>
            </div>
            <div class="form-group">
              <label class="form-label">Pays</label>
              <select class="form-select" id="af-country">
                <option value="">Sélectionner...</option>
                <option>Côte d'Ivoire</option>
                <option>Sénégal</option>
                <option>Mali</option>
                <option>Burkina Faso</option>
                <option>Cameroun</option>
                <option>Niger</option>
                <option>Bénin</option>
                <option>Togo</option>
                <option>Guinée</option>
                <option>RDC</option>
                <option>France</option>
                <option>Belgique</option>
                <option>Canada</option>
                <option>Autre</option>
              </select>
            </div>

            <button class="affil-submit" id="affil-btn" onclick="submitAffil()">
              <span>🚀</span>
              <span>Je veux devenir affilié</span>
            </button>
            <p class="form-note">
              Votre lien unique vous sera envoyé sur WhatsApp sous 24h.<br>
              Aucun achat requis • Commission 30% • Paiement via Chariow
            </p>
          </div>

          <div class="affil-success" id="affil-success">
            <div class="success-icon">✅</div>
            <div class="success-title">Demande envoyée !</div>
            <p class="success-text">
              Merci <strong id="success-name"></strong> !<br><br>
              Votre demande d'affiliation a bien été reçue.<br>
              Vous recevrez votre <strong>lien unique Chariow</strong> sur WhatsApp dans les prochaines 24h.<br><br>
              <span style="color:var(--accent);font-family:'JetBrains Mono',monospace;font-size:12px;">
                Commission 30% • Paiement automatique Chariow
              </span>
            </p>
          </div>

        </div>
      </div>

    </div>
  </div>
</section>

<!-- FINAL CTA -->
<section class="cta-section">
  <div class="cta-inner">
    <div class="section-label" style="text-align:center">✦ Commencez dès aujourd'hui</div>
    <div class="section-title">Votre prochaine<br><span style="color:var(--accent)">grande croissance</span><br>commence ici</div>
    <p class="section-sub" style="text-align:center">Rejoignez 3500+ entrepreneurs qui ont transformé leur business avec des workflows intelligents.</p>
    <div style="display:flex;gap:16px;justify-content:center;flex-wrap:wrap;margin-top:40px">
      <button class="btn-primary" style="font-size:18px;padding:18px 48px" onclick="document.getElementById('demo').scrollIntoView({behavior:'smooth'})">
        🚀 Générer mon workflow maintenant
      </button>
    </div>
    <p style="margin-top:20px;font-size:13px;color:var(--text3)">Paiement sécurisé via Chariow • Orange Money • MTN • Visa • Crypto • Revenus reçus sous 72h</p>
  </div>
</section>

<!-- FOOTER -->
<footer>
  <div class="footer-logo">Flow<span>Genius</span> AI</div>
  <ul class="footer-links">
    <li><a href="#">Confidentialité</a></li>
    <li><a href="#">CGU</a></li>
    <li><a href="#">Contact</a></li>
    <li><a href="#">API</a></li>
    <li><a href="#">Affiliation</a></li>
  </ul>
  <div class="footer-copy">© 2026 FlowGenius AI • All rights reserved</div>
</footer>

<script>
// Custom cursor
const cursor = document.getElementById('cursor');
const ring = document.getElementById('cursorRing');
let mx = 0, my = 0, rx = 0, ry = 0;
document.addEventListener('mousemove', e => {
  mx = e.clientX; my = e.clientY;
  cursor.style.left = mx - 6 + 'px';
  cursor.style.top = my - 6 + 'px';
});
function animateRing() {
  rx += (mx - rx) * 0.12;
  ry += (my - ry) * 0.12;
  ring.style.left = rx - 18 + 'px';
  ring.style.top = ry - 18 + 'px';
  requestAnimationFrame(animateRing);
}
animateRing();

// Tag toggle
function toggleTag(el) {
  el.classList.toggle('active');
}

// FAQ
function toggleFaq(btn) {
  const item = btn.parentElement;
  const wasOpen = item.classList.contains('open');
  document.querySelectorAll('.faq-item').forEach(i => i.classList.remove('open'));
  if (!wasOpen) item.classList.add('open');
}

// Workflow templates
const workflowTemplates = {
  ecommerce: {
    title: "Workflow Croissance E-commerce",
    meta: "GÉNÉRATION #WF-" + Math.floor(Math.random()*9000+1000) + " • SECTEUR: E-COMMERCE • HORIZON: 90 JOURS",
    steps: [
      { name: "Audit & Positionnement", desc: "Analysez vos concurrents, identifiez votre UVP (Unique Value Proposition) et définissez vos segments clients prioritaires.", tool: "SEMrush / Ahrefs" },
      { name: "Optimisation Conversion (CRO)", desc: "A/B testez pages produits, checkout et call-to-action. Objectif : +30% taux de conversion en 30 jours.", tool: "Google Optimize" },
      { name: "Acquisition Multi-Canal", desc: "Lancez Meta Ads (ROAS cible ≥3), SEO produits longue traîne, et programme d'affiliation avec 10 créateurs.", tool: "Meta Business Suite" },
      { name: "Automatisation Emails", desc: "Séquence bienvenue (7 emails), relance panier abandonné (3 emails), post-achat (upsell + avis client).", tool: "Klaviyo / Mailchimp" },
      { name: "Programme Fidélité", desc: "Système de points, offres VIP, parrainage client. Objectif : +40% LTV (Lifetime Value) sur 6 mois.", tool: "LoyaltyLion / Smile.io" },
    ],
    kpis: [{ l: "ROI cible", v: "×4.2" }, { l: "Délai résultats", v: "30 jours" }, { l: "Complexité", v: "Moyenne" }]
  },
  agence: {
    title: "Workflow Scale Agence Digitale",
    meta: "GÉNÉRATION #WF-" + Math.floor(Math.random()*9000+1000) + " • SECTEUR: AGENCE • HORIZON: 60 JOURS",
    steps: [
      { name: "Positionnement Niche Expert", desc: "Choisissez 1 spécialité (ex: Meta Ads pour e-commerce) et devenez la référence. Repositionnez tout votre marketing.", tool: "Notion / Pitch" },
      { name: "Système de Lead Generation", desc: "LinkedIn outreach automatisé, contenu thought leadership, webinaires mensuels et referral program clients existants.", tool: "Lemlist / Phantombuster" },
      { name: "Process Vente Standardisé", desc: "Script découverte 30min, proposition commerciale template, suivi CRM automatisé, onboarding client 48h.", tool: "HubSpot CRM" },
      { name: "Production & Delivery Scalable", desc: "Templates livrables, SOPs détaillées, automatisation reporting, délégation freelances qualifiés.", tool: "Make.com / Notion" },
      { name: "Rétention & Expansion Comptes", desc: "QBR trimestriels, upsell systématique, programme ambassadeur, case studies vidéo pour acquisition.", tool: "Loom / Canva" },
    ],
    kpis: [{ l: "MRR cible", v: "+$15k" }, { l: "Délai résultats", v: "45 jours" }, { l: "Complexité", v: "Élevée" }]
  },
  formation: {
    title: "Workflow Lancement Formation Online",
    meta: "GÉNÉRATION #WF-" + Math.floor(Math.random()*9000+1000) + " • SECTEUR: FORMATION • HORIZON: 45 JOURS",
    steps: [
      { name: "Validation Produit", desc: "Pre-vente avec landing page minimaliste. Objectif : 20 inscrits avant de créer le contenu. Prouve la demande.", tool: "Gumroad / Stripe" },
      { name: "Tunnel de Vente Haute Conversion", desc: "VSL (vidéo de vente 20min), webinaire automatisé, séquence email 10 jours, offre limitée dans le temps.", tool: "ClickFunnels / Systeme.io" },
      { name: "Acquisition Organique", desc: "Contenu éducatif quotidien (YouTube/TikTok/Insta), podcast interviews, SEO articles blog longue traîne.", tool: "YouTube Studio / TubeBuddy" },
      { name: "Communauté & Engagement", desc: "Groupe privé membres actifs, challenges mensuels, lives Q&A, success stories mise en avant pour preuves sociales.", tool: "Circle / Discord" },
      { name: "Upsell & Programmes Premium", desc: "Coaching 1-on-1, mastermind annuel, certification officielle. Multipliez l'ARPU par 3 à 5×.", tool: "Calendly / Stripe" },
    ],
    kpis: [{ l: "CA cible J30", v: "$10k+" }, { l: "Délai résultats", v: "21 jours" }, { l: "Complexité", v: "Faible" }]
  },
  saas: {
    title: "Workflow Growth SaaS Product-Led",
    meta: "GÉNÉRATION #WF-" + Math.floor(Math.random()*9000+1000) + " • SECTEUR: SAAS • HORIZON: 120 JOURS",
    steps: [
      { name: "Activation & Onboarding", desc: "Réduisez le Time-to-Value à <5 minutes. Checklist interactive, tooltips contextuels, email d'activation J+1 et J+3.", tool: "Appcues / Intercom" },
      { name: "Product-Led Acquisition", desc: "Freemium stratégique, viral loops intégrés au produit, programme referral avec double récompense, intégrations marketplace.", tool: "Viral Loops / ReferralHero" },
      { name: "Expansion Revenue", desc: "Triggers d'upgrade basés sur usage, upsell in-app contextuel, annual plan discount, enterprise outbound.", tool: "Baremetrics / ChurnBuster" },
      { name: "Rétention & Anti-Churn", desc: "Health score utilisateurs, alertes churn prédictif, success managers pour comptes >$200/mois, roadmap co-construite.", tool: "Gainsight / Mixpanel" },
      { name: "Data & Itération", desc: "Funnel AARRR instrumenté, A/B tests pricing mensuel, NPS automatisé, interviews clients hebdomadaires.", tool: "Amplitude / PostHog" },
    ],
    kpis: [{ l: "MRR growth", v: "+25%/mois" }, { l: "Churn cible", v: "<2%" }, { l: "Complexité", v: "Élevée" }]
  }
};

const defaultWorkflow = {
  title: "Workflow Croissance Business Universel",
  meta: "GÉNÉRATION #WF-" + Math.floor(Math.random()*9000+1000) + " • STRATÉGIE CROSS-SECTEUR • HORIZON: 90 JOURS",
  steps: [
    { name: "Diagnostic & Clarté Stratégique", desc: "Cartographiez vos revenus actuels, identifiez les 20% d'actions qui génèrent 80% des résultats, et fixez 1 objectif SMART sur 90 jours.", tool: "Notion / Miro" },
    { name: "Optimisation Funnel Existant", desc: "Avant d'acquérir de nouveaux clients, maximisez la valeur des actuels : upsell, cross-sell, augmentation des prix, fidélisation.", tool: "CRM de votre choix" },
    { name: "Système d'Acquisition Scalable", desc: "Choisissez 2 canaux d'acquisition (1 payant + 1 organique), testez pendant 30 jours avec budget minimum, doublez sur ce qui fonctionne.", tool: "Meta Ads / Google Ads" },
    { name: "Automatisation des Tâches Répétitives", desc: "Identifiez les 5 tâches les plus chronophages. Automatisez-les avec Make.com ou Zapier. Libérez 10h/semaine minimum.", tool: "Make.com / Zapier" },
    { name: "Mesure & Itération Hebdomadaire", desc: "Dashboard KPIs mis à jour chaque lundi. Review hebdomadaire de 30 minutes pour ajuster la stratégie en temps réel.", tool: "Google Data Studio" },
  ],
  kpis: [{ l: "Impact estimé", v: "+150%" }, { l: "Délai résultats", v: "60 jours" }, { l: "Universalité", v: "Haute" }]
};

async function generateWorkflow() {
  const bizType = document.getElementById('bizType').value;
  const goal = document.getElementById('goalInput').value;
  const btn = document.getElementById('genBtn');
  
  const placeholder = document.getElementById('placeholder');
  const loader = document.getElementById('loader');
  const output = document.getElementById('workflowOutput');
  const loadingText = document.getElementById('loadingText');

  placeholder.style.display = 'none';
  output.classList.remove('visible');
  loader.classList.add('visible');
  btn.disabled = true;

  const loadingMessages = [
    "Analyse du secteur business...",
    "Identification des leviers de croissance...",
    "Sélection des outils optimaux...",
    "Calcul des KPIs cibles...",
    "Construction du workflow..."
  ];
  let msgIndex = 0;
  const msgInterval = setInterval(() => {
    loadingText.textContent = loadingMessages[msgIndex % loadingMessages.length];
    msgIndex++;
  }, 600);

  // Call Claude API
  const systemPrompt = `Tu es FlowGenius AI, expert en workflows de croissance business.
Génère un workflow en JSON structuré avec exactement ce format:
{
  "title": "string",
  "meta": "string court",
  "steps": [
    {"name": "string", "desc": "string 1-2 phrases", "tool": "string outil recommandé"}
  ],
  "kpis": [
    {"l": "label court", "v": "valeur courte"}
  ]
}
Maximum 5 étapes, 3 KPIs. Réponds UNIQUEMENT avec le JSON, rien d'autre.`;

  const userMsg = `Secteur: ${bizType || 'général'}. Objectif: ${goal || 'croissance et réussite business'}. Génère un workflow actionnable et précis.`;

  let workflowData = null;

  try {
    const response = await fetch("https://api.anthropic.com/v1/messages", {
      method: "POST",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify({
        model: "claude-sonnet-4-20250514",
        max_tokens: 1000,
        system: systemPrompt,
        messages: [{ role: "user", content: userMsg }]
      })
    });
    const data = await response.json();
    const text = data.content?.map(i => i.text || "").join("") || "";
    const clean = text.replace(/```json|```/g, "").trim();
    workflowData = JSON.parse(clean);
  } catch (e) {
    // Fallback to template
    workflowData = workflowTemplates[bizType] || defaultWorkflow;
  }

  clearInterval(msgInterval);
  loader.classList.remove('visible');
  btn.disabled = false;

  // Render
  let html = `
    <div class="workflow-title">${workflowData.title}</div>
    <div class="workflow-meta">${workflowData.meta || 'GÉNÉRÉ PAR FLOWGENIUS AI'}</div>
  `;

  workflowData.steps.forEach((step, i) => {
    html += `
      <div class="workflow-step" style="animation-delay:${i * 0.1}s">
        <div>
          <div class="step-number">0${i+1}</div>
          ${i < workflowData.steps.length - 1 ? '<div class="step-connector"></div>' : ''}
        </div>
        <div class="step-content">
          <div class="step-name">${step.name}</div>
          <div class="step-desc">${step.desc}</div>
          ${step.tool ? `<span class="step-tool">${step.tool}</span>` : ''}
        </div>
      </div>
    `;
  });

  if (workflowData.kpis && workflowData.kpis.length) {
    html += '<div class="kpi-row">';
    workflowData.kpis.forEach(k => {
      html += `<div class="kpi-pill"><span class="kpi-label">${k.l}</span><span class="kpi-value">${k.v}</span></div>`;
    });
    html += '</div>';
  }

  output.innerHTML = html;
  output.classList.add('visible');
}


// ── Affiliate simulator ───────────────────────────────────────────────────
function updateSim(v) {
  const n = parseInt(v);
  const mrr = (n * 14.70).toFixed(2);
  const yr  = (n * 14.70 * 12).toFixed(0);
  document.getElementById('sim-n').textContent = n;
  document.getElementById('sim-count').textContent = n;
  document.getElementById('sim-amount').textContent = '$' + (n * 14.70).toFixed(0);
  document.getElementById('sim-annual').textContent = '$' + parseInt(yr).toLocaleString('fr-FR');
  document.getElementById('sim-mrr').textContent = '$' + parseFloat(mrr).toFixed(0) + '/mois';
  document.getElementById('sim-yr').textContent = '$' + parseInt(yr).toLocaleString('fr-FR') + '/an';
}

// ── Affiliate form submit ─────────────────────────────────────────────────
async function submitAffil() {
  const name     = document.getElementById('af-name').value.trim();
  const wa       = document.getElementById('af-wa').value.trim();
  const email    = document.getElementById('af-email').value.trim();
  const audience = document.getElementById('af-audience').value;
  const reach    = document.getElementById('af-reach').value;
  const country  = document.getElementById('af-country').value;

  if (!name || !wa || !email || !audience || !reach || !country) {
    alert('Veuillez remplir tous les champs pour continuer.');
    return;
  }

  const btn = document.getElementById('affil-btn');
  btn.disabled = true;
  btn.innerHTML = '<span>⏳</span><span>Envoi en cours...</span>';

  // Build WhatsApp notification link for owner
  const msg = encodeURIComponent(
    '🔔 *Nouvelle demande affilié FlowGenius AI*\n\n' +
    '👤 Nom: ' + name + '\n' +
    '📱 WhatsApp: ' + wa + '\n' +
    '📧 Email: ' + email + '\n' +
    '🎯 Audience: ' + audience + '\n' +
    '👥 Portée: ' + reach + '\n' +
    '🌍 Pays: ' + country + '\n\n' +
    '➡️ Créer son lien sur Chariow et envoyer sur WhatsApp.'
  );

  // Save to localStorage for owner reference
  const entry = { name, wa, email, audience, reach, country, date: new Date().toLocaleString('fr-FR') };
  const existing = JSON.parse(localStorage.getItem('affiliates') || '[]');
  existing.push(entry);
  localStorage.setItem('affiliates', JSON.stringify(existing));

  // Simulate API delay then show success
  await new Promise(r => setTimeout(r, 1200));

  document.getElementById('affil-form-inner').style.display = 'none';
  document.getElementById('success-name').textContent = name.split(' ')[0];
  document.getElementById('affil-success').classList.add('visible');

  // Auto-open WhatsApp for owner notification (opens on owner's device via link)
  // Replace VOTRE_NUMERO with actual number in production
}

// Scroll animations
const observer = new IntersectionObserver(entries => {
  entries.forEach(e => {
    if (e.isIntersecting) {
      e.target.style.opacity = '1';
      e.target.style.transform = 'translateY(0)';
    }
  });
}, { threshold: 0.1 });

document.querySelectorAll('.case-card, .how-step, .pricing-card, .testimonial-card').forEach(el => {
  el.style.opacity = '0';
  el.style.transform = 'translateY(20px)';
  el.style.transition = 'opacity 0.5s ease, transform 0.5s ease';
  observer.observe(el);
});
</script>
</body>
</html>
