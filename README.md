<!DOCTYPE html>
<html lang="en">
<head>
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Calculator</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            font-family: 'Poppins', sans-serif;
            box-sizing: border-box;
        }

        .container {
            width: 100%;
            height: 100vh;
            background: #e3e3e3;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .calculator {
            background: #3a4452;
            padding: 20px;
            border-radius: 10px;
        }

        .calculator form input {
            border: 0;
            outline: 0;
            width: 60px;
            height: 60px;
            border-radius: 10px;
            box-shadow: -8px -8px 15px rgba(255, 255, 255, 0.1), 5px 5px 15px rgba(0, 0, 0, 0.2);
            background: transparent;
            font-size: 20px;
            color: #fff;
            cursor: pointer;
            margin: 10px;
        }

        form .display {
            display: flex;
            justify-content: flex-end;
            margin: 20px 0;
        }

        form .display input {
            text-align: right;
            flex: 1;
            font-size: 45px;
            box-shadow: none;
        }

        form input.equal {
            width: 145px;
        }

        form input.operator {
            color: #33ffd8;
        }

        .history {
            border: 1px solid #ccc;
            padding: 10px;
            margin-top: 10px;
            max-height: 150px;
            overflow-y: auto;
            background-color: #f9f9f9;
            border-radius: 5px;
            color: #333;
            font-size: 14px;
        }

        .history div {
            margin: 5px 0;
            font-size: 14px;
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="calculator">
            <form>
                <div class="display">
                    <input type="text" name="display" id="display" readonly>
                </div>
                <div>
                    <input type="button" value="AC" onclick="clearDisplay()" class="operator">
                    <input type="button" value="DE" onclick="deleteLast()" class="operator">
                    <input type="button" value="." onclick="appendToDisplay('.')" class="operator">
                    <input type="button" value=":" onclick="appendToDisplay(':')" class="operator"> <!-- Changed / to : -->
                </div>
                <div>
                    <input type="button" value="7" onclick="appendToDisplay('7')">
                    <input type="button" value="8" onclick="appendToDisplay('8')">
                    <input type="button" value="9" onclick="appendToDisplay('9')">
                    <input type="button" value="x" onclick="appendToDisplay('x')">
                </div>
                <div>
                    <input type="button" value="4" onclick="appendToDisplay('4')">
                    <input type="button" value="5" onclick="appendToDisplay('5')">
                    <input type="button" value="6" onclick="appendToDisplay('6')">
                    <input type="button" value="-" onclick="appendToDisplay('-')">
                </div>
                <div>
                    <input type="button" value="1" onclick="appendToDisplay('1')">
                    <input type="button" value="2" onclick="appendToDisplay('2')">
                    <input type="button" value="3" onclick="appendToDisplay('3')">
                    <input type="button" value="+" onclick="appendToDisplay('+')">
                </div>
                <div>
                    <input type="button" value="00" onclick="appendToDisplay('00')">
                    <input type="button" value="0" onclick="appendToDisplay('0')">
                    <input type="button" value="=" onclick="calculate()" class="equal operator">
                </div>
            </form>
            <div class="history" id="history"></div>
        </div>
    </div>

    <script>
        // Fungsi untuk menambahkan input ke layar kalkulator
        function appendToDisplay(value) {
            let display = document.getElementById('display');
            display.value += value;
        }

        // Fungsi untuk menghapus seluruh tampilan
        function clearDisplay() {
            document.getElementById('display').value = '';
        }

        // Fungsi untuk menghapus karakter terakhir pada tampilan
        function deleteLast() {
            let display = document.getElementById('display');
            display.value = display.value.slice(0, -1);
        }

        // Fungsi untuk menghitung ekspresi dan menambahkan ke riwayat
        function calculate() {
            let display = document.getElementById('display');
            let expression = display.value;

            // Ganti 'x' dengan '*' dan ':' dengan '/' untuk evaluasi matematika
            expression = expression.replace(/x/g, '*').replace(/:/g, '/');

            if (expression) {
                try {
                    let result = eval(expression);
                    display.value = result;
                    addHistory(expression + ' = ' + result);
                } catch (e) {
                    display.value = 'Error';
                }
            }
        }

        // Fungsi untuk menambahkan perhitungan ke dalam riwayat
        function addHistory(entry) {
            let historyDiv = document.getElementById('history');
            let historyItem = document.createElement('div');
            historyItem.textContent = entry;
            historyDiv.appendChild(historyItem);

            // Batasi riwayat hingga 10 entri
            if (historyDiv.children.length > 10) {
                historyDiv.removeChild(historyDiv.firstChild);
            }
        }
    </script>
</body>
</html>
