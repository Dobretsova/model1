<html lang="ru">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>Калькулятор риска ГСД</title>
  <style>
    * {
      box-sizing: border-box;
    }

    body {
      font-family: Arial, sans-serif;
      margin: 0;
      padding: 20px;
      background: #f1f1f1;
    }

    .container {
      max-width: 500px;
      margin: 0 auto;
      background: #fff;
      padding: 20px;
      border-radius: 10px;
      box-shadow: 0 0 10px rgba(0,0,0,0.1);
    }

    h1 {
      text-align: center;
      font-size: 24px;
      margin-bottom: 20px;
    }

    label {
      display: block;
      margin-top: 15px;
      font-weight: bold;
      font-size: 16px;
    }

    input {
      width: 100%;
      padding: 10px;
      margin-top: 5px;
      font-size: 16px;
      border: 1px solid #ccc;
      border-radius: 5px;
    }

    button {
      margin-top: 25px;
      padding: 14px;
      width: 100%;
      background-color: #4CAF50;
      color: white;
      border: none;
      border-radius: 5px;
      font-size: 18px;
      cursor: pointer;
    }

    .result {
      margin-top: 20px;
      padding: 15px;
      border-radius: 5px;
      font-weight: bold;
      text-align: center;
    }

    .high-risk {
      background-color: #f8d7da;
      color: #721c24;
      border: 1px solid #f5c6cb;
    }

    .low-risk {
      background-color: #d4edda;
      color: #155724;
      border: 1px solid #c3e6cb;
    }
  </style>
</head>
<body>

  <div class="container">
    <h1>Калькулятор риска ГСД</h1>

    <label>Аланин</label>
    <input type="number" id="alanin" step="any">

    <label>Аспарагиновая кислота</label>
    <input type="number" id="asp_ksl" step="any">

    <label>Аспаргин</label>
    <input type="number" id="aspargin" step="any">

    <label>Глицин</label>
    <input type="number" id="glycin" step="any">

    <label>Глутамин</label>
    <input type="number" id="glutamin" step="any">

    <label>Глутаминовая кислота</label>
    <input type="number" id="glutam_ksl" step="any">

    <button onclick="calculate()">Рассчитать</button>

    <div id="result" class="result"></div>
  </div>

  <script>
    function calculate() {
      const alanin = parseFloat(document.getElementById('alanin').value) || 0;
      const asp_ksl = parseFloat(document.getElementById('asp_ksl').value) || 0;
      const aspargin = parseFloat(document.getElementById('aspargin').value) || 0;
      const glycin = parseFloat(document.getElementById('glycin').value) || 0;
      const glutamin = parseFloat(document.getElementById('glutamin').value) || 0;
      const glutam_ksl = parseFloat(document.getElementById('glutam_ksl').value) || 0;

      const z = 288.780
                + (1.326 * alanin)
                - (235.461 * asp_ksl)
                - (14.813 * aspargin)
                - (4.032 * glycin)
                + (41.517 * glutamin)
                + (72.569 * glutam_ksl);

      const P = 1 / (1 + Math.exp(-z));
      const percent = (P * 100).toFixed(2);

      const resultDiv = document.getElementById('result');
      resultDiv.innerHTML = `Риск: <strong>${percent}%</strong><br>`;

      if (P <= 0.557) {
        resultDiv.className = 'result high-risk';
        resultDiv.innerHTML += '⛔ <strong>Высокий риск</strong> гестационного сахарного диабета';
      } else {
        resultDiv.className = 'result low-risk';
        resultDiv.innerHTML += '✅ <strong>Низкий риск</strong> гестационного сахарного диабета';
      }
    }
  </script>

</body>
</html>
