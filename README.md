<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Blade Sniper Calc</title>
  <style>
    body {
      font-family: 'Segoe UI', sans-serif;
      background: linear-gradient(to bottom right, #1e1e2f, #2e2e3f);
      color: #fff;
      margin: 0;
      padding: 0;
      text-align: center;
    }
    h1 {
      margin-top: 20px;
    }
    .calculator {
      max-width: 900px;
      margin: 40px auto;
      background-color: #2f2f3f;
      padding: 20px;
      border-radius: 10px;
      box-shadow: 0 0 20px #000;
    }
    select {
      width: 100%;
      margin: 8px 0;
      padding: 10px;
      background-color: #3f3f4f;
      color: white;
      border: none;
      border-radius: 5px;
      font-size: 16px;
    }
    button {
      background-color: #5e5eff;
      border: none;
      padding: 12px 24px;
      color: white;
      font-size: 16px;
      cursor: pointer;
      margin-top: 20px;
      border-radius: 5px;
    }
    button:hover {
      background-color: #4e4edf;
    }
    .result {
      margin-top: 20px;
      font-size: 20px;
      font-weight: bold;
    }
    .row {
      display: flex;
      justify-content: space-between;
      flex-wrap: wrap;
    }
    .column {
      flex: 1;
      margin: 10px;
    }
    footer {
      margin-top: 40px;
      font-size: 12px;
      color: #aaa;
    }
  </style>
</head>
<body>
  <h1>Blade Sniper Calc</h1>
  <div class="calculator">
    <div class="row">
      <div class="column">
        <h2>Your Offer</h2>
        <div id="yourOfferSlots"></div>
      </div>
      <div class="column">
        <h2>Their Offer</h2>
        <div id="theirOfferSlots"></div>
      </div>
    </div>
    <button onclick="compareOffers()">Compare</button>
    <div class="result" id="result"></div>
  </div>
  <footer>Made by Blade</footer>

  <script>
    const itemValues = {
      "bat scythe": 0.15, "black df gun": 3.1, "black df knife": 2.2,
      "black df sniper": 3.9, "black flutter gun": 0.55, "black flutter knife": 0.45,
      "blue df gun": 2.5, "blue df knife": 2.1, "blue df sniper": 3,
      "cel sniper": 1.2, "fb crossbow": 8.5, "flutter sniper": 1,
      "gsg": 29, "gsk": 8, "gss": 37, "gwg": 17, "gwk": 6,
      "pwg": 34.5, "pwk": 10, "psg": 55, "psk": 12,
      "rwg": 22, "rwk": 7, "rsg": 32.5, "rsk": 9, "rss": 41.5,
      "reef gun": 12, "reef knife": 4, "rose gun": 5,
      "ysg": 20.5, "ysk": 6.5,
      "purple df sniper": 4, "red df sniper": 3, "blue flutter gun": 0.5,
      "normal sniper": 1
    };

    const itemOptions = Object.keys(itemValues).sort();

    function createDropdown(id) {
      const select = document.createElement("select");
      select.innerHTML = `<option value="">Select item</option>` +
        itemOptions.map(item => `<option value="${item}">${item}</option>`).join("");
      document.getElementById(id).appendChild(select);
    }

    function setupSlots(containerId, count) {
      for (let i = 0; i < count; i++) {
        createDropdown(containerId);
      }
    }

    function calculateTotal(slotId) {
      const selects = document.getElementById(slotId).getElementsByTagName("select");
      let total = 0;
      for (let s of selects) {
        if (s.value) total += itemValues[s.value] || 0;
      }
      return total;
    }

    function compareOffers() {
      const yourTotal = calculateTotal("yourOfferSlots");
      const theirTotal = calculateTotal("theirOfferSlots");
      let diff = (yourTotal - theirTotal).toFixed(2);

      let resultText = `Your offer: ${yourTotal} snipers | Their offer: ${theirTotal} snipers\n`;
      if (yourTotal > theirTotal) {
        resultText += `You are overpaying by ${diff} snipers (L)`;
      } else if (yourTotal < theirTotal) {
        resultText += `You are winning by ${Math.abs(diff)} snipers (W)`;
      } else {
        resultText += `Fair trade (0 sniper diff)`;
      }

      document.getElementById("result").innerText = resultText;
    }

    setupSlots("yourOfferSlots", 8);
    setupSlots("theirOfferSlots", 8);
  </script>
</body>
</html>
