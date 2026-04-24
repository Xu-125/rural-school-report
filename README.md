<!DOCTYPE html>
<html lang="zh-CN">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>故土与新途 · 毕业设计</title>

<!-- 使用国内可访问的字体 CDN（解决 GitHub Pages 在中国访问 Google Fonts 慢/失败问题） -->
<link rel="preconnect" href="https://fonts.font.im">
<link href="https://fonts.font.im/css2?family=Noto+Serif+SC:wght@300;400;500;700;900&family=Noto+Sans+SC:wght@300;400;500;700&family=Cormorant+Garamond:ital,wght@0,300;0,400;0,600;1,400;1,600&display=swap" rel="stylesheet">

<style>
  * { margin:0; padding:0; box-sizing:border-box; }
  :root{
    --bg:#f4f5ee;
    --bg-warm:#ebeadb;
    --bg-dark:#0f1a14;
    --paper:#e6e8d6;
    --ink:#1a2a1f;
    --muted:#5a6b5a;
    --line:#bccab1;
    --accent:#3d6b4a;
    --accent-2:#5a8c5a;
    --leaf:#7ba05b;
    --gold:#a8b85a;
    --moss:#4a6b3a;
  }
  html{scroll-behavior:smooth;}
  body{
    /* 字体 fallback 优化：先用系统中文字体兜底，避免 Google Fonts 加载失败时变丑 */
    font-family: 'Noto Serif SC', 'Source Han Serif SC', 'Songti SC', 'STSong',
                 'PingFang SC', 'Microsoft YaHei', 'SimSun', serif;
    background:var(--bg);
    color:var(--ink);
    line-height:1.7;
    overflow-x:hidden;
    cursor:none;
  }
  ::selection{background:var(--leaf); color:#fff;}

  /* ===== 自定义鼠标光标 ===== */
  .cursor-dot, .cursor-ring{
    position:fixed; top:0; left:0;
    pointer-events:none;
    z-index:9999;
    transform:translate(-50%,-50%);
    transition:opacity .3s;
  }
  .cursor-dot{
    width:6px; height:6px;
    background:var(--accent);
    border-radius:50%;
  }
  .cursor-ring{
    width:36px; height:36px;
    border:1px solid var(--leaf);
    border-radius:50%;
    transition:transform .2s ease, width .3s, height .3s, border-color .3s;
  }
  .cursor-ring.hover{
    width:60px; height:60px;
    border-color:var(--accent);
    background:rgba(123,160,91,0.1);
  }
  @media(max-width:900px){
    body{cursor:auto;}
    .cursor-dot, .cursor-ring{display:none;}
  }

  /* ===== NAV ===== */
  nav{
    position:fixed; top:0; left:0; right:0;
    padding:14px 40px;
    background:rgba(244,245,238,0.85);
    backdrop-filter:blur(12px);
    -webkit-backdrop-filter:blur(12px);
    border-bottom:1px solid var(--line);
    z-index:100;
    display:flex; justify-content:space-between; align-items:center;
    font-size:13px;
    transition:all .4s;
  }
  nav .brand{font-weight:700; letter-spacing:2px; color:var(--accent);}
  nav ul{display:flex; gap:28px; list-style:none;}
  nav a{
    color:var(--muted); text-decoration:none;
    transition:color .3s; position:relative;
  }
  nav a::after{
    content:""; position:absolute; left:0; bottom:-4px;
    width:0; height:1px; background:var(--accent);
    transition:width .3s;
  }
  nav a:hover{color:var(--accent);}
  nav a:hover::after{width:100%;}

  /* ===== HERO ===== */
  .hero{
    min-height:100vh;
    background:
      linear-gradient(180deg, rgba(15,26,20,0.45) 0%, rgba(15,26,20,0.85) 100%),
      url('https://images.unsplash.com/photo-1500382017468-9049fed747ef?w=2000&q=80') center/cover fixed;
    color:#f4f5ee;
    display:flex; flex-direction:column; justify-content:center;
    padding:80px 8vw;
    position:relative;
    overflow:hidden;
  }
  /* 飘叶 */
  .leaf{
    position:absolute;
    width:30px; height:30px;
    opacity:0.4;
    animation:floatLeaf 15s linear infinite;
    pointer-events:none;
  }
  .leaf svg{width:100%; height:100%; fill:#a8b85a;}
  .leaf:nth-child(1){top:10%; left:15%; animation-duration:18s;}
  .leaf:nth-child(2){top:30%; left:80%; animation-duration:22s; animation-delay:-5s; width:20px;height:20px;}
  .leaf:nth-child(3){top:60%; left:25%; animation-duration:25s; animation-delay:-10s; width:25px;height:25px;}
  .leaf:nth-child(4){top:75%; left:70%; animation-duration:20s; animation-delay:-3s;}
  .leaf:nth-child(5){top:20%; left:50%; animation-duration:28s; animation-delay:-15s; width:18px;height:18px;}
  .leaf:nth-child(6){top:50%; left:10%; animation-duration:30s; animation-delay:-7s; width:22px;height:22px;}
  .leaf:nth-child(7){top:85%; left:40%; animation-duration:24s; animation-delay:-12s; width:16px;height:16px;}
  .leaf:nth-child(8){top:15%; left:65%; animation-duration:26s; animation-delay:-18s;}
  @keyframes floatLeaf{
    0%{transform:translate(0,0) rotate(0deg);}
    25%{transform:translate(60px,-40px) rotate(90deg);}
    50%{transform:translate(120px,30px) rotate(180deg);}
    75%{transform:translate(40px,80px) rotate(270deg);}
    100%{transform:translate(0,0) rotate(360deg);}
  }

  /* 鼠标跟随光晕 */
  .hero-glow{
    position:absolute;
    width:500px; height:500px;
    border-radius:50%;
    background:radial-gradient(circle, rgba(168,184,90,0.15), transparent 60%);
    pointer-events:none;
    transform:translate(-50%,-50%);
    transition:opacity .3s;
    z-index:1;
  }

  .hero-content{position:relative; z-index:3;}
  .hero .meta{
    font-size:12px; letter-spacing:6px; color:#bccab1;
    margin-bottom:30px; font-family:'Noto Sans SC', sans-serif;
    opacity:0;
    animation:fadeUp 1s .2s forwards;
  }
  .hero .meta span{color:var(--gold);}
  .hero .badge{
    display:inline-block;
    padding:6px 16px;
    border:1px solid rgba(168,184,90,0.5);
    border-radius:20px;
    font-size:12px;
    font-family:'Noto Sans SC', sans-serif;
    letter-spacing:3px;
    color:var(--gold);
    margin-bottom:30px;
    opacity:0;
    animation:fadeUp 1s .1s forwards;
    backdrop-filter:blur(4px);
  }
  .hero h1{
    font-size:clamp(48px, 9vw, 130px);
    font-weight:900;
    line-height:1.05;
    letter-spacing:4px;
    margin-bottom:30px;
  }
  .hero h1 span{
    display:inline-block;
    opacity:0;
    transform:translateY(60px);
    animation:fadeUp 1.1s forwards;
  }
  .hero h1 span:nth-child(1){animation-delay:.4s;}
  .hero h1 span:nth-child(2){animation-delay:.6s;}
  .hero h1 span:nth-child(3){animation-delay:.8s; color:var(--gold); font-style:italic; font-family:'Cormorant Garamond', 'Noto Serif SC', serif;}
  .hero .sub{
    font-size:clamp(16px, 1.5vw, 20px);
    color:#d8e0c8;
    max-width:680px;
    margin-top:30px;
    line-height:2;
    opacity:0;
    animation:fadeUp 1s 1.2s forwards;
  }
  .hero .author{
    margin-top:50px;
    font-size:14px;
    color:#bccab1;
    font-family:'Noto Sans SC', sans-serif;
    letter-spacing:3px;
    opacity:0;
    animation:fadeUp 1s 1.5s forwards;
    border-top:1px solid rgba(168,184,90,0.3);
    padding-top:20px;
    max-width:400px;
  }
  @keyframes fadeUp{
    to{opacity:1; transform:translateY(0);}
  }
  .hero .scroll{
    position:absolute; bottom:40px; left:50%; transform:translateX(-50%);
    color:#bccab1; font-size:11px; letter-spacing:4px;
    font-family:'Noto Sans SC', sans-serif;
    z-index:2;
    opacity:0;
    animation:fadeUp 1s 1.8s forwards, bounce 2s 2.8s infinite;
  }
  @keyframes bounce{
    0%,100%{transform:translate(-50%,0);} 50%{transform:translate(-50%,12px);}
  }

  /* ===== Reveal ===== */
  .reveal{opacity:0; transform:translateY(40px); transition:opacity .9s ease, transform .9s ease;}
  .reveal.visible{opacity:1; transform:translateY(0);}
  .reveal-delay-1{transition-delay:.15s;}
  .reveal-delay-2{transition-delay:.3s;}
  .reveal-delay-3{transition-delay:.45s;}

  .reveal-left{opacity:0; transform:translateX(-60px); transition:all .9s ease;}
  .reveal-left.visible{opacity:1; transform:translateX(0);}
  .reveal-right{opacity:0; transform:translateX(60px); transition:all .9s ease;}
  .reveal-right.visible{opacity:1; transform:translateX(0);}
  .reveal-scale{opacity:0; transform:scale(0.9); transition:all 1s ease;}
  .reveal-scale.visible{opacity:1; transform:scale(1);}

  /* ===== Section ===== */
  section{padding:120px 8vw; max-width:1400px; margin:0 auto;}
  .section-tag{
    display:inline-block;
    font-family:'Noto Sans SC', sans-serif;
    font-size:11px; letter-spacing:5px;
    color:var(--accent);
    border-top:2px solid var(--accent);
    padding-top:8px;
    margin-bottom:24px;
    position:relative;
    overflow:hidden;
  }
  .section-tag::after{
    content:""; position:absolute; top:-2px; left:-100%;
    width:100%; height:2px;
    background:linear-gradient(90deg, transparent, var(--gold), transparent);
    animation:shine 3s ease-in-out infinite;
  }
  @keyframes shine{
    0%,100%{left:-100%;} 50%{left:100%;}
  }
  .section-title{
    font-size:clamp(36px, 5vw, 64px);
    font-weight:700;
    line-height:1.2;
    margin-bottom:20px;
    letter-spacing:2px;
    color:var(--ink);
  }
  .section-sub{
    font-size:18px; color:var(--muted);
    max-width:700px; margin-bottom:80px;
    line-height:1.9;
  }

  /* ===== TIMELINE ===== */
  .timeline{position:relative; border-top:1px solid var(--line);}
  .timeline::before{
    content:""; position:absolute; left:100px; top:0; bottom:0;
    width:1px; background:linear-gradient(180deg, var(--leaf), transparent);
    opacity:0.4;
  }
  .stage{
    display:grid;
    grid-template-columns:200px 1fr 1fr;
    gap:40px;
    padding:60px 0;
    border-bottom:1px solid var(--line);
    transition:background .5s;
    position:relative;
  }
  .stage::before{
    content:"";
    position:absolute; left:96px; top:80px;
    width:9px; height:9px; border-radius:50%;
    background:var(--leaf);
    box-shadow:0 0 0 4px rgba(123,160,91,0.2);
    transition:all .4s;
  }
  .stage:hover{background:rgba(123,160,91,0.06);}
  .stage:hover::before{
    background:var(--accent);
    box-shadow:0 0 0 8px rgba(61,107,74,0.2);
    transform:scale(1.4);
  }
  .stage-num{
    font-family:'Cormorant Garamond', serif;
    font-size:14px; letter-spacing:4px; color:var(--accent);
  }
  .stage-num .big{
    display:block; font-size:90px; font-weight:300; color:var(--ink);
    line-height:1; margin-top:10px; font-style:italic;
    transition:color .4s, transform .4s;
  }
  .stage:hover .stage-num .big{color:var(--accent); transform:translateX(8px);}
  .stage-num .years{
    display:block; color:var(--muted); font-size:13px;
    margin-top:12px; font-family:'Noto Sans SC', sans-serif;
  }
  .stage-content h3{font-size:24px; font-weight:700; margin-bottom:14px;}
  .stage-content .core{
    font-size:14px; color:var(--accent); font-family:'Noto Sans SC', sans-serif;
    margin-bottom:18px; padding-left:12px; border-left:2px solid var(--accent);
  }
  .stage-content ul{list-style:none; font-size:14px; color:var(--muted); line-height:1.9;}
  .stage-content ul li{margin-bottom:8px; padding-left:14px; position:relative;}
  .stage-content ul li:before{content:"›"; position:absolute; left:0; color:var(--leaf); font-weight:700;}
  .stage-content .feature{
    margin-top:20px; padding:14px 18px;
    background:rgba(123,160,91,0.1); border-left:3px solid var(--leaf);
    font-size:13px; color:var(--ink); transition:transform .3s;
  }
  .stage:hover .stage-content .feature{transform:translateX(6px);}
  .stage-data{
    background:var(--paper); padding:30px; border-radius:2px;
    transition:transform .4s, box-shadow .4s;
  }
  .stage:hover .stage-data{
    transform:translateY(-4px);
    box-shadow:0 20px 40px rgba(61,107,74,0.12);
  }
  .stage-data .data-label{
    font-family:'Noto Sans SC', sans-serif;
    font-size:11px; letter-spacing:3px; color:var(--muted); margin-bottom:18px;
  }
  .stage-data .data-num{
    font-family:'Cormorant Garamond', serif;
    font-size:54px; font-weight:600; color:var(--accent);
    line-height:1; margin-bottom:6px;
  }
  .stage-data .data-num .small{font-size:20px; color:var(--ink);}
  .stage-data .data-desc{font-size:13px; color:var(--ink); margin-bottom:18px; line-height:1.7;}
  .stage-data .data-bar{height:6px; background:#d4d8c0; border-radius:3px; margin:14px 0; overflow:hidden;}
  .stage-data .data-bar span{
    display:block; height:100%; width:0;
    background:linear-gradient(90deg,var(--leaf),var(--accent));
    transition:width 1.8s ease;
  }
  .stage-data.visible .data-bar span{width:var(--w);}
  .stage-data ul{list-style:none; font-size:13px; color:var(--muted); line-height:1.9; margin-top:10px;}
  .stage-data ul li{padding:4px 0; border-bottom:1px dashed var(--line);}

  /* ===== CASE ===== */
  .case{background:var(--bg-dark); color:#dde4d2; padding:0; max-width:none; margin:0;}
  .case-hero{
    min-height:80vh; padding:120px 8vw;
    display:flex; flex-direction:column; justify-content:center;
    position:relative; overflow:hidden;
  }
  .case-hero.shaanxi{
    background:
      linear-gradient(90deg, rgba(15,26,20,0.92) 30%, rgba(15,26,20,0.4) 100%),
      url('https://images.unsplash.com/photo-1464822759023-fed622ff2c3b?w=2000&q=80') center/cover;
  }
  .case-hero.hunan{
    background:
      linear-gradient(90deg, rgba(15,26,20,0.92) 30%, rgba(15,26,20,0.4) 100%),
      url('https://images.unsplash.com/photo-1470770841072-f978cf4d019e?w=2000&q=80') center/cover;
  }
  .case-hero.scholars{
    background:
      linear-gradient(90deg, rgba(15,26,20,0.92) 30%, rgba(15,26,20,0.4) 100%),
      url('https://images.unsplash.com/photo-1481627834876-b7833e8f5570?w=2000&q=80') center/cover;
  }
  .case-hero::after{
    content:""; position:absolute; inset:0;
    background:radial-gradient(circle at 70% 50%, transparent, rgba(15,26,20,0.4));
    pointer-events:none;
  }
  .case-hero > *{position:relative; z-index:2;}
  .case-hero .place{
    font-family:'Cormorant Garamond', serif;
    font-size:14px; letter-spacing:8px; color:var(--gold); margin-bottom:24px;
  }
  .case-hero h2{
    font-size:clamp(40px, 6vw, 80px); font-weight:700;
    line-height:1.2; margin-bottom:20px; letter-spacing:3px; color:#f4f5ee;
  }
  .case-hero .case-sub{
    font-size:18px; color:#b8c5a8; max-width:600px;
    border-left:3px solid var(--gold); padding-left:20px; margin-top:30px;
  }
  /* 案例封面装饰元素 */
  .case-deco{
    position:absolute; right:8vw; top:50%; transform:translateY(-50%);
    width:300px; height:300px; opacity:0.15;
    z-index:1;
  }
  .case-deco svg{width:100%; height:100%;}
  .case-deco .ring{
    fill:none; stroke:var(--gold); stroke-width:1;
    transform-origin:center;
    animation:rotate 30s linear infinite;
  }
  .case-deco .ring2{animation-direction:reverse; animation-duration:40s;}
  @keyframes rotate{
    to{transform:rotate(360deg);}
  }
  @media(max-width:900px){.case-deco{display:none;}}

  .case-body{padding:100px 8vw; max-width:1400px; margin:0 auto;}
  .case-quote{
    font-size:clamp(22px, 2.5vw, 32px); font-weight:300; line-height:1.7;
    color:#e8efd8; margin-bottom:80px; padding:40px 60px;
    border-left:2px solid var(--gold); font-family:'Noto Serif SC', serif;
  }
  .case-quote em{color:var(--gold); font-style:normal;}
  .school-grid{
    display:grid; grid-template-columns:repeat(auto-fit,minmax(320px,1fr));
    gap:30px; margin-bottom:80px;
  }
  .school-card{
    background:rgba(255,255,255,0.04);
    border:1px solid rgba(168,184,90,0.15);
    padding:36px 30px;
    transition:all .5s cubic-bezier(.2,.8,.2,1);
    position:relative; overflow:hidden;
  }
  .school-card::before{
    content:""; position:absolute; top:0; left:-100%;
    width:100%; height:100%;
    background:linear-gradient(90deg, transparent, rgba(168,184,90,0.08), transparent);
    transition:left .8s;
  }
  .school-card:hover::before{left:100%;}
  .school-card:hover{
    transform:translateY(-8px); border-color:var(--gold);
    background:rgba(168,184,90,0.06); box-shadow:0 20px 40px rgba(0,0,0,0.3);
  }
  .school-card .num{
    position:absolute; top:20px; right:24px;
    font-family:'Cormorant Garamond', serif;
    font-size:48px; color:var(--gold); opacity:0.4; font-style:italic;
    transition:transform .4s, opacity .4s;
  }
  .school-card:hover .num{transform:scale(1.2) rotate(-5deg); opacity:0.8;}
  .school-card h4{font-size:22px; font-weight:700; margin-bottom:8px; color:#f4f5ee;}
  .school-card .school-tag{
    font-family:'Noto Sans SC', sans-serif;
    font-size:11px; letter-spacing:3px; color:var(--gold); margin-bottom:20px;
  }
  .school-card ul{list-style:none; font-size:14px; color:#b8c5a8; line-height:1.9;}
  .school-card ul li{padding-left:16px; position:relative; margin-bottom:6px;}
  .school-card ul li:before{content:"—"; position:absolute; left:0; color:var(--leaf);}

  .kid-section{margin-top:60px;}
  .kid-section h3{
    font-size:24px; margin-bottom:30px; color:#f4f5ee; font-weight:500;
    border-bottom:1px solid rgba(168,184,90,0.2); padding-bottom:14px;
  }
  .kid-grid{
    display:grid; grid-template-columns:repeat(auto-fit,minmax(260px,1fr)); gap:20px;
  }
  .kid-card{
    background:rgba(0,0,0,0.25); padding:24px;
    border-top:2px solid var(--leaf); transition:all .4s;
  }
  .kid-card:hover{
    background:rgba(168,184,90,0.08); border-top-color:var(--gold);
    transform:translateY(-4px);
  }
  .kid-card .kid-name{font-size:18px; font-weight:700; color:var(--gold); margin-bottom:10px;}
  .kid-card p{font-size:13px; color:#b8c5a8; line-height:1.8;}

  .case-end{
    text-align:center; margin-top:80px; padding-top:60px;
    border-top:1px solid rgba(168,184,90,0.15);
  }
  .case-end p{font-size:18px; color:#b8c5a8; margin-bottom:10px; font-weight:300;}
  .case-end .big-line{
    font-size:28px; color:var(--gold); font-weight:500;
    margin-top:20px; letter-spacing:2px;
  }

  .stat-row{
    display:grid; grid-template-columns:repeat(4,1fr); gap:30px;
    margin:60px 0; padding:40px 0;
    border-top:1px solid rgba(168,184,90,0.15);
    border-bottom:1px solid rgba(168,184,90,0.15);
  }
  .stat-item{text-align:center;}
  .stat-item .stat-num{
    font-family:'Cormorant Garamond', serif;
    font-size:54px; color:var(--gold); font-weight:600; line-height:1;
    display:inline-block; transition:transform .3s;
  }
  .stat-item:hover .stat-num{transform:scale(1.15); color:#d4e296;}
  .stat-item .stat-label{
    font-size:12px; color:#b8c5a8; letter-spacing:3px; margin-top:10px;
    font-family:'Noto Sans SC', sans-serif;
  }

  /* ===== VOICES ===== */
  .voices-section{background:linear-gradient(180deg, var(--bg) 0%, var(--bg-warm) 100%);}
  .voices-grid{
    display:grid; grid-template-columns:repeat(auto-fill,minmax(300px,1fr));
    gap:24px; grid-auto-flow:dense;
  }
  .voice-card{
    background:#fff; padding:30px; cursor:pointer;
    transition:all .5s cubic-bezier(.2,.8,.2,1);
    border:1px solid var(--line);
    position:relative; overflow:hidden; border-radius:4px;
  }
  .voice-card::before{
    content:"❝"; position:absolute; top:-15px; right:20px;
    font-size:90px; color:var(--leaf); opacity:0.15;
    font-family:serif; transition:transform .5s, opacity .5s;
  }
  .voice-card:hover::before{transform:rotate(10deg) scale(1.1); opacity:0.3;}
  .voice-card:hover{
    border-color:var(--accent); transform:translateY(-6px);
    box-shadow:0 24px 50px rgba(61,107,74,0.15);
  }
  .voice-card.expanded{
    grid-column:span 2;
    background:linear-gradient(135deg, var(--paper), #fff);
    border-color:var(--accent);
    box-shadow:0 30px 60px rgba(61,107,74,0.2);
    transform:translateY(-6px);
  }
  @media(max-width:700px){.voice-card.expanded{grid-column:span 1;}}
  .voice-card .v-name{font-size:22px; font-weight:700; color:var(--ink); margin-bottom:6px;}
  .voice-card .v-role{
    font-size:12px; color:var(--accent); font-family:'Noto Sans SC', sans-serif;
    letter-spacing:1px; margin-bottom:18px; padding-bottom:14px;
    border-bottom:1px dashed var(--line);
  }
  .voice-card .v-preview{font-size:14px; color:var(--muted); line-height:1.8; font-style:italic;}
  .voice-card .v-expand{
    max-height:0; overflow:hidden; opacity:0;
    transition:max-height .6s ease, opacity .5s ease, margin .5s ease;
  }
  .voice-card.expanded .v-expand{max-height:500px; opacity:1; margin-top:20px;}
  .voice-card.expanded .v-preview{display:none;}
  .voice-card .v-expand p{
    font-size:16px; line-height:2; color:var(--ink);
    padding:14px 0 14px 20px;
    border-left:3px solid var(--leaf);
    margin-bottom:14px;
    background:rgba(123,160,91,0.05);
    padding-right:16px;
  }
  .voice-card .v-toggle{
    font-size:11px; color:var(--accent); margin-top:16px;
    letter-spacing:3px; font-family:'Noto Sans SC', sans-serif;
    display:flex; align-items:center; gap:8px;
  }
  .voice-card .v-toggle .icon{
    display:inline-block; width:18px; height:18px;
    border:1px solid var(--accent); border-radius:50%;
    text-align:center; line-height:16px; font-size:14px;
    transition:transform .4s;
  }
  .voice-card.expanded .v-toggle .icon{
    transform:rotate(45deg); background:var(--accent); color:#fff;
  }

  /* ===== SCHOLARS ===== */
  .scholars-section{
    background:var(--paper);
    position:relative; overflow:hidden;
  }
  .scholars-section::before{
    content:""; position:absolute; top:-100px; right:-100px;
    width:400px; height:400px;
    background:radial-gradient(circle, rgba(123,160,91,0.15), transparent 70%);
    border-radius:50%;
  }
  .scholar{
    display:grid; grid-template-columns:1fr 2fr; gap:60px;
    padding:60px 0; border-bottom:1px solid var(--line);
    align-items:start; position:relative;
  }
  .scholar:last-child{border-bottom:none;}
  .scholar .s-info h4{font-size:32px; margin-bottom:8px; transition:color .3s;}
  .scholar:hover .s-info h4{color:var(--accent);}
  .scholar .s-info .s-title{
    font-size:13px; color:var(--accent); font-family:'Noto Sans SC', sans-serif; letter-spacing:2px;
  }
  .scholar .s-info .s-num{
    font-family:'Cormorant Garamond', serif;
    font-size:80px; font-weight:300; color:var(--leaf);
    font-style:italic; line-height:1;
    margin-bottom:20px; opacity:0.5;
  }
  .scholar .s-content p{font-size:16px; color:var(--ink); line-height:2; margin-bottom:24px;}
  .scholar .s-content .pull{
    font-size:22px; color:var(--accent); font-weight:500; line-height:1.7;
    padding:24px 30px; background:#fff;
    border-left:4px solid var(--leaf); margin-top:20px;
    transition:all .4s; position:relative;
  }
  .scholar:hover .s-content .pull{
    border-left-color:var(--accent); transform:translateX(8px);
    box-shadow:0 12px 30px rgba(61,107,74,0.1);
  }

  /* ===== FOOTER ===== */
  footer{
    background:var(--bg-dark); color:#b8c5a8;
    padding:120px 8vw 60px; text-align:center;
    position:relative; overflow:hidden;
  }
  footer::before{
    content:""; position:absolute; bottom:0; left:0; right:0; height:60%;
    background:radial-gradient(ellipse at center bottom, rgba(123,160,91,0.15), transparent 70%);
    pointer-events:none;
  }
  footer .foot-title{
    font-size:clamp(28px, 4vw, 48px); color:#f4f5ee;
    font-weight:300; line-height:1.6; margin-bottom:40px;
    max-width:800px; margin-left:auto; margin-right:auto; position:relative;
  }
  footer .foot-title em{color:var(--gold); font-style:normal; font-weight:500;}
  footer .credits{
    font-size:13px; color:#7a8a7a; margin-top:60px;
    padding-top:30px; border-top:1px solid #2a3a2a;
    letter-spacing:2px; position:relative;
  }
  footer .credits strong{color:var(--gold);}

  /* progress bar */
  .progress{
    position:fixed; top:0; left:0; height:3px;
    background:linear-gradient(90deg, var(--leaf), var(--accent));
    width:0; z-index:999; transition:width .1s;
  }

  /* 章节序章特效 - 文字逐字出现 */
  .text-stagger span{
    display:inline-block; opacity:0; transform:translateY(20px);
    transition:all .6s ease;
  }
  .text-stagger.visible span{opacity:1; transform:translateY(0);}

  /* 数据条上的脉冲点 */
  .pulse-dot{
    display:inline-block; width:8px; height:8px; border-radius:50%;
    background:var(--leaf); margin-right:8px;
    animation:pulse 2s infinite;
  }
  @keyframes pulse{
    0%,100%{box-shadow:0 0 0 0 rgba(123,160,91,0.6);}
    50%{box-shadow:0 0 0 8px rgba(123,160,91,0);}
  }

  /* 滚动到底部时的章节切换提示 */
  .chapter-transition{
    text-align:center; padding:40px 0;
    color:var(--muted); font-size:12px; letter-spacing:4px;
    font-family:'Noto Sans SC', sans-serif;
  }
  .chapter-transition::before{
    content:""; display:block; width:1px; height:60px;
    background:linear-gradient(180deg, transparent, var(--leaf));
    margin:0 auto 20px;
  }

  /* ===== RESPONSIVE ===== */
  @media(max-width:900px){
    nav{padding:14px 20px;}
    nav ul{display:none;}
    section{padding:80px 6vw;}
    .stage{grid-template-columns:1fr; gap:20px;}
    .timeline::before{left:0;}
    .stage::before{left:-4px; top:60px;}
    .scholar{grid-template-columns:1fr; gap:20px;}
    .stat-row{grid-template-columns:repeat(2,1fr);}
    .case-quote{padding:20px 24px;}
  }
</style>
</head>
<body>

<!-- 自定义鼠标光标 -->
<div class="cursor-dot" id="cursorDot"></div>
<div class="cursor-ring" id="cursorRing"></div>

<div class="progress" id="progress"></div>

<nav>
  <div class="brand">毕业设计 · GRADUATION PROJECT</div>
  <ul>
    <li><a href="#policy">政策</a></li>
    <li><a href="#shaanxi">陕西</a></li>
    <li><a href="#hunan">湖南</a></li>
    <li><a href="#voices">声音</a></li>
    <li><a href="#scholars">观点</a></li>
  </ul>
</nav>

<!-- ===== HERO ===== -->
<header class="hero">
  <div class="hero-glow" id="heroGlow"></div>

  <div class="leaf"><svg viewBox="0 0 24 24"><path d="M17 8C8 10 5.9 16.17 3.82 21.34l1.89.66.95-2.3c.48.17.98.3 1.34.3C19 20 22 3 22 3c-1 2-8 2.25-13 3.25S2 11.5 2 13.5s1.75 3.75 1.75 3.75C7 8 17 8 17 8z"/></svg></div>
  <div class="leaf"><svg viewBox="0 0 24 24"><path d="M17 8C8 10 5.9 16.17 3.82 21.34l1.89.66.95-2.3c.48.17.98.3 1.34.3C19 20 22 3 22 3c-1 2-8 2.25-13 3.25S2 11.5 2 13.5s1.75 3.75 1.75 3.75C7 8 17 8 17 8z"/></svg></div>
  <div class="leaf"><svg viewBox="0 0 24 24"><path d="M17 8C8 10 5.9 16.17 3.82 21.34l1.89.66.95-2.3c.48.17.98.3 1.34.3C19 20 22 3 22 3c-1 2-8 2.25-13 3.25S2 11.5 2 13.5s1.75 3.75 1.75 3.75C7 8 17 8 17 8z"/></svg></div>
  <div class="leaf"><svg viewBox="0 0 24 24"><path d="M17 8C8 10 5.9 16.17 3.82 21.34l1.89.66.95-2.3c.48.17.98.3 1.34.3C19 20 22 3 22 3c-1 2-8 2.25-13 3.25S2 11.5 2 13.5s1.75 3.75 1.75 3.75C7 8 17 8 17 8z"/></svg></div>
  <div class="leaf"><svg viewBox="0 0 24 24"><path d="M17 8C8 10 5.9 16.17 3.82 21.34l1.89.66.95-2.3c.48.17.98.3 1.34.3C19 20 22 3 22 3c-1 2-8 2.25-13 3.25S2 11.5 2 13.5s1.75 3.75 1.75 3.75C7 8 17 8 17 8z"/></svg></div>
  <div class="leaf"><svg viewBox="0 0 24 24"><path d="M17 8C8 10 5.9 16.17 3.82 21.34l1.89.66.95-2.3c.48.17.98.3 1.34.3C19 20 22 3 22 3c-1 2-8 2.25-13 3.25S2 11.5 2 13.5s1.75 3.75 1.75 3.75C7 8 17 8 17 8z"/></svg></div>
  <div class="leaf"><svg viewBox="0 0 24 24"><path d="M17 8C8 10 5.9 16.17 3.82 21.34l1.89.66.95-2.3c.48.17.98.3 1.34.3C19 20 22 3 22 3c-1 2-8 2.25-13 3.25S2 11.5 2 13.5s1.75 3.75 1.75 3.75C7 8 17 8 17 8z"/></svg></div>
  <div class="leaf"><svg viewBox="0 0 24 24"><path d="M17 8C8 10 5.9 16.17 3.82 21.34l1.89.66.95-2.3c.48.17.98.3 1.34.3C19 20 22 3 22 3c-1 2-8 2.25-13 3.25S2 11.5 2 13.5s1.75 3.75 1.75 3.75C7 8 17 8 17 8z"/></svg></div>

  <div class="hero-content">
    <div class="badge">文学与新闻传播学院 · 2022 级本科生毕业设计</div>
    <div class="meta">DEEP REPORT · <span>RURAL PRIMARY SCHOOLS IN CHINA</span></div>
    <h1><span>故土</span><span>与新途</span><br><span>乡村小学的撤并倒计时</span></h1>
    <p class="sub">从 1997 年的 51.3 万所到 2023 年的 7.06 万所，一代人的求学迁徙正在悄然完成。当政策从"能撤尽撤"转向"应留必留"，村小的命运仍在城镇化的浪潮中艰难选择。</p>
    <div class="author">
      文学与新闻传播学院 &nbsp;·&nbsp; 2022 级本科生毕业设计作品
    </div>
  </div>
  <div class="scroll">SCROLL ↓</div>
</header>

<!-- ===== POLICY ===== -->
<section id="policy">
  <div class="reveal"><div class="section-tag">CHAPTER 01 · 时间轴</div></div>
  <h2 class="section-title reveal">政策的演变，<br>数据的起伏</h2>
  <p class="section-sub reveal reveal-delay-1">四十年间，撤点并校政策经历了从萌芽、提速、纠偏到稳慎的四个阶段。每一次转向背后，都是数十万所乡村小学的命运浮沉。</p>

  <div class="timeline">
    <div class="stage reveal">
      <div class="stage-num">STAGE<span class="big">01</span><span class="years">1980s — 2000<br>初步萌芽</span></div>
      <div class="stage-content">
        <h3>规模效益的初次试水</h3>
        <div class="core">主张规模效益，改变"村村有小学"分散格局</div>
        <ul>
          <li>1985 年 国务院《关于教育体制改革的决定》</li>
          <li>1998 年 教育部在东部试点学校布局优化</li>
          <li>2000 年 国务院部署农村税费改革，同步推进布局优化</li>
        </ul>
        <div class="feature">局部试点、非强制、以提升办学效益为目标</div>
      </div>
      <div class="stage-data" style="--w:100%">
        <div class="data-label"><span class="pulse-dot"></span>FOUNDATIONAL DATA</div>
        <div class="data-num">51.3<span class="small">万所</span></div>
        <div class="data-desc">1997 年全国乡村小学总数<br>班级数 305 万个</div>
        <div class="data-bar"><span></span></div>
        <ul>
          <li>2000 年 · 全国农村小学 44.7 万所</li>
          <li>逐步进入调整通道</li>
        </ul>
      </div>
    </div>

    <div class="stage reveal">
      <div class="stage-num">STAGE<span class="big">02</span><span class="years">2001 — 2005<br>成型提速</span></div>
      <div class="stage-content">
        <h3>自上而下的强力推进</h3>
        <div class="core">鼓励推进，集中资源</div>
        <ul>
          <li>2001 年 国务院《关于基础教育改革与发展的决定》</li>
          <li>2003 年 财政部《中小学布局调整专项资金管理办法》</li>
        </ul>
        <div class="feature">部分地区出现"一刀切""盲目撤并"现象</div>
      </div>
      <div class="stage-data" style="--w:80%">
        <div class="data-label"><span class="pulse-dot"></span>RAPID DECLINE</div>
        <div class="data-num">-22.94<span class="small">万所</span></div>
        <div class="data-desc">2000—2010 农村小学十年净减<br>从 44.7 万 → 21.8 万</div>
        <div class="data-bar"><span></span></div>
        <ul>
          <li>日均消失 63 所乡村小学</li>
          <li>教学点减少 11.1 万个，减幅 60%</li>
          <li>每消失 1 所城镇小学 = 15 所乡村小学</li>
        </ul>
      </div>
    </div>

    <div class="stage reveal">
      <div class="stage-num">STAGE<span class="big">03</span><span class="years">2006 — 2012<br>变形纠偏</span></div>
      <div class="stage-content">
        <h3>紧急刹车与制度补救</h3>
        <div class="core">坚决制止盲目撤并，规范撤并程序</div>
        <ul>
          <li>2006 年 教育部关于上学远问题的通知</li>
          <li>2010 年 推进义务教育均衡发展</li>
          <li>2012 年 国务院办公厅《规范布局调整意见》——紧急叫停</li>
        </ul>
        <div class="feature">建立百人以下村小经费托底机制；撤并必须论证、公示、听证</div>
      </div>
      <div class="stage-data" style="--w:30%">
        <div class="data-label"><span class="pulse-dot"></span>EMERGENCY BRAKE</div>
        <div class="data-num">15.5<span class="small">万所</span></div>
        <div class="data-desc">2012 年乡村小学存量<br>政策刹车后消亡惯性仍在</div>
        <div class="data-bar"><span></span></div>
        <ul>
          <li>2001—2011 累计减少超 26 万所</li>
          <li>减幅超 60%</li>
        </ul>
      </div>
    </div>

    <div class="stage reveal">
      <div class="stage-num">STAGE<span class="big">04</span><span class="years">2013 — 2026<br>稳慎优化</span></div>
      <div class="stage-content">
        <h3>从"能撤尽撤"到"应留必留"</h3>
        <div class="core">审慎推进，按需保留，民生优先</div>
        <ul>
          <li>2018 年后 中央多次强调"办好必要的乡村小规模学校"</li>
          <li>2025 年《教育强国建设规划纲要》</li>
          <li>2026 年中央一号文件：稳慎优化布局</li>
        </ul>
        <div class="feature">从"能撤尽撤"转向"应留必留、先建后撤"</div>
      </div>
      <div class="stage-data" style="--w:14%">
        <div class="data-label"><span class="pulse-dot"></span>CURRENT STATE</div>
        <div class="data-num">7.06<span class="small">万所</span></div>
        <div class="data-desc">2023 年乡村小学存量<br>较 1997 年降幅 86.2%</div>
        <div class="data-bar"><span></span></div>
        <ul>
          <li>2018—2024 教学点 10.14 万 → 5.22 万</li>
          <li>日均仍有 22 所村小停办</li>
          <li>2001—2023 缩减超 80%</li>
        </ul>
      </div>
    </div>
  </div>
</section>

<!-- ===== SHAANXI ===== -->
<div class="case" id="shaanxi">
  <div class="case-hero shaanxi">
    <div class="case-deco">
      <svg viewBox="0 0 200 200">
        <circle class="ring" cx="100" cy="100" r="80"/>
        <circle class="ring ring2" cx="100" cy="100" r="60"/>
        <circle class="ring" cx="100" cy="100" r="40"/>
      </svg>
    </div>
    <div class="place reveal-left">陕西 · SHAANXI</div>
    <h2 class="reveal-left reveal-delay-1">一代人的<br>求学迁徙</h2>
    <p class="case-sub reveal-left reveal-delay-2">兴平·丰仪·策村——被时间与生源慢慢掏空的村小</p>
  </div>
  <div class="case-body">
    <p class="case-quote reveal">一堵堵水泥墙封死校门，一间间校舍变成<em>辣椒加工厂、仓库、厂房</em>。<br>三所学校，三段消亡样本。</p>

    <div class="school-grid">
      <div class="school-card reveal-scale">
        <span class="num">01</span>
        <div class="school-tag">苟延残喘</div>
        <h4>策村小学</h4>
        <ul>
          <li>全校 80 余名学生，6 个年级</li>
          <li>一年级 6 人，二年级 14-16 人</li>
          <li>教师 11 人，普遍一人教多科</li>
          <li>张娜：16 年教龄，负责英语和科学两科</li>
          <li>硬件改善，但留不住生源</li>
        </ul>
      </div>
      <div class="school-card reveal-scale reveal-delay-1">
        <span class="num">02</span>
        <div class="school-tag">水泥封门</div>
        <h4>周村小学</h4>
        <ul>
          <li>村民集资建校，关停未充分告知</li>
          <li>校舍被租给辣椒厂</li>
          <li>校门用水泥封死</li>
          <li>丰仪镇：从 16 村 16 校 → 仅剩 4 所</li>
        </ul>
      </div>
      <div class="school-card reveal-scale reveal-delay-2">
        <span class="num">03</span>
        <div class="school-tag">借钱建校</div>
        <h4>水道口小学</h4>
        <ul>
          <li>2003 年 韩怀生自借 5 万启动</li>
          <li>巅峰：覆盖 6 村，600 多学生，8 辆校车</li>
          <li>2014 年 生源枯竭正式关停</li>
          <li>之后转为民办，以新身份存续</li>
        </ul>
      </div>
    </div>

    <p class="case-quote reveal">能走的都走了，<em>留下的，是最走不掉的孩子。</em></p>

    <div class="kid-section">
      <h3 class="reveal">那些留下来的孩子</h3>
      <div class="kid-grid">
        <div class="kid-card reveal-left">
          <div class="kid-name">杨嘉祺</div>
          <p>转学 4 次，5 岁到深圳，10 岁回陕西。有家暴、自残经历，极度缺乏归属感。</p>
        </div>
        <div class="kid-card reveal-right reveal-delay-1">
          <div class="kid-name">多数孩子</div>
          <p>留守儿童，老人抚养，管不了功课，也管不了心理。</p>
        </div>
      </div>
    </div>

    <div class="case-end reveal">
      <p>黄土高原的风，吹过一间间空下来的教室。</p>
      <p>有人在坚守，有人在告别，有人在无奈，有人在等待。</p>
      <div class="big-line">村庄可以老去，但孩子的未来，必须有路可走。</div>
    </div>
  </div>
</div>

<!-- ===== HUNAN ===== -->
<div class="case" id="hunan">
  <div class="case-hero hunan">
    <div class="case-deco">
      <svg viewBox="0 0 200 200">
        <circle class="ring" cx="100" cy="100" r="80"/>
        <circle class="ring ring2" cx="100" cy="100" r="60"/>
        <circle class="ring" cx="100" cy="100" r="40"/>
      </svg>
    </div>
    <div class="place reveal-left">湖南 · HUNAN</div>
    <h2 class="reveal-left reveal-delay-1">群山褶皱里<br>告别最后一学期</h2>
    <p class="case-sub reveal-left reveal-delay-2">娄底·云山——所有人都知道：这是最后一程</p>
  </div>
  <div class="case-body">
    <p class="case-quote reveal">没有红头文件，没有公开宣告。<br>但所有人都知道：这所<em>近百年校史</em>的村小，已经进入倒计时。</p>

    <div class="stat-row reveal">
      <div class="stat-item"><div class="stat-num" data-count="300">0</div><div class="stat-label">鼎盛人数</div></div>
      <div class="stat-item"><div class="stat-num" data-count="14">0</div><div class="stat-label">如今学生</div></div>
      <div class="stat-item"><div class="stat-num" data-count="4">0</div><div class="stat-label">老师</div></div>
      <div class="stat-item"><div class="stat-num" data-count="1">0</div><div class="stat-label">保安</div></div>
    </div>

    <p class="reveal" style="font-size:18px; color:#b8c5a8; max-width:700px; line-height:2; margin-bottom:60px;">
      硬件困境：三层教学楼仅 2 间教室在用，投影仪使用 10 多年，屏幕泛绿。<br>
      一年级不足 5 人无法开班——这不是衰落，是<em style="color:var(--gold);font-style:normal;">结构性消失</em>。
    </p>

    <div class="kid-section">
      <h3 class="reveal">最后 14 个孩子，在告别中长大</h3>
      <div class="kid-grid">
        <div class="kid-card reveal-scale"><div class="kid-name">曾湘欧</div><p>母亲离家，父亲打工，爷爷疏于看管。曾喝墨水、爬栏杆，情绪冲动缺乏引导。</p></div>
        <div class="kid-card reveal-scale reveal-delay-1"><div class="kid-name">曾皓轩</div><p>父母离异，经历"家暴"，因为母亲吃回吐出的东西而患胃病。</p></div>
        <div class="kid-card reveal-scale reveal-delay-2"><div class="kid-name">廖雨辰</div><p>家庭关系复杂，常年住校跟校长生活，自理早熟，像小大人一样处理班级矛盾。</p></div>
        <div class="kid-card reveal-scale reveal-delay-3"><div class="kid-name">曾景桐</div><p>脑瘫学生，学校每月上门两次提供教学，守住义务教育底线。</p></div>
      </div>
    </div>

    <div class="kid-section">
      <h3 class="reveal">在废墟上维持秩序的他们</h3>
      <div class="school-grid">
        <div class="school-card reveal-left">
          <span class="num">A</span>
          <div class="school-tag">21岁的校长</div>
          <h4>尹佳绮</h4>
          <ul>
            <li>00 后校长，2005 年生，公费师范生</li>
            <li>6 个身份：校长 + 班主任 + 语文 + 音乐 + 行政 + 技术</li>
            <li>2 套课表：一套应付检查，一套照顾老教师</li>
            <li>住校守校</li>
          </ul>
        </div>
        <div class="school-card reveal-right reveal-delay-1">
          <span class="num">B</span>
          <div class="school-tag">41年教龄</div>
          <h4>曾良平</h4>
          <ul>
            <li>62 岁，见证云山学校的发展</li>
            <li>指出形式主义占用教学时间</li>
            <li>最担心农村孩子因学校撤并而失学</li>
          </ul>
        </div>
      </div>
    </div>

    <div class="case-end reveal">
      <p>本学期结束，雨石学校将正式并入中心校。</p>
      <p>从 300 人到 14 人，从书声琅琅到空楼寂寂。</p>
      <div class="big-line">春雨还在下，告别已无声。</div>
    </div>
  </div>
</div>

<!-- ===== VOICES ===== -->
<div class="voices-section">
<section id="voices">
  <div class="reveal"><div class="section-tag">CHAPTER 02 · 众声</div></div>
  <h2 class="section-title reveal">还有更多声音</h2>
  <p class="section-sub reveal reveal-delay-1">他们的话，就是村小的真实命运。<strong style="color:var(--accent);">点击卡片</strong>，倾听完整语录。</p>
  <div class="voices-grid" id="voicesGrid"></div>
</section>
</div>

<!-- ===== SCHOLARS COVER ===== -->
<div class="case">
  <div class="case-hero scholars">
    <div class="case-deco">
      <svg viewBox="0 0 200 200">
        <circle class="ring" cx="100" cy="100" r="80"/>
        <circle class="ring ring2" cx="100" cy="100" r="60"/>
        <circle class="ring" cx="100" cy="100" r="40"/>
      </svg>
    </div>
    <div class="place reveal-left">CHAPTER 03 · 学者视角</div>
    <h2 class="reveal-left reveal-delay-1">不只是<br>"撤"或"留"</h2>
    <p class="case-sub reveal-left reveal-delay-2">在数字与情感之间，三位研究者给出的另一种思考路径</p>
  </div>
</div>

<!-- ===== SCHOLARS ===== -->
<div class="scholars-section">
<section id="scholars">

  <div class="scholar reveal">
    <div class="s-info">
      <div class="s-num">01</div>
      <h4>赵小旺</h4>
      <div class="s-title">兴平市教育局基础教育科科长</div>
    </div>
    <div class="s-content">
      <p>当前不少乡村小学的消失，并非单纯由政策推动，而是人口流动、生源减少和家长择校共同作用下的"自然消亡"。但撤并不能只按人数和效率推进，还应考虑家庭接送能力、困难儿童的就学条件，以及村民对学校这一公共资产的情感与权益。</p>
      <div class="pull">"撤并不能只看数字，更要看最后一个孩子还能不能上学。"</div>
    </div>
  </div>

  <div class="scholar reveal">
    <div class="s-info">
      <div class="s-num">02</div>
      <h4>王学男</h4>
      <div class="s-title">中国教育科学研究院副研究员</div>
    </div>
    <div class="s-content">
      <p>中国乡村教育已进入"后撤并时代"。政策重点不再是大规模压缩乡村小学，而是根据实际需求保留必要的小规模学校，并探索更灵活的办学方式。未来的乡村学校未必追求"大而全"，而可能转向"小规模、综合化、开放式"的教育空间。</p>
      <div class="pull">"未来的乡村学校，不一定更大，但可以更灵活、更开放。"</div>
    </div>
  </div>

  <div class="scholar reveal">
    <div class="s-info">
      <div class="s-num">03</div>
      <h4>孙艳霞</h4>
      <div class="s-title">中国海洋大学教育系副教授</div>
    </div>
    <div class="s-content">
      <p>今天的乡村小学撤并，越来越多是人口现实倒逼的结果。随着农村生源持续减少，单纯依靠情怀和投入去维持学校并不现实，"小而美"也未必真正可持续。比起一味保留，更重要的是思考撤并之后，校舍如何继续服务村庄公共生活。</p>
      <div class="pull">"没有学生的学校留不住，但校舍仍可以继续服务村庄。"</div>
    </div>
  </div>
</section>
</div>

<!-- ===== FOOTER ===== -->
<footer>
  <p class="foot-title reveal">从书声琅琅到空楼寂寂，<br>这不是一所学校的故事，<br>而是<em>千万个村庄</em>共同的告别。</p>
  <div class="credits">
    <strong>文学与新闻传播学院</strong> · 2022 级本科生毕业设计 / 2026
  </div>
</footer>

<script>
/* ===== Voices ===== */
const voices = [
  {name:"尹佳绮", role:"湖南云山学校 · 00后校长", preview:"毕竟是我毕业之后第一个学校、第一批学生……", quote:["毕竟是我毕业之后第一个学校、第一批学生、第一个环境。","希望我们未来都会越来越好，我会永远记得我是从这里出发的。"]},
  {name:"张娜", role:"陕西策村小学 · 16年教龄教师", preview:"撤不撤我也没有办法……", quote:["撤不撤我也没有办法。","所有学习都要靠我们去抓，没有别的环境可以依靠。"]},
  {name:"曾良平", role:"湖南云山学校 · 41年教龄老教师", preview:"我最放心不下的，是那些没钱没势的穷孩子……", quote:["我最放心不下的，是那些没钱没势的穷孩子。","形式主义表格太多，把教书的时间都占了。"]},
  {name:"黄老师", role:"广西恭城瑶族自治县 · 双科教师", preview:"山里面不会听我们外地人的……", quote:["山里面不会听我们外地人的。","撤校的事情我们在学校都是避而不谈的。"]},
  {name:"王志超", role:"衡水建国镇中心校主任", preview:"撤不撤都会有困难……", quote:["撤不撤都会有困难。","学生比较少的成绩却很好，这是不是和小班有关系。"]},
  {name:"赵小旺", role:"兴平市教育局基教科科长", preview:"教育永远围绕以学生为中心……", quote:["教育永远围绕以学生为中心，服务辖区人民群众。","未来村小撤并的趋势必然是教育资源全面整合升级。"]},
  {name:"曾皓轩", role:"湖南云山学校 · 学生", preview:"因为我讨厌妈妈……", quote:["因为我讨厌妈妈。","我不想爷爷给我送饭了，不然他会快一点变老的。"]},
  {name:"华芝涵", role:"扬州市渌洋湖中心小学 · 学生", preview:"老师有时候会拿教棍打手……", quote:["老师有时候会拿教棍打手，或者是打几下头，在学业方面比较负责，但是育人方面不太行。","在农村读的小学让我看不到希望。"]}
];

const grid = document.getElementById('voicesGrid');
voices.forEach((v,i)=>{
  const card = document.createElement('div');
  card.className='voice-card reveal';
  card.style.transitionDelay = (i%4 * 0.1) + 's';
  card.innerHTML = `
    <div class="v-name">${v.name}</div>
    <div class="v-role">${v.role}</div>
    <div class="v-preview">"${v.preview}"</div>
    <div class="v-expand">${v.quote.map(q=>`<p>"${q}"</p>`).join('')}</div>
    <div class="v-toggle"><span class="icon">+</span> <span class="txt">展开完整语录</span></div>
  `;
  card.addEventListener('click', ()=>{
    card.classList.toggle('expanded');
    const txt = card.querySelector('.v-toggle .txt');
    txt.textContent = card.classList.contains('expanded') ? '收起' : '展开完整语录';
  });
  grid.appendChild(card);
});

/* ===== Reveal Observer ===== */
const observer = new IntersectionObserver((entries)=>{
  entries.forEach(entry=>{
    if(entry.isIntersecting){
      entry.target.classList.add('visible');
      if(entry.target.classList.contains('stage')){
        const bar = entry.target.querySelector('.stage-data');
        if(bar) bar.classList.add('visible');
      }
      if(entry.target.classList.contains('stat-row')){
        entry.target.querySelectorAll('.stat-num').forEach(el=>animateCount(el));
      }
    }
  });
},{threshold:0.12});
document.querySelectorAll('.reveal, .reveal-left, .reveal-right, .reveal-scale').forEach(el=>observer.observe(el));

function animateCount(el){
  if(el.dataset.done) return;
  el.dataset.done = 1;
  const target = +el.dataset.count;
  const dur = 1400;
  const start = performance.now();
  function step(t){
    const p = Math.min(1,(t-start)/dur);
    const eased = 1 - Math.pow(1-p, 3);
    el.textContent = Math.round(target * eased);
    if(p<1) requestAnimationFrame(step);
  }
  requestAnimationFrame(step);
}

/* progress bar */
window.addEventListener('scroll',()=>{
  const h = document.documentElement;
  const scrolled = (h.scrollTop / (h.scrollHeight - h.clientHeight)) * 100;
  document.getElementById('progress').style.width = scrolled + '%';

  const nav = document.querySelector('nav');
  if(window.scrollY > 50){
    nav.style.background = 'rgba(244,245,238,0.95)';
    nav.style.boxShadow = '0 4px 20px rgba(61,107,74,0.06)';
  } else {
    nav.style.background = 'rgba(244,245,238,0.85)';
    nav.style.boxShadow = 'none';
  }
});

/* ===== 自定义鼠标 ===== */
const dot = document.getElementById('cursorDot');
const ring = document.getElementById('cursorRing');
let mouseX=0, mouseY=0, ringX=0, ringY=0;
window.addEventListener('mousemove', e=>{
  mouseX = e.clientX; mouseY = e.clientY;
  dot.style.left = mouseX+'px'; dot.style.top = mouseY+'px';
});
function loop(){
  ringX += (mouseX - ringX) * 0.15;
  ringY += (mouseY - ringY) * 0.15;
  ring.style.left = ringX+'px'; ring.style.top = ringY+'px';
  requestAnimationFrame(loop);
}
loop();

/* 鼠标悬浮在可点击元素上时变大 */
document.querySelectorAll('a, .voice-card, .school-card, .stage, .stat-item, .scholar, button').forEach(el=>{
  el.addEventListener('mouseenter', ()=>ring.classList.add('hover'));
  el.addEventListener('mouseleave', ()=>ring.classList.remove('hover'));
});

/* ===== Hero 鼠标光晕跟随 ===== */
const heroGlow = document.getElementById('heroGlow');
const hero = document.querySelector('.hero');
hero.addEventListener('mousemove', e=>{
  const rect = hero.getBoundingClientRect();
  heroGlow.style.left = (e.clientX - rect.left) + 'px';
  heroGlow.style.top = (e.clientY - rect.top) + 'px';
  heroGlow.style.opacity = '1';
});
hero.addEventListener('mouseleave', ()=>{
  heroGlow.style.opacity = '0';
});

/* ===== Hero 视差滚动 ===== */
window.addEventListener('scroll',()=>{
  const sc = window.scrollY;
  if(sc < window.innerHeight){
    document.querySelector('.hero-content').style.transform = `translateY(${sc * 0.3}px)`;
    document.querySelector('.hero-content').style.opacity = 1 - sc / (window.innerHeight * 0.8);
  }
});
</script>

</body>
</html>
