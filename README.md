<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Kalkulator Warna Ungu</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            height: 100vh;
            margin: 0;
            background-color: #d9aeeb;
        }
        .calculator {
            background-color: #a364b6;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 0 20px rgba(0, 0, 0, 0.1);
            width: 300px;
            text-align: center;
        }
        #display {
            width: 90%;
            height: 40px;
            text-align: right;
            padding: 10px;
            margin-bottom: 10px;
            font-size: 18px;
            border: 2px solid #aa6be6;
            border-radius: 5px;
            background-color: #fff;
        }
        .buttons {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 10px;
        }
        button {
            padding: 20px;
            font-size: 18px;
            border: none;
            border-radius: 5px;
            background-color: #dcdcff;
            color: #4b0082;
            cursor: pointer;
            font-weight: bold;
        }
        button:hover {
            background-color: #b0a7f1;
        }
        button.equals {
            background-color: #834fb3;
            color: white;
        }
        button.equals:hover {
            background-color: #6a0dad;
        }
        #fact {
            margin-top: 20px;
            font-size: 16px;
            color: #4b0082;
        }
    </style>
</head>
<body>
    <div class="calculator">
        <input type="text" id="display" disabled>
        <div class="buttons">
            <button onclick="appendOperator('+')">+</button>
            <button onclick="appendNumber(7)">7</button>
            <button onclick="appendNumber(8)">8</button>
            <button onclick="appendNumber(9)">9</button>
            <button onclick="appendOperator('-')">-</button>
            <button onclick="appendNumber(4)">4</button>
            <button onclick="appendNumber(5)">5</button>
            <button onclick="appendNumber(6)">6</button>
            <button onclick="appendOperator('*')">x</button>
            <button onclick="appendNumber(1)">1</button>
            <button onclick="appendNumber(2)">2</button>
            <button onclick="appendNumber(3)">3</button>
            <button onclick="appendOperator('/')">/</button>
            <button onclick="clearDisplay()">C</button>
            <button onclick="appendNumber(0)">0</button>
            <button class="equals" onclick="calculate()">=</button>
        </div>
    </div>
    <p id="fact"></p>
    <script>
        let display = document.getElementById('display');
        let fact = document.getElementById('fact');

        function appendNumber(number) {
            display.value += number;
        }

        function appendOperator(operator) {
            display.value += operator;
        }

        function clearDisplay() {
            display.value = '';
            fact.innerText = '';
        }

        function calculate() {
            try {
                let result = eval(display.value);
                display.value = result;
                fetchFact(result);
            } catch (error) {
                alert("Input tidak valid");
                clearDisplay();
            }
        }

        function fetchFact(number) {
            fetch(`http://numbersapi.com/${number}`)
                .then(response => response.text())
                .then(data => fact.innerText = `Fakta: ${data}`)
                .catch(error => fact.innerText = "Tidak dapat mengambil fakta");
        }
    </script>
</body>
</html>
