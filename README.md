
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
    datalist {
      background: black;
      color: white;
    }
  </style>
</head>
<body>

  <h1>🔍 Raad de Persoon</h1>
  <p>Typ een naam en ontdek via eigenschappen wie het is!</p>

  <input id="guessInput" list="nameList" placeholder="Voer een naam in...">
  <datalist id="nameList"></datalist>
  <button onclick="checkGuess()">Check</button>

  <div class="hint" id="hintText">Tip verschijnt na 2, 3 en 5 pogingen</div>
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
    const personen = [
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
    afbeelding: "Maxime.jpg"
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
    afbeelding: "Dennis.jpg"
  },
  {
    naam: "Quinten",
    geslacht: "Man",
    woonplaats: ["Moorsel"],
    hobby: ["Voetballen" , "jagen"],
    verjaardag: "07/12",
    schoolrichting: "Economie",
    hints: [
      "hij houdt drinken.",
      "Hij tackelt graag op de ...",
      "Hij houdt van jagen."
    ],
    afbeelding: "Quinten.jpg"
  },
  {
    naam: "Alexandre",
    geslacht: "Man",
    woonplaats: ["Zaventem"],
    hobby: ["Voetballen"],
    verjaardag: "01/06",
    schoolrichting: "Natuurwetenschappen",
    hints: [
      "hij heeft een lief.",
      "Hij is te nonchalante.",
      "Hij was/is ros."
    ],
    afbeelding: "Alex.jpg"
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
    afbeelding: "Lou.jpg"
  },
  {
    naam: "Quinten.U.F",
    geslacht: "Man",
    woonplaats: ["Tervuren"],
    hobby: ["Voetballen","jeugdbeweging"],
    verjaardag: "31/07",
    schoolrichting: "Natuurwetenschappen",
    hints: [
      "Zij grapjes zijn niet grappig",
      "Zijn huis is een plaats waar iedereen zicht thuis voelt",
      "Hij heeft twee huisdieren"
    ],
    afbeelding: "Quinte.jpg"
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
    afbeelding: "Milhane.jpg"
  },
  {
    naam: "Miro",
    geslacht: "Man",
    woonplaats: ["Kortenberg"],
    hobby: ["voetballen"],
    verjaardag: "10/12",
    schoolrichting: "Natuurwetenschappen",
    hints: [
      "Hij staat altijd wel klaar voor een kapsalon",
      "Zonder L",
      "Hij heeft een broer",
    ],
    afbeelding: "Miro.jpg"
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
      "Naast iemand anders red zijn studie richting",
      "Lust geen kaas",
    ],
    afbeelding: "Milo.jpg"
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
      "Is hij gay?",
      "Houdt van konten aanraken",
    ],
    afbeelding: "Hodaka.jpg"
  },
  {
    naam: "Noah",
    geslacht: "Man",
    woonplaats: ["Neerrijsen"],
    hobby: ["Gym"],
    verjaardag: "28/10",
    schoolrichting: "Economie",
    hints: [
      "Valorante is zijn leven",
      "Hij helpt mensen met eet problemen",
      "Hij is rijk",
    ],
    afbeelding: "Noah.jpg"
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
    afbeelding: "Xander.jpg"
  },
  {
    naam: "Aymane",
    geslacht: "Man",
    woonplaats: ["Overijse"],
    hobby: ["Gym"],
    verjaardag: "17/01",
    schoolrichting: "Natuurwetenschappen",
    hints: [
      "Nederlands is niet zijn moedertaal",
      "Hij loopt elk jaar wel met krukken",
      "Hij lacht met zijn eigen grapjes",
    ],
    afbeelding: "Aymane.jpg"
  },
      {
    naam: "Nio",
    geslacht: "Man",
    woonplaats: ["Duisburg"],
    hobby: ["Judo"],
    verjaardag: "27/07",
    schoolrichting: "Natuutwetenschappen",
    hints: [
      "Hij komt met de fiets naar school",
      "Hij heeft een lief",
      "Hij is vrij lang",
    ],
    afbeelding: "Nio.jpg"
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
    afbeelding: "Lennox.jpg"
  },
      {
    naam: "Finn",
    geslacht: "Man",
    woonplaats: ["Moorsel"],
    hobby: ["Padel" , "hockey"],
    verjaardag: "20/02",
    schoolrichting: "economie",
    hints: [
      "Hij doet padel",
      "Hij komt met de fiets naar school",
      "Hij deed voetbal bij moorsel",
    ],
    afbeelding: "Finn.jpg"
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
    afbeelding: "Max.jpg"
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
    afbeelding: "Robin.jpg"
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
    afbeelding: "Fares.jpg"
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
    afbeelding: "Bram.jpg"
  },
      {
    naam: "Robbe",
    geslacht: "Man",
    woonplaats: ["Duisburg"],
    hobby: ["parcour", "jeugdbeweging"],
    verjaardag: "18/07",
    schoolrichting: "grafische technieken",
    hints: [
      "Hij zit op de KSA",
      "Hij zat op het KAT maar is getranferd",
      "Hij heeft het lef om op zijn mama te roepen",
    ],
    afbeelding: "Robbe.jpg"
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
        <td>${gevonden.naam}</td>
        ${eigenschappen.map((eig, i) => `
          <td class="${kleuren[i]}">${gevonden[eig]}</td>
        `).join("")}
      `;

      tbody.appendChild(rij);

      if (gevonden.naam.toLowerCase() === doelPersoon.naam.toLowerCase()) {
        document.getElementById("hintText").textContent = `✅ Juist! Het was ${doelPersoon.naam}`;
        toonAfbeelding();
      } else {
        geefHint();
      }
    }

    function geefHint() {
      const hintText = document.getElementById("hintText");
      if (pogingen === 2) {
        hintText.textContent = `Hint 1: ${doelPersoon.hints[0]}`;
      } else if (pogingen === 3) {
        hintText.textContent = `Hint 2: ${doelPersoon.hints[1]}`;
      } else if (pogingen === 5) {
        hintText.textContent = `Laatste Hint: ${doelPersoon.hints[2]}`;
        toonAfbeelding();
      }
    }

    function toonAfbeelding() {
      const img = document.getElementById("personImage");
      img.src = doelPersoon.afbeelding;
      img.style.display = "block";
    }

    function herstartSpel() {
      location.reload();
    }
  </script>

</body>
</html>
