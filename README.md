<?xml version="1.0" encoding="utf-8"?>
<svg xmlns="http://www.w3.org/2000/svg" width="1200" height="160" viewBox="0 0 1200 160" preserveAspectRatio="xMidYMid slice">
  <defs>
    <linearGradient id="g" x1="0" x2="1">
      <stop offset="0%" stop-color="#00FF00"/>
      <stop offset="50%" stop-color="#9cff00"/>
      <stop offset="100%" stop-color="#00ffd6"/>
    </linearGradient>
    <filter id="f" x="-20%" y="-20%" width="140%" height="140%">
      <feGaussianBlur stdDeviation="2" result="b"/>
      <feMerge><feMergeNode in="b"/><feMergeNode in="SourceGraphic"/></feMerge>
    </filter>
  </defs>

  <!-- background -->
  <rect width="100%" height="100%" fill="#040404"/>

  <!-- shadow copy for depth -->
  <text x="50%" y="52%" text-anchor="middle" font-family="Share Tech Mono, monospace" font-size="42" fill="#001100" opacity="0.25">
    Mishbahop — Creative Coder | Gamer | Tech Explorer
  </text>

  <!-- base neon -->
  <text id="t" x="50%" y="50%" text-anchor="middle" font-family="Share Tech Mono, monospace" font-size="42" fill="url(#g)" filter="url(#f)" style="letter-spacing:1px">
    Mishbahop — Creative Coder | Gamer | Tech Explorer
  </text>

  <!-- glitch layers -->
  <text x="50%" y="50%" text-anchor="middle" font-family="Share Tech Mono, monospace" font-size="42" fill="#00ff66" style="mix-blend-mode:screen;opacity:0.9">
    <animate attributeName="x" values="50%;49%;51%;50%" dur="3s" repeatCount="indefinite"/>
  Mishbahop — Creative Coder | Gamer | Tech Explorer</text>

  <text x="50%" y="50%" text-anchor="middle" font-family="Share Tech Mono, monospace" font-size="42" fill="#00ffd8" style="opacity:0.6">
    <animate attributeName="x" values="50%;51%;49%;50%" dur="4s" repeatCount="indefinite"/>
  Mishbahop — Creative Coder | Gamer | Tech Explorer</text>

  <!-- scanline -->
  <rect x="0" y="78" width="1200" height="2" fill="#002200" opacity="0.25">
    <animate attributeName="x" from="-1200" to="1200" dur="6s" repeatCount="indefinite"/>
  </rect>
</svg>
