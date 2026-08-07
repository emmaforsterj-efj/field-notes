<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Field Notes — A Health Guide</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Fraunces:ital,opsz,wght@0,9..144,500;0,9..144,600;0,9..144,700;1,9..144,500&family=Inter:wght@400;500;600;700&family=IBM+Plex+Mono:wght@400;500&display=swap" rel="stylesheet">
<style>
  :root{
    --bg:#F5F6EF;
    --surface:#FFFFFF;
    --ink:#20261D;
    --muted:#6C7266;
    --line:#DEE1D2;
    --accent:#2D6A5F;
    --accent-ink:#F5F6EF;
    --accent-soft:#E4EDE6;
    --danger:#A6433C;
    --radius:14px;

    --tag-respiratory:#2D6A5F;
    --tag-skin:#B5652E;
    --tag-digestive:#7A8B4F;
    --tag-infectious:#A6433C;
    --tag-mind:#5B6EA8;
    --tag-endocrine:#C79A3D;
    --tag-muscoskel:#8C6E4F;
    --tag-blood:#935F70;
  }

  *{box-sizing:border-box;}
  html{scroll-behavior:smooth;}
  @media (prefers-reduced-motion: reduce){
    html{scroll-behavior:auto;}
    *{animation-duration:0.01ms !important; transition-duration:0.01ms !important;}
  }

  body{
    margin:0;
    background:var(--bg);
    color:var(--ink);
    font-family:'Inter',sans-serif;
    -webkit-font-smoothing:antialiased;
  }

  a{color:var(--accent);}
  ::selection{background:var(--accent-soft);}
  :focus-visible{outline:3px solid var(--accent); outline-offset:2px; border-radius:4px;}
  .mono{font-family:'IBM Plex Mono',monospace;}

  header.site{
    position:sticky; top:0; z-index:40;
    background:rgba(245,246,239,0.92);
    backdrop-filter:blur(6px);
    border-bottom:1px solid var(--line);
  }
  .site-inner{
    max-width:1180px; margin:0 auto;
    padding:14px 24px;
    display:flex; align-items:center; justify-content:space-between; gap:16px;
  }
  .brand{display:flex; align-items:baseline; gap:8px;}
  .brand .mark{font-family:'Fraunces',serif; font-weight:700; font-size:22px; letter-spacing:-0.01em;}
  .brand .tag{font-size:11px; color:var(--muted); letter-spacing:0.06em; text-transform:uppercase;}
  .nav-actions{display:flex; gap:10px; align-items:center;}
  .btn{
    font-family:'Inter',sans-serif; font-weight:600; font-size:13.5px;
    padding:9px 15px; border-radius:999px; border:1px solid var(--line);
    background:var(--surface); color:var(--ink); cursor:pointer;
    display:inline-flex; align-items:center; gap:6px;
    transition:border-color .15s ease, transform .1s ease;
  }
  .btn:hover{border-color:var(--accent);}
  .btn:active{transform:scale(0.97);}
  .btn.primary{background:var(--accent); color:var(--accent-ink); border-color:var(--accent);}
  .count-pill{
    background:var(--accent); color:var(--accent-ink);
    font-family:'IBM Plex Mono',monospace; font-size:10.5px;
    border-radius:999px; padding:1px 7px; margin-left:2px;
  }

  .hero{max-width:1180px; margin:0 auto; padding:56px 24px 28px;}
  .hero .eyebrow{
    font-family:'IBM Plex Mono',monospace; font-size:12px; color:var(--accent);
    text-transform:uppercase; letter-spacing:0.1em; margin-bottom:14px;
    display:flex; align-items:center; gap:8px;
  }
  .hero .eyebrow::before{content:''; width:16px; height:1px; background:var(--accent); display:inline-block;}
  .hero h1{
    font-family:'Fraunces',serif; font-weight:600; font-style:italic;
    font-size:clamp(32px,5vw,52px); line-height:1.05; margin:0 0 16px; max-width:14ch;
    letter-spacing:-0.01em;
  }
  .hero p.lede{font-size:16.5px; color:var(--muted); max-width:56ch; line-height:1.6; margin:0 0 28px;}

  .disclaimer{
    display:flex; gap:12px; align-items:flex-start;
    background:var(--surface); border:1px solid var(--line); border-left:3px solid var(--accent);
    border-radius:10px; padding:14px 16px; max-width:640px; margin-bottom:32px;
  }
  .disclaimer svg{flex-shrink:0; margin-top:2px;}
  .disclaimer p{margin:0; font-size:13px; line-height:1.55; color:var(--muted);}
  .disclaimer strong{color:var(--ink);}

  .search-wrap{position:relative; max-width:560px; margin-bottom:8px;}
  .search-box{
    display:flex; align-items:center; gap:10px;
    background:var(--surface); border:1.5px solid var(--line); border-radius:12px;
    padding:13px 16px; transition:border-color .15s ease;
  }
  .search-box:focus-within{border-color:var(--accent);}
  .search-box input{border:none; outline:none; background:transparent; flex:1; font-family:'Inter',sans-serif; font-size:15px; color:var(--ink);}
  .search-box input::placeholder{color:#9BA396;}
  .search-status{font-size:12px; color:var(--muted); margin-top:8px; min-height:16px;}

  .search-results{
    position:absolute; top:calc(100% + 8px); left:0; right:0;
    background:var(--surface); border:1px solid var(--line); border-radius:12px;
    box-shadow:0 12px 32px rgba(32,38,29,0.12);
    max-height:360px; overflow-y:auto; z-index:30;
    display:none;
  }
  .search-results.open{display:block;}
  .search-result-item{display:flex; flex-direction:column; gap:2px; padding:12px 16px; cursor:pointer; border-bottom:1px solid var(--line);}
  .search-result-item:last-child{border-bottom:none;}
  .search-result-item:hover, .search-result-item:focus-visible{background:var(--accent-soft);}
  .search-result-item .r-title{font-weight:600; font-size:14px;}
  .search-result-item .r-snippet{font-size:12.5px; color:var(--muted); line-height:1.4;}

  .layout{max-width:1180px; margin:0 auto; padding:0 24px 80px; display:grid; grid-template-columns:220px 1fr; gap:32px;}
  @media (max-width:820px){.layout{grid-template-columns:1fr;}}

  .rail{position:sticky; top:88px; align-self:start;}
  .rail-title{font-family:'IBM Plex Mono',monospace; font-size:11px; color:var(--muted); text-transform:uppercase; letter-spacing:0.08em; margin-bottom:12px;}
  .rail-list{list-style:none; margin:0; padding:0; display:flex; flex-direction:column; gap:2px;}
  .rail-item button{
    width:100%; text-align:left; background:none; border:none; cursor:pointer;
    display:flex; align-items:center; gap:10px;
    padding:9px 10px; border-radius:8px;
    font-family:'Inter',sans-serif; font-size:13.5px; color:var(--ink);
  }
  .rail-item button:hover{background:var(--surface);}
  .rail-item.active button{background:var(--surface); box-shadow:inset 3px 0 0 var(--dot);}
  .rail-item .dot{width:9px; height:9px; border-radius:2px; background:var(--dot); flex-shrink:0;}
  .rail-item .n{margin-left:auto; font-family:'IBM Plex Mono',monospace; font-size:11px; color:var(--muted);}

  @media (max-width:820px){
    .rail{position:static; padding-bottom:8px; border-bottom:1px solid var(--line); margin-bottom:8px;}
    .rail-list{flex-direction:row; overflow-x:auto; gap:8px; padding-bottom:6px;}
    .rail-item button{white-space:nowrap; border:1px solid var(--line);}
  }

  .grid-head{display:flex; align-items:baseline; justify-content:space-between; margin-bottom:16px; gap:12px; flex-wrap:wrap;}
  .grid-head h2{font-family:'Fraunces',serif; font-weight:600; font-size:22px; margin:0;}
  .grid-head .sub{font-size:12.5px; color:var(--muted); font-family:'IBM Plex Mono',monospace;}

  .card-grid{display:grid; grid-template-columns:repeat(auto-fill,minmax(240px,1fr)); gap:16px;}
  .card{
    background:var(--surface); border:1px solid var(--line); border-radius:var(--radius);
    padding:16px; cursor:pointer; position:relative; overflow:hidden;
    display:flex; flex-direction:column; gap:8px; min-height:150px;
    transition:transform .12s ease, box-shadow .12s ease;
  }
  .card:hover, .card:focus-visible{transform:translateY(-2px); box-shadow:0 10px 24px rgba(32,38,29,0.10);}
  .card::before{content:''; position:absolute; top:0; left:0; width:100%; height:3px; background:var(--dot);}
  .card .tag-chip{
    align-self:flex-start;
    font-family:'IBM Plex Mono',monospace; font-size:10.5px; text-transform:uppercase; letter-spacing:0.05em;
    color:var(--dot); background:color-mix(in srgb, var(--dot) 12%, white);
    padding:3px 8px; border-radius:5px;
  }
  .card h3{font-family:'Fraunces',serif; font-weight:600; font-size:17px; margin:0; line-height:1.25;}
  .card p{font-size:13px; color:var(--muted); line-height:1.5; margin:0; flex:1;
    display:-webkit-box; -webkit-line-clamp:3; -webkit-box-orient:vertical; overflow:hidden;}
  .card .skeleton{background:linear-gradient(90deg,var(--line) 25%,#eceee2 50%,var(--line) 75%); background-size:200% 100%; animation:shimmer 1.4s infinite; border-radius:6px; height:12px;}
  @keyframes shimmer{0%{background-position:200% 0;}100%{background-position:-200% 0;}}

  .empty-state{grid-column:1/-1; text-align:center; padding:48px 20px; color:var(--muted);}
  .empty-state .mono{display:block; margin-bottom:6px; color:var(--accent);}

  .overlay{position:fixed; inset:0; background:rgba(32,38,29,0.35); z-index:50; display:none; align-items:stretch; justify-content:flex-end;}
  .overlay.open{display:flex;}
  .panel{width:min(400px,92vw); background:var(--bg); height:100%; padding:24px; overflow-y:auto; border-left:1px solid var(--line);}
  .panel-head{display:flex; justify-content:space-between; align-items:center; margin-bottom:20px;}
  .panel-head h2{font-family:'Fraunces',serif; font-size:20px; margin:0;}
  .icon-btn{background:none; border:none; cursor:pointer; padding:6px; border-radius:8px;}
  .icon-btn:hover{background:var(--accent-soft);}
  .history-item{display:flex; align-items:center; gap:10px; padding:10px; border-radius:10px; cursor:pointer; border:1px solid transparent;}
  .history-item:hover{background:var(--surface); border-color:var(--line);}
  .history-item .dot{width:8px; height:8px; border-radius:2px; flex-shrink:0; background:var(--dot);}
  .history-item .h-body{flex:1; min-width:0;}
  .history-item .h-title{font-weight:600; font-size:13.5px; white-space:nowrap; overflow:hidden; text-overflow:ellipsis;}
  .history-item .h-time{font-size:11px; color:var(--muted); font-family:'IBM Plex Mono',monospace;}
  .history-empty{color:var(--muted); font-size:13px; padding:20px 0;}
  .clear-link{font-size:12px; color:var(--danger); background:none; border:none; cursor:pointer; padding:0; margin-top:14px;}

  .detail-overlay{position:fixed; inset:0; background:rgba(32,38,29,0.45); z-index:60; display:none; align-items:center; justify-content:center; padding:20px;}
  .detail-overlay.open{display:flex;}
  .detail-card{
    background:var(--bg); border-radius:18px; max-width:640px; width:100%; max-height:85vh; overflow-y:auto;
    padding:32px; position:relative; border:1px solid var(--line);
  }
  .detail-card .close-btn{position:absolute; top:16px; right:16px;}
  .detail-tag{
    font-family:'IBM Plex Mono',monospace; font-size:11px; text-transform:uppercase; letter-spacing:0.06em;
    color:var(--dot); margin-bottom:10px; display:inline-block;
  }
  .detail-card h2{font-family:'Fraunces',serif; font-style:italic; font-weight:600; font-size:30px; margin:0 0 14px; max-width:22ch;}
  .detail-card h3{font-family:'Fraunces',serif; font-weight:600; font-size:15px; margin:18px 0 6px;}
  .detail-card .extract{font-size:15px; line-height:1.7; color:var(--ink); margin-bottom:12px;}
  .detail-card ul{margin:0 0 4px; padding-left:20px; font-size:14px; line-height:1.7; color:var(--ink);}
  .detail-card .thumb{width:100%; max-height:220px; object-fit:cover; border-radius:12px; margin-bottom:18px; border:1px solid var(--line);}
  .detail-card .src-link{font-size:13px; font-weight:600; display:inline-block; margin-top:16px;}
  .detail-note{margin-top:22px; padding-top:18px; border-top:1px dashed var(--line); font-size:12.5px; color:var(--muted); line-height:1.6;}

  /* ---------- Quiz ---------- */
  .quiz-progress{font-family:'IBM Plex Mono',monospace; font-size:12px; color:var(--muted); margin-bottom:14px;}
  .quiz-option{
    display:block; width:100%; text-align:left; padding:14px 16px; margin-bottom:10px;
    border:1.5px solid var(--line); border-radius:10px; background:var(--surface); cursor:pointer;
    font-family:'Inter',sans-serif; font-size:14.5px; color:var(--ink);
    transition:border-color .15s ease, background .15s ease;
  }
  .quiz-option:hover:not(:disabled){border-color:var(--accent);}
  .quiz-option.correct{border-color:#4C7A5A; background:#E4EDE6;}
  .quiz-option.incorrect{border-color:var(--danger); background:#F6E7E5;}
  .quiz-option:disabled{cursor:default;}
  .quiz-category-grid{display:grid; grid-template-columns:repeat(auto-fill,minmax(150px,1fr)); gap:10px; margin-top:16px;}
  .quiz-category-btn{
    border:1.5px solid var(--line); background:var(--surface); border-radius:12px; padding:14px;
    cursor:pointer; text-align:left; font-family:'Inter',sans-serif;
  }
  .quiz-category-btn:hover:not(:disabled){border-color:var(--dot);}
  .quiz-category-btn:disabled{opacity:0.4; cursor:not-allowed;}
  .quiz-category-btn .dot{width:9px; height:9px; border-radius:2px; background:var(--dot); display:inline-block; margin-bottom:8px;}
  .quiz-category-btn .qc-label{display:block; font-weight:600; font-size:14px; color:var(--ink);}
  .quiz-category-btn .qc-count{display:block; font-family:'IBM Plex Mono',monospace; font-size:11px; color:var(--muted); margin-top:2px;}
  .quiz-result{text-align:center; padding:20px 0;}
  .quiz-result .score-big{font-family:'Fraunces',serif; font-size:48px; font-weight:600; margin:12px 0;}
  .quiz-past{margin-top:24px; border-top:1px dashed var(--line); padding-top:16px;}
  .quiz-past-item{display:flex; justify-content:space-between; font-size:12.5px; color:var(--muted); padding:6px 0; font-family:'IBM Plex Mono',monospace;}

  /* ---------- Symptom checker ---------- */
  .chip-row{display:flex; flex-wrap:wrap; gap:8px; margin:14px 0;}
  .chip{
    display:inline-flex; align-items:center; gap:6px;
    background:var(--accent-soft); color:var(--accent); border-radius:999px;
    padding:6px 8px 6px 12px; font-size:13px; font-weight:600;
  }
  .chip button{background:none; border:none; cursor:pointer; color:var(--accent); display:flex; align-items:center; padding:3px; border-radius:50%;}
  .chip button:hover{background:rgba(45,106,95,0.15);}
  .match-item{
    display:flex; gap:12px; align-items:flex-start; justify-content:space-between;
    padding:14px; border:1px solid var(--line); border-radius:12px; margin-bottom:10px;
    cursor:pointer; background:var(--surface); transition:border-color .15s ease;
  }
  .match-item:hover{border-color:var(--dot);}
  .match-item h4{margin:2px 0 4px; font-family:'Fraunces',serif; font-size:16px;}
  .match-item .matched-syms{font-size:12px; color:var(--muted); line-height:1.5;}
  .match-score{
    font-family:'IBM Plex Mono',monospace; font-size:11px; font-weight:600; color:var(--dot);
    background:color-mix(in srgb, var(--dot) 12%, white);
    padding:4px 9px; border-radius:6px; white-space:nowrap; flex-shrink:0;
  }

  footer{max-width:1180px; margin:0 auto; padding:24px; color:var(--muted); font-size:12px; text-align:center;}
</style>
</head>
<body>

<header class="site">
  <div class="site-inner">
    <div class="brand">
      <span class="mark">Field Notes</span>
      <span class="tag">a health index</span>
    </div>
    <div class="nav-actions">
      <button class="btn" id="checkerBtn">
        <svg width="15" height="15" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M11 2v6M8 5h6M4 22h16M6 22V11a4 4 0 0 1 4-4h4a4 4 0 0 1 4 4v11"/></svg>
        Check symptoms
      </button>
      <button class="btn" id="quizBtn">
        <svg width="15" height="15" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M9 9a3 3 0 1 1 4 2.8c-.6.3-1 1-1 1.7v.5M12 17h.01"/><circle cx="12" cy="12" r="9"/></svg>
        Quiz
      </button>
      <button class="btn" id="historyBtn">
        <svg width="15" height="15" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M12 8v4l3 3"/><circle cx="12" cy="12" r="9"/></svg>
        History <span class="count-pill" id="historyCount">0</span>
      </button>
    </div>
  </div>
</header>

<section class="hero">
  <div class="eyebrow">Vol. 1 — Common conditions</div>
  <h1>Understand what's going on with your body.</h1>
  <p class="lede">Browse conditions by body system, search anything you're wondering about, quiz yourself on what you've learned, and keep a running log of what you've looked into.</p>

  <div class="disclaimer">
    <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="#A6433C" stroke-width="2"><circle cx="12" cy="12" r="10"/><path d="M12 8v5M12 16h.01"/></svg>
    <p><strong>This is an educational reference, not a diagnosis.</strong> If something feels wrong or you're worried about a symptom, talk to a doctor, nurse, or another trusted adult. This index can't tell you what's actually going on with you.</p>
  </div>

  <div class="search-wrap">
    <div class="search-box">
      <svg width="17" height="17" viewBox="0 0 24 24" fill="none" stroke="#6C7266" stroke-width="2"><circle cx="11" cy="11" r="8"/><path d="m21 21-4.3-4.3"/></svg>
      <input type="text" id="searchInput" placeholder="Search any condition — e.g. 'sore throat', 'ADHD'..." autocomplete="off">
    </div>
    <div class="search-results" id="searchResults"></div>
    <div class="search-status" id="searchStatus"></div>
  </div>
</section>

<div class="layout">
  <nav class="rail">
    <div class="rail-title">Body systems</div>
    <ul class="rail-list" id="railList"></ul>
  </nav>

  <main>
    <div class="grid-head">
      <h2 id="gridTitle">All entries</h2>
      <span class="sub mono" id="gridSub"></span>
    </div>
    <div class="card-grid" id="cardGrid"></div>
  </main>
</div>

<footer>Some content is supplemented live from Wikipedia and may not reflect current medical consensus. Not a substitute for professional care.</footer>

<div class="overlay" id="historyOverlay">
  <div class="panel">
    <div class="panel-head">
      <h2>Your history</h2>
      <button class="icon-btn" id="closeHistory" aria-label="Close history">
        <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M18 6 6 18M6 6l12 12"/></svg>
      </button>
    </div>
    <div id="historyList"></div>
  </div>
</div>

<div class="detail-overlay" id="detailOverlay">
  <div class="detail-card" id="detailCard"></div>
</div>

<div class="detail-overlay" id="quizOverlay">
  <div class="detail-card" id="quizCard"></div>
</div>

<div class="detail-overlay" id="checkerOverlay">
  <div class="detail-card" id="checkerCard"></div>
</div>

<script>
(function(){
  const TAGS = [
    {id:'respiratory', label:'Respiratory', color:'var(--tag-respiratory)'},
    {id:'skin', label:'Skin', color:'var(--tag-skin)'},
    {id:'digestive', label:'Digestive', color:'var(--tag-digestive)'},
    {id:'infectious', label:'Infectious', color:'var(--tag-infectious)'},
    {id:'mind', label:'Mind & Nerves', color:'var(--tag-mind)'},
    {id:'endocrine', label:'Endocrine', color:'var(--tag-endocrine)'},
    {id:'muscoskel', label:'Muscle & Bone', color:'var(--tag-muscoskel)'},
    {id:'blood', label:'Blood Disorders', color:'var(--tag-blood)'},
  ];

  const DISEASES = [
{title:"Iron-deficiency anemia",display:"Iron Deficiency Anemia",tag:"blood",
overview:"Iron deficiency anemia occurs when your body doesn't have enough iron to produce healthy red blood cells.",
symptoms:["Fatigue","Weakness","Pale skin","Shortness of breath","Dizziness"],
causes:["Low dietary iron","Blood loss","Poor iron absorption"],
diagnosis:["CBC blood test","Ferritin test","Iron studies"],
treatment:["Iron supplements","Iron-rich foods","Treat the underlying cause"],
prevention:["Eat iron-rich foods","Pair iron with vitamin C"],
funFact:"Iron deficiency affects over one billion people worldwide."},
{title:"Thalassemia",display:"Thalassemia",tag:"blood",
overview:"Thalassemia is an inherited blood disorder that reduces the amount of hemoglobin your body produces.",
symptoms:["Fatigue","Pale skin","Slow growth"],
causes:["Inherited genetic mutation"],
diagnosis:["Blood tests","Genetic testing"],
treatment:["Blood transfusions","Iron chelation therapy"],
prevention:["Genetic counselling"],
funFact:"Thalassemia is one of the world's most common inherited blood disorders."},
{title:"Sickle cell disease",display:"Sickle Cell Disease",tag:"blood",
overview:"Sickle cell disease is an inherited condition that causes red blood cells to become stiff and crescent-shaped, reducing oxygen delivery around the body.",
symptoms:["Episodes of severe pain","Fatigue","Swollen hands and feet","Frequent infections","Delayed growth"],
causes:["Inherited mutation in the hemoglobin gene"],
diagnosis:["Blood test","Newborn screening","Genetic testing"],
treatment:["Pain relief","Hydration","Hydroxyurea","Blood transfusions","Bone marrow transplant in some cases"],
prevention:["Genetic counselling","Avoid dehydration","Regular vaccinations"],
funFact:"People with sickle cell trait have some natural protection against malaria."},
{title:"Hemophilia",display:"Hemophilia",tag:"blood",
overview:"Hemophilia is an inherited bleeding disorder where the blood cannot clot properly because certain clotting factors are missing.",
symptoms:["Easy bruising","Frequent nosebleeds","Bleeding into joints","Long-lasting bleeding after injuries"],
causes:["Inherited mutation affecting clotting factors"],
diagnosis:["Clotting factor blood tests","Genetic testing"],
treatment:["Replacement clotting factor injections","Preventive therapy"],
prevention:["Avoid contact sports","Regular specialist care"],
funFact:"Hemophilia was once known as the 'Royal Disease' because it spread through several European royal families."},
{title:"Leukemia",display:"Leukemia",tag:"blood",
overview:"Leukemia is a cancer of the blood-forming tissues that causes the body to produce abnormal white blood cells.",
symptoms:["Fatigue","Frequent infections","Easy bruising","Weight loss","Fever"],
causes:["Genetic mutations","Previous radiation exposure","Certain chemicals"],
diagnosis:["Complete blood count","Bone marrow biopsy","Genetic testing"],
treatment:["Chemotherapy","Targeted therapy","Bone marrow transplant","Immunotherapy"],
prevention:["Most cases cannot be prevented"],
funFact:"Leukemia is the most common cancer diagnosed in children."},
{title:"Vitamin B12 deficiency anemia",display:"Vitamin B12 Deficiency Anemia",tag:"blood",
overview:"Vitamin B12 deficiency anemia occurs when the body lacks enough vitamin B12 to produce healthy red blood cells.",
symptoms:["Fatigue","Pale skin","Pins and needles","Memory problems","Difficulty walking"],
causes:["Poor diet","Pernicious anemia","Digestive disorders"],
diagnosis:["Blood tests","Vitamin B12 level","Complete blood count"],
treatment:["Vitamin B12 tablets","Vitamin B12 injections"],
prevention:["Eat foods rich in vitamin B12","Take supplements if needed"],
funFact:"Unlike iron deficiency, B12 deficiency can damage nerves if left untreated."},
{title:"Aplastic anemia",display:"Aplastic Anemia",tag:"blood",
overview:"Aplastic anemia is a rare condition where the bone marrow fails to produce enough new blood cells.",
symptoms:["Extreme tiredness","Frequent infections","Easy bruising","Shortness of breath"],
causes:["Autoimmune disease","Radiation","Certain medications","Unknown causes"],
diagnosis:["Blood tests","Bone marrow biopsy"],
treatment:["Blood transfusions","Immunosuppressant medicines","Bone marrow transplant"],
prevention:["No reliable prevention exists"],
funFact:"Aplastic anemia affects all three major blood cell types at once."},
{title:"Polycythemia vera",display:"Polycythemia Vera",tag:"blood",
overview:"Polycythemia vera is a rare blood disorder where the body produces too many red blood cells, making the blood thicker than normal.",
symptoms:["Headaches","Dizziness","Itchy skin","Blurred vision"],
causes:["Mutation in the JAK2 gene"],
diagnosis:["Blood tests","Bone marrow biopsy","Genetic testing"],
treatment:["Regular blood removal (phlebotomy)","Medication to reduce blood cell production"],
prevention:["No known prevention"],
funFact:"Although rare, polycythemia vera can often be managed successfully for many years."},
{title:"Deep vein thrombosis",display:"Deep Vein Thrombosis (DVT)",tag:"blood",
overview:"Deep vein thrombosis is a blood clot that usually forms in a deep vein of the leg and can become dangerous if it travels to the lungs.",
symptoms:["Swollen leg","Pain or tenderness","Warm skin","Redness"],
causes:["Long periods of sitting","Recent surgery","Pregnancy","Blood clotting disorders"],
diagnosis:["Ultrasound","Blood test (D-dimer)"],
treatment:["Blood-thinning medication","Compression stockings"],
prevention:["Stay active","Move during long journeys","Stay hydrated"],
funFact:"Walking around during long flights helps lower your risk of developing DVT."},
{title:"Asthma",display:"Asthma",tag:"respiratory",
overview:"Asthma is a chronic condition that causes inflammation and narrowing of the airways, making breathing difficult.",
symptoms:["Wheezing","Shortness of breath","Chest tightness","Persistent cough"],
causes:["Allergies","Exercise","Cold air","Respiratory infections"],
diagnosis:["Spirometry","Peak flow test","Physical examination"],
treatment:["Reliever inhalers","Preventer inhalers","Avoiding triggers"],
prevention:["Avoid triggers","Take prescribed medication"],
funFact:"Around 262 million people worldwide live with asthma."},
{title:"Pneumonia",display:"Pneumonia",tag:"respiratory",
overview:"Pneumonia is an infection that causes the air sacs in the lungs to fill with fluid or pus.",
symptoms:["Fever","Cough","Chest pain","Shortness of breath"],
causes:["Bacteria","Viruses","Fungi"],
diagnosis:["Chest X-ray","Blood tests","Physical examination"],
treatment:["Antibiotics if bacterial","Rest","Fluids"],
prevention:["Vaccination","Hand washing","Don't smoke"],
funFact:"Pneumonia is one of the leading infectious causes of death worldwide."},
{title:"Chronic obstructive pulmonary disease",display:"COPD",tag:"respiratory",
overview:"COPD is a long-term lung disease that makes airflow difficult due to damage to the airways and lungs.",
symptoms:["Shortness of breath","Chronic cough","Mucus production","Wheezing"],
causes:["Smoking","Air pollution","Genetics"],
diagnosis:["Spirometry","Chest X-ray","CT scan"],
treatment:["Inhalers","Pulmonary rehabilitation","Oxygen therapy"],
prevention:["Avoid smoking","Reduce exposure to pollutants"],
funFact:"Most COPD cases are linked to smoking."},
{title:"Bronchitis",display:"Bronchitis",tag:"respiratory",
overview:"Bronchitis is inflammation of the bronchial tubes that carry air into the lungs.",
symptoms:["Persistent cough","Mucus","Chest discomfort","Fatigue"],
causes:["Viruses","Smoking","Air pollution"],
diagnosis:["Physical examination","Chest X-ray if needed"],
treatment:["Rest","Fluids","Pain relief"],
prevention:["Don't smoke","Wash hands regularly"],
funFact:"Acute bronchitis usually develops after a cold."},
{title:"Tuberculosis",display:"Tuberculosis (TB)",tag:"respiratory",
overview:"Tuberculosis is a bacterial infection that mainly affects the lungs but can spread to other parts of the body.",
symptoms:["Persistent cough","Weight loss","Night sweats","Fever"],
causes:["Mycobacterium tuberculosis bacteria"],
diagnosis:["Chest X-ray","Sputum test","Skin or blood test"],
treatment:["Several months of antibiotics"],
prevention:["Early treatment","TB vaccination in some countries"],
funFact:"TB has been affecting humans for thousands of years."},
{title:"Cystic fibrosis",display:"Cystic Fibrosis",tag:"respiratory",
overview:"Cystic fibrosis is an inherited disorder that causes thick mucus to build up in the lungs and digestive system.",
symptoms:["Persistent cough","Frequent lung infections","Poor growth","Salty skin"],
causes:["Inherited mutation in the CFTR gene"],
diagnosis:["Sweat test","Genetic testing"],
treatment:["Airway clearance therapy","Antibiotics","CFTR medications"],
prevention:["Genetic counselling"],
funFact:"Modern treatments have greatly increased life expectancy for people with cystic fibrosis."},
{title:"Lung cancer",display:"Lung Cancer",tag:"respiratory",
overview:"Lung cancer occurs when abnormal cells grow uncontrollably in the lungs.",
symptoms:["Persistent cough","Chest pain","Weight loss","Coughing up blood"],
causes:["Smoking","Second-hand smoke","Radon exposure"],
diagnosis:["CT scan","Bronchoscopy","Biopsy"],
treatment:["Surgery","Chemotherapy","Radiotherapy","Immunotherapy"],
prevention:["Don't smoke","Avoid second-hand smoke"],
funFact:"Stopping smoking greatly reduces the risk of developing lung cancer."},
{title:"Pulmonary embolism",display:"Pulmonary Embolism",tag:"respiratory",
overview:"A pulmonary embolism occurs when a blood clot blocks one of the arteries in the lungs.",
symptoms:["Sudden shortness of breath","Chest pain","Rapid heartbeat","Coughing up blood"],
causes:["Deep vein thrombosis","Long periods of immobility","Recent surgery"],
diagnosis:["CT pulmonary angiogram","Blood tests","Ultrasound of the legs"],
treatment:["Blood-thinning medication","Clot-dissolving medicine in severe cases"],
prevention:["Stay active","Move during long journeys","Compression stockings when recommended"],
funFact:"Many pulmonary embolisms begin as blood clots in the legs."},
{title:"Acne",display:"Acne",tag:"skin",
overview:"Acne is a common skin condition that occurs when hair follicles become blocked with oil and dead skin cells.",
symptoms:["Pimples","Blackheads","Whiteheads","Oily skin"],
causes:["Hormonal changes","Excess oil production","Blocked pores","Bacteria"],
diagnosis:["Physical examination"],
treatment:["Benzoyl peroxide","Retinoids","Antibiotics","Good skincare"],
prevention:["Wash skin gently","Avoid picking pimples"],
funFact:"Around 85% of teenagers experience acne."},
{title:"Eczema",display:"Eczema (Atopic Dermatitis)",tag:"skin",
overview:"Eczema is a long-term condition that causes dry, itchy, inflamed skin.",
symptoms:["Itchy skin","Dry skin","Red patches","Cracked skin"],
causes:["Genetics","Allergies","Immune system overreaction"],
diagnosis:["Physical examination"],
treatment:["Moisturizers","Steroid creams","Avoiding triggers"],
prevention:["Keep skin moisturized","Avoid irritants"],
funFact:"Eczema often begins during childhood."},
{title:"Psoriasis",display:"Psoriasis",tag:"skin",
overview:"Psoriasis is an autoimmune condition that causes skin cells to build up too quickly.",
symptoms:["Red patches","Silvery scales","Itchy skin","Dry cracked skin"],
causes:["Immune system disorder","Genetics"],
diagnosis:["Physical examination","Skin biopsy"],
treatment:["Steroid creams","Light therapy","Immune-suppressing medication"],
prevention:["Avoid known triggers","Keep skin moisturized"],
funFact:"Psoriasis is not contagious."},
{title:"Cellulitis",display:"Cellulitis",tag:"skin",
overview:"Cellulitis is a bacterial infection of the deeper layers of the skin.",
symptoms:["Redness","Swelling","Warm skin","Pain"],
causes:["Bacterial infection through broken skin"],
diagnosis:["Physical examination"],
treatment:["Antibiotics"],
prevention:["Clean cuts promptly","Protect broken skin"],
funFact:"Untreated cellulitis can spread rapidly."},
{title:"Impetigo",display:"Impetigo",tag:"skin",
overview:"Impetigo is a highly contagious bacterial skin infection commonly affecting children.",
symptoms:["Blisters","Honey-colored crusts","Itchy sores"],
causes:["Staphylococcus bacteria","Streptococcus bacteria"],
diagnosis:["Physical examination"],
treatment:["Antibiotic cream","Oral antibiotics"],
prevention:["Wash hands","Avoid sharing towels"],
funFact:"Impetigo spreads easily in schools."},
{title:"Ringworm",display:"Ringworm",tag:"skin",
overview:"Ringworm is a fungal infection that causes a ring-shaped rash.",
symptoms:["Circular rash","Itchy skin","Scaly patches"],
causes:["Fungal infection"],
diagnosis:["Skin examination","Skin scraping"],
treatment:["Antifungal creams","Antifungal tablets"],
prevention:["Keep skin dry","Don't share towels"],
funFact:"Ringworm is caused by a fungus, not a worm."},
{title:"Vitiligo",display:"Vitiligo",tag:"skin",
overview:"Vitiligo is a condition where patches of skin lose their pigment.",
symptoms:["White skin patches","Premature whitening of hair"],
causes:["Autoimmune condition"],
diagnosis:["Wood's lamp examination","Physical examination"],
treatment:["Steroid creams","Light therapy"],
prevention:["No known prevention"],
funFact:"Vitiligo affects about 1% of the world's population."},
{title:"Melanoma",display:"Melanoma",tag:"skin",
overview:"Melanoma is the most serious form of skin cancer.",
symptoms:["Changing mole","Irregular borders","Different colors","Bleeding mole"],
causes:["UV radiation","Genetics"],
diagnosis:["Skin examination","Biopsy"],
treatment:["Surgery","Immunotherapy","Targeted therapy"],
prevention:["Wear sunscreen","Avoid excessive sun exposure"],
funFact:"Early detection gives melanoma a very high survival rate."},
{title:"Hives",display:"Hives (Urticaria)",tag:"skin",
overview:"Hives are raised, itchy welts that appear due to an allergic reaction or other trigger.",
symptoms:["Raised itchy bumps","Red welts","Swelling"],
causes:["Allergies","Infections","Stress"],
diagnosis:["Physical examination"],
treatment:["Antihistamines","Avoid triggers"],
prevention:["Identify allergens"],
funFact:"Individual hives usually disappear within 24 hours."},
{title:"Sunburn",display:"Sunburn",tag:"skin",
overview:"Sunburn is skin damage caused by too much ultraviolet (UV) radiation from the sun.",
symptoms:["Red skin","Pain","Peeling","Blisters"],
causes:["Excessive UV exposure"],
diagnosis:["Physical examination"],
treatment:["Cool compresses","Moisturizer","Pain relief"],
prevention:["Wear sunscreen","Seek shade","Protective clothing"],
funFact:"Even one severe sunburn can increase the risk of skin cancer later in life."},
{title:"Gastroesophageal reflux disease",display:"GERD",tag:"digestive",
overview:"GERD is a long-term condition where stomach acid frequently flows back into the esophagus, causing irritation.",
symptoms:["Heartburn","Acid reflux","Chest pain","Difficulty swallowing"],
causes:["Weak lower esophageal sphincter","Obesity","Hiatal hernia"],
diagnosis:["Endoscopy","24-hour pH monitoring"],
treatment:["Antacids","Proton pump inhibitors","Lifestyle changes"],
prevention:["Maintain a healthy weight","Avoid large meals before bed"],
funFact:"Occasional acid reflux is common, but frequent reflux may be GERD."},
{title:"Irritable bowel syndrome",display:"IBS",tag:"digestive",
overview:"IBS is a common disorder affecting the large intestine, causing abdominal discomfort and changes in bowel habits.",
symptoms:["Abdominal pain","Bloating","Diarrhea","Constipation"],
causes:["Abnormal gut movement","Stress","Changes in gut bacteria"],
diagnosis:["Medical history","Physical examination"],
treatment:["Diet changes","Fiber supplements","Medication"],
prevention:["Manage stress","Identify food triggers"],
funFact:"IBS affects around 10 to 15 percent of adults worldwide."},
{title:"Crohn's disease",display:"Crohn's Disease",tag:"digestive",
overview:"Crohn's disease is an inflammatory bowel disease that can affect any part of the digestive tract.",
symptoms:["Abdominal pain","Diarrhea","Weight loss","Fatigue"],
causes:["Immune system dysfunction","Genetics"],
diagnosis:["Colonoscopy","Blood tests","CT scan"],
treatment:["Anti-inflammatory medication","Immunosuppressants","Surgery"],
prevention:["No known prevention"],
funFact:"Crohn's disease often develops between ages 15 and 35."},
{title:"Ulcerative colitis",display:"Ulcerative Colitis",tag:"digestive",
overview:"Ulcerative colitis is an inflammatory bowel disease affecting the lining of the large intestine.",
symptoms:["Bloody diarrhea","Abdominal pain","Urgent bowel movements","Fatigue"],
causes:["Immune system disorder","Genetics"],
diagnosis:["Colonoscopy","Biopsy"],
treatment:["Anti-inflammatory medication","Biologic therapy","Surgery"],
prevention:["No known prevention"],
funFact:"Ulcerative colitis only affects the colon and rectum."},
{title:"Appendicitis",display:"Appendicitis",tag:"digestive",
overview:"Appendicitis is inflammation of the appendix and is a medical emergency.",
symptoms:["Lower right abdominal pain","Fever","Nausea","Loss of appetite"],
causes:["Blockage of the appendix"],
diagnosis:["Physical examination","Ultrasound","CT scan"],
treatment:["Appendix removal surgery","Antibiotics"],
prevention:["No reliable prevention"],
funFact:"Appendicitis is one of the most common reasons for emergency abdominal surgery."},
{title:"Peptic ulcer disease",display:"Peptic Ulcer",tag:"digestive",
overview:"A peptic ulcer is an open sore that develops in the lining of the stomach or upper small intestine.",
symptoms:["Burning stomach pain","Bloating","Nausea","Heartburn"],
causes:["Helicobacter pylori infection","Long-term NSAID use"],
diagnosis:["Endoscopy","Breath test"],
treatment:["Antibiotics","Acid-reducing medication"],
prevention:["Avoid unnecessary NSAID use","Treat H. pylori infection"],
funFact:"Most stomach ulcers are caused by H. pylori bacteria."},
{title:"Gallstones",display:"Gallstones",tag:"digestive",
overview:"Gallstones are hardened deposits that form in the gallbladder.",
symptoms:["Upper abdominal pain","Nausea","Vomiting","Pain after fatty meals"],
causes:["High cholesterol in bile","Family history","Obesity"],
diagnosis:["Ultrasound","CT scan"],
treatment:["Pain relief","Gallbladder removal surgery"],
prevention:["Maintain a healthy weight","Eat a balanced diet"],
funFact:"Many people have gallstones without ever developing symptoms."},
{title:"Celiac disease",display:"Celiac Disease",tag:"digestive",
overview:"Celiac disease is an autoimmune disorder where eating gluten damages the small intestine.",
symptoms:["Diarrhea","Bloating","Weight loss","Fatigue"],
causes:["Autoimmune reaction to gluten"],
diagnosis:["Blood tests","Small intestine biopsy"],
treatment:["Strict gluten-free diet"],
prevention:["No known prevention"],
funFact:"Even tiny amounts of gluten can trigger symptoms in people with celiac disease."},
{title:"Food poisoning",display:"Food Poisoning",tag:"digestive",
overview:"Food poisoning is illness caused by eating contaminated food or drinks.",
symptoms:["Vomiting","Diarrhea","Stomach cramps","Fever"],
causes:["Bacteria","Viruses","Parasites"],
diagnosis:["Medical history","Stool tests"],
treatment:["Fluids","Rest","Sometimes antibiotics"],
prevention:["Cook food thoroughly","Wash hands","Store food safely"],
funFact:"Most cases of food poisoning improve within a few days."},
{title:"Lactose intolerance",display:"Lactose Intolerance",tag:"digestive",
overview:"Lactose intolerance occurs when the body cannot properly digest lactose, the sugar found in milk.",
symptoms:["Bloating","Gas","Diarrhea","Stomach cramps"],
causes:["Low levels of lactase enzyme"],
diagnosis:["Hydrogen breath test","Lactose tolerance test"],
treatment:["Avoid lactose","Lactase tablets"],
prevention:["No prevention, but symptoms can be managed"],
funFact:"Around 65% of the world's population has some degree of lactose intolerance."},
{title:"Influenza",display:"Influenza (Flu)",tag:"infectious",
overview:"Influenza is a contagious viral infection that affects the nose, throat, and lungs.",
symptoms:["Fever","Cough","Sore throat","Muscle aches","Fatigue"],
causes:["Influenza virus spread through droplets"],
diagnosis:["Physical examination","Rapid flu test","PCR test"],
treatment:["Rest","Fluids","Antiviral medication in some cases"],
prevention:["Annual flu vaccine","Hand washing","Avoid close contact with sick people"],
funFact:"The flu vaccine changes almost every year because influenza viruses evolve quickly."},
{title:"COVID-19",display:"COVID-19",tag:"infectious",
overview:"COVID-19 is a contagious disease caused by the SARS-CoV-2 virus that mainly affects the respiratory system.",
symptoms:["Fever","Cough","Loss of taste or smell","Fatigue","Shortness of breath"],
causes:["SARS-CoV-2 virus"],
diagnosis:["Rapid antigen test","PCR test"],
treatment:["Rest","Fluids","Antiviral medication for high-risk patients","Hospital care for severe illness"],
prevention:["Vaccination","Hand hygiene","Good ventilation"],
funFact:"COVID-19 was first identified in late 2019."},
{title:"Tuberculosis (infectious)",display:"Tuberculosis",tag:"infectious",
overview:"Tuberculosis is a bacterial infection that usually affects the lungs but can spread to other organs.",
symptoms:["Persistent cough","Weight loss","Night sweats","Fever","Coughing blood"],
causes:["Mycobacterium tuberculosis bacteria"],
diagnosis:["Chest X-ray","Sputum test","Skin test","Blood test"],
treatment:["Several months of antibiotics"],
prevention:["Early treatment","BCG vaccine in some countries"],
funFact:"Around one-quarter of the world's population carries latent TB."},
{title:"Malaria",display:"Malaria",tag:"infectious",
overview:"Malaria is a mosquito-borne disease caused by Plasmodium parasites.",
symptoms:["Fever","Chills","Sweating","Headache","Nausea"],
causes:["Plasmodium parasites transmitted by mosquitoes"],
diagnosis:["Blood smear","Rapid diagnostic test"],
treatment:["Antimalarial medicines"],
prevention:["Mosquito nets","Insect repellent","Preventive medication when travelling"],
funFact:"Only female Anopheles mosquitoes spread malaria."},
{title:"Dengue fever",display:"Dengue Fever",tag:"infectious",
overview:"Dengue fever is a viral illness spread by Aedes mosquitoes and is common in tropical countries.",
symptoms:["High fever","Severe headache","Muscle pain","Joint pain","Rash"],
causes:["Dengue virus"],
diagnosis:["Blood test"],
treatment:["Rest","Fluids","Pain relief"],
prevention:["Avoid mosquito bites","Remove standing water"],
funFact:"Dengue is sometimes called 'breakbone fever' because of the severe muscle and joint pain."},
{title:"Chickenpox",display:"Chickenpox",tag:"infectious",
overview:"Chickenpox is a highly contagious viral infection that causes an itchy blister-like rash.",
symptoms:["Itchy rash","Fever","Fatigue","Loss of appetite"],
causes:["Varicella-zoster virus"],
diagnosis:["Physical examination"],
treatment:["Rest","Calamine lotion","Antiviral medicine for high-risk patients"],
prevention:["Chickenpox vaccine"],
funFact:"The same virus that causes chickenpox can later cause shingles."},
{title:"Measles",display:"Measles",tag:"infectious",
overview:"Measles is a highly contagious viral illness that causes fever and a widespread rash.",
symptoms:["Fever","Cough","Runny nose","Red eyes","Rash"],
causes:["Measles virus"],
diagnosis:["Blood test","PCR test"],
treatment:["Supportive care","Vitamin A"],
prevention:["MMR vaccine"],
funFact:"Measles is one of the most contagious diseases known."},
{title:"Meningitis",display:"Meningitis",tag:"infectious",
overview:"Meningitis is inflammation of the protective membranes around the brain and spinal cord.",
symptoms:["Severe headache","Neck stiffness","Fever","Confusion","Sensitivity to light"],
causes:["Bacteria","Viruses","Fungi"],
diagnosis:["Lumbar puncture","Blood tests","CT scan"],
treatment:["Antibiotics for bacterial meningitis","Supportive care"],
prevention:["Vaccination","Good hygiene"],
funFact:"Bacterial meningitis is a medical emergency."},
{title:"Lyme disease",display:"Lyme Disease",tag:"infectious",
overview:"Lyme disease is a bacterial infection spread by infected ticks.",
symptoms:["Bull's-eye rash","Fever","Fatigue","Joint pain"],
causes:["Borrelia bacteria spread by tick bites"],
diagnosis:["Blood tests","Clinical examination"],
treatment:["Antibiotics"],
prevention:["Tick repellent","Protective clothing","Check for ticks after outdoor activities"],
funFact:"Early treatment usually leads to a full recovery."},
{title:"HIV infection",display:"HIV Infection",tag:"infectious",
overview:"Human Immunodeficiency Virus (HIV) attacks the immune system and can lead to AIDS if untreated.",
symptoms:["Fever","Swollen lymph nodes","Weight loss","Frequent infections","Fatigue"],
causes:["Human Immunodeficiency Virus"],
diagnosis:["Blood test","Rapid HIV test"],
treatment:["Antiretroviral therapy (ART)"],
prevention:["Safe sex","Do not share needles","PrEP for high-risk individuals"],
funFact:"With modern treatment, many people with HIV live long, healthy lives."},
{title:"Diabetes mellitus",display:"Diabetes Mellitus",tag:"endocrine",
overview:"Diabetes mellitus is a condition where the body cannot properly regulate blood sugar because of problems with insulin.",
symptoms:["Increased thirst","Frequent urination","Fatigue","Blurred vision","Weight loss"],
causes:["Autoimmune destruction of insulin-producing cells","Insulin resistance","Genetics"],
diagnosis:["Blood glucose test","HbA1c test","Urine tests"],
treatment:["Insulin","Blood sugar monitoring","Healthy diet","Exercise"],
prevention:["Maintain a healthy weight","Exercise regularly"],
funFact:"Over 500 million people worldwide live with diabetes."},
{title:"Hypothyroidism",display:"Hypothyroidism",tag:"endocrine",
overview:"Hypothyroidism occurs when the thyroid gland does not produce enough thyroid hormones.",
symptoms:["Fatigue","Weight gain","Cold intolerance","Dry skin","Constipation"],
causes:["Hashimoto disease","Thyroid surgery","Iodine deficiency"],
diagnosis:["TSH blood test","Thyroid hormone tests"],
treatment:["Levothyroxine medication"],
prevention:["Adequate iodine intake"],
funFact:"Hypothyroidism is far more common in women than men."},
{title:"Hyperthyroidism",display:"Hyperthyroidism",tag:"endocrine",
overview:"Hyperthyroidism is a condition where the thyroid gland produces too much thyroid hormone.",
symptoms:["Weight loss","Rapid heartbeat","Sweating","Anxiety","Shaking hands"],
causes:["Graves disease","Thyroid nodules"],
diagnosis:["Blood tests","Thyroid scan"],
treatment:["Antithyroid medication","Radioactive iodine","Surgery"],
prevention:["No specific prevention"],
funFact:"Graves disease is the most common cause of hyperthyroidism."},
{title:"Hashimoto thyroiditis",display:"Hashimoto Thyroiditis",tag:"endocrine",
overview:"Hashimoto thyroiditis is an autoimmune disease that gradually damages the thyroid gland.",
symptoms:["Fatigue","Weight gain","Cold intolerance","Depression"],
causes:["Autoimmune disease","Genetics"],
diagnosis:["Blood tests","Thyroid antibody tests"],
treatment:["Thyroid hormone replacement"],
prevention:["No proven prevention"],
funFact:"Hashimoto disease is the leading cause of hypothyroidism."},
{title:"Graves disease",display:"Graves Disease",tag:"endocrine",
overview:"Graves disease is an autoimmune disorder that causes the thyroid gland to become overactive.",
symptoms:["Weight loss","Fast heartbeat","Bulging eyes","Heat intolerance"],
causes:["Autoimmune disease"],
diagnosis:["Blood tests","Thyroid scan"],
treatment:["Medication","Radioactive iodine","Surgery"],
prevention:["No known prevention"],
funFact:"Graves disease can affect the eyes, causing them to bulge outward."},
{title:"Cushing syndrome",display:"Cushing Syndrome",tag:"endocrine",
overview:"Cushing syndrome occurs when the body is exposed to high levels of cortisol for a long time.",
symptoms:["Weight gain","Round face","Purple stretch marks","Muscle weakness"],
causes:["Long-term steroid medication","Adrenal tumors"],
diagnosis:["Urine cortisol test","Blood tests","MRI"],
treatment:["Reduce steroid use","Surgery","Medication"],
prevention:["Use steroids only as prescribed"],
funFact:"Cortisol is often called the body's 'stress hormone.'"},
{title:"Addison disease",display:"Addison Disease",tag:"endocrine",
overview:"Addison disease happens when the adrenal glands do not produce enough cortisol and aldosterone.",
symptoms:["Fatigue","Weight loss","Low blood pressure","Darkened skin"],
causes:["Autoimmune disease","Tuberculosis","Adrenal damage"],
diagnosis:["Blood tests","ACTH stimulation test"],
treatment:["Hormone replacement therapy"],
prevention:["Cannot usually be prevented"],
funFact:"John F. Kennedy lived with Addison disease."},
{title:"Polycystic ovary syndrome",display:"PCOS",tag:"endocrine",
overview:"PCOS is a hormonal disorder that affects the ovaries and can interfere with ovulation.",
symptoms:["Irregular periods","Acne","Weight gain","Excess facial hair"],
causes:["Hormonal imbalance","Insulin resistance","Genetics"],
diagnosis:["Blood tests","Ultrasound"],
treatment:["Lifestyle changes","Birth control pills","Metformin"],
prevention:["Healthy lifestyle may reduce symptoms"],
funFact:"PCOS affects around 1 in 10 women of reproductive age."},
{title:"Acromegaly",display:"Acromegaly",tag:"endocrine",
overview:"Acromegaly is caused by excess growth hormone in adults, leading to enlargement of bones and tissues.",
symptoms:["Large hands","Large feet","Headaches","Joint pain"],
causes:["Pituitary gland tumor"],
diagnosis:["Growth hormone blood tests","MRI scan"],
treatment:["Surgery","Medication","Radiotherapy"],
prevention:["No known prevention"],
funFact:"Acromegaly develops slowly and may take years to diagnose."},
{title:"Diabetes insipidus",display:"Diabetes Insipidus",tag:"endocrine",
overview:"Diabetes insipidus is a rare condition that causes excessive thirst and production of large amounts of urine.",
symptoms:["Extreme thirst","Frequent urination","Dehydration"],
causes:["Lack of antidiuretic hormone","Kidney resistance to the hormone"],
diagnosis:["Water deprivation test","Blood tests","Urine tests"],
treatment:["Desmopressin","Treat underlying cause"],
prevention:["Usually cannot be prevented"],
funFact:"Despite the name, diabetes insipidus is completely different from diabetes mellitus."},
{title:"Osteoporosis",display:"Osteoporosis",tag:"muscoskel",
overview:"Osteoporosis is a condition where bones become weak and brittle, making them more likely to break.",
symptoms:["Back pain","Loss of height","Stooped posture","Bone fractures"],
causes:["Aging","Low calcium","Hormonal changes","Lack of exercise"],
diagnosis:["Bone density scan (DEXA)","X-rays"],
treatment:["Calcium","Vitamin D","Exercise","Bone-strengthening medication"],
prevention:["Weight-bearing exercise","Adequate calcium","Vitamin D"],
funFact:"Around one in three women over age 50 will experience an osteoporosis-related fracture."},
{title:"Osteoarthritis",display:"Osteoarthritis",tag:"muscoskel",
overview:"Osteoarthritis is the most common type of arthritis and occurs when the cartilage protecting joints wears down.",
symptoms:["Joint pain","Joint stiffness","Reduced movement","Swelling"],
causes:["Aging","Joint injury","Obesity"],
diagnosis:["Physical examination","X-rays","MRI"],
treatment:["Exercise","Pain relievers","Physical therapy","Joint replacement surgery"],
prevention:["Maintain healthy weight","Stay active"],
funFact:"The knees are among the most commonly affected joints."},
{title:"Rheumatoid arthritis",display:"Rheumatoid Arthritis",tag:"muscoskel",
overview:"Rheumatoid arthritis is an autoimmune disease that causes the body's immune system to attack the joints.",
symptoms:["Painful joints","Morning stiffness","Swollen joints","Fatigue"],
causes:["Autoimmune disease","Genetics"],
diagnosis:["Blood tests","X-rays","MRI"],
treatment:["Disease-modifying medications","Physical therapy","Pain relief"],
prevention:["No proven prevention"],
funFact:"Rheumatoid arthritis can affect organs as well as joints."},
{title:"Scoliosis",display:"Scoliosis",tag:"muscoskel",
overview:"Scoliosis is an abnormal sideways curvature of the spine that often develops during adolescence.",
symptoms:["Uneven shoulders","Uneven hips","Back pain","Curved spine"],
causes:["Unknown (idiopathic)","Birth defects","Neuromuscular disorders"],
diagnosis:["Physical examination","X-rays"],
treatment:["Observation","Brace","Surgery"],
prevention:["Cannot usually be prevented"],
funFact:"Most scoliosis cases are classified as idiopathic, meaning the cause is unknown."},
{title:"Tendinitis",display:"Tendinitis",tag:"muscoskel",
overview:"Tendinitis is inflammation or irritation of a tendon, usually caused by overuse.",
symptoms:["Pain","Tenderness","Swelling","Difficulty moving the joint"],
causes:["Repetitive movement","Sports injuries","Overuse"],
diagnosis:["Physical examination","Ultrasound","MRI"],
treatment:["Rest","Ice","Physical therapy","Anti-inflammatory medication"],
prevention:["Warm up before exercise","Avoid repetitive strain"],
funFact:"Tennis elbow is a common form of tendinitis."},
{title:"Carpal tunnel syndrome",display:"Carpal Tunnel Syndrome",tag:"muscoskel",
overview:"Carpal tunnel syndrome occurs when the median nerve in the wrist becomes compressed.",
symptoms:["Hand numbness","Tingling","Weak grip","Hand pain"],
causes:["Repetitive hand movements","Pregnancy","Diabetes"],
diagnosis:["Physical examination","Nerve conduction study"],
treatment:["Wrist splint","Steroid injections","Surgery"],
prevention:["Take breaks during repetitive tasks","Maintain good wrist posture"],
funFact:"Carpal tunnel syndrome is one of the most common nerve compression disorders."},
{title:"Gout",display:"Gout",tag:"muscoskel",
overview:"Gout is a type of arthritis caused by the buildup of uric acid crystals in joints.",
symptoms:["Sudden joint pain","Swelling","Redness","Warm joints"],
causes:["High uric acid levels","Diet","Kidney disease"],
diagnosis:["Joint fluid test","Blood test"],
treatment:["Anti-inflammatory medication","Medicines to lower uric acid"],
prevention:["Stay hydrated","Limit alcohol","Reduce high-purine foods"],
funFact:"The big toe is the joint most commonly affected by gout."},
{title:"Fibromyalgia",display:"Fibromyalgia",tag:"muscoskel",
overview:"Fibromyalgia is a chronic condition that causes widespread pain, fatigue, and sleep problems.",
symptoms:["Widespread pain","Fatigue","Poor sleep","Memory difficulties"],
causes:["Unknown","Genetics","Stress"],
diagnosis:["Clinical assessment"],
treatment:["Exercise","Medication","Stress management","Sleep improvement"],
prevention:["No known prevention"],
funFact:"Fibromyalgia affects women more often than men."},
{title:"Muscular dystrophy",display:"Muscular Dystrophy",tag:"muscoskel",
overview:"Muscular dystrophy is a group of inherited diseases that cause muscles to become progressively weaker.",
symptoms:["Muscle weakness","Difficulty walking","Frequent falls"],
causes:["Inherited genetic mutations"],
diagnosis:["Genetic testing","Muscle biopsy","Blood tests"],
treatment:["Physical therapy","Medication","Assistive devices"],
prevention:["Genetic counselling"],
funFact:"There are more than 30 different types of muscular dystrophy."},
{title:"Ankylosing spondylitis",display:"Ankylosing Spondylitis",tag:"muscoskel",
overview:"Ankylosing spondylitis is an inflammatory disease that mainly affects the spine and can cause the vertebrae to fuse together.",
symptoms:["Lower back pain","Morning stiffness","Reduced flexibility"],
causes:["Autoimmune factors","Genetics"],
diagnosis:["X-rays","MRI","Blood tests"],
treatment:["Exercise","Anti-inflammatory medication","Biologic therapy"],
prevention:["No known prevention"],
funFact:"Regular stretching and exercise are important parts of managing ankylosing spondylitis."},
{title:"Migraine",display:"Migraine",tag:"mind",
overview:"Migraine is a neurological condition that causes recurring headaches, often accompanied by nausea and sensitivity to light or sound.",
symptoms:["Severe headache","Nausea","Sensitivity to light","Sensitivity to sound","Visual disturbances"],
causes:["Genetics","Hormonal changes","Stress","Certain foods"],
diagnosis:["Medical history","Neurological examination","MRI if needed"],
treatment:["Pain relievers","Triptans","Preventive medication"],
prevention:["Avoid triggers","Regular sleep","Stress management"],
funFact:"About 1 billion people worldwide experience migraines."},
{title:"Epilepsy",display:"Epilepsy",tag:"mind",
overview:"Epilepsy is a neurological disorder that causes repeated seizures due to abnormal electrical activity in the brain.",
symptoms:["Seizures","Confusion","Loss of consciousness","Muscle stiffness"],
causes:["Genetics","Head injury","Stroke","Brain infection"],
diagnosis:["EEG","MRI","Blood tests"],
treatment:["Anti-seizure medication","Surgery in some cases","Special diets"],
prevention:["Prevent head injuries where possible"],
funFact:"Most people with epilepsy can control seizures with medication."},
{title:"Parkinson disease",display:"Parkinson Disease",tag:"mind",
overview:"Parkinson disease is a progressive neurological disorder that mainly affects movement.",
symptoms:["Hand tremor","Slow movement","Muscle stiffness","Balance problems"],
causes:["Loss of dopamine-producing brain cells"],
diagnosis:["Neurological examination"],
treatment:["Levodopa","Physical therapy","Deep brain stimulation"],
prevention:["No known prevention"],
funFact:"Symptoms usually develop gradually over many years."},
{title:"Alzheimer disease",display:"Alzheimer Disease",tag:"mind",
overview:"Alzheimer disease is the most common cause of dementia and gradually affects memory and thinking.",
symptoms:["Memory loss","Confusion","Difficulty speaking","Personality changes"],
causes:["Age","Genetics","Brain protein buildup"],
diagnosis:["Memory tests","Brain imaging"],
treatment:["Medications","Supportive care"],
prevention:["Regular exercise","Healthy diet","Mental activity"],
funFact:"Alzheimer disease accounts for around 60 to 70 percent of dementia cases."},
{title:"Multiple sclerosis",display:"Multiple Sclerosis",tag:"mind",
overview:"Multiple sclerosis is an autoimmune disease where the immune system attacks the protective covering of nerves.",
symptoms:["Vision problems","Muscle weakness","Numbness","Balance difficulties"],
causes:["Autoimmune disease","Genetics"],
diagnosis:["MRI","Lumbar puncture","Neurological examination"],
treatment:["Disease-modifying medication","Steroids","Physical therapy"],
prevention:["No known prevention"],
funFact:"Symptoms often come and go in the early stages."},
{title:"Attention deficit hyperactivity disorder",display:"ADHD",tag:"mind",
overview:"Attention deficit hyperactivity disorder (ADHD) is a neurodevelopmental condition that affects attention, impulsivity, and activity levels.",
symptoms:["Difficulty concentrating","Hyperactivity","Impulsiveness","Forgetfulness"],
causes:["Genetics","Brain development differences"],
diagnosis:["Clinical assessment","Behaviour questionnaires"],
treatment:["Behavioural therapy","Medication","Educational support"],
prevention:["No known prevention"],
funFact:"ADHD can continue into adulthood."},
{title:"Autism spectrum disorder",display:"Autism Spectrum Disorder",tag:"mind",
overview:"Autism spectrum disorder is a neurodevelopmental condition that affects communication, social interaction, and behaviour.",
symptoms:["Difficulty with social interaction","Repetitive behaviours","Sensory sensitivities","Communication differences"],
causes:["Genetics","Brain development differences"],
diagnosis:["Developmental assessment","Behavioural evaluation"],
treatment:["Speech therapy","Occupational therapy","Educational support"],
prevention:["No known prevention"],
funFact:"Autism is called a spectrum because it affects each person differently."},
{title:"Generalized anxiety disorder",display:"Generalized Anxiety Disorder",tag:"mind",
overview:"Generalized anxiety disorder causes excessive and persistent worry about everyday situations.",
symptoms:["Constant worry","Restlessness","Trouble sleeping","Difficulty concentrating"],
causes:["Genetics","Stress","Brain chemistry"],
diagnosis:["Psychological assessment"],
treatment:["Cognitive behavioural therapy","Medication","Stress management"],
prevention:["Manage stress","Regular exercise"],
funFact:"Anxiety disorders are among the most common mental health conditions worldwide."},
{title:"Major depressive disorder",display:"Major Depressive Disorder",tag:"mind",
overview:"Major depressive disorder is a mental health condition that causes persistent sadness and loss of interest in daily activities.",
symptoms:["Persistent sadness","Fatigue","Loss of interest","Sleep changes","Difficulty concentrating"],
causes:["Brain chemistry","Genetics","Stressful life events"],
diagnosis:["Clinical assessment"],
treatment:["Psychotherapy","Medication","Lifestyle changes"],
prevention:["Maintain social connections","Manage stress"],
funFact:"Depression is one of the leading causes of disability worldwide."},
{title:"Obsessive-compulsive disorder",display:"OCD",tag:"mind",
overview:"Obsessive-compulsive disorder is a mental health condition involving unwanted repetitive thoughts and behaviours.",
symptoms:["Obsessive thoughts","Compulsive behaviours","Anxiety","Time-consuming rituals"],
causes:["Genetics","Brain chemistry"],
diagnosis:["Psychological assessment"],
treatment:["Cognitive behavioural therapy","Medication"],
prevention:["No proven prevention"],
funFact:"Effective treatment helps many people greatly reduce OCD symptoms."}
  ];

  const ENTRIES = DISEASES;
  const diseaseLookup = Object.fromEntries(DISEASES.map(d => [d.title, d]));
  const tagMap = Object.fromEntries(TAGS.map(t => [t.id, t]));
  const ALL_SYMPTOMS = Array.from(new Set(DISEASES.flatMap(d => d.symptoms))).sort();
  const summaryCache = {};
  let activeTag = 'all';
  let history = [];
  let quizScores = [];
  let quizState = null;
  let checkerSelected = [];
  let checkerChecks = [];

  const el = id => document.getElementById(id);
  const cardGrid = el('cardGrid');
  const railList = el('railList');
  const gridTitle = el('gridTitle');
  const gridSub = el('gridSub');

  function countFor(tagId){
    return tagId === 'all' ? ENTRIES.length : ENTRIES.filter(e => e.tag === tagId).length;
  }

  function renderRail(){
    const items = [{id:'all', label:'All entries', color:'var(--accent)'}, ...TAGS];
    railList.innerHTML = items.map(t => `
      <li class="rail-item ${activeTag===t.id?'active':''}" style="--dot:${t.color}">
        <button data-tag="${t.id}">
          <span class="dot"></span>
          <span>${t.label}</span>
          <span class="n">${countFor(t.id)}</span>
        </button>
      </li>
    `).join('');
    railList.querySelectorAll('button').forEach(btn => {
      btn.addEventListener('click', () => {
        activeTag = btn.dataset.tag;
        renderRail();
        renderGrid();
      });
    });
  }

  function renderGrid(){
    const list = activeTag === 'all' ? ENTRIES : ENTRIES.filter(e => e.tag === activeTag);
    gridTitle.textContent = activeTag === 'all' ? 'All entries' : tagMap[activeTag].label;
    gridSub.textContent = `${list.length} condition${list.length===1?'':'s'}`;

    if(!list.length){
      cardGrid.innerHTML = `<div class="empty-state"><span class="mono">— nothing here —</span>Try another category.</div>`;
      return;
    }

    cardGrid.innerHTML = list.map(e => {
      const t = tagMap[e.tag];
      return `
        <div class="card" tabindex="0" style="--dot:${t.color}" data-title="${e.title}" data-display="${e.display}" data-tag="${e.tag}">
          <span class="tag-chip">${t.label}</span>
          <h3>${e.display}</h3>
          <p>${e.overview}</p>
        </div>
      `;
    }).join('');

    cardGrid.querySelectorAll('.card').forEach(card => {
      card.addEventListener('click', () => openDetail(card.dataset.title, card.dataset.display, card.dataset.tag));
      card.addEventListener('keydown', (ev) => { if(ev.key === 'Enter') openDetail(card.dataset.title, card.dataset.display, card.dataset.tag); });
    });
  }

  async function loadSummary(title){
    if(summaryCache[title]) return summaryCache[title];
    try{
      const res = await fetch(`https://en.wikipedia.org/api/rest_v1/page/summary/${encodeURIComponent(title)}`);
      if(!res.ok) throw new Error('not found');
      const data = await res.json();
      summaryCache[title] = data;
      return data;
    }catch(err){
      summaryCache[title] = {extract:null, thumbnail:null, content_urls:{desktop:{page:`https://en.wikipedia.org/wiki/${encodeURIComponent(title)}`}}};
      return summaryCache[title];
    }
  }

  // ---------- Detail modal ----------
  const detailOverlay = el('detailOverlay');
  const detailCard = el('detailCard');

  async function openDetail(title, display, tagId){
    const t = tagMap[tagId] || {label:'General', color:'var(--accent)'};
    const disease = diseaseLookup[title];
    detailCard.innerHTML = `
      <button class="icon-btn close-btn" id="closeDetail" aria-label="Close">
        <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M18 6 6 18M6 6l12 12"/></svg>
      </button>
      <span class="detail-tag" style="--dot:${t.color}">${t.label}</span>
      <h2>${display}</h2>
      <p class="extract">Loading…</p>
    `;
    detailOverlay.classList.add('open');
    el('closeDetail').addEventListener('click', closeDetail);

    logHistory(title, display, tagId);

    const data = await loadSummary(title);
    const pageUrl = (data.content_urls && data.content_urls.desktop && data.content_urls.desktop.page) || `https://en.wikipedia.org/wiki/${encodeURIComponent(title)}`;

    detailCard.innerHTML = `
      <button class="icon-btn close-btn" id="closeDetail" aria-label="Close">
        <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M18 6 6 18M6 6l12 12"/></svg>
      </button>
      <span class="detail-tag" style="--dot:${t.color}">${t.label}</span>
      <h2>${display}</h2>
      ${data.thumbnail ? `<img class="thumb" src="${data.thumbnail.source}" alt="${display}">` : ''}
      ${disease ? `
        <p class="extract">${disease.overview}</p>
        <h3>Symptoms</h3>
        <ul>${disease.symptoms.map(s => `<li>${s}</li>`).join('')}</ul>
        <h3>Causes</h3>
        <ul>${disease.causes.map(c => `<li>${c}</li>`).join('')}</ul>
        <h3>Diagnosis</h3>
        <ul>${disease.diagnosis.map(d => `<li>${d}</li>`).join('')}</ul>
        <h3>Treatment</h3>
        <ul>${disease.treatment.map(x => `<li>${x}</li>`).join('')}</ul>
        <h3>Prevention</h3>
        <ul>${disease.prevention.map(p => `<li>${p}</li>`).join('')}</ul>
        <p class="extract"><strong>Interesting fact:</strong> ${disease.funFact}</p>
      ` : `<p class="extract">${data.extract || 'No summary available.'}</p>`}
      <a class="src-link" href="${pageUrl}" target="_blank" rel="noopener">Read more on Wikipedia →</a>
      <div class="detail-note">Saved to your history automatically. Noticing a pattern in your symptoms over time? That's worth bringing up with a doctor — this page is just a starting point.</div>
    `;
    el('closeDetail').addEventListener('click', closeDetail);
  }

  function closeDetail(){ detailOverlay.classList.remove('open'); }
  detailOverlay.addEventListener('click', (e) => { if(e.target === detailOverlay) closeDetail(); });

  // ---------- Search (local, across curated data) ----------
  const searchInput = el('searchInput');
  const searchResultsEl = el('searchResults');
  const searchStatus = el('searchStatus');
  let searchTimer = null;

  searchInput.addEventListener('input', () => {
    clearTimeout(searchTimer);
    const q = searchInput.value.trim();
    if(!q){ searchResultsEl.classList.remove('open'); searchStatus.textContent=''; return; }
    searchStatus.textContent = 'Searching…';
    searchTimer = setTimeout(() => runSearch(q), 250);
  });

  document.addEventListener('click', (e) => {
    if(!e.target.closest('.search-wrap')) searchResultsEl.classList.remove('open');
  });

  function runSearch(query){
    const q = query.toLowerCase().trim();
    const results = DISEASES.filter(entry => {
      const nameMatch = entry.display.toLowerCase().includes(q) || entry.title.toLowerCase().includes(q);
      const symptomMatch = entry.symptoms && entry.symptoms.some(s => s.toLowerCase().includes(q));
      return nameMatch || symptomMatch;
    }).slice(0, 12);

    if(results.length === 0){
      searchResultsEl.innerHTML = `<div class="search-result-item">No matching condition found.</div>`;
    }else{
      searchResultsEl.innerHTML = results.map(r => `
        <div class="search-result-item" data-title="${r.title.replace(/"/g,'&quot;')}" data-display="${r.display.replace(/"/g,'&quot;')}" data-tag="${r.tag}">
          <span class="r-title">${r.display}</span>
          <span class="r-snippet">${r.symptoms.slice(0,3).join(' • ')}</span>
        </div>
      `).join('');
      searchResultsEl.querySelectorAll('.search-result-item[data-title]').forEach(item => {
        item.addEventListener('click', () => {
          openDetail(item.dataset.title, item.dataset.display, item.dataset.tag);
          searchResultsEl.classList.remove('open');
          searchInput.value = '';
          searchStatus.textContent = '';
        });
      });
    }
    searchResultsEl.classList.add('open');
    searchStatus.textContent = `${results.length} result${results.length===1?'':'s'}`;
  }

  // ---------- History (persistent storage) ----------
  const historyOverlay = el('historyOverlay');
  const historyList = el('historyList');
  const historyCount = el('historyCount');

  async function loadHistory(){
    try{
      const res = await window.storage.get('history', false);
      history = res && res.value ? JSON.parse(res.value) : [];
    }catch(err){
      history = [];
    }
    renderHistory();
  }

  async function saveHistory(){
    try{
      await window.storage.set('history', JSON.stringify(history), false);
    }catch(err){ /* best-effort */ }
  }

  function logHistory(title, display, tagId){
    history = history.filter(h => h.title !== title);
    history.unshift({title, display, tagId, viewedAt: Date.now()});
    history = history.slice(0, 30);
    renderHistory();
    saveHistory();
  }

  function timeAgo(ts){
    const s = Math.floor((Date.now()-ts)/1000);
    if(s < 60) return 'just now';
    if(s < 3600) return Math.floor(s/60)+'m ago';
    if(s < 86400) return Math.floor(s/3600)+'h ago';
    return Math.floor(s/86400)+'d ago';
  }

  function renderHistory(){
    historyCount.textContent = history.length;
    if(!history.length){
      historyList.innerHTML = `<div class="history-empty">Nothing viewed yet. Conditions you open will show up here so you can track what you've looked into.</div>`;
      return;
    }
    historyList.innerHTML = history.map(h => {
      const t = h.tagId && tagMap[h.tagId] ? tagMap[h.tagId] : {color:'var(--accent)'};
      return `
        <div class="history-item" data-title="${h.title.replace(/"/g,'&quot;')}" data-display="${(h.display||h.title).replace(/"/g,'&quot;')}" data-tag="${h.tagId||''}">
          <span class="dot" style="--dot:${t.color}"></span>
          <div class="h-body">
            <div class="h-title">${h.display || h.title}</div>
            <div class="h-time">${timeAgo(h.viewedAt)}</div>
          </div>
        </div>
      `;
    }).join('') + `<button class="clear-link" id="clearHistory">Clear history</button>`;

    historyList.querySelectorAll('.history-item').forEach(item => {
      item.addEventListener('click', () => {
        historyOverlay.classList.remove('open');
        openDetail(item.dataset.title, item.dataset.display, item.dataset.tag || null);
      });
    });
    const clearBtn = el('clearHistory');
    if(clearBtn) clearBtn.addEventListener('click', (e) => {
      e.stopPropagation();
      history = [];
      renderHistory();
      saveHistory();
    });
  }

  el('historyBtn').addEventListener('click', () => historyOverlay.classList.add('open'));
  el('closeHistory').addEventListener('click', () => historyOverlay.classList.remove('open'));
  historyOverlay.addEventListener('click', (e) => { if(e.target === historyOverlay) historyOverlay.classList.remove('open'); });

  // ---------- Quiz ----------
  const quizOverlay = el('quizOverlay');
  const quizCard = el('quizCard');

  const QUESTION_FIELDS = [
    {field:'symptoms', promptTpl: c => `Which condition is commonly associated with the symptom "${c}"?`},
    {field:'treatment', promptTpl: c => `Which condition is commonly treated with "${c}"?`},
    {field:'causes', promptTpl: c => `Which condition can be caused by "${c}"?`}
  ];

  function shuffle(arr){
    const a = arr.slice();
    for(let i=a.length-1;i>0;i--){
      const j = Math.floor(Math.random()*(i+1));
      [a[i],a[j]] = [a[j],a[i]];
    }
    return a;
  }
  function pick(arr){ return arr[Math.floor(Math.random()*arr.length)]; }

  async function loadQuizScores(){
    try{
      const res = await window.storage.get('quizScores', false);
      quizScores = res && res.value ? JSON.parse(res.value) : [];
    }catch(err){ quizScores = []; }
  }
  async function saveQuizScores(){
    try{ await window.storage.set('quizScores', JSON.stringify(quizScores), false); }catch(err){ /* best-effort */ }
  }

  function openQuizHome(){
    const cats = [{id:'all', label:'All conditions', color:'var(--accent)'}, ...TAGS];
    quizCard.innerHTML = `
      <button class="icon-btn close-btn" id="closeQuiz" aria-label="Close">
        <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M18 6 6 18M6 6l12 12"/></svg>
      </button>
      <span class="detail-tag">Quiz</span>
      <h2 style="font-size:26px;">Test what you know</h2>
      <p class="extract" style="margin-bottom:4px;">Pick a category. Every question is pulled straight from the symptoms, causes, and treatments in the index.</p>
      <div class="quiz-category-grid">
        ${cats.map(c => {
          const poolSize = c.id==='all' ? DISEASES.length : DISEASES.filter(d=>d.tag===c.id).length;
          const disabled = poolSize < 3;
          return `<button class="quiz-category-btn" data-tag="${c.id}" style="--dot:${c.color}" ${disabled?'disabled':''}>
            <span class="dot"></span>
            <span class="qc-label">${c.label}</span>
            <span class="qc-count">${poolSize} entries</span>
          </button>`;
        }).join('')}
      </div>
      <div class="quiz-past" id="quizPast"></div>
    `;
    el('closeQuiz').addEventListener('click', () => quizOverlay.classList.remove('open'));
    quizCard.querySelectorAll('.quiz-category-btn:not([disabled])').forEach(btn => {
      btn.addEventListener('click', () => startQuiz(btn.dataset.tag));
    });
    renderQuizPast();
  }

  function renderQuizPast(){
    const box = el('quizPast');
    if(!box) return;
    if(!quizScores.length){
      box.innerHTML = `<div class="history-empty">No quiz attempts yet.</div>`;
      return;
    }
    box.innerHTML = `<div class="rail-title">Past attempts</div>` + quizScores.slice(0,6).map(s => `
      <div class="quiz-past-item"><span>${s.tagLabel}</span><span>${s.score}/${s.total} — ${new Date(s.date).toLocaleDateString()}</span></div>
    `).join('');
  }

  function buildQuestion(disease, pool){
    const available = QUESTION_FIELDS.filter(qf => disease[qf.field] && disease[qf.field].length);
    const qf = pick(available.length ? available : QUESTION_FIELDS);
    const sourceArr = (disease[qf.field] && disease[qf.field].length) ? disease[qf.field] : disease.symptoms;
    const correct = pick(sourceArr);
    const prompt = qf.promptTpl(correct);
    const answer = disease.display;

    const distractorPool = pool.filter(d => d.title !== disease.title);
    let wrongNames = shuffle(distractorPool.map(d => d.display)).filter((v,i,arr) => arr.indexOf(v)===i && v !== answer).slice(0,3);
    if(wrongNames.length < 3){
      const fallback = shuffle(DISEASES.map(d => d.display)).filter(v => v !== answer && !wrongNames.includes(v));
      wrongNames = wrongNames.concat(fallback).slice(0,3);
    }
    const options = shuffle([answer, ...wrongNames]);
    return {prompt, options, answer};
  }

  function startQuiz(tagId){
    const pool = tagId === 'all' ? DISEASES : DISEASES.filter(d => d.tag === tagId);
    const tagLabel = tagId === 'all' ? 'All conditions' : tagMap[tagId].label;
    const chosen = shuffle(pool).slice(0, Math.min(8, pool.length));
    const questions = chosen.map(d => buildQuestion(d, pool));
    quizState = {tagId, tagLabel, questions, index:0, score:0};
    renderQuizQuestion();
  }

  function renderQuizQuestion(){
    const q = quizState.questions[quizState.index];
    quizCard.innerHTML = `
      <button class="icon-btn close-btn" id="closeQuiz" aria-label="Close">
        <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M18 6 6 18M6 6l12 12"/></svg>
      </button>
      <span class="detail-tag">${quizState.tagLabel}</span>
      <div class="quiz-progress">Question ${quizState.index+1} of ${quizState.questions.length} — Score: ${quizState.score}</div>
      <h2 style="font-size:22px;">${q.prompt}</h2>
      <div id="quizOptions">
        ${q.options.map(opt => `<button class="quiz-option" data-opt="${opt.replace(/"/g,'&quot;')}">${opt}</button>`).join('')}
      </div>
    `;
    el('closeQuiz').addEventListener('click', () => quizOverlay.classList.remove('open'));
    quizCard.querySelectorAll('.quiz-option').forEach(btn => {
      btn.addEventListener('click', () => answerQuiz(btn.dataset.opt));
    });
  }

  function answerQuiz(chosen){
    const q = quizState.questions[quizState.index];
    if(chosen === q.answer) quizState.score++;
    quizCard.querySelectorAll('.quiz-option').forEach(btn => {
      btn.disabled = true;
      if(btn.dataset.opt === q.answer) btn.classList.add('correct');
      else if(btn.dataset.opt === chosen) btn.classList.add('incorrect');
    });
    setTimeout(() => {
      quizState.index++;
      if(quizState.index >= quizState.questions.length) finishQuiz();
      else renderQuizQuestion();
    }, 900);
  }

  function finishQuiz(){
    const {score, questions, tagId, tagLabel} = quizState;
    quizScores.unshift({tagId, tagLabel, score, total: questions.length, date: Date.now()});
    quizScores = quizScores.slice(0, 40);
    saveQuizScores();
    const pct = Math.round((score/questions.length)*100);
    const message = pct >= 80 ? "Great work — you clearly know this area well."
      : pct >= 50 ? "Solid attempt. A little more reading and you'll have it down."
      : "Good start — this is a good area to browse more in the index.";
    quizCard.innerHTML = `
      <button class="icon-btn close-btn" id="closeQuiz" aria-label="Close">
        <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M18 6 6 18M6 6l12 12"/></svg>
      </button>
      <div class="quiz-result">
        <span class="detail-tag">${tagLabel}</span>
        <div class="score-big">${score}/${questions.length}</div>
        <p class="extract">${message}</p>
        <div style="display:flex;gap:10px;justify-content:center;margin-top:16px;">
          <button class="btn primary" id="retryQuiz">Try another</button>
          <button class="btn" id="doneQuiz">Done</button>
        </div>
      </div>
    `;
    el('closeQuiz').addEventListener('click', () => quizOverlay.classList.remove('open'));
    el('retryQuiz').addEventListener('click', openQuizHome);
    el('doneQuiz').addEventListener('click', () => quizOverlay.classList.remove('open'));
  }

  el('quizBtn').addEventListener('click', () => { openQuizHome(); quizOverlay.classList.add('open'); });
  quizOverlay.addEventListener('click', (e) => { if(e.target === quizOverlay) quizOverlay.classList.remove('open'); });

  // ---------- Symptom checker ----------
  const checkerOverlay = el('checkerOverlay');
  const checkerCard = el('checkerCard');

  async function loadCheckerHistory(){
    try{
      const res = await window.storage.get('symptomChecks', false);
      checkerChecks = res && res.value ? JSON.parse(res.value) : [];
    }catch(err){ checkerChecks = []; }
  }
  async function saveCheckerHistory(){
    try{ await window.storage.set('symptomChecks', JSON.stringify(checkerChecks), false); }catch(err){ /* best-effort */ }
  }

  function openCheckerHome(){
    checkerSelected = [];
    renderCheckerHome();
  }

  function renderCheckerHome(){
    checkerCard.innerHTML = `
      <button class="icon-btn close-btn" id="closeChecker" aria-label="Close">
        <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M18 6 6 18M6 6l12 12"/></svg>
      </button>
      <span class="detail-tag">Symptom matcher</span>
      <h2 style="font-size:24px;">What are you noticing?</h2>
      <div class="disclaimer" style="margin:14px 0 4px; max-width:100%;">
        <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="#A6433C" stroke-width="2"><circle cx="12" cy="12" r="10"/><path d="M12 8v5M12 16h.01"/></svg>
        <p><strong>This only compares your symptoms against the ${DISEASES.length} conditions in this index</strong> using simple keyword overlap. It's not a diagnosis and can't account for everything about your situation. If something feels off, talk to a doctor or another trusted adult.</p>
      </div>
      <div class="search-wrap" style="max-width:100%;">
        <div class="search-box">
          <svg width="17" height="17" viewBox="0 0 24 24" fill="none" stroke="#6C7266" stroke-width="2"><circle cx="11" cy="11" r="8"/><path d="m21 21-4.3-4.3"/></svg>
          <input type="text" id="symptomInput" placeholder="Type a symptom, e.g. 'sore throat'..." autocomplete="off">
        </div>
        <div class="search-results" id="symptomSuggest"></div>
      </div>
      <div class="chip-row" id="chipRow"></div>
      <div style="display:flex; gap:10px; margin-top:6px;">
        <button class="btn primary" id="findMatchesBtn" disabled>Find closest matches</button>
      </div>
      <div id="checkerPast"></div>
    `;
    el('closeChecker').addEventListener('click', () => checkerOverlay.classList.remove('open'));
    renderChips();
    renderCheckerPast();

    const input = el('symptomInput');
    const suggest = el('symptomSuggest');
    let sTimer = null;

    input.addEventListener('input', () => {
      clearTimeout(sTimer);
      const q = input.value.trim().toLowerCase();
      if(!q){ suggest.classList.remove('open'); return; }
      sTimer = setTimeout(() => {
        const matches = ALL_SYMPTOMS.filter(s => s.toLowerCase().includes(q) && !checkerSelected.includes(s)).slice(0,8);
        if(!matches.length){
          suggest.innerHTML = `<div class="search-result-item">No matching symptoms indexed. Try a different word.</div>`;
        }else{
          suggest.innerHTML = matches.map(s => `<div class="search-result-item" data-sym="${s.replace(/"/g,'&quot;')}"><span class="r-title">${s}</span></div>`).join('');
          suggest.querySelectorAll('.search-result-item[data-sym]').forEach(item => {
            item.addEventListener('click', () => {
              addSymptom(item.dataset.sym);
              input.value = '';
              suggest.classList.remove('open');
              input.focus();
            });
          });
        }
        suggest.classList.add('open');
      }, 150);
    });

    input.addEventListener('keydown', (e) => {
      if(e.key === 'Enter'){
        e.preventDefault();
        const q = input.value.trim();
        const exact = ALL_SYMPTOMS.find(s => s.toLowerCase() === q.toLowerCase());
        if(exact){ addSymptom(exact); input.value=''; suggest.classList.remove('open'); }
      }
    });

    document.addEventListener('click', (e) => {
      if(!e.target.closest('.search-wrap')) suggest.classList.remove('open');
    });

    el('findMatchesBtn').addEventListener('click', () => runMatch());
  }

  function addSymptom(sym){
    if(!checkerSelected.includes(sym)) checkerSelected.push(sym);
    renderChips();
  }
  function removeSymptom(sym){
    checkerSelected = checkerSelected.filter(s => s !== sym);
    renderChips();
  }
  function renderChips(){
    const row = el('chipRow');
    if(!row) return;
    row.innerHTML = checkerSelected.map(s => `
      <span class="chip">${s}<button data-sym="${s.replace(/"/g,'&quot;')}" aria-label="Remove ${s}">
        <svg width="12" height="12" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="3"><path d="M18 6 6 18M6 6l12 12"/></svg>
      </button></span>
    `).join('');
    row.querySelectorAll('button[data-sym]').forEach(btn => {
      btn.addEventListener('click', () => removeSymptom(btn.dataset.sym));
    });
    const findBtn = el('findMatchesBtn');
    if(findBtn) findBtn.disabled = checkerSelected.length === 0;
  }

  function computeMatches(selected){
    const selLower = selected.map(s => s.toLowerCase());
    const scored = DISEASES.map(d => {
      const dSymLower = d.symptoms.map(s => s.toLowerCase());
      const matched = selected.filter((s,i) => dSymLower.includes(selLower[i]));
      return {disease:d, matchedCount:matched.length, matchedSymptoms:matched};
    }).filter(r => r.matchedCount > 0);
    scored.sort((a,b) => b.matchedCount - a.matchedCount || (b.matchedCount/b.disease.symptoms.length) - (a.matchedCount/a.disease.symptoms.length));
    return scored.slice(0,6);
  }

  function runMatch(){
    const results = computeMatches(checkerSelected);
    checkerChecks.unshift({
      symptoms: checkerSelected.slice(),
      topMatches: results.slice(0,3).map(r => ({title:r.disease.title, display:r.disease.display, count:r.matchedCount})),
      date: Date.now()
    });
    checkerChecks = checkerChecks.slice(0, 20);
    saveCheckerHistory();
    renderMatchResults(results);
  }

  function renderMatchResults(results){
    checkerCard.innerHTML = `
      <button class="icon-btn close-btn" id="closeChecker" aria-label="Close">
        <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M18 6 6 18M6 6l12 12"/></svg>
      </button>
      <span class="detail-tag">Symptom matcher</span>
      <h2 style="font-size:24px;">Closest matches</h2>
      <p class="extract" style="margin-bottom:14px;">Based on: ${checkerSelected.join(', ')}</p>
      ${results.length ? results.map(r => {
        const t = tagMap[r.disease.tag];
        return `
          <div class="match-item" data-title="${r.disease.title.replace(/"/g,'&quot;')}" data-display="${r.disease.display.replace(/"/g,'&quot;')}" data-tag="${r.disease.tag}" style="--dot:${t.color}">
            <div style="flex:1;">
              <span class="tag-chip" style="margin-bottom:6px;">${t.label}</span>
              <h4>${r.disease.display}</h4>
              <div class="matched-syms">Matches: ${r.matchedSymptoms.join(', ')}</div>
            </div>
            <span class="match-score">${r.matchedCount}/${checkerSelected.length}</span>
          </div>
        `;
      }).join('') : `<div class="empty-state"><span class="mono">— no matches —</span>None of the indexed conditions list these symptoms. Try different terms.</div>`}
      <div style="display:flex; gap:10px; margin-top:18px;">
        <button class="btn primary" id="checkerAgain">Check again</button>
        <button class="btn" id="checkerDone">Done</button>
      </div>
      <div class="detail-note">This list is based on shared keywords with a small curated index, not a medical evaluation. If your symptoms are severe, sudden, or worrying, contact a doctor.</div>
    `;
    el('closeChecker').addEventListener('click', () => checkerOverlay.classList.remove('open'));
    el('checkerAgain').addEventListener('click', openCheckerHome);
    el('checkerDone').addEventListener('click', () => checkerOverlay.classList.remove('open'));
    checkerCard.querySelectorAll('.match-item').forEach(item => {
      item.addEventListener('click', () => {
        checkerOverlay.classList.remove('open');
        openDetail(item.dataset.title, item.dataset.display, item.dataset.tag);
      });
    });
  }

  function renderCheckerPast(){
    const box = el('checkerPast');
    if(!box) return;
    if(!checkerChecks.length){ box.innerHTML = ''; return; }
    box.innerHTML = `<div class="quiz-past"><div class="rail-title">Past checks</div>` + checkerChecks.slice(0,5).map(c => `
      <div class="quiz-past-item"><span>${c.symptoms.slice(0,3).join(', ')}${c.symptoms.length>3?'…':''}</span><span>${new Date(c.date).toLocaleDateString()}</span></div>
    `).join('') + `</div>`;
  }

  el('checkerBtn').addEventListener('click', () => { openCheckerHome(); checkerOverlay.classList.add('open'); });
  checkerOverlay.addEventListener('click', (e) => { if(e.target === checkerOverlay) checkerOverlay.classList.remove('open'); });

  document.addEventListener('keydown', (e) => {
    if(e.key === 'Escape'){ closeDetail(); historyOverlay.classList.remove('open'); quizOverlay.classList.remove('open'); checkerOverlay.classList.remove('open'); }
  });

  // ---------- Init ----------
  renderRail();
  renderGrid();
  loadHistory();
  loadQuizScores();
  loadCheckerHistory();
})();
</script>
</body>
</html>
