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
      margin-bottom: 10px;
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
    /* Fade-in animatie */
    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(10px); }
      to { opacity: 1; transform: translateY(0); }
    }
    /* Spelgedeelte */
    #gameContainer {
      display: none;
      animation: fadeIn 1s ease-in;
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
    th {
      background: #333;
    }
    .green { background-color: #4CAF50; }
    .orange { background-color: #FF9800; }
    .red { background-color: #F44336; }
    .hint {
      margin-top: 15px;
      font-weight: bold;
      color: #ffeb3b;
    }
    img {
      margin-top: 20px;
      max-width: 200px;
      border-radius: 10px;
      display: none;
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
    button:hover {
      transform: scale(1.05);
    }
    datalist {
      background: black;
      color: red;
    }
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
  <!-- SPELGEBIED -->
  <div id="gameContainer">
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
  </div>
  <!-- SCRIPT -->
  <script>
    // Eventlistener voor startknop
    document.getElementById("startButton").addEventListener("click", startSpel);
    function startSpel() {
      document.getElementById("startScreen").style.display = "none";
      document.getElementById("gameContainer").style.display = "block";
    }
    // De rest van je bestaande JavaScript code (personenlijst, checkGuess, hints, enz.)
    // mag hieronder blijven staan zoals je al had.
  </script>
    let startTime;
let timerInterval;

function startSpel() {
  document.getElementById("startScreen").style.display = "none";
  document.getElementById("gameContainer").style.display = "block";
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
  document.getElementById("timer").textContent =
    `⏱️ Tijd: ${minuten}:${seconden.toString().padStart(2, "0")}`;
}
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
    let doelPersoon = personen[Math.floor(Math.random() * personen.length)];
    let pogingen = 0;
    let hintIndex = 0;
    let startTime;
    let timerInterval;
    // autocomplete lijst opbouwen
    const nameList = document.getElementById("nameList");
    personen.forEach(p => {
      const opt = document.createElement("option");
      opt.value = p.naam;
      nameList.appendChild(opt);
    });
    function levenshtein(a, b) {
      const matrix = Array.from({ length: b.length + 1 }, (_, i) =>
        Array(a.length + 1).fill(0)
      );
      for (let i = 0; i <= b.length; i++) matrix[i][0] = i;
      for (let j = 0; j <= a.length; j++) matrix[0][j] = j;
      for (let i = 1; i <= b.length; i++) {
        for (let j = 1; j <= a.length; j++) {
          matrix[i][j] = b[i - 1] === a[j - 1]
            ? matrix[i - 1][j - 1]
            : Math.min(
                matrix[i - 1][j - 1] + 1,
                matrix[i][j - 1] + 1,
                matrix[i - 1][j] + 1
              );
        }
      }
      return matrix[b.length][a.length];
    }

  function vergelijkEigenschap(gegokt, echt) {
  const naarArray = val => Array.isArray(val) ? val : val.split("/").map(s => s.trim());
  const normalize = str => str.toLowerCase().trim();


  const gegoktArray = naarArray(gegokt).map(normalize);
  const echtArray = naarArray(echt).map(normalize);
  // Volledige match
  if (gegoktArray.length === echtArray.length &&
      gegoktArray.every(g => echtArray.includes(g))) {
    return "green";
  }

  // Gedeeltelijke match
  const match = gegoktArray.some(g => 
    echtArray.some(e => e.includes(g) || levenshtein(g, e) <= 2)
  );

  return match ? "orange" : "red";
}
    function checkGuess() {
      const input = document.getElementById("guessInput").value.trim();
      if (!input) return;
      const gevonden = personen.find(p => p.naam.toLowerCase() === input.toLowerCase());
      const tbody = document.querySelector("#guessTable tbody");
      if (!gevonden) {
        alert("Naam niet gevonden in lijst.");
        return;
      }
      pogingen++;
      const rij = document.createElement("tr");
      const eigenschappen = ["geslacht", "woonplaats", "hobby", "verjaardag", "schoolrichting"];
      const kleuren = eigenschappen.map(eig =>
        vergelijkEigenschap(gevonden[eig], doelPersoon[eig])
      );
      rij.innerHTML = `
        <td class="${gevonden.naam.toLowerCase() === doelPersoon.naam.toLowerCase() ? 'green' : 'red'}">${gevonden.naam}</td>
        ${eigenschappen.map((eig, i) => `
          <td class="${kleuren[i]}">${gevonden[eig]}</td>
        `).join("")}
      `;
      tbody.appendChild(rij);
      setTimeout(() => rij.classList.add("show"), 50);
      if (gevonden.naam.toLowerCase() === doelPersoon.naam.toLowerCase()) {
  const hintText = document.getElementById("hintText");
  const totaleTijd = stopTimer();
  const minuten = Math.floor(totaleTijd / 60);
  const seconden = totaleTijd % 60;

  function stopTimer() {
      clearInterval(timerInterval);
      return Math.floor((new Date() - startTime) / 1000);
    }
  // Fade-out
  hintText.classList.add("fade");
  setTimeout(() => {
    hintText.textContent = `✅ Juist! Het was ${doelPersoon.naam}! 
🎯 Je deed er ${pogingen} pogingen over en ${minuten}:${seconden
      .toString()
      .padStart(2, "0")} minuten.`;
    hintText.classList.remove("fade");
  }, 300);

  toonAfbeelding();
} else {
  geefHint();
}
  }
   function geefHint() {
  const hintText = document.getElementById("hintText");

  // Fade-out
  hintText.classList.add("fade");

  setTimeout(() => {
    if (pogingen === 4) {
      hintText.textContent = `Hint 1: ${doelPersoon.hints[0]}`;
    } else if (pogingen === 5) {
      hintText.textContent = `Hint 2: ${doelPersoon.hints[1]}`;
    } else if (pogingen === 7) {
      hintText.textContent = `Laatste Hint: ${doelPersoon.hints[2]}`;
    }
    // Fade-in
    hintText.classList.remove("fade");
  }, 300); 
}   
   img {
  margin-top: 20px;
  max-width: 200px;
  border-radius: 10px;
  display: none;
  opacity: 0;
  transition: opacity 0.6s ease; /* <-- zorgt voor de fade-in */
}
img.show {
  display: block;
  opacity: 1;
}
    }
    function herstartSpel() {
      location.reload();
    }
    document.getElementById("startButton").addEventListener("click", startSpel);
  </script>
</body>
</html>
