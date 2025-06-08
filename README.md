# blade-sniper-calc<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Blade Sniper Calc</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: #111;
      color: #fff;
      text-align: center;
      padding: 20px;
    }
    h1 {
      color: #8cfffb;
      margin-bottom: 10px;
    }
    .container {
      display: flex;
      justify-content: space-around;
      flex-wrap: wrap;
      margin-top: 20px;
    }
    .side {
      width: 45%;
      min-width: 300px;
      margin-bottom: 20px;
    }
    select {
      width: 90%;
      padding: 8px;
      margin: 5px 0;
      background-color: #222;
      color: #fff;
      border: 1px solid #555;
      border-radius: 5px;
    }
    button {
      padding: 10px 25px;
      margin-top: 20px;
      background-color: #00c2ff;
      border: none;
      border-radius: 5px;
      font-weight: bold;
      cursor: pointer;
    }
    button:hover {
      background-color: #00a8db;
    }
    #result {
      font-size: 18px;
      margin-top: 20px;
      color: #fff;
    }
    .credit {
      margin-top: 40px;
      font-size: 12px;
      color: #888;
    }
  </style>
</head>
<body>
  <h1>Blade Sniper Calc</h1>
  <div class="container">
    <div class="side" id="side1">
      <h3>Your Offer</h3>
      <select class="item"><option value="">Select item</option></select>
      <select class="item"><option value="">Select item</option></select>
      <select class="item"><option value="">Select item</option></select>
      <select class="item"><option value="">Select item</option></select>
    </div>
    <div class="side" id="side2">
      <h3>Their Offer</h3>
      <select class="item"><option value="">Select item</option></select>
      <select class="item"><option value="">Select item</option></select>
      <select class="item"><option value="">Select item</option></select>
      <select class="item"><option value="">Select item</option></select>
    </div>
  </div>
  <button onclick="compare()">Compare</button>
  <div id="result"></div>
  <div class="credit">Made by Blade</div>

  <script>
    const values = {
      "bat scythe": 0.15,
      "black df gun": 3.1,
      "black df knife": 2.2,
      "black df sniper": 3.85,
      "black flutter gun": 0.55,
      "black flutter knife": 0.45,
      "black ice peg knife": 0.3,
      "blue df gun": 2.5,
      "blue df knife": 2.1,
      "blue df sniper": 3,
      "blue flutter gun": 0.5,
      "blue flutter knife": 0.5,
      "blue ice peg knife": 0.3,
      "blue orn gun": 1,
      "bwg": 57,
      "bwk": 13,
      "cel sniper": 1.2,
      "cel gun": 0.6,
      "celestial knife": 0.15,
      "dragonbreath": 0.15,
      "enchanted mermaid gun": 0.28,
      "enchanted reaper knife": 0.22,
      "fb crossbow": 8,
      "normal fang gun": 0.47,
      "normal fang knife": 0.38,
      "flutter sniper": 1,
      "frost fang knife": 0.3,
      "gsg": 29,
      "gsk": 8,
      "gss": 37,
      "gwk": 6,
      "gwg": 16.5,
      "harmonic knife": 0.15,
      "nebula gun": 0.5,
      "nebula knife": 0.35,
      "nebula sniper": 1,
      "normal mermaid gun": 0.4,
      "normal mermaid knife": 0.31,
      "normal sniper": 1,
      "ornament gun": 1,
      "ornament knife": 0.5,
      "orn set": 1.7,
      "psg": 54,
      "psk": 12,
      "pwg": 34.5,
      "pwk": 10,
      "purple rhine knife": 0.5,
      "purple df gun": 3.85,
      "purple df knife": 2.25,
      "purple df sniper": 4,
      "peppermint gun (green)": 5.1,
      "peppermint knife (green)": 5.5,
      "red df gun": 2.5,
      "red df knife": 2.1,
      "red df sniper": 3,
      "red ice peg gun": 0.37,
      "reef gun": 12,
      "reef knife": 4,
      "rhine gun": 1,
      "rhine set": 1.6,
      "rhine sniper": 1.5,
      "rose gun": 5,
      "rosethorn knife": 0.15,
      "rsg": 32.5,
      "rsk": 9,
      "rss": 41.5,
      "rwg": 22,
      "rwk": 7,
      "rws": 29,
      "void crossbow": 0.15,
      "wc": 36,
      "white ice peg knife": 0.3,
      "winx gun": 0.45,
      "winx knife": 0.3,
      "ysg": 20.5,
      "ysk": 6.5
    };

    function populateDropdowns() {
      const selects = document.querySelectorAll("select");
      for (const select of selects) {
        for (const item in values) {
          const option = document.createElement("option");
          option.value = item;
          option.textContent = item;
          select.appendChild(option);
        }
      }
    }

    function calculateTotal(selects) {
      let total = 0;
      for (const select of selects) {
        const val = values[select.value];
        if (val) total += val;
      }
      return total;
    }

    function compare() {
      const side1 = document.querySelectorAll("#side1 select");
      const side2 = document.querySelectorAll("#side2 select");
      const total1 = calculateTotal(side1);
      const total2 = calculateTotal(side2);
      const diff = Math.abs(total1 - total2).toFixed(2);
      let verdict;

      if (total1 > total2) {
        verdict = `Win by ${diff} snipers`;
      } else if (total1 < total2) {
        verdict = `Loss by ${diff} snipers`;
      } else {
        verdict = "Fair trade";
      }

      document.getElementById("result").textContent = `Result: ${verdict}`;
    }

    populateDropdowns();
  </script>
</body>
</html>
