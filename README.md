<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Wasser Tracker</title>
    <style>
        body { font-family: Arial, sans-serif; text-align: center; }
        .tracker { font-size: 2em; margin: 20px; }
        .button { font-size: 1.5em; padding: 10px; cursor: pointer; }
    </style>
</head>
<body>
    <h1>Wasser Tracker</h1>
    <div class="tracker">Getrunken: <span id="counter">0</span> L</div>
    <button class="button" onclick="addWater(0.25)">+250ml</button>
    <button class="button" onclick="resetWater()">Reset</button>

    <script>
        let waterIntake = localStorage.getItem("water") || 0;
        document.getElementById("counter").textContent = waterIntake;

        function addWater(amount) {
            waterIntake = parseFloat(waterIntake) + amount;
            localStorage.setItem("water", waterIntake);
            document.getElementById("counter").textContent = waterIntake;
        }

        function resetWater() {
            waterIntake = 0;
            localStorage.setItem("water", waterIntake);
            document.getElementById("counter").textContent = waterIntake;
        }
    </script>
</body>
</html>
