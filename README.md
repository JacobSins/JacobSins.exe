<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Hacker Calculator</title>
    <style>
        body {
            font-family: 'Courier New', Courier, monospace;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            background-color: #0f0f0f;
            color: #33ff33;
            margin: 0;
        }

        .calculator {
            background-color: #1a1a1a;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0px 0px 15px rgba(0, 255, 0, 0.7);
        }

        .display {
            width: 100%;
            padding: 15px;
            font-size: 24px;
            margin-bottom: 20px;
            text-align: right;
            border: 1px solid #33ff33;
            border-radius: 5px;
            background-color: #000;
            color: #33ff33;
        }

        .buttons {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 10px;
        }

        .buttons button {
            padding: 20px;
            font-size: 18px;
            cursor: pointer;
            border: none;
            border-radius: 5px;
            background-color: #0f0f0f;
            color: #33ff33;
            box-shadow: 0 0 10px rgba(0, 255, 0, 0.5);
        }

        .buttons button:hover {
            background-color: #33ff33;
            color: #000;
        }

        .equal {
            background-color: #33ff33;
            color: #000;
            grid-column: 4 / 5;
            grid-row: span 2;
        }

        .equal:hover {
            background-color: #29cc29;
        }

        .clear {
            background-color: #ff3333;
            color: #000;
            grid-column: span 2;
        }

        .clear:hover {
            background-color: #ff6666;
        }

        .zero {
            grid-column: span 2;
        }
    </style>
</head>
<body>
    <div class="calculator">
        <input type="text" id="result" class="display" disabled>
        <div class="buttons">
            <button onclick="clearDisplay()" class="clear">C</button>
            <button onclick="appendToDisplay('/')">/</button>
            <button onclick="appendToDisplay('*')">*</button>
            <button onclick="appendToDisplay('-')">-</button>
            
            <button onclick="appendToDisplay('7')">7</button>
            <button onclick="appendToDisplay('8')">8</button>
            <button onclick="appendToDisplay('9')">9</button>
            <button onclick="appendToDisplay('+')">+</button>
            
            <button onclick="appendToDisplay('4')">4</button>
            <button onclick="appendToDisplay('5')">5</button>
            <button onclick="appendToDisplay('6')">6</button>
            
            <button onclick="appendToDisplay('1')">1</button>
            <button onclick="appendToDisplay('2')">2</button>
            <button onclick="appendToDisplay('3')">3</button>
            
            <button onclick="appendToDisplay('0')" class="zero">0</button>
            <button onclick="appendToDisplay('.')">.</button>
            <button onclick="calculate()" class="equal">=</button>
        </div>
    </div>

    <script>
        function appendToDisplay(value) {
            document.getElementById('result').value += value;
        }

        function clearDisplay() {
            document.getElementById('result').value = '';
        }

        function calculate() {
            let expression = document.getElementById('result').value;
            if (expression === '1+1') {
                document.getElementById('result').value = 'I love you';
            } else {
                try {
                    document.getElementById('result').value = eval(expression);
                } catch {
                    document.getElementById('result').value = 'Error';
                }
            }
        }
    </script>
</body>
</html>
