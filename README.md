# Egg-opener-4
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Egg Opener Game</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            background-color: #f7f7f7;
            padding: 20px;
        }
        .button {
            padding: 15px 25px;
            font-size: 20px;
            color: #fff;
            background-color: #007BFF;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }
        .button:hover {
            background-color: #0056b3;
        }
        .output {
            margin-top: 20px;
            font-size: 24px;
            color: #333;
        }
        .pet-popup {
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background-color: white;
            border: 2px solid #ccc;
            border-radius: 10px;
            padding: 20px;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2);
            opacity: 0;
            animation: fadeInScale 0.7s forwards;
        }
        @keyframes fadeInScale {
            from {
                opacity: 0;
                transform: translate(-50%, -50%) scale(0.8);
            }
            to {
                opacity: 1;
                transform: translate(-50%, -50%) scale(1);
            }
        }
        /* Confetti Animation */
        .confetti {
            position: fixed;
            top: 0;
            left: 50%;
            transform: translateX(-50%);
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 10;
        }
        .confetti-piece {
            position: absolute;
            width: 10px;
            height: 20px;
            background-color: #FFC107;
            animation: fall 2s ease-out infinite;
        }
        @keyframes fall {
            0% {
                transform: translateY(-100px) rotate(0deg);
            }
            100% {
                transform: translateY(100vh) rotate(360deg);
            }
        }
        .pet-list {
            margin-top: 20px;
            text-align: left;
            margin-left: auto;
            margin-right: auto;
            max-width: 600px;
        }
        .pet-list table {
            width: 100%;
            border-collapse: collapse;
        }
        .pet-list th, .pet-list td {
            border: 1px solid #ccc;
            padding: 8px;
            text-align: center;
        }
        .pet-list th {
            background-color: #007BFF;
            color: white;
        }
    </style>
</head>
<body>
    <h1>Egg Opener Simulator</h1>
    <button class="button" onclick="openEgg()">Open Egg</button>
    <div class="output" id="output">Click the button to open an egg!</div>
    <div id="popupContainer"></div>
    <div class="confetti" id="confettiContainer"></div>

    <div class="pet-list">
        <h2>Pet Collection</h2>
        <table>
            <thead>
                <tr>
                    <th>Pet</th>
                    <th>Probability</th>
                    <th>Count</th>
                </tr>
            </thead>
            <tbody id="petTableBody">
                <!-- Pet rows will be populated here -->
            </tbody>
        </table>
    </div>

    <script>
        // Pets and their probabilities
        const pets = [
            { name: "Common Cat", chance: 60.0, count: 0 },
            { name: "Common Dog", chance: 20.0, count: 0 },
            { name: "Uncommon Bird", chance: 10.0, count: 0 },
            { name: "Rare Fox", chance: 5.0, count: 0 },
            { name: "Epic Dragon", chance: 2.5, count: 0 },
            { name: "Legendary Unicorn", chance: 1.0, count: 0 },
            { name: "Mythic Phoenix", chance: 0.5, count: 0 },
            { name: "Divine Tiger", chance: 0.25, count: 0 },
            { name: "Godly Wolf", chance: 0.1, count: 0 },
            { name: "Celestial Whale", chance: 0.05, count: 0 },
            { name: "Stellar Griffin", chance: 0.02, count: 0 },
            { name: "Galactic Serpent", chance: 0.01, count: 0 },
            { name: "Astral Beast", chance: 0.005, count: 0 },
            { name: "Ethereal Spirit", chance: 0.001, count: 0 },
            { name: "Ultimate Egglord", chance: 0.00001, count: 0 },
        ];

        // Calculate total chance
        const totalChance = pets.reduce((sum, pet) => sum + pet.chance, 0);

        // Initialize pet table
        const petTableBody = document.getElementById("petTableBody");
        pets.forEach(pet => {
            const row = document.createElement("tr");
            row.innerHTML = `<td>${pet.name}</td><td>${pet.chance}%</td><td id="${pet.name}-count">0</td>`;
            petTableBody.appendChild(row);
        });

        // Function to draw a random pet
        function openEgg() {
            const random = Math.random() * totalChance;
            let cumulativeChance = 0;

            for (const pet of pets) {
                cumulativeChance += pet.chance;
                if (random <= cumulativeChance) {
                    pet.count++;
                    document.getElementById(`${pet.name}-count`).innerText = pet.count;
                    showPopup(pet.name);
                    showConfetti();
                    return;
                }
            }
        }

        // Function to display popup with animation
        function showPopup(petName) {
            const popupContainer = document.getElementById("popupContainer");

            // Clear previous popup
            popupContainer.innerHTML = "";

            // Create popup element
            const popup = document.createElement("div");
            popup.className = "pet-popup";
            popup.textContent = `You got: ${petName}`;

            // Add popup to container
            popupContainer.appendChild(popup);

            // Remove popup after 3 seconds
            setTimeout(() => {
                popup.remove();
            }, 3000);
        }

        // Function to show confetti animation
        function showConfetti() {
            const confettiContainer = document.getElementById("confettiContainer");

            // Clear existing confetti
            confettiContainer.innerHTML = "";

            // Generate confetti pieces
            for (let i = 0; i < 100; i++) {
                const confetti = document.createElement("div");
                confetti.className = "confetti-piece";
                confetti.style.left = Math.random() * 100 + "vw";
                confetti.style.backgroundColor = `hsl(${Math.random() * 360}, 100%, 50%)`;
                confetti.style.animationDuration = Math.random() * 
            }

            // Remove confetti after 3 seconds
            setTimeout(() => {
                confettiContainer.innerHTML = "";
            }, 3000);
        }
    </script>
</body>
</html>
