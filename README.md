<!doctype html>
<html lang="fr">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>ALIBI CAR — Complicité (Final)</title>
  <style>
    :root{
      --bg:#05080a; --line:#1b2a31;
      --text:#e7f1f3; --muted:#9bb0b7;
      --green:#25ff8b; --red:#ff4040;
      --mono: ui-monospace, SFMono-Regular, Menlo, Monaco, Consolas, "Liberation Mono","Courier New", monospace;
      --sans: ui-sans-serif, system-ui, -apple-system, Segoe UI, Roboto, Arial, sans-serif;
      --radius:16px; --shadow: 0 10px 28px rgba(0,0,0,.45);
    }
    *{ box-sizing:border-box; }
    body{
      margin:0;
      background: radial-gradient(1200px 800px at 15% 0%, #0a141a 0%, var(--bg) 55%) fixed;
      color:var(--text);
      font-family: var(--sans);
    }
    .wrap{ max-width: 980px; margin: 0 auto; padding: 16px 12px 34px; }
    .top{ display:flex; align-items:center; justify-content:space-between; gap:10px; margin-bottom: 12px; }
    .tag{
      border:1px solid var(--line);
      background: linear-gradient(180deg, #0c171c, #070c0f);
      padding:8px 10px; border-radius:999px; box-shadow: var(--shadow);
      white-space:nowrap; font-family: var(--mono); letter-spacing:.08em; text-transform:uppercase; font-size:12px; color:var(--muted);
    }
    .grid{ display:grid; grid-template-columns: 1.1fr .9fr; gap:12px; }
    @media (max-width: 900px){ .grid{ grid-template-columns: 1fr; } }
    .card{
      border:1px solid var(--line);
      background: linear-gradient(180deg, rgba(12,23,29,.92), rgba(9,16,20,.92));
      border-radius: var(--radius);
      box-shadow: var(--shadow);
      overflow:hidden;
    }
    .card h2{
      margin:0; padding:12px 12px 10px;
      font-family: var(--mono);
      color: var(--muted);
      font-size: 13px;
      letter-spacing:.07em;
      text-transform:uppercase;
      border-bottom:1px solid var(--line);
      background: linear-gradient(180deg, rgba(12,23,28,.9), rgba(8,13,16,.9));
    }
    .content{ padding:12px; }
    .row{ display:flex; gap:10px; flex-wrap:wrap; align-items:center; }
    .row > *{ flex: 1; min-width: 160px; }
    label{
      display:block; margin-bottom:6px;
      font-family: var(--mono); color: var(--muted);
      font-size: 12px; letter-spacing:.02em;
    }
    select{
      width:100%;
      padding:10px 10px;
      border-radius: 12px;
      border:1px solid var(--line);
      background: rgba(6,9,11,.7);
      color: var(--text);
      outline:none;
      font-size: 14px;
    }
    .btns{ display:flex; gap:10px; flex-wrap:wrap; margin-top:10px; }
    button{
      cursor:pointer;
      border-radius: 12px;
      border:1px solid var(--line);
      padding:10px 12px;
      background: rgba(10,18,22,.9);
      color: var(--text);
      font-family: var(--mono);
      font-weight: 800;
      letter-spacing:.02em;
    }
    button.primary{ border-color: rgba(37,255,139,.35); box-shadow: 0 0 0 2px rgba(37,255,139,.07); }
    button.danger{ border-color: rgba(255,64,64,.35); box-shadow: 0 0 0 2px rgba(255,64,64,.06); }
    button:disabled{ opacity:.45; cursor:not-allowed; }
    .box{
      border:1px dashed rgba(155,176,183,.35);
      border-radius: 14px;
      padding: 12px;
      background: rgba(0,0,0,.18);
      white-space: pre-wrap;
    }
    .hint{ color: var(--muted); font-size: 13px; margin: 10px 0 0; }
    .divider{ height:1px; background: var(--line); margin: 10px 0; }
    .timer{
      font-family: var(--mono);
      font-size: 44px;
      letter-spacing:.06em;
      text-align:center;
      color: var(--green);
      text-shadow: 0 0 18px rgba(37,255,139,.18);
      margin: 6px 0 8px;
    }
    .hidden{ display:none !important; }
    .score{
      display:flex; gap:10px; flex-wrap:wrap; align-items:center; justify-content:space-between;
      border:1px solid var(--line);
      border-radius: 14px;
      padding: 10px 12px;
      background: rgba(0,0,0,.18);
      font-family: var(--mono);
    }
    .score strong{ color: var(--green); font-size: 20px; }
    .kbd{
      font-family: var(--mono);
      border:1px solid var(--line);
      border-radius: 10px;
      padding: 2px 8px;
      color: var(--muted);
      background: rgba(0,0,0,.12);
      font-size: 12px;
      white-space:nowrap;
    }
    .qbox{
      border:1px solid var(--line);
      border-radius: 14px;
      padding: 12px;
      background: rgba(0,0,0,.16);
    }
    .qhead{
      display:flex; justify-content:space-between; gap:10px;
      color: var(--muted);
      font-family: var(--mono);
      font-size: 12px;
      margin-bottom: 8px;
      letter-spacing:.02em;
    }
    .qtext{ font-size: 18px; line-height: 1.25; font-weight: 800; }
  </style>
</head>

<body>
  <div class="wrap">
    <div class="top">
      <div class="tag" id="sessionTag">SESSION: —</div>
      <div class="tag" id="roundTag">MANCHE: 1</div>
    </div>

    <div class="grid">
      <div class="card">
        <h2>Contrôle</h2>
        <div class="content">

          <div id="stepSetup">
            <div class="row">
              <div>
                <label>Manche</label>
                <select id="roundSelect">
                  <option value="1">Manche 1 — Grand scénario</option>
                  <option value="2">Manche 2 — Grand scénario</option>
                  <option value="3">Manche 3 — Grand scénario</option>
                  <option value="4">Manche 4 — Grand scénario</option>
                  <option value="5">Manche 5 — Surprise</option>
                  <option value="6">Manche 6 — Surprise</option>
                </select>
              </div>
              <div>
                <label>Lecture (grand scénario)</label>
                <select id="readTimeSelect">
                  <option value="75">75s</option>
                  <option value="90" selected>90s</option>
                  <option value="120">120s</option>
                </select>
              </div>
            </div>

            <div class="divider"></div>

            <label>Scénario / Contexte</label>
            <div class="box" id="scenarioBox">Clique “Générer”.</div>

            <div class="btns">
              <button class="primary" id="btnGenerate">Générer</button>
              <button id="btnStart">Démarrer</button>
              <button class="danger" id="btnReset">Reset</button>
            </div>

            <p class="hint">
              Règle importante : suspects ne regardent pas l’écran pendant les questions. Réponse : “3,2,1, maintenant” +5sec pour repondre = eliminer.
            </p>
          </div>

          <div id="stepTimer" class="hidden">
            <div class="timer" id="timer">01:30</div>

            <label>Scénario</label>
            <div class="box" id="scenarioLive"></div>

            <div class="btns">
              <button class="danger" id="btnStopTimer">Stop</button>
            </div>
            <p class="hint">Après la lecture, interrogatoire.</p>
          </div>

          <div id="stepInterro" class="hidden">
            <div class="score">
              <span>Score: <strong id="score">0</strong>/10</span>
              <span>Q: <span class="kbd" id="qIndex">1/10</span></span>
            </div>

            <div class="divider"></div>

            <div class="qbox">
              <div class="qhead">
                <span id="qType">—</span>
                <span class="kbd">point / pas point</span>
              </div>
              <div class="qtext" id="qText">—</div>
            </div>

            <div class="btns" style="margin-top:12px;">
              <button class="primary" id="btnPoint">POINT</button>
              <button class="danger" id="btnNoPoint">PAS POINT</button>
              <button id="btnPrev">Précédent</button>
            </div>

            <div class="divider"></div>

            <div class="btns">
              <button class="primary" id="btnFinish">Finir la manche</button>
            </div>
          </div>

          <div id="stepEnd" class="hidden">
            <div class="score">
              <span>Score final: <strong id="finalScore">0</strong>/10</span>
              <span id="verdict" class="kbd">—</span>
            </div>

            <div class="divider"></div>

            <label>Récap (questions)</label>
            <div class="box" id="recapBox">—</div>

            <div class="btns">
              <button class="primary" id="btnNext">Manche suivante</button>
              <button class="danger" id="btnHardReset">Reset total</button>
            </div>
          </div>

        </div>
      </div>

      <div class="card">
        <h2>Règles rapides</h2>
        <div class="content">
          <div class="box" style="font-family:var(--mono);">
Règles du jeu — ALIBI

1.Composition des équipes
Le jeu se joue à 4 joueurs.
Les joueurs se divisent en 2 duos.
Exemple :
Duo 1 : Joueur A + Joueur B
Duo 2 : Joueur C + Joueur D
Chaque duo joue à tour de rôle.

2.Objectif du jeu
Le but est simple :
👉 répondre exactement la même chose que son partenaire.
Les deux joueurs doivent répondre en même temps aux questions de l’inspecteur.

Si les réponses sont suffisamment similaires, l’équipe gagne 1 point.

⚠️ Ce n’est pas un jeu de mémoire.
C’est un jeu de complicité et de logique commune.

3.Déroulement d’une manche
Une manche se déroule en trois phases :
a. Lecture du scénario
Les deux joueurs du duo lisent ensemble le scénario.
Le scénario décrit une situation générale, mais beaucoup de détails ne sont pas précisés.

Les joueurs doivent imaginer ensemble les détails de l’histoire.

Ils ont un temps limité pour se mettre d’accord.

b. Interrogatoire
Après la lecture :
Les joueurs retournent avec les autres.
Les inspecteurs (l’autre duo) posent 10 questions.
Les deux joueurs interrogés doivent répondre :
👉 à voix haute
👉 en même temps
👉 après le signal :

“3… 2… 1… maintenant.”

c. Attribution des points
Après chaque question, les inspecteurs décident :
POINT → les réponses sont suffisamment similaires
PAS POINT → les réponses sont différentes
Il n’y a pas de débat long.
Les inspecteurs prennent la décision rapidement.

4.Les types de manches
Le jeu comporte 6 manches :
🎭 Manches 1 à 4 — Scénarios principaux
Un grand scénario est donné.
Les joueurs ont un temps de lecture pour imaginer leur version.
Les inspecteurs posent ensuite 10 questions.
⚡ Manches 5 et 6 — Scénarios surprise
Un contexte court est donné.
Les joueurs n’ont pas de temps pour préparer.
Les questions arrivent immédiatement.

5.Règles importantes
❌ Pas de communication pendant l’interrogatoire
Les deux joueurs ne doivent pas discuter entre les questions.
❌ Pas de regard vers l’écran pendant les questions
Les joueurs interrogés ne doivent pas voir les questions à l’avance.
⏱ Réponses simultanées
Les deux joueurs doivent répondre exactement au même moment.
Si l’un répond après l’autre :

👉 PAS POINT

⚖️ Décision des inspecteurs
Les inspecteurs jugent si les réponses sont :
assez proches → POINT
différentes → PAS POINT
Exemple :
“resto” et “restaurant” → POINT
“pizza” et “burger” → PAS POINT

6.Score
Chaque manche comporte 10 questions.
Score possible :

8 à 10 points → Complicité excellente
5 à 7 points → Bonne complicité
0 à 4 points → sah c'est quoi ce duo de merde

7.Victoire
Après que les deux duos ont joué, on compare les scores.
👉 Le duo avec le plus de points gagne la manche.

8.Conseil
Ne cherchez pas la réponse parfaite.
Cherchez la même réponse que votre partenaire.






          </div>
        </div>
      </div>
    </div>
  </div>

<script>
(() => {
  const $ = (id) => document.getElementById(id);

  function pad2(n){ return String(n).padStart(2,"0"); }
  function uid(){ return "ALB-" + Math.random().toString(16).slice(2,6).toUpperCase() + "-" + Math.random().toString(16).slice(2,6).toUpperCase(); }

  // ====== TES SCÉNARIOS (inchangés) + NOUVELLES QUESTIONS ======
  const rounds = {
    1: {
      title: "🎭 Scénario 1 — Le mariage qui a tourné au chaos",
      scenario: `Contexte pour les joueurs
Vous étiez invités au mariage d’un ami proche. La cérémonie se déroulait dans une grande salle louée pour l’occasion, avec un jardin à l’extérieur pour le cocktail.
Vous êtes arrivés ensemble au début de l’après-midi. À votre arrivée, les invités commençaient déjà à discuter et à prendre des photos avec les mariés.
La cérémonie s’est déroulée normalement et tout le monde est ensuite sorti dans le jardin pour le cocktail. Il y avait de la musique, plusieurs tables avec des boissons et des petits plats.
Après le cocktail, les invités sont entrés dans la salle principale pour le dîner. Vous étiez assis à une table avec d’autres invités que vous ne connaissiez pas très bien. Le repas a commencé normalement mais un événement inattendu s’est produit pendant le dîner.
Cet incident a complètement changé l’ambiance du mariage et beaucoup d’invités ont commencé à en parler. Certains étaient choqués, d’autres trouvaient la situation plutôt drôle.
Après cet événement, la soirée a continué mais l’ambiance n’était plus tout à fait la même. Certains invités sont restés pour la soirée dansante, d’autres sont partis plus tôt.
Vous êtes restés encore un moment avant de finalement quitter le mariage.`,
      questions: [
        {type:"INVITATION", text:"Qui vous a invités à ce mariage ?"},
        {type:"ARRIVÉE", text:"À votre arrivée, vous êtes allés où en premier dans le lieu du mariage ?"},
        {type:"COCKTAIL", text:"Pendant le cocktail dans le jardin, qu’est-ce que vous faisiez surtout ?"},
        {type:"PLACEMENT", text:"Pendant le dîner, vous étiez assis plutôt près, au milieu, ou au fond de la salle ?"},
        {type:"AVANT", text:"Quel détail vous a marqué juste avant que l’incident arrive ?"},
        {type:"INCIDENT", text:"L’incident concernait plutôt une personne, un objet, ou une situation ?"},
        {type:"RÉACTION", text:"Qui a réagi en premier autour de vous ?"},
        {type:"APRÈS", text:"Qu’est-ce que vous avez fait juste après l’incident ?"},
        {type:"SUITE", text:"Après le dîner, vous êtes restés plutôt à l’intérieur ou à l’extérieur ?"},
        {type:"AMBIANCE", text:"Quand vous êtes partis, l’ambiance était plutôt tendue, drôle, ou normale ?"},
      ]
    },

    2: {
      title: "🎭 Scénario 2 — La panne en pleine nuit",
      scenario: `Contexte
Vous deviez faire un trajet en voiture pour vous rendre dans une autre ville. Le trajet devait durer environ deux heures.
Vous êtes partis en fin de soirée, pensant qu’il y aurait moins de circulation.
Au début du trajet tout se passait normalement. Vous écoutiez de la musique et discutiez pendant que la route avançait tranquillement.
Après environ une heure de route, vous avez commencé à remarquer que quelque chose n’allait pas avec la voiture. Un bruit étrange ou un voyant s’est allumé.
Vous avez décidé de continuer encore un peu pour voir si le problème disparaissait, mais quelques minutes plus tard le problème est devenu plus sérieux.
Vous avez donc dû vous arrêter sur le côté de la route pour regarder ce qu’il se passait. L’endroit n’était pas très rassurant car il faisait nuit et il n’y avait pas beaucoup de voitures autour.
Vous avez essayé de comprendre d’où venait le problème et vous avez réfléchi à ce que vous pouviez faire : réparer, appeler quelqu’un ou chercher de l’aide.
Finalement la situation s’est réglée d’une manière ou d’une autre et vous avez pu reprendre votre route.`,
      questions: [
        {type:"RAISON", text:"Pourquoi vous faisiez ce trajet en voiture ?"},
        {type:"CONDUITE", text:"Qui conduisait au début du trajet ?"},
        {type:"SIGNE", text:"Qu’est-ce qui vous a fait comprendre que la voiture avait un problème ?"},
        {type:"ARRÊT", text:"Quand vous vous êtes arrêtés, vous étiez plutôt sur une route, une aire, ou un parking ?"},
        {type:"SORTIE", text:"Qui est sorti de la voiture en premier ?"},
        {type:"ACTION", text:"La première chose que vous avez faite pour vérifier le problème ?"},
        {type:"LIEU", text:"L’endroit vous paraissait plutôt isolé ou fréquenté ?"},
        {type:"SOLUTION", text:"Comment la situation s’est finalement réglée ?"},
        {type:"RESSENTI", text:"Après avoir redémarré, vous étiez plutôt rassurés ou encore stressés ?"},
        {type:"SUJET", text:"Pendant le reste du trajet, vous parliez encore de la panne ou vous avez changé de sujet ?"},
      ]
    },

    3: {
      title: "🎭 Scénario 3 — La soirée d’anniversaire qui dégénère",
      scenario: `Contexte
Vous étiez invités à une soirée d’anniversaire chez un ami. La soirée se passait dans un appartement assez grand avec plusieurs pièces.
Quand vous êtes arrivés, la musique jouait déjà et plusieurs personnes discutaient dans le salon pendant que d’autres étaient dans la cuisine.
Au début l’ambiance était détendue. Les gens parlaient, mangeaient, buvaient un verre et certains jouaient à des jeux.
Plus tard dans la soirée, la musique est devenue plus forte et plus de personnes sont arrivées. L’appartement était presque plein.
À un moment donné, une situation étrange ou inattendue s’est produite entre plusieurs invités. La tension est montée et certaines personnes ont commencé à intervenir.
La situation a attiré l’attention de presque toute la soirée et tout le monde a arrêté ce qu’il faisait pour regarder ce qu’il se passait.
Après quelques minutes la situation s’est calmée, mais l’ambiance de la soirée avait clairement changé.
Certains invités ont décidé de partir peu après cet événement tandis que d’autres sont restés encore un moment.
Vous avez fini par quitter la soirée vous aussi.`,
      questions: [
        {type:"HÔTE", text:"Chez qui se passait la soirée ?"},
        {type:"ARRIVÉE", text:"En arrivant dans l’appartement, vous êtes allés dans quelle pièce en premier ?"},
        {type:"DÉBUT", text:"Au début de la soirée, vous faisiez quoi ?"},
        {type:"MONDE", text:"Quand l’appartement s’est rempli, vous étiez plutôt dans le salon, la cuisine, ou ailleurs ?"},
        {type:"DÉCLENCHEUR", text:"Qu’est-ce qui a déclenché le problème pendant la soirée ?"},
        {type:"CALMER", text:"Qui a essayé de calmer la situation en premier ?"},
        {type:"RÉACTION", text:"Les invités autour de vous ont plutôt regardé, intervenu, ou rigolé ?"},
        {type:"APRÈS", text:"Après que la situation s’est calmée, vous êtes restés dans la même pièce ou vous avez bougé ?"},
        {type:"TEMPS", text:"Combien de temps environ vous êtes restés après cet événement ?"},
        {type:"FIN", text:"Quand vous êtes partis, la soirée continuait ou beaucoup de gens partaient aussi ?"},
      ]
    },

    4: {
      title: "🎭 Scénario 4 — La journée au parc d’attractions",
      scenario: `Contexte
Vous avez décidé de passer la journée dans un parc d’attractions. Vous êtes arrivés le matin quand le parc venait d’ouvrir.
Au début il n’y avait pas beaucoup de monde et vous avez pu faire plusieurs attractions assez rapidement.
Vous avez ensuite pris le temps de vous promener dans le parc, de regarder certaines boutiques et de manger quelque chose vers le milieu de la journée.
Après le repas vous avez décidé de faire les attractions les plus populaires du parc, même si les files d’attente étaient plus longues.
À un moment de la journée quelque chose d’inhabituel s’est produit dans une attraction ou dans le parc, ce qui a attiré l’attention de beaucoup de visiteurs.
Vous avez continué votre journée après cet événement et vous avez fait encore quelques attractions avant la fermeture du parc.
Finalement vous avez quitté le parc en fin de journée.`,
      questions: [
        {type:"ENTRÉE", text:"Quelle a été la première chose que vous avez faite en entrant dans le parc ?"},
        {type:"1ÈRE", text:"Votre première attraction était plutôt forte, familiale, ou tranquille ?"},
        {type:"MATIN", text:"Dans la matinée, vous avez fait plusieurs attractions ou vous vous êtes surtout promenés ?"},
        {type:"REPAS", text:"Où vous avez décidé de manger dans le parc ?"},
        {type:"PLACE", text:"Pendant le repas, vous étiez assis plutôt dedans ou dehors ?"},
        {type:"INCIDENT", text:"L’événement inhabituel concernait plutôt une attraction, un visiteur, ou le parc lui-même ?"},
        {type:"RÉACTION", text:"Comment les visiteurs autour de vous ont réagi à cet événement ?"},
        {type:"APRÈS", text:"Après cet incident, vous avez continué les attractions ou vous avez fait une pause ?"},
        {type:"DERNIÈRE", text:"La dernière attraction de la journée était plutôt calme ou à sensations ?"},
        {type:"SORTIE", text:"En quittant le parc, vous étiez plutôt fatigués, contents, ou surpris par la journée ?"},
      ]
    },

    5: {
      title: "⚡ Scénario surprise 1 — Le pique-nique improvisé",
      scenario: `Contexte
Il faisait beau et vous avez décidé au dernier moment d’aller faire un pique-nique dans un parc.
Avant d’y aller, vous êtes passés dans un petit magasin pour acheter de quoi manger et boire.
Une fois dans le parc, vous avez marché un peu pour trouver un endroit tranquille.
Vous vous êtes installés dans l’herbe pour manger et discuter tout en regardant les gens passer.`,
      questions: [
        {type:"IDÉE", text:"Qui a proposé l’idée du pique-nique ?"},
        {type:"MAGASIN", text:"Dans quel type de magasin vous êtes passés avant le parc ?"},
        {type:"MANGER", text:"Qu’est-ce que vous avez acheté à manger ?"},
        {type:"BOIRE", text:"Qu’est-ce que vous avez pris à boire ?"},
        {type:"ENDROIT", text:"Dans le parc, vous vous êtes installés plutôt au soleil ou à l’ombre ?"},
        {type:"ASSIS", text:"Vous étiez assis sur quoi ?"},
        {type:"SACS", text:"Qui s’est occupé de sortir la nourriture ?"},
        {type:"PENDANT", text:"Pendant le pique-nique, vous regardiez plutôt les gens passer ou vous discutiez entre vous ?"},
        {type:"MONDE", text:"L’endroit était plutôt calme ou avec beaucoup de monde ?"},
        {type:"APRÈS", text:"Après avoir fini de manger, vous comptiez faire quoi ?"},
      ]
    },

    6: {
      title: "⚡ Scénario surprise 2 — L’attente au cinéma",
      scenario: `Contexte
Vous êtes arrivés au cinéma pour voir un film.
Quand vous êtes arrivés, la séance n’avait pas encore commencé et il restait encore du temps avant l’ouverture de la salle.
Vous avez donc attendu dans le hall du cinéma.
Vous avez regardé les affiches des films, discuté un peu et peut-être acheté quelque chose à manger ou à boire.`,
      questions: [
        {type:"GENRE", text:"Quel genre de film vous êtes venus voir ?"},
        {type:"CHOIX", text:"Qui a choisi ce film ?"},
        {type:"ATTENTE", text:"Combien de temps environ vous deviez attendre avant l’ouverture de la salle ?"},
        {type:"LIEU", text:"Où vous attendiez dans le hall du cinéma ?"},
        {type:"ACTIVITÉ", text:"Pendant l’attente, vous faisiez quoi principalement ?"},
        {type:"ACHAT", text:"Est-ce que vous avez acheté quelque chose à manger ou boire ?"},
        {type:"BILLETS", text:"Qui s’est occupé des billets ?"},
        {type:"MONDE", text:"Le hall du cinéma était plutôt plein ou tranquille ?"},
        {type:"ENTRÉE", text:"Quand la salle a ouvert, vous êtes entrés directement ou vous avez attendu un peu ?"},
        {type:"PLACEMENT", text:"Vos places dans la salle étaient plutôt devant, au milieu, ou au fond ?"},
      ]
    }
  };

  // ====== STATE ======
  let state = {
    sessionId: uid(),
    round: 1,
    scenarioText: "",
    questions: [],
    idx: 0,
    points: Array(10).fill(null),
    score: 0,
  };

  function updateTags(){
    $("sessionTag").textContent = "SESSION: " + state.sessionId;
    $("roundTag").textContent = "MANCHE: " + state.round;
    $("roundSelect").value = String(state.round);
  }

  function show(stepId){
    ["stepSetup","stepTimer","stepInterro","stepEnd"].forEach(id => $(id).classList.add("hidden"));
    $(stepId).classList.remove("hidden");
  }

  let timerHandle = null;
  function startTimer(seconds){
    let t = seconds;
    function tick(){
      const mm = Math.floor(t/60), ss = t%60;
      $("timer").textContent = `${pad2(mm)}:${pad2(ss)}`;
      if(t <= 0){ stopTimer(); return; }
      t--;
    }
    tick();
    timerHandle = setInterval(tick, 1000);
  }
  function stopTimer(){
    if(timerHandle){ clearInterval(timerHandle); timerHandle = null; }
    state.idx = 0;
    state.points = Array(10).fill(null);
    state.score = 0;
    show("stepInterro");
    renderQuestion();
  }

  function recalcScore(){
    state.score = state.points.reduce((acc, v) => acc + (v === true ? 1 : 0), 0);
    $("score").textContent = String(state.score);
    $("qIndex").textContent = `${state.idx+1}/10`;
  }

  function renderQuestion(){
    const q = state.questions[state.idx];
    $("qType").textContent = q.type;
    $("qText").textContent = `Q${q.n}. ${q.text}`;
    recalcScore();
  }

  function setPoint(val){
    state.points[state.idx] = val;
    if(state.idx < 9){
      state.idx++;
      renderQuestion();
    } else {
      recalcScore();
    }
  }

  function verdictText(score){
    if(score >= 8) return "Complicité solide.";
    if(score >= 5) return "Ça tient… mais fragile.";
    return "Alibi éclaté.";
  }

  function recap(){
    const lines = [];
    lines.push(`MANCHE ${state.round} — SCORE ${state.score}/10`);
    lines.push("");
    state.questions.forEach((q,i)=>{
      const p = state.points[i] === true ? "POINT" : (state.points[i] === false ? "0" : "?");
      lines.push(`Q${i+1} [${p}] ${q.text}`);
    });
    return lines.join("\n");
  }

  function generateRound(){
    const r = state.round;
    const pack = rounds[r];

    $("scenarioBox").textContent = pack.title + "\n\n" + pack.scenario;

    state.scenarioText = pack.title + "\n\n" + pack.scenario;
    state.questions = pack.questions.map((q,i)=>({n:i+1, ...q}));

    state.idx = 0;
    state.points = Array(10).fill(null);
    state.score = 0;
  }

  // ====== EVENTS ======
  $("roundSelect").addEventListener("change",(e)=>{
    state.round = parseInt(e.target.value,10);
    updateTags();
    generateRound();
    show("stepSetup");
  });

  $("btnGenerate").addEventListener("click", ()=>{
    generateRound();
  });

  $("btnStart").addEventListener("click", ()=>{
    if(!state.scenarioText) generateRound();

    if(state.round >= 1 && state.round <= 4){
      const seconds = parseInt($("readTimeSelect").value, 10);
      $("scenarioLive").textContent = state.scenarioText;
      show("stepTimer");
      startTimer(seconds);
      return;
    }

    // surprises: contexte affiché puis direct questions
    show("stepInterro");
    state.idx = 0;
    state.points = Array(10).fill(null);
    state.score = 0;
    renderQuestion();
  });

  $("btnStopTimer").addEventListener("click", ()=> stopTimer());

  $("btnPoint").addEventListener("click", ()=> setPoint(true));
  $("btnNoPoint").addEventListener("click", ()=> setPoint(false));

  $("btnPrev").addEventListener("click", ()=>{
    if(state.idx > 0){
      state.idx--;
      renderQuestion();
    }
  });

  $("btnFinish").addEventListener("click", ()=>{
    recalcScore();
    $("finalScore").textContent = String(state.score);
    $("verdict").textContent = verdictText(state.score);
    $("recapBox").textContent = recap();
    show("stepEnd");
  });

  $("btnNext").addEventListener("click", ()=>{
    state.sessionId = uid();
    state.round = Math.min(6, state.round + 1);
    updateTags();
    generateRound();
    show("stepSetup");
  });

  function hardReset(){
    state.sessionId = uid();
    state.round = 1;
    updateTags();
    generateRound();
    show("stepSetup");
  }

  $("btnReset").addEventListener("click", hardReset);
  $("btnHardReset").addEventListener("click", hardReset);

  // INIT
  updateTags();
  generateRound();
  show("stepSetup");
})();
</script>
</body>
</html>
