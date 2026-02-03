<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Valentine 💖</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <style>
    body {
      margin: 0;
      font-family: Arial, sans-serif;
      background: linear-gradient(135deg, #ff9a9e, #fad0c4);
      height: 100vh;
      display: flex;
      align-items: center;
      justify-content: center;
      overflow: hidden;
    }

    .card {
      background: white;
      padding: 30px;
      border-radius: 15px;
      text-align: center;
      box-shadow: 0 10px 30px rgba(0,0,0,0.2);
      max-width: 320px;
      width: 90%;
    }

    h1 {
      color: #ff4d6d;
      font-size: 22px;
    }

    button {
      margin: 12px;
      padding: 12px 20px;
      font-size: 18px;
      border: none;
      border-radius: 25px;
      cursor: pointer;
      transition: transform 0.3s;
    }

    .choice { background-color: #ffd6e0; }
    .yes { background-color: #ff4d6d; color: white; }
    .no { background-color: #ccc; }

    .hidden { display: none; }

    .message {
      font-size: 32px;
      color: white;
      display: none;
      text-align: center;
      z-index: 2;
    }

    .flowers {
      position: absolute;
      top: -50px;
      font-size: 30px;
      animation: fall linear infinite;
    }

    @keyframes fall {
      to { transform: translateY(110vh) rotate(360deg); }
    }
  </style>
</head>
<body>

  <!-- SONS -->
  <audio id="catSound" src="https://assets.mixkit.co/sfx/preview/mixkit-cat-meow-119.mp3"></audio>
  <audio id="crocSound" src="https://assets.mixkit.co/sfx/preview/mixkit-monster-mouth-bite-1961.mp3"></audio>
  <audio id="musicSound" src="https://assets.mixkit.co/sfx/preview/mixkit-fun-bell-287.mp3"></audio>
  <audio id="webSound" src="https://assets.mixkit.co/sfx/preview/mixkit-fast-zip-movement-1159.mp3"></audio>
  <audio id="noSound" src="https://assets.mixkit.co/sfx/preview/mixkit-wrong-answer-fail-notification-946.mp3"></audio>
  <audio id="yesSound" src="https://assets.mixkit.co/sfx/preview/mixkit-video-game-win-2016.mp3"></audio>

  <!-- Question 1 -->
  <div class="card" id="q1">
    <h1>Quel est ton animal préféré ? 🐾</h1>
    <button class="choice" onclick="play('catSound'); next('q1','q2')">LES CHATS 🐱</button>
    <button class="choice" onclick="play('crocSound'); next('q1','q2')">LES CROCODILES 🐊</button>
  </div>

  <!-- Question 2 -->
  <div class="card hidden" id="q2">
    <h1>Tu préfères quoi ? 🎬</h1>
    <button class="choice" onclick="play('musicSound'); next('q2','q3')">Mamma Mia 🎶</button>
    <button class="choice" onclick="play('webSound'); next('q2','q3')">Spider-Man 🕷️</button>
  </div>

  <!-- Question Valentine -->
  <div class="card hidden" id="q3">
    <h1>Est-ce que tu veux être ma Valentine ? 💖</h1>
    <button class="yes" id="yesBtn" onclick="yesAnswer()">Oui</button>
    <button class="no" id="noBtn" onclick="noAnswer()">Non</button>
  </div>

  <div class="message" id="message"></div>

  <script>
    let scale = 1;

    function play(id) {
      document.getElementById(id).play();
    }

    function next(current, next) {
      document.getElementById(current).classList.add("hidden");
      document.getElementById(next).classList.remove("hidden");
    }

    function noAnswer() {
      play('noSound');
      scale += 0.3;
      document.getElementById("yesBtn").style.transform = `scale(${scale})`;
      if (scale >= 2.2) document.getElementById("noBtn").style.display = "none";
    }

    function yesAnswer() {
      play('yesSound');
      document.getElementById("q3").style.display = "none";
      const msg = document.getElementById("message");
      msg.style.display = "block";
      msg.innerHTML = "Bonne réponse ,tu es donc ma valentine pour la vie ptit coeur💖🌸";

      for (let i = 0; i < 40; i++) createFlower();
    }

    function createFlower() {
      const f = document.createElement("div");
      f.className = "flowers";
      f.innerHTML = "🌸";
      f.style.left = Math.random() * 100 + "vw";
      f.style.animationDuration = (Math.random() * 3 + 2) + "s";
      document.body.appendChild(f);
      setTimeout(() => f.remove(), 5000);
    }
  </script>

</body>
</html>
