
<html lang="nl">
<head>
  <meta charset="UTF-8">
  <title>Raad de Persoon</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #111;
      color: White;
      text-align: center;
      padding: 20px;
    }
    table {
      width: 90%;
      margin: 0 auto;
      border-collapse: collapse;
      margin-top: 20px;
    }
    th, td {
      border: 1px solid #333;
      padding: 10px;
    }
    th {
      background: #333;
    }
    .green {
      background-color: #4CAF50;
    }
    .orange {
      background-color: #FF9800;
    }
    .red {
      background-color: #F44336;
    }
    .hint {
      margin-top: 15px;
      font-weight: bold;
      color: #ffeb3b;
      transition: opacity 0.5s ease;
  opacity: 1;
}
.hint.fade {
  opacity: 0;
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
    }
    /* Startscherm-stijl */
#startScreen {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100vh;
  background: radial-gradient(circle at center, #222 0%, #000 100%);
  color: white;
  text-align: center;
  animation: fadeIn 1s ease-in-out;
}

#startScreen h1 {
  font-size: 2.5em;
  margin-bottom: 10px;
}

#startScreen button {
  padding: 12px 25px;
  font-size: 18px;
  background-color: #ffeb3b;
  color: #111;
  border: none;
  border-radius: 10px;
  cursor: pointer;
  transition: transform 0.2s, background-color 0.2s;
}

#startScreen button:hover {
  background-color: #fdd835;
  transform: scale(1.05);
}

@keyframes fadeIn {
  from { opacity: 0; }
  to { opacity: 1; }
}

#timer {
  font-size: 18px;
  color: #ffeb3b;
  margin-top: 10px;
}
    datalist {
      background: black;
      color: red;
    }
  datalist {
    background: black;
    color: red;
  }
      
  tr {
    opacity: 0;
    transform: translateY(-5px);
    transition: opacity 0.5s ease, transform 0.5s ease;
  }

  tr.show {
    opacity: 1;
    transform: translateY(0);
  }
  </style>
</head>
<body>
<div id="startScreen">
  <h1>👤 Welkom bij <span style="color:#ffeb3b;">Wie is het?</span></h1>
  <p>Gemaakt door <strong>Quinten</strong></p>
  <p style="margin-top: 20px;">Test je kennis van je vrienden en probeer te raden wie het is!</p>
  <button id="startButton">🎮 Start het spel</button>
</div>

<div id="gameContainer" style="display:none;">
  <h1>🔍 Raad de Persoon</h1>
  <p>Typ een naam en ontdek via eigenschappen wie het is!</p>
  <div id="timer">⏱️ Tijd: 0:00</div>

  <input id="guessInput" list="nameList" placeholder="Voer een naam in...">
  <datalist id="nameList"></datalist>
  <button onclick="checkGuess()">Check</button>

  <div class="hint" id="hintText">Tip verschijnt na  4, 5 en 7 pogingen</div>
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
  <script>
    document.getElementById("startButton").addEventListener("click", startSpel);
    
    function startSpel() {
      document.getElementById("startScreen").style.display = "none";
      document.getElementById("gameContainer").style.display = "block";
      startTimer();
    }
  </script>
    </div>
  <script>
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
    `⏱️ Tijd: ${minuten}:${seconden.toString().padStart(2, '0')}`;
}

function stopTimer() {
  clearInterval(timerInterval);
}

    const personen = [
       {
    naam: "Billy",
    geslacht: "Man",
    woonplaats: ["Tervuren"],
    hobby: ["Rugby"],
    verjaardag: "13/01",
    schoolrichting: "latijn",
    hints: [
      "Unieke sport",
      "Loopt graag zonder broek rond",
      "is pas sinds midden van het 4de studie jaar op het kat"
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
      "Muziek maker",
      "Union fan",
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
      "Burn out"
    ],
    afbeelding: "eliese.jpg"
   },
          {
    naam: "Van gijsel",
    geslacht: "Vrouw",
    woonplaats: ["Leuven"],
    hobby: ["Geen"],
    verjaardag: "00/00",
    schoolrichting: "Olc",
    hints: [
      "Heeft een dochter",
      "Olc",
      "Vroeger wiskunde leerkracht"
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
      "Kan niet zo goed nederlands",
      "Cr7",
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
      "hij houdt van gamen.",
      "Hij is niet zo groot.",
      "Hij is aan alles algerisch."
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
      "heeft een zus",
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
      "heeft een zus",
      "Rare geluiden",
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
      "Tweelings broer"
    ],
    afbeelding: "Nico.jpg.jpg"
  },
  {
    naam: "Paulussen",
    geslacht: "Man",
    woonplaats: ["Leuven"],
    hobby: ["Rare video's maken"],
    verjaardag: "00/00",
    schoolrichting: "Aarderijkskunde",
    hints: [
      "Koffiegeur",
      "Raar kapsel",
      "The goat in meerkeuzen examen"
    ],
    afbeelding: "Paulussen.jpg.jpg"
  },
  {
    naam: "Dennis",
    geslacht: "Man",
    woonplaats: ["Duisburg"],
    hobby: ["Gamen", "jeugdbeweging"],
    verjaardag: "27/07",
    schoolrichting: "Economie",
    hints: [
      "Hij is blond.",
      "Hij zit graag achter een scherm.",
      "Hij heeft 3 katten."
    ],
    afbeelding: "Dennis.jpg.jpg"
  },
  {
    naam: "Quinten",
    geslacht: "Man",
    woonplaats: ["Moorsel"],
    hobby: ["Voetballen" , "jagen"],
    verjaardag: "07/12",
    schoolrichting: "Economie",
    hints: [
      "Das observeren ",
      "Hij tackelt graag op de ...",
      "Hij staat wel klaar voor jenever."
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
      "Waal.",
      "Hij is te nonchalante.",
      "Hij was/is ros."
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
      "Hij wordt vereerd in een cult",
      "Hij draagt een bril"
    ],
    afbeelding: "Lou.jpg.jpg"
  },
  {
    naam: "Quinten.U.F",
    geslacht: "Man",
    woonplaats: ["Wezembeek", "Vrebos "],
    hobby: ["Voetballen","jeugdbeweging"],
    verjaardag: "31/07",
    schoolrichting: "Natuurwetenschappen",
    hints: [
      "Zij grapjes zijn grappig",
      "Korfbal",
      "Hij heeft twee huisdieren"
    ],
    afbeelding: "Quinte.jpg.jpg"
  },
  {
    naam: "Milhane",
    geslacht: "Man",
    woonplaats: ["Tervuren" , "Laken"],
    hobby: ["jeugdbeweging"],
    verjaardag: "03/07",
    schoolrichting: "Natuurwetenschappen",
    hints: [
      "Hij woont op twee verschillende plaatsen",
      "Hij is de lieve variante van zijn soort",
      "Hij heeft een broer",
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
      "Hij staat altijd wel klaar voor een kapsalon",
      "Zonder L",
      "Hij heeft een broer",
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
      "Naast iemand anders, red hij zijn studie richting",
      "Lust geen kaas",
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
      "Houdt van konten aanraken",
    ],
    afbeelding: "Hodaka.jpg.jpg"
  },
  {
    naam: "Noah",
    geslacht: "Man",
    woonplaats: ["Neerrijsen"],
    hobby: ["Gym" , "gamen"],
    verjaardag: "28/10",
    schoolrichting: "Economie",
    hints: [
      "Valorante is zijn leven",
      "Hij helpt mensen met eet problemen",
      "Hij is rijk",
    ],
    afbeelding: "Noah.jpg.jpg"
  },
  {
    naam: "Xander",
    geslacht: "Man",
    woonplaats: ["Zaventem"],
    hobby: ["jeugdbeweging"],
    verjaardag: "05/07",
    schoolrichting: "Economie",
    hints: [
      "Je kan wel zeggen dat hij graag drinkt",
      "Eten is zijn leven",
      "Hij is al blijven zitten",
    ],
    afbeelding: "Xander.jpg.jpg"
  },
  {
    naam: "Aymane",
    geslacht: "Man",
    woonplaats: ["Overijse"],
    hobby: ["Gym" , " gamen"],
    verjaardag: "17/01",
    schoolrichting: "Natuurwetenschappen",
    hints: [
      "Nederlands is niet zijn moedertaal",
      "Hij loopt elk jaar wel met krukken",
      "Hij lacht met zijn eigen grapjes",
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
      "Hij heeft een broer",
      "Hij is uniek ",
      "Hij is vrij lang",
    ],
    afbeelding: "Nio.jpg.jpg"
  },
      {
    naam: "Lennox",
    geslacht: "Man",
    woonplaats: ["Moorsel"],
    hobby: ["Voetballen" , "Handbal"],
    verjaardag: "05/06",
    schoolrichting: "Natuurwetenschappen",
    hints: [
      "Hij kan wel zesty zijn",
      "Hij komt met de fiets naar school.",
      "Duitsland is zijn tweede thuis wel",
    ],
    afbeelding: "Lennox.jpg.jpg"
  },
      {
    naam: "Finn",
    geslacht: "Man",
    woonplaats: ["Moorsel"],
    hobby: ["Padel" , "hockey"],
    verjaardag: "20/02",
    schoolrichting: "sport",
    hints: [
      "Hij doet padel",
      "Hij komt met de fiets naar school",
      "Hij deed voetbal bij moorsel",
    ],
    afbeelding: "Finn.jpg.jpg"
  },
      {
    naam: "Max",
    geslacht: "Man",
    woonplaats: ["Moorsel"],
    hobby: ["Voetballen" , "golf"],
    verjaardag: "05/01",
    schoolrichting: "economie",
    hints: [
      "Speelt golf",
      "Is een jaar hoger",
      "Zijn kapper is dood",
    ],
    afbeelding: "Max.jpg.jpg"
  },
      {
    naam: "Robin",
    geslacht: "Man",
    woonplaats: ["Hoeilaart"],
    hobby: ["Gamen" , "lopen"],
    verjaardag: "27/11",
    schoolrichting: "Natuurwetenschappen",
    hints: [
      "Is blijven zitten",
      "Heeft een lief",
      "Is vrij klein",
    ],
    afbeelding: "Robin.jpg.jpg"
  },
      {
    naam: "Fares",
    geslacht: "Man",
    woonplaats: ["Tervuren"],
    hobby: ["gamen", "jeugdbeweging"],
    verjaardag: "11/09",
    schoolrichting: "Natuurwetenschappen",
    hints: [
      "Doet hij aan bombarderen?",
      "Hij weet wel veel over pc's",
      "Hij zit op de KSA",
    ],
    afbeelding: "Fares.jpg.jpg"
  },
      {
    naam: "Bram",
    geslacht: "Man",
    woonplaats: ["Kortenberg" , "Tervuren"],
    hobby: ["jeugdbeweging"],
    verjaardag: "11/02",
    schoolrichting: "Natuurwetenschappen",
    hints: [
      "Hij speelde voetbal",
      "Hij komt met de fiets/bus naar school",
      "Hij heeft een slecht woord in discord gedropt",
    ],
    afbeelding: "Bram.jpg.jpg"
  },
      {
    naam: "Robbe",
    geslacht: "Man",
    woonplaats: ["Duisburg"],
    hobby: ["parcour", "jeugdbeweging" , "Thaikwando"],
    verjaardag: "18/07",
    schoolrichting: "grafische technieken",
    hints: [
      "Hij zit op de KSA",
      "Hij zat op het KAT maar is getranferd",
      "Hij heeft het lef om op zijn mama te roepen",
    ],
    afbeelding: "Robbe.jpg.jpg"
  },    
      {
    naam: "Rube",
    geslacht: "Man",
    woonplaats: ["Tervuren"],
    hobby: ["Voetballen", "Lopen" , "fappen"],
    verjaardag: "11/10",
    schoolrichting: "Economie",
    hints: [
      "Hij heeft een zus",
      "Hij heeft een hete zus ",
      "Hij speelt bij tervuren ",
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
      "Het heeft een broer",
      "Pasieve drinker",
      "Het heeft een kind (gertie)",
       ],
          afbeelding: "Schermafbeelding 2025-10-23 104636.jpg"
    },
      ];

    let doelPersoon = personen[Math.floor(Math.random() * personen.length)];
    let pogingen = 0;

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
  
  stopTimer();
const eindTijd = new Date();
const tijdVerschil = Math.floor((eindTijd - startTime) / 1000);
const minuten = Math.floor(tijdVerschil / 60);
const seconden = tijdVerschil % 60;
document.getElementById("hintText").textContent += ` ⏱️ (${minuten}:${seconden.toString().padStart(2,'0')}) in ${pogingen} pogingen!`;


 
  hintText.classList.add("fade");

  setTimeout(() => {
    hintText.textContent = `✅ Juist! Het was ${doelPersoon.naam}`;
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
