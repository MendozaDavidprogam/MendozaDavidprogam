<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>DAVID.EXE — Full Stack Developer</title>
<link href="https://fonts.googleapis.com/css2?family=Share+Tech+Mono&family=Orbitron:wght@400;700;900&family=Rajdhani:wght@300;400;600;700&display=swap" rel="stylesheet">
<style>
  :root {
    --blood: #c8001a;
    --blood-dim: #7a0010;
    --neon-green: #00ff9d;
    --neon-dim: #00cc7a;
    --cyan: #00e5ff;
    --amber: #ffb800;
    --dark: #050508;
    --panel: #0a0a10;
    --panel2: #0d0d16;
    --border: rgba(200,0,26,0.35);
    --text: #c8c8d8;
    --mono: 'Share Tech Mono', monospace;
    --display: 'Orbitron', monospace;
    --body: 'Rajdhani', sans-serif;
  }

  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  html { scroll-behavior: smooth; }

  body {
    background: var(--dark);
    color: var(--text);
    font-family: var(--body);
    font-size: 16px;
    line-height: 1.6;
    overflow-x: hidden;
    cursor: crosshair;
  }

  /* SCANLINE OVERLAY */
  body::before {
    content: '';
    position: fixed;
    inset: 0;
    background: repeating-linear-gradient(
      0deg,
      transparent,
      transparent 2px,
      rgba(0,0,0,0.07) 2px,
      rgba(0,0,0,0.07) 4px
    );
    pointer-events: none;
    z-index: 9999;
  }

  /* NOISE TEXTURE */
  body::after {
    content: '';
    position: fixed;
    inset: 0;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)' opacity='0.04'/%3E%3C/svg%3E");
    pointer-events: none;
    z-index: 9998;
    opacity: 0.5;
  }

  /* NAVBAR */
  nav {
    position: fixed;
    top: 0;
    width: 100%;
    z-index: 1000;
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 14px 48px;
    background: rgba(5,5,8,0.92);
    border-bottom: 1px solid var(--border);
    backdrop-filter: blur(12px);
  }

  .nav-logo {
    font-family: var(--display);
    font-size: 13px;
    font-weight: 900;
    color: var(--blood);
    letter-spacing: 4px;
    text-transform: uppercase;
    position: relative;
  }

  .nav-logo::after {
    content: '_';
    animation: blink 1s step-end infinite;
    color: var(--neon-green);
  }

  .nav-links {
    display: flex;
    gap: 36px;
    list-style: none;
  }

  .nav-links a {
    font-family: var(--mono);
    font-size: 11px;
    color: var(--text);
    text-decoration: none;
    letter-spacing: 3px;
    text-transform: uppercase;
    position: relative;
    transition: color 0.2s;
  }

  .nav-links a::before {
    content: '> ';
    color: var(--blood);
    opacity: 0;
    transition: opacity 0.2s;
  }

  .nav-links a:hover { color: var(--neon-green); }
  .nav-links a:hover::before { opacity: 1; }

  .nav-status {
    font-family: var(--mono);
    font-size: 10px;
    color: var(--neon-green);
    display: flex;
    align-items: center;
    gap: 8px;
    letter-spacing: 2px;
  }

  .status-dot {
    width: 7px; height: 7px;
    border-radius: 50%;
    background: var(--neon-green);
    animation: pulse-green 2s ease-in-out infinite;
  }

  /* HERO */
  #hero {
    min-height: 100vh;
    display: flex;
    align-items: center;
    position: relative;
    overflow: hidden;
    padding: 120px 48px 80px;
  }

  .hero-grid {
    position: absolute;
    inset: 0;
    background-image:
      linear-gradient(rgba(200,0,26,0.07) 1px, transparent 1px),
      linear-gradient(90deg, rgba(200,0,26,0.07) 1px, transparent 1px);
    background-size: 60px 60px;
    animation: grid-move 20s linear infinite;
  }

  .hero-glow-left {
    position: absolute;
    left: -200px;
    top: 50%;
    transform: translateY(-50%);
    width: 600px; height: 600px;
    background: radial-gradient(circle, rgba(200,0,26,0.15) 0%, transparent 70%);
    pointer-events: none;
  }

  .hero-glow-right {
    position: absolute;
    right: -100px;
    bottom: 0;
    width: 400px; height: 400px;
    background: radial-gradient(circle, rgba(0,255,157,0.08) 0%, transparent 70%);
    pointer-events: none;
  }

  .hero-content {
    position: relative;
    z-index: 2;
    max-width: 900px;
  }

  .hero-tag {
    font-family: var(--mono);
    font-size: 11px;
    color: var(--blood);
    letter-spacing: 5px;
    text-transform: uppercase;
    margin-bottom: 20px;
    display: flex;
    align-items: center;
    gap: 12px;
    animation: fadeInDown 0.8s ease both;
  }

  .hero-tag::before {
    content: '';
    width: 40px; height: 1px;
    background: var(--blood);
  }

  .hero-name {
    font-family: var(--display);
    font-size: clamp(52px, 7vw, 96px);
    font-weight: 900;
    line-height: 0.9;
    text-transform: uppercase;
    margin-bottom: 8px;
    animation: fadeInDown 0.8s 0.1s ease both;
  }

  .hero-name .line1 { color: #fff; display: block; }
  .hero-name .line2 {
    color: var(--blood);
    display: block;
    text-shadow: 0 0 40px rgba(200,0,26,0.6), 0 0 80px rgba(200,0,26,0.3);
    position: relative;
  }

  .glitch {
    position: relative;
  }

  .glitch::before, .glitch::after {
    content: attr(data-text);
    position: absolute;
    top: 0; left: 0;
    width: 100%;
    overflow: hidden;
  }

  .glitch::before {
    color: var(--cyan);
    animation: glitch1 3s infinite;
    clip-path: polygon(0 20%, 100% 20%, 100% 40%, 0 40%);
    transform: translateX(-3px);
    opacity: 0.7;
  }

  .glitch::after {
    color: var(--neon-green);
    animation: glitch2 3s infinite;
    clip-path: polygon(0 60%, 100% 60%, 100% 80%, 0 80%);
    transform: translateX(3px);
    opacity: 0.7;
  }

  .hero-role {
    font-family: var(--mono);
    font-size: 15px;
    color: var(--neon-green);
    margin: 24px 0 16px;
    animation: fadeInDown 0.8s 0.2s ease both;
    letter-spacing: 2px;
  }

  .hero-desc {
    font-family: var(--body);
    font-size: 17px;
    font-weight: 300;
    color: rgba(200,200,216,0.7);
    max-width: 560px;
    line-height: 1.7;
    margin-bottom: 40px;
    animation: fadeInDown 0.8s 0.3s ease both;
  }

  .hero-desc strong { color: var(--text); font-weight: 600; }

  .hero-buttons {
    display: flex;
    gap: 16px;
    flex-wrap: wrap;
    animation: fadeInDown 0.8s 0.4s ease both;
  }

  .btn-primary {
    font-family: var(--mono);
    font-size: 11px;
    letter-spacing: 3px;
    text-transform: uppercase;
    padding: 14px 32px;
    background: var(--blood);
    color: #fff;
    border: none;
    text-decoration: none;
    display: inline-flex;
    align-items: center;
    gap: 10px;
    cursor: crosshair;
    position: relative;
    overflow: hidden;
    clip-path: polygon(0 0, calc(100% - 12px) 0, 100% 12px, 100% 100%, 12px 100%, 0 calc(100% - 12px));
    transition: all 0.3s;
  }

  .btn-primary::before {
    content: '';
    position: absolute;
    inset: 0;
    background: rgba(255,255,255,0.1);
    transform: translateX(-100%);
    transition: transform 0.3s;
  }

  .btn-primary:hover { box-shadow: 0 0 30px rgba(200,0,26,0.6); }
  .btn-primary:hover::before { transform: translateX(0); }

  .btn-ghost {
    font-family: var(--mono);
    font-size: 11px;
    letter-spacing: 3px;
    text-transform: uppercase;
    padding: 13px 32px;
    background: transparent;
    color: var(--neon-green);
    border: 1px solid var(--neon-green);
    text-decoration: none;
    display: inline-flex;
    align-items: center;
    gap: 10px;
    cursor: crosshair;
    clip-path: polygon(0 0, calc(100% - 12px) 0, 100% 12px, 100% 100%, 12px 100%, 0 calc(100% - 12px));
    transition: all 0.3s;
  }

  .btn-ghost:hover {
    background: rgba(0,255,157,0.1);
    box-shadow: 0 0 20px rgba(0,255,157,0.3);
  }

  /* CORNER DECORATIONS */
  .corner-deco {
    position: absolute;
    width: 80px; height: 80px;
    pointer-events: none;
  }

  .corner-deco.tl { top: 20px; left: 20px; border-top: 2px solid var(--blood); border-left: 2px solid var(--blood); }
  .corner-deco.tr { top: 20px; right: 20px; border-top: 2px solid var(--blood); border-right: 2px solid var(--blood); }
  .corner-deco.bl { bottom: 20px; left: 20px; border-bottom: 2px solid var(--blood); border-left: 2px solid var(--blood); }
  .corner-deco.br { bottom: 20px; right: 20px; border-bottom: 2px solid var(--blood); border-right: 2px solid var(--blood); }

  .hero-side-text {
    position: absolute;
    right: 48px;
    top: 50%;
    transform: translateY(-50%) rotate(90deg);
    font-family: var(--mono);
    font-size: 10px;
    color: rgba(200,0,26,0.4);
    letter-spacing: 4px;
    text-transform: uppercase;
  }

  /* SECTION BASE */
  section {
    padding: 100px 48px;
    position: relative;
  }

  .section-label {
    font-family: var(--mono);
    font-size: 10px;
    color: var(--blood);
    letter-spacing: 5px;
    text-transform: uppercase;
    margin-bottom: 12px;
    display: flex;
    align-items: center;
    gap: 12px;
  }

  .section-label::after {
    content: '';
    flex: 1;
    height: 1px;
    background: linear-gradient(to right, var(--blood-dim), transparent);
    max-width: 200px;
  }

  .section-title {
    font-family: var(--display);
    font-size: clamp(28px, 4vw, 48px);
    font-weight: 900;
    text-transform: uppercase;
    color: #fff;
    margin-bottom: 16px;
  }

  .section-sub {
    font-family: var(--body);
    font-size: 16px;
    color: rgba(200,200,216,0.55);
    font-weight: 300;
    margin-bottom: 60px;
    letter-spacing: 1px;
  }

  /* ABOUT */
  #about {
    background: var(--panel);
    border-top: 1px solid var(--border);
    border-bottom: 1px solid var(--border);
  }

  .about-inner {
    display: grid;
    grid-template-columns: auto 1fr;
    gap: 80px;
    align-items: start;
    max-width: 1200px;
    margin: 0 auto;
  }

  .about-photo-wrap {
    position: relative;
    flex-shrink: 0;
  }

  .about-photo {
    width: 220px; height: 220px;
    border-radius: 0;
    object-fit: cover;
    clip-path: polygon(0 0, calc(100% - 20px) 0, 100% 20px, 100% 100%, 20px 100%, 0 calc(100% - 20px));
    filter: grayscale(30%) contrast(1.1);
    display: block;
  }

  .about-photo-border {
    position: absolute;
    inset: -6px;
    clip-path: polygon(0 0, calc(100% - 22px) 0, 100% 22px, 100% 100%, 22px 100%, 0 calc(100% - 22px));
    border: 1px solid var(--blood);
    pointer-events: none;
  }

  .about-photo-scan {
    position: absolute;
    inset: 0;
    background: linear-gradient(transparent 0%, rgba(200,0,26,0.1) 50%, transparent 100%);
    animation: scan 3s ease-in-out infinite;
    pointer-events: none;
  }

  .about-photo-label {
    position: absolute;
    bottom: -28px;
    left: 0;
    right: 0;
    text-align: center;
    font-family: var(--mono);
    font-size: 9px;
    color: var(--blood);
    letter-spacing: 3px;
  }

  .about-text .section-label { margin-bottom: 6px; }

  .about-text p {
    font-size: 16px;
    font-weight: 300;
    color: rgba(200,200,216,0.8);
    line-height: 1.8;
    margin-bottom: 18px;
  }

  .about-text p strong { color: var(--neon-green); font-weight: 600; }

  .about-stats {
    display: flex;
    gap: 40px;
    margin: 32px 0;
    padding: 24px 0;
    border-top: 1px solid rgba(200,0,26,0.2);
    border-bottom: 1px solid rgba(200,0,26,0.2);
  }

  .stat {
    text-align: center;
  }

  .stat-num {
    font-family: var(--display);
    font-size: 32px;
    font-weight: 900;
    color: var(--blood);
    display: block;
    text-shadow: 0 0 20px rgba(200,0,26,0.5);
  }

  .stat-label {
    font-family: var(--mono);
    font-size: 9px;
    color: rgba(200,200,216,0.5);
    letter-spacing: 2px;
    text-transform: uppercase;
  }

  .about-actions {
    display: flex;
    gap: 14px;
    flex-wrap: wrap;
    margin-top: 32px;
  }

  /* SKILLS */
  #skills {
    background: var(--dark);
  }

  .skills-inner {
    max-width: 1200px;
    margin: 0 auto;
  }

  .skills-category {
    margin-bottom: 60px;
  }

  .skills-cat-header {
    display: flex;
    align-items: center;
    gap: 14px;
    margin-bottom: 32px;
    padding-bottom: 14px;
    border-bottom: 1px solid rgba(200,0,26,0.2);
  }

  .skills-cat-dot {
    width: 8px; height: 8px;
    border-radius: 50%;
    flex-shrink: 0;
  }

  .skills-cat-dot.frontend { background: var(--cyan); box-shadow: 0 0 10px var(--cyan); }
  .skills-cat-dot.backend { background: var(--neon-green); box-shadow: 0 0 10px var(--neon-green); }

  .skills-cat-title {
    font-family: var(--mono);
    font-size: 12px;
    letter-spacing: 4px;
    text-transform: uppercase;
    color: var(--text);
  }

  .skills-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(140px, 1fr));
    gap: 14px;
  }

  .skill-card {
    background: var(--panel2);
    border: 1px solid rgba(200,0,26,0.2);
    padding: 20px 16px;
    position: relative;
    cursor: crosshair;
    transition: all 0.3s;
    clip-path: polygon(0 0, calc(100% - 10px) 0, 100% 10px, 100% 100%, 10px 100%, 0 calc(100% - 10px));
    overflow: hidden;
  }

  .skill-card::before {
    content: '';
    position: absolute;
    inset: 0;
    background: linear-gradient(135deg, rgba(200,0,26,0.05), transparent);
    opacity: 0;
    transition: opacity 0.3s;
  }

  .skill-card:hover {
    border-color: var(--blood);
    transform: translateY(-3px);
    box-shadow: 0 8px 30px rgba(200,0,26,0.25);
  }

  .skill-card:hover::before { opacity: 1; }

  .skill-icon {
    font-size: 28px;
    margin-bottom: 10px;
    display: block;
    filter: drop-shadow(0 0 8px currentColor);
  }

  .skill-name {
    font-family: var(--mono);
    font-size: 11px;
    color: var(--text);
    letter-spacing: 1px;
    margin-bottom: 10px;
    display: block;
  }

  .skill-bar-track {
    height: 2px;
    background: rgba(255,255,255,0.08);
    position: relative;
    overflow: visible;
    margin-bottom: 6px;
  }

  .skill-bar-fill {
    height: 100%;
    position: relative;
    transition: width 1.2s cubic-bezier(0.4,0,0.2,1);
  }

  .skill-bar-fill::after {
    content: '';
    position: absolute;
    right: 0;
    top: -3px;
    width: 8px; height: 8px;
    border-radius: 50%;
    background: currentColor;
    box-shadow: 0 0 8px currentColor;
  }

  .skill-pct {
    font-family: var(--mono);
    font-size: 9px;
    color: rgba(200,200,216,0.4);
    letter-spacing: 1px;
    text-align: right;
    display: block;
  }

  /* CONTACT */
  #contact {
    background: var(--panel);
    border-top: 1px solid var(--border);
  }

  .contact-inner {
    max-width: 900px;
    margin: 0 auto;
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 60px;
    align-items: start;
  }

  .contact-info-items {
    display: flex;
    flex-direction: column;
    gap: 20px;
  }

  .contact-item {
    display: flex;
    gap: 18px;
    align-items: flex-start;
    padding: 18px 20px;
    background: var(--panel2);
    border: 1px solid rgba(200,0,26,0.2);
    clip-path: polygon(0 0, calc(100% - 10px) 0, 100% 10px, 100% 100%, 0 100%);
    transition: all 0.3s;
    text-decoration: none;
    color: inherit;
  }

  .contact-item:hover {
    border-color: var(--blood);
    background: rgba(200,0,26,0.06);
  }

  .contact-icon {
    width: 36px; height: 36px;
    display: flex;
    align-items: center;
    justify-content: center;
    border: 1px solid rgba(200,0,26,0.4);
    clip-path: polygon(0 0, calc(100% - 6px) 0, 100% 6px, 100% 100%, 6px 100%, 0 calc(100% - 6px));
    flex-shrink: 0;
    font-size: 15px;
  }

  .contact-label {
    font-family: var(--mono);
    font-size: 9px;
    color: var(--blood);
    letter-spacing: 3px;
    text-transform: uppercase;
    margin-bottom: 4px;
    display: block;
  }

  .contact-value {
    font-family: var(--body);
    font-size: 15px;
    color: var(--text);
    font-weight: 400;
  }

  .contact-form {
    display: flex;
    flex-direction: column;
    gap: 14px;
  }

  .form-group {
    position: relative;
  }

  .form-label {
    font-family: var(--mono);
    font-size: 9px;
    color: var(--blood);
    letter-spacing: 3px;
    text-transform: uppercase;
    margin-bottom: 6px;
    display: block;
  }

  .form-input, .form-textarea {
    width: 100%;
    background: var(--panel2);
    border: 1px solid rgba(200,0,26,0.25);
    color: var(--text);
    font-family: var(--mono);
    font-size: 13px;
    padding: 12px 16px;
    outline: none;
    transition: border-color 0.3s, box-shadow 0.3s;
    clip-path: polygon(0 0, calc(100% - 8px) 0, 100% 8px, 100% 100%, 0 100%);
  }

  .form-textarea { height: 100px; resize: none; }

  .form-input:focus, .form-textarea:focus {
    border-color: var(--blood);
    box-shadow: 0 0 12px rgba(200,0,26,0.2);
  }

  .form-input::placeholder, .form-textarea::placeholder {
    color: rgba(200,200,216,0.2);
  }

  /* FOOTER */
  footer {
    padding: 30px 48px;
    border-top: 1px solid var(--border);
    display: flex;
    align-items: center;
    justify-content: space-between;
    background: var(--dark);
  }

  .footer-copy {
    font-family: var(--mono);
    font-size: 10px;
    color: rgba(200,200,216,0.3);
    letter-spacing: 2px;
  }

  .footer-status {
    display: flex;
    align-items: center;
    gap: 8px;
    font-family: var(--mono);
    font-size: 10px;
    color: var(--neon-green);
    letter-spacing: 2px;
  }

  /* DIVIDER */
  .cyber-divider {
    display: flex;
    align-items: center;
    gap: 12px;
    margin-bottom: 60px;
  }

  .cyber-divider::before, .cyber-divider::after {
    content: '';
    flex: 1;
    height: 1px;
    background: linear-gradient(to right, transparent, rgba(200,0,26,0.4));
  }
  .cyber-divider::after {
    background: linear-gradient(to left, transparent, rgba(200,0,26,0.4));
  }

  .cyber-diamond {
    width: 8px; height: 8px;
    background: var(--blood);
    transform: rotate(45deg);
    box-shadow: 0 0 10px var(--blood);
  }

  /* GLITCH TEXT ANIM */
  @keyframes glitch1 {
    0%, 80%, 100% { transform: translateX(-3px); opacity: 0; }
    82% { transform: translateX(-3px); opacity: 0.7; clip-path: polygon(0 20%, 100% 20%, 100% 40%, 0 40%); }
    84% { transform: translateX(3px); opacity: 0.7; clip-path: polygon(0 60%, 100% 60%, 100% 80%, 0 80%); }
    86% { transform: translateX(-3px); opacity: 0; }
  }

  @keyframes glitch2 {
    0%, 83%, 100% { transform: translateX(3px); opacity: 0; }
    85% { transform: translateX(3px); opacity: 0.7; clip-path: polygon(0 60%, 100% 60%, 100% 80%, 0 80%); }
    87% { transform: translateX(-3px); opacity: 0.7; clip-path: polygon(0 30%, 100% 30%, 100% 50%, 0 50%); }
    89% { transform: translateX(3px); opacity: 0; }
  }

  @keyframes blink {
    0%, 100% { opacity: 1; }
    50% { opacity: 0; }
  }

  @keyframes pulse-green {
    0%, 100% { opacity: 1; box-shadow: 0 0 6px var(--neon-green); }
    50% { opacity: 0.4; box-shadow: 0 0 2px var(--neon-green); }
  }

  @keyframes scan {
    0% { transform: translateY(-100%); }
    100% { transform: translateY(200%); }
  }

  @keyframes grid-move {
    0% { background-position: 0 0; }
    100% { background-position: 60px 60px; }
  }

  @keyframes fadeInDown {
    from { opacity: 0; transform: translateY(-20px); }
    to { opacity: 1; transform: translateY(0); }
  }

  /* SCROLL ANIMATIONS */
  .reveal {
    opacity: 0;
    transform: translateY(30px);
    transition: opacity 0.7s ease, transform 0.7s ease;
  }

  .reveal.visible {
    opacity: 1;
    transform: translateY(0);
  }

  /* SYSTEM LOG */
  .sys-log {
    font-family: var(--mono);
    font-size: 11px;
    color: rgba(0,255,157,0.45);
    margin-bottom: 40px;
    display: flex;
    flex-direction: column;
    gap: 4px;
    animation: fadeInDown 0.8s 0.5s ease both;
  }

  .sys-log span { display: block; }

  .typing-cursor::after {
    content: '█';
    animation: blink 0.8s step-end infinite;
    color: var(--neon-green);
  }

  /* RESPONSIVE */
  @media (max-width: 768px) {
    nav { padding: 14px 20px; }
    nav .nav-links { display: none; }
    section { padding: 70px 20px; }
    #hero { padding: 100px 20px 60px; }
    .about-inner { grid-template-columns: 1fr; gap: 40px; }
    .contact-inner { grid-template-columns: 1fr; gap: 40px; }
    .hero-side-text { display: none; }
    footer { padding: 24px 20px; flex-direction: column; gap: 10px; text-align: center; }
  }
</style>
</head>
<body>

<!-- NAV -->
<nav>
  <div class="nav-logo">DAVID.EXE</div>
  <ul class="nav-links">
    <li><a href="#about">PERFIL</a></li>
    <li><a href="#skills">SISTEMAS</a></li>
    <li><a href="#contact">CONTACTO</a></li>
  </ul>
  <div class="nav-status">
    <span class="status-dot"></span>
    SISTEMA ACTIVO
  </div>
</nav>

<!-- HERO -->
<section id="hero">
  <div class="hero-grid"></div>
  <div class="hero-glow-left"></div>
  <div class="hero-glow-right"></div>

  <div class="corner-deco tl"></div>
  <div class="corner-deco tr"></div>
  <div class="corner-deco bl"></div>
  <div class="corner-deco br"></div>
  <div class="hero-side-text">// PORTFOLIO v2.0 // LARA VENEZUELA //</div>

  <div class="hero-content">
    <div class="hero-tag">// IDENTIFICACIÓN DEL OPERADOR</div>

    <h1 class="hero-name">
      <span class="line1">DAVID</span>
      <span class="line2 glitch" data-text="MENDOZA">MENDOZA</span>
    </h1>

    <div class="hero-role">> FULL_STACK_DEVELOPER<span class="typing-cursor"></span></div>

    <div class="sys-log">
      <span>[SYS] Cargando módulos de desarrollo...</span>
      <span>[OK] Frontend :: React / TypeScript / HTML5 / CSS3</span>
      <span>[OK] Backend :: Node.js / Java / Python / NestJS</span>
      <span>[OK] DB :: PostgreSQL / MySQL</span>
      <span>[READY] Bienvenido a mi portafolio</span>
    </div>

    <p class="hero-desc">
      Desarrollador <strong>Full Stack</strong> con enfoque en backend y frontend.
      Apasionado por crear aplicaciones web con <strong>buen rendimiento</strong> y
      experiencias de usuario claras. Estudiante en <strong>Gracosoft</strong>,
      siempre en búsqueda de nuevos desafíos.
    </p>

    <div class="hero-buttons">
      <a href="#contact" class="btn-primary">▶ CONTACTAR</a>
      <a href="#skills" class="btn-ghost">// VER SISTEMAS</a>
    </div>
  </div>
</section>

<!-- ABOUT -->
<section id="about">
  <div class="about-inner">
    <div class="about-photo-wrap reveal">
      <!-- Placeholder avatar since we can't embed the actual photo -->
      <svg width="220" height="220" viewBox="0 0 220 220" style="display:block; clip-path: polygon(0 0, calc(100% - 20px) 0, 100% 20px, 100% 100%, 20px 100%, 0 calc(100% - 20px)); filter: grayscale(30%) contrast(1.1);">
        <rect width="220" height="220" fill="#0d0d16"/>
        <rect x="60" y="40" width="100" height="100" rx="50" fill="#1a1a2e"/>
        <circle cx="110" cy="85" r="35" fill="#252538"/>
        <ellipse cx="110" cy="175" rx="60" ry="45" fill="#252538"/>
        <!-- Scan line overlay -->
        <rect width="220" height="220" fill="url(#scanGrad)" opacity="0.3"/>
        <defs>
          <linearGradient id="scanGrad" x1="0" y1="0" x2="0" y2="1">
            <stop offset="0%" stop-color="#c8001a" stop-opacity="0"/>
            <stop offset="50%" stop-color="#c8001a" stop-opacity="0.15"/>
            <stop offset="100%" stop-color="#c8001a" stop-opacity="0"/>
          </linearGradient>
        </defs>
        <text x="110" y="215" text-anchor="middle" font-family="Share Tech Mono, monospace" font-size="9" fill="#c8001a" letter-spacing="2">DAVID M.</text>
      </svg>
      <div class="about-photo-border"></div>
      <div class="about-photo-scan"></div>
      <div class="about-photo-label">// ID: DM-2025 //</div>
    </div>

    <div class="about-text reveal" style="transition-delay:0.15s">
      <div class="section-label">// SOBRE MÍ</div>
      <h2 class="section-title" style="margin-bottom:24px;">QUIÉN SOY</h2>

      <p>
        Estudiante de <strong>Desarrollo de Software en Gracosoft</strong>, con formación en fundamentos de programación utilizando <strong>Java, C# y Python</strong>. Poseo conocimientos en diseño y modelado de bases de datos.
      </p>
      <p>
        Me especializo en desarrollo web con <strong>JavaScript, HTML y CSS</strong>, enfocado en escribir código claro, funcional y orientado a buenas prácticas. Cada proyecto me impulsa a fortalecer mis habilidades y estar listo para nuevos desafíos.
      </p>

      <div class="about-stats">
        <div class="stat">
          <span class="stat-num">14+</span>
          <span class="stat-label">Tecnologías</span>
        </div>
        <div class="stat">
          <span class="stat-num">Full</span>
          <span class="stat-label">Stack</span>
        </div>
        <div class="stat">
          <span class="stat-num">VE</span>
          <span class="stat-label">Lara · Venezuela</span>
        </div>
      </div>

      <div class="about-actions">
        <a href="#" class="btn-primary">▶ VER CV</a>
        <a href="#" class="btn-ghost">⬇ DESCARGAR CV</a>
      </div>
    </div>
  </div>
</section>

<!-- SKILLS -->
<section id="skills">
  <div class="skills-inner">
    <div class="section-label reveal">// CONOCIMIENTOS</div>
    <h2 class="section-title reveal">TECNOLOGÍAS</h2>
    <p class="section-sub reveal">Herramientas y lenguajes con los que trabajo.</p>

    <!-- FRONTEND -->
    <div class="skills-category reveal">
      <div class="skills-cat-header">
        <div class="skills-cat-dot frontend"></div>
        <span class="skills-cat-title">Frontend</span>
      </div>
      <div class="skills-grid">
        <div class="skill-card" style="--delay:0s">
          <span class="skill-icon" style="color:#61dafb;">⚛</span>
          <span class="skill-name">React</span>
          <div class="skill-bar-track">
            <div class="skill-bar-fill" style="width:75%; background:#61dafb; color:#61dafb;"></div>
          </div>
          <span class="skill-pct">75%</span>
        </div>
        <div class="skill-card">
          <span class="skill-icon" style="color:#3178c6;">TS</span>
          <span class="skill-name">TypeScript</span>
          <div class="skill-bar-track">
            <div class="skill-bar-fill" style="width:70%; background:#3178c6; color:#3178c6;"></div>
          </div>
          <span class="skill-pct">70%</span>
        </div>
        <div class="skill-card">
          <span class="skill-icon" style="color:#f7df1e;">JS</span>
          <span class="skill-name">JavaScript</span>
          <div class="skill-bar-track">
            <div class="skill-bar-fill" style="width:75%; background:#f7df1e; color:#f7df1e;"></div>
          </div>
          <span class="skill-pct">75%</span>
        </div>
        <div class="skill-card">
          <span class="skill-icon" style="color:#e34f26;">⬡</span>
          <span class="skill-name">HTML5</span>
          <div class="skill-bar-track">
            <div class="skill-bar-fill" style="width:80%; background:#e34f26; color:#e34f26;"></div>
          </div>
          <span class="skill-pct">80%</span>
        </div>
        <div class="skill-card">
          <span class="skill-icon" style="color:#264de4;">◈</span>
          <span class="skill-name">CSS3</span>
          <div class="skill-bar-track">
            <div class="skill-bar-fill" style="width:70%; background:#264de4; color:#264de4;"></div>
          </div>
          <span class="skill-pct">70%</span>
        </div>
        <div class="skill-card">
          <span class="skill-icon" style="color:#61dafb;">⊛</span>
          <span class="skill-name">React Native</span>
          <div class="skill-bar-track">
            <div class="skill-bar-fill" style="width:65%; background:#61dafb; color:#61dafb;"></div>
          </div>
          <span class="skill-pct">65%</span>
        </div>
      </div>
    </div>

    <!-- BACKEND -->
    <div class="skills-category reveal" style="transition-delay:0.2s">
      <div class="skills-cat-header">
        <div class="skills-cat-dot backend"></div>
        <span class="skills-cat-title">Backend &amp; Herramientas</span>
      </div>
      <div class="skills-grid">
        <div class="skill-card">
          <span class="skill-icon" style="color:#f89820;">☕</span>
          <span class="skill-name">Java</span>
          <div class="skill-bar-track">
            <div class="skill-bar-fill" style="width:75%; background:#f89820; color:#f89820;"></div>
          </div>
          <span class="skill-pct">75%</span>
        </div>
        <div class="skill-card">
          <span class="skill-icon" style="color:#6da55f;">⬡</span>
          <span class="skill-name">Node.js</span>
          <div class="skill-bar-track">
            <div class="skill-bar-fill" style="width:75%; background:#6da55f; color:#6da55f;"></div>
          </div>
          <span class="skill-pct">75%</span>
        </div>
        <div class="skill-card">
          <span class="skill-icon" style="color:#336791;">🐘</span>
          <span class="skill-name">PostgreSQL</span>
          <div class="skill-bar-track">
            <div class="skill-bar-fill" style="width:70%; background:#336791; color:#336791;"></div>
          </div>
          <span class="skill-pct">70%</span>
        </div>
        <div class="skill-card">
          <span class="skill-icon" style="color:#4479a1;">🐬</span>
          <span class="skill-name">MySQL</span>
          <div class="skill-bar-track">
            <div class="skill-bar-fill" style="width:75%; background:#4479a1; color:#4479a1;"></div>
          </div>
          <span class="skill-pct">75%</span>
        </div>
        <div class="skill-card">
          <span class="skill-icon" style="color:#f05032;">⎇</span>
          <span class="skill-name">Git</span>
          <div class="skill-bar-track">
            <div class="skill-bar-fill" style="width:75%; background:#f05032; color:#f05032;"></div>
          </div>
          <span class="skill-pct">75%</span>
        </div>
        <div class="skill-card">
          <span class="skill-icon" style="color:#8892bf;">🐘</span>
          <span class="skill-name">PHP</span>
          <div class="skill-bar-track">
            <div class="skill-bar-fill" style="width:65%; background:#8892bf; color:#8892bf;"></div>
          </div>
          <span class="skill-pct">65%</span>
        </div>
        <div class="skill-card">
          <span class="skill-icon" style="color:#3776ab;">🐍</span>
          <span class="skill-name">Python</span>
          <div class="skill-bar-track">
            <div class="skill-bar-fill" style="width:75%; background:#3776ab; color:#3776ab;"></div>
          </div>
          <span class="skill-pct">75%</span>
        </div>
        <div class="skill-card">
          <span class="skill-icon" style="color:#e0234e;">N</span>
          <span class="skill-name">NestJS</span>
          <div class="skill-bar-track">
            <div class="skill-bar-fill" style="width:75%; background:#e0234e; color:#e0234e;"></div>
          </div>
          <span class="skill-pct">75%</span>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- CONTACT -->
<section id="contact">
  <div class="contact-inner">
    <div>
      <div class="section-label reveal">// CONTACTO</div>
      <h2 class="section-title reveal">TRANSMITIR<br>SEÑAL</h2>
      <p style="font-size:15px; color:rgba(200,200,216,0.55); font-weight:300; margin-bottom:36px; font-family:var(--body);" class="reveal">Disponible para proyectos, colaboraciones y nuevas oportunidades.</p>

      <div class="contact-info-items">
        <a href="mailto:mendozadavidprogramacion2.0@gmail.com" class="contact-item reveal">
          <div class="contact-icon">✉</div>
          <div>
            <span class="contact-label">CORREO</span>
            <span class="contact-value">mendozadavidprogramacion2.0@gmail.com</span>
          </div>
        </a>
        <a href="tel:+585184163" class="contact-item reveal" style="transition-delay:0.1s">
          <div class="contact-icon">☎</div>
          <div>
            <span class="contact-label">TELÉFONO</span>
            <span class="contact-value">+58 424-5184163</span>
          </div>
        </a>
        <div class="contact-item reveal" style="transition-delay:0.2s">
          <div class="contact-icon">◎</div>
          <div>
            <span class="contact-label">UBICACIÓN</span>
            <span class="contact-value">Agua Viva, Cabudare · Lara, Venezuela</span>
          </div>
        </div>
        <a href="https://github.com/MendozaDavidprogam" target="_blank" class="contact-item reveal" style="transition-delay:0.3s">
          <div class="contact-icon">⌥</div>
          <div>
            <span class="contact-label">GITHUB</span>
            <span class="contact-value">github.com/MendozaDavidprogam</span>
          </div>
        </a>
      </div>
    </div>

    <div class="contact-form reveal" style="transition-delay:0.2s">
      <label class="form-label">NOMBRE</label>
      <div class="form-group">
        <input type="text" class="form-input" placeholder="Identificador...">
      </div>
      <label class="form-label">CORREO</label>
      <div class="form-group">
        <input type="email" class="form-input" placeholder="señal@dominio.com">
      </div>
      <label class="form-label">MENSAJE</label>
      <div class="form-group">
        <textarea class="form-textarea" placeholder="Transmisión..."></textarea>
      </div>
      <button class="btn-primary" style="width:100%; justify-content:center; margin-top:8px;">▶ ENVIAR TRANSMISIÓN</button>
    </div>
  </div>
</section>

<!-- FOOTER -->
<footer>
  <div class="footer-copy">© 2025 DAVID MENDOZA // TODOS LOS SISTEMAS RESERVADOS</div>
  <div class="footer-status">
    <span class="status-dot"></span>
    ONLINE :: LARA, VE
  </div>
</footer>

<script>
  // Scroll reveal
  const reveals = document.querySelectorAll('.reveal');
  const observer = new IntersectionObserver(entries => {
    entries.forEach((entry, i) => {
      if (entry.isIntersecting) {
        entry.target.classList.add('visible');
        observer.unobserve(entry.target);
      }
    });
  }, { threshold: 0.12 });

  reveals.forEach(el => observer.observe(el));

  // Random glitch flicker
  function randomGlitch() {
    const hero = document.querySelector('.hero-name .line2');
    if (hero) {
      hero.style.textShadow = '3px 0 #00e5ff, -3px 0 #00ff9d, 0 0 40px rgba(200,0,26,0.6)';
      setTimeout(() => {
        hero.style.textShadow = '0 0 40px rgba(200,0,26,0.6), 0 0 80px rgba(200,0,26,0.3)';
      }, 100);
    }
    setTimeout(randomGlitch, Math.random() * 6000 + 3000);
  }
  randomGlitch();

  // Skill bar animation on scroll
  const skillBars = document.querySelectorAll('.skill-bar-fill');
  const widths = [];
  skillBars.forEach(bar => {
    widths.push(bar.style.width);
    bar.style.width = '0%';
  });

  const barObserver = new IntersectionObserver(entries => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        skillBars.forEach((bar, i) => {
          setTimeout(() => { bar.style.width = widths[i]; }, i * 60);
        });
        barObserver.disconnect();
      }
    });
  }, { threshold: 0.3 });

  const skillSection = document.getElementById('skills');
  if (skillSection) barObserver.observe(skillSection);
</script>
</body>
</html>
