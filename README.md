<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Digital Task Readiness Scoring</title>
    <style>
        body { font-family: Arial, sans-serif; margin: 40px; }
        h2 { color: #2e6c80; }
        label { display: block; margin: 10px 0 5px; }
        input[type=number] { width: 60px; padding: 5px; }
        button { margin-top: 20px; padding: 10px 20px; background-color: #2e6c80; color: white; border: none; cursor: pointer; }
        .result { margin-top: 20px; font-size: 1.2em; font-weight: bold; }
    </style>
</head>
<body>
    <h2>🧪 Digital Task Readiness Scoring</h2>

    <label for="objective">1. Objective Clarity (1–5):</label>
    <input type="number" id="objective" min="1" max="5">

    <label for="relevance">2. Consumer Relevance (1–5):</label>
    <input type="number" id="relevance" min="1" max="5">

    <label for="best_practice">3. Platform Best Practice (1–5):</label>
    <input type="number" id="best_practice" min="1" max="5">

    <label for="mroi">4. MROI / Effectiveness (1–5):</label>
    <input type="number" id="mroi" min="1" max="5">

    <label for="governance">5. Governance Check (1–5):</label>
    <input type="number" id="governance" min="1" max="5">

    <button onclick="calculateScore()">Calculate Readiness Score</button>

    <div class="result" id="result"></div>

    <script>
        function calculateScore() {
            const weights = { objective: 0.25, relevance: 0.20, best_practice: 0.20, mroi: 0.20, governance: 0.15 };
            let objective = parseInt(document.getElementById("objective").value);
            let relevance = parseInt(document.getElementById("relevance").value);
            let best_practice = parseInt(document.getElementById("best_practice").value);
            let mroi = parseInt(document.getElementById("mroi").value);
            let governance = parseInt(document.getElementById("governance").value);

            if ([objective, relevance, best_practice, mroi, governance].some(isNaN)) {
                document.getElementById("result").innerText = "❗ Please fill all scores (1–5).";
                return;
            }

            let score = (objective * weights.objective +
                         relevance * weights.relevance +
                         best_practice * weights.best_practice +
                         mroi * weights.mroi +
                         governance * weights.governance) * 20;

            let resultText = `✅ Your Readiness Score: ${score.toFixed(2)}%\n`;

            if (score >= 80) resultText += "🟢 Approved: Ready to go!";
            else if (score >= 60) resultText += "🟡 Needs Refinement: Review with the team.";
            else resultText += "🔴 Not Ready: Please reassess.";

            document.getElementById("result").innerText = resultText;
        }
    </script>
</body>
</html>
