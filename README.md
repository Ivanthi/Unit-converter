<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Unit Converter</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f0f0f0;
      display: flex;
      justify-content: center;
      margin-top: 50px;
    }

    .converter {
      background: #fff;
      padding: 25px;
      border-radius: 12px;
      box-shadow: 0 0 15px rgba(0,0,0,0.2);
      width: 300px;
    }

    .converter h2 {
      text-align: center;
    }

    .converter label,
    .converter select,
    .converter input {
      display: block;
      width: 100%;
      margin: 10px 0;
    }
  </style>
</head>
<body>
  <div class="converter">
    <h2>Unit Converter</h2>

    <label for="category">Select Category:</label>
    <select id="category" onchange="updateUnits()">
      <option value="length">Length</option>
      <option value="weight">Weight</option>
    </select>

    <label for="fromUnit">From:</label>
    <select id="fromUnit"></select>

    <label for="toUnit">To:</label>
    <select id="toUnit"></select>

    <label for="inputValue">Value:</label>
    <input type="number" id="inputValue" oninput="convert()">

    <h3>Result: <span id="result">0</span></h3>
  </div>

  <script>
    const units = {
      length: {
        meter: 1,
        kilometer: 0.001,
        mile: 0.000621371
      },
      weight: {
        gram: 1,
        kilogram: 0.001,
        pound: 0.00220462
      }
    };

    function updateUnits() {
      const category = document.getElementById("category").value;
      const fromSelect = document.getElementById("fromUnit");
      const toSelect = document.getElementById("toUnit");

      fromSelect.innerHTML = "";
      toSelect.innerHTML = "";

      for (let unit in units[category]) {
        fromSelect.innerHTML += `<option value="${unit}">${unit}</option>`;
        toSelect.innerHTML += `<option value="${unit}">${unit}</option>`;
      }

      convert();
    }

    function convert() {
      const category = document.getElementById("category").value;
      const fromUnit = document.getElementById("fromUnit").value;
      const toUnit = document.getElementById("toUnit").value;
      const inputValue = parseFloat(document.getElementById("inputValue").value);
      const resultSpan = document.getElementById("result");

      if (isNaN(inputValue)) {
        resultSpan.textContent = "0";
        return;
      }

      const baseValue = inputValue * units[category][fromUnit];
      const convertedValue = baseValue / units[category][toUnit];

      resultSpan.textContent = convertedValue.toFixed(4);
    }

    window.onload = updateUnits;
  </script>
</body>
</html>
