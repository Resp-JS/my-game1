<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <title>Угадай число</title>

    <style>
        body {
            font-family: Arial, sans-serif;
            background: linear-gradient(135deg, #1e1e2f, #2c2c54);
            color: white;
            text-align: center;
            margin-top: 100px;
        }

        .game-box {
            background: #2f2f4f;
            padding: 30px;
            border-radius: 15px;
            display: inline-block;
            box-shadow: 0 0 20px rgba(0,0,0,0.5);
        }

        input {
            padding: 10px;
            font-size: 16px;
            border-radius: 8px;
            border: none;
            margin-top: 10px;
        }

        button {
            padding: 10px 20px;
            margin-top: 10px;
            border: none;
            border-radius: 10px;
            background: #4CAF50;
            color: white;
            font-size: 16px;
            cursor: pointer;
            transition: 0.2s;
        }

        button:hover {
            background: #45a049;
            transform: scale(1.05);
        }

        .reset-btn {
            background: #ff4757;
        }

        .reset-btn:hover {
            background: #e84118;
        }
    </style>
</head>

<body>

<div class="game-box">
    <h1>🎮 Угадай число</h1>
    <p>Я загадал число от 1 до 100</p>

    <input type="number" id="guess" placeholder="Введи число">
    <br>

    <button onclick="checkGuess()">Проверить</button>
    <button class="reset-btn" onclick="resetGame()">🔁 Заново</button>

    <p id="result"></p>
    <p id="attempts">Попыток: 0</p>
    <p id="record">🏆 Рекорд: —</p>
</div>

<script>
    let number;
    let attempts;

    function startGame() {
        number = Math.floor(Math.random() * 100) + 1;
        attempts = 0;
        document.getElementById("result").textContent = "";
        document.getElementById("attempts").textContent = "Попыток: 0";
        document.getElementById("guess").value = "";
    }

    function checkGuess() {
        let guess = Number(document.getElementById("guess").value);
        let result = document.getElementById("result");

        if (!guess) {
            result.textContent = "❌ Введи число!";
            return;
        }

        attempts++;

        if (guess < number) {
            result.textContent = "📉 Загаданное число больше!";
        } else if (guess > number) {
            result.textContent = "📈 Загаданное число меньше!";
        } else {
            result.textContent = "🎉 Ты угадал!";

            let record = localStorage.getItem("record");

            if (!record || attempts < record) {
                localStorage.setItem("record", attempts);
                document.getElementById("record").textContent = "🏆 Рекорд: " + attempts;
            }
        }

        document.getElementById("attempts").textContent = "Попыток: " + attempts;
    }

    function resetGame() {
        startGame();
    }

    function loadRecord() {
        let record = localStorage.getItem("record");
        if (record) {
            document.getElementById("record").textContent = "🏆 Рекорд: " + record;
        }
    }

    startGame();
    loadRecord();
</script>

</body>
</html>
