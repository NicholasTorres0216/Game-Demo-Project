<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Pet Gacha Clicker Prototype</title>
    <link href="https://fonts.googleapis.com/css2?family=Fredoka+One&family=Open+Sans:wght@400;700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Open Sans', sans-serif;
            background-color: #fce4ec;
            color: #333;
            text-align: center;
            padding: 20px;
        }

        header {
            background-color: #ff80ab;
            padding: 10px;
            border-radius: 10px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
            margin-bottom: 20px;
        }

        h1 {
            font-family: 'Fredoka One', cursive;
            color: #fff;
            font-size: 2.5em;
            margin: 0;
        }

        #game-container {
            max-width: 900px;
            margin: 0 auto;
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 20px;
        }

        .panel {
            background-color: #fff;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
            text-align: left;
        }

        .instructions {
            grid-column: 1 / 3;
            background-color: #ffe5f1;
        }

        .instructions h2, .stats h2, .gallery h2 {
            font-family: 'Fredoka One', cursive;
            color: #e91e63;
            margin-top: 0;
            border-bottom: 2px solid #f48fb1;
            padding-bottom: 5px;
        }

        .click-section {
            grid-column: 1 / 3;
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 10px;
        }

        #click-button {
            background-color: #81c784;
            color: white;
            font-family: 'Fredoka One', cursive;
            font-size: 3em;
            padding: 40px;
            border: none;
            border-radius: 50%;
            cursor: pointer;
            box-shadow: 0 8px #689f38;
            transition: all 0.1s;
            outline: none;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            width: 200px;
            height: 200px;
            position: relative;
        }

        #click-button:active {
            box-shadow: 0 4px #689f38;
            transform: translateY(4px);
        }

        #click-button .icon {
            font-size: 2em;
            line-height: 1;
        }
        #click-button .text {
            font-size: 0.5em;
        }

        .roll-section {
            grid-column: 1 / 3;
            text-align: center;
        }

        #roll-button {
            background-color: #4fc3f7;
            color: white;
            font-family: 'Fredoka One', cursive;
            font-size: 1.5em;
            padding: 15px 30px;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            box-shadow: 0 4px #0288d1;
            transition: all 0.1s;
        }

        #roll-button:disabled {
            background-color: #b0bec5;
            box-shadow: 0 4px #78909c;
            cursor: not-allowed;
        }

        #roll-button:enabled:active {
            box-shadow: 0 2px #0288d1;
            transform: translateY(2px);
        }

        #roll-result {
            margin-top: 15px;
            font-size: 1.2em;
            font-weight: bold;
            color: #e91e63;
        }

        #pet-gallery {
            display: flex;
            flex-wrap: wrap;
            gap: 15px;
            justify-content: center;
            margin-top: 15px;
        }

        .pet-card {
            border: 3px solid #f48fb1;
            border-radius: 10px;
            padding: 10px;
            text-align: center;
            width: 120px;
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2);
            transition: transform 0.2s;
            background-color: #fff;
            position: relative;
            overflow: hidden;
        }

        .pet-card.owned {
            border-color: #4caf50;
            background-color: #e8f5e9;
        }

        .pet-card img {
            width: 100px;
            height: 100px;
            object-fit: cover;
            border-radius: 5px;
        }

        .pet-card .rarity {
            font-size: 0.8em;
            font-weight: bold;
            margin-top: 5px;
            padding: 2px 5px;
            border-radius: 4px;
            color: #fff;
        }

        .rarity-common { background-color: #64b5f6; }
        .rarity-uncommon { background-color: #ffb74d; }
        .rarity-rare { background-color: #9575cd; }
        .rarity-epic { background-color: #e57373; }

        .not-owned::before {
            content: "???";
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background-color: rgba(0, 0, 0, 0.8);
            color: white;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 2em;
            font-family: 'Fredoka One', cursive;
            z-index: 10;
        }
    </style>
</head>
<body>

    <header>
        <h1>🌟 Pet Gacha Clicker 🐾</h1>
    </header>

    <div id="game-container">
        <div class="panel instructions">
            <h2>📜 How to Play</h2>
            <ul>
                <li>Click the **Big Paw Button** to earn Clicks (1 click per press).</li>
                <li>Spend **10 Clicks** to **Roll** for a new Pet.</li>
                <li>Collect all the unique, adorable pets!</li>
            </ul>
        </div>
        
        <div class="panel stats">
            <h2>📊 Game Stats</h2>
            <p>Total Clicks: <span id="click-count">0</span></p>
            <p>Unique Pets Collected: <span id="unique-pets-count">0</span> / <span id="total-pets">0</span></p>
        </div>
        
        <div class="click-section">
            <button id="click-button" aria-label="Click to earn Clicks">
                <span class="icon">🐾</span>
                <span class="text">Click Me!</span>
            </button>
        </div>

        <div class="roll-section">
            <button id="roll-button" disabled>Roll for Pet (10 Clicks)</button>
            <div id="roll-result"></div>
        </div>

        <div class="panel gallery">
            <h2>🖼️ Pet Collection Gallery</h2>
            <div id="pet-gallery">
            </div>
        </div>

    </div>

    <script>
        document.addEventListener('DOMContentLoaded', () => {
            const PET_IMAGES = [
                { id: 1, name: "Cool Cabbage Cat", file: "Cat Picture 1.jpg", rarity: "Common" },
                { id: 2, name: "Unicorn Shiba", file: "pexels-shvetsa-4588049.jpg", rarity: "Common" },
                { id: 3, name: "Big Smile Chihuahua", file: "images.jfif", rarity: "Uncommon" },
                { id: 4, name: "Sunset Flower Retriever", file: "b05c4816a3b4d1d0c57e2a67592b5084.jpg", rarity: "Uncommon" },
                
                // --- Rarity Swap ---
                { id: 5, name: "Propeller Hat Pup", file: "dog-cute.gif", rarity: "Epic" }, // NEW EPIC! (2% chance)
                { id: 6, name: "Golden Phoenix Dog", file: "dog-cute-rare.jpg", rarity: "Rare" } // NEW RARE! (8% chance)
                // -------------------
            ];

            const ROLL_COST = 10;
            let clicks = 0;
            let ownedPets = {};

            const clickCountEl = document.getElementById('click-count');
            const uniquePetsCountEl = document.getElementById('unique-pets-count');
            const totalPetsEl = document.getElementById('total-pets');
            const clickButton = document.getElementById('click-button');
            const rollButton = document.getElementById('roll-button');
            const rollResultEl = document.getElementById('roll-result');
            const galleryEl = document.getElementById('pet-gallery');
            
            totalPetsEl.textContent = PET_IMAGES.length;

            function updateUI() {
                clicks = Math.max(0, clicks);
                clickCountEl.textContent = clicks;

                const uniqueCount = Object.keys(ownedPets).length;
                uniquePetsCountEl.textContent = uniqueCount;

                rollButton.disabled = clicks < ROLL_COST;
            }

            function handleClick() {
                clicks += 1;
                updateUI();
            }

            function rollForPet() {
                const rand = Math.random() * 100;

                let selectedPet;

                if (rand < 2) {
                    const epics = PET_IMAGES.filter(p => p.rarity === "Epic");
                    selectedPet = epics[Math.floor(Math.random() * epics.length)];
                } else if (rand < 10) {
                    const rares = PET_IMAGES.filter(p => p.rarity === "Rare");
                    selectedPet = rares[Math.floor(Math.random() * rares.length)];
                } else if (rand < 40) {
                    const uncommons = PET_IMAGES.filter(p => p.rarity === "Uncommon");
                    selectedPet = uncommons[Math.floor(Math.random() * uncommons.length)];
                } else {
                    const commons = PET_IMAGES.filter(p => p.rarity === "Common");
                    selectedPet = commons[Math.floor(Math.random() * commons.length)];
                }
                
                return selectedPet;
            }

            function handleRoll() {
                if (clicks < ROLL_COST) return;

                clicks -= ROLL_COST;

                const pet = rollForPet();
                const isNew = !ownedPets[pet.id];

                ownedPets[pet.id] = true;
                updateGallery(pet.id);

                updateUI();

                let message = `You rolled the ${pet.rarity} **${pet.name}**! `;
                if (isNew) {
                    message += "🎉 **NEW PET!** 🎉";
                } else {
                    message += "(Duplicate)";
                }
                rollResultEl.innerHTML = message;
            }
            
            function initGallery() {
                galleryEl.innerHTML = '';
                PET_IMAGES.forEach(pet => {
                    const petCard = document.createElement('div');
                    petCard.className = 'pet-card';
                    petCard.id = `pet-${pet.id}`;
                    
                    if (!ownedPets[pet.id]) {
                        petCard.classList.add('not-owned');
                    } else {
                        petCard.classList.add('owned');
                    }

                    petCard.innerHTML = `
                        <img src="${pet.file}" alt="${pet.name}">
                        <div class="name">${pet.name}</div>
                        <div class="rarity rarity-${pet.rarity.toLowerCase()}">${pet.rarity}</div>
                    `;
                    
                    galleryEl.appendChild(petCard);
                });
            }

            function updateGallery(petId) {
                const card = document.getElementById(`pet-${petId}`);
                if (card) {
                    card.classList.remove('not-owned');
                    card.classList.add('owned');
                }
            }
            
            clickButton.addEventListener('click', handleClick);
            rollButton.addEventListener('click', handleRoll);

            initGallery();
            updateUI();
        });
    </script>
</body>
</html>
