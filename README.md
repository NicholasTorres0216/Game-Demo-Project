<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Pet Gacha Clicker Pro</title>
    <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&family=Montserrat:wght@600&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Roboto', sans-serif;
            background-color: #f4f7f6;
            color: #333;
            text-align: center;
            padding: 20px;
        }

        header {
            background-color: #2c3e50;
            padding: 15px;
            border-radius: 8px;
            margin-bottom: 30px;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
        }

        h1 {
            font-family: 'Montserrat', sans-serif;
            color: #ecf0f1;
            font-size: 2.2em;
            margin: 0;
            letter-spacing: 1px;
        }

        #game-container {
            max-width: 1000px;
            margin: 0 auto;
            display: grid;
            grid-template-columns: 1fr 2fr;
            gap: 25px;
        }

        .panel {
            background-color: #fff;
            padding: 25px;
            border-radius: 8px;
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
            text-align: left;
        }

        h2 {
            font-family: 'Montserrat', sans-serif;
            color: #34495e;
            margin-top: 0;
            border-bottom: 2px solid #bdc3c7;
            padding-bottom: 10px;
            font-size: 1.5em;
        }

        .left-column {
            display: flex;
            flex-direction: column;
            gap: 25px;
        }

        .instructions ul {
            list-style: disc;
            padding-left: 20px;
            margin: 10px 0 0 0;
            line-height: 1.6;
        }
        
        .stats p {
            font-size: 1.1em;
            margin: 8px 0;
        }
        .stats span {
            font-weight: 700;
            color: #2980b9;
        }
        
        .click-section {
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 15px;
        }

        #click-button {
            background-color: #2ecc71;
            color: white;
            font-family: 'Montserrat', sans-serif;
            font-size: 3.5em;
            padding: 50px;
            border: none;
            border-radius: 50%;
            cursor: pointer;
            box-shadow: 0 8px #27ae60;
            transition: all 0.1s;
            outline: none;
            width: 180px;
            height: 180px;
            position: relative;
            margin-top: 15px;
            display: flex;
            align-items: center;
            justify-content: center;
            text-shadow: 1px 1px 2px rgba(0,0,0,0.2);
        }

        #click-button:active {
            box-shadow: 0 4px #27ae60;
            transform: translateY(4px);
        }

        #roll-button {
            background-color: #3498db;
            color: white;
            font-family: 'Montserrat', sans-serif;
            font-size: 1.3em;
            padding: 12px 25px;
            border: none;
            border-radius: 6px;
            cursor: pointer;
            box-shadow: 0 3px #2980b9;
            transition: all 0.1s;
            width: 100%;
            max-width: 300px;
        }

        #roll-button:disabled {
            background-color: #bdc3c7;
            box-shadow: 0 3px #95a5a6;
            cursor: not-allowed;
        }

        #roll-button:enabled:active {
            box-shadow: 0 1px #2980b9;
            transform: translateY(2px);
        }

        #roll-result {
            margin-top: 15px;
            font-size: 1.1em;
            font-weight: bold;
            color: #e74c3c;
            min-height: 20px;
        }
        
        #let-it-ride-message {
            color: #e67e22;
            font-family: 'Montserrat', sans-serif;
            font-size: 1.2em;
            margin-top: 5px;
            min-height: 25px;
        }

        .gallery {
            grid-column: 2 / 3;
        }

        #pet-gallery {
            display: flex;
            flex-wrap: wrap;
            gap: 15px;
            justify-content: flex-start;
            margin-top: 15px;
        }

        .pet-card {
            border: 1px solid #ddd;
            border-radius: 6px;
            padding: 8px;
            text-align: center;
            width: 100px;
            box-shadow: 0 1px 3px rgba(0, 0, 0, 0.05);
            background-color: #fcfcfc;
            position: relative;
            overflow: hidden;
        }

        .pet-card.owned {
            border-color: #2ecc71;
            background-color: #f0fff0;
        }

        .pet-card img {
            width: 90px;
            height: 90px;
            object-fit: cover;
            border-radius: 4px;
        }

        .pet-card .name {
            font-size: 0.8em;
            font-weight: 700;
            margin-top: 5px;
            height: 2.2em;
            line-height: 1.1;
        }
        
        .pet-card .rarity {
            font-size: 0.7em;
            font-weight: 700;
            padding: 2px 4px;
            border-radius: 3px;
            color: #fff;
            margin-top: 3px;
            display: inline-block;
        }

        .rarity-common { background-color: #3498db; }
        .rarity-uncommon { background-color: #f39c12; }
        .rarity-rare { background-color: #9b59b6; }
        .rarity-epic { background-color: #e74c3c; }

        .not-owned::before {
            content: "???";
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background-color: rgba(44, 62, 80, 0.9);
            color: white;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.5em;
            font-family: 'Montserrat', sans-serif;
            z-index: 10;
        }
    </style>
</head>
<body>

    <header>
        <h1>💎 GACHA COLLECTOR PROTOTYPE 💎</h1>
    </header>

    <div id="game-container">
        
        <div class="left-column">
            
            <div class="panel instructions">
                <h2>📜 How to Play</h2>
                <ul>
                    <li>Click the **Big Paw Button** at the center to earn Clicks (1 click per press).</li>
                    <li>Once at **10 Clicks**, you may spend them to **Roll** for a chance to obtain an animal picture of varying rarity's.</li>
                    <li>Collect all the unique, adorable pets and brag to all your friends!</li>
                </ul>
            </div>
            
            <div class="panel stats">
                <h2>📊 Status</h2>
                <p>Total Clicks: <span id="click-count">0</span></p>
                <p>Unique Pets Collected: <span id="unique-pets-count">0</span> / <span id="total-pets">0</span></p>
            </div>

            <div class="panel click-section">
                <h2>🖱️ Clicker</h2>
                <button id="click-button" aria-label="Click to earn Clicks">
                    🐾
                </button>

                <button id="roll-button" disabled>Roll for Pet (10 Clicks)</button>
                <div id="let-it-ride-message"></div>
                <div id="roll-result"></div>
            </div>

        </div>

        <div class="panel gallery">
            <h2>🖼️ Collection Gallery</h2>
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
                
                { id: 5, name: "Propeller Hat Pup", file: "dog-cute.gif", rarity: "Rare" },
                { id: 6, name: "Let It Ride Cat", file: "let-it.gif", rarity: "Rare" }, 
                
                { id: 7, name: "Dogs Playing Poker", file: "91Bh8U5goFL.jpg", rarity: "Epic" }
            ];

            const ROLL_COST = 10;
            const CONSECUTIVE_ROLLS_NEEDED = 30;
            
            let clicks = 0;
            let ownedPets = {};
            let consecutiveDuplicateRolls = 0;

            const clickCountEl = document.getElementById('click-count');
            const uniquePetsCountEl = document.getElementById('unique-pets-count');
            const totalPetsEl = document.getElementById('total-pets');
            const clickButton = document.getElementById('click-button');
            const rollButton = document.getElementById('roll-button');
            const rollResultEl = document.getElementById('roll-result');
            const galleryEl = document.getElementById('pet-gallery');
            const letItRideMessageEl = document.getElementById('let-it-ride-message');
            
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

                if (isNew) {
                    consecutiveDuplicateRolls = 0;
                    letItRideMessageEl.textContent = '';
                } else {
                    consecutiveDuplicateRolls++;
                }

                if (consecutiveDuplicateRolls >= CONSECUTIVE_ROLLS_NEEDED) {
                    letItRideMessageEl.innerHTML = `🔥 **LET IT RIDE!** (${consecutiveDuplicateRolls} Duplicates in a row!) 🔥`;
                } else {
                    letItRideMessageEl.textContent = `Need ${CONSECUTIVE_ROLLS_NEEDED - consecutiveDuplicateRolls} duplicate rolls for the message.`;
                }

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
            letItRideMessageEl.textContent = `Need ${CONSECUTIVE_ROLLS_NEEDED} duplicate rolls for the message.`;
        });
    </script>
