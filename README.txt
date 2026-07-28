<!doctype html>
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Keelhaul Gaming vs Xenos Petting Zoo</title>
<style>
:root {
  color-scheme: dark;
  --bg:#010912;
  --panel:#03111d;
  --panel-2:#061725;
  --cyan:#16c8ff;
  --cyan-soft:#0c86ba;
  --purple:#cb54ff;
  --purple-soft:#7d2aa0;
  --text:#f4f7fa;
  --muted:#b8c1cc;
  --gold:#efc27b;
}
* { box-sizing:border-box; }
html { background:#00070e; }
body {
  margin:0;
  min-height:100vh;
  color:var(--text);
  font-family:"Arial Narrow","Roboto Condensed","Segoe UI",Arial,sans-serif;
  background:
    radial-gradient(circle at 84% 8%, rgba(0,154,255,.12), transparent 28rem),
    radial-gradient(circle at 8% 70%, rgba(167,40,255,.11), transparent 30rem),
    radial-gradient(circle at 20% 25%, #ffffff 0 1px, transparent 1.5px),
    radial-gradient(circle at 73% 58%, #ffffff 0 1px, transparent 1.5px),
    radial-gradient(circle at 91% 80%, #39a9ff 0 1px, transparent 1.5px),
    linear-gradient(145deg,#020711,#00040a 72%);
  background-size:auto,auto,190px 190px,260px 260px,330px 330px,auto;
}
button,input { font:inherit; }
.site-shell { width:min(1536px,100%); margin:0 auto; padding:14px 14px 24px; }

.discord-bar {
  display:grid;
  grid-template-columns:1fr 1px 1fr;
  align-items:center;
  min-height:142px;
  border:1px solid transparent;
  border-radius:18px;
  background:
    linear-gradient(#020b15,#020b15) padding-box,
    linear-gradient(90deg,var(--purple),var(--cyan)) border-box;
  overflow:hidden;
}
.discord-divider { width:1px;height:88px;background:#334250;justify-self:center; }
.discord-link {
  min-width:0;
  display:grid;
  grid-template-columns:98px 1fr;
  gap:20px;
  align-items:center;
  padding:20px 58px;
  color:white;
  text-decoration:none;
}
.discord-link img { width:88px;height:88px;object-fit:cover;border-radius:22px; }
.discord-copy strong {
  display:block;
  font-size:clamp(1.45rem,2.6vw,2.45rem);
  line-height:1;
  letter-spacing:.04em;
  text-transform:uppercase;
}
.discord-link:first-child strong,.discord-link:first-child .invite { color:#c461ff; }
.discord-link:last-child strong,.discord-link:last-child .invite { color:#29cfff; }
.discord-copy span { display:block;margin-top:8px;font-size:1.18rem;color:#e0e5ea; }
.discord-copy .invite { text-decoration:underline;font-size:1.05rem; }

.scoreboard {
  margin-top:20px;
  position:relative;
}
.team-heading {
  display:grid;
  grid-template-columns:1fr auto auto 1fr;
  gap:18px;
  align-items:center;
  margin:10px 0 8px;
  text-transform:uppercase;
}
.team-heading::before,.team-heading::after {
  content:"";
  height:2px;
  background:linear-gradient(90deg,transparent,currentColor);
}
.team-heading::after { background:linear-gradient(90deg,currentColor,transparent); }
.team-heading h2 {
  margin:0;
  white-space:nowrap;
  font-size:clamp(1.5rem,3vw,2.25rem);
  letter-spacing:.08em;
}
.team-total {
  white-space:nowrap;
  font-size:clamp(1rem,1.8vw,1.45rem);
  font-weight:800;
  letter-spacing:.04em;
}
.team-total strong { font-size:1.35em; }
.keelhaul-heading { color:#dce4ea; }
.keelhaul-heading .team-total strong { color:var(--cyan); }
.xpz-heading { color:#b86cf1; }
.xpz-heading .team-total strong { color:var(--purple); }

.board-scroller { overflow-x:auto; padding-bottom:8px; }
.board {
  min-width:1230px;
  display:grid;
  grid-template-columns:repeat(8,minmax(135px,1fr));
  gap:8px;
  align-items:start;
}
.matchup {
  display:grid;
  grid-template-rows:255px 142px 255px;
  gap:10px;
  min-width:0;
}
.army-card {
  position:relative;
  display:grid;
  grid-template-rows:155px 1fr;
  width:100%;
  padding:0;
  overflow:hidden;
  color:#fff;
  border-radius:11px;
  background:linear-gradient(#051525,#020912);
  cursor:pointer;
  text-align:center;
  transition:transform .14s ease,filter .14s ease,box-shadow .14s ease;
}
.keelhaul-card { border:1.5px solid var(--cyan); box-shadow:inset 0 0 18px #061c2d; }
.xpz-card { border:1.5px solid var(--purple); box-shadow:inset 0 0 18px #21102c; }
.army-card:hover,.army-card:focus-visible {
  transform:translateY(-4px);
  filter:brightness(1.12);
  outline:none;
  z-index:3;
}
.keelhaul-card:hover,.keelhaul-card:focus-visible { box-shadow:0 0 0 2px #7ce5ff,0 10px 25px #000; }
.xpz-card:hover,.xpz-card:focus-visible { box-shadow:0 0 0 2px #e4a2ff,0 10px 25px #000; }
.army-card img { width:100%;height:155px;object-fit:cover;border-bottom:1px solid #263a4a; }
.card-copy { min-height:98px;display:flex;flex-direction:column;justify-content:center;padding:8px 7px 11px; }
.card-copy strong {
  display:block;
  font-size:.98rem;
  line-height:1.22;
  text-transform:uppercase;
}
.card-copy small {
  display:block;
  margin-top:9px;
  color:#e0e5eb;
  font-size:.9rem;
  line-height:1.15;
}
.slot-number {
  position:absolute;z-index:2;top:6px;left:7px;
  font-weight:900;font-size:1.2rem;text-shadow:0 1px 3px #000;
}
.score-stack {
  position:relative;
  display:grid;
  grid-template-rows:42px 32px 42px;
  justify-items:center;
  align-content:center;
  gap:4px;
}
.score-stack::before,.score-stack::after {
  content:"";
  position:absolute;
  top:12px;bottom:12px;width:1px;background:#263845;
}
.score-stack::before { left:0; }
.score-stack::after { right:0; }
.score-input {
  width:86px;height:40px;
  border-radius:7px;
  background:#020812;
  color:white;
  text-align:center;
  font-size:1.45rem;
  font-weight:900;
  outline:none;
}
.keelhaul-score { border:1.5px solid var(--cyan); }
.xpz-score { border:1.5px solid var(--purple); }
.score-input:focus { box-shadow:0 0 0 2px #ffffff55; }
.score-stack span { color:#7f8790;font-weight:900;font-size:1.1rem;align-self:center; }

.help {
  text-align:center;
  margin:18px 0 0;
  color:#c7cbd1;
  font-size:1rem;
  word-spacing:.12em;
}

.preview {
  position:fixed;
  z-index:60;
  display:none;
  width:min(340px,calc(100vw - 20px));
  pointer-events:none;
  border:1px solid #28cfff;
  border-radius:10px;
  background:#03101bf4;
  padding:14px 16px;
  box-shadow:0 16px 40px #000;
}
.preview strong { display:block;color:var(--gold);font-size:1.1rem; }
.preview span { display:block;margin-top:6px;color:#dce4eb; }
.preview small { display:block;margin-top:5px;color:#aeb8c3; }

.army-panel {
  position:fixed;
  z-index:100;
  top:120px;
  right:16px;
  width:min(430px,calc(100vw - 24px));
  height:min(82vh,835px);
  display:none;
  flex-direction:column;
  border:1.5px solid var(--cyan);
  border-radius:18px;
  background:linear-gradient(155deg,#07121d,#020a12 76%);
  box-shadow:0 20px 70px #000;
  overflow:hidden;
}
.army-panel.open { display:flex; }
.panel-head {
  display:grid;
  grid-template-columns:64px 1fr 34px;
  gap:12px;
  align-items:start;
  padding:18px 16px 14px;
  border-bottom:1px solid #30404c;
}
.panel-emblem {
  width:58px;height:58px;border-radius:50%;
  display:grid;place-items:center;
  border:1px solid #8f744e;
  color:#f4d8a3;
  font:900 1.65rem Georgia,serif;
  background:#121416;
}
.panel-head h3 {
  margin:0;
  color:var(--gold);
  font-size:1.25rem;
  text-transform:uppercase;
}
.panel-head p { margin:5px 0 0;color:#cfd6dd;font-size:.9rem;line-height:1.35; }
.panel-close {
  border:0;background:transparent;color:#7b87a1;font-size:1.8rem;cursor:pointer;padding:0;
}
.panel-list {
  margin:0;
  padding:14px 18px 28px;
  overflow:auto;
  white-space:pre-wrap;
  color:#f2f3f4;
  font:14px/1.55 "Arial Narrow","Segoe UI",Arial,sans-serif;
}
.panel-list::-webkit-scrollbar { width:8px; }
.panel-list::-webkit-scrollbar-thumb { background:#69737c;border-radius:8px; }

@media(max-width:900px) {
  .discord-bar { grid-template-columns:1fr; }
  .discord-divider { width:calc(100% - 32px);height:1px; }
  .discord-link { padding:18px 24px;grid-template-columns:72px 1fr; }
  .discord-link img { width:66px;height:66px;border-radius:16px; }
  .team-heading { grid-template-columns:1fr;gap:5px;text-align:center; }
  .team-heading::before,.team-heading::after { display:none; }
  .army-panel { top:12px;right:12px;height:calc(100vh - 24px); }
}
</style>
</head>
<body>
<div class="site-shell">
  <nav class="discord-bar" aria-label="Team Discord servers">
    <a class="discord-link" href="https://discord.gg/ZdPpB8VPE" target="_blank" rel="noopener noreferrer">
      <img src="assets/discord-xpz.png" alt="Discord logo">
      <span class="discord-copy">
        <strong>XPZ Discord</strong>
        <span>Join the Xenos Petting Zoo</span>
        <span class="invite">discord.gg/ZdPpB8VPE</span>
      </span>
    </a>
    <span class="discord-divider" aria-hidden="true"></span>
    <a class="discord-link" href="https://discord.gg/q3psAhPPP" target="_blank" rel="noopener noreferrer">
      <img src="assets/discord-keelhaul.png" alt="Discord logo">
      <span class="discord-copy">
        <strong>Keelhaul Gaming Discord</strong>
        <span>Join Keelhaul Gaming</span>
        <span class="invite">discord.gg/q3psAhPPP</span>
      </span>
    </a>
  </nav>

  <main class="scoreboard">
    <header class="team-heading keelhaul-heading">
      <span></span>
      <h2>Keelhaul Gaming</h2>
      <div class="team-total">Total: <strong id="keelhaulTotal">0</strong> Points</div>
      <span></span>
    </header>

    <div class="board-scroller">
      <section class="board" aria-label="Eight team matchups">
        
      <article class="matchup">
        <button class="army-card keelhaul-card" data-index="0" aria-label="Open RECON army list">
          <span class="slot-number">1</span>
          <img src="assets/top-1.jpg" alt="Adepta Sororitas themed artwork">
          <span class="card-copy">
            <strong>RECON</strong>
            <small>Adepta Sororitas</small>
          </span>
        </button>

        <div class="score-stack">
          <input class="score-input keelhaul-score" aria-label="Keelhaul Gaming score, matchup 1"
                 type="text" inputmode="numeric" pattern="[0-9]*" value="0">
          <span>VS</span>
          <input class="score-input xpz-score" aria-label="Xenos Petting Zoo score, matchup 1"
                 type="text" inputmode="numeric" pattern="[0-9]*" value="0">
        </div>

        <button class="army-card xpz-card" data-index="8" aria-label="Open KYLE N. army list">
          <img src="assets/bottom-1.jpg" alt="Emperor’s Children themed artwork">
          <span class="card-copy">
            <strong>KYLE N.</strong>
            <small>Emperor’s Children</small>
          </span>
        </button>
      </article>
    
      <article class="matchup">
        <button class="army-card keelhaul-card" data-index="1" aria-label="Open SHE ASSIMILATION army list">
          <span class="slot-number">2</span>
          <img src="assets/top-2.jpg" alt="Tyranids themed artwork">
          <span class="card-copy">
            <strong>SHE ASSIMILATION</strong>
            <small>Tyranids</small>
          </span>
        </button>

        <div class="score-stack">
          <input class="score-input keelhaul-score" aria-label="Keelhaul Gaming score, matchup 2"
                 type="text" inputmode="numeric" pattern="[0-9]*" value="0">
          <span>VS</span>
          <input class="score-input xpz-score" aria-label="Xenos Petting Zoo score, matchup 2"
                 type="text" inputmode="numeric" pattern="[0-9]*" value="0">
        </div>

        <button class="army-card xpz-card" data-index="9" aria-label="Open MATT GREEN army list">
          <img src="assets/bottom-2.jpg" alt="Thousand Sons themed artwork">
          <span class="card-copy">
            <strong>MATT GREEN</strong>
            <small>Thousand Sons</small>
          </span>
        </button>
      </article>
    
      <article class="matchup">
        <button class="army-card keelhaul-card" data-index="2" aria-label="Open A NIGHT AT THE R’AUXBURY army list">
          <span class="slot-number">3</span>
          <img src="assets/top-3.jpg" alt="T’au Empire themed artwork">
          <span class="card-copy">
            <strong>A NIGHT AT THE R’AUXBURY</strong>
            <small>T’au Empire</small>
          </span>
        </button>

        <div class="score-stack">
          <input class="score-input keelhaul-score" aria-label="Keelhaul Gaming score, matchup 3"
                 type="text" inputmode="numeric" pattern="[0-9]*" value="0">
          <span>VS</span>
          <input class="score-input xpz-score" aria-label="Xenos Petting Zoo score, matchup 3"
                 type="text" inputmode="numeric" pattern="[0-9]*" value="0">
        </div>

        <button class="army-card xpz-card" data-index="10" aria-label="Open LOGAN HEATH army list">
          <img src="assets/bottom-3.jpg" alt="T’au Empire themed artwork">
          <span class="card-copy">
            <strong>LOGAN HEATH</strong>
            <small>T’au Empire</small>
          </span>
        </button>
      </article>
    
      <article class="matchup">
        <button class="army-card keelhaul-card" data-index="3" aria-label="Open GRANNY FANNY’S FIGHTING FORCE army list">
          <span class="slot-number">4</span>
          <img src="assets/top-4.jpg" alt="Adeptus Mechanicus themed artwork">
          <span class="card-copy">
            <strong>GRANNY FANNY’S FIGHTING FORCE</strong>
            <small>Adeptus Mechanicus</small>
          </span>
        </button>

        <div class="score-stack">
          <input class="score-input keelhaul-score" aria-label="Keelhaul Gaming score, matchup 4"
                 type="text" inputmode="numeric" pattern="[0-9]*" value="0">
          <span>VS</span>
          <input class="score-input xpz-score" aria-label="Xenos Petting Zoo score, matchup 4"
                 type="text" inputmode="numeric" pattern="[0-9]*" value="0">
        </div>

        <button class="army-card xpz-card" data-index="11" aria-label="Open ISAAC T army list">
          <img src="assets/bottom-4.jpg" alt="Custodes themed artwork">
          <span class="card-copy">
            <strong>ISAAC T</strong>
            <small>Custodes</small>
          </span>
        </button>
      </article>
    
      <article class="matchup">
        <button class="army-card keelhaul-card" data-index="4" aria-label="Open JAKE MADE ME TOUCH YOU army list">
          <span class="slot-number">5</span>
          <img src="assets/top-5.jpg" alt="Orks themed artwork">
          <span class="card-copy">
            <strong>JAKE MADE ME TOUCH YOU</strong>
            <small>Orks</small>
          </span>
        </button>

        <div class="score-stack">
          <input class="score-input keelhaul-score" aria-label="Keelhaul Gaming score, matchup 5"
                 type="text" inputmode="numeric" pattern="[0-9]*" value="0">
          <span>VS</span>
          <input class="score-input xpz-score" aria-label="Xenos Petting Zoo score, matchup 5"
                 type="text" inputmode="numeric" pattern="[0-9]*" value="0">
        </div>

        <button class="army-card xpz-card" data-index="12" aria-label="Open JASON MCKENZIE army list">
          <img src="assets/bottom-5.jpg" alt="Chaos Daemons themed artwork">
          <span class="card-copy">
            <strong>JASON MCKENZIE</strong>
            <small>Chaos Daemons</small>
          </span>
        </button>
      </article>
    
      <article class="matchup">
        <button class="army-card keelhaul-card" data-index="5" aria-label="Open ROCK AND STONE COLD STEVE AUSTIN army list">
          <span class="slot-number">6</span>
          <img src="assets/top-6.jpg" alt="Leagues of Votann themed artwork">
          <span class="card-copy">
            <strong>ROCK AND STONE COLD STEVE AUSTIN</strong>
            <small>Leagues of Votann</small>
          </span>
        </button>

        <div class="score-stack">
          <input class="score-input keelhaul-score" aria-label="Keelhaul Gaming score, matchup 6"
                 type="text" inputmode="numeric" pattern="[0-9]*" value="0">
          <span>VS</span>
          <input class="score-input xpz-score" aria-label="Xenos Petting Zoo score, matchup 6"
                 type="text" inputmode="numeric" pattern="[0-9]*" value="0">
        </div>

        <button class="army-card xpz-card" data-index="13" aria-label="Open RAINEY army list">
          <img src="assets/bottom-6.jpg" alt="Space Marines (Ultramarines) themed artwork">
          <span class="card-copy">
            <strong>RAINEY</strong>
            <small>Space Marines (Ultramarines)</small>
          </span>
        </button>
      </article>
    
      <article class="matchup">
        <button class="army-card keelhaul-card" data-index="6" aria-label="Open TECHNOSORCERY army list">
          <span class="slot-number">7</span>
          <img src="assets/top-7.jpg" alt="Necrons themed artwork">
          <span class="card-copy">
            <strong>TECHNOSORCERY</strong>
            <small>Necrons</small>
          </span>
        </button>

        <div class="score-stack">
          <input class="score-input keelhaul-score" aria-label="Keelhaul Gaming score, matchup 7"
                 type="text" inputmode="numeric" pattern="[0-9]*" value="0">
          <span>VS</span>
          <input class="score-input xpz-score" aria-label="Xenos Petting Zoo score, matchup 7"
                 type="text" inputmode="numeric" pattern="[0-9]*" value="0">
        </div>

        <button class="army-card xpz-card" data-index="14" aria-label="Open TONY army list">
          <img src="assets/bottom-7.jpg" alt="Orks themed artwork">
          <span class="card-copy">
            <strong>TONY</strong>
            <small>Orks</small>
          </span>
        </button>
      </article>
    
      <article class="matchup">
        <button class="army-card keelhaul-card" data-index="7" aria-label="Open RED HOT GREEN CHILI PEPPERS army list">
          <span class="slot-number">8</span>
          <img src="assets/top-8.jpg" alt="Space Marines themed artwork">
          <span class="card-copy">
            <strong>RED HOT GREEN CHILI PEPPERS</strong>
            <small>Space Marines</small>
          </span>
        </button>

        <div class="score-stack">
          <input class="score-input keelhaul-score" aria-label="Keelhaul Gaming score, matchup 8"
                 type="text" inputmode="numeric" pattern="[0-9]*" value="0">
          <span>VS</span>
          <input class="score-input xpz-score" aria-label="Xenos Petting Zoo score, matchup 8"
                 type="text" inputmode="numeric" pattern="[0-9]*" value="0">
        </div>

        <button class="army-card xpz-card" data-index="15" aria-label="Open DILLON army list">
          <img src="assets/bottom-8.jpg" alt="Tyranids themed artwork">
          <span class="card-copy">
            <strong>DILLON</strong>
            <small>Tyranids</small>
          </span>
        </button>
      </article>
    
      </section>
    </div>

    <header class="team-heading xpz-heading">
      <span></span>
      <h2>Xenos Petting Zoo</h2>
      <div class="team-total">Total: <strong id="xpzTotal">0</strong> Points</div>
      <span></span>
    </header>

    <p class="help">Hover a card for preview &nbsp;•&nbsp; Click a card to view full army list &nbsp;•&nbsp; Edit scores in the boxes</p>
  </main>
</div>

<div class="preview" id="preview" role="status"></div>

<aside class="army-panel" id="armyPanel" aria-hidden="true">
  <div class="panel-head">
    <div class="panel-emblem" id="panelEmblem">◆</div>
    <div>
      <h3 id="panelTitle"></h3>
      <p id="panelMeta"></p>
    </div>
    <button class="panel-close" id="panelClose" aria-label="Close army list">×</button>
  </div>
  <pre class="panel-list" id="panelList"></pre>
</aside>

<script>
const armies = [{"team": "Keelhaul Gaming", "player": "Recon", "faction": "Adepta Sororitas", "title": "Recon — 2,000 pts", "meta": "Army of Faith + Chorus of Condemnation • Reconnaissance", "list": "ATTACHED UNITS\nMorvenn Vahl (200) + Paragon Warsuits (210)\nSaint Celestine (150) + Zephyrim Squad (75)\nCanoness with Jump Pack (90, Blade of Saint Ellynor) + Zephyrim Squad (75)\n\nCHARACTERS\nDaemonifuge (85)\n\nBATTLELINE\nBattle Sisters Squad (100)\n\nDEDICATED TRANSPORTS\nImmolator (100) — Immolation flamers\nImmolator (100) — Immolation flamers\nImmolator (115) — Twin multi-melta\n\nOTHER DATASHEETS\nCastigator (165) — Battle cannon\nCastigator (165) — Battle cannon\nDominion Squad (110) — 4 meltaguns\nDominion Squad (110) — 4 meltaguns\nSeraphim Squad (75) — Inferno pistols\nSeraphim Squad (75) — Hand flamers"}, {"team": "Keelhaul Gaming", "player": "Swarm", "faction": "Tyranids", "title": "She assimilation on my swarm till my biophagic flows — 2,000 pts", "meta": "Assimilation Swarm + Talons of the Norn Queen • Take and Hold", "list": "CHARACTERS\nTyranid Prime with Lash Whip (75) — Warlord\n\nOTHER DATASHEETS\nBiovores (60)\nExocrine (140)\nMaleceptor (190)\nMaleceptor (190)\nNorn Assimilator (275) — Synaptoprescience\nNorn Assimilator (270)\nNorn Emissary (250)\nPsychophage (110)\nPsychophage (110)\nRipper Swarms (30)\nTyrannofex (190) — Acid spray\nVon Ryan’s Leapers (55)\nVon Ryan’s Leapers (55)"}, {"team": "Keelhaul Gaming", "player": "R’Auxbury", "faction": "T’au Empire", "title": "A NIGHT AT THE R'AUXBURY — 2,000 pts", "meta": "Retaliation Cadre • Purge the Foe", "list": "ATTACHED UNITS\nCommander Farsight (70) + Crisis Sunforge Battlesuits (125)\nEnforcer Commander (100, Starflare Ignition System) + Crisis Fireknife Battlesuits (130)\nColdstar Commander (110, Prototype Weapon System) + Crisis Starscythe Battlesuits (90)\nColdstar Commander (95) + Crisis Sunforge Battlesuits (125)\n\nCHARACTERS\nThe Twin Lance (220)\n\nOTHER DATASHEETS\nGhostkeel Battlesuit (150)\nKroot Carnivores (65)\nPathfinder Team (90)\nRiptide Battlesuit (215)\nRiptide Battlesuit (215)\nStealth Battlesuits (100)\nStealth Battlesuits (100)"}, {"team": "Keelhaul Gaming", "player": "Granny Fanny", "faction": "Adeptus Mechanicus", "title": "Granny Fanny’s Fighting Force — 1,995 pts", "meta": "Eradication Cohort • Purge the Foe", "list": "ATTACHED UNITS\nSkitarii Marshal (35) + Hastarii Exterminators (105)\nSkitarii Marshal (35) + Hastarii Fusiliers (115)\nTech-Priest Dominus (80, Martial Signatum Amplificator) + Kataphron Breachers (310)\n\nCHARACTERS\nSydonian Skatros (50)\nThulia Ghuld (180) — Warlord\n\nBATTLELINE\nSkitarii Rangers (85)\nSkitarii Rangers (85)\nSkitarii Vanguard (85)\nSkitarii Vanguard (85)\n\nOTHER DATASHEETS\nOnager Dunecrawler (155)\nSicarian Infiltrators (75)\nSicarian Infiltrators (75)\nSicarian Ruststalkers (75)\nSicarian Ruststalkers (75)\nSkorpius Disintegrator (170)\nSydonian Dragoon with Taser Lance (60)\nSydonian Dragoon with Taser Lance (60)"}, {"team": "Keelhaul Gaming", "player": "Jake", "faction": "Orks", "title": "Jake Made Me Touch You — 2,000 pts", "meta": "Green Tide • Take and Hold", "list": "ATTACHED UNITS\nGhazghkull Thraka (235) + Painboy (105, Bloodthirsty Belligerence) + 20 Boyz (160)\nBigboss (55) + Painboy (90) + 20 Boyz (160)\nBigboss (75, Raucous Warcaller) + Painboy (90) + 20 Boyz (160)\nWeirdboy (65) + 20 Boyz (170)\nBigboss (65, Ferocious Show Off) + 20 Boyz (170)\nZodgrod Wortsnagga (80) + 20 Gretchin / 2 Runtherds (90)\n\nOTHER DATASHEETS\nGretchin (45)\nKommandos (120)\nStormboyz (65)"}, {"team": "Keelhaul Gaming", "player": "Rock & Stone", "faction": "Leagues of Votann", "title": "Rock and Stone Cold Steve Austin — 1,995 pts", "meta": "Armoured Trailblazers + Needgaârd Oathband • Disruption", "list": "ATTACHED UNITS\nBrôkhyr Iron-master (100, Oathbound Speculator) + 6 Brôkhyr Thunderkyn (160)\nKâhl (65) + 10 Einhyr Hearthguard (270)\n\nCHARACTERS\nÛthar the Destined (90) — Warlord\n\nBATTLELINE\nHearthkyn Warriors (100)\nHearthkyn Warriors (100)\n\nDEDICATED TRANSPORTS\nKapricus Carrier (70)\nKapricus Carrier (70)\nSagitaur (100, Saturation Rounds)\nSagitaur (85)\n\nOTHER DATASHEETS\nBrôkhyr Thunderkyn (160)\nBrôkhyr Thunderkyn (90)\nEinhyr Hearthguard (130)\nHernkyn Pioneers (80)\nHernkyn Pioneers (80)\nHernkyn Yaegirs (90)\nHernkyn Yaegirs (90)\nKapricus Defenders (65)"}, {"team": "Keelhaul Gaming", "player": "Technosorcerer", "faction": "Necrons", "title": "Cryptek Conclave / Skyshroud Spearhead — 2,000 pts", "meta": "Priority Assets • 16 units", "list": "CHARACTERS\nC’tan Shard of the Void Dragon (345)\nChronomancer (85) — Gravitic Bolas\nIlluminor Szeras (175)\nOverlord with Translocation Shroud (105) — Quantum Abacus\nPlasmancer (65) — Atomic Disintegrators\nTechnomancer (80)\n\nUNITS\nImmortals x10 (140) — Tesla carbines\nImmortals x10 (140) — Gauss blasters\nCanoptek Reanimator (75)\nCanoptek Tomb Crawlers x2 (50)\nCanoptek Tomb Crawlers x2 (50)\nCanoptek Wraiths x6 (220)\nOphydian Destroyers x3 (80)\nTomb Blades x6 (140)\nTomb Blades x6 (140)\nTriarch Stalker (110)"}, {"team": "Keelhaul Gaming", "player": "Salamanders", "faction": "Space Marines", "title": "Red Hot Green Chili Peppers — 2,000 pts", "meta": "Salamanders • Forgefather’s Seekers + Librarius Conclave • Priority Assets", "list": "ATTACHED UNITS\nAdrax Agatone (80) + Lieutenant (45) + Bladeguard Veterans x6 (160)\nLibrarian (105, Fusillade) + Hellblasters x10 (220)\nLibrarian (80, Immolator) + Infernus Marines x10 (180)\nLibrarian (95, Temporal Corridor) + Infernus Marines x10 (180)\n\nCHARACTERS\nVulkan He’stan (85) — Warlord\n\nOTHER DATASHEETS\nIncursor Squad (85)\nLand Raider Redeemer (250)\nScout Squad (65)\nVindicator (185)\nVindicator (185)"}, {"team": "Xenos Petting Zoo", "player": "Kyle N.", "faction": "Emperor’s Children", "title": "Carnival Disruption Teams — 1,995 pts", "meta": "Carnival of Excess + Elegant Brutes • Disruption • Discord: DysposableHero", "list": "CHARACTERS\nFulgrim (340) — Warlord\nKeeper of Secrets (255)\nLord Exultant (80)\nLord Exultant (80)\n\nBATTLELINE\nDaemonettes (90)\nDaemonettes (90)\nDaemonettes (90)\nInfractors (85)\nInfractors (85)\nTormentors (80)\n\nDEDICATED TRANSPORTS\nChaos Rhino (70)\n\nOTHER DATASHEETS\nChaos Terminators (160) — Frenzied Ferocity\nChaos Terminators (160) — Frenzied Ferocity\nDefiler (330)"}, {"team": "Xenos Petting Zoo", "player": "Matt Green", "faction": "Thousand Sons", "title": "Coven — 1,995 pts", "meta": "Grand Coven • Priority Assets • Discord: Headstrong", "list": "CHARACTERS\nDaemon Prince of Tzeentch with Wings (205) — Eldritch Vortex of E’Taph\nMagnus the Red (455) — Warlord\nSorcerer (85)\nSorcerer (105) — Umbralefic Crystal\nSorcerer (95)\nTzaangor Shaman (65)\nTzaangor Shaman (65)\n\nBATTLELINE\nRubric Marines (100)\nRubric Marines (100)\nRubric Marines (100)\nRubric Marines (110)\n\nDEDICATED TRANSPORTS\nChaos Rhino (80)\n\nOTHER DATASHEETS\nChaos Predator Annihilator (140)\nChaos Predator Annihilator (140)\nChaos Predator Annihilator (150)"}, {"team": "Xenos Petting Zoo", "player": "Logan Heath", "faction": "T’au Empire", "title": "Tau — 2,000 pts", "meta": "Retaliation Cadre • Purge the Foe • Discord: homelesspope", "list": "ATTACHED UNITS\nEnforcer Commander (100, Starflare Ignition System) + Crisis Fireknife Battlesuits (130)\nColdstar Commander (95) + Crisis Fireknife Battlesuits (130)\n\nCHARACTERS\nCommander Shadowsun (100) — Warlord\nEthereal (50)\nThe Twin Lance (220)\n\nOTHER DATASHEETS\nBroadside Battlesuits x2 (150)\nBroadside Battlesuits x2 (150)\nCrisis Starscythe Battlesuits (90)\nCrisis Starscythe Battlesuits (90)\nGhostkeel Battlesuit (165)\nRiptide Battlesuit (215)\nRiptide Battlesuit (215)\nStealth Battlesuits (100)"}, {"team": "Xenos Petting Zoo", "player": "Isaac T", "faction": "Adeptus Custodes", "title": "Lions of the Emperor / Silent Hunters — 2,000 pts", "meta": "Reconnaissance • Discord: ComanderChaCha", "list": "ATTACHED UNITS\nInquisitor Draxus (110) + Custodian Guard x4 (170)\nShield-Captain on Dawneagle Jetbike (155, Fierce Conqueror) + Vertus Praetors x2 (145)\nShield-Captain on Dawneagle Jetbike (170, Admonimortis) + Vertus Praetors x3 (215)\n\nCHARACTERS\nShield-Captain on Dawneagle Jetbike (165, Praesidius) — Warlord\n\nOTHER DATASHEETS\nAllarus Custodians x3 (165)\nAllarus Custodians x5 (275)\nVenatari Custodians x3 (165)\nVenatari Custodians x3 (165)\nWitchseekers x4 (50)\nWitchseekers x4 (50)"}, {"team": "Xenos Petting Zoo", "player": "Jason McKenzie", "faction": "Chaos Daemons", "title": "Shadow Stepping Like It’s DDR Night at Round 1 — 1,995 pts", "meta": "Cavalcade of Chaos + Shadow Legion • Purge the Foe • Discord: kindredfaeit", "list": "ATTACHED UNITS\nFlamers x6 (130)\nFateskimmer (125, Fade to Darkness) + Screamers x6 (160)\n\nCHARACTERS\nBe’lakor (390) — Warlord\nExalted Flamer (65)\nLord of Change (345) — Malice Made Manifest\n\nBATTLELINE\nPlaguebearers (115)\n\nOTHER DATASHEETS\nBeast of Nurgle (75)\nBeast of Nurgle (75)\nBurning Chariot (125) — Apocalyptic Steeds\nBurning Chariot (125) — Apocalyptic Steeds\nFlamers x6 (130)\nSoul Grinder (180) — Tzeentch\n\nALLIED UNITS\nChaos Lord in Terminator Armour (85)"}, {"team": "Xenos Petting Zoo", "player": "Rainey", "faction": "Space Marines", "title": "Luna Wolves 2.1 — 1,995 pts", "meta": "Ultramarines • Ceramite Sentinels • Take and Hold • Discord: @azenkrom", "list": "ATTACHED UNITS\nTerminator Captain (85) + Assault Terminators x10 (360)\nCaptain Titus (100) + Wardens of Ultramar (120) + Bladeguard Veterans x6 (160)\nTerminator Chaplain (90, Spy-skull Data Link) + Terminators x10 (320)\n\nBATTLELINE\nIntercessor Squad (80)\n\nOTHER DATASHEETS\nJump Pack Assault Intercessors (85)\nGladiator Lancer (160)\nGladiator Lancer (160)\nLand Speeder (105)\nLand Speeder (105)\nScout Squad (65)"}, {"team": "Xenos Petting Zoo", "player": "Tony", "faction": "Orks", "title": "Equal Booty for All — 1,995 pts", "meta": "Equatorial Hordes + Freebooter Krew • Take and Hold • Discord: TonyB", "list": "ATTACHED UNITS\nGhazghkull Thraka (235) + Painboy (105, Bionik Workshop) + Boyz x20 (160)\nBeastboss (80) + Beast Snagga Boyz x10 (90)\nBeastboss (80) + Beast Snagga Boyz x10 (90)\nWarboss (110, Kunnin’ Hunta) + Boyz x20 (160)\nZodgrod Wortsnagga (80) + Gretchin x20 / Runtherds x2 (90)\nBig Mek with Shokk Attack Gun (80) + Lootas x10 (100)\nBig Mek with Shokk Attack Gun (90, Git-Spotter Squig) + Tankbustas (125)\n\nCHARACTERS\nWazdakka Gutsmek (175)\n\nDEDICATED TRANSPORTS\nTrukk (55)\n\nOTHER DATASHEETS\nGretchin (45)\nGretchin (45)"}, {"team": "Xenos Petting Zoo", "player": "Dillon", "faction": "Tyranids", "title": "Ambush Predators / Vanguard Onslaught — 2,000 pts", "meta": "Reconnaissance • Enhancements: Encircling Horrors x2, Cryptophotaic Camouflage x2", "list": "UNITS\nDeathleaper (80)\nBroodlord (80) + Genestealers x10 (140)\nBroodlord (80) + Genestealers x10 (140)\nBroodlord (80) + Genestealers x10 (150)\nHyperadapted Raveners x5 (165) + Raveners x5 (125)\nHyperadapted Raveners x5 (165) + Raveners x5 (125)\nNeurotyrant (115)\nGargoyles x10 (80)\nBiovores (60)\nLictor (60)\nNeurolictor (100) — Encircling Horrors\nNeurolictor (100) — Encircling Horrors\nVon Ryan’s Leapers x3 (70) — Cryptophotaic Camouflage\nVon Ryan’s Leapers x3 (70) — Cryptophotaic Camouflage"}];
const cards = document.querySelectorAll('.army-card');
const preview = document.getElementById('preview');
const panel = document.getElementById('armyPanel');
const panelTitle = document.getElementById('panelTitle');
const panelMeta = document.getElementById('panelMeta');
const panelList = document.getElementById('panelList');
const panelEmblem = document.getElementById('panelEmblem');

function openArmy(index) {
  const army = armies[index];
  panelTitle.textContent = army.title;
  panelMeta.textContent = `${army.faction}\n${army.meta}`;
  panelList.textContent = army.list;
  panelEmblem.textContent = army.faction.charAt(0);
  panel.classList.add('open');
  panel.setAttribute('aria-hidden','false');
}

cards.forEach(card => {
  const index = Number(card.dataset.index);
  const army = armies[index];

  card.addEventListener('click', () => openArmy(index));
  card.addEventListener('pointerenter', () => {
    preview.innerHTML = `<strong>${army.title}</strong><span>${army.faction}</span><small>${army.meta}</small>`;
    preview.style.display = 'block';
  });
  card.addEventListener('pointermove', event => {
    const gap = 16;
    const maxX = innerWidth - preview.offsetWidth - gap;
    const maxY = innerHeight - preview.offsetHeight - gap;
    preview.style.left = Math.max(gap,Math.min(event.clientX + gap,maxX)) + 'px';
    preview.style.top = Math.max(gap,Math.min(event.clientY + gap,maxY)) + 'px';
  });
  card.addEventListener('pointerleave', () => preview.style.display = 'none');
});

document.getElementById('panelClose').addEventListener('click', () => {
  panel.classList.remove('open');
  panel.setAttribute('aria-hidden','true');
});
document.addEventListener('keydown', event => {
  if(event.key === 'Escape') {
    panel.classList.remove('open');
    panel.setAttribute('aria-hidden','true');
  }
});

function cleanScore(input) {
  const cleaned = input.value.replace(/[^0-9]/g,'');
  if(cleaned !== input.value) input.value = cleaned;
  return Number(cleaned || 0);
}
function updateTotals() {
  const keelhaul = [...document.querySelectorAll('.keelhaul-score')]
    .reduce((sum,input) => sum + cleanScore(input),0);
  const xpz = [...document.querySelectorAll('.xpz-score')]
    .reduce((sum,input) => sum + cleanScore(input),0);
  document.getElementById('keelhaulTotal').textContent = keelhaul;
  document.getElementById('xpzTotal').textContent = xpz;
}
document.querySelectorAll('.score-input').forEach(input => input.addEventListener('input',updateTotals));
updateTotals();
</script>
</body>
</html>
