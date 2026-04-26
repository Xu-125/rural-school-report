<!DOCTYPE html>
<html lang="zh-CN">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>故土与新途 · 文学与新闻传播学院 2022 级毕业设计</title>

<link rel="preconnect" href="https://fonts.font.im" />
<link href="https://fonts.font.im/css2?family=Cormorant+Garamond:ital,wght@0,300;0,400;0,600;1,400;1,600&display=swap" rel="stylesheet" />

<style>
  *{margin:0;padding:0;box-sizing:border-box}

  :root{
    --font-cn:'STZhongsong','华文中宋','STSong','Songti SC','Source Han Serif SC','Noto Serif SC','SimSun','宋体','Microsoft YaHei',serif;
    --font-en:'Cormorant Garamond','Times New Roman',Georgia,serif;

    --bg:#f4f5ee;
    --bg-warm:#ecebdd;
    --bg-dark:#0f1713;
    --paper:#eef0e2;
    --paper-2:rgba(255,255,255,.82);
    --ink:#16241a;
    --muted:#5f6f61;
    --line:#c4cfbc;
    --accent:#355e46;
    --accent-2:#6e925f;
    --leaf:#8eab68;
    --gold:#b8c46c;
    --moss:#4b6a3b;
    --shadow:0 24px 60px rgba(26,42,31,.12);
    --shadow-strong:0 24px 60px rgba(0,0,0,.28);
  }

  html{scroll-behavior:smooth}
  body{
    font-family:var(--font-cn);
    background:var(--bg);
    color:var(--ink);
    line-height:1.9;
    overflow-x:hidden;
    cursor:none;
    -webkit-font-smoothing:antialiased;
    -moz-osx-font-smoothing:grayscale;
    text-rendering:optimizeLegibility;
  }

  ::selection{background:var(--leaf);color:#fff}

  .cursor-dot,.cursor-ring{
    position:fixed;
    top:0;left:0;
    pointer-events:none;
    z-index:9999;
    transform:translate(-50%,-50%);
  }
  .cursor-dot{
    width:6px;height:6px;border-radius:50%;
    background:var(--accent);
    transition:transform .12s ease;
  }
  .cursor-ring{
    width:34px;height:34px;border-radius:50%;
    border:1px solid var(--leaf);
    transition:transform .25s ease,width .3s,height .3s,border-color .3s,background .3s;
  }
  .cursor-ring.hover{
    width:60px;height:60px;
    border-color:var(--accent);
    background:rgba(142,171,104,.12);
    backdrop-filter:blur(2px);
  }
  .cursor-ring.click{
    transform:translate(-50%,-50%) scale(.7);
    background:rgba(53,94,70,.28);
  }

  @media(max-width:900px){
    body{cursor:auto}
    .cursor-dot,.cursor-ring{display:none}
  }

  .ripple{
    position:fixed;
    pointer-events:none;
    z-index:9998;
    width:8px;height:8px;border-radius:50%;
    background:var(--leaf);
    transform:translate(-50%,-50%);
    animation:rippleAnim .8s ease-out forwards;
  }
  @keyframes rippleAnim{
    0%{opacity:.7;width:8px;height:8px}
    100%{opacity:0;width:120px;height:120px}
  }

  .progress{
    position:fixed;
    top:0;left:0;
    height:3px;width:0;
    background:linear-gradient(90deg,var(--leaf),var(--accent),var(--gold));
    z-index:999;
    box-shadow:0 0 14px rgba(184,196,108,.5);
  }

  nav{
    position:fixed;
    top:0;left:0;right:0;
    z-index:100;
    padding:14px 40px;
    background:rgba(244,245,238,.80);
    backdrop-filter:blur(12px);
    border-bottom:1px solid rgba(196,207,188,.7);
    display:flex;
    justify-content:space-between;
    align-items:center;
    transition:all .4s ease;
  }
  nav .brand{
    font-size:12px;
    letter-spacing:2px;
    color:var(--accent);
    font-weight:700;
  }
  nav ul{
    list-style:none;
    display:flex;
    gap:28px;
  }
  nav a{
    text-decoration:none;
    color:var(--muted);
    font-size:13px;
    position:relative;
    transition:.3s ease;
    font-family:var(--font-en);
    letter-spacing:1px;
  }
  nav a::after{
    content:"";
    position:absolute;
    left:0;bottom:-6px;
    width:0;height:1px;
    background:var(--accent);
    transition:width .35s ease;
  }
  nav a:hover{color:var(--accent)}
  nav a:hover::after{width:100%}

  .hero,.case-hero{
    position:relative;
    overflow:hidden;
  }

  .hero{
    min-height:100vh;
    padding:90px 8vw;
    display:flex;
    align-items:center;
    color:#f5f7ee;
    background:
      linear-gradient(180deg, rgba(12,19,15,.30) 0%, rgba(12,19,15,.72) 100%),
      url('https://images.unsplash.com/photo-1500382017468-9049fed747ef?auto=format&fit=crop&w=2000&q=80') center/cover fixed;
  }

  .hero::after,
  .case-hero::after{
    content:"";
    position:absolute;
    inset:0;
    background:
      radial-gradient(circle at center, transparent 35%, rgba(0,0,0,.18) 100%);
    pointer-events:none;
  }

  .mist{
    position:absolute;
    inset:-10%;
    background:
      radial-gradient(circle at 20% 30%, rgba(255,255,255,.10), transparent 18%),
      radial-gradient(circle at 80% 28%, rgba(255,255,255,.08), transparent 22%),
      radial-gradient(circle at 58% 72%, rgba(255,255,255,.05), transparent 24%);
    mix-blend-mode:screen;
    animation:mistMove 18s ease-in-out infinite alternate;
    pointer-events:none;
    z-index:1;
  }
  @keyframes mistMove{
    from{transform:translate3d(-1%,0,0)}
    to{transform:translate3d(2.6%,-1.2%,0)}
  }

  .grain{
    position:absolute;
    inset:0;
    opacity:.11;
    background-image:radial-gradient(rgba(255,255,255,.18) 1px, transparent 1px);
    background-size:4px 4px;
    mix-blend-mode:soft-light;
    pointer-events:none;
    z-index:1;
    animation:grainMove 8s linear infinite;
  }
  @keyframes grainMove{
    0%{transform:translate(0,0)}
    25%{transform:translate(6px,-3px)}
    50%{transform:translate(-4px,5px)}
    75%{transform:translate(5px,3px)}
    100%{transform:translate(0,0)}
  }

  .hero-glow{
    position:absolute;
    width:520px;height:520px;
    border-radius:50%;
    background:radial-gradient(circle, rgba(184,196,108,.16), transparent 60%);
    pointer-events:none;
    transform:translate(-50%,-50%);
    transition:opacity .3s;
    z-index:2;
    opacity:0;
  }

  .leaf-layer,.dust-layer{
    position:absolute;
    inset:0;
    pointer-events:none;
    overflow:hidden;
    z-index:2;
  }
  .leaf{
    position:absolute;
    top:-10%;
    width:18px;height:12px;
    border-radius:60% 40% 70% 30%;
    opacity:.38;
    animation:fall linear infinite;
  }
  .leaf.green{background:rgba(136,171,104,.55)}
  .leaf.gold{background:rgba(184,196,108,.56)}
  .leaf.brown{background:rgba(120,90,58,.45)}
  @keyframes fall{
    0%{transform:translate3d(0,-10vh,0) rotate(0deg) scale(1);opacity:0}
    10%{opacity:.45}
    50%{transform:translate3d(45px,46vh,0) rotate(160deg) scale(1.04)}
    100%{transform:translate3d(-28px,112vh,0) rotate(360deg) scale(.96);opacity:0}
  }
  .dust{
    position:absolute;
    width:3px;height:3px;border-radius:50%;
    background:rgba(255,255,255,.18);
    animation:dustFloat linear infinite;
  }
  @keyframes dustFloat{
    0%{transform:translateY(0) translateX(0);opacity:0}
    20%{opacity:.4}
    80%{opacity:.28}
    100%{transform:translateY(-120px) translateX(36px);opacity:0}
  }

  .hero-content{
    position:relative;
    z-index:3;
    max-width:980px;
  }
  .hero .badge{
    display:inline-block;
    padding:8px 18px;
    border:1px solid rgba(184,196,108,.45);
    border-radius:999px;
    font-size:11px;
    letter-spacing:3px;
    color:var(--gold);
    margin-bottom:26px;
    backdrop-filter:blur(4px);
    background:rgba(15,26,20,.16);
    opacity:0;
    animation:fadeUp .9s .15s forwards;
  }
  .hero .meta{
    font-size:11px;
    letter-spacing:4px;
    color:#c8d0bb;
    margin-bottom:26px;
    font-family:var(--font-en);
    opacity:0;
    animation:fadeUp .9s .25s forwards;
  }
  .hero h1{
    font-size:clamp(48px,9vw,124px);
    line-height:1.08;
    letter-spacing:5px;
    margin-bottom:24px;
  }
  .hero h1 span{
    display:inline-block;
    opacity:0;
    transform:translateY(60px);
    animation:fadeUp 1s forwards;
  }
  .hero h1 span:nth-child(1){animation-delay:.45s}
  .hero h1 span:nth-child(2){animation-delay:.62s}
  .hero h1 span:nth-child(3){
    animation-delay:.8s;
    color:var(--gold);
    font-family:var(--font-en);
    letter-spacing:2px;
    font-style:italic;
  }
  .hero .sub{
    font-size:clamp(15px,1.35vw,19px);
    max-width:720px;
    color:#d9e1cd;
    line-height:2;
    opacity:0;
    animation:fadeUp .9s 1s forwards;
  }
  .hero .author{
    margin-top:36px;
    font-size:11px;
    color:#bfc8b3;
    letter-spacing:3px;
    padding-top:18px;
    max-width:480px;
    border-top:1px solid rgba(184,196,108,.24);
    opacity:0;
    animation:fadeUp .9s 1.2s forwards;
  }
  .hero .scroll{
    position:absolute;
    bottom:34px;
    left:50%;
    transform:translateX(-50%);
    font-size:10px;
    letter-spacing:4px;
    color:#c8d0bb;
    font-family:var(--font-en);
    opacity:0;
    animation:fadeUp .9s 1.5s forwards, bounce 2s 2.6s infinite;
  }

  @keyframes fadeUp{
    to{opacity:1;transform:translateY(0)}
  }
  @keyframes bounce{
    0%,100%{transform:translate(-50%,0)}
    50%{transform:translate(-50%,10px)}
  }

  .reveal{opacity:0;transform:translateY(36px);transition:opacity .9s ease, transform .9s ease}
  .reveal.visible{opacity:1;transform:translateY(0)}
  .reveal-delay-1{transition-delay:.12s}
  .reveal-delay-2{transition-delay:.24s}
  .reveal-delay-3{transition-delay:.36s}
  .reveal-left{opacity:0;transform:translateX(-54px);transition:all .9s ease}
  .reveal-left.visible{opacity:1;transform:translateX(0)}
  .reveal-right{opacity:0;transform:translateX(54px);transition:all .9s ease}
  .reveal-right.visible{opacity:1;transform:translateX(0)}
  .reveal-scale{opacity:0;transform:scale(.92);transition:all 1s ease}
  .reveal-scale.visible{opacity:1;transform:scale(1)}
  .reveal-blur{opacity:0;filter:blur(12px);transition:all 1.1s ease}
  .reveal-blur.visible{opacity:1;filter:blur(0)}

  section{
    padding:110px 8vw;
    max-width:1400px;
    margin:0 auto;
    position:relative;
  }

  .section-tag{
    display:inline-block;
    font-family:var(--font-en);
    font-size:10px;
    letter-spacing:5px;
    color:var(--accent);
    border-top:2px solid var(--accent);
    padding-top:8px;
    margin-bottom:22px;
    position:relative;
    overflow:hidden;
  }
  .section-tag::after{
    content:"";
    position:absolute;
    top:-2px;left:-100%;
    width:100%;height:2px;
    background:linear-gradient(90deg, transparent, var(--gold), transparent);
    animation:shine 3s ease-in-out infinite;
  }
  @keyframes shine{
    0%,100%{left:-100%}
    50%{left:100%}
  }

  .section-title{
    font-size:clamp(36px,5vw,64px);
    line-height:1.24;
    letter-spacing:4px;
    color:var(--ink);
    margin-bottom:18px;
  }
  .section-sub{
    max-width:680px;
    color:var(--muted);
    font-size:16px;
    margin-bottom:60px;
    line-height:2;
  }

  .big-chapter{
    position:absolute;
    right:4vw;
    top:50%;
    transform:translateY(-50%);
    font-family:var(--font-en);
    font-size:clamp(180px,30vw,380px);
    font-style:italic;
    font-weight:300;
    line-height:1;
    color:rgba(123,160,91,.05);
    user-select:none;
    pointer-events:none;
  }

  /* ===== 数据区 ===== */
  .data-viz-wrap{
    display:grid;
    grid-template-columns:1.15fr .85fr;
    gap:28px;
    align-items:start;
  }

  .data-card{
    background:linear-gradient(180deg, rgba(255,255,255,.84), rgba(255,255,255,.68));
    border:1px solid var(--line);
    box-shadow:var(--shadow);
    border-radius:4px;
    padding:28px;
    backdrop-filter:blur(10px);
    transition:transform .35s ease, box-shadow .35s ease;
  }
  .data-card:hover{
    transform:translateY(-6px);
    box-shadow:0 24px 50px rgba(53,94,70,.12);
  }

  .data-title{
    display:flex;
    justify-content:space-between;
    align-items:end;
    gap:12px;
    flex-wrap:wrap;
    margin-bottom:16px;
  }
  .data-title h3{
    font-size:24px;
    color:var(--ink);
  }
  .data-title small{
    font-size:11px;
    color:var(--muted);
    letter-spacing:2px;
    font-family:var(--font-en);
  }

  .control{
    display:grid;
    gap:12px;
    margin-bottom:14px;
  }

  .year-row{
    display:flex;
    justify-content:space-between;
    gap:12px;
    align-items:center;
    flex-wrap:wrap;
  }
  .year-label{
    font-size:18px;
    color:var(--accent);
    font-family:var(--font-en);
    letter-spacing:1px;
  }
  .value-badge{
    display:inline-flex;
    align-items:center;
    gap:8px;
    padding:8px 14px;
    border-radius:999px;
    background:rgba(123,160,91,.10);
    color:var(--ink);
    font-size:13px;
    transition:.3s ease;
  }
  .value-badge.flash{
    transform:scale(1.05);
    background:rgba(123,160,91,.18);
  }

  input[type="range"]{
    width:100%;
    appearance:none;
    height:6px;
    border-radius:999px;
    background:linear-gradient(90deg, rgba(123,160,91,.18), rgba(61,107,74,.08));
    outline:none;
  }
  input[type="range"]::-webkit-slider-thumb{
    appearance:none;
    width:18px;height:18px;
    border-radius:50%;
    background:var(--accent);
    border:3px solid #e9efe1;
    box-shadow:0 6px 16px rgba(0,0,0,.16);
    cursor:pointer;
  }

  .chart-wrap{
    position:relative;
    padding:10px;
    border-radius:4px;
    background:linear-gradient(180deg, rgba(255,255,255,.44), rgba(255,255,255,.14));
    border:1px solid rgba(188,202,177,.5);
    overflow:hidden;
  }
  .chart-wrap::after{
    content:"";
    position:absolute;
    inset:auto -10% -18% -10%;
    height:60%;
    background:radial-gradient(circle, rgba(142,171,104,.14), transparent 60%);
    pointer-events:none;
  }

  .chart-svg{width:100%;display:block;height:auto}
  .tooltip{
    position:absolute;
    transform:translate(-50%,-120%);
    background:rgba(15,26,20,.94);
    color:#fff;
    font-size:12px;
    padding:8px 10px;
    border-radius:10px;
    white-space:nowrap;
    pointer-events:none;
    opacity:0;
    transition:.2s ease;
    box-shadow:0 10px 24px rgba(0,0,0,.16);
    z-index:5;
  }

  .legend{
    margin-top:12px;
    display:flex;
    gap:16px;
    flex-wrap:wrap;
    font-size:12px;
    color:var(--muted);
  }
  .legend span{display:inline-flex;align-items:center;gap:8px}
  .l-line,.l-area,.l-point{
    display:inline-block;border-radius:999px
  }
  .l-line{width:26px;height:3px;background:var(--accent)}
  .l-area{width:26px;height:10px;background:linear-gradient(180deg, rgba(123,160,91,.28), rgba(123,160,91,.04))}
  .l-point{width:10px;height:10px;border-radius:50%;background:var(--gold)}

  .stats-grid{
    display:grid;
    grid-template-columns:repeat(2,1fr);
    gap:12px;
    margin-top:18px;
  }
  .stat-box{
    padding:16px;
    background:rgba(255,255,255,.56);
    border:1px solid rgba(196,207,188,.55);
    transition:.3s ease;
    position:relative;
    overflow:hidden;
  }
  .stat-box::after{
    content:"";
    position:absolute;
    right:-16px;top:-16px;
    width:76px;height:76px;border-radius:50%;
    background:radial-gradient(circle, rgba(123,160,91,.16), transparent 68%);
  }
  .stat-box:hover{
    transform:translateY(-4px);
    box-shadow:0 16px 30px rgba(26,42,31,.08);
  }
  .stat-box strong{
    display:block;
    font-family:var(--font-en);
    font-size:32px;
    line-height:1;
    color:var(--accent);
  }
  .stat-box span{
    display:block;
    margin-top:8px;
    font-size:12px;
    color:var(--muted);
    line-height:1.8;
  }

  .phase-list{
    display:grid;
    gap:12px;
  }
  .phase-item{
    padding:16px;
    background:rgba(255,255,255,.56);
    border:1px solid rgba(196,207,188,.55);
    transition:.28s ease;
  }
  .phase-item.active{
    transform:translateX(4px);
    background:linear-gradient(135deg, rgba(142,171,104,.14), rgba(255,255,255,.76));
    border-color:rgba(53,94,70,.16);
    box-shadow:0 12px 24px rgba(26,42,31,.06);
  }
  .phase-head{
    display:flex;
    justify-content:space-between;
    gap:10px;
    align-items:center;
    margin-bottom:8px;
  }
  .phase-head strong{
    font-size:15px;
    color:var(--ink);
    letter-spacing:1px;
  }
  .phase-head span{
    font-size:11px;
    color:var(--muted);
    font-family:var(--font-en);
  }
  .bar{
    height:8px;border-radius:999px;overflow:hidden;
    background:rgba(123,160,91,.10);
    margin-bottom:8px;
  }
  .bar i{
    display:block;height:100%;width:0;
    background:linear-gradient(90deg,var(--leaf),var(--accent));
    transition:width 1.4s cubic-bezier(.2,.7,.2,1);
  }
  .phase-item small{
    display:block;
    font-size:12px;
    color:var(--muted);
    line-height:1.8;
  }

  /* ===== case hero ===== */
  .case{
    background:var(--bg-dark);
    color:#dce5d1;
    padding:0;
    max-width:none;
    margin:0;
  }

  .case-hero{
    min-height:78vh;
    padding:120px 8vw;
    display:flex;
    flex-direction:column;
    justify-content:center;
    position:relative;
  }

  .case-hero.shaanxi{
    background:
      linear-gradient(90deg, rgba(10,18,14,.90) 26%, rgba(10,18,14,.38) 100%),
      url('https://images.unsplash.com/photo-1464822759023-fed622ff2c3b?auto=format&fit=crop&w=2000&q=80') center/cover;
  }
  .case-hero.hunan{
    background:
      linear-gradient(90deg, rgba(10,18,14,.90) 26%, rgba(10,18,14,.38) 100%),
      url('https://images.unsplash.com/photo-1470770841072-f978cf4d019e?auto=format&fit=crop&w=2000&q=80') center/cover;
  }
  .case-hero.voices{
    background:
      linear-gradient(90deg, rgba(10,18,14,.92) 26%, rgba(10,18,14,.42) 100%),
      url('https://images.unsplash.com/photo-1497633762265-9d179a990aa6?auto=format&fit=crop&w=2000&q=80') center/cover;
  }
  .case-hero.scholars{
    background:
      linear-gradient(90deg, rgba(10,18,14,.92) 26%, rgba(10,18,14,.42) 100%),
      url('https://images.unsplash.com/photo-1481627834876-b7833e8f5570?auto=format&fit=crop&w=2000&q=80') center/cover;
  }
  .case-hero.ending{
    background:
      linear-gradient(90deg, rgba(10,18,14,.88) 26%, rgba(10,18,14,.44) 100%),
      url('https://images.unsplash.com/photo-1500530855697-b586d89ba3ee?auto=format&fit=crop&w=2000&q=80') center/cover;
  }

  .case-hero > *{position:relative;z-index:3}
  .case-hero .place{
    font-family:var(--font-en);
    font-size:13px;
    letter-spacing:8px;
    color:var(--gold);
    margin-bottom:20px;
  }
  .case-hero h2{
    font-size:clamp(40px,6vw,80px);
    line-height:1.2;
    letter-spacing:5px;
    margin-bottom:18px;
    color:#f5f7ee;
  }
  .case-hero .case-sub{
    max-width:620px;
    font-size:17px;
    color:#c0ccb2;
    line-height:2;
    border-left:3px solid var(--gold);
    padding-left:18px;
    margin-top:24px;
  }

  .case-deco{
    position:absolute;
    right:7vw;
    top:50%;
    transform:translateY(-50%);
    width:300px;height:300px;
    opacity:.14;
    z-index:1;
    pointer-events:none;
  }
  .case-deco svg{width:100%;height:100%}
  .case-deco .ring{
    fill:none;stroke:var(--gold);stroke-width:1;
    transform-origin:center;
    animation:rotate 30s linear infinite;
  }
  .case-deco .ring2{
    animation-direction:reverse;
    animation-duration:40s;
  }
  @keyframes rotate{to{transform:rotate(360deg)}}

  .case-body{
    padding:96px 8vw;
    max-width:1400px;
    margin:0 auto;
  }

  .case-quote{
    font-size:clamp(22px,2.3vw,32px);
    line-height:1.9;
    color:#e8efd8;
    margin-bottom:70px;
    padding:34px 52px;
    border-left:2px solid var(--gold);
    letter-spacing:2px;
  }
  .case-quote em{
    color:var(--gold);
    font-style:normal;
  }

  .school-grid{
    display:grid;
    grid-template-columns:repeat(auto-fit,minmax(320px,1fr));
    gap:28px;
    margin-bottom:74px;
  }
  .school-card{
    background:rgba(255,255,255,.04);
    border:1px solid rgba(184,196,108,.14);
    padding:34px 28px;
    transition:all .35s cubic-bezier(.2,.8,.2,1);
    position:relative;
    overflow:hidden;
    transform-style:preserve-3d;
  }
  .school-card::before{
    content:"";
    position:absolute;
    top:0;left:-100%;
    width:100%;height:100%;
    background:linear-gradient(90deg, transparent, rgba(184,196,108,.08), transparent);
    transition:left .8s;
  }
  .school-card:hover::before{left:100%}
  .school-card:hover{
    transform:translateY(-10px);
    border-color:var(--gold);
    background:rgba(184,196,108,.05);
    box-shadow:0 24px 50px rgba(0,0,0,.35);
  }
  .school-card .num{
    position:absolute;
    top:18px;right:22px;
    font-family:var(--font-en);
    font-size:46px;
    color:var(--gold);
    opacity:.35;
    transition:.35s ease;
  }
  .school-card:hover .num{
    transform:scale(1.24) rotate(-8deg);
    opacity:.75;
  }
  .school-card h4{
    font-size:22px;
    margin-bottom:8px;
    color:#f5f7ee;
    letter-spacing:2px;
  }
  .school-card .school-tag{
    font-size:11px;
    letter-spacing:3px;
    color:var(--gold);
    margin-bottom:18px;
  }
  .school-card ul{
    list-style:none;
    font-size:14px;
    color:#b8c5a8;
    line-height:2;
  }
  .school-card ul li{
    position:relative;
    padding-left:16px;
    margin-bottom:6px;
  }
  .school-card ul li::before{
    content:"—";
    position:absolute;
    left:0;
    color:var(--leaf);
  }

  .kid-section{margin-top:54px}
  .kid-section h3{
    font-size:24px;
    margin-bottom:24px;
    color:#f5f7ee;
    letter-spacing:3px;
    border-bottom:1px solid rgba(184,196,108,.18);
    padding-bottom:12px;
  }
  .kid-grid{
    display:grid;
    grid-template-columns:repeat(auto-fit,minmax(260px,1fr));
    gap:20px;
  }
  .kid-card{
    background:rgba(0,0,0,.22);
    padding:22px;
    border-top:2px solid var(--leaf);
    transition:.35s ease;
  }
  .kid-card:hover{
    background:rgba(184,196,108,.06);
    border-top-color:var(--gold);
    transform:translateY(-6px) rotate(-1deg);
    box-shadow:0 10px 30px rgba(0,0,0,.28);
  }
  .kid-card .kid-name{
    font-size:18px;
    color:var(--gold);
    margin-bottom:10px;
    letter-spacing:2px;
  }
  .kid-card p{
    font-size:13px;
    color:#b8c5a8;
    line-height:1.9;
  }

  .stat-row{
    display:grid;
    grid-template-columns:repeat(4,1fr);
    gap:26px;
    margin:54px 0;
    padding:34px 0;
    border-top:1px solid rgba(184,196,108,.15);
    border-bottom:1px solid rgba(184,196,108,.15);
  }
  .stat-item{text-align:center}
  .stat-item .stat-num{
    display:inline-block;
    font-family:var(--font-en);
    font-size:52px;
    color:var(--gold);
    line-height:1;
    transition:.3s ease;
  }
  .stat-item:hover .stat-num{
    transform:scale(1.18);
    color:#dae98d;
  }
  .stat-item .stat-label{
    font-size:11px;
    color:#b8c5a8;
    letter-spacing:3px;
    margin-top:10px;
  }

  .case-end{
    text-align:center;
    margin-top:70px;
    padding-top:56px;
    border-top:1px solid rgba(184,196,108,.15);
  }
  .case-end p{
    font-size:17px;
    color:#b8c5a8;
    margin-bottom:8px;
    letter-spacing:1px;
  }
  .case-end .big-line{
    font-size:28px;
    color:var(--gold);
    margin-top:18px;
    letter-spacing:4px;
  }

  /* ===== voices ===== */
  .voices-section{
    background:linear-gradient(180deg, var(--bg) 0%, var(--bg-warm) 100%);
  }
  .voices-grid{
    display:grid;
    grid-template-columns:repeat(auto-fill,minmax(300px,1fr));
    gap:24px;
    grid-auto-flow:dense;
  }
  .voice-card{
    background:#fff;
    padding:28px;
    border:1px solid var(--line);
    position:relative;
    overflow:hidden;
    transition:all .35s cubic-bezier(.2,.8,.2,1);
    cursor:pointer;
    will-change:transform;
  }
  .voice-card::before{
    content:"❝";
    position:absolute;
    top:-18px;right:18px;
    font-size:90px;
    color:var(--leaf);
    opacity:.14;
    transition:.45s ease;
    font-family:serif;
  }
  .voice-card:hover::before{
    transform:rotate(10deg) scale(1.14);
    opacity:.32;
  }
  .voice-card:hover{
    transform:translateY(-8px);
    border-color:var(--accent);
    box-shadow:0 24px 50px rgba(53,94,70,.16);
  }
  .voice-card.expanded{
    grid-column:span 2;
    background:linear-gradient(135deg, var(--paper), #fff);
    border-color:var(--accent);
    box-shadow:0 30px 60px rgba(53,94,70,.18);
  }
  @media(max-width:700px){
    .voice-card.expanded{grid-column:span 1}
  }

  .voice-card .v-name{
    font-size:22px;
    color:var(--ink);
    margin-bottom:6px;
    letter-spacing:2px;
  }
  .voice-card .v-role{
    font-size:11px;
    color:var(--accent);
    letter-spacing:1px;
    margin-bottom:16px;
    padding-bottom:12px;
    border-bottom:1px dashed var(--line);
  }
  .voice-card .v-preview{
    font-size:14px;
    color:var(--muted);
    line-height:1.9;
    font-style:italic;
  }
  .voice-card .v-expand{
    max-height:0;
    overflow:hidden;
    opacity:0;
    transition:max-height .5s ease, opacity .4s ease, margin .4s ease;
  }
  .voice-card.expanded .v-expand{
    max-height:500px;
    opacity:1;
    margin-top:18px;
  }
  .voice-card.expanded .v-preview{display:none}
  .voice-card .v-expand p{
    font-size:15px;
    line-height:2;
    color:var(--ink);
    padding:12px 16px 12px 18px;
    border-left:3px solid var(--leaf);
    margin-bottom:12px;
    background:rgba(123,160,91,.05);
  }
  .voice-card .v-toggle{
    font-size:10px;
    color:var(--accent);
    margin-top:14px;
    letter-spacing:3px;
    display:flex;
    align-items:center;
    gap:8px;
  }
  .voice-card .v-toggle .icon{
    width:18px;height:18px;
    border-radius:50%;
    border:1px solid var(--accent);
    display:inline-flex;
    align-items:center;
    justify-content:center;
    font-size:14px;
    transition:.35s ease;
  }
  .voice-card.expanded .v-toggle .icon{
    transform:rotate(45deg);
    background:var(--accent);
    color:#fff;
  }

  /* ===== scholars ===== */
  .scholars-section{
    background:var(--paper);
    position:relative;
    overflow:hidden;
  }
  .scholars-section::before{
    content:"";
    position:absolute;
    top:-100px;right:-100px;
    width:400px;height:400px;
    border-radius:50%;
    background:radial-gradient(circle, rgba(123,160,91,.14), transparent 70%);
    animation:floatBg 20s ease-in-out infinite;
  }
  @keyframes floatBg{
    0%,100%{transform:translate(0,0)}
    50%{transform:translate(-50px,28px)}
  }

  .scholar{
    display:grid;
    grid-template-columns:1fr 2fr;
    gap:60px;
    padding:56px 0;
    border-bottom:1px solid var(--line);
    align-items:start;
    position:relative;
  }
  .scholar:last-child{border-bottom:none}
  .scholar .s-info h4{
    font-size:30px;
    margin-bottom:8px;
    letter-spacing:3px;
    transition:.3s ease;
  }
  .scholar:hover .s-info h4{color:var(--accent)}
  .scholar .s-info .s-title{
    font-size:12px;
    color:var(--accent);
    letter-spacing:2px;
  }
  .scholar .s-info .s-num{
    font-family:var(--font-en);
    font-size:78px;
    font-style:italic;
    color:var(--leaf);
    opacity:.5;
    line-height:1;
    margin-bottom:18px;
    transition:.35s ease;
  }
  .scholar:hover .s-info .s-num{
    opacity:.9;
    transform:translateX(8px);
  }
  .scholar .s-content p{
    font-size:16px;
    color:var(--ink);
    line-height:2.05;
    margin-bottom:20px;
    letter-spacing:.5px;
  }
  .scholar .s-content .pull{
    font-size:21px;
    color:var(--accent);
    line-height:1.8;
    padding:22px 28px;
    background:#fff;
    border-left:4px solid var(--leaf);
    transition:.35s ease;
    letter-spacing:1px;
  }
  .scholar:hover .s-content .pull{
    transform:translateX(8px);
    border-left-color:var(--accent);
    box-shadow:0 12px 30px rgba(53,94,70,.10);
  }

  footer{
    background:var(--bg-dark);
    color:#b8c5a8;
    padding:110px 8vw 54px;
    text-align:center;
    position:relative;
    overflow:hidden;
  }
  footer::before{
    content:"";
    position:absolute;
    bottom:0;left:0;right:0;height:60%;
    background:radial-gradient(ellipse at center bottom, rgba(123,160,91,.14), transparent 70%);
    pointer-events:none;
  }
  footer .foot-title{
    max-width:820px;
    margin:0 auto 34px;
    font-size:clamp(28px,4vw,48px);
    line-height:1.75;
    color:#f4f5ee;
    letter-spacing:3px;
    position:relative;
  }
  footer .foot-title em{
    color:var(--gold);
    font-style:normal;
  }
  footer .credits{
    margin-top:40px;
    padding-top:24px;
    border-top:1px solid #2a3a2a;
    font-size:11px;
    color:#879687;
    letter-spacing:3px;
    position:relative;
  }
  footer .credits strong{color:var(--gold)}

  .pulse-dot{
    display:inline-block;
    width:8px;height:8px;border-radius:50%;
    background:var(--leaf);
    margin-right:8px;
    animation:pulse 2s infinite;
  }
  @keyframes pulse{
    0%,100%{box-shadow:0 0 0 0 rgba(123,160,91,.6)}
    50%{box-shadow:0 0 0 8px rgba(123,160,91,0)}
  }

  @media(max-width:900px){
    nav{padding:14px 20px}
    nav ul{display:none}
    section{padding:80px 6vw}
    .data-viz-wrap,.scholar,.stat-row{grid-template-columns:1fr}
    .big-chapter{display:none}
    .case-quote{padding:20px 24px}
    .case-deco{display:none}
  }
</style>
</head>
<body>

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

<header class="hero">
  <div class="hero-glow" id="heroGlow"></div>
  <div class="mist"></div>
  <div class="grain"></div>
  <div class="dust-layer" id="dust-hero"></div>
  <div class="leaf-layer" id="leaf-hero"></div>

  <div class="hero-content">
    <div class="badge">文学与新闻传播学院 · 2022级本科生毕业设计</div>
    <div class="meta">DEEP REPORT · <span style="color:var(--gold)">RURAL PRIMARY SCHOOLS IN CHINA</span></div>
    <h1>
      <span>故土</span><span>与新途</span><br>
      <span>乡村小学的撤并倒计时</span>
    </h1>
    <p class="sub">从 1997 年的 51.3 万所到 2023 年的 7.06 万所，一代人的求学迁徙正在悄然完成。当政策从“能撤尽撤”转向“应留必留”，村小的命运仍在城镇化的浪潮中艰难选择。</p>
    <div class="author">文学与新闻传播学院 · 2022 级本科生毕业设计作品</div>
  </div>
  <div class="scroll">SCROLL ↓</div>
</header>

<section id="policy">
  <div class="big-chapter">01</div>
  <div class="reveal"><div class="section-tag">CHAPTER 01 · DATA</div></div>
  <h2 class="section-title reveal">政策的演变，<br>数据的起伏</h2>
  <p class="section-sub reveal reveal-delay-1">把变化看出来，而不是只读出来。拖动年份，观察乡村小学在二十余年间如何迅速减少，并对应到政策阶段的变化。</p>

  <div class="data-viz-wrap">
    <div class="data-card reveal">
      <div class="data-title">
        <h3>乡村小学数量变化</h3>
        <small>1997 — 2023 / 单位：万所</small>
      </div>

      <div class="control">
        <div class="year-row">
          <div class="year-label">YEAR / <span id="yearNow">1997</span></div>
          <div class="value-badge" id="valueBadge">数量：<strong id="schoolValue">51.3</strong> 万所</div>
        </div>
        <input type="range" id="yearRange" min="0" max="5" step="1" value="0" />
      </div>

      <div class="chart-wrap">
        <svg class="chart-svg" viewBox="0 0 720 400">
          <g stroke="rgba(53,94,70,.10)" stroke-width="1">
            <line x1="74" y1="320" x2="670" y2="320"/>
            <line x1="74" y1="266" x2="670" y2="266"/>
            <line x1="74" y1="212" x2="670" y2="212"/>
            <line x1="74" y1="158" x2="670" y2="158"/>
            <line x1="74" y1="104" x2="670" y2="104"/>
            <line x1="74" y1="50" x2="670" y2="50"/>
          </g>

          <g fill="#5f6f61" font-size="12" font-family="Cormorant Garamond, serif">
            <text x="42" y="324">0</text>
            <text x="30" y="270">10</text>
            <text x="30" y="216">20</text>
            <text x="30" y="162">30</text>
            <text x="30" y="108">40</text>
            <text x="30" y="54">50</text>
          </g>

          <g id="xLabels"></g>

          <defs>
            <linearGradient id="lineGrad" x1="0" y1="0" x2="1" y2="0">
              <stop offset="0%" stop-color="#89a86d"/>
              <stop offset="100%" stop-color="#2f5c45"/>
            </linearGradient>
            <linearGradient id="areaGrad" x1="0" y1="0" x2="0" y2="1">
              <stop offset="0%" stop-color="rgba(142,171,104,.34)"/>
              <stop offset="100%" stop-color="rgba(142,171,104,0)"/>
            </linearGradient>
            <filter id="glow">
              <feGaussianBlur stdDeviation="3.6" result="blur"/>
              <feMerge>
                <feMergeNode in="blur"/>
                <feMergeNode in="SourceGraphic"/>
              </feMerge>
            </filter>
          </defs>

          <path id="areaPath" fill="url(#areaGrad)" opacity=".95"></path>
          <path id="lineGlow" fill="none" stroke="rgba(184,196,108,.36)" stroke-width="10" stroke-linecap="round" stroke-linejoin="round" filter="url(#glow)"></path>
          <path id="linePath" fill="none" stroke="url(#lineGrad)" stroke-width="4" stroke-linecap="round" stroke-linejoin="round"></path>

          <g id="points"></g>
          <circle id="focusDot" r="7" fill="#d0bf84" stroke="#214230" stroke-width="3"></circle>
          <circle id="focusRing" r="15" fill="none" stroke="rgba(208,191,132,.35)" stroke-width="2"></circle>
        </svg>
        <div class="tooltip" id="tooltip"></div>
      </div>

      <div class="legend">
        <span><i class="l-line"></i>数量变化折线</span>
        <span><i class="l-area"></i>变化面积</span>
        <span><i class="l-point"></i>关键年份节点</span>
      </div>

      <div class="stats-grid">
        <div class="stat-box"><strong id="dropPercent">86.2%</strong><span>1997—2023 整体降幅</span></div>
        <div class="stat-box"><strong id="dailyRate">63</strong><span>高峰时期日均消失（所/天）</span></div>
        <div class="stat-box"><strong id="remainValue">7.06</strong><span>2023 年乡村小学数量（万所）</span></div>
        <div class="stat-box"><strong id="ratioValue">1:15</strong><span>2012—2021 镇区与乡村减量对比</span></div>
      </div>
    </div>

    <div class="data-card reveal">
      <div class="data-title">
        <h3>撤点并校政策阶段</h3>
        <small><span class="pulse-dot"></span>PHASE SHIFT</small>
      </div>

      <div class="phase-list">
        <div class="phase-item" data-phase="0">
          <div class="phase-head"><strong>初步萌芽</strong><span>1980s — 2000</span></div>
          <div class="bar"><i data-width="22"></i></div>
          <small>局部试点，规模效益逻辑进入基层教育布局。</small>
        </div>

        <div class="phase-item" data-phase="1">
          <div class="phase-head"><strong>成型提速</strong><span>2001 — 2005</span></div>
          <div class="bar"><i data-width="92"></i></div>
          <small>推进最快，部分地区出现一刀切、盲目撤并。</small>
        </div>

        <div class="phase-item" data-phase="2">
          <div class="phase-head"><strong>变形纠偏</strong><span>2006 — 2012</span></div>
          <div class="bar"><i data-width="55"></i></div>
          <small>开始强调程序、公示、听证与上学距离问题。</small>
        </div>

        <div class="phase-item" data-phase="3">
          <div class="phase-head"><strong>稳慎优化</strong><span>2013 — 2026</span></div>
          <div class="bar"><i data-width="38"></i></div>
          <small>从“能撤尽撤”转向“应留必留”，但自然消亡仍在继续。</small>
        </div>
      </div>
    </div>
  </div>
</section>

<div class="case" id="shaanxi">
  <div class="case-hero shaanxi">
    <div class="mist"></div>
    <div class="grain"></div>
    <div class="dust-layer" id="dust-shaanxi"></div>
    <div class="leaf-layer" id="leaf-shaanxi"></div>
    <div class="case-deco">
      <svg viewBox="0 0 200 200">
        <circle class="ring" cx="100" cy="100" r="80"></circle>
        <circle class="ring ring2" cx="100" cy="100" r="60"></circle>
        <circle class="ring" cx="100" cy="100" r="40"></circle>
      </svg>
    </div>
    <div class="place reveal-left">陕西 · SHAANXI</div>
    <h2 class="reveal-left reveal-delay-1">一代人的<br>求学迁徙</h2>
    <p class="case-sub reveal-left reveal-delay-2">兴平·丰仪·策村——被时间与生源慢慢掏空的村小</p>
  </div>

  <div class="case-body">
    <p class="case-quote reveal-blur">一堵堵水泥墙封死校门，一间间校舍变成<em>辣椒加工厂、仓库、厂房</em>。<br>三所学校，三段消亡样本。</p>

    <div class="school-grid">
      <div class="school-card reveal-scale tilt">
        <span class="num">01</span>
        <div class="school-tag">苟延残喘</div>
        <h4>策村小学</h4>
        <ul>
          <li>全校 80 余名学生，6 个年级</li>
          <li>一年级 6 人，二年级 14—16 人</li>
          <li>教师 11 人，普遍一人教多科</li>
          <li>张娜：16 年教龄，负责英语和科学两科</li>
          <li>硬件改善，但留不住生源</li>
        </ul>
      </div>

      <div class="school-card reveal-scale reveal-delay-1 tilt">
        <span class="num">02</span>
        <div class="school-tag">水泥封门</div>
        <h4>周村小学</h4>
        <ul>
          <li>村民集资建校，关停未充分告知</li>
          <li>校舍被租给辣椒厂</li>
          <li>校门被水泥封死</li>
          <li>丰仪镇：16 村 16 校 → 仅剩 4 所</li>
        </ul>
      </div>

      <div class="school-card reveal-scale reveal-delay-2 tilt">
        <span class="num">03</span>
        <div class="school-tag">借钱建校</div>
        <h4>水道口小学</h4>
        <ul>
          <li>2003 年韩怀生自借 5 万启动</li>
          <li>巅峰：覆盖 6 村，600 多学生，8 辆校车</li>
          <li>2014 年生源枯竭正式关停</li>
          <li>之后转为民办，以新身份存续</li>
        </ul>
      </div>
    </div>

    <p class="case-quote reveal-blur">能走的都走了，<em>留下的，是最走不掉的孩子。</em></p>

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

<div class="case" id="hunan">
  <div class="case-hero hunan">
    <div class="mist"></div>
    <div class="grain"></div>
    <div class="dust-layer" id="dust-hunan"></div>
    <div class="leaf-layer" id="leaf-hunan"></div>
    <div class="case-deco">
      <svg viewBox="0 0 200 200">
        <circle class="ring" cx="100" cy="100" r="80"></circle>
        <circle class="ring ring2" cx="100" cy="100" r="60"></circle>
        <circle class="ring" cx="100" cy="100" r="40"></circle>
      </svg>
    </div>
    <div class="place reveal-left">湖南 · HUNAN</div>
    <h2 class="reveal-left reveal-delay-1">群山褶皱里<br>告别最后一学期</h2>
    <p class="case-sub reveal-left reveal-delay-2">娄底·云山——所有人都知道：这是最后一程</p>
  </div>

  <div class="case-body">
    <p class="case-quote reveal-blur">没有红头文件，没有公开宣告。<br>但所有人都知道：这所<em>近百年校史</em>的村小，已经进入倒计时。</p>

    <div class="stat-row reveal">
      <div class="stat-item"><div class="stat-num" data-count="300">0</div><div class="stat-label">鼎盛人数</div></div>
      <div class="stat-item"><div class="stat-num" data-count="14">0</div><div class="stat-label">如今学生</div></div>
      <div class="stat-item"><div class="stat-num" data-count="4">0</div><div class="stat-label">老师</div></div>
      <div class="stat-item"><div class="stat-num" data-count="1">0</div><div class="stat-label">保安</div></div>
    </div>

    <p class="reveal" style="font-size:17px;color:#b8c5a8;max-width:700px;line-height:2.1;margin-bottom:56px;">
      硬件困境：三层教学楼仅 2 间教室在用，投影仪使用 10 多年，屏幕泛绿。<br>
      一年级不足 5 人无法开班——这不是衰落，而是<em style="color:var(--gold);font-style:normal;">结构性消失</em>。
    </p>

    <div class="kid-section">
      <h3 class="reveal">最后 14 个孩子，在告别中长大</h3>
      <div class="kid-grid">
        <div class="kid-card reveal-scale"><div class="kid-name">曾湘欧</div><p>母亲离家，父亲打工，爷爷疏于看管。曾喝墨水、爬栏杆，情绪冲动缺乏引导。</p></div>
        <div class="kid-card reveal-scale reveal-delay-1"><div class="kid-name">曾皓轩</div><p>父母离异，经历“家暴”，因为母亲吃回吐出的东西而患胃病。</p></div>
        <div class="kid-card reveal-scale reveal-delay-2"><div class="kid-name">廖雨辰</div><p>家庭关系复杂，常年住校跟校长生活，自理早熟，像小大人一样处理班级矛盾。</p></div>
        <div class="kid-card reveal-scale reveal-delay-3"><div class="kid-name">曾景桐</div><p>脑瘫学生，学校每月上门两次提供教学，守住义务教育底线。</p></div>
      </div>
    </div>

    <div class="kid-section">
      <h3 class="reveal">在废墟上维持秩序的他们</h3>
      <div class="school-grid">
        <div class="school-card reveal-left tilt">
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
        <div class="school-card reveal-right reveal-delay-1 tilt">
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

<div class="voices-section">
<section id="voices">
  <div class="big-chapter">02</div>
  <div class="reveal"><div class="section-tag">CHAPTER 02 · VOICES</div></div>
  <h2 class="section-title reveal">还有更多声音</h2>
  <p class="section-sub reveal reveal-delay-1">点击卡片，展开完整语录。</p>
  <div class="voices-grid" id="voicesGrid"></div>
</section>
</div>

<div class="case">
  <div class="case-hero scholars">
    <div class="mist"></div>
    <div class="grain"></div>
    <div class="dust-layer" id="dust-scholars"></div>
    <div class="leaf-layer" id="leaf-scholars"></div>
    <div class="case-deco">
      <svg viewBox="0 0 200 200">
        <circle class="ring" cx="100" cy="100" r="80"></circle>
        <circle class="ring ring2" cx="100" cy="100" r="60"></circle>
        <circle class="ring" cx="100" cy="100" r="40"></circle>
      </svg>
    </div>
    <div class="place reveal-left">CHAPTER 03 · 学者视角</div>
    <h2 class="reveal-left reveal-delay-1">不只是<br>“撤”或“留”</h2>
    <p class="case-sub reveal-left reveal-delay-2">在数字与情感之间，三位研究者给出的另一种思考路径</p>
  </div>
</div>

<div class="scholars-section">
<section id="scholars">
  <div class="scholar reveal">
    <div class="s-info">
      <div class="s-num">01</div>
      <h4>赵小旺</h4>
      <div class="s-title">兴平市教育局基础教育科科长</div>
    </div>
    <div class="s-content">
      <p>当前不少乡村小学的消失，并非单纯由政策推动，而是人口流动、生源减少和家长择校共同作用下的“自然消亡”。但撤并不能只按人数和效率推进，还应考虑家庭接送能力、困难儿童就学条件，以及村民对学校这一公共资产的情感与权益。</p>
      <div class="pull">“撤并不能只看数字，更要看最后一个孩子还能不能上学。”</div>
    </div>
  </div>

  <div class="scholar reveal">
    <div class="s-info">
      <div class="s-num">02</div>
      <h4>王学男</h4>
      <div class="s-title">中国教育科学研究院副研究员</div>
    </div>
    <div class="s-content">
      <p>中国乡村学校已进入“后撤并时代”。政策重点不再是大规模压缩，而是根据实际需求保留必要的小规模学校，并探索更灵活的办学方式。未来的乡村学校未必追求“大而全”，而可能转向“小规模、综合化、开放式”的教育空间。</p>
      <div class="pull">“未来的乡村学校，不一定更大，但可以更灵活、更开放。”</div>
    </div>
  </div>

  <div class="scholar reveal">
    <div class="s-info">
      <div class="s-num">03</div>
      <h4>孙艳霞</h4>
      <div class="s-title">中国海洋大学教育系副教授</div>
    </div>
    <div class="s-content">
      <p>今天的乡村小学撤并，越来越多是人口现实倒逼的结果。随着农村生源持续减少，单纯依靠情怀和投入去维持学校并不现实，“小而美”也未必真正可持续。比起一味保留，更重要的是思考撤并之后，校舍如何继续服务村庄公共生活。</p>
      <div class="pull">“没有学生的学校留不住，但校舍仍可以继续服务村庄。”</div>
    </div>
  </div>
</section>
</div>

<div class="case">
  <div class="case-hero ending">
    <div class="mist"></div>
    <div class="grain"></div>
    <div class="dust-layer" id="dust-ending"></div>
    <div class="leaf-layer" id="leaf-ending"></div>
    <div class="case-deco">
      <svg viewBox="0 0 200 200">
        <circle class="ring" cx="100" cy="100" r="80"></circle>
        <circle class="ring ring2" cx="100" cy="100" r="60"></circle>
        <circle class="ring" cx="100" cy="100" r="40"></circle>
      </svg>
    </div>
    <div class="place reveal-left">ENDING</div>
    <h2 class="reveal-left reveal-delay-1">村庄可以老去，<br>但孩子的未来，必须有路可走</h2>
    <p class="case-sub reveal-left reveal-delay-2">当最后一所村小关门，消失的不只是钟声与操场。</p>
  </div>
</div>

<footer>
  <p class="foot-title reveal">从书声琅琅到空楼寂寂，<br>这不是一所学校的故事，<br>而是<em>千万个村庄</em>共同的告别。</p>
  <div class="credits"><strong>文学与新闻传播学院</strong> · 2022级本科生毕业设计 / 2026</div>
</footer>

<script>
  const voices = [
    {name:"尹佳绮", role:"湖南云山学校 · 00后校长", preview:"毕竟是我毕业之后第一个学校、第一批学生……", quote:["毕竟是我毕业之后第一个学校、第一批学生、第一个环境。","希望我们未来都会越来越好，我会永远记得我是从这里出发的。"]},
    {name:"张娜", role:"陕西策村小学 · 16年教龄教师", preview:"撤不撤我也没有办法……", quote:["撤不撤我也没有办法。","所有学习都要靠我们去抓，没有别的环境可以依靠。"]},
    {name:"曾良平", role:"湖南云山学校 · 41年教龄老教师", preview:"我最放心不下的，是那些没钱没势的穷孩子……", quote:["我最放心不下的，是那些没钱没势的穷孩子。","形式主义表格太多，把教书的时间都占了。"]},
    {name:"黄老师", role:"广西恭城瑶族自治县 · 双科教师", preview:"山里面不会听我们外地人的……", quote:["山里面不会听我们外地人的。","撤校的事情我们在学校都是避而不谈的。"]},
    {name:"王志超", role:"衡水建国镇中心校主任", preview:"撤不撤都会有困难……", quote:["撤不撤都会有困难。","学生比较少的成绩却很好，这是不是和小班有关系。"]},
    {name:"赵小旺", role:"兴平市教育局基教科科长", preview:"教育永远围绕以学生为中心……", quote:["教育永远围绕以学生为中心，服务辖区人民群众。","未来村小撤并的趋势必然是教育资源全面整合升级。"]},
    {name:"曾皓轩", role:"湖南云山学校 · 学生", preview:"因为我讨厌妈妈……", quote:["因为我讨厌妈妈。","我不想爷爷给我送饭了，不然他会快一点变老的。"]},
    {name:"华芝涵", role:"扬州市渌洋湖中心小学 · 学生", preview:"老师有时候会拿教棍打手……", quote:["老师有时候会拿教棍打手，或者打几下头，在学业方面比较负责，但是育人方面不太行。","在农村读的小学让我看不到希望。"]}
  ];

  const grid = document.getElementById('voicesGrid');
  voices.forEach((v,i)=>{
    const card = document.createElement('div');
    card.className = 'voice-card reveal';
    card.style.transitionDelay = (i % 4 * 0.08) + 's';
    card.innerHTML = `
      <div class="v-name">${v.name}</div>
      <div class="v-role">${v.role}</div>
      <div class="v-preview">"${v.preview}"</div>
      <div class="v-expand">${v.quote.map(q=>`<p>"${q}"</p>`).join('')}</div>
      <div class="v-toggle"><span class="icon">+</span><span class="txt">展开完整语录</span></div>
    `;
    card.addEventListener('click',(e)=>{
      e.stopPropagation();
      card.classList.toggle('expanded');
      const txt = card.querySelector('.v-toggle .txt');
      txt.textContent = card.classList.contains('expanded') ? '收起' : '展开完整语录';
    });
    grid.appendChild(card);
  });

  const observer = new IntersectionObserver((entries)=>{
    entries.forEach(entry=>{
      if(entry.isIntersecting){
        entry.target.classList.add('visible');

        if(entry.target.classList.contains('stat-row')){
          entry.target.querySelectorAll('.stat-num').forEach(el=>animateCount(el));
        }
      }
    });
  },{threshold:.12});

  document.querySelectorAll('.reveal,.reveal-left,.reveal-right,.reveal-scale,.reveal-blur').forEach(el=>observer.observe(el));

  function animateCount(el){
    if(el.dataset.done) return;
    el.dataset.done = 1;
    const target = +el.dataset.count;
    const dur = 1400;
    const start = performance.now();
    function step(t){
      const p = Math.min(1,(t-start)/dur);
      const eased = 1 - Math.pow(1-p,3);
      el.textContent = Math.round(target*eased);
      if(p<1) requestAnimationFrame(step);
    }
    requestAnimationFrame(step);
  }

  window.addEventListener('scroll',()=>{
    const h = document.documentElement;
    const scrolled = (h.scrollTop / (h.scrollHeight - h.clientHeight)) * 100;
    document.getElementById('progress').style.width = scrolled + '%';

    const nav = document.querySelector('nav');
    if(window.scrollY > 50){
      nav.style.background = 'rgba(244,245,238,0.93)';
      nav.style.boxShadow = '0 4px 20px rgba(61,107,74,0.08)';
    }else{
      nav.style.background = 'rgba(244,245,238,0.80)';
      nav.style.boxShadow = 'none';
    }

    document.querySelectorAll('.big-chapter').forEach(el=>{
      const rect = el.getBoundingClientRect();
      const offset = (window.innerHeight / 2 - rect.top) * 0.08;
      el.style.transform = `translateY(calc(-50% + ${offset}px))`;
    });
  });

  const dot = document.getElementById('cursorDot');
  const ring = document.getElementById('cursorRing');
  let mouseX = 0, mouseY = 0, ringX = 0, ringY = 0;

  window.addEventListener('mousemove', e=>{
    mouseX = e.clientX;
    mouseY = e.clientY;
    dot.style.left = mouseX + 'px';
    dot.style.top = mouseY + 'px';
  });

  function loop(){
    ringX += (mouseX - ringX) * 0.18;
    ringY += (mouseY - ringY) * 0.18;
    ring.style.left = ringX + 'px';
    ring.style.top = ringY + 'px';
    requestAnimationFrame(loop);
  }
  loop();

  function bindHover(){
    document.querySelectorAll('a,.voice-card,.school-card,.stat-item,.scholar,.kid-card,button,.data-card,.phase-item').forEach(el=>{
      el.addEventListener('mouseenter', ()=>ring.classList.add('hover'));
      el.addEventListener('mouseleave', ()=>ring.classList.remove('hover'));
    });
  }
  bindHover();
  setTimeout(bindHover, 120);

  window.addEventListener('mousedown', e=>{
    ring.classList.add('click');
    const r = document.createElement('div');
    r.className = 'ripple';
    r.style.left = e.clientX + 'px';
    r.style.top = e.clientY + 'px';
    document.body.appendChild(r);
    setTimeout(()=>r.remove(),800);
  });
  window.addEventListener('mouseup', ()=>ring.classList.remove('click'));

  const heroGlow = document.getElementById('heroGlow');
  const hero = document.querySelector('.hero');
  hero.addEventListener('mousemove', e=>{
    const rect = hero.getBoundingClientRect();
    heroGlow.style.left = (e.clientX - rect.left) + 'px';
    heroGlow.style.top = (e.clientY - rect.top) + 'px';
    heroGlow.style.opacity = '1';
  });
  hero.addEventListener('mouseleave', ()=>heroGlow.style.opacity='0');

  window.addEventListener('scroll',()=>{
    const sc = window.scrollY;
    if(sc < window.innerHeight){
      const hc = document.querySelector('.hero-content');
      hc.style.transform = `translateY(${sc * 0.22}px)`;
      hc.style.opacity = 1 - sc / (window.innerHeight * 0.9);
    }
  });

  document.querySelectorAll('.tilt').forEach(card=>{
    card.addEventListener('mousemove', e=>{
      const rect = card.getBoundingClientRect();
      const x = e.clientX - rect.left;
      const y = e.clientY - rect.top;
      const cx = rect.width/2, cy = rect.height/2;
      const rx = (y - cy) / cy * -5;
      const ry = (x - cx) / cx * 5;
      card.style.transform = `translateY(-10px) perspective(1000px) rotateX(${rx}deg) rotateY(${ry}deg)`;
    });
    card.addEventListener('mouseleave', ()=>card.style.transform='');
  });

  document.querySelectorAll('nav a').forEach(a=>{
    a.addEventListener('click', ()=>{
      ring.classList.add('hover');
      setTimeout(()=>ring.classList.remove('hover'), 400);
    });
  });

  /* 数据图 */
  const schoolData = [
    { year: 1997, value: 51.3, phase: 0 },
    { year: 2000, value: 44.7, phase: 0 },
    { year: 2001, value: 41.62, phase: 1 },
    { year: 2010, value: 21.8, phase: 2 },
    { year: 2012, value: 15.5, phase: 2 },
    { year: 2023, value: 7.06, phase: 3 }
  ];

  const yearRange = document.getElementById('yearRange');
  const yearNow = document.getElementById('yearNow');
  const schoolValue = document.getElementById('schoolValue');
  const xLabels = document.getElementById('xLabels');
  const linePath = document.getElementById('linePath');
  const lineGlow = document.getElementById('lineGlow');
  const areaPath = document.getElementById('areaPath');
  const pointsGroup = document.getElementById('points');
  const focusDot = document.getElementById('focusDot');
  const focusRing = document.getElementById('focusRing');
  const tooltip = document.getElementById('tooltip');
  const valueBadge = document.getElementById('valueBadge');

  const chart = { left:74, right:670, top:50, bottom:320, height:270, maxY:55 };

  function xPos(i){
    const step = (chart.right - chart.left) / (schoolData.length - 1);
    return chart.left + i * step;
  }
  function yPos(val){
    return chart.bottom - (val / chart.maxY) * chart.height;
  }

  function renderChart(){
    xLabels.innerHTML = '';
    pointsGroup.innerHTML = '';

    let lineD = '';
    let areaD = '';

    schoolData.forEach((d,i)=>{
      const x = xPos(i);
      const y = yPos(d.value);

      lineD += `${i===0?'M':'L'} ${x} ${y} `;
      if(i===0) areaD = `M ${x} ${chart.bottom} L ${x} ${y} `;
      else areaD += `L ${x} ${y} `;

      const tx = document.createElementNS('http://www.w3.org/2000/svg','text');
      tx.setAttribute('x', x - 18);
      tx.setAttribute('y', 352);
      tx.setAttribute('fill', '#5f6f61');
      tx.setAttribute('font-size', '12');
      tx.setAttribute('font-family', 'Cormorant Garamond, serif');
      tx.textContent = d.year;
      xLabels.appendChild(tx);

      const c = document.createElementNS('http://www.w3.org/2000/svg','circle');
      c.setAttribute('cx', x);
      c.setAttribute('cy', y);
      c.setAttribute('r', 5);
      c.setAttribute('fill', '#214230');
      c.style.cursor = 'pointer';

      c.addEventListener('mouseenter', ()=>showTip(x,y,d));
      c.addEventListener('mouseleave', hideTip);
      c.addEventListener('click', ()=>{
        yearRange.value = i;
        updateFocus(i);
      });

      pointsGroup.appendChild(c);
    });

    const lastX = xPos(schoolData.length-1);
    areaD += `L ${lastX} ${chart.bottom} Z`;

    linePath.setAttribute('d', lineD.trim());
    lineGlow.setAttribute('d', lineD.trim());
    areaPath.setAttribute('d', areaD.trim());

    const total = linePath.getTotalLength();
    linePath.style.strokeDasharray = total;
    linePath.style.strokeDashoffset = total;
    lineGlow.style.strokeDasharray = total;
    lineGlow.style.strokeDashoffset = total;
  }

  function showTip(x,y,d){
    tooltip.style.left = x + 'px';
    tooltip.style.top = y + 'px';
    tooltip.innerHTML = `${d.year}年：${d.value} 万所`;
    tooltip.style.opacity = 1;
  }
  function hideTip(){
    tooltip.style.opacity = 0;
  }

  function updateFocus(index){
    const d = schoolData[index];
    const x = xPos(index);
    const y = yPos(d.value);

    focusDot.setAttribute('cx', x);
    focusDot.setAttribute('cy', y);
    focusRing.setAttribute('cx', x);
    focusRing.setAttribute('cy', y);

    yearNow.textContent = d.year;
    schoolValue.textContent = d.value;

    valueBadge.classList.add('flash');
    setTimeout(()=>valueBadge.classList.remove('flash'), 240);

    document.querySelectorAll('.phase-item').forEach(p=>p.classList.remove('active'));
    const targetPhase = document.querySelector(`.phase-item[data-phase="${d.phase}"]`);
    if(targetPhase) targetPhase.classList.add('active');
  }

  yearRange.addEventListener('input', e=>{
    updateFocus(parseInt(e.target.value,10));
  });

  renderChart();
  updateFocus(0);

  const chartObserver = new IntersectionObserver((entries)=>{
    entries.forEach(entry=>{
      if(entry.isIntersecting){
        requestAnimationFrame(()=>{
          linePath.style.transition = 'stroke-dashoffset 1.8s cubic-bezier(.2,.7,.2,1)';
          lineGlow.style.transition = 'stroke-dashoffset 1.8s cubic-bezier(.2,.7,.2,1)';
          linePath.style.strokeDashoffset = '0';
          lineGlow.style.strokeDashoffset = '0';

          document.querySelectorAll('.bar i').forEach((bar,i)=>{
            setTimeout(()=>bar.style.width = bar.dataset.width + '%', i * 120);
          });
        });
        chartObserver.unobserve(entry.target);
      }
    });
  },{threshold:.3});
  chartObserver.observe(document.querySelector('.data-card'));

  function animateTextNumber(el, end, suffix = ''){
    const start = performance.now();
    const duration = 1400;
    function frame(now){
      const p = Math.min((now - start) / duration, 1);
      const ease = 1 - Math.pow(1 - p, 3);
      const val = end * ease;
      el.textContent = Number.isInteger(end) ? Math.floor(val) + suffix : val.toFixed(1) + suffix;
      if(p < 1) requestAnimationFrame(frame);
      else el.textContent = (Number.isInteger(end) ? end : end.toFixed(1)) + suffix;
    }
    requestAnimationFrame(frame);
  }

  const statObserver = new IntersectionObserver((entries)=>{
    entries.forEach(entry=>{
      if(entry.isIntersecting){
        animateTextNumber(document.getElementById('dropPercent'), 86.2, '%');
        animateTextNumber(document.getElementById('dailyRate'), 63);
        animateTextNumber(document.getElementById('remainValue'), 7.06);
        statObserver.unobserve(entry.target);
      }
    });
  },{threshold:.4});
  statObserver.observe(document.querySelector('.stats-grid'));

  function makeLeaves(id, count = 12){
    const layer = document.getElementById(id);
    if(!layer) return;
    const colors = ['green','gold','brown'];
    for(let i=0;i<count;i++){
      const leaf = document.createElement('span');
      leaf.className = `leaf ${colors[Math.floor(Math.random()*colors.length)]}`;
      leaf.style.left = Math.random() * 100 + '%';
      leaf.style.animationDuration = (10 + Math.random()*12) + 's';
      leaf.style.animationDelay = (Math.random()*10) + 's';
      leaf.style.width = (10 + Math.random()*14) + 'px';
      leaf.style.height = (7 + Math.random()*10) + 'px';
      leaf.style.opacity = 0.14 + Math.random()*0.28;
      layer.appendChild(leaf);
    }
  }

  function makeDust(id, count = 18){
    const layer = document.getElementById(id);
    if(!layer) return;
    for(let i=0;i<count;i++){
      const d = document.createElement('span');
      d.className = 'dust';
      d.style.left = Math.random()*100 + '%';
      d.style.top = (40 + Math.random()*60) + '%';
      const size = 1 + Math.random()*3;
      d.style.width = size + 'px';
      d.style.height = size + 'px';
      d.style.animationDuration = (8 + Math.random()*10) + 's';
      d.style.animationDelay = (Math.random()*8) + 's';
      layer.appendChild(d);
    }
  }

  ['leaf-hero','leaf-shaanxi','leaf-hunan','leaf-scholars','leaf-ending'].forEach(id=>makeLeaves(id,12));
  ['dust-hero','dust-shaanxi','dust-hunan','dust-scholars','dust-ending'].forEach(id=>makeDust(id,18));
</script>

</body>
</html>
