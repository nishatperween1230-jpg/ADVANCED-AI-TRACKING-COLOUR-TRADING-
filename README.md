<!DOCTYPE html>
<html>
<head>
    <title>AI Pattern Analyzer PRO</title>

    <style>
        body {
            font-family: Arial;
            text-align: center;
            background: linear-gradient(135deg, #141e30, #243b55);
            color: white;
        }

        h1 {
            margin-top: 20px;
        }

        button {
            padding: 15px 25px;
            margin: 8px;
            font-size: 18px;
            border-radius: 12px;
            border: none;
            cursor: pointer;
        }

        .big { background: #00e676; color: black; }
        .small { background: #ff1744; }
        .clear { background: gray; }

        .card {
            background: rgba(255,255,255,0.1);
            margin: 15px;
            padding: 15px;
            border-radius: 15px;
        }

        #result {
            font-size: 22px;
            font-weight: bold;
            margin-top: 15px;
        }

        input {
            padding: 10px;
            border-radius: 10px;
            border: none;
            text-align: center;
        }
    </style>
</head>

<body>

<h1>🤖 AI Pattern Analyzer PRO</h1>

<div class="card">
    <button class="big" onclick="add('B')">BIG</button>
    <button class="small" onclick="add('S')">SMALL</button>
    <button class="clear" onclick="reset()">CLEAR</button>
</div>

<div class="card">
    <h3>📊 Last 5 (Latest → Oldest)</h3>
    <p id="history"></p>
</div>

<div id="result">Enter at least 5 results</div>

<div class="card">
    <h3>💰 Balance</h3>
    <input type="number" id="money" placeholder="Enter money">
    <p id="advice"></p>
</div>

<script>

let data = [];

function add(val) {
    data.push(val);
    update();
}

function reset() {
    data = [];
    update();
}

function update() {

    let last5 = data.slice(-5).reverse();

    // ✅ FIX: no extra space
    document.getElementById("history").innerText = last5.join(" | ");

    if (data.length < 5) {
        document.getElementById("result").innerText = "Enter at least 5 results";
        return;
    }

    let real = data.slice(-5);

    let countB = real.filter(x => x === 'B').length;
    let countS = real.filter(x => x === 'S').length;

    let resultText = "";

    if (countB >= 4) {
        resultText = "🔥 HIGH CHANCE → BIG";
    }
    else if (countS >= 4) {
        resultText = "🔥 HIGH CHANCE → SMALL";
    }
    else if (countB === 3) {
        resultText = "⚡ MEDIUM CHANCE → BIG";
    }
    else if (countS === 3) {
        resultText = "⚡ MEDIUM CHANCE → SMALL";
    }
    else {
        resultText = "❌ NO CLEAR PATTERN";
    }

    document.getElementById("result").innerText = resultText;

    moneyAdvice();
}

function moneyAdvice() {
    let money = document.getElementById("money").value;

    if (money == "" || money <= 0) {
        document.getElementById("advice").innerText = "❌ No money → Don't bet";
    } 
    else if (money < 50) {
        document.getElementById("advice").innerText = "⚠️ Low balance → Play small";
    } 
    else {
        document.getElementById("advice").innerText = "✅ Safe to play smart";
    }
}

</script>

</body>
</html>
