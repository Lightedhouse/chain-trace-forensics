<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>ChainTrace Forensics — Blockchain Asset Recovery Specialists</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;600;700;800&family=DM+Mono:wght@300;400;500&family=Instrument+Serif:ital@0;1&display=swap" rel="stylesheet">
<style>
  :root {
    --bg: #050810;
    --surface: #0a0f1e;
    --surface2: #0f1628;
    --border: rgba(0,200,255,0.12);
    --accent: #00c8ff;
    --accent2: #00ff88;
    --accent3: #ff6b35;
    --text: #e8edf5;
    --muted: #6b7a99;
    --danger: #ff3b5c;
    --glow: 0 0 40px rgba(0,200,255,0.15);
  }

  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  html { scroll-behavior: smooth; }

  body {
    font-family: 'DM Mono', monospace;
    background: var(--bg);
    color: var(--text);
    overflow-x: hidden;
    cursor: none;
  }

  /* CUSTOM CURSOR */
  .cursor {
    width: 12px; height: 12px;
    background: var(--accent);
    border-radius: 50%;
    position: fixed; z-index: 9999;
    pointer-events: none;
    transform: translate(-50%, -50%);
    transition: transform 0.1s, width 0.2s, height 0.2s;
    mix-blend-mode: screen;
  }
  .cursor-ring {
    width: 36px; height: 36px;
    border: 1px solid rgba(0,200,255,0.5);
    border-radius: 50%;
    position: fixed; z-index: 9998;
    pointer-events: none;
    transform: translate(-50%, -50%);
    transition: transform 0.18s ease, width 0.2s, height 0.2s;
  }

  /* SCANLINES OVERLAY */
  body::before {
    content: '';
    position: fixed; inset: 0; z-index: 9990;
    background: repeating-linear-gradient(0deg, transparent, transparent 2px, rgba(0,0,0,0.03) 2px, rgba(0,0,0,0.03) 4px);
    pointer-events: none;
  }

  /* NAV */
  nav {
    position: fixed; top: 0; left: 0; right: 0; z-index: 1000;
    display: flex; align-items: center; justify-content: space-between;
    padding: 0 48px;
    height: 72px;
    background: rgba(5,8,16,0.85);
    backdrop-filter: blur(20px);
    border-bottom: 1px solid var(--border);
  }

  .nav-logo {
    display: flex; align-items: center; gap: 12px;
    text-decoration: none;
  }
  .logo-icon {
    width: 36px; height: 36px;
    background: linear-gradient(135deg, var(--accent), var(--accent2));
    clip-path: polygon(50% 0%, 100% 25%, 100% 75%, 50% 100%, 0% 75%, 0% 25%);
    display: flex; align-items: center; justify-content: center;
    animation: logoPulse 3s ease-in-out infinite;
  }
  @keyframes logoPulse { 0%,100%{filter:brightness(1)} 50%{filter:brightness(1.4)} }

  .logo-text {
    font-family: 'Syne', sans-serif;
    font-weight: 800;
    font-size: 18px;
    color: var(--text);
    letter-spacing: -0.5px;
  }
  .logo-text span { color: var(--accent); }

  .nav-links {
    display: flex; gap: 36px; list-style: none;
  }
  .nav-links a {
    color: var(--muted);
    text-decoration: none;
    font-size: 11px;
    letter-spacing: 2px;
    text-transform: uppercase;
    transition: color 0.2s;
  }
  .nav-links a:hover { color: var(--accent); }

  .nav-cta {
    background: transparent;
    border: 1px solid var(--accent);
    color: var(--accent);
    font-family: 'DM Mono', monospace;
    font-size: 11px;
    letter-spacing: 2px;
    text-transform: uppercase;
    padding: 10px 24px;
    cursor: none;
    transition: all 0.2s;
    text-decoration: none;
  }
  .nav-cta:hover {
    background: var(--accent);
    color: var(--bg);
    box-shadow: 0 0 24px rgba(0,200,255,0.4);
  }

  /* HERO */
  .hero {
    min-height: 100vh;
    display: flex; flex-direction: column; justify-content: center;
    padding: 120px 48px 80px;
    position: relative;
    overflow: hidden;
  }

  .hero-grid {
    position: absolute; inset: 0;
    background-image:
      linear-gradient(rgba(0,200,255,0.04) 1px, transparent 1px),
      linear-gradient(90deg, rgba(0,200,255,0.04) 1px, transparent 1px);
    background-size: 80px 80px;
    animation: gridDrift 20s linear infinite;
  }
  @keyframes gridDrift { to { transform: translateY(80px); } }

  .hero-glow {
    position: absolute;
    top: -200px; left: 50%; transform: translateX(-50%);
    width: 900px; height: 600px;
    background: radial-gradient(ellipse, rgba(0,200,255,0.08) 0%, transparent 70%);
    pointer-events: none;
  }

  .hero-badge {
    display: inline-flex; align-items: center; gap: 8px;
    border: 1px solid rgba(0,255,136,0.3);
    background: rgba(0,255,136,0.05);
    padding: 6px 16px;
    font-size: 10px;
    letter-spacing: 3px;
    text-transform: uppercase;
    color: var(--accent2);
    margin-bottom: 40px;
    width: fit-content;
  }
  .badge-dot {
    width: 6px; height: 6px;
    background: var(--accent2);
    border-radius: 50%;
    animation: blink 1.5s ease-in-out infinite;
  }
  @keyframes blink { 0%,100%{opacity:1} 50%{opacity:0.2} }

  .hero h1 {
    font-family: 'Syne', sans-serif;
    font-weight: 800;
    font-size: clamp(42px, 6vw, 90px);
    line-height: 0.95;
    letter-spacing: -3px;
    margin-bottom: 32px;
    max-width: 900px;
  }
  .hero h1 em {
    font-style: normal;
    color: var(--accent);
    position: relative;
  }
  .hero h1 .serif {
    font-family: 'Instrument Serif', serif;
    font-style: italic;
    color: var(--muted);
  }

  .hero-sub {
    font-size: 14px;
    line-height: 1.8;
    color: var(--muted);
    max-width: 560px;
    margin-bottom: 52px;
    letter-spacing: 0.3px;
  }

  .hero-actions {
    display: flex; gap: 16px; align-items: center; flex-wrap: wrap;
    margin-bottom: 80px;
  }

  .btn-primary {
    background: var(--accent);
    color: var(--bg);
    border: none;
    font-family: 'DM Mono', monospace;
    font-size: 11px;
    letter-spacing: 2px;
    text-transform: uppercase;
    padding: 16px 36px;
    cursor: none;
    text-decoration: none;
    font-weight: 500;
    transition: all 0.2s;
    position: relative;
    overflow: hidden;
  }
  .btn-primary::after {
    content: '';
    position: absolute; inset: 0;
    background: linear-gradient(90deg, transparent, rgba(255,255,255,0.2), transparent);
    transform: translateX(-100%);
    transition: transform 0.4s;
  }
  .btn-primary:hover::after { transform: translateX(100%); }
  .btn-primary:hover { box-shadow: 0 0 40px rgba(0,200,255,0.5); }

  .btn-ghost {
    background: transparent;
    color: var(--text);
    border: 1px solid var(--border);
    font-family: 'DM Mono', monospace;
    font-size: 11px;
    letter-spacing: 2px;
    text-transform: uppercase;
    padding: 16px 36px;
    cursor: none;
    text-decoration: none;
    transition: all 0.2s;
  }
  .btn-ghost:hover { border-color: var(--accent); color: var(--accent); }

  .hero-stats {
    display: flex; gap: 64px;
    padding-top: 48px;
    border-top: 1px solid var(--border);
  }
  .stat-item {}
  .stat-num {
    font-family: 'Syne', sans-serif;
    font-size: 36px;
    font-weight: 800;
    color: var(--accent);
    letter-spacing: -1px;
    line-height: 1;
  }
  .stat-label {
    font-size: 10px;
    letter-spacing: 2px;
    text-transform: uppercase;
    color: var(--muted);
    margin-top: 6px;
  }

  /* TICKER */
  .ticker-wrap {
    background: var(--surface);
    border-top: 1px solid var(--border);
    border-bottom: 1px solid var(--border);
    overflow: hidden;
    padding: 14px 0;
  }
  .ticker-track {
    display: flex; gap: 0;
    animation: ticker 30s linear infinite;
    white-space: nowrap;
  }
  @keyframes ticker { to { transform: translateX(-50%); } }
  .ticker-item {
    display: inline-flex; align-items: center; gap: 8px;
    padding: 0 32px;
    font-size: 11px;
    letter-spacing: 1px;
    color: var(--muted);
    border-right: 1px solid var(--border);
  }
  .ticker-item .up { color: var(--accent2); }
  .ticker-coin { color: var(--accent); font-weight: 500; }

  /* SECTION BASE */
  section { padding: 120px 48px; }

  .section-label {
    font-size: 10px;
    letter-spacing: 4px;
    text-transform: uppercase;
    color: var(--accent);
    margin-bottom: 20px;
  }
  .section-title {
    font-family: 'Syne', sans-serif;
    font-weight: 800;
    font-size: clamp(32px, 4vw, 56px);
    letter-spacing: -2px;
    line-height: 1.05;
    margin-bottom: 20px;
  }
  .section-sub {
    font-size: 13px;
    line-height: 1.8;
    color: var(--muted);
    max-width: 520px;
  }

  /* SERVICES */
  .services { background: var(--surface); }

  .services-header {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 64px;
    align-items: end;
    margin-bottom: 72px;
  }

  .services-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 1px;
    background: var(--border);
    border: 1px solid var(--border);
  }

  .service-card {
    background: var(--surface2);
    padding: 48px 36px;
    position: relative;
    overflow: hidden;
    transition: all 0.3s;
    cursor: none;
  }
  .service-card::before {
    content: '';
    position: absolute;
    top: 0; left: 0; right: 0;
    height: 2px;
    background: linear-gradient(90deg, var(--accent), var(--accent2));
    transform: scaleX(0);
    transform-origin: left;
    transition: transform 0.4s;
  }
  .service-card:hover::before { transform: scaleX(1); }
  .service-card:hover { background: #111827; }

  .service-num {
    font-size: 10px;
    letter-spacing: 3px;
    color: var(--accent);
    margin-bottom: 24px;
  }
  .service-icon {
    font-size: 32px;
    margin-bottom: 20px;
    display: block;
  }
  .service-title {
    font-family: 'Syne', sans-serif;
    font-weight: 700;
    font-size: 20px;
    margin-bottom: 16px;
    letter-spacing: -0.5px;
  }
  .service-desc {
    font-size: 12px;
    line-height: 1.8;
    color: var(--muted);
    margin-bottom: 28px;
  }
  .service-tags {
    display: flex; flex-wrap: wrap; gap: 8px;
  }
  .tag {
    font-size: 9px;
    letter-spacing: 1.5px;
    text-transform: uppercase;
    color: var(--accent);
    border: 1px solid rgba(0,200,255,0.2);
    padding: 4px 10px;
    background: rgba(0,200,255,0.05);
  }

  /* PROCESS */
  .process { background: var(--bg); }

  .process-steps {
    display: grid;
    grid-template-columns: repeat(7, 1fr);
    gap: 0;
    margin-top: 72px;
    position: relative;
  }
  .process-steps::before {
    content: '';
    position: absolute;
    top: 28px; left: 7%; right: 7%;
    height: 1px;
    background: linear-gradient(90deg, var(--accent), var(--accent2), var(--accent));
    z-index: 0;
  }

  .step {
    display: flex; flex-direction: column; align-items: center;
    text-align: center;
    padding: 0 12px;
    position: relative; z-index: 1;
  }
  .step-num {
    width: 56px; height: 56px;
    border: 1px solid var(--accent);
    background: var(--bg);
    display: flex; align-items: center; justify-content: center;
    font-family: 'Syne', sans-serif;
    font-weight: 800;
    font-size: 18px;
    color: var(--accent);
    margin-bottom: 20px;
    clip-path: polygon(50% 0%, 100% 25%, 100% 75%, 50% 100%, 0% 75%, 0% 25%);
    transition: all 0.3s;
  }
  .step:hover .step-num {
    background: var(--accent);
    color: var(--bg);
    box-shadow: 0 0 30px rgba(0,200,255,0.5);
  }
  .step-title {
    font-family: 'Syne', sans-serif;
    font-weight: 700;
    font-size: 13px;
    margin-bottom: 8px;
    letter-spacing: -0.3px;
  }
  .step-desc {
    font-size: 10px;
    line-height: 1.6;
    color: var(--muted);
    letter-spacing: 0.3px;
  }

  /* WHY US */
  .why { background: var(--surface); }

  .why-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 80px;
    align-items: center;
    margin-top: 72px;
  }

  .why-left {}
  .why-features {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 1px;
    background: var(--border);
    border: 1px solid var(--border);
    margin-top: 48px;
  }
  .why-feature {
    background: var(--surface2);
    padding: 32px 28px;
    transition: background 0.2s;
  }
  .why-feature:hover { background: #111827; }
  .feature-icon { font-size: 24px; margin-bottom: 14px; }
  .feature-title {
    font-family: 'Syne', sans-serif;
    font-weight: 700;
    font-size: 15px;
    margin-bottom: 8px;
  }
  .feature-desc { font-size: 11px; line-height: 1.7; color: var(--muted); }

  .why-right {
    position: relative;
  }
  .stats-block {
    border: 1px solid var(--border);
    background: var(--surface2);
    padding: 48px;
  }
  .stats-block-title {
    font-family: 'Syne', sans-serif;
    font-size: 13px;
    letter-spacing: 1px;
    color: var(--muted);
    margin-bottom: 36px;
    text-transform: uppercase;
  }
  .big-stat {
    margin-bottom: 36px;
    padding-bottom: 36px;
    border-bottom: 1px solid var(--border);
  }
  .big-stat:last-child { border: none; margin-bottom: 0; padding-bottom: 0; }
  .big-num {
    font-family: 'Syne', sans-serif;
    font-size: 52px;
    font-weight: 800;
    letter-spacing: -2px;
    color: var(--accent);
    line-height: 1;
  }
  .big-label {
    font-size: 11px;
    letter-spacing: 2px;
    text-transform: uppercase;
    color: var(--muted);
    margin-top: 8px;
  }
  .progress-bar {
    height: 2px;
    background: var(--border);
    margin-top: 12px;
    position: relative;
    overflow: hidden;
  }
  .progress-fill {
    height: 100%;
    background: linear-gradient(90deg, var(--accent), var(--accent2));
    animation: fillBar 2s ease-out forwards;
  }
  @keyframes fillBar { from { width: 0; } }

  /* TESTIMONIALS */
  .testimonials { background: var(--bg); }

  .testi-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 1px;
    background: var(--border);
    border: 1px solid var(--border);
    margin-top: 72px;
  }
  .testi-card {
    background: var(--surface);
    padding: 40px 36px;
    position: relative;
    transition: background 0.2s;
  }
  .testi-card:hover { background: var(--surface2); }
  .testi-quote {
    font-family: 'Instrument Serif', serif;
    font-style: italic;
    font-size: 17px;
    line-height: 1.6;
    color: var(--text);
    margin-bottom: 28px;
    opacity: 0.9;
  }
  .testi-meta { display: flex; align-items: center; gap: 14px; }
  .testi-avatar {
    width: 42px; height: 42px;
    background: linear-gradient(135deg, var(--accent), var(--accent2));
    display: flex; align-items: center; justify-content: center;
    font-family: 'Syne', sans-serif;
    font-weight: 800;
    font-size: 13px;
    color: var(--bg);
    flex-shrink: 0;
  }
  .testi-name {
    font-family: 'Syne', sans-serif;
    font-weight: 700;
    font-size: 14px;
    margin-bottom: 2px;
  }
  .testi-loc { font-size: 10px; color: var(--muted); letter-spacing: 1px; }
  .testi-amount {
    position: absolute;
    top: 28px; right: 28px;
    font-size: 11px;
    color: var(--accent2);
    letter-spacing: 1px;
    border: 1px solid rgba(0,255,136,0.2);
    background: rgba(0,255,136,0.05);
    padding: 4px 10px;
  }

  /* CASE SUBMISSION */
  .case-submit { background: var(--surface); }

  .case-grid {
    display: grid;
    grid-template-columns: 1fr 480px;
    gap: 80px;
    margin-top: 72px;
  }

  .case-info {}
  .case-info h3 {
    font-family: 'Syne', sans-serif;
    font-size: 20px;
    font-weight: 700;
    margin-bottom: 16px;
  }
  .case-info p { font-size: 12px; line-height: 1.8; color: var(--muted); margin-bottom: 32px; }

  .info-items { display: flex; flex-direction: column; gap: 16px; }
  .info-item {
    display: flex; align-items: center; gap: 16px;
    padding: 16px 20px;
    border: 1px solid var(--border);
    background: var(--surface2);
  }
  .info-item-icon { font-size: 20px; flex-shrink: 0; }
  .info-item-text { font-size: 12px; color: var(--muted); }
  .info-item-label { font-family: 'Syne', sans-serif; font-size: 13px; color: var(--text); margin-bottom: 2px; }

  .case-form {}
  .form-group { margin-bottom: 20px; }
  .form-row { display: grid; grid-template-columns: 1fr 1fr; gap: 16px; }
  .form-label {
    display: block;
    font-size: 9px;
    letter-spacing: 2px;
    text-transform: uppercase;
    color: var(--muted);
    margin-bottom: 8px;
  }
  .form-input, .form-select, .form-textarea {
    width: 100%;
    background: var(--surface2);
    border: 1px solid var(--border);
    color: var(--text);
    font-family: 'DM Mono', monospace;
    font-size: 12px;
    padding: 14px 16px;
    outline: none;
    transition: border-color 0.2s;
    -webkit-appearance: none;
    appearance: none;
  }
  .form-input:focus, .form-select:focus, .form-textarea:focus {
    border-color: var(--accent);
    box-shadow: 0 0 0 1px var(--accent), inset 0 0 16px rgba(0,200,255,0.04);
  }
  .form-textarea { min-height: 120px; resize: vertical; }
  .form-select { cursor: none; }
  option { background: var(--surface2); }

  .form-check { display: flex; align-items: flex-start; gap: 12px; margin-bottom: 24px; }
  .form-check input[type="checkbox"] { margin-top: 2px; accent-color: var(--accent); flex-shrink: 0; }
  .form-check label { font-size: 10px; color: var(--muted); line-height: 1.6; }

  .btn-submit {
    width: 100%;
    background: var(--accent);
    color: var(--bg);
    border: none;
    font-family: 'DM Mono', monospace;
    font-size: 11px;
    letter-spacing: 2px;
    text-transform: uppercase;
    padding: 18px;
    cursor: none;
    font-weight: 500;
    transition: all 0.3s;
    position: relative;
    overflow: hidden;
  }
  .btn-submit:hover { box-shadow: 0 0 50px rgba(0,200,255,0.4); background: #19d6ff; }

  /* CTA BAND */
  .cta-band {
    background: var(--bg);
    padding: 80px 48px;
    border-top: 1px solid var(--border);
    border-bottom: 1px solid var(--border);
    text-align: center;
    position: relative;
    overflow: hidden;
  }
  .cta-band::before {
    content: '';
    position: absolute; inset: 0;
    background: radial-gradient(ellipse at center, rgba(0,200,255,0.06) 0%, transparent 70%);
  }
  .cta-band h2 {
    font-family: 'Syne', sans-serif;
    font-size: clamp(28px, 4vw, 52px);
    font-weight: 800;
    letter-spacing: -2px;
    margin-bottom: 16px;
    position: relative;
  }
  .cta-band p { font-size: 13px; color: var(--muted); margin-bottom: 40px; position: relative; }
  .cta-actions { display: flex; gap: 16px; justify-content: center; flex-wrap: wrap; position: relative; }

  /* SAFETY TIPS */
  .safety { background: var(--surface); }
  .safety-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 1px;
    background: var(--border);
    border: 1px solid var(--border);
    margin-top: 72px;
  }
  .safety-card {
    background: var(--surface2);
    padding: 40px 32px;
    transition: background 0.2s;
  }
  .safety-card:hover { background: #111827; }
  .safety-num {
    font-family: 'Syne', sans-serif;
    font-size: 48px;
    font-weight: 800;
    color: rgba(0,200,255,0.12);
    line-height: 1;
    margin-bottom: 16px;
    letter-spacing: -2px;
  }
  .safety-title {
    font-family: 'Syne', sans-serif;
    font-weight: 700;
    font-size: 16px;
    margin-bottom: 12px;
  }
  .safety-desc { font-size: 11px; line-height: 1.7; color: var(--muted); }

  .warning-box {
    border: 1px solid rgba(255,59,92,0.3);
    background: rgba(255,59,92,0.04);
    padding: 32px 36px;
    margin-bottom: 48px;
    display: flex; gap: 20px; align-items: flex-start;
  }
  .warning-icon { font-size: 24px; flex-shrink: 0; margin-top: 2px; }
  .warning-title {
    font-family: 'Syne', sans-serif;
    font-weight: 700;
    font-size: 15px;
    color: var(--danger);
    margin-bottom: 8px;
  }
  .warning-text { font-size: 12px; line-height: 1.7; color: var(--muted); }

  /* FOOTER */
  footer {
    background: var(--surface);
    border-top: 1px solid var(--border);
    padding: 72px 48px 40px;
  }
  .footer-top {
    display: grid;
    grid-template-columns: 1.5fr 1fr 1fr 1fr;
    gap: 64px;
    margin-bottom: 56px;
    padding-bottom: 56px;
    border-bottom: 1px solid var(--border);
  }
  .footer-brand-desc {
    font-size: 12px;
    line-height: 1.8;
    color: var(--muted);
    margin-top: 20px;
    margin-bottom: 28px;
  }
  .footer-social { display: flex; gap: 12px; }
  .social-link {
    width: 36px; height: 36px;
    border: 1px solid var(--border);
    display: flex; align-items: center; justify-content: center;
    text-decoration: none;
    font-size: 14px;
    transition: all 0.2s;
  }
  .social-link:hover { border-color: var(--accent); color: var(--accent); }

  .footer-col h4 {
    font-family: 'Syne', sans-serif;
    font-size: 12px;
    font-weight: 700;
    letter-spacing: 2px;
    text-transform: uppercase;
    color: var(--text);
    margin-bottom: 20px;
  }
  .footer-links { list-style: none; }
  .footer-links li { margin-bottom: 12px; }
  .footer-links a {
    text-decoration: none;
    font-size: 12px;
    color: var(--muted);
    transition: color 0.2s;
    letter-spacing: 0.3px;
  }
  .footer-links a:hover { color: var(--accent); }

  .footer-contact-item {
    display: flex; align-items: center; gap: 10px;
    font-size: 12px;
    color: var(--muted);
    margin-bottom: 14px;
  }
  .contact-icon { font-size: 14px; color: var(--accent); }

  .footer-bottom {
    display: flex; justify-content: space-between; align-items: center;
    flex-wrap: wrap; gap: 16px;
  }
  .footer-copy { font-size: 11px; color: var(--muted); letter-spacing: 0.5px; }
  .footer-legal { display: flex; gap: 24px; }
  .footer-legal a {
    font-size: 11px;
    color: var(--muted);
    text-decoration: none;
    letter-spacing: 0.5px;
    transition: color 0.2s;
  }
  .footer-legal a:hover { color: var(--accent); }

  /* SCROLLBAR */
  ::-webkit-scrollbar { width: 4px; }
  ::-webkit-scrollbar-track { background: var(--bg); }
  ::-webkit-scrollbar-thumb { background: var(--accent); border-radius: 2px; }

  /* MOBILE */
  @media (max-width: 900px) {
    nav { padding: 0 24px; }
    .nav-links { display: none; }
    section { padding: 80px 24px; }
    .hero { padding: 100px 24px 64px; }
    .hero-stats { gap: 32px; flex-wrap: wrap; }
    .services-header { grid-template-columns: 1fr; gap: 24px; }
    .services-grid { grid-template-columns: 1fr; }
    .process-steps { grid-template-columns: repeat(3, 1fr); gap: 32px; }
    .process-steps::before { display: none; }
    .why-grid { grid-template-columns: 1fr; gap: 48px; }
    .testi-grid { grid-template-columns: 1fr; }
    .case-grid { grid-template-columns: 1fr; gap: 48px; }
    .safety-grid { grid-template-columns: 1fr; }
    .footer-top { grid-template-columns: 1fr 1fr; gap: 40px; }
    .form-row { grid-template-columns: 1fr; }
  }

  /* ANIMATIONS */
  .fade-up {
    opacity: 0;
    transform: translateY(30px);
    transition: opacity 0.6s ease, transform 0.6s ease;
  }
  .fade-up.visible {
    opacity: 1;
    transform: translateY(0);
  }
</style>
</head>
<body>

<!-- Custom Cursor -->
<div class="cursor" id="cursor"></div>
<div class="cursor-ring" id="cursorRing"></div>

<!-- NAV -->
<nav>
  <a href="#" class="nav-logo">
    <div class="logo-icon">
      <svg width="18" height="18" viewBox="0 0 18 18" fill="none">
        <path d="M9 2L15 5.5V12.5L9 16L3 12.5V5.5L9 2Z" stroke="#050810" stroke-width="1.5" fill="none"/>
        <circle cx="9" cy="9" r="2" fill="#050810"/>
      </svg>
    </div>
    <span class="logo-text">Chain<span>Trace</span> Forensics</span>
  </a>
  <ul class="nav-links">
    <li><a href="#services">Services</a></li>
    <li><a href="#process">Process</a></li>
    <li><a href="#testimonials">Cases</a></li>
    <li><a href="#safety">Safety</a></li>
    <li><a href="#about">About</a></li>
  </ul>
  <a href="#submit" class="nav-cta">Start Recovery</a>
</nav>

<!-- HERO -->
<section class="hero" id="home">
  <div class="hero-grid"></div>
  <div class="hero-glow"></div>

  <div class="hero-badge">
    <span class="badge-dot"></span>
    Certified Blockchain Forensics · Legal-Grade Evidence
  </div>

  <h1>
    Recover Your<br>
    <em>Stolen Crypto</em><br>
    <span class="serif">with Precision.</span>
  </h1>

  <p class="hero-sub">
    ChainTrace Forensics deploys advanced blockchain intelligence and certified analysts to trace stolen digital assets across every major chain — building court-ready evidence and coordinating global recovery.
  </p>

  <div class="hero-actions">
    <a href="#submit" class="btn-primary">Start Recovery Case</a>
    <a href="#process" class="btn-ghost">View Our Process</a>
  </div>

  <div class="hero-stats">
    <div class="stat-item">
      <div class="stat-num" data-count="50">$50M+</div>
      <div class="stat-label">Assets Traced</div>
    </div>
    <div class="stat-item">
      <div class="stat-num">500+</div>
      <div class="stat-label">Cases Resolved</div>
    </div>
    <div class="stat-item">
      <div class="stat-num">45+</div>
      <div class="stat-label">Countries Served</div>
    </div>
    <div class="stat-item">
      <div class="stat-num">24/7</div>
      <div class="stat-label">Case Support</div>
    </div>
  </div>
</section>

<!-- TICKER -->
<div class="ticker-wrap">
  <div class="ticker-track" id="ticker">
    <span class="ticker-item"><span class="ticker-coin">BTC</span> Bitcoin <span class="up">Active Tracing ↑</span></span>
    <span class="ticker-item"><span class="ticker-coin">ETH</span> Ethereum <span class="up">Active Tracing ↑</span></span>
    <span class="ticker-item"><span class="ticker-coin">USDT</span> Tether <span class="up">Monitored</span></span>
    <span class="ticker-item"><span class="ticker-coin">SOL</span> Solana <span class="up">Active Tracing ↑</span></span>
    <span class="ticker-item"><span class="ticker-coin">XRP</span> Ripple <span class="up">Monitored</span></span>
    <span class="ticker-item"><span class="ticker-coin">BNB</span> BNB Chain <span class="up">Active Tracing ↑</span></span>
    <span class="ticker-item"><span class="ticker-coin">ADA</span> Cardano <span class="up">Monitored</span></span>
    <span class="ticker-item"><span class="ticker-coin">MATIC</span> Polygon <span class="up">Active Tracing ↑</span></span>
    <!-- duplicate for loop -->
    <span class="ticker-item"><span class="ticker-coin">BTC</span> Bitcoin <span class="up">Active Tracing ↑</span></span>
    <span class="ticker-item"><span class="ticker-coin">ETH</span> Ethereum <span class="up">Active Tracing ↑</span></span>
    <span class="ticker-item"><span class="ticker-coin">USDT</span> Tether <span class="up">Monitored</span></span>
    <span class="ticker-item"><span class="ticker-coin">SOL</span> Solana <span class="up">Active Tracing ↑</span></span>
    <span class="ticker-item"><span class="ticker-coin">XRP</span> Ripple <span class="up">Monitored</span></span>
    <span class="ticker-item"><span class="ticker-coin">BNB</span> BNB Chain <span class="up">Active Tracing ↑</span></span>
    <span class="ticker-item"><span class="ticker-coin">ADA</span> Cardano <span class="up">Monitored</span></span>
    <span class="ticker-item"><span class="ticker-coin">MATIC</span> Polygon <span class="up">Active Tracing ↑</span></span>
  </div>
</div>

<!-- SERVICES -->
<section class="services" id="services">
  <div class="services-header">
    <div>
      <div class="section-label">// Core Services</div>
      <h2 class="section-title">Comprehensive<br>Recovery Solutions</h2>
    </div>
    <p class="section-sub">
      From initial blockchain tracing to court-ready forensic reports and exchange coordination — we cover every angle of crypto asset recovery.
    </p>
  </div>

  <div class="services-grid">
    <div class="service-card fade-up">
      <div class="service-num">01</div>
      <span class="service-icon">🔍</span>
      <div class="service-title">Crypto Asset Tracing</div>
      <p class="service-desc">Advanced blockchain analysis tracking stolen funds across multiple chains, wallets, and mixing services. We identify destination addresses and transaction patterns with 87% fund identification rate.</p>
      <div class="service-tags">
        <span class="tag">Graph Analysis</span>
        <span class="tag">Multi-Chain</span>
        <span class="tag">AI Detection</span>
      </div>
    </div>

    <div class="service-card fade-up">
      <div class="service-num">02</div>
      <span class="service-icon">🕵️</span>
      <div class="service-title">Fraud Investigation</div>
      <p class="service-desc">Deep-dive investigations into crypto scams, phishing attacks, and fraudulent schemes. We uncover perpetrator identities across romance scams, rug pulls, Ponzi schemes, and exchange fraud.</p>
      <div class="service-tags">
        <span class="tag">OSINT</span>
        <span class="tag">Dark Web</span>
        <span class="tag">Scammer ID</span>
      </div>
    </div>

    <div class="service-card fade-up">
      <div class="service-num">03</div>
      <span class="service-icon">📄</span>
      <div class="service-title">Forensic Evidence Reports</div>
      <p class="service-desc">Court-ready blockchain forensic reports with detailed transaction flows, entity analysis, and investigative conclusions. Used in 200+ legal proceedings across 50+ jurisdictions worldwide.</p>
      <div class="service-tags">
        <span class="tag">Court-Ready</span>
        <span class="tag">Certified</span>
        <span class="tag">Chain of Custody</span>
      </div>
    </div>

    <div class="service-card fade-up">
      <div class="service-num">04</div>
      <span class="service-icon">🏦</span>
      <div class="service-title">Exchange Liaison</div>
      <p class="service-desc">Professional coordination with 100+ cryptocurrency exchanges to freeze accounts, submit compliance requests, and facilitate fund recovery. 73% successful account freeze rate.</p>
      <div class="service-tags">
        <span class="tag">100+ Exchanges</span>
        <span class="tag">Global Network</span>
        <span class="tag">24-48hr Response</span>
      </div>
    </div>

    <div class="service-card fade-up">
      <div class="service-num">05</div>
      <span class="service-icon">⚖️</span>
      <div class="service-title">Legal Coordination</div>
      <p class="service-desc">Strategic support for attorneys and law enforcement with evidence packets, expert testimony, and recovery pathway recommendations across civil and criminal proceedings.</p>
      <div class="service-tags">
        <span class="tag">Expert Witness</span>
        <span class="tag">Law Enforcement</span>
        <span class="tag">Multi-Jurisdiction</span>
      </div>
    </div>

    <div class="service-card fade-up">
      <div class="service-num">06</div>
      <span class="service-icon">🗺️</span>
      <div class="service-title">Recovery Strategy</div>
      <p class="service-desc">Customized action plans combining legal, forensic, and intelligence-driven approaches. 81% of cases show improved recovery outcomes with our strategic planning methodology.</p>
      <div class="service-tags">
        <span class="tag">Custom Plan</span>
        <span class="tag">Timeline Mgmt</span>
        <span class="tag">Intelligence-Driven</span>
      </div>
    </div>
  </div>
</section>

<!-- PROCESS -->
<section class="process" id="process">
  <div style="text-align:center; max-width:600px; margin:0 auto;">
    <div class="section-label">// Recovery Process</div>
    <h2 class="section-title">From Case Intake<br>to Asset Recovery</h2>
    <p class="section-sub" style="max-width:100%; margin:0 auto;">A proven, systematic 7-step approach combining blockchain forensics with strategic global coordination.</p>
  </div>

  <div class="process-steps">
    <div class="step fade-up">
      <div class="step-num">1</div>
      <div class="step-title">Case Intake</div>
      <div class="step-desc">Submit details via secure form. 24-hour initial review.</div>
    </div>
    <div class="step fade-up">
      <div class="step-num">2</div>
      <div class="step-title">Data Collection</div>
      <div class="step-desc">Wallets, TXIDs, comms, and evidence gathered.</div>
    </div>
    <div class="step fade-up">
      <div class="step-num">3</div>
      <div class="step-title">Chain Tracing</div>
      <div class="step-desc">Advanced forensic analysis across 50+ blockchains.</div>
    </div>
    <div class="step fade-up">
      <div class="step-num">4</div>
      <div class="step-title">Forensic Report</div>
      <div class="step-desc">Court-ready documentation with flow charts.</div>
    </div>
    <div class="step fade-up">
      <div class="step-num">5</div>
      <div class="step-title">Strategy</div>
      <div class="step-desc">Custom recovery pathway developed in 2-3 days.</div>
    </div>
    <div class="step fade-up">
      <div class="step-num">6</div>
      <div class="step-title">Coordination</div>
      <div class="step-desc">Exchanges, law enforcement & legal liaison.</div>
    </div>
    <div class="step fade-up">
      <div class="step-num">7</div>
      <div class="step-title">Monitoring</div>
      <div class="step-desc">Continuous surveillance with regular updates.</div>
    </div>
  </div>
</section>

<!-- WHY US -->
<section class="why" id="about">
  <div class="why-grid">
    <div class="why-left">
      <div class="section-label">// Why Choose Us</div>
      <h2 class="section-title">Results Others<br>Can't Deliver</h2>
      <p class="section-sub">We combine cutting-edge blockchain forensics with legal expertise and global recovery networks.</p>

      <div class="why-features">
        <div class="why-feature">
          <div class="feature-icon">🏅</div>
          <div class="feature-title">Certified Expertise</div>
          <p class="feature-desc">Certified blockchain analysts, cybersecurity pros & forensic investigators.</p>
        </div>
        <div class="why-feature">
          <div class="feature-icon">⚖️</div>
          <div class="feature-title">Legal Compliance</div>
          <p class="feature-desc">All investigations follow ethical standards ensuring court admissibility.</p>
        </div>
        <div class="why-feature">
          <div class="feature-icon">🛰️</div>
          <div class="feature-title">Advanced Technology</div>
          <p class="feature-desc">Government-grade forensic tools and proprietary intelligence databases.</p>
        </div>
        <div class="why-feature">
          <div class="feature-icon">🌐</div>
          <div class="feature-title">Global Reach</div>
          <p class="feature-desc">Cross-border strategies coordinating with exchanges in 45+ countries.</p>
        </div>
        <div class="why-feature">
          <div class="feature-icon">📡</div>
          <div class="feature-title">Transparent Updates</div>
          <p class="feature-desc">Clear progress reports and realistic recovery potential assessments.</p>
        </div>
        <div class="why-feature">
          <div class="feature-icon">⚡</div>
          <div class="feature-title">Rapid Response</div>
          <p class="feature-desc">Case triage begins within 24 hours. Every minute matters.</p>
        </div>
      </div>
    </div>

    <div class="why-right">
      <div class="stats-block">
        <div class="stats-block-title">Performance Metrics</div>
        <div class="big-stat">
          <div class="big-num">87%</div>
          <div class="big-label">Fund Identification Rate</div>
          <div class="progress-bar"><div class="progress-fill" style="width:87%"></div></div>
        </div>
        <div class="big-stat">
          <div class="big-num">92%</div>
          <div class="big-label">Scammer ID Success</div>
          <div class="progress-bar"><div class="progress-fill" style="width:92%"></div></div>
        </div>
        <div class="big-stat">
          <div class="big-num">73%</div>
          <div class="big-label">Exchange Freeze Rate</div>
          <div class="progress-bar"><div class="progress-fill" style="width:73%"></div></div>
        </div>
        <div class="big-stat">
          <div class="big-num">81%</div>
          <div class="big-label">Improved Recovery Outcomes</div>
          <div class="progress-bar"><div class="progress-fill" style="width:81%"></div></div>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- TESTIMONIALS -->
<section class="testimonials" id="testimonials">
  <div style="text-align:center; max-width:600px; margin:0 auto 0;">
    <div class="section-label">// Client Stories</div>
    <h2 class="section-title">Real Recoveries,<br>Real Results</h2>
  </div>

  <div class="testi-grid">
    <div class="testi-card fade-up">
      <span class="testi-amount">$127K Recovered · 45 Days</span>
      <p class="testi-quote">"I lost $127,000 to a fake DeFi platform. ChainTrace traced the funds across five blockchains and provided evidence that helped law enforcement freeze the assets. Professionalism beyond compare."</p>
      <div class="testi-meta">
        <div class="testi-avatar">JM</div>
        <div>
          <div class="testi-name">James Mitchell</div>
          <div class="testi-loc">New York, USA</div>
        </div>
      </div>
    </div>

    <div class="testi-card fade-up">
      <span class="testi-amount">£89K Recovered · 60 Days</span>
      <p class="testi-quote">"After a romance scam stole my £89,000 in Bitcoin, I thought it was gone. ChainTrace's forensic team not only traced the transactions but identified the perpetrators. Outstanding."</p>
      <div class="testi-meta">
        <div class="testi-avatar">ST</div>
        <div>
          <div class="testi-name">Sarah Thompson</div>
          <div class="testi-loc">London, United Kingdom</div>
        </div>
      </div>
    </div>

    <div class="testi-card fade-up">
      <span class="testi-amount">42 ETH Traced · 30 Days</span>
      <p class="testi-quote">"Our company was hacked and 42 ETH stolen from our corporate wallet. ChainTrace provided forensic reports crucial for our insurance claim and law enforcement case. Highly professional."</p>
      <div class="testi-meta">
        <div class="testi-avatar">MK</div>
        <div>
          <div class="testi-name">Michael Klein</div>
          <div class="testi-loc">Berlin, Germany</div>
        </div>
      </div>
    </div>

    <div class="testi-card fade-up">
      <span class="testi-amount">$215K Traced · 52 Days</span>
      <p class="testi-quote">"I invested in what I thought was a legitimate crypto fund. When I tried to withdraw, they vanished with $215,000. ChainTrace traced the funds and worked with authorities. I'm grateful."</p>
      <div class="testi-meta">
        <div class="testi-avatar">AR</div>
        <div>
          <div class="testi-name">Amanda Rodriguez</div>
          <div class="testi-loc">Los Angeles, USA</div>
        </div>
      </div>
    </div>

    <div class="testi-card fade-up">
      <span class="testi-amount">8.5 BTC Traced · 38 Days</span>
      <p class="testi-quote">"My wallet was compromised and 8.5 BTC stolen. ChainTrace tracked transactions through multiple mixers and provided crucial evidence. Their expertise is unmatched in the industry."</p>
      <div class="testi-meta">
        <div class="testi-avatar">PD</div>
        <div>
          <div class="testi-name">Pierre Dubois</div>
          <div class="testi-loc">Paris, France</div>
        </div>
      </div>
    </div>

    <div class="testi-card fade-up">
      <span class="testi-amount">$340K Recovered · 55 Days</span>
      <p class="testi-quote">"A phishing attack cost me $340,000 in USDT. ChainTrace traced where the funds went and coordinated with exchanges to freeze assets. Their 24/7 support was invaluable during this stressful time."</p>
      <div class="testi-meta">
        <div class="testi-avatar">RC</div>
        <div>
          <div class="testi-name">Robert Chen</div>
          <div class="testi-loc">Houston, USA</div>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- CTA BAND -->
<div class="cta-band">
  <h2>Time Is Critical.<br>Act Now.</h2>
  <p>Every hour increases the chance of funds being liquidated or laundered beyond reach.</p>
  <div class="cta-actions">
    <a href="#submit" class="btn-primary">Get Free Case Assessment</a>
    <a href="tel:+18132032289" class="btn-ghost">📞 Emergency Hotline</a>
  </div>
</div>

<!-- SAFETY TIPS -->
<section class="safety" id="safety">
  <div class="section-label">// Security Intelligence</div>
  <h2 class="section-title">Protect Yourself<br>From Crypto Fraud</h2>

  <div class="warning-box">
    <span class="warning-icon">⚠️</span>
    <div>
      <div class="warning-title">Critical Warning</div>
      <div class="warning-text">If an investment opportunity sounds too good to be true, it almost certainly is. Red flags: unsolicited DMs, guaranteed returns, inability to withdraw, fake celebrity endorsements, and pressure tactics. Never share your private keys or seed phrase with anyone — ever.</div>
    </div>
  </div>

  <div class="safety-grid">
    <div class="safety-card fade-up">
      <div class="safety-num">01</div>
      <div class="safety-title">Research Before Investing</div>
      <p class="safety-desc">Always verify the project, team, and legitimacy. Check for audited smart contracts, verified social media presence, and community reviews before committing any funds.</p>
    </div>
    <div class="safety-card fade-up">
      <div class="safety-num">02</div>
      <div class="safety-title">Never Share Private Keys</div>
      <p class="safety-desc">Your private keys and seed phrases should NEVER be shared with anyone, under any circumstances. Legitimate services will never ask for them — period.</p>
    </div>
    <div class="safety-card fade-up">
      <div class="safety-num">03</div>
      <div class="safety-title">Verify URLs and Addresses</div>
      <p class="safety-desc">Double-check website URLs and wallet addresses character by character. Scammers create pixel-perfect replicas of legitimate platforms to steal your credentials.</p>
    </div>
    <div class="safety-card fade-up">
      <div class="safety-num">04</div>
      <div class="safety-title">Use Hardware Wallets</div>
      <p class="safety-desc">Store significant holdings in hardware wallets offline. Enable two-factor authentication on all exchange accounts and use unique passwords for every platform.</p>
    </div>
    <div class="safety-card fade-up">
      <div class="safety-num">05</div>
      <div class="safety-title">Beware Guaranteed Returns</div>
      <p class="safety-desc">No legitimate investment guarantees returns. Be deeply skeptical of any promises like "double your money" or "risk-free profits" — these are defining hallmarks of fraud.</p>
    </div>
    <div class="safety-card fade-up">
      <div class="safety-num">06</div>
      <div class="safety-title">Resist Pressure Tactics</div>
      <p class="safety-desc">Scammers manufacture urgency and exploit FOMO. Take your time researching any investment. If someone is pressuring you for a fast decision, that pressure itself is a red flag.</p>
    </div>
  </div>
</section>

<!-- CASE SUBMISSION -->
<section class="case-submit" id="submit">
  <div class="section-label">// Case Submission</div>
  <h2 class="section-title">Start Your<br>Recovery Today</h2>

  <div class="case-grid">
    <div class="case-info">
      <h3>Confidential & Secure</h3>
      <p>Complete this form to begin your case assessment. Our certified analysts will review your submission within 24 hours and contact you with next steps. All information is encrypted and handled with strict confidentiality.</p>

      <div class="info-items">
        <div class="info-item">
          <span class="info-item-icon">🔒</span>
          <div>
            <div class="info-item-label">100% Confidential</div>
            <div class="info-item-text">End-to-end encrypted case handling</div>
          </div>
        </div>
        <div class="info-item">
          <span class="info-item-icon">⏱️</span>
          <div>
            <div class="info-item-label">24-Hour Review</div>
            <div class="info-item-text">Initial assessment within one business day</div>
          </div>
        </div>
        <div class="info-item">
          <span class="info-item-icon">💼</span>
          <div>
            <div class="info-item-label">No Recovery, No Fee Options</div>
            <div class="info-item-text">Flexible arrangements available</div>
          </div>
        </div>
        <div class="info-item">
          <span class="info-item-icon">📞</span>
          <div>
            <div class="info-item-label">Emergency Hotline</div>
            <div class="info-item-text"><a href="tel:+18132032289" style="color:var(--accent);text-decoration:none;">+1 (813) 203-2289</a></div>
          </div>
        </div>
      </div>
    </div>

    <div class="case-form">
      <div class="form-row">
        <div class="form-group">
          <label class="form-label">First Name *</label>
          <input type="text" class="form-input" placeholder="John">
        </div>
        <div class="form-group">
          <label class="form-label">Last Name *</label>
          <input type="text" class="form-input" placeholder="Doe">
        </div>
      </div>

      <div class="form-group">
        <label class="form-label">Email Address *</label>
        <input type="email" class="form-input" placeholder="john@example.com">
      </div>

      <div class="form-row">
        <div class="form-group">
          <label class="form-label">Phone Number *</label>
          <input type="tel" class="form-input" placeholder="+1 (555) 000-0000">
        </div>
        <div class="form-group">
          <label class="form-label">Country *</label>
          <input type="text" class="form-input" placeholder="United States">
        </div>
      </div>

      <div class="form-row">
        <div class="form-group">
          <label class="form-label">Amount Lost (USD) *</label>
          <input type="text" class="form-input" placeholder="e.g. $50,000">
        </div>
        <div class="form-group">
          <label class="form-label">Asset Type *</label>
          <select class="form-select">
            <option>Select Asset Type</option>
            <option>Bitcoin (BTC)</option>
            <option>Ethereum (ETH)</option>
            <option>Tether (USDT)</option>
            <option>Solana (SOL)</option>
            <option>BNB</option>
            <option>XRP</option>
            <option>Other</option>
          </select>
        </div>
      </div>

      <div class="form-group">
        <label class="form-label">Type of Incident *</label>
        <select class="form-select">
          <option>Select Incident Type</option>
          <option>Investment Scam / Ponzi Scheme</option>
          <option>Phishing Attack</option>
          <option>Wallet Hack / Breach</option>
          <option>Romance Scam</option>
          <option>Fake Exchange Platform</option>
          <option>Rug Pull / Exit Scam</option>
          <option>Unauthorized Transfer</option>
          <option>Other</option>
        </select>
      </div>

      <div class="form-group">
        <label class="form-label">Transaction Hash / ID</label>
        <input type="text" class="form-input" placeholder="0x... or txid...">
      </div>

      <div class="form-group">
        <label class="form-label">Destination Wallet Address</label>
        <input type="text" class="form-input" placeholder="Where your funds were sent">
      </div>

      <div class="form-group">
        <label class="form-label">Description of Incident *</label>
        <textarea class="form-textarea" placeholder="Please describe what happened in as much detail as possible..."></textarea>
      </div>

      <div class="form-check">
        <input type="checkbox" id="consent">
        <label for="consent">I understand that ChainTrace Forensics will keep my information confidential and use it solely for case investigation purposes. I consent to be contacted regarding my case assessment.</label>
      </div>

      <button class="btn-submit" onclick="handleSubmit(this)">
        Submit Case for Review →
      </button>
    </div>
  </div>
</section>

<!-- FOOTER -->
<footer>
  <div class="footer-top">
    <div>
      <a href="#" class="nav-logo" style="margin-bottom:0">
        <div class="logo-icon">
          <svg width="18" height="18" viewBox="0 0 18 18" fill="none">
            <path d="M9 2L15 5.5V12.5L9 16L3 12.5V5.5L9 2Z" stroke="#050810" stroke-width="1.5" fill="none"/>
            <circle cx="9" cy="9" r="2" fill="#050810"/>
          </svg>
        </div>
        <span class="logo-text">Chain<span>Trace</span> Forensics</span>
      </a>
      <p class="footer-brand-desc">Global crypto asset recovery and blockchain forensic specialists. Helping victims recover stolen digital assets through legal-grade investigations and certified expertise.</p>
      <div class="footer-social">
        <a href="#" class="social-link">𝕏</a>
        <a href="#" class="social-link">in</a>
        <a href="#" class="social-link">▶</a>
      </div>
    </div>

    <div class="footer-col">
      <h4>Quick Links</h4>
      <ul class="footer-links">
        <li><a href="#home">Home</a></li>
        <li><a href="#services">Services</a></li>
        <li><a href="#process">Our Process</a></li>
        <li><a href="#testimonials">Client Stories</a></li>
        <li><a href="#safety">Safety Tips</a></li>
      </ul>
    </div>

    <div class="footer-col">
      <h4>Services</h4>
      <ul class="footer-links">
        <li><a href="#services">Crypto Asset Tracing</a></li>
        <li><a href="#services">Fraud Investigation</a></li>
        <li><a href="#services">Forensic Reports</a></li>
        <li><a href="#services">Exchange Liaison</a></li>
        <li><a href="#submit">Submit a Case</a></li>
      </ul>
    </div>

    <div class="footer-col">
      <h4>Contact</h4>
      <div class="footer-contact-item">
        <span class="contact-icon">📍</span>
        501 E. Las Olas Blvd., Miami, FL
      </div>
      <div class="footer-contact-item">
        <span class="contact-icon">📧</span>
        info@chaintrace.io
      </div>
      <div class="footer-contact-item">
        <span class="contact-icon">📞</span>
        +1 (813) 203-2289
      </div>
      <div class="footer-contact-item">
        <span class="contact-icon">💬</span>
        WhatsApp Available
      </div>
    </div>
  </div>

  <div class="footer-bottom">
    <span class="footer-copy">© 2026 ChainTrace Forensics. All rights reserved. Professional Blockchain Forensics & Asset Recovery.</span>
    <div class="footer-legal">
      <a href="#">Terms & Conditions</a>
      <a href="#">Privacy Policy</a>
      <a href="#">Anti-Fraud Disclaimer</a>
    </div>
  </div>
</footer>

<script>
  // Custom cursor
  const cursor = document.getElementById('cursor');
  const ring = document.getElementById('cursorRing');
  let mx = 0, my = 0, rx = 0, ry = 0;

  document.addEventListener('mousemove', e => {
    mx = e.clientX; my = e.clientY;
    cursor.style.left = mx + 'px';
    cursor.style.top = my + 'px';
  });

  function animateRing() {
    rx += (mx - rx) * 0.12;
    ry += (my - ry) * 0.12;
    ring.style.left = rx + 'px';
    ring.style.top = ry + 'px';
    requestAnimationFrame(animateRing);
  }
  animateRing();

  document.querySelectorAll('a, button, input, select, textarea').forEach(el => {
    el.addEventListener('mouseenter', () => {
      cursor.style.width = '20px';
      cursor.style.height = '20px';
      ring.style.width = '52px';
      ring.style.height = '52px';
    });
    el.addEventListener('mouseleave', () => {
      cursor.style.width = '12px';
      cursor.style.height = '12px';
      ring.style.width = '36px';
      ring.style.height = '36px';
    });
  });

  // Scroll animations
  const faders = document.querySelectorAll('.fade-up');
  const observer = new IntersectionObserver(entries => {
    entries.forEach((entry, i) => {
      if (entry.isIntersecting) {
        setTimeout(() => entry.target.classList.add('visible'), i * 80);
        observer.unobserve(entry.target);
      }
    });
  }, { threshold: 0.1 });
  faders.forEach(el => observer.observe(el));

  // Form submit
  function handleSubmit(btn) {
    btn.textContent = '⏳ Submitting Case...';
    btn.style.opacity = '0.7';
    setTimeout(() => {
      btn.textContent = '✓ Case Submitted — We\'ll contact you within 24 hours';
      btn.style.background = 'var(--accent2)';
      btn.style.opacity = '1';
    }, 1800);
  }

  // Smooth scroll for nav links
  document.querySelectorAll('a[href^="#"]').forEach(a => {
    a.addEventListener('click', e => {
      const target = document.querySelector(a.getAttribute('href'));
      if (target) {
        e.preventDefault();
        target.scrollIntoView({ behavior: 'smooth', block: 'start' });
      }
    });
  });
</script>

</body>
</html>
