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
    const personen = [
  {
    naam: "Billy",
    geslacht: "Man",
    woonplaats: ["Tervuren"],
    hobby: ["Rugby"],
    verjaardag: "13/01",
    schoolrichting: "Latijn",
    hints: [
      "Unieke sport",
      "Loopt graag zonder broek rond",
      "Is pas sinds midden van het 4de studiejaar op het KAT"
    ],
    afbeelding: "Billy.jpg.jpg"
  },
  {
    naam: "Buyle",
    geslacht: "Man",
    woonplaats: ["Leuven"],
    hobby: ["Muziek"],
    verjaardag: "00/00",
    schoolrichting: "Geschiedenis",
    hints: [
      "Muziekmaker",
      "Union-fan",
      "Fan van koffie"
    ],
    afbeelding: "buyelen.jpg"
  },
  {
    naam: "Vranxc",
    geslacht: "Vrouw",
    woonplaats: ["Antwerpen"],
    hobby: ["Lezen"],
    verjaardag: "00/00",
    schoolrichting: "Nederlands",
    hints: [
      "Nederlands",
      "Bril",
      "Dochters en zonen"
    ],
    afbeelding: "vrancx.jpg"
  },
  {
    naam: "Elise",
    geslacht: "Vrouw",
    woonplaats: ["Meerbeek"],
    hobby: ["Lopen"],
    verjaardag: "00/00",
    schoolrichting: "Natuurwetenschappen",
    hints: [
      "Heeft een hond",
      "Lopen",
      "Burn-out"
    ],
    afbeelding: "eliese.jpg"
  },
  {
    naam: "Van Gijsel",
    geslacht: "Vrouw",
    woonplaats: ["Leuven"],
    hobby: ["Geen"],
    verjaardag: "00/00",
    schoolrichting: "OLC",
    hints: [
      "Heeft een dochter",
      "OLC",
      "Vroeger wiskundeleerkracht"
    ],
    afbeelding: "gijsel.jpg"
  },
  {
    naam: "Moriau",
    geslacht: "Vrouw",
    woonplaats: ["Tervuren"],
    hobby: ["Geen"],
    verjaardag: "00/00",
    schoolrichting: "Zedeleer",
    hints: [
      "Roept graag op eerste jaartjes",
      "Zedeleer",
      "Geeft les"
    ],
    afbeelding: "Moriau.jpg.jpg"
  },
  {
    naam: "Pontinha",
    geslacht: "Vrouw",
    woonplaats: ["Laken"],
    hobby: ["Geen"],
    verjaardag: "00/00",
    schoolrichting: "PO",
    hints: [
      "Kan niet zo goed Nederlands",
      "CR7",
      "Portugees"
    ],
    afbeelding: "Pontinha.jpg.jpg"
  },
  {
    naam: "Maxime",
    geslacht: "Man",
    woonplaats: ["Zaventem"],
    hobby: ["Geen"],
    verjaardag: "07/09",
    schoolrichting: "Economie",
    hints: [
      "Houdt van gamen",
      "Niet zo groot",
      "Allergisch aan alles"
    ],
    afbeelding: "Maxime.jpg.jpg"
  },
  {
    naam: "Ferdia",
    geslacht: "Man",
    woonplaats: ["Tervuren"],
    hobby: ["Fotograaf"],
    verjaardag: "21/06",
    schoolrichting: "Natuurwetenschappen",
    hints: [
      "Heeft een zus",
      "Raar gebouwd",
      "Een lange nek"
    ],
    afbeelding: "Ferdia.jpg.jpg"
  },
  {
    naam: "Mateo",
    geslacht: "Man",
    woonplaats: ["Moorsel"],
    hobby: ["Jeugdbeweging"],
    verjaardag: "09/09",
    schoolrichting: "Natuurwetenschappen",
    hints: [
      "Heeft een zus",
      "Maakt rare geluiden",
      "Legendarische bijnaam (P***)"
    ],
    afbeelding: "Mateo.jpg.jpg"
  },
  {
    naam: "Nico",
    geslacht: "Man",
    woonplaats: ["Tervuren"],
    hobby: ["Jeugdbeweging"],
    verjaardag: "23/11",
    schoolrichting: "Humane",
    hints: [
      "Kaas",
      "Heeft een bril",
      "Tweelingsbroer"
    ],
    afbeelding: "Nico.jpg.jpg"
  },
  {
    naam: "Paulussen",
    geslacht: "Man",
    woonplaats: ["Leuven"],
    hobby: ["Rare video's maken"],
    verjaardag: "00/00",
    schoolrichting: "Aardrijkskunde",
    hints: [
      "Koffiegeur",
      "Raar kapsel",
      "The GOAT in meerkeuze-examens"
    ],
    afbeelding: "Paulussen.jpg.jpg"
  },
  {
    naam: "Dennis",
    geslacht: "Man",
    woonplaats: ["Duisburg"],
    hobby: ["Gamen", "Jeugdbeweging"],
    verjaardag: "27/07",
    schoolrichting: "Economie",
    hints: [
      "Hij is blond",
      "Zit graag achter een scherm",
      "Heeft 3 katten"
    ],
    afbeelding: "Dennis.jpg.jpg"
  },
  {
    naam: "Quinten",
    geslacht: "Man",
    woonplaats: ["Moorsel"],
    hobby: ["Voetballen", "Jagen"],
    verjaardag: "07/12",
    schoolrichting: "Economie",
    hints: [
      "Das observeren",
      "Tackelt graag op de ...",
      "Staat altijd klaar voor jenever"
    ],
    afbeelding: "Quinten.jpg.jpg"
  },
  {
    naam: "Alexandre",
    geslacht: "Man",
    woonplaats: ["Zaventem"],
    hobby: ["Voetballen"],
    verjaardag: "01/06",
    schoolrichting: "Natuurwetenschappen",
    hints: [
      "Waal",
      "Te nonchalant",
      "Was/is ros"
    ],
    afbeelding: "Alex.jpg.jpg"
  },
  {
    naam: "Lou",
    geslacht: "Man",
    woonplaats: ["Hoeilaart"],
    hobby: ["Voetballen"],
    verjaardag: "19/02",
    schoolrichting: "Natuurwetenschappen",
    hints: [
      "Hij is blond",
      "Wordt vereerd in een cult",
      "Draagt een bril"
    ],
    afbeelding: "Lou.jpg.jpg"
  },
  {
    naam: "Quinten.U.F",
    geslacht: "Man",
    woonplaats: ["Wezembeek", "Vrebos"],
    hobby: ["Voetballen", "Jeugdbeweging"],
    verjaardag: "31/07",
    schoolrichting: "Natuurwetenschappen",
    hints: [
      "Zijn grapjes zijn grappig",
      "Korfbal",
      "Heeft twee huisdieren"
    ],
    afbeelding: "Quinte.jpg.jpg"
  },
  {
    naam: "Milhane",
    geslacht: "Man",
    woonplaats: ["Tervuren", "Laken"],
    hobby: ["Jeugdbeweging"],
    verjaardag: "03/07",
    schoolrichting: "Natuurwetenschappen",
    hints: [
      "Woont op twee verschillende plaatsen",
      "Lieve variant van zijn soort",
      "Heeft een broer"
    ],
    afbeelding: "Milhane.jpg.jpg"
  },
  {
    naam: "Miro",
    geslacht: "Man",
    woonplaats: ["Kortenberg"],
    hobby: ["Voetballen"],
    verjaardag: "10/12",
    schoolrichting: "Economie",
    hints: [
      "Altijd klaar voor een kapsalon",
      "Zonder L",
      "Heeft een broer"
    ],
    afbeelding: "Miro.jpg.jpg"
  },
  {
    naam: "Milo",
    geslacht: "Man",
    woonplaats: ["Kortenberg"],
    hobby: ["Gamen"],
    verjaardag: "16/09",
    schoolrichting: "Latijn",
    hints: [
      "Raar gebouwd",
      "Redt zijn studierichting naast iemand anders",
      "Lust geen kaas"
    ],
    afbeelding: "Milo.jpg.jpg"
  },
  {
    naam: "Hodaka",
    geslacht: "Man",
    woonplaats: ["Zaventem"],
    hobby: ["Judo"],
    verjaardag: "15/06",
    schoolrichting: "Economie",
    hints: [
      "Raar gebouwd",
      "Ziet niet veel",
      "Houdt van konten aanraken"
    ],
    afbeelding: "Hodaka.jpg.jpg"
  },
  {
    naam: "Noah",
    geslacht: "Man",
    woonplaats: ["Neerijse"],
    hobby: ["Gym", "Gamen"],
    verjaardag: "28/10",
    schoolrichting: "Economie",
    hints: [
      "Valorant is zijn leven",
      "Helpt mensen met eetproblemen",
      "Hij is rijk"
    ],
    afbeelding: "Noah.jpg.jpg"
  },
  {
    naam: "Xander",
    geslacht: "Man",
    woonplaats: ["Zaventem"],
    hobby: ["Jeugdbeweging"],
    verjaardag: "05/07",
    schoolrichting: "Economie",
    hints: [
      "Drinkt graag",
      "Eten is zijn leven",
      "Is al blijven zitten"
    ],
    afbeelding: "Xander.jpg.jpg"
  },
  {
    naam: "Aymane",
    geslacht: "Man",
    woonplaats: ["Overijse"],
    hobby: ["Gym", "Gamen"],
    verjaardag: "17/01",
    schoolrichting: "Natuurwetenschappen",
    hints: [
      "Nederlands is niet zijn moedertaal",
      "Loopt elk jaar met krukken",
      "Lacht met zijn eigen grapjes"
    ],
    afbeelding: "Aymane.jpg.jpg"
  },
  {
    naam: "Nio",
    geslacht: "Man",
    woonplaats: ["Duisburg"],
    hobby: ["Jiujitsu"],
    verjaardag: "27/07",
    schoolrichting: "Natuurwetenschappen",
    hints: [
      "Heeft een broer",
      "Hij is uniek",
      "Hij is vrij lang"
    ],
    afbeelding: "Nio.jpg.jpg"
  },
  {
    naam: "Lennox",
    geslacht: "Man",
    woonplaats: ["Moorsel"],
    hobby: ["Voetballen", "Handbal"],
    verjaardag: "05/06",
    schoolrichting: "Natuurwetenschappen",
    hints: [
      "Kan wel zesty zijn",
      "Komt met de fiets naar school",
      "Duitsland is zijn tweede thuis"
    ],
    afbeelding: "Lennox.jpg.jpg"
  },
  {
    naam: "Finn",
    geslacht: "Man",
    woonplaats: ["Moorsel"],
    hobby: ["Padel", "Hockey"],
    verjaardag: "20/02",
    schoolrichting: "Sport",
    hints: [
      "Doet padel",
      "Komt met de fiets naar school",
      "Deed voetbal bij Moorsel"
    ],
    afbeelding: "Finn.jpg.jpg"
  },
  {
    naam: "Max",
    geslacht: "Man",
    woonplaats: ["Moorsel"],
    hobby: ["Voetballen", "Golf"],
    verjaardag: "05/01",
    schoolrichting: "Economie",
    hints: [
      "Speelt golf",
      "Is een jaar hoger",
      "Zijn kapper is dood"
    ],
    afbeelding: "Max.jpg.jpg"
  },
  {
    naam: "Robin",
    geslacht: "Man",
    woonplaats: ["Hoeilaart"],
    hobby: ["Gamen", "Lopen"],
    verjaardag: "27/11",
    schoolrichting: "Natuurwetenschappen",
    hints: [
      "Is blijven zitten",
      "Heeft een lief",
      "Is vrij klein"
    ],
    afbeelding: "Robin.jpg.jpg"
  },
  {
    naam: "Fares",
    geslacht: "Man",
    woonplaats: ["Tervuren"],
    hobby: ["Gamen", "Jeugdbeweging"],
    verjaardag: "11/09",
    schoolrichting: "Natuurwetenschappen",
    hints: [
      "Doet hij aan bombarderen?",
      "Weet veel over pc's",
      "Zit op de KSA"
    ],
    afbeelding: "Fares.jpg.jpg"
  },
  {
    naam: "Bram",
    geslacht: "Man",
    woonplaats: ["Kortenberg", "Tervuren"],
    hobby: ["Jeugdbeweging"],
    verjaardag: "11/02",
    schoolrichting: "Natuurwetenschappen",
    hints: [
      "Speelde voetbal",
      "Komt met de fiets of bus naar school",
      "Heeft een slecht woord in Discord gedropt"
    ],
    afbeelding: "Bram.jpg.jpg"
  },
  {
    naam: "Robbe",
    geslacht: "Man",
    woonplaats: ["Duisburg"],
    hobby: ["Parcours", "Jeugdbeweging", "Taekwondo"],
    verjaardag: "18/07",
    schoolrichting: "Grafische technieken",
    hints: [
      "Zit op de KSA",
      "Zat op het KAT maar is getransfereerd",
      "Heeft het lef om op zijn mama te roepen"
    ],
    afbeelding: "Robbe.jpg.jpg"
  },
  {
    naam: "Rube",
    geslacht: "Man",
    woonplaats: ["Tervuren"],
    hobby: ["Voetballen", "Lopen", "Fappen"],
    verjaardag: "11/10",
    schoolrichting: "Economie",
    hints: [
      "Heeft een zus",
      "Heeft een hete zus",
      "Speelt bij Tervuren"
    ],
    afbeelding: "Rube.jpg.jpg"
  },
  {
    naam: "Roos",
    geslacht: "Vrouw",
    woonplaats: ["Duisburg"],
    hobby: ["Hockey"],
    verjaardag: "03/12",
    schoolrichting: "Economie",
    hints: [
      "Heeft een broer",
      "Passieve drinker",
      "Heeft een kind (Gertie)"
    ],
    afbeelding: "Schermafbeelding 2025-10-23 104636.jpg"
  }
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

