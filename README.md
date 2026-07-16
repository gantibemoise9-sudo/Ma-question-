<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Une question pour toi 💌</title>
<style>
  :root{
    --rose-deep:#c2185b;
    --rose-mid:#f06292;
    --rose-light:#ffd9e6;
    --cream:#fff5f8;
    --gold:#e8b4bc;
  }
  *{box-sizing:border-box;}
  html,body{
    margin:0;
    height:100%;
    font-family:'Georgia', 'Iowan Old Style', serif;
    background:linear-gradient(160deg, var(--cream) 0%, var(--rose-light) 55%, #ffc1d9 100%);
    overflow:hidden;
    position:relative;
  }

  .heart{
    position:absolute;
    top:-10%;
    color:var(--rose-mid);
    opacity:0.55;
    animation:fall linear infinite;
    user-select:none;
    pointer-events:none;
  }
  @keyframes fall{
    to{ transform:translateY(115vh) rotate(360deg); }
  }

  .stage{
    position:relative;
    z-index:2;
    height:100%;
    display:flex;
    flex-direction:column;
    align-items:center;
    justify-content:center;
    text-align:center;
    padding:24px;
  }

  .eyebrow{
    letter-spacing:0.35em;
    text-transform:uppercase;
    font-size:0.7rem;
    color:var(--rose-deep);
    font-family:'Helvetica Neue', Arial, sans-serif;
    margin-bottom:14px;
    opacity:0.75;
  }

  h1{
    font-size:clamp(1.8rem, 6vw, 3rem);
    color:var(--rose-deep);
    margin:0 0 8px 0;
    font-weight:400;
    line-height:1.25;
  }
  h1 em{
    font-style:italic;
    color:#a4133c;
  }

  .sub{
    font-family:'Helvetica Neue', Arial, sans-serif;
    color:#8a4a5c;
    font-size:0.95rem;
    margin-bottom:44px;
    max-width:320px;
  }

  .btn-row{
    display:flex;
    gap:20px;
    align-items:center;
    justify-content:center;
    flex-wrap:wrap;
    min-height:80px;
  }

  button{
    border:none;
    border-radius:999px;
    font-family:'Helvetica Neue', Arial, sans-serif;
    font-weight:600;
    cursor:pointer;
    transition:transform 0.15s ease, box-shadow 0.15s ease, padding 0.15s ease, font-size 0.15s ease;
  }

  #yes{
    background:linear-gradient(135deg, var(--rose-deep), #ff477e);
    color:white;
    padding:18px 46px;
    font-size:1.05rem;
    box-shadow:0 10px 25px rgba(194, 24, 91, 0.35);
  }
  #yes:hover{
    transform:translateY(-2px) scale(1.04);
    box-shadow:0 14px 30px rgba(194, 24, 91, 0.45);
  }

  #no{
    background:white;
    color:var(--rose-deep);
    padding:18px 46px;
    font-size:1.05rem;
    border:1.5px solid var(--rose-mid);
  }

  .result{
    display:none;
    animation:pop 0.5s ease;
  }
  .result.show{ display:block; }
  @keyframes pop{
    0%{ transform:scale(0.6); opacity:0; }
    70%{ transform:scale(1.08); opacity:1; }
    100%{ transform:scale(1); }
  }
  .result h1{ margin-bottom:6px; }
  .result .sub{ margin-bottom:0; }

  .signature{
    position:absolute;
    bottom:18px;
    font-family:'Helvetica Neue', Arial, sans-serif;
    font-size:0.68rem;
    letter-spacing:0.15em;
    text-transform:uppercase;
    color:var(--rose-deep);
    opacity:0.5;
  }

  @media (prefers-reduced-motion: reduce){
    .heart{ animation:none; opacity:0.2; }
    #yes:hover{ transform:none; }
  }
</style>
</head>
<body>

<div class="stage">
  <div id="question">
    <p class="eyebrow">Une petite question</p>
    <h1>Est-ce que tu veux <em>être ma copine</em> ?</h1>
    <p class="sub">Prends ton temps... enfin, pas trop 🙂</p>
    <div class="btn-row">
      <button id="yes" onclick="sayYes()">Oui 💕</button>
      <button id="no" onclick="shrinkNo()">Non</button>
    </div>
  </div>

  <div class="result" id="result">
    <h1>Yes ! 🎉💗</h1>
    <p class="sub">Je savais que t'allais dire oui.</p>
  </div>
</div>

<div class="signature">fait avec 💗</div>

<script>
  // Coeurs qui tombent en fond
  const stage = document.body;
  const heartChars = ['♥','♡','❤'];
  for(let i=0;i<22;i++){
    const h = document.createElement('div');
    h.className = 'heart';
    h.textContent = heartChars[Math.floor(Math.random()*heartChars.length)];
    h.style.left = Math.random()*100 + 'vw';
    h.style.fontSize = (12 + Math.random()*22) + 'px';
    h.style.animationDuration = (8 + Math.random()*10) + 's';
    h.style.animationDelay = (Math.random()*10) + 's';
    stage.appendChild(h);
  }

  let noScale = 1;
  const noBtn = document.getElementById('no');
  const yesBtn = document.getElementById('yes');

  function shrinkNo(){
    noScale = Math.max(noScale - 0.18, 0.12);
    noBtn.style.transform = 'scale(' + noScale + ')';
    const yesScale = Math.min(1 + (1 - noScale) * 0.5, 1.6);
    yesBtn.style.transform = 'scale(' + yesScale + ')';
    if(noScale <= 0.15){
      noBtn.style.pointerEvents = 'none';
      noBtn.style.opacity = '0.3';
    }
  }

  function sayYes(){
    document.getElementById('question').style.display = 'none';
    document.getElementById('result').classList.add('show');
  }
</script>

</body>
</html>
