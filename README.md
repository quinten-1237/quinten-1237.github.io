<!DOCTYPE html>
<html lang="nl">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Raad de Persoon</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: #121212;
      color: white;
      text-align: center;
      margin: 0;
      padding: 0;
    }

    h1 {
      margin-top: 20px;
    }

    #startScreen {
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      height: 100vh;
      background: linear-gradient(135deg, #1e1e1e, #333);
      animation: fadeIn 1.5s ease-in;
    }

    #startButton {
      padding: 12px 25px;
      font-size: 18px;
      background-color: #ffcc00;
      border: none;
      border-radius: 12px;
      cursor: pointer;
      transition: transform 0.2s;
    }

    #startButton:hover {
      transform: scale(1.1);
    }

    #gameContainer {
      display: none;
      animation: fadeIn 1s ease-in;
    }

    #timer {
      font-size: 18px;
      margin-top: 5px;
      color: #ffcc00;
    }

    #scoreBar {
      font-size: 18px;
      color: #ffcc00;
      margin-top: 5px;
      margin-bottom: 10px;
      animation: fadeIn 0.5s ease-in;
    }

    #hintText {
      margin: 20px;
      font-size: 18px;
      color: #ffcc00;
      transition: opacity 0.5s;
    }

    #hintText.fade {
      opacity: 0;
    }

    #leaderboardContainer {
      display: none;
      background: rgba(0, 0, 0, 0.8);
      padding: 20px;
      border-radius: 20px;
      width: 350px;
      text-align: center;
      margin: 50px auto;
      color: #fff;
      animation: fadeIn 1s ease-in;
    }

    #leaderboardList {
      list-style: none;
      padding: 0;
      text-align: left;
    }

    #leaderboardList li {
      margin: 6px 0;
      padding: 6px 10px;
      background: #222;
      border-radius: 10px;
    }

    #scoreForm input {
      padding: 8px;
      border-radius: 8px;
      border: none;
      outline: none;
      width: 60%;
    }

    #scoreForm button {
      padding: 8px 10px;
      border: none;
      background-color: #ffcc00;
      color: #000;
      border-radius: 8px;
      cursor: pointer;
      font-weight: bold;
    }

    #restartButton {
      margin-top: 15px;
      padding: 10px 15px;
      background-color: #4caf50;
      color: white;
      border: none;
      border-radius: 8px;
      cursor: pointer;
    }

    @keyframes fadeIn {
      from { opacity: 0; }
      to { opacity: 1; }
    }
  </style>
</head>
<body>

  <div id="startScreen">
    <h1>🎮 Raad de Persoon</h1>
    <button id="startButton">Start het spel</button>
  </div>

  <div id="gameContainer">
    <h1>🔍 Raad de Persoon</h1>
    <div id="timer">⏱️ Tijd: 0:00</div>
    <div id="scoreBar">🎯 Pogingen: <span id="pogingenDisplay">0</span></div>

    <div id="hintText">Typ een naam om te beginnen!</div>
    <input type="text" id="guessInput" placeholder="Typ hier een naam..." />
    <button id="guessButton">Raden</button>

    <div id="personImageContainer">
      <img id="personImage" style="display:none; margin-top:20px; border-radius:10px; max-width:200px;">
    </div>
  </div>

  <div id="leaderboardContainer">
    <h2>🏆 Leaderboard</h2>
    <form id="scoreForm">
      <input type="text" id="playerName" placeholder="Jouw naam" required />
      <button type="submit">💾 Opslaan</button>
    </form>
    <ol id="leaderboardList"></ol>
    <button id="restartButton">🔁 Opnieuw spelen</button>
  </div>

  <script>
    const personen = [
      { naam: "Elon Musk", hints: ["SpaceX", "Tesla", "Twitter"], afbeelding: "https://upload.wikimedia.org/wikipedia/commons/e/ed/Elon_Musk_Royal_Society_%28crop2%29.jpg" },
      { naam: "Taylor Swift", hints: ["Zangeres", "Pop", "Eras Tour"], afbeelding: "https://upload.wikimedia.org/wikipedia/commons/f/f2/Taylor_Swift_2_-_2019_by_Glenn_Francis.jpg" },
      { naam: "Barack Obama", hints: ["President", "VS", "Michelle"], afbeelding: "https://upload.wikimedia.org/wikipedia/commons/8/8d/President_Barack_Obama.jpg" }
    ];

    let doelPersoon;
    let pogingen = 0;
    let hintIndex = 0;
    let startTime;
    let timerInterval;

    function startSpel() {
      document.getElementById("startScreen").style.display = "none";
      document.getElementById("leaderboardContainer").style.display = "none";
      document.getElementById("gameContainer").style.display = "block";

      doelPersoon = personen[Math.floor(Math.random() * personen.length)];
      pogingen = 0;
      hintIndex = 0;
      document.getElementById("hintText").textContent = "Typ een naam om te beginnen!";
      document.getElementById("personImage").style.display = "none";
      document.getElementById("pogingenDisplay").textContent = 0;
      document.getElementById("guessInput").value = "";

      startTimer();
    }

    function startTimer() {
      startTime = new Date();
      timerInterval = setInterval(updateTimer, 1000);
    }

    function updateTimer() {
      const now = new Date();
      const diff = Math.floor((now - startTime) / 1000);
      const minuten = Math.floor(diff / 60);
      const seconden = diff % 60;
      document.getElementById("timer").textContent = `⏱️ Tijd: ${minuten}:${seconden.toString().padStart(2, "0")}`;
    }

    function stopTimer() {
      clearInterval(timerInterval);
      return Math.floor((new Date() - startTime) / 1000);
    }

    function checkGuess() {
      const guess = document.getElementById("guessInput").value.trim().toLowerCase();
      if (!guess) return;

      pogingen++;
      document.getElementById("pogingenDisplay").textContent = pogingen;

      const gevonden = personen.find(p => p.naam.toLowerCase() === guess);
      if (gevonden && gevonden.naam.toLowerCase() === doelPersoon.naam.toLowerCase()) {
        const hintText = document.getElementById("hintText");
        const totaleTijd = stopTimer();
        const minuten = Math.floor(totaleTijd / 60);
        const seconden = totaleTijd % 60;

        hintText.classList.add("fade");

        setTimeout(() => {
          hintText.textContent = `✅ Juist! Het was ${doelPersoon.naam}! 🎯 Je deed er ${pogingen} pogingen over en ${minuten}:${seconden.toString().padStart(2, "0")} minuten.`;
          hintText.classList.remove("fade");
        }, 300);

        toonAfbeelding();

        setTimeout(() => toonLeaderboard(totaleTijd, pogingen), 2000);
      } else {
        geefHint();
      }
    }

    function geefHint() {
      const hintText = document.getElementById("hintText");
      if (hintIndex < doelPersoon.hints.length) {
        hintText.textContent = "💡 Hint: " + doelPersoon.hints[hintIndex];
        hintIndex++;
      } else {
        hintText.textContent = "😅 Geen hints meer!";
      }
    }

    function toonAfbeelding() {
      const img = document.getElementById("personImage");
      img.src = doelPersoon.afbeelding;
      img.style.display = "block";
    }

    // ------------------ LEADERBOARD ------------------
    function toonLeaderboard(tijd, pogingen) {
      document.getElementById("gameContainer").style.display = "none";
      document.getElementById("leaderboardContainer").style.display = "block";

      document.getElementById("scoreForm").dataset.tijd = tijd;
      document.getElementById("scoreForm").dataset.pogingen = pogingen;
      updateLeaderboard();
    }

    function updateLeaderboard() {
      const leaderboardList = document.getElementById("leaderboardList");
      leaderboardList.innerHTML = "";

      const scores = JSON.parse(localStorage.getItem("leaderboard")) || [];
      scores.sort((a, b) => a.tijd - b.tijd)
        .slice(0, 10)
        .forEach((score, index) => {
          const li = document.createElement("li");
          li.textContent = `${index + 1}. ${score.naam} — ⏱️ ${score.min}:${score.sec.toString().padStart(2, "0")} — 🎯 ${score.pogingen} pogingen`;
          leaderboardList.appendChild(li);
        });
    }

    document.getElementById("scoreForm").addEventListener("submit", (e) => {
      e.preventDefault();
      const naam = document.getElementById("playerName").value.trim();
      if (!naam) return;

      const tijd = parseInt(e.target.dataset.tijd);
      const pogingen = parseInt(e.target.dataset.pogingen);
      const min = Math.floor(tijd / 60);
      const sec = tijd % 60;

      const newScore = { naam, tijd, min, sec, pogingen };
      const scores = JSON.parse(localStorage.getItem("leaderboard")) || [];
      scores.push(newScore);
      localStorage.setItem("leaderboard", JSON.stringify(scores));

      document.getElementById("playerName").value = "";
      updateLeaderboard();
    });

    document.getElementById("restartButton").addEventListener("click", () => {
      document.getElementById("leaderboardContainer").style.display = "none";
      document.getElementById("startScreen").style.display = "flex";
    });

    // ------------------ EVENT LISTENERS ------------------
    document.getElementById("startButton").addEventListener("click", startSpel);
    document.getElementById("guessButton").addEventListener("click", checkGuess);
    document.getElementById("guessInput").addEventListener("keypress", (e) => {
      if (e.key === "Enter") checkGuess();
    });
  </script>
</body>
</html>

