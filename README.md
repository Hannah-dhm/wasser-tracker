<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Wasser Tracker</title>
    <style>
        body { font-family: Arial, sans-serif; text-align: center; padding: 20px; }
        
        .container {
            width: 200px;
            height: 300px;
            border: 2px solid blue;
            margin: auto;
            position: relative;
            background-color: rgba(0, 0, 255, 0.2);
        }

        .water {
            width: 100%;
            position: absolute;
            bottom: 0;
            background-color: blue;
            transition: height 0.3s ease-in-out;
        }

        .controls {
            display: flex;
            justify-content: center;
            align-items: center;
            margin-top: 20px;
            gap: 10px;
        }

        .button {
            background-color: blue;
            color: white;
            border: none;
            padding: 15px;
            font-size: 20px;
            width: 50px;
            cursor: pointer;
        }

        .button:disabled {
            background-color: gray;
            cursor: not-allowed;
        }

        .display {
            font-size: 24px;
            font-weight: bold;
            color: blue;
        }
    </style>
</head>
<body>

    <h1>Wasser Tracker</h1>

    <div class="container">
        <div class="water" id="water" style="height: 0%;"></div>
    </div>

    <div class="controls">
        <button class="button" id="minus">−</button>
        <span class="display" id="counter">0,0l</span>
        <button class="button" id="plus">+</button>
    </div>

    <script>
        let waterIntake = localStorage.getItem("water") ? parseFloat(localStorage.getItem("water")) : 0;
        const maxWater = 3.0;
        const step = 0.5;

        const waterDiv = document.getElementById("water");
        const counterSpan = document.getElementById("counter");
        const minusButton = document.getElementById("minus");
        const plusButton = document.getElementById("plus");

        function updateUI() {
            counterSpan.textContent = waterIntake.toFixed(1).replace('.', ',') + "l";
            const heightPercentage = (waterIntake / maxWater) * 100;
            waterDiv.style.height = heightPercentage + "%";

            minusButton.disabled = waterIntake === 0;
            plusButton.disabled = waterIntake >= maxWater;

            localStorage.setItem("water", waterIntake);
        }

        minusButton.addEventListener("click", () => {
            if (waterIntake > 0) {
                waterIntake -= step;
                updateUI();
            }
        });

        plusButton.addEventListener("click", () => {
            if (waterIntake < maxWater) {
                waterIntake += step;
                updateUI();
            }
        });

        updateUI();
    </script>

</body>
</html>

