<!DOCTYPE html>
<html>
<head>
  <title>Калькулятор гестационного сахарного диабета</title>
  <style>
    /* стили для интерфейса */
  </style>
</head>
<body>
  <h1>Калькулятор гестационного сахарного диабета</h1>
  <form>
    <label>Концентрация аланина:</label>
    <input type="number" id="alanine" value="1">
    <br>
    <label>Концентрация аспаргина:</label>
    <input type="number" id="asparagine" value="1">
    <br>
    <label>Концентрация аспаргиновой кислоты:</label>
    <input type="number" id="aspartic_acid" value="1">
    <br>
    <label>Концентрация глицина:</label>
    <input type="number" id="glycine" value="1">
    <br>
    <label>Концентрация глутамина:</label>
    <input type="number" id="glutamine" value="1">
    <br>
    <label>Концентрация глутаминовой кислоты:</label>
    <input type="number" id="glutamic_acid" value="1">
    <br>
    <button id="calculate">Рассчитать</button>
    <p id="result"></p>
  </form>
  <script>
    // функция для расчета риска гестационного сахарного диабета
    function calculateGSDRisk(alanine, asparagine, aspartic_acid, glycine, glutamine, glutamic_acid) {
      var z = 288.780 + (1.326 * alanine) - (235.461 * aspartic_acid) - (14.813 * asparagine) - (4.032 * glycine) + (41.517 * glutamine) + (72.569 * glutamic_acid);
      var p = 1 / (1 + Math.exp(-z)) * 100;
      return p;
    }
    // функция для вывода результата
    function showResult(p) {
      if (p <= 0.557) {
        document.getElementById("result").innerHTML = "Высокий риск";
      } else {
        document.getElementById("result").innerHTML = "Низкий риск";
      }
    }
    // обработчик события для кнопки "Рассчитать"
    document.getElementById("calculate").addEventListener("click", function() {
      var alanine = parseFloat(document.getElementById("alanine").value);
      var asparagine = parseFloat(document.getElementById("asparagine").value);
      var aspartic_acid = parseFloat(document.getElementById("aspartic_acid").value);
      var glycine = parseFloat(document.getElementById("glycine").value);
      var glutamine = parseFloat(document.getElementById("glutamine").value);
      var glutamic_acid = parseFloat(document.getElementById("glutamic_acid").value);
      var p = calculateGSDRisk(alanine, asparagine, aspartic_acid, glycine, glutamine, glutamic_acid);
      showResult(p);
    });
  </script>
</body>
</html>
