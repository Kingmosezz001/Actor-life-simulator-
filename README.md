<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Barbing Simulator Game</title>
    <style>
        body {
            font-family: 'Poppins', sans-serif;
            margin: 0;
            padding: 0;
            background: linear-gradient(135deg, #1a1a1a, #3a3a3a), url('https://source.unsplash.com/random/1920x1080/?barber') no-repeat center center fixed;
            background-size: cover;
            color: #fff;
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
        }
        .page {
            width: 90%;
            max-width: 600px;
            margin: 10px;
            background: rgba(255, 255, 255, 0.95);
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 4px 16px rgba(0, 0, 0, 0.2);
            backdrop-filter: blur(8px);
            display: none;
            animation: fadeIn 0.5s ease-in-out;
            box-sizing: border-box;
        }
        #form-page, #game-page, #shop-page, #leaderboard-page {
            display: block;
        }
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }
        h1 {
            color: #2c3e50;
            font-size: 1.8em;
            margin: 10px 0;
            text-align: center;
            text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.1);
        }
        .status-card, .form-container {
            background: #ffffff;
            padding: 15px;
            border-radius: 8px;
            box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
            margin-bottom: 15px;
        }
        .status-card p {
            margin: 8px 0;
            font-size: 1em;
            color: #34495e;
        }
        .button-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(120px, 1fr));
            gap: 8px;
            margin: 15px 0;
        }
        button {
            padding: 10px;
            font-size: 0.9em;
            cursor: pointer;
            background: linear-gradient(45deg, #e67e22, #d35400);
            color: white;
            border: none;
            border-radius: 6px;
            transition: transform 0.2s, box-shadow 0.2s;
        }
        button:hover {
            transform: translateY(-2px);
            box-shadow: 0 2px 8px rgba(0, 0, 0, 0.2);
        }
        button:disabled {
            background: #cccccc;
            cursor: not-allowed;
            transform: none;
            box-shadow: none;
        }
        #message, #shop-message, #leaderboard-message, #form-message {
            color: #c0392b;
            font-weight: bold;
            margin: 8px 0;
            font-size: 0.9em;
            text-align: center;
        }
        input, select {
            padding: 10px;
            margin: 8px 0;
            font-size: 0.9em;
            border-radius: 6px;
            border: 1px solid #ddd;
            width: 100%;
            max-width: 100%;
            box-sizing: border-box;
        }
        .form-container label {
            font-size: 1em;
            color: #2c3e50;
            margin-bottom: 5px;
            display: block;
        }
        #leaderboard-table {
            width: 100%;
            border-collapse: collapse;
            margin: 15px 0;
            background: #fff;
            border-radius: 8px;
            overflow: hidden;
        }
        #leaderboard-table th, #leaderboard-table td {
            border: 1px solid #ddd;
            padding: 10px;
            text-align: center;
            color: #34495e;
            font-size: 0.9em;
        }
        #leaderboard-table th {
            background: linear-gradient(45deg, #e67e22, #d35400);
            color: white;
        }
        #leaderboard-table tr:nth-child(even) {
            background: #f2f2f2;
        }
        #leaderboard-table tr.player {
            background: #ffe8d6;
            font-weight: bold;
        }
        #comment-modal, #event-modal, #no-customer-modal, #loading-modal {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.5);
            display: none;
            justify-content: center;
            align-items: center;
            z-index: 1000;
        }
        .modal-content {
            background: #ffffff;
            padding: 15px;
            border-radius: 8px;
            box-shadow: 0 2px 8px rgba(0, 0, 0, 0.2);
            max-width: 90%;
            width: 400px;
            text-align: center;
            box-sizing: border-box;
        }
        .modal-content p {
            margin: 10px 0;
            font-size: 1em;
            color: #34495e;
        }
        .modal-buttons {
            display: flex;
            flex-direction: column;
            gap: 8px;
            margin-top: 15px;
        }
        .loading-bar-container {
            width: 80%;
            height: 20px;
            background: #ddd;
            border-radius: 10px;
            overflow: hidden;
            margin: 10px auto;
        }
        .loading-bar {
            width: 0;
            height: 100%;
            background: linear-gradient(45deg, #e67e22, #d35400);
            animation: load 2s linear forwards;
        }
        @keyframes load {
            from { width: 0; }
            to { width: 100%; }
        }
    </style>
</head>
<body>
    <!-- Form Page -->
    <div id="form-page" class="page">
        <h1>Welcome to Barbing Simulator</h1>
        <div class="form-container">
            <label for="real-name">Your Real Name:</label>
            <input type="text" id="real-name" placeholder="Enter your real name">
            <label for="shop-name">Shop Name (Barbing Saloon will be added):</label>
            <input type="text" id="shop-name" placeholder="Enter shop name">
            <label for="start-date">Starting Date:</label>
            <input type="date" id="start-date" value="2025-08-10">
            <label for="difficulty">Difficulty Level:</label>
            <select id="difficulty">
                <option value="Easy">Easy</option>
                <option value="Normal" selected>Normal</option>
                <option value="Hard">Hard</option>
            </select>
            <label for="country">Country:</label>
            <select id="country" onchange="updateCurrency()">
                <option value="Nigeria" selected>Nigeria</option>
                <option value="United States">United States</option>
                <option value="United Kingdom">United Kingdom</option>
                <option value="Germany">Germany</option>
                <option value="Japan">Japan</option>
                <option value="India">India</option>
                <option value="South Africa">South Africa</option>
            </select>
            <label for="currency">Currency:</label>
            <input type="text" id="currency" readonly value="₦">
            <button onclick="startGame()">Start Game</button>
            <div id="form-message"></div>
        </div>
    </div>

    <!-- Main Game Page -->
    <div id="game-page" class="page">
        <h1 id="game-title">Barbing Simulator Game</h1>
        <div class="status-card">
            <p>Date & Time: <span id="datetime">11:29 PM WAT, Sunday, August 10, 2025</span></p>
            <p>Money: <span id="money">100</span></p>
            <p>Energy: <span id="energy">100</span></p>
            <p>Reputation: <span id="reputation">1</span></p>
            <p>Customers Barbered Today: <span id="customers">0</span></p>
            <p>Housing: <span id="housing">None</span></p>
            <p>Car: <span id="car">None</span></p>
            <p>Girlfriend: <span id="girlfriend">None</span></p>
            <p>Shop Type: <span id="shop-type">Basic</span></p>
            <p>Tools: <span id="tools">None</span></p>
            <p>Day: <span id="day">1</span></p>
            <p>Difficulty: <span id="difficulty-display">Normal</span></p>
        </div>
        <div id="message"></div>
        <div class="button-grid">
            <button id="cut-hair-btn" onclick="cutHair()">Cut Hair (10, -5 Energy)</button>
            <button id="buy-food-btn" onclick="buyFood()">Buy Food (5, +20 Energy)</button>
            <button id="rent-house-btn" onclick="rentHouse()">Rent House (50/month)</button>
            <button onclick="showShopPage()">Go to Shop</button>
            <button onclick="showLeaderboardPage()">View Leaderboard</button>
            <button onclick="saveGame()">Save Game</button>
            <button onclick="resetGame()">Reset Game</button>
            <button onclick="startNextDay()">Next Day</button>
            <button onclick="startFreeDay()">Free Day</button>
        </div>
    </div>

    <!-- Shop Page -->
    <div id="shop-page" class="page">
        <h1>Shop</h1>
        <div class="status-card">
            <p>Money: <span id="shop-money">100</span></p>
            <p>Reputation: <span id="shop-reputation">1</span></p>
            <p>Housing: <span id="shop-housing">None</span></p>
            <p>Car: <span id="shop-car">None</span></p>
            <p>Girlfriend: <span id="shop-girlfriend">None</span></p>
            <p>Shop Type: <span id="shop-shop-type">Basic</span></p>
            <p>Tools: <span id="shop-tools">None</span></p>
        </div>
        <div id="shop-message"></div>
        <h3>Buy a House</h3>
        <select id="house-select">
            <option value="">Select House Type</option>
            <option value="Apartment|1000">Apartment (1000)</option>
            <option value="Bungalow|2000">Bungalow (2000)</option>
            <option value="Mansion|5000">Mansion (5000)</option>
            <option value="Condo|1500">Condo (1500)</option>
            <option value="Villa|3000">Villa (3000)</option>
            <option value="Penthouse|7000">Penthouse (7000)</option>
        </select>
        <button onclick="buyHouse()">Buy House</button>
        <h3>Buy a Car</h3>
        <select id="car-select">
            <option value="">Select Car</option>
            <option value="Toyota Corolla|500">Toyota Corolla (500)</option>
            <option value="Honda Civic|700">Honda Civic (700)</option>
            <option value="BMW X5|1500">BMW X5 (1500)</option>
        </select>
        <button onclick="buyCar()">Buy Car</button>
        <h3>Find a Girlfriend</h3>
        <select id="girlfriend-select">
            <option value="">Select Girlfriend</option>
            <option value="Amara|50">Amara (50/month)</option>
            <option value="Chloe|100">Chloe (100/month)</option>
            <option value="Sophia|150">Sophia (150/month)</option>
        </select>
        <button onclick="getGirlfriend()">Get Girlfriend</button>
        <h3>Buy Barbing Tools</h3>
        <select id="tool-select">
            <option value="">Select Tool</option>
            <option value="Clippers|100">Clippers (100, +0.5 Reputation)</option>
            <option value="Scissors|50">Scissors (50, +0.5 Reputation)</option>
            <option value="Sterilizer|150">Sterilizer (150, +0.5 Reputation)</option>
            <option value="Trimmer|75">Trimmer (75, +0.5 Reputation)</option>
            <option value="Razor|30">Razor (30, +0.25 Reputation)</option>
            <option value="Hair Dryer|120">Hair Dryer (120, +0.75 Reputation)</option>
        </select>
        <button onclick="buyTool()">Buy Tool</button>
        <h3>Upgrade Shop</h3>
        <select id="shop-upgrade-select">
            <option value="">Select Shop Upgrade</option>
            <option value="Basic Shop|500">Basic Shop (500, +1 Reputation)</option>
            <option value="Modern Shop|1000">Modern Shop (1000, +2 Reputation)</option>
            <option value="Luxury Shop|2000">Luxury Shop (2000, +3 Reputation)</option>
            <option value="Premium Shop|3000">Premium Shop (3000, +4 Reputation)</option>
            <option value="Elite Shop|5000">Elite Shop (5000, +5 Reputation)</option>
            <option value="Ultimate Shop|10000">Ultimate Shop (10000, +6 Reputation)</option>
        </select>
        <button onclick="upgradeShop()">Upgrade Shop</button>
        <div class="button-grid">
            <button onclick="showGamePage()">Back to Game</button>
        </div>
    </div>

    <!-- Leaderboard Page -->
    <div id="leaderboard-page" class="page">
        <h1>Barber Leaderboard</h1>
        <div class="status-card">
            <p>Your Rank: <span id="player-rank">N/A</span></p>
            <p>Money: <span id="leaderboard-money">100</span></p>
            <p>Reputation: <span id="leaderboard-reputation">1</span></p>
        </div>
        <div id="leaderboard-message"></div>
        <table id="leaderboard-table">
            <thead>
                <tr>
                    <th>Rank</th>
                    <th>Barber Name</th>
                    <th>Reputation</th>
                    <th>Net Worth</th>
                </tr>
            </thead>
            <tbody id="leaderboard-body"></tbody>
        </table>
        <div class="button-grid">
            <button onclick="showGamePage()">Back to Game</button>
        </div>
    </div>

    <!-- Comment Modal -->
    <div id="comment-modal">
        <div class="modal-content">
            <p id="comment-text"></p>
            <div class="modal-buttons">
                <button id="response-1" onclick="handleCommentResponse(0)"></button>
                <button id="response-2" onclick="handleCommentResponse(1)"></button>
            </div>
        </div>
    </div>

    <!-- Event Modal -->
    <div id="event-modal">
        <div class="modal-content">
            <p id="event-text"></p>
            <div class="modal-buttons">
                <button id="event-response-1" onclick="handleEventResponse(0)"></button>
                <button id="event-response-2" onclick="handleEventResponse(1)"></button>
            </div>
        </div>
    </div>

    <!-- No Customer Modal -->
    <div id="no-customer-modal">
        <div class="modal-content">
            <p id="no-customer-text">No customer at the moment. Wait or try again later.</p>
            <div class="modal-buttons">
                <button onclick="closeNoCustomerModal()">OK</button>
            </div>
        </div>
    </div>

    <!-- Loading Modal -->
    <div id="loading-modal">
        <div class="modal-content">
            <p>Loading...</p>
            <div class="loading-bar-container">
                <div class="loading-bar"></div>
            </div>
        </div>
    </div>

    <script>
        let money = 100;
        let energy = 100;
        let reputation = 1;
        let customersBarbered = 0;
        let housing = "None";
        let car = "None";
        let girlfriend = "None";
        let shopType = "Basic";
        let tools = [];
        let day = 1;
        let daysSinceLastPayment = 0;
        let daysSinceLastRentPayment = 0;
        let rentActive = false;
        let girlfriendCost = 0;
        let realName = "";
        let shopName = "";
        let difficulty = "Normal";
        let currentDate = new Date('2025-08-10T23:29:00+01:00');
        let currentComment = null;
        let clockInterval = null;
        let country = "Nigeria";
        let currencySymbol = "₦";
        let currentEvent = null;
        let dailyCustomerFactor = 1.0;
        let exchangeRate = 1;

        const barbers = [
            { name: "Tony Snips", reputation: 70, netWorth: 8000 },
            { name: "Lila Cuts", reputation: 65, netWorth: 6000 },
            { name: "Mike Razor", reputation: 55, netWorth: 4000 },
            { name: "Sarah Shears", reputation: 80, netWorth: 10000 },
            { name: "Jake Fade", reputation: 50, netWorth: 2500 },
            { name: "Emma Trim", reputation: 60, netWorth: 5000 },
            { name: "Chris Clip", reputation: 55, netWorth: 3500 },
            { name: "Nina Buzz", reputation: 75, netWorth: 7000 }
        ];

        const commentTypes = [
            { type: 'positive', text: 'Nice cut! You’re off to a good start.', reputation: 0.5, responses: [
                { reply: 'Thanks for the support!', emoji: '😊', repChange: -0.5 },
                { reply: 'Glad you liked it!', emoji: '✅', repChange: 0.5 }
            ]},
            { type: 'positive', text: 'Clean fade, I’ll tell my friends!', reputation: 1, responses: [
                { reply: 'Appreciate the word-of-mouth!', emoji: '😊', repChange: -0.5 },
                { reply: 'Thanks, come back soon!', emoji: '✅', repChange: 0.5 }
            ]},
            { type: 'positive', text: 'Pretty good for a new barber!', reputation: 0.5, responses: [
                { reply: 'Thanks for the encouragement!', emoji: '😊', repChange: -0.5 },
                { reply: 'I’m learning, glad you approve!', emoji: '✅', repChange: 0.5 }
            ]},
            { type: 'positive', text: 'Solid haircut, keep it up!', reputation: 1, responses: [
                { reply: 'Thanks, I’m trying my best!', emoji: '😊', repChange: -0.5 },
                { reply: 'Appreciate the feedback!', emoji: '✅', repChange: 0.5 }
            ]},
            { type: 'negative', text: 'The cut was uneven, needs work.', reputation: -3, responses: [
                { reply: 'Sorry, I’ll be more careful next time.', emoji: '✅', repChange: 0.5 },
                { reply: 'Thanks for the feedback.', emoji: '😣', repChange: -1 }
            ]},
            { type: 'negative', text: 'You took too long, I was late!', reputation: -4, responses: [
                { reply: 'Apologies, I’ll speed up next time.', emoji: '✅', repChange: 0.5 },
                { reply: 'Noted, thanks for letting me know.', emoji: '😣', repChange: -1 }
            ]},
            { type: 'negative', text: 'Not what I asked for, disappointed.', reputation: -4, responses: [
                { reply: 'I’m sorry, let me make it right.', emoji: '✅', repChange: 0.5 },
                { reply: 'Thanks for the input.', emoji: '😣', repChange: -1 }
            ]},
            { type: 'negative', text: 'Your tools look old, upgrade them.', reputation: -3, responses: [
                { reply: 'Sorry, I’m working on getting better tools.', emoji: '✅', repChange: 0.5 },
                { reply: 'Thanks for the suggestion.', emoji: '😣', repChange: -1 }
            ]},
            { type: 'abusive', text: 'Horrible haircut! You’re clueless!', reputation: -6, responses: [
                { reply: 'I’m so sorry, can I fix it for free?', emoji: '✅', repChange: 0.5 },
                { reply: 'Apologies for the bad experience.', emoji: '😣', repChange: -1 }
            ]},
            { type: 'abusive', text: 'Worst barber ever, don’t quit your day job!', reputation: -8, responses: [
                { reply: 'Sorry you feel that way, I’ll improve.', emoji: '✅', repChange: 0.5 },
                { reply: 'I apologize, I’m still learning.', emoji: '😣', repChange: -1 }
            ]},
            { type: 'abusive', text: 'You ruined my look, terrible service!', reputation: -7, responses: [
                { reply: 'I’m sorry, let me make it up to you.', emoji: '✅', repChange: 0.5 },
                { reply: 'Apologies for the mistake.', emoji: '😣', repChange: -1 }
            ]},
            { type: 'abusive', text: 'This place is a mess, never coming back!', reputation: -6, responses: [
                { reply: 'Sorry, I’ll clean up and do better.', emoji: '✅', repChange: 0.5 },
                { reply: 'I hear you, I’ll work on it.', emoji: '😣', repChange: -1 }
            ]}
        ];

        const randomEvents = [
            { text: 'You found some money on the street! Keep it or try to return it?', responses: [
                { reply: 'Keep it', effect: () => { money += 10; reputation -= 1; showMessage('You kept the money. +' + currencySymbol + '10, -1 Reputation'); } },
                { reply: 'Try to return it', effect: () => { reputation += 2; showMessage('You tried to return it. +2 Reputation'); } }
            ]},
            { text: 'A customer offers a tip but complains about the service. Accept tip or offer free fix?', responses: [
                { reply: 'Accept tip', effect: () => { money += 5; reputation -= 2; showMessage('Accepted tip. +' + currencySymbol + '5, -2 Reputation'); } },
                { reply: 'Offer free fix', effect: () => { reputation += 3; showMessage('Offered free fix. +3 Reputation'); } }
            ]},
            { text: 'Your clippers broke. Repair now or use backup?', responses: [
                { reply: 'Repair (' + currencySymbol + '20)', effect: () => { if (money >= 20) { money -= 20; showMessage('Repaired clippers. -' + currencySymbol + '20'); } else { showMessage('Not enough money.'); } } },
                { reply: 'Use backup', effect: () => { energy -= 10; showMessage('Used backup. -10 Energy'); } }
            ]},
            { text: 'A local event is happening. Participate to gain reputation?', responses: [
                { reply: 'Participate (-10 Energy)', effect: () => { energy -= 10; reputation += 5; showMessage('Participated in event. -10 Energy, +5 Reputation'); } },
                { reply: 'Skip', effect: () => { showMessage('Skipped the event.'); } }
            ]},
            { text: 'You feel ill. Rest or keep working?', responses: [
                { reply: 'Rest', effect: () => { energy += 15; money -= 5; showMessage('Rested. +15 Energy, -' + currencySymbol + '5 (lost business)'); } },
                { reply: 'Keep working', effect: () => { reputation -= 2; showMessage('Worked while ill. -2 Reputation'); } }
            ]},
            { text: 'Friend asks for free haircut. Agree or charge?', responses: [
                { reply: ' Agree free', effect: () => { reputation += 2; showMessage('Gave free haircut. +2 Reputation'); } },
                { reply: 'Charge', effect: () => { money += 10; reputation -= 1; showMessage('Charged friend. +' + currencySymbol + '10, -1 Reputation'); } }
            ]}
        ];

        function saveGame() {
            const gameState = {
                money: money,
                energy: energy,
                reputation: reputation,
                customersBarbered: customersBarbered,
                housing: housing,
                car: car,
                girlfriend: girlfriend,
                shopType: shopType,
                tools: tools,
                day: day,
                daysSinceLastPayment: daysSinceLastPayment,
                daysSinceLastRentPayment: daysSinceLastRentPayment,
                rentActive: rentActive,
                girlfriendCost: girlfriendCost,
                realName: realName,
                shopName: shopName,
                currentDate: currentDate.toISOString(),
                difficulty: difficulty,
                country: country,
                currencySymbol: currencySymbol
            };
            localStorage.setItem('barbingSimulatorSave', JSON.stringify(gameState));
        }

        function loadGame() {
            const savedState = localStorage.getItem('barbingSimulatorSave');
            if (savedState) {
                const gameState = JSON.parse(savedState);
                money = gameState.money || 100;
                energy = gameState.energy || 100;
                reputation = gameState.reputation || 1;
                customersBarbered = gameState.customersBarbered || 0;
                housing = gameState.housing || "None";
                car = gameState.car || "None";
                girlfriend = gameState.girlfriend || "None";
                shopType = gameState.shopType || "Basic";
                tools = gameState.tools || [];
                day = gameState.day || 1;
                daysSinceLastPayment = gameState.daysSinceLastPayment || 0;
                daysSinceLastRentPayment = gameState.daysSinceLastRentPayment || 0;
                rentActive = gameState.rentActive || false;
                girlfriendCost = gameState.girlfriendCost || 0;
                realName = gameState.realName || "";
                shopName = gameState.shopName || "";
                currentDate = new Date(gameState.currentDate || '2025-08-10T23:29:00+01:00');
                difficulty = gameState.difficulty || "Normal";
                country = gameState.country || "Nigeria";
                currencySymbol = gameState.currencySymbol || "₦";
                if (realName && shopName) {
                    showGamePage();
                } else {
                    showFormPage();
                    document.getElementById('real-name').value = realName;
                    document.getElementById('shop-name').value = shopName.replace(' Barbing Saloon', '');
                    document.getElementById('start-date').value = currentDate.toISOString().split('T')[0];
                    document.getElementById('difficulty').value = difficulty;
                    document.getElementById('country').value = country;
                    updateCurrency();
                }
            } else {
                showFormPage();
            }
        }

        function resetGame() {
            localStorage.removeItem('barbingSimulatorSave');
            money = 100;
            energy = 100;
            reputation = 1;
            customersBarbered = 0;
            housing = "None";
            car = "None";
            girlfriend = "None";
            shopType = "Basic";
            tools = [];
            day = 1;
            daysSinceLastPayment = 0;
            daysSinceLastRentPayment = 0;
            rentActive = false;
            girlfriendCost = 0;
            realName = "";
            shopName = "";
            currentDate = new Date('2025-08-10T23:29:00+01:00');
            difficulty = "Normal";
            country = "Nigeria";
            currencySymbol = "₦";
            currentComment = null;
            currentEvent = null;
            if (clockInterval) clearInterval(clockInterval);
            showMessage('Game reset! Start a new game.', 'form');
            showFormPage();
            document.getElementById('real-name').value = '';
            document.getElementById('shop-name').value = '';
            document.getElementById('start-date').value = '2025-08-10';
            document.getElementById('difficulty').value = 'Normal';
            document.getElementById('country').value = 'Nigeria';
            updateCurrency();
        }

        function updateCurrency() {
            const countrySelect = document.getElementById('country').value;
            let symbol;
            switch (countrySelect) {
                case 'Nigeria':
                    symbol = '₦';
                    break;
                case 'United States':
                    symbol = '$';
                    break;
                case 'United Kingdom':
                    symbol = '£';
                    break;
                case 'Germany':
                    symbol = '€';
                    break;
                case 'Japan':
                    symbol = '¥';
                    break;
                case 'India':
                    symbol = '₹';
                    break;
                case 'South Africa':
                    symbol = 'R';
                    break;
            }
            document.getElementById('currency').value = symbol;
            currencySymbol = symbol;
        }

        function startClock() {
            if (clockInterval) clearInterval(clockInterval);
            clockInterval = setInterval(() => {
                if (currentComment !== null || currentEvent !== null) return;
                const hours = currentDate.getHours();
                if (hours >= 22) {
                    clearInterval(clockInterval);
                    showMessage("It's 10:00 PM or later! Time to rest or go home. Click 'Next Day' to continue.");
                    document.getElementById('cut-hair-btn').disabled = true;
                    return;
                }
                currentDate = new Date(currentDate.getTime() + 60 * 1000);
                updateStatus();
            }, 1000);
        }

        function updateStatus() {
            document.getElementById('money').textContent = currencySymbol + money.toFixed(2);
            document.getElementById('energy').textContent = energy;
            document.getElementById('reputation').textContent = reputation.toFixed(1);
            document.getElementById('customers').textContent = customersBarbered;
            document.getElementById('housing').textContent = housing;
            document.getElementById('car').textContent = car;
            document.getElementById('girlfriend').textContent = girlfriend;
            document.getElementById('shop-type').textContent = shopType;
            document.getElementById('tools').textContent = tools.length ? tools.join(', ') : 'None';
            document.getElementById('day').textContent = day;
            document.getElementById('difficulty-display').textContent = difficulty;
            document.getElementById('shop-money').textContent = currencySymbol + money.toFixed(2);
            document.getElementById('shop-reputation').textContent = reputation.toFixed(1);
            document.getElementById('shop-housing').textContent = housing;
            document.getElementById('shop-car').textContent = car;
            document.getElementById('shop-girlfriend').textContent = girlfriend;
            document.getElementById('shop-shop-type').textContent = shopType;
            document.getElementById('shop-tools').textContent = tools.length ? tools.join(', ') : 'None';
            document.getElementById('leaderboard-money').textContent = currencySymbol + money.toFixed(2);
            document.getElementById('leaderboard-reputation').textContent = reputation.toFixed(1);
            document.getElementById('message').textContent = '';
            document.getElementById('shop-message').textContent = '';
            document.getElementById('leaderboard-message').textContent = '';
            document.getElementById('game-title').textContent = shopName || 'Barbing Simulator Game';
            updateDateTime();
            updateLeaderboard();
            updateGameButtons();
            checkTimeForRest();
        }

        function updateGameButtons() {
            const modifiers = getDifficultyModifiers();
            document.getElementById('cut-hair-btn').textContent = `Cut Hair (${currencySymbol}${modifiers.haircutEarnings.toFixed(2)}, -${modifiers.energyCost.toFixed(1)} Energy)`;
            document.getElementById('buy-food-btn').textContent = `Buy Food (${currencySymbol}5, +20 Energy)`;
            document.getElementById('rent-house-btn').textContent = `Rent House (${currencySymbol}50/month)`;
        }

        function updateDateTime() {
            const options = {
                timeZone: 'Africa/Lagos',
                hour: '2-digit',
                minute: '2-digit',
                hour12: true,
                weekday: 'long',
                year: 'numeric',
                month: 'long',
                day: 'numeric'
            };
            document.getElementById('datetime').textContent = currentDate.toLocaleString('en-US', options);
        }

        function checkTimeForRest() {
            const hours = currentDate.getHours();
            const isAfter10PM = hours >= 22;
            const cutHairBtn = document.getElementById('cut-hair-btn');
            cutHairBtn.disabled = isAfter10PM || currentComment !== null || currentEvent !== null;
            if (isAfter10PM) {
                showMessage("It's 10:00 PM or later! Time to rest or go home. Click 'Next Day' to continue.");
            }
        }

        function showMessage(msg, page = 'game') {
            document.getElementById(page === 'game' ? 'message' : page === 'shop' ? 'shop-message' : page === 'form' ? 'form-message' : 'leaderboard-message').textContent = msg;
        }

        function showFormPage() {
            document.getElementById('form-page').style.display = 'block';
            document.getElementById('game-page').style.display = 'none';
            document.getElementById('shop-page').style.display = 'none';
            document.getElementById('leaderboard-page').style.display = 'none';
            document.getElementById('comment-modal').style.display = 'none';
            document.getElementById('event-modal').style.display = 'none';
            document.getElementById('no-customer-modal').style.display = 'none';
            document.getElementById('loading-modal').style.display = 'none';
            if (clockInterval) clearInterval(clockInterval);
        }

        function showGamePage() {
            document.getElementById('form-page').style.display = 'none';
            document.getElementById('game-page').style.display = 'block';
            document.getElementById('shop-page').style.display = 'none';
            document.getElementById('leaderboard-page').style.display = 'none';
            document.getElementById('comment-modal').style.display = currentComment ? 'flex' : 'none';
            document.getElementById('event-modal').style.display = currentEvent ? 'flex' : 'none';
            document.getElementById('no-customer-modal').style.display = 'none';
            document.getElementById('loading-modal').style.display = 'none';
            startClock();
            updateStatus();
        }

        function showShopPage() {
            document.getElementById('form-page').style.display = 'none';
            document.getElementById('game-page').style.display = 'none';
            document.getElementById('shop-page').style.display = 'block';
            document.getElementById('leaderboard-page').style.display = 'none';
            document.getElementById('comment-modal').style.display = 'none';
            document.getElementById('event-modal').style.display = 'none';
            document.getElementById('no-customer-modal').style.display = 'none';
            document.getElementById('loading-modal').style.display = 'none';
            if (clockInterval) clearInterval(clockInterval);
            updateStatus();
        }

        function showLeaderboardPage() {
            document.getElementById('form-page').style.display = 'none';
            document.getElementById('game-page').style.display = 'none';
            document.getElementById('shop-page').style.display = 'none';
            document.getElementById('leaderboard-page').style.display = 'block';
            document.getElementById('comment-modal').style.display = 'none';
            document.getElementById('event-modal').style.display = 'none';
            document.getElementById('no-customer-modal').style.display = 'none';
            document.getElementById('loading-modal').style.display = 'none';
            if (clockInterval) clearInterval(clockInterval);
            updateLeaderboard();
            updateStatus();
        }

        function showCommentModal(comment) {
            currentComment = comment;
            document.getElementById('comment-text').textContent = comment.text;
            document.getElementById('response-1').textContent = comment.responses[0].reply;
            document.getElementById('response-2').textContent = comment.responses[1].reply;
            document.getElementById('comment-modal').style.display = 'flex';
            document.getElementById('cut-hair-btn').disabled = true;
        }

        function handleCommentResponse(index) {
            if (currentComment) {
                const selectedResponse = currentComment.responses[index];
                reputation = Math.max(0, Math.min(100, reputation + selectedResponse.repChange));
                showMessage(`You replied: "${selectedResponse.reply}" Customer responds: ${selectedResponse.emoji}`);
                document.getElementById('comment-modal').style.display = 'none';
                currentComment = null;
                updateStatus();
                saveGame();
            }
        }

        function showLoadingModal(callback) {
            document.getElementById('loading-modal').style.display = 'flex';
            const loadingBar = document.querySelector('.loading-bar');
            loadingBar.style.width = '0';
            setTimeout(() => {
                document.getElementById('loading-modal').style.display = 'none';
                callback();
            }, 2000);
        }

        function startGame() {
            const realNameInput = document.getElementById('real-name').value.trim();
            const shopNameInput = document.getElementById('shop-name').value.trim();
            const startDateInput = document.getElementById('start-date').value;
            const difficultyInput = document.getElementById('difficulty').value;
            country = document.getElementById('country').value;
            updateCurrency();
            if (realNameInput === "" || shopNameInput === "" || startDateInput === "") {
                showMessage('Please fill in your real name, shop name, and starting date!', 'form');
                return;
            }
            realName = realNameInput;
            shopName = `${shopNameInput} Barbing Saloon`;
            currentDate = new Date(`${startDateInput}T23:29:00+01:00`);
            difficulty = difficultyInput;
            showLoadingModal(() => {
                showGamePage();
                saveGame();
            });
        }

        function getDifficultyModifiers() {
            switch (difficulty) {
                case "Easy":
                    return {
                        haircutEarnings: 15,
                        energyCost: 2.5,
                        costMultiplier: 0.8,
                        positiveCommentChance: 0.4,
                        abusiveCommentChance: 0.2,
                        customerChance: 0.9
                    };
                case "Hard":
                    return {
                        haircutEarnings: 5,
                        energyCost: 7.5,
                        costMultiplier: 1.2,
                        positiveCommentChance: 0.2,
                        abusiveCommentChance: 0.5,
                        customerChance: 0.6
                    };
                case "Normal":
                default:
                    return {
                        haircutEarnings: 10,
                        energyCost: 5,
                        costMultiplier: 1,
                        positiveCommentChance: 0.3,
                        abusiveCommentChance: 0.3,
                        customerChance: 0.8
                    };
            }
        }

        function cutHair() {
            const modifiers = getDifficultyModifiers();
            if (energy < modifiers.energyCost) {
                showMessage('Not enough energy to cut hair!');
                return;
            }
            if (currentComment !== null || currentEvent !== null) {
                showMessage('Please respond to the current pop-up before continuing!');
                return;
            }
            let customerChance = modifiers.customerChance + (reputation / 100) * 0.2;
            customerChance = Math.min(1, customerChance);
            if (Math.random() > customerChance) {
                showNoCustomerModal();
                return;
            }
            const haircutTime = Math.floor(Math.random() * 31) + 10;
            const newTime = new Date(currentDate.getTime() + haircutTime * 60 * 1000);
            if (newTime.getHours() >= 22) {
                showMessage("It's 10:00 PM or later! Time to rest or go home. Click 'Next Day' to continue.");
                document.getElementById('cut-hair-btn').disabled = true;
                clearInterval(clockInterval);
                return;
            }
            currentDate = newTime;
            money += modifiers.haircutEarnings;
            energy -= modifiers.energyCost;
            customersBarbered += 1;
            reputation = Math.max(0, Math.min(100, reputation + 0.1));
            showMessage(`You barbered a customer and earned ${currencySymbol}${modifiers.haircutEarnings.toFixed(2)}! Took ${haircutTime} minutes. Customers today: ${customersBarbered}`);
            const randomValue = Math.random();
            let comment;
            if (randomValue < modifiers.positiveCommentChance) {
                comment = commentTypes.filter(c => c.type === 'positive')[Math.floor(Math.random() * commentTypes.filter(c => c.type === 'positive').length)];
            } else if (randomValue < modifiers.positiveCommentChance + modifiers.abusiveCommentChance) {
                comment = commentTypes.filter(c => c.type === 'abusive')[Math.floor(Math.random() * commentTypes.filter(c => c.type === 'abusive').length)];
            } else {
                comment = commentTypes.filter(c => c.type === 'negative')[Math.floor(Math.random() * commentTypes.filter(c => c.type === 'negative').length)];
            }
            if (comment) {
                reputation = Math.max(0, Math.min(100, reputation + comment.reputation));
                showCommentModal(comment);
            }
            if (Math.random() < 0.1) triggerRandomEvent();
            updateStatus();
            saveGame();
        }

        function showNoCustomerModal() {
            document.getElementById('no-customer-modal').style.display = 'flex';
        }

        function closeNoCustomerModal() {
            document.getElementById('no-customer-modal').style.display = 'none';
        }

        function buyFood() {
            if (money >= 5) {
                money -= 5;
                energy = Math.min(100, energy + 20);
                showMessage('You bought food and gained 20 energy!');
                updateStatus();
                saveGame();
            } else {
                showMessage('Not enough money to buy food! You need ' + currencySymbol + '5, but you have ' + currencySymbol + money.toFixed(2) + '.');
            }
        }

        function rentHouse() {
            if (housing === "None") {
                housing = "Rented";
                rentActive = true;
                daysSinceLastRentPayment = 0;
                showMessage('You rented a house for ' + currencySymbol + '50/month! Payment due at month\'s end.');
                updateStatus();
                saveGame();
            } else {
                showMessage('You already have housing!');
            }
        }

        function buyHouse() {
            if (housing !== "None") {
                showMessage('You already have housing!', 'shop');
                return;
            }
            const modifiers = getDifficultyModifiers();
            const select = document.getElementById('house-select');
            const value = select.value;
            if (!value) {
                showMessage('Please select a house type!', 'shop');
                return;
            }
            const [houseType, cost] = value.split('|');
            const houseCost = parseFloat(cost) * modifiers.costMultiplier;
            if (isNaN(houseCost)) {
                showMessage('Invalid house cost!', 'shop');
                return;
            }
            if (money >= houseCost) {
                money -= houseCost;
                housing = houseType;
                rentActive = false;
                daysSinceLastRentPayment = 0;
                select.value = '';
                showMessage(`You bought a ${houseType} for ${currencySymbol}${houseCost.toFixed(2)}!`, 'shop');
                updateStatus();
                saveGame();
            } else {
                showMessage(`Not enough money to buy a ${houseType}! You need ${currencySymbol}${houseCost.toFixed(2)}, but you have ${currencySymbol}${money.toFixed(2)}.`, 'shop');
            }
        }

        function buyCar() {
            if (car !== "None") {
                showMessage('You already own a car!', 'shop');
                return;
            }
            const modifiers = getDifficultyModifiers();
            const select = document.getElementById('car-select');
            const value = select.value;
            if (!value) {
                showMessage('Please select a car!', 'shop');
                return;
            }
            const [carName, cost] = value.split('|');
            const carCost = parseFloat(cost) * modifiers.costMultiplier;
            if (isNaN(carCost)) {
                showMessage('Invalid car cost!', 'shop');
                return;
            }
            if (money >= carCost) {
                money -= carCost;
                car = carName;
                select.value = '';
                showMessage(`You bought a ${carName} for ${currencySymbol}${carCost.toFixed(2)}!`, 'shop');
                updateStatus();
                saveGame();
            } else {
                showMessage(`Not enough money to buy a ${carName}! You need ${currencySymbol}${carCost.toFixed(2)}, but you have ${currencySymbol}${money.toFixed(2)}.`, 'shop');
            }
        }

        function getGirlfriend() {
            if (girlfriend !== "None") {
                showMessage('You already have a girlfriend!', 'shop');
                return;
            }
            const modifiers = getDifficultyModifiers();
            const select = document.getElementById('girlfriend-select');
            const value = select.value;
            if (!value) {
                showMessage('Please select a girlfriend!', 'shop');
                return;
            }
            const [gfName, cost] = value.split('|');
            const gfCost = parseFloat(cost) * modifiers.costMultiplier;
            if (isNaN(gfCost)) {
                showMessage('Invalid girlfriend cost!', 'shop');
                return;
            }
            if (money >= gfCost) {
                money -= gfCost;
                girlfriend = gfName;
                girlfriendCost = gfCost;
                daysSinceLastPayment = 0;
                select.value = '';
                showMessage(`You are now dating ${gfName}! (Costs ${currencySymbol}${gfCost.toFixed(2)}/month)`, 'shop');
                updateStatus();
                saveGame();
            } else {
                showMessage(`Not enough money to date ${gfName}! You need ${currencySymbol}${gfCost.toFixed(2)}, but you have ${currencySymbol}${money.toFixed(2)}.`, 'shop');
            }
        }

        function buyTool() {
            const modifiers = getDifficultyModifiers();
            const select = document.getElementById('tool-select');
            const value = select.value;
            if (!value) {
                showMessage('Please select a tool!', 'shop');
                return;
            }
            const [toolName, cost] = value.split('|');
            const toolCost = parseFloat(cost) * modifiers.costMultiplier;
            if (isNaN(toolCost)) {
                showMessage('Invalid tool cost!', 'shop');
                return;
            }
            if (tools.includes(toolName)) {
                showMessage(`You already own ${toolName}!`, 'shop');
                return;
            }
            if (money >= toolCost) {
                money -= toolCost;
                tools.push(toolName);
                const repGain = toolName === 'Razor' ? 0.25 : toolName === 'Hair Dryer' ? 0.75 : 0.5;
                reputation = Math.max(0, Math.min(100, reputation + repGain));
                select.value = '';
                showMessage(`You bought ${toolName} for ${currencySymbol}${toolCost.toFixed(2)}! (+${repGain} Reputation)`, 'shop');
                updateStatus();
                saveGame();
            } else {
                showMessage(`Not enough money to buy ${toolName}! You need ${currencySymbol}${toolCost.toFixed(2)}, but you have ${currencySymbol}${money.toFixed(2)}.`, 'shop');
            }
        }

        function upgradeShop() {
            const modifiers = getDifficultyModifiers();
            const select = document.getElementById('shop-upgrade-select');
            const value = select.value;
            if (!value) {
                showMessage('Please select a shop upgrade!', 'shop');
                return;
            }
            const [newShopType, cost] = value.split('|');
            const shopCost = parseFloat(cost) * modifiers.costMultiplier;
            if (isNaN(shopCost)) {
                showMessage('Invalid shop upgrade cost!', 'shop');
                return;
            }
            if (shopType === newShopType) {
                showMessage(`You already own a ${newShopType}!`, 'shop');
                return;
            }
            if (money >= shopCost) {
                money -= shopCost;
                shopType = newShopType;
                let repGain;
                switch (newShopType) {
                    case 'Basic Shop':
                        repGain = 1;
                        break;
                    case 'Modern Shop':
                        repGain = 2;
                        break;
                    case 'Luxury Shop':
                        repGain = 3;
                        break;
                    case 'Premium Shop':
                        repGain = 4;
                        break;
                    case 'Elite Shop':
                        repGain = 5;
                        break;
                    case 'Ultimate Shop':
                        repGain = 6;
                        break;
                }
                reputation = Math.max(0, Math.min(100, reputation + repGain));
                select.value = '';
                showMessage(`You upgraded to a ${newShopType} for ${currencySymbol}${shopCost.toFixed(2)}! (+${repGain} Reputation)`, 'shop');
                updateStatus();
                saveGame();
            } else {
                showMessage(`Not enough money to upgrade to ${newShopType}! You need ${currencySymbol}${shopCost.toFixed(2)}, but you have ${currencySymbol}${money.toFixed(2)}.`, 'shop');
            }
        }

        function freeDay() {
            const currentMonth = currentDate.getMonth();
            day++;
            daysSinceLastPayment++;
            daysSinceLastRentPayment++;
            currentDate = new Date(currentDate.getFullYear(), currentDate.getMonth(), currentDate.getDate() + 1, 8, 0);
            const newMonth = currentDate.getMonth();
            energy = Math.min(100, energy + 20);
            reputation = Math.max(0, reputation - 2);
            customersBarbered = 0;
            if (rentActive && currentMonth !== newMonth) {
                if (money >= 50) {
                    money -= 50;
                    daysSinceLastRentPayment = 0;
                    showMessage('Paid ' + currencySymbol + '50 for monthly rent.');
                } else {
                    housing = "None";
                    rentActive = false;
                    daysSinceLastRentPayment = 0;
                    showMessage('Evicted! Not enough money for rent.');
                }
            }
            if (girlfriend !== "None" && daysSinceLastPayment >= 30) {
                if (money >= girlfriendCost) {
                    money -= girlfriendCost;
                    daysSinceLastPayment = 0;
                    showMessage(`Paid ${currencySymbol}${girlfriendCost} for your girlfriend, ${girlfriend}.`);
                } else {
                    girlfriend = "None";
                    girlfriendCost = 0;
                    daysSinceLastPayment = 0;
                    showMessage(`You broke up with ${girlfriend}! Not enough money.`);
                }
            }
            showMessage('You took a free day and rested. Energy +20, Reputation -2.');
            if (Math.random() < 0.3) triggerRandomEvent();
            startClock();
            updateStatus();
            saveGame();
        }

        function startFreeDay() {
            showLoadingModal(() => {
                freeDay();
            });
        }

        function calculateNetWorth() {
            let netWorth = money;
            if (housing === 'Apartment') netWorth += 1000;
            else if (housing === 'Bungalow') netWorth += 2000;
            else if (housing === 'Mansion') netWorth += 5000;
            else if (housing === 'Condo') netWorth += 2000;
            else if (housing === 'Villa') netWorth += 3000;
            else if (housing === 'Penthouse') netWorth += 7000;
            if (car === 'Toyota Corolla') netWorth += 500;
            else if (car === 'Honda Civic') netWorth += 700;
            else if (car === 'BMW X5') netWorth += 1500;
            if (shopType === 'Basic Shop') netWorth += 500;
            else if (shopType === 'Modern Shop') netWorth += 1000;
            else if (shopType === 'Luxury Shop') netWorth += 2000;
            else if (shopType === 'Premium Shop') netWorth += 3000;
            else if (shopType === 'Elite Shop') netWorth += 5000;
            else if (shopType === 'Ultimate Shop') netWorth += 10000;
            netWorth += tools.reduce((sum, tool) => sum + (tool === 'Clippers' ? 100 : tool === 'Scissors' ? 50 : tool === 'Sterilizer' ? 150 : tool === 'Trimmer' ? 75 : tool === 'Razor' ? 30 : 120), 0);
            return netWorth;
        }

        function updateLeaderboard() {
            const player = { name: shopName || 'You', reputation: reputation, netWorth: calculateNetWorth() };
            const allBarbers = [...barbers, player].sort((a, b) => b.netWorth - a.netWorth);
            const leaderboardBody = document.getElementById('leaderboard-body');
            leaderboardBody.innerHTML = '';
            allBarbers.forEach((barber, index) => {
                const row = document.createElement('tr');
                row.className = barber.name === (shopName || 'You') ? 'player' : '';
                row.innerHTML = `
                    <td>${index + 1}</td>
                    <td>${barber.name}</td>
                    <td>${barber.reputation.toFixed(1)}</td>
                    <td>${currencySymbol}${barber.netWorth.toFixed(2)}</td>
                `;
                leaderboardBody.appendChild(row);
                if (barber.name === (shopName || 'You')) {
                    document.getElementById('player-rank').textContent = index + 1;
                }
            });
        }

        function nextDay() {
            const currentMonth = currentDate.getMonth();
            day++;
            daysSinceLastPayment++;
            daysSinceLastRentPayment++;
            currentDate = new Date(currentDate.getFullYear(), currentDate.getMonth(), currentDate.getDate() + 1, 8, 0);
            const newMonth = currentDate.getMonth();
            energy = Math.min(100, energy + 10);
            customersBarbered = 0;
            dailyCustomerFactor = Math.random() * 0.6 + 0.4;
            if (rentActive && currentMonth !== newMonth) {
                if (money >= 50) {
                    money -= 50;
                    daysSinceLastRentPayment = 0;
                    showMessage('Paid ' + currencySymbol + '50 for monthly rent.');
                } else {
                    housing = "None";
                    rentActive = false;
                    daysSinceLastRentPayment = 0;
                    showMessage('Evicted! Not enough money for rent.');
                }
            }
            if (girlfriend !== "None" && daysSinceLastPayment >= 30) {
                if (money >= girlfriendCost) {
                    money -= girlfriendCost;
                    daysSinceLastPayment = 0;
                    showMessage(`Paid ${currencySymbol}${girlfriendCost} for your girlfriend, ${girlfriend}.`);
                } else {
                    girlfriend = "None";
                    girlfriendCost = 0;
                    daysSinceLastPayment = 0;
                    showMessage(`You broke up with ${girlfriend}! Not enough money.`);
                }
            }
            if (Math.random() < 0.3) triggerRandomEvent();
            startClock();
            updateStatus();
            saveGame();
        }

        function startNextDay() {
            showLoadingModal(() => {
                nextDay();
            });
        }

        function triggerRandomEvent() {
            if (!currentEvent) {
                const event = randomEvents[Math.floor(Math.random() * randomEvents.length)];
                currentEvent = event;
                document.getElementById('event-text').textContent = event.text;
                document.getElementById('event-response-1').textContent = event.responses[0].reply;
                document.getElementById('event-response-2').textContent = event.responses[1].reply;
                document.getElementById('event-modal').style.display = 'flex';
                document.getElementById('cut-hair-btn').disabled = true;
            }
        }

        function handleEventResponse(index) {
            if (currentEvent) {
                currentEvent.responses[index].effect();
                document.getElementById('event-modal').style.display = 'none';
                currentEvent = null;
                updateStatus();
                saveGame();
            }
        }

        loadGame();
    </script>
</body>
</html>
