<html lang="nl">
<head>
  <meta charset="UTF-8">
  <title>Wie is het? | Raad de Persoon</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #111;
      color: white;
      text-align: center;
      padding: 20px;
    }
    /* Startscherm */
    #startScreen {
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      height: 100vh;
      background: linear-gradient(135deg, #1f1f1f, #2b2b2b);
      animation: fadeIn 1.5s ease-in;
    }
    #startScreen h1 {
      font-size: 3em;
      color: #ffcc00;
    }
    #startScreen p {
      font-size: 1.2em;
      color: #ddd;
      max-width: 600px;
    }
    #startButton {
      margin-top: 30px;
      padding: 15px 30px;
      font-size: 18px;
      background-color: #ffcc00;
      color: #111;
      border: none;
      border-radius: 8px;
      cursor: pointer;
      transition: 0.3s;
    }
    #startButton:hover {
      background-color: #ffdb4d;
      transform: scale(1.05);
    }
    /* fade animatie */
    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(10px); }
      to { opacity: 1; transform: translateY(0); }
    }
    /* Spelgedeelte */
    #gameContainer {
      display: none;
      animation: fadeIn 1s ease-in;
    }
    #timer {
      font-size: 1.1em;
      color: #ffcc00;
      margin-bottom: 10px;
    }
    table {
      width: 90%;
      margin: 20px auto;
      border-collapse: collapse;
    }
    th, td {
      border: 1px solid #333;
      padding: 10px;
    }
    th { background: #333; }
    .green { background-color: #4CAF50; }
    .orange { background-color: #FF9800; }
    .red { background-color: #F44336; }
    .hint {
      margin-top: 15px;
      font-weight: bold;
      color: #ffeb3b;
      transition: opacity 0.3s ease;
    }
    img {
      margin-top: 20px;
      max-width: 200px;
      border-radius: 10px;
      display: none;
      opacity: 0;
      transition: opacity 0.6s ease;
    }
    img.show {
      display: block;
      opacity: 1;
    }
    input {
      padding: 10px;
      font-size: 16px;
      width: 250px;
    }
    button {
      padding: 10px 15px;
      font-size: 16px;
      margin-left: 10px;
      cursor: pointer;
      border-radius: 8px;
      transition: 0.2s;
    }
    button:hover { transform: scale(1.05); }
    /* Leaderboard */
    #leaderboard {
      background: #222;
      border-radius: 12px;
      padding: 15px;
      width: 80%;
      margin: 30px auto;
    }
    #leaderboard h2 { color: #ffcc00; }
    #leaderboard table { width: 100%; color: white; }
    #leaderboard th { background: #333; }
    #leaderboard td { border: 1px solid #444; padding: 8px; }
  </style>
</head>
<body>

  <!-- STARTSCHERM -->
  <div id="startScreen">
    <h1>🎯 Welkom bij "Wie is het?"</h1>
    <p>Test je kennis van je vrienden en probeer te raden wie het is!</p>
    <p>Gemaakt door Quinten 💻</p>
    <button id="startButton">Start het spel 🎮</button>
  </div>

  <!-- SPEL -->
  <div id="gameContainer">
    <div id="timer">⏱️ Tijd: 0:00</div>
    <h1>🔍 Raad de Persoon</h1>
    <p>Typ een naam en ontdek via eigenschappen wie het is!</p>
    <input id="guessInput" list="nameList" placeholder="Voer een naam in...">
    <datalist id="nameList"></datalist>
    <button onclick="checkGuess()">Check</button>
    <div class="hint" id="hintText">Tip verschijnt na 4, 5 en 7 pogingen</div>
    <img id="personImage" src="" alt="Foto van de persoon">
    <br>
    <button onclick="herstartSpel()" style="margin-top: 20px;">🔄 Opnieuw spelen</button>
    <table id="guessTable">
      <thead>
        <tr>
          <th>Naam</th>
          <th>Geslacht</th>
          <th>Woonplaats</th>
          <th>Hobby</th>
          <th>Verjaardag</th>
          <th>Schoolrichting</th>
        </tr>
      </thead>
      <tbody></tbody>
    </table>
    <div id="leaderboard">
      <h2>🏆 Leaderboard</h2>
      <table id="leaderboardTable">
        <thead>
          <tr><th>Naam</th><th>Pogingen</th><th>Tijd (s)</th></tr>
        </thead>
        <tbody></tbody>
      </table>
    </div>
  </div>

  <script>
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
    naam: "Mathias Buyle",
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
    naam: "Francesca Vranck",
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
    naam: "Elise Eggerickx",
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
    naam: "Ingrid Van Gysel",
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
    naam: "Kathleen Moriau",
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
    naam: "Ana Pontinha",
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
  },
    ];

    let doelPersoon, pogingen = 0, hintIndex = 0, startTime, timerInterval;

    // Autocomplete
    const nameList = document.getElementById("nameList");
    personen.forEach(p => {
      const opt = document.createElement("option");
      opt.value = p.naam;
      nameList.appendChild(opt);
    });

    // Start scherm
    document.getElementById("startButton").addEventListener("click", startSpel);
    function startSpel() {
      document.getElementById("startScreen").style.display = "none";
      document.getElementById("gameContainer").style.display = "block";
      doelPersoon = personen[Math.floor(Math.random() * personen.length)];
      startTimer();
      laadLeaderboard();
    }

    // Timer
    function startTimer() {
      startTime = new Date();
      timerInterval = setInterval(() => {
        const diff = Math.floor((new Date() - startTime) / 1000);
        const min = Math.floor(diff / 60);
        const sec = diff % 60;
        document.getElementById("timer").textContent = `⏱️ Tijd: ${min}:${sec.toString().padStart(2, "0")}`;
      }, 1000);
    }
    function stopTimer() {
      clearInterval(timerInterval);
      return Math.floor((new Date() - startTime) / 1000);
    }

    // Functie om overeenkomsten te checken
    function vergelijkEigenschap(gegokt, echt) {
      const arr = v => Array.isArray(v) ? v : [v];
      gegokt = arr(gegokt).map(x => x.toLowerCase());
      echt = arr(echt).map(x => x.toLowerCase());
      if (gegokt.some(g => echt.includes(g))) return "green";
      if (gegokt.some(g => echt.some(e => e.includes(g)))) return "orange";
      return "red";
    }

    // Check de gok
    function checkGuess() {
      const input = document.getElementById("guessInput").value.trim();
      if (!input) return;
      const gevonden = personen.find(p => p.naam.toLowerCase() === input.toLowerCase());
      if (!gevonden) { alert("Naam niet gevonden."); return; }

      pogingen++;
      const tbody = document.querySelector("#guessTable tbody");
      const eigenschappen = ["geslacht", "woonplaats", "hobby", "verjaardag", "schoolrichting"];
      const kleuren = eigenschappen.map(e => vergelijkEigenschap(gevonden[e], doelPersoon[e]));

      const rij = document.createElement("tr");
      rij.innerHTML = `
        <td class="${gevonden.naam === doelPersoon.naam ? 'green' : 'red'}">${gevonden.naam}</td>
        ${eigenschappen.map((eig, i) => `<td class="${kleuren[i]}">${gevonden[eig]}</td>`).join("")}
      `;
      tbody.appendChild(rij);

      if (gevonden.naam === doelPersoon.naam) {
        const tijd = stopTimer();
        const naam = prompt("🎉 Juist! Vul je naam in voor het leaderboard:");
        if (naam) voegToeAanLeaderboard(naam, tijd);
        toonAfbeelding();
      } else {
        geefHint();
      }
    }

    function geefHint() {
      const hintText = document.getElementById("hintText");
      if ([4, 5, 7].includes(pogingen)) {
        hintText.style.opacity = 0;
        setTimeout(() => {
          hintText.textContent = doelPersoon.hints[hintIndex++] || "Geen extra hints meer!";
          hintText.style.opacity = 1;
        }, 300);
      }
    }

    function toonAfbeelding() {
      const img = document.getElementById("personImage");
      img.src = doelPersoon.afbeelding;
      img.classList.add("show");
    }

    function herstartSpel() { location.reload(); }

    // Leaderboard
    function laadLeaderboard() {
      const data = JSON.parse(localStorage.getItem("leaderboard") || "[]");
      const tbody = document.querySelector("#leaderboardTable tbody");
      tbody.innerHTML = "";
      data.sort((a, b) => a.time - b.time).slice(0, 5).forEach(d => {
        const tr = document.createElement("tr");
        tr.innerHTML = `<td>${d.name}</td><td>${d.attempts}</td><td>${d.time}</td>`;
        tbody.appendChild(tr);
      });
    }

    function voegToeAanLeaderboard(name, time) {
      const data = JSON.parse(localStorage.getItem("leaderboard") || "[]");
      data.push({ name, attempts: pogingen, time });
      localStorage.setItem("leaderboard", JSON.stringify(data));
      laadLeaderboard();
    }
  </script>
</body>
</html>

 

