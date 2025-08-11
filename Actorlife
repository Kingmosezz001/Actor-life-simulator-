<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>🎭 Actor Simulator</title>
  <style>
    body {
      font-family: 'Segoe UI', sans-serif;
      background: linear-gradient(to right, #dfe9f3, #ffffff);
      padding: 20px;
      color: #333;
    }
    h1, h2, h3 {
      color: #1a1a1a;
    }
    #profileForm, #game {
      background: white;
      padding: 25px;
      max-width: 650px;
      margin: auto;
      box-shadow: 0 0 15px rgba(0,0,0,0.1);
      border-radius: 12px;
    }
    input, select, button {
      width: 100%;
      padding: 12px;
      margin: 10px 0;
      border-radius: 8px;
      border: 1px solid #ccc;
      font-size: 16px;
    }
    button {
      background: #007bff;
      color: white;
      cursor: pointer;
      border: none;
    }
    button:hover {
      background: #0056b3;
    }
    #stats {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 5px; /* Reduced from 10px */
  margin-top: 8px; /* Slightly reduced from 10px */
  margin-bottom: 16px; /* Slightly reduced from 20px */
}
.stat-card {
  background: #f0f8ff;
  padding: 6px; /* Reduced from 10px */
  border-radius: 6px; /* Reduced from 8px */
  text-align: center;
  font-size: 14px; /* Smaller font for labels */
}
.stat-card span {
  font-size: 16px; /* Slightly larger for values to maintain readability */
  font-weight: bold; /* Emphasize values */
}

/* Media query for smaller screens */
@media (max-width: 500px) {
  #stats {
    grid-template-columns: repeat(2, 1fr); /* Switch to 2-column layout */
    gap: 4px; /* Further reduce gap */
  }
  .stat-card {
    padding: 5px; /* Further reduce padding */
    font-size: 13px; /* Slightly smaller labels */
  }
  .stat-card span {
    font-size: 15px; /* Slightly smaller values */
  }
}
    #weekChoices {
  display: flex;
  flex-direction: column;
  gap: 0; /* Remove any vertical gap between buttons */
}

#weekChoices {
  display: flex;
  flex-direction: column;
  gap: 0; /* Remove any vertical gap between buttons */
}

.choice-btn {
  background: #28a745;
  color: white;
  font-weight: bold;
  padding: 8px;
  font-size: 14px;
  margin: 0; /* Remove all margins to eliminate side spacing */
  border-radius: 6px;
  width: 100%; /* Ensure buttons take full width of the container */
  box-sizing: border-box; /* Include padding and border in width calculation */
}
.choice-btn:hover {
  background: #1e7e34;
}
.choice-btn:disabled {
  background: #cccccc;
  cursor: not-allowed;
}
    #log {
      margin-top: 20px;
      padding: 15px;
      background: #fffbea;
      border: 1px dashed #999;
      border-radius: 8px;
    }
    #topButtons {
      display: flex;
      justify-content: space-between;
      margin-bottom: 10px;
    }
    #nextWeekContainer {
  margin-top: 10px; /* Space below #topButtons */
}
#nextWeekBtn {
  background: #ffc107;
  color: #333;
  font-weight: bold;
  width: 100%; /* Match other buttons */
  padding: 12px; /* Consistent with global button styles */
  border-radius: 8px; /* Consistent with global button styles */
  border: none; /* Consistent with global button styles */
  font-size: 16px; /* Consistent with global button styles */
  cursor: pointer; /* Consistent with global button styles */
}
#nextWeekBtn:hover {
  background: #e0a800;
}
    #modal {
      display: none;
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: rgba(0, 0, 0, 0.5);
      justify-content: center;
      align-items: center;
      z-index: 1000;
    }
    .modal-content {
      background: white;
      padding: 20px;
      border-radius: 12px;
      max-width: 400px;
      text-align: center;
      box-shadow: 0 0 15px rgba(0,0,0,0.2);
    }
    .modal-buttons {
      display: flex;
      justify-content: space-around;
      margin-top: 20px;
    }
    .modal-ok-button {
      display: none;
      margin-top: 20px;
    }
    .modal-btn {
      width: 45%;
      padding: 10px;
      border-radius: 8px;
      cursor: pointer;
    }
    .modal-btn.yes {
      background: #28a745;
      color: white;
    }
    .modal-btn.yes:hover {
      background: #1e7e34;
    }
    .modal-btn.no {
      background: #dc3545;
      color: white;
    }
    .modal-btn.no:hover {
      background: #c82333;
    }
    .modal-btn.ok {
      background: #007bff;
      color: white; /* Fixed typo */
      width: 100%;
    }
    .modal-btn.ok:hover {
      background: #0056b3;
    }
    .modal-buttons.info {
      display: none;
    }
    .modal-ok-button.info {
      display: block;
    }
    #lifestyleChoices {
      margin-top: 20px;
    }
    #saveNotification {
      display: none;
      position: fixed;
      top: 20px;
      right: 20px;
      background: #28a745;
      color: white;
      padding: 10px 20px;
      border-radius: 8px;
      z-index: 1001;
    }
  </style>
</head>
<body>
  <h1 style="text-align:center;">🎭 ACTOR SIMULATOR</h1>

  <div id="profileForm" style="display:none;">
    <h2>📋 Create Your Actor Profile</h2>
    <input type="text" id="fullName" placeholder="Full Name">
    <input type="text" id="stageName" placeholder="Stage Name">
    <input type="number" id="age" placeholder="Age (17-60)" min="17" max="60">
    <input type="text" id="city" placeholder="City">
    <label>📅 Starting Date:</label>
    <input type="date" id="startDate" min="2025-01-01" max="2028-12-31">
    <label>💱 Choose Currency:</label>
    <select id="currency">
      <option value="$">$ Dollar</option>
      <option value="€">€ Euro</option>
      <option value="£">£ Pound</option>
    </select>
    <button onclick="startGame()">Start My Acting Career</button>
  </div>

  <div id="game" style="display:none;">
  <div id="topButtons">
    <button onclick="saveGame()">💾 Save</button>
    <button onclick="resetGame()">🔄 Reset</button>
  </div>
  <div id="nextWeekContainer">
    <button id="nextWeekBtn" onclick="nextWeek()">➡️ Next Week</button>
  </div>

  <div id="saveNotification">Game Saved!</div>

  <h2>🎬 Welcome, <span id="nameDisplay"></span></h2>
  <p><strong>From:</strong> <span id="cityDisplay"></span></p>
  <p><strong>Age:</strong> <span id="ageDisplay"></span></p>
  <p><strong>Started:</strong> <span id="startDateDisplay"></span></p>

  <div id="stats">
    <div class="stat-card">📱 Followers<br><span id="followers">10</span></div>
    <div class="stat-card">💰 Money<br><span id="currencySymbol">$</span><span id="money">500</span></div>
    <div class="stat-card">🌟 Fame<br><span id="fame">1</span>/100</div>
    <div class="stat-card">🎭 Skill<br><span id="skill">Beginner</span></div>
    <div class="stat-card">⚡ Energy<br><span id="energy">100</span>/100</div>
    <div class="stat-card">📅 Year & Week<br><span id="weekNum">Year 1, Week 1</span></div>
    <div class="stat-card">🎬 Blockbusters<br><span id="blockbusters">0</span></div>
    <div class="stat-card">📜 Scripts<br><span id="scripts">0</span></div>
    <div class="stat-card">💍 Status<br><span id="marriageStatus">Single</span></div>
  </div>

  <h3>🎯 This Week – Choose your actions:</h3>
  <div id="weekChoices">
    <button class="choice-btn" onclick="chooseAction(1, 50)">🎤 Audition ($1,000) -50⚡</button>
    <button class="choice-btn" onclick="chooseAction(2, 15)">📲 Post TikTok -15⚡</button>
    <button class="choice-btn" onclick="chooseAction(3, 30)">🎓 Attend Workshop -30⚡</button>
    <button class="choice-btn" onclick="practice()">🧘 Practice Acting -30⚡</button>
    <button class="choice-btn" onclick="chooseAction(4, 20)">🤝 Hire Talent Agent ($2,000) -20⚡</button>
    <button class="choice-btn" onclick="chooseAction(5, 30)">💼 Take a Side Job -30⚡</button>
    <button class="choice-btn" id="blockbusterBtn" onclick="chooseAction(6, 40)">🎬 Hire for Blockbuster Movie -40⚡</button>
    <button class="choice-btn" id="writeScriptBtn" onclick="writeScript()">✍️ Write Script -30⚡</button>
    <button class="choice-btn" id="sellScriptBtn" onclick="sellScript()">💸 Sell Script -20⚡</button>
    <button class="choice-btn" id="aListPartyBtn" onclick="attendAListParty()">🥂 Attend A-List Party ($2,500) -25⚡</button>
    <button class="choice-btn" id="voiceActBtn" onclick="voiceActVideoGame()">🎮 Voice Act in Video Game -30⚡</button>
    <button class="choice-btn" id="endorsementBtn" onclick="doBrandEndorsement()">📺 Do Brand Endorsement Deal ($1,000) -20⚡</button>
    <button class="choice-btn" id="networkingBtn" onclick="attendNetworkingEvent()">🤝 Attend Industry Networking Event ($2,000) -25⚡</button>
    <button class="choice-btn" id="merchLineBtn" onclick="launchMerchLine()">🛍️ Launch Merchandise Line ($15,000) -40⚡</button>
  </div>

  <h3>🛍️ Lifestyle Purchases</h3>
  <div id="lifestyleChoices">
    <!-- Lifestyle buttons will be dynamically generated -->
  </div>

  <div id="log"></div>
</div>

  <!-- Modal for Notifications -->
  <div id="modal">
    <div class="modal-content">
      <p id="modalMessage"></p>
      <div id="modalButtons" class="modal-buttons">
        <button class="modal-btn yes" onclick="resolveModal(true)">Yes</button>
        <button class="modal-btn no" onclick="resolveModal(false)">No</button>
      </div>
      <div id="modalOkButton" class="modal-ok-button">
        <button class="modal-btn ok" onclick="resolveModal(true)">OK</button>
      </div>
    </div>
  </div>

  <script>
    let money;
let fame = 1;
let followers = 10;
let skill = "Beginner";
let week = 1;
let year = 1; // New variable to track the current year
let energy = 100;
let currencySymbol = "$";
let practiceXP = 0;
let startDate = "";
let age = 17;
let hasAgent = false;
let blockbusters = 0;
let scripts = 0;
let scriptQualities = [];
let voiceActingIncome = 0;
let voiceActingWeeks = 0;
let merchIncome = 0;
let merchWeeks = 0;
let merchFailed = false; // Track if merch line has failed
let purchasedItems = [];
let isTikTokMonetized = false;
let tiktokIncome = 0;
let tiktokMonetizationWeeks = 0;
let isMarried = false;
let spouseName = "";
// New variables for cooldowns and availability
let actionCooldowns = {
  writeScript: 0,       // Weeks until Write Script is available again
  blockbuster: 0,       // Weeks until Hire for Blockbuster Movie is available
  aListParty: 0,        // Weeks until Attend A-List Party is available
  voiceAct: 0,          // Weeks until Voice Act in Video Game is available
  endorsement: 0,       // Weeks until Do Brand Endorsement Deal is available
  networking: 0,        // Weeks until Attend Industry Networking Event is available
  merchLine: 0          // Weeks until Launch Merchandise Line is available
};
let actionAvailability = {
  writeScript: true,    // Always available initially, but limited by cooldown
  blockbuster: false,
  aListParty: false,
  voiceAct: false,
  endorsement: false,
  networking: false,
  merchLine: false
};
let actionUses = {
  writeScript: 0,       // Track total uses of Write Script
  blockbuster: 0,       // Track total uses of Hire for Blockbuster Movie
  aListParty: 0,        // Track total uses of Attend A-List Party
  voiceAct: 0,          // Track total uses of Voice Act in Video Game
  endorsement: 0,       // Track total uses of Do Brand Endorsement Deal
  networking: 0,        // Track total uses of Attend Industry Networking Event
  merchLine: 0          // Track total uses of Launch Merchandise Line
};
const MAX_ACTION_USES_PER_YEAR = {
  writeScript: 4,       // Max 4 scripts per year
  blockbuster: 1,       // Max 1 blockbuster role per year
  aListParty: 3,        // Max 3 parties per year
  voiceAct: 2,          // Max 2 voice acting gigs per year
  endorsement: 3,       // Max 3 endorsements per year
  networking: 3,        // Max 3 networking events per year
  merchLine: 1          // Max 1 merch line launch per year
};
let modalResolve;
const SAVE_VERSION = "1.2";

    const lifestyleItems = [
      { name: "Designer Clothes", price: 20000, fameReward: 0.2 },
      { name: "Gold Necklace", price: 50000, fameReward: 0.3 },
      { name: "Sports Car", price: 100000, fameReward: 0.4 },
      { name: "Luxury Watch", price: 250000, fameReward: 0.5 },
      { name: "Penthouse Apartment", price: 1000000, fameReward: 0.6 },
      { name: "Luxury Boutique", price: 5000000, fameReward: 0.7 },
      { name: "Mansion", price: 10000000, fameReward: 0.8 },
      { name: "Yacht", price: 50000000, fameReward: 0.9 },
      { name: "Customized Private Jet", price: 1000000000, fameReward: 1 }
    ];

    function getStartingMoney(currency) {
      switch (currency) {
        case "$": return 500;
        case "€": return 425;
        case "£": return 375;
        default: return 500;
      }
    }

    function convertCurrency(amount) {
      switch (currencySymbol) {
        case "€": return Math.round(amount * 0.85);
        case "£": return Math.round(amount * 0.75);
        default: return amount;
      }
    }

function formatMoney(amount) {
  const absAmount = Math.abs(amount);
  let formatted = "";
  let suffix = "";

  if (absAmount >= 1_000_000_000) {
    formatted = (amount / 1_000_000_000).toFixed(1).replace(/\.0$/, "");
    suffix = "b";
  } else if (absAmount >= 1_000_000) {
    formatted = (amount / 1_000_000).toFixed(1).replace(/\.0$/, "");
    suffix = "m";
  } else if (absAmount >= 1_000) {
    formatted = (amount / 1_000).toFixed(1).replace(/\.0$/, "");
    suffix = "k";
  } else {
    formatted = amount.toString();
  }

  return `${amount < 0 ? '-' : ''}${currencySymbol}${formatted}${suffix}`;
}

    function getSkillByXP(xp) {
      if (xp >= 30) return "Master";
      if (xp >= 20) return "Pro";
      if (xp >= 12) return "Trained";
      if (xp >= 7) return "Improving";
      if (xp >= 3) return "Learning";
      return "Beginner";
    }

    function showModal(message, type = "choice") {
      return new Promise((resolve) => {
        document.getElementById("modalMessage").textContent = message;
        const modalButtons = document.getElementById("modalButtons");
        const modalOkButton = document.getElementById("modalOkButton");
        modalButtons.className = "modal-buttons" + (type === "info" ? " info" : "");
        modalOkButton.className = "modal-ok-button" + (type === "info" ? " info" : "");
        document.getElementById("modal").style.display = "flex";
        modalResolve = resolve;
      });
    }

    function showInfoModal(message) {
      return showModal(message, "info");
    }

    function resolveModal(choice) {
      document.getElementById("modal").style.display = "none";
      modalResolve(choice);
    }

    function showSaveNotification() {
      const notification = document.getElementById("saveNotification");
      notification.style.display = "block";
      setTimeout(() => {
        notification.style.display = "none";
      }, 2000);
    }

    function saveGame() {
  const data = {
    version: SAVE_VERSION,
    money,
    fame,
    followers,
    skill,
    week,
    year, // Add year to saved data
    energy,
    currencySymbol,
    practiceXP,
    startDate,
    age,
    hasAgent,
    blockbusters,
    scripts,
    scriptQualities,
    voiceActingIncome,
    voiceActingWeeks,
    merchIncome,
    merchWeeks,
    merchFailed,
    purchasedItems,
    isTikTokMonetized,
    tiktokIncome,
    tiktokMonetizationWeeks,
    isMarried,
    spouseName,
    actionCooldowns,
    actionAvailability,
    actionUses,
    fullName: document.getElementById("nameDisplay").textContent.split(" (")[1]?.replace(")", "") || "",
    stageName: document.getElementById("nameDisplay").textContent.split(" (")[0] || "",
    city: document.getElementById("cityDisplay").textContent || ""
  };
  setTimeout(() => {
    try {
      localStorage.setItem("actorSimSave", JSON.stringify(data));
      showSaveNotification();
    } catch (e) {
      console.error("Save failed:", e);
      showModal("Failed to save game. Try again?");
    }
  }, 0);
}

    function loadGame() {
  const savedData = localStorage.getItem("actorSimSave");
  if (!savedData) {
    console.log("No saved game found, starting fresh.");
    document.getElementById("profileForm").style.display = "block";
    document.getElementById("game").style.display = "none";
    return false;
  }

  try {
    const data = JSON.parse(savedData);
    // Validate save version
    if (data.version !== SAVE_VERSION) {
      console.warn(`Save version mismatch: expected ${SAVE_VERSION}, got ${data.version}. Starting fresh.`);
      localStorage.removeItem("actorSimSave");
      document.getElementById("profileForm").style.display = "block";
      document.getElementById("game").style.display = "none";
      return false;
    }

    // Assign values with fallbacks
    money = Number(data.money) || getStartingMoney(data.currencySymbol || "$");
    fame = Number(data.fame) || Number(data.reputation) || 1;
    followers = Number(data.followers) || 10;
    skill = data.skill || "Beginner";
    week = Number(data.week) || 1;
    year = Number(data.year) || 1; // Load year with fallback
    energy = Number(data.energy) || 100;
    currencySymbol = data.currencySymbol || "$";
    practiceXP = Number(data.practiceXP) || 0;
    startDate = data.startDate || "";
    age = Number(data.age) || 17;
    hasAgent = data.hasAgent || false;
    blockbusters = Number(data.blockbusters) || 0;
    scripts = Number(data.scripts) || 0;
    scriptQualities = Array.isArray(data.scriptQualities) ? data.scriptQualities : [];
    voiceActingIncome = Number(data.voiceActingIncome) || 0;
    voiceActingWeeks = Number(data.voiceActingWeeks) || 0;
    merchIncome = Number(data.merchIncome) || 0;
    merchWeeks = Number(data.merchWeeks) || 0;
    merchFailed = data.merchFailed || false;
    purchasedItems = Array.isArray(data.purchasedItems) ? data.purchasedItems : [];
    isTikTokMonetized = data.isTikTokMonetized || false;
    tiktokIncome = Number(data.tiktokIncome) || 0;
    tiktokMonetizationWeeks = Number(data.tiktokMonetizationWeeks) || 0;
    isMarried = data.isMarried || false;
    spouseName = data.spouseName || "";
    actionCooldowns = data.actionCooldowns || {
      writeScript: 0,
      blockbuster: 0,
      aListParty: 0,
      voiceAct: 0,
      endorsement: 0,
      networking: 0,
      merchLine: 0
    };
    actionAvailability = data.actionAvailability || {
      writeScript: true,
      blockbuster: false,
      aListParty: false,
      voiceAct: false,
      endorsement: false,
      networking: false,
      merchLine: false
    };
    actionUses = data.actionUses || {
      writeScript: 0,
      blockbuster: 0,
      aListParty: 0,
      voiceAct: 0,
      endorsement: 0,
      networking: 0,
      merchLine: 0
    };

    // Ensure critical UI fields are set
    skill = getSkillByXP(practiceXP);
    document.getElementById("currencySymbol").textContent = currencySymbol;
    document.getElementById("weekNum").textContent = week;
    document.getElementById("startDateDisplay").textContent = startDate;
    document.getElementById("ageDisplay").textContent = age;
    document.getElementById("nameDisplay").textContent = data.stageName ? `${data.stageName} (${data.fullName || ''})` : "Unknown Actor";
    document.getElementById("cityDisplay").textContent = data.city || "Unknown City";
    document.getElementById("profileForm").style.display = "none";
    document.getElementById("game").style.display = "block";

    updateStats();
    updateLifestyleButtons();
    checkEnergy();

    console.log("Game loaded successfully.");
    return true;
  } catch (e) {
    console.error("Load failed:", e);
    localStorage.removeItem("actorSimSave"); // Clear corrupted save
    document.getElementById("profileForm").style.display = "block";
    document.getElementById("game").style.display = "none";
    showInfoModal("Failed to load saved game due to an error. Starting fresh.");
    return false;
  }
}

    function updateLifestyleButtons() {
  const lifestyleChoices = document.getElementById("lifestyleChoices");
  lifestyleChoices.innerHTML = "";
  lifestyleItems.forEach((item, index) => {
    const convertedPrice = convertCurrency(item.price);
    const isPurchased = purchasedItems.includes(index);
    const button = document.createElement("button");
    button.className = "choice-btn";
    button.textContent = isPurchased
      ? `🛍️ ${item.name} (Owned)`
      : `🛍️ Buy ${item.name} (${currencySymbol}${convertedPrice}, +${item.fameReward} Fame)`;
    button.disabled = isPurchased || money < convertedPrice;
    button.onclick = () => buyLifestyleItem(index);
    lifestyleChoices.appendChild(button);
  });

  // Add Get Married button
  const marriageButton = document.createElement("button");
  marriageButton.className = "choice-btn";
  marriageButton.textContent = isMarried
    ? `💍 Married to ${spouseName}`
    : `💍 Get Married (${currencySymbol}10,000, +0.5 Fame, +100 Followers)`;
  marriageButton.disabled = isMarried || age < 20 || money < convertCurrency(10000) || fame < 20 || energy < 30;
  marriageButton.onclick = getMarried;
  lifestyleChoices.appendChild(marriageButton);
}

    async function buyLifestyleItem(itemIndex) {
      const item = lifestyleItems[itemIndex];
      const convertedPrice = convertCurrency(item.price);

      if (money < convertedPrice) {
        await showInfoModal(`Not enough money to purchase ${item.name} (${currencySymbol}${convertedPrice} required).`);
        return;
      }
      if (purchasedItems.includes(itemIndex)) {
        await showInfoModal(`You already own ${item.name}.`);
        return;
      }

      money -= convertedPrice;
      fame += item.fameReward;
      purchasedItems.push(itemIndex);

      await showInfoModal(`🗓️ Week ${week} Action:\n🛍️ Purchased ${item.name}! +${item.fameReward} Fame`);
      fame = Math.floor(fame || 1);
      updateStats();
      updateLifestyleButtons();
      checkEnergy();
      saveGame();
    }

function updateWeekChoices() {
  const buttons = {
    writeScript: document.getElementById("writeScriptBtn"),
    blockbuster: document.getElementById("blockbusterBtn"),
    aListParty: document.getElementById("aListPartyBtn"),
    voiceAct: document.getElementById("voiceActBtn"),
    endorsement: document.getElementById("endorsementBtn"),
    networking: document.getElementById("networkingBtn"),
    merchLine: document.getElementById("merchLineBtn")
  };

  // Write Script
  if (actionCooldowns.writeScript > 0) {
    buttons.writeScript.textContent = `✍️ Write Script (Available in ${actionCooldowns.writeScript} weeks)`;
    buttons.writeScript.disabled = true;
  } else if (actionUses.writeScript >= MAX_ACTION_USES_PER_YEAR.writeScript) {
    buttons.writeScript.textContent = `✍️ Write Script (Yearly limit reached)`;
    buttons.writeScript.disabled = true;
  } else {
    buttons.writeScript.textContent = `✍️ Write Script -30⚡`;
    buttons.writeScript.disabled = practiceXP < 7 || energy < 30;
  }

  // Hire for Blockbuster Movie
  if (actionCooldowns.blockbuster > 0) {
    buttons.blockbuster.textContent = `🎬 Hire for Blockbuster Movie (Available in ${actionCooldowns.blockbuster} weeks)`;
    buttons.blockbuster.disabled = true;
  } else if (actionUses.blockbuster >= MAX_ACTION_USES_PER_YEAR.blockbuster) {
    buttons.blockbuster.textContent = `🎬 Hire for Blockbuster Movie (Yearly limit reached)`;
    buttons.blockbuster.disabled = true;
  } else if (!actionAvailability.blockbuster) {
    buttons.blockbuster.textContent = `🎬 Hire for Blockbuster Movie (No roles available)`;
    buttons.blockbuster.disabled = true;
  } else {
    buttons.blockbuster.textContent = `🎬 Hire for Blockbuster Movie -40⚡`;
    buttons.blockbuster.disabled = fame < 45 || energy < 40;
  }

  // Attend A-List Party
  if (actionCooldowns.aListParty > 0) {
    buttons.aListParty.textContent = `🥂 Attend A-List Party (Available in ${actionCooldowns.aListParty} weeks)`;
    buttons.aListParty.disabled = true;
  } else if (actionUses.aListParty >= MAX_ACTION_USES_PER_YEAR.aListParty) {
    buttons.aListParty.textContent = `🥂 Attend A-List Party (Yearly limit reached)`;
    buttons.aListParty.disabled = true;
  } else if (!actionAvailability.aListParty) {
    buttons.aListParty.textContent = `🥂 Attend A-List Party (No invitations)`;
    buttons.aListParty.disabled = true;
  } else {
    buttons.aListParty.textContent = `🥂 Attend A-List Party (${currencySymbol}2,500) -25⚡`;
    buttons.aListParty.disabled = money < 2500 || fame < 20 || energy < 25;
  }

  // Voice Act in Video Game
  if (actionCooldowns.voiceAct > 0) {
    buttons.voiceAct.textContent = `🎮 Voice Act in Video Game (Available in ${actionCooldowns.voiceAct} weeks)`;
    buttons.voiceAct.disabled = true;
  } else if (actionUses.voiceAct >= MAX_ACTION_USES_PER_YEAR.voiceAct) {
    buttons.voiceAct.textContent = `🎮 Voice Act in Video Game (Yearly limit reached)`;
    buttons.voiceAct.disabled = true;
  } else if (!actionAvailability.voiceAct) {
    buttons.voiceAct.textContent = `🎮 Voice Act in Video Game (No roles available)`;
    buttons.voiceAct.disabled = true;
  } else {
    buttons.voiceAct.textContent = `🎮 Voice Act in Video Game -30⚡`;
    buttons.voiceAct.disabled = fame < 15 || energy < 30;
  }

  // Do Brand Endorsement Deal
  if (actionCooldowns.endorsement > 0) {
    buttons.endorsement.textContent = `📺 Do Brand Endorsement Deal (Available in ${actionCooldowns.endorsement} weeks)`;
    buttons.endorsement.disabled = true;
  } else if (actionUses.endorsement >= MAX_ACTION_USES_PER_YEAR.endorsement) {
    buttons.endorsement.textContent = `📺 Do Brand Endorsement Deal (Yearly limit reached)`;
    buttons.endorsement.disabled = true;
  } else if (!actionAvailability.endorsement) {
    buttons.endorsement.textContent = `📺 Do Brand Endorsement Deal (No offers available)`;
    buttons.endorsement.disabled = true;
  } else {
    buttons.endorsement.textContent = `📺 Do Brand Endorsement Deal (${currencySymbol}1,000) -20⚡`;
    buttons.endorsement.disabled = money < 1000 || fame < 30 || energy < 20;
  }

  // Attend Industry Networking Event
  if (actionCooldowns.networking > 0) {
    buttons.networking.textContent = `🤝 Attend Industry Networking Event (Available in ${actionCooldowns.networking} weeks)`;
    buttons.networking.disabled = true;
  } else if (actionUses.networking >= MAX_ACTION_USES_PER_YEAR.networking) {
    buttons.networking.textContent = `🤝 Attend Industry Networking Event (Yearly limit reached)`;
    buttons.networking.disabled = true;
  } else if (!actionAvailability.networking) {
    buttons.networking.textContent = `🤝 Attend Industry Networking Event (No events available)`;
    buttons.networking.disabled = true;
  } else {
    buttons.networking.textContent = `🤝 Attend Industry Networking Event (${currencySymbol}2,000) -25⚡`;
    buttons.networking.disabled = money < 2000 || fame < 25 || practiceXP < 20 || energy < 25;
  }

  // Launch Merchandise Line
  if (actionCooldowns.merchLine > 0) {
    buttons.merchLine.textContent = `🛍️ Launch Merchandise Line (Available in ${actionCooldowns.merchLine} weeks)`;
    buttons.merchLine.disabled = true;
  } else if (actionUses.merchLine >= MAX_ACTION_USES_PER_YEAR.merchLine) {
    buttons.merchLine.textContent = `🛍️ Launch Merchandise Line (Yearly limit reached)`;
    buttons.merchLine.disabled = true;
  } else if (!actionAvailability.merchLine) {
    buttons.merchLine.textContent = `🛍️ Launch Merchandise Line (Not trending now)`;
    buttons.merchLine.disabled = true;
  } else {
    buttons.merchLine.textContent = `🛍️ Launch Merchandise Line (${currencySymbol}15,000) -40⚡`;
    buttons.merchLine.disabled = money < 15000 || fame < 35 || followers < 500 || energy < 40;
  }
}

    function generateReview(isSuccess, reward) {
      const critics = [
        { name: "Jane Doe", outlet: "Variety" },
        { name: "John Smith", outlet: "The Hollywood Reporter" },
        { name: "Emma Lee", outlet: "Screen Daily" },
        { name: "Michael Brown", outlet: "IndieWire" },
        { name: "Sarah Chen", outlet: "The Wrap" }
      ];
      const positiveReviews = [
        "A captivating performance that lights up the screen.",
        "Shows remarkable emotional depth for their experience level.",
        "A breakout star with undeniable charisma.",
        "Delivers a nuanced portrayal that resonates with audiences.",
        "Commands every scene with confidence and skill."
      ];
      const neutralReviews = [
        "A solid effort, though there's room to grow.",
        "Shows promise but needs more polish in key moments.",
        "A decent performance that blends into the ensemble.",
        "Competent acting, but lacks a defining spark.",
        "A serviceable turn, with potential for more impact."
      ];
      const negativeReviews = [
        "Struggles to connect emotionally with the role.",
        "Performance feels flat and uninspired.",
        "Lacks the screen presence needed for a lead role.",
        "Delivery feels forced and unconvincing.",
        "Seems out of their depth in this production."
      ];

      const critic = critics[Math.floor(Math.random() * critics.length)];
      let reviewSnippets = [];
      let fameChange = 0;

      if (practiceXP >= 20 && fame >= 50 && isSuccess) {
        reviewSnippets = [positiveReviews[Math.floor(Math.random() * positiveReviews.length)]];
        if (Math.random() < 0.3) {
          reviewSnippets.push(positiveReviews[Math.floor(Math.random() * positiveReviews.length)]);
          fameChange = 0.1;
        } else {
          reviewSnippets.push(neutralReviews[Math.floor(Math.random() * neutralReviews.length)]);
        }
      } else if (practiceXP >= 7 && fame >= 20 && isSuccess) {
        reviewSnippets = [positiveReviews[Math.floor(Math.random() * positiveReviews.length)]];
        reviewSnippets.push(neutralReviews[Math.floor(Math.random() * neutralReviews.length)]);
      } else if (practiceXP < 7 && fame < 20 && isSuccess) {
        reviewSnippets = [neutralReviews[Math.floor(Math.random() * neutralReviews.length)]];
        if (Math.random() < 0.5) {
          reviewSnippets.push(positiveReviews[Math.floor(Math.random() * positiveReviews.length)]);
        } else {
          reviewSnippets.push(neutralReviews[Math.floor(Math.random() * neutralReviews.length)]);
        }
      } else if (!isSuccess) {
        reviewSnippets = [negativeReviews[Math.floor(Math.random() * negativeReviews.length)]];
        if (Math.random() < 0.5) {
          reviewSnippets.push(neutralReviews[Math.floor(Math.random() * neutralReviews.length)]);
        } else {
          reviewSnippets.push(negativeReviews[Math.floor(Math.random() * negativeReviews.length)]);
          if (practiceXP < 7 && fame < 20) fameChange = -0.1;
        }
      }

      if (reward && reward > 5000) {
        reviewSnippets[0] = positiveReviews[Math.floor(Math.random() * positiveReviews.length)];
        fameChange = fameChange || 0.1;
      }

      return { review: `${critic.name}, ${critic.outlet}: ${reviewSnippets.join(" ")}`, fameChange };
    }

    async function generateFollowerReaction(isSuccess, isBlockbuster = false) {
      let followerGain = 0;
      let fameChange = 0;
      let reaction = "";

      if (isSuccess) {
        followerGain = isBlockbuster ? Math.floor(Math.random() * 151) + 50 : Math.floor(Math.random() * 101) + 50;
        fameChange = 0.25;
        reaction = isBlockbuster
          ? `📱 Your fans are buzzing about your blockbuster role! +${followerGain} Followers, +0.25 Fame`
          : `📱 Your followers loved seeing you in that role! +${followerGain} Followers, +0.25 Fame`;
      } else {
        followerGain = Math.floor(Math.random() * 41) + 10;
        reaction = `📱 Some fans noticed your audition attempt. +${followerGain} Followers`;
      }

      followers += followerGain;
      fame += fameChange;
      await showInfoModal(reaction);
      fame = Math.floor(fame || 1);
      updateStats();
      saveGame();
    }

    async function startGame() {
  const fullName = document.getElementById("fullName").value;
  const stageName = document.getElementById("stageName").value;
  age = Number(document.getElementById("age").value);
  const city = document.getElementById("city").value;
  startDate = document.getElementById("startDate").value;
  currencySymbol = document.getElementById("currency").value;

  year = 1; // Initialize year for new game

  if (!fullName || !stageName || !age || !city || !startDate) {
    let retry = await showModal("Please fill in all fields, including the starting date. Retry?");
    if (retry) return;
    else return;
  }
  if (age < 17) {
    let retry = await showModal("Minimum age to enter is 17. Retry?");
    if (retry) return;
    else return;
  }
  if (age > 60) {
    let retry = await showModal("Maximum age to enter is 60. Retry?");
    if (retry) return;
    else return;
  }

  money = getStartingMoney(currencySymbol);

  document.getElementById("nameDisplay").textContent = `${stageName} (${fullName})`;
  document.getElementById("cityDisplay").textContent = city;
  document.getElementById("ageDisplay").textContent = age;
  document.getElementById("startDateDisplay").textContent = startDate;
  document.getElementById("currencySymbol").textContent = currencySymbol;

  document.getElementById("profileForm").style.display = "none";
  document.getElementById("game").style.display = "block";
  updateStats();
  updateLifestyleButtons();
  saveGame();
}

    async function chooseAction(choice, cost) {
  if (energy < cost) {
    await showModal("Not enough energy for this action. Try another action?");
    return;
  }
  if (choice === 1 && money < 1000) {
    await showModal("Not enough money for an audition. Try another action?");
    return;
  }
  if (choice === 4 && money < 2000) {
    await showModal("Not enough money to hire a talent agent. Try another action?");
    return;
  }
  if (choice === 6) {
    if (!actionAvailability.blockbuster) {
      await showModal("No blockbuster movie roles are available right now. Try another action?");
      return;
    }
    if (actionUses.blockbuster >= MAX_ACTION_USES_PER_YEAR.blockbuster) {
      await showModal("You've reached the yearly limit for blockbuster movie roles. Try another action?");
      return;
    }
    if (fame < 45) {
      await showModal("You need at least 45 Fame to be considered for blockbuster movie roles. Try another action?");
      return;
    }
  }
  energy -= cost;
  let outcome = "";

  if (choice === 1) {
    money -= 1000;
    let chance = Math.random() + (practiceXP * 0.01);
    if (chance < 0.4) {
      fame += 1;
      money += 3000;
      blockbusters += 1;
      outcome = `🎉 You got a minor acting role! +${currencySymbol}3000, +1 Fame, +1 Blockbuster`;
      let { review, fameChange } = generateReview(true, 3000);
      await showInfoModal(`${review} (${fameChange >= 0 ? '+' : ''}${fameChange} Fame)`);
      fame = Math.max(fame + fameChange, 1);
      await generateFollowerReaction(true, true);
    } else {
      fame += 0.25;
      outcome = "😕 You tried but didn’t get selected. +0.25 Fame";
      await generateFollowerReaction(false);
    }
  } else if (choice === 2) {
    let tiktokOutcome = "";
    if (Math.random() < 0.2) {
      const followerGain = 500 + Math.floor(Math.random() * 501);
      followers += followerGain;
      fame += 0.5;
      tiktokOutcome = `📈 Your monologue got some buzz! +${followerGain} Followers, +0.5 Fame`;
    } else {
      const followerGain = 5 + Math.floor(Math.random() * 16);
      followers += followerGain;
      fame += 0.25;
      tiktokOutcome = `👻 Your post got a few views. +${followerGain} Followers, +0.25 Fame`;
    }
    outcome = tiktokOutcome;
    if (practiceXP >= 12) {
      if (Math.random() < 0.1) {
        const hireReward = 500 + (fame * 25);
        let accept = await showModal(`🎬 Your TikTok impressed a director! Accept role? (+${currencySymbol}${hireReward}, +0.5 Fame, +1 Blockbuster)`);
        if (accept) {
          money += hireReward;
          fame += 0.5;
          blockbusters += 1;
          outcome += `\n🎬 You accepted the director’s role! +${currencySymbol}${hireReward}, +0.5 Fame, +1 Blockbuster`;
          let { review, fameChange } = generateReview(true, hireReward);
          await showInfoModal(`${review} (${fameChange >= 0 ? '+' : ''}${fameChange} Fame)`);
          fame = Math.max(fame + fameChange, 1);
          await generateFollowerReaction(true, true);
        } else {
          outcome += "\n🙅 You declined the director’s offer.";
        }
      } else if (Math.random() < 0.2) {
        fame += 0.25;
        outcome += "\n🤝 Your TikTok caught a producer's eye! +0.25 Fame";
      }
    }
  } else if (choice === 3) {
    fame += 0.5;
    practiceXP++;
    outcome = "🎭 Workshop attended. You feel sharper. +0.5 Fame, +1 XP";
    if (Math.random() < 0.2) {
      let scriptAccepted = await showModal("📜 You gained inspiration. Accept script? (+1 Script)");
      if (scriptAccepted) {
        scripts += 1;
        outcome += "\n📜 You gained a script! +1 Script";
      } else {
        outcome += "\n🙅 You discarded the script idea.";
      }
    }
  } else if (choice === 4) {
    money -= 2000;
    hasAgent = true;
    if (fame >= 10) {
      let chance = Math.random() + (practiceXP * 0.01);
      if (chance < 0.6) {
        fame += 1.5;
        money += 4000;
        blockbusters += 1;
        outcome = `🎬 Your agent landed you a big audition! You got the role! +${currencySymbol}4000, +1.5 Fame, +1 Blockbuster`;
        let { review, fameChange } = generateReview(true, 4000);
        await showInfoModal(`${review} (${fameChange >= 0 ? '+' : ''}${fameChange} Fame)`);
        fame = Math.max(fame + fameChange, 1);
        await generateFollowerReaction(true, true);
      } else {
        fame += 0.5;
        outcome = "😕 Your agent got you a big audition, but you didn’t get the role. +0.5 Fame";
        await generateFollowerReaction(false);
      }
    } else {
      fame += 0.25;
      outcome = "🤝 Your agent couldn’t find big auditions yet. +0.25 Fame";
    }
  } else if (choice === 5) {
    const jobs = ["waiter", "barista", "rideshare driver", "retail worker"];
    const job = jobs[Math.floor(Math.random() * jobs.length)];
    const jobReward = Math.floor(Math.random() * 201) + 200;
    money += jobReward;
    outcome = `💼 You worked as a ${job}! +${currencySymbol}${jobReward}`;
  } else if (choice === 6) {
    actionCooldowns.blockbuster = 26; // 6-month cooldown
    actionUses.blockbuster++;
    actionAvailability.blockbuster = false;
    let chance = Math.random() + (practiceXP * 0.01);
    if (chance < 0.4) { // Reduced success chance
      const movieReward = 1000 + (fame * 30); // Reduced reward multiplier
      money += movieReward;
      fame += 0.5; // Reduced fame reward
      blockbusters += 1;
      outcome = `🎬 You were hired for a blockbuster movie role! +${currencySymbol}${movieReward}, +0.5 Fame, +1 Blockbuster`;
      let { review, fameChange } = generateReview(true, movieReward);
      await showInfoModal(`${review} (${fameChange >= 0 ? '+' : ''}${fameChange} Fame)`);
      fame = Math.max(fame + fameChange, 1);
      await generateFollowerReaction(true, true);
    } else {
      fame += 0.1;
      outcome = "😕 You auditioned for a blockbuster movie role but weren’t hired. +0.1 Fame";
      await generateFollowerReaction(false);
    }
  }

  await showInfoModal(`🗓️ Week ${week} Action:\n${outcome}`);
  fame = Math.floor(fame || 1);
  skill = getSkillByXP(practiceXP);
  updateStats();
  updateWeekChoices();
  updateLifestyleButtons();
  checkEnergy();
  saveGame();
}

    async function practice() {
      if (energy < 30) {
        await showModal("You're too tired to practice. Try another action?");
        return;
      }
      energy -= 30;
      practiceXP++;
      let outcome = "🧘 You practiced. XP +1. You're improving slowly.";
      if (Math.random() < 0.1) fame += 0.25;
      fame = Math.floor(fame || 1);
      skill = getSkillByXP(practiceXP);
      await showInfoModal(`🗓️ Week ${week} Action:\n${outcome}`);
      updateStats();
      updateLifestyleButtons();
      checkEnergy();
      saveGame();
    }

    async function writeScript() {
  if (!actionAvailability.writeScript) {
    await showModal("You're not inspired to write a script right now. Try another action?");
    return;
  }
  if (actionUses.writeScript >= MAX_ACTION_USES_PER_YEAR.writeScript) {
    await showModal("You've reached the yearly limit for writing scripts. Try another action?");
    return;
  }
  if (energy < 30) {
    await showModal("Not enough energy to write a script. Try another action?");
    return;
  }
  if (practiceXP < 7) {
    await showModal("You need at least Improving skill (7 XP) to write a script. Try another action?");
    return;
  }
  energy -= 30;
  scripts += 1;
  actionCooldowns.writeScript = 8; // 2-month cooldown
  actionUses.writeScript++;
  let qualityChance = Math.min(practiceXP * 0.02, 0.8);
  let scriptQuality = Math.random() < qualityChance ? "High-Quality" : "Standard";
  scriptQualities.push(scriptQuality);
  let outcome = `✍️ You wrote a ${scriptQuality} script! +1 Script`;
  if (Math.random() < 0.05 && fame >= 20) { // Reduced fame gain chance
    fame += 0.2;
    outcome += " +0.2 Fame due to industry buzz!";
  }
  await showInfoModal(`🗓️ Week ${week} Action:\n${outcome}`);
  fame = Math.floor(fame || 1);
  updateStats();
  updateWeekChoices();
  updateLifestyleButtons();
  checkEnergy();
  saveGame();
}

    async function sellScript() {
  if (energy < 20) {
    await showModal("Not enough energy to sell a script. Try another action?");
    return;
  }
  if (scripts < 1) {
    await showModal("You need a script to sell. Try another action?");
    return;
  }
  if (practiceXP < 7) {
    await showModal("You need at least Improving skill (7 XP) to sell a script. Try another action?");
    return;
  }
  energy -= 20;
  scripts -= 1;
  let scriptQuality = scriptQualities.shift() || "Standard"; // Get quality of the sold script

  // Define buyers based on fame
  const bigBuyers = [
    { name: "Netflix", type: "Streaming Platform" },
    { name: "Warner Bros.", type: "Studio" },
    { name: "Universal Pictures", type: "Studio" },
    { name: "Lionsgate", type: "Studio" },
    { name: "A24", type: "Independent Studio" }
  ];
  const smallBuyers = [
    { name: "Jane Doe Productions", type: "Independent Producer" },
    { name: "Local Theater Group", type: "Community Theater" },
    { name: "Indie Filmmaker", type: "Independent Filmmaker" },
    { name: "Student Film Project", type: "Student Production" }
  ];

  // Determine buyer based on fame
  let buyerPool = fame >= 30 ? bigBuyers : smallBuyers;
  const buyer = buyerPool[Math.floor(Math.random() * buyerPool.length)];

  // Calculate script value based on fame, skill, and quality
  let baseValue;
  if (fame < 20) {
    baseValue = 500 + Math.floor(Math.random() * 501); // Very low for low fame
  } else if (fame < 50) {
    baseValue = 2000 + Math.floor(Math.random() * 3001); // Moderate for medium fame
  } else {
    baseValue = 10000 + Math.floor(Math.random() * 20001); // High for high fame
  }

  // Adjust value based on script quality and skill
  let qualityMultiplier = scriptQuality === "High-Quality" ? 1.5 : 1;
  let skillMultiplier = Math.min(practiceXP * 0.05, 2); // Skill boosts value up to 2x
  let scriptValue = Math.round(baseValue * qualityMultiplier * skillMultiplier);

  // Reduce chance of high-value sales for low fame
  let saleChance = Math.min(fame * 0.01 + (scriptQuality === "High-Quality" ? 0.2 : 0), 0.9);
  if (fame < 50 && Math.random() > saleChance) {
    scriptValue = Math.round(scriptValue * 0.5); // Halve value for low-fame, low-chance sales
  }

  const convertedValue = convertCurrency(scriptValue);
  let accept = await showModal(`💸 ${buyer.name} (${buyer.type}) wants to buy your ${scriptQuality} script for ${currencySymbol}${convertedValue}! Accept?`);
  let outcome = "";
  if (accept) {
    money += convertedValue;
    if (fame >= 30 && scriptQuality === "High-Quality" && Math.random() < 0.2) {
      fame += 0.5;
      outcome = `💸 Sold your ${scriptQuality} script to ${buyer.name} for ${currencySymbol}${convertedValue}! +0.5 Fame due to industry recognition.`;
      await generateFollowerReaction(true);
    } else if (Math.random() < 0.1) {
      fame += 0.25;
      outcome = `💸 Sold your ${scriptQuality} script to ${buyer.name} for ${currencySymbol}${convertedValue}! +0.25 Fame`;
    } else {
      outcome = `💸 Sold your ${scriptQuality} script to ${buyer.name} for ${currencySymbol}${convertedValue}!`;
    }
  } else {
    outcome = `🙅 You declined to sell your ${scriptQuality} script to ${buyer.name}.`;
  }

  await showInfoModal(`🗓️ Week ${week} Action:\n${outcome}`);
  fame = Math.floor(fame || 1);
  updateStats();
  updateLifestyleButtons();
  checkEnergy();
  saveGame();
}

    async function attendAListParty() {
  if (!actionAvailability.aListParty) {
    await showModal("No A-List party invitations are available right now. Try another action?");
    return;
  }
  if (actionUses.aListParty >= MAX_ACTION_USES_PER_YEAR.aListParty) {
    await showModal("You've reached the yearly limit for attending A-List parties. Try another action?");
    return;
  }
  if (energy < 25) {
    await showModal("Not enough energy to attend an A-List party. Try another action?");
    return;
  }
  if (money < 2500) {
    await showModal(`Not enough money to attend an A-List party (${currencySymbol}2,500 required). Try another action?`);
    return;
  }
  if (fame < 20) {
    await showModal("You need at least 20 Fame to attend an A-List party. Try another action?");
    return;
  }
  energy -= 25;
  money -= 2500;
  actionCooldowns.aListParty = 8; // 2-month cooldown
  actionUses.aListParty++;
  actionAvailability.aListParty = false;
  let outcome = "";
  let chance = Math.random();
  if (chance < 0.25) { // Slightly reduced success chance
    const partyReward = Math.floor(Math.random() * 3001) + 3000; // Lower reward
    let accept = await showModal(`🎉 You networked at the A-List party and landed a movie role! Accept? (+${currencySymbol}${partyReward}, +1.5 Fame, +1 Blockbuster)`);
    if (accept) {
      fame += 1.5; // Reduced fame reward
      blockbusters += 1;
      money += partyReward;
      outcome = `🎉 You accepted the movie role! +${currencySymbol}${partyReward}, +1.5 Fame, +1 Blockbuster`;
      let { review, fameChange } = generateReview(true, partyReward);
      await showInfoModal(`${review} (${fameChange >= 0 ? '+' : ''}${fameChange} Fame)`);
      fame = Math.max(fame + fameChange, 1);
      await generateFollowerReaction(true, true);
    } else {
      outcome = "🙅 You declined the movie role.";
    }
  } else if (chance < 0.5) {
    fame = Math.max(fame - 0.5, 1); // Reduced fame penalty
    outcome = `😳 A scandal at the A-List party hurt your reputation! -0.5 Fame`;
  } else {
    fame += 0.2; // Reduced fame gain
    outcome = `🥂 You mingled at the A-List party and made some connections. +0.2 Fame`;
  }
  await showInfoModal(`🗓️ Week ${week} Action:\n${outcome}`);
  fame = Math.floor(fame || 1);
  updateStats();
  updateWeekChoices();
  updateLifestyleButtons();
  checkEnergy();
  saveGame();
}

    async function voiceActVideoGame() {
  if (!actionAvailability.voiceAct) {
    await showModal("No voice acting roles are available right now. Try another action?");
    return;
  }
  if (actionUses.voiceAct >= MAX_ACTION_USES_PER_YEAR.voiceAct) {
    await showModal("You've reached the yearly limit for voice acting roles. Try another action?");
    return;
  }
  if (energy < 30) {
    await showModal("Not enough energy to voice act in a video game. Try another action?");
    return;
  }
  if (fame < 15) {
    await showModal("You need at least 15 Fame to voice act in a video game. Try another action?");
    return;
  }
  energy -= 30;
  actionCooldowns.voiceAct = 12; // 3-month cooldown
  actionUses.voiceAct++;
  actionAvailability.voiceAct = false;
  let outcome = "";
  let chance = Math.random() + (practiceXP * 0.01);
  if (chance < 0.5) { // Reduced success chance
    const followerGain = Math.floor(Math.random() * 101) + 50; // Reduced follower gain
    fame += 0.75; // Reduced fame reward
    followers += followerGain;
    voiceActingIncome = 400; // Reduced income
    voiceActingWeeks = 8; // Reduced duration
    outcome = `🎮 Your video game voice acting role was a hit! +${followerGain} Followers, +0.75 Fame, +${currencySymbol}400/week for 8 weeks`;
    await generateFollowerReaction(true);
  } else {
    fame += 0.2; // Reduced fame gain
    outcome = `😕 Your video game voice acting role didn’t stand out, but you gained some exposure. +0.2 Fame`;
    await generateFollowerReaction(false);
  }
  await showInfoModal(`🗓️ Week ${week} Action:\n${outcome}`);
  fame = Math.floor(fame || 1);
  updateStats();
  updateWeekChoices();
  updateLifestyleButtons();
  checkEnergy();
  saveGame();
}

    async function doBrandEndorsement() {
  if (!actionAvailability.endorsement) {
    await showModal("No brand endorsement offers are available right now. Try another action?");
    return;
  }
  if (actionUses.endorsement >= MAX_ACTION_USES_PER_YEAR.endorsement) {
    await showModal("You've reached the yearly limit for brand endorsements. Try another action?");
    return;
  }
  if (energy < 20) {
    await showModal("Not enough energy to do a brand endorsement deal. Try another action?");
    return;
  }
  if (money < 1000) {
    await showModal(`Not enough money for a brand endorsement deal (${currencySymbol}1,000 required). Try another action?`);
    return;
  }
  if (fame < 30) {
    await showModal("You need at least 30 Fame to do a brand endorsement deal. Try another action?");
    return;
  }
  energy -= 20;
  money -= 1000;
  actionCooldowns.endorsement = 8; // 2-month cooldown
  actionUses.endorsement++;
  actionAvailability.endorsement = false;
  let outcome = "";
  let chance = Math.random() + (practiceXP * 0.01);
  if (chance < 0.6) { // Reduced success chance
    const endorsementReward = Math.floor(Math.random() * 7001) + 5000; // Reduced reward
    const followerGain = Math.floor(Math.random() * 151) + 50; // Reduced follower gain
    fame += 0.4; // Reduced fame reward
    followers += followerGain;
    money += endorsementReward;
    outcome = `📺 Your brand endorsement deal was a success! +${currencySymbol}${endorsementReward}, +${followerGain} Followers, +0.4 Fame`;
  } else {
    fame += 0.2; // Reduced fame gain
    outcome = `😕 The brand endorsement deal didn’t resonate, but you gained some exposure. +0.2 Fame`;
  }
  await showInfoModal(`🗓️ Week ${week} Action:\n${outcome}`);
  fame = Math.floor(fame || 1);
  updateStats();
  updateWeekChoices();
  updateLifestyleButtons();
  checkEnergy();
  saveGame();
}

    async function attendNetworkingEvent() {
  if (!actionAvailability.networking) {
    await showModal("No industry networking events are available right now. Try another action?");
    return;
  }
  if (actionUses.networking >= MAX_ACTION_USES_PER_YEAR.networking) {
    await showModal("You've reached the yearly limit for networking events. Try another action?");
    return;
  }
  if (energy < 25) {
    await showModal("Not enough energy to attend an industry networking event. Try another action?");
    return;
  }
  if (money < 2000) {
    await showModal(`Not enough money to attend an industry networking event (${currencySymbol}2,000 required). Try another action?`);
    return;
  }
  if (fame < 25) {
    await showModal("You need at least 25 Fame to attend an industry networking event. Try another action?");
    return;
  }
  if (practiceXP < 20) {
    await showModal("You need at least Pro skill (20 XP) to attend an industry networking event. Try another action?");
    return;
  }
  energy -= 25;
  money -= 2000;
  actionCooldowns.networking = 8; // 2-month cooldown
  actionUses.networking++;
  actionAvailability.networking = false;
  let outcome = "";
  let chance = Math.random();
  if (chance < 0.2) { // Reduced success chance
    const producerReward = Math.floor(Math.random() * 4001) + 4000; // Reduced reward
    let accept = await showModal(`🤝 You met a top producer at the networking event and landed a big role! Accept? (+${currencySymbol}${producerReward}, +1.5 Fame, +1 Blockbuster)`);
    if (accept) {
      fame += 1.5; // Reduced fame reward
      blockbusters += 1;
      money += producerReward;
      outcome = `🤝 You accepted the big role! +${currencySymbol}${producerReward}, +1.5 Fame, +1 Blockbuster`;
      let { review, fameChange } = generateReview(true, producerReward);
      await showInfoModal(`${review} (${fameChange >= 0 ? '+' : ''}${fameChange} Fame)`);
      fame = Math.max(fame + fameChange, 1);
      await generateFollowerReaction(true, true);
    } else {
      outcome = "🙅 You declined the big role.";
    }
  } else if (chance < 0.5) { // Adjusted probability
    const callbackReward = Math.floor(Math.random() * 2001) + 1500; // Reduced reward
    let isBlockbuster = Math.random() < 0.4; // Reduced blockbuster chance
    let accept = await showModal(`🎬 You got a callback for a supporting role at the networking event! Accept? (+${currencySymbol}${callbackReward}, +0.75 Fame${isBlockbuster ? ", +1 Blockbuster" : ""})`);
    if (accept) {
      fame += 0.75; // Reduced fame reward
      money += callbackReward;
      if (isBlockbuster) blockbusters += 1;
      outcome = `🎬 You accepted the supporting role! +${currencySymbol}${callbackReward}, +0.75 Fame${isBlockbuster ? ", +1 Blockbuster" : ""}`;
      let { review, fameChange } = generateReview(true, callbackReward);
      await showInfoModal(`${review} (${fameChange >= 0 ? '+' : ''}${fameChange} Fame)`);
      fame = Math.max(fame + fameChange, 1);
      await generateFollowerReaction(true, isBlockbuster);
    } else {
      outcome = "🙅 You declined the supporting role.";
    }
  } else {
    fame += 0.2; // Reduced fame gain
    outcome = `🤝 You made some connections at the networking event. +0.2 Fame`;
  }
  await showInfoModal(`🗓️ Week ${week} Action:\n${outcome}`);
  fame = Math.floor(fame || 1);
  updateStats();
  updateWeekChoices();
  updateLifestyleButtons();
  checkEnergy();
  saveGame();
}

    async function launchMerchLine() {
  if (!actionAvailability.merchLine) {
    await showModal("Your brand isn’t trending enough to launch a merchandise line right now. Try another action?");
    return;
  }
  if (actionUses.merchLine >= MAX_ACTION_USES_PER_YEAR.merchLine) {
    await showModal("You've reached the yearly limit for launching merchandise lines. Try another action?");
    return;
  }
  if (energy < 40) {
    await showModal("Not enough energy to launch a merchandise line. Try another action?");
    return;
  }
  if (money < 15000) {
    await showModal(`Not enough money to launch a merchandise line (${currencySymbol}15,000 required). Try another action?`);
    return;
  }
  if (fame < 35) {
    await showModal("You need at least 35 Fame to launch a merchandise line. Try another action?");
    return;
  }
  if (followers < 500) {
    await showModal("You need at least 500 Followers to launch a merchandise line. Try another action?");
    return;
  }
  energy -= 40;
  money -= 15000;
  actionCooldowns.merchLine = 26; // 6-month cooldown
  actionUses.merchLine++;
  actionAvailability.merchLine = false;
  merchFailed = false; // Reset failure state
  let outcome = "";
  let chance = Math.random() + (fame * 0.005);
  if (chance < 0.5) {
    const followerGain = Math.floor(Math.random() * 201) + 50;
    fame += 0.75;
    followers += followerGain;
    merchIncome = convertCurrency(800 + Math.floor(fame * 10)); // Income scales with fame
    merchWeeks = Infinity; // Indefinite income
    outcome = `🛍️ Your merchandise line was a hit! +${followerGain} Followers, +0.75 Fame, +${currencySymbol}${merchIncome}/week indefinitely`;
    await generateFollowerReaction(true);
  } else {
    fame += 0.2;
    outcome = `😕 Your merchandise line didn’t sell well, but you gained some exposure. +0.2 Fame`;
  }
  await showInfoModal(`🗓️ Week ${week} Action:\n${outcome}`);
  fame = Math.floor(fame || 1);
  updateStats();
  updateWeekChoices();
  updateLifestyleButtons();
  checkEnergy();
  saveGame();
}

async function getMarried() {
  if (isMarried) {
    await showInfoModal("You are already married!");
    return;
  }
  if (age < 20) {
    await showInfoModal("You must be at least 20 years old to get married. Try another action?");
    return;
  }
  if (money < 10000) {
    await showInfoModal(`Not enough money to get married (${currencySymbol}10,000 required). Try another action?`);
    return;
  }
  if (fame < 20) {
    await showInfoModal("You need at least 20 Fame to attract a partner for marriage. Try another action?");
    return;
  }
  if (energy < 30) {
    await showInfoModal("Not enough energy to get married. Try another action?");
    return;
  }

  const spouseNames = [
    "Emma Watson", "Sofia Vergara", "Zendaya Coleman", "Priyanka Chopra", "Margot Robbie",
    "Gal Gadot", "Scarlett Johansson", "Natalie Portman", "Jennifer Lawrence", "Deepika Padukone"
  ];
  spouseName = spouseNames[Math.floor(Math.random() * spouseNames.length)];
  isMarried = true;
  money -= convertCurrency(10000);
  fame += 0.5;
  followers += 100;
  energy -= 30;

  const outcome = `💍 Congratulations! You married ${spouseName}! +0.5 Fame, +100 Followers`;
  await showInfoModal(`🗓️ Week ${week} Action:\n${outcome}`);
  fame = Math.floor(fame || 1);
  updateStats();
  updateLifestyleButtons();
  checkEnergy();
  saveGame();
}

    async function nextWeek() {
  week++;

  // Reset action uses annually
  if (week > 52) {
    week = 1;
    year += 1; // Increment year
    age += 1;
    actionUses = {
      writeScript: 0,
      blockbuster: 0,
      aListParty: 0,
      voiceAct: 0,
      endorsement: 0,
      networking: 0,
      merchLine: 0
    };
    await showInfoModal(`🎉 Happy New Year! You are now ${age} years old, starting Year ${year}.`);
  }

  if (age >= 70) {
    await showInfoModal("🎭 You've reached age 70. It's time to retire from your acting career. Thank you for an incredible journey!");
    resetGame();
    return;
  }

  hasAgent = false;
  energy = 100;
  document.getElementById("weekNum").textContent = week;
  document.getElementById("log").innerHTML = "";

  // Decrement cooldowns
  for (let action in actionCooldowns) {
    if (actionCooldowns[action] > 0) {
      actionCooldowns[action]--;
    }
  }

  // Update action availability based on fame and random chance
  actionAvailability.writeScript = actionCooldowns.writeScript === 0 && actionUses.writeScript < MAX_ACTION_USES_PER_YEAR.writeScript && practiceXP >= 7;
  actionAvailability.blockbuster = actionCooldowns.blockbuster === 0 && actionUses.blockbuster < MAX_ACTION_USES_PER_YEAR.blockbuster && fame >= 45 && Math.random() < 0.2;
  actionAvailability.aListParty = actionCooldowns.aListParty === 0 && actionUses.aListParty < MAX_ACTION_USES_PER_YEAR.aListParty && fame >= 20 && Math.random() < 0.3;
  actionAvailability.voiceAct = actionCooldowns.voiceAct === 0 && actionUses.voiceAct < MAX_ACTION_USES_PER_YEAR.voiceAct && fame >= 15 && Math.random() < 0.35;
  actionAvailability.endorsement = actionCooldowns.endorsement === 0 && actionUses.endorsement < MAX_ACTION_USES_PER_YEAR.endorsement && fame >= 30 && Math.random() < 0.3;
  actionAvailability.networking = actionCooldowns.networking === 0 && actionUses.networking < MAX_ACTION_USES_PER_YEAR.networking && fame >= 25 && practiceXP >= 20 && Math.random() < 0.3;
  actionAvailability.merchLine = actionCooldowns.merchLine === 0 && actionUses.merchLine < MAX_ACTION_USES_PER_YEAR.merchLine && fame >= 35 && followers >= 500 && Math.random() < 0.25;

  if (isMarried && Math.random() < 0.05) {
    const divorceAmount = Math.floor(money / 2);
    money -= divorceAmount;
    fame = Math.max(fame - 0.5, 1);
    await showInfoModal(`💔 ${spouseName} has filed for divorce and taken ${currencySymbol}${formatMoney(divorceAmount)} of your assets! -0.5 Fame`);
    isMarried = false;
    spouseName = "";
    updateStats();
    updateLifestyleButtons();
  }

  if (voiceActingWeeks > 0) {
    money += voiceActingIncome;
    voiceActingWeeks--;
    await showInfoModal(`💸 Received ${currencySymbol}${voiceActingIncome} from video game voice acting. ${voiceActingWeeks} weeks remaining.`);
    updateStats();
  }

  if (merchWeeks > 0 && !merchFailed) {
  money += merchIncome;
  if (Math.random() < 0.02) { // 2% chance of merch failure
    merchFailed = true;
    merchIncome = 0;
    merchWeeks = 0;
    await showInfoModal(`😕 Your merchandise line crashed due to market trends or a scandal! Income stopped.`);
  } else {
    await showInfoModal(`💸 Received ${currencySymbol}${merchIncome} from merchandise sales.`);
  }
  updateStats();
}

  if (tiktokMonetizationWeeks > 0) {
    money += tiktokIncome;
    tiktokMonetizationWeeks--;
    await showInfoModal(`💸 Received ${currencySymbol}${tiktokIncome} from TikTok Creator Fund. ${tiktokMonetizationWeeks} weeks remaining.`);
    updateStats();
  }

  const awardCycle = Math.floor(Math.random() * 3) + 10;
  if (week % awardCycle === 0) {
    await checkAwardShows();
  }

  let offerChance = Math.min(0.05 + ((fame || 1) / 100) * 0.2, 0.3);
  if (Math.random() < offerChance && fame >= 45) {
    let movieReward = 2000 + ((fame || 1) * 100);
    let accept = await showModal(`🎥 You've been offered a blockbuster movie role! Accept? (+${currencySymbol}${movieReward}, +1 Fame, +1 Blockbuster, -50⚡)`);
    if (accept && energy >= 50) {
      energy -= 50;
      money += movieReward;
      fame += 1;
      blockbusters += 1;
      actionCooldowns.blockbuster = 26; // 6-month cooldown for blockbuster
      actionUses.blockbuster++;
      actionAvailability.blockbuster = false;
      let { review, fameChange } = generateReview(true, movieReward);
      await showInfoModal(`${review} (${fameChange >= 0 ? '+' : ''}${fameChange} Fame)`);
      fame = Math.max(fame + fameChange, 1);
      await showInfoModal(`🎬 You starred in a blockbuster movie! Earned ${currencySymbol}${movieReward}, +1 Fame, +1 Blockbuster.`);
      await generateFollowerReaction(true, true);
      fame = Math.floor(fame || 1);
      updateStats();
    } else if (accept && energy < 50) {
      await showModal("😕 Not enough energy to take the blockbuster movie role. Try another action?");
    } else {
      await showInfoModal("🙅 You declined the blockbuster movie role offer.");
    }
  }

  enableButtons();
  updateStats();
  updateLifestyleButtons();
  checkEnergy();
  saveGame();
}

    async function checkAwardShows() {
  const awards = [
    { name: "AMVCA", fameMin: 15, blockbustersMin: 2, fameRewardWin: 2, moneyRewardWin: 5000, fameRewardNom: 0.5 },
    { name: "NEA", fameMin: 15, blockbustersMin: 2, fameRewardWin: 2, moneyRewardWin: 5000, fameRewardNom: 0.5 },
    { name: "BON Awards", fameMin: 15, blockbustersMin: 2, fameRewardWin: 2, moneyRewardWin: 5000, fameRewardNom: 0.5 },
    { name: "AMAA", fameMin: 30, blockbustersMin: 4, fameRewardWin: 3, moneyRewardWin: 10000, fameRewardNom: 0.75 },
    { name: "TIFF", fameMin: 40, blockbustersMin: 5, fameRewardWin: 4, moneyRewardWin: 20000, fameRewardNom: 1 },
    { name: "Emmys", fameMin: 50, blockbustersMin: 6, fameRewardWin: 5, moneyRewardWin: 50000, fameRewardNom: 1.5 },
    { name: "Oscars", fameMin: 60, blockbustersMin: 8, fameRewardWin: 6, moneyRewardWin: 75000, fameRewardNom: 2 }
  ];

  let eligibleAwards = awards.filter(award => fame >= award.fameMin && blockbusters >= award.blockbustersMin);
  if (eligibleAwards.length === 0) {
    if (fame >= 50) {
      await showInfoModal("😕 Your fame is high, but you need more blockbuster roles to be invited to award shows.");
      fame = Math.max(fame - 0.5, 1);
    }
    return;
  }

  const award = eligibleAwards[Math.floor(Math.random() * eligibleAwards.length)];
  let invited = await showModal(`🎉 You've been invited to the ${award.name}! Attend?`);
  if (!invited) {
    await showInfoModal("🙅 You skipped the award show.");
    return;
  }

  let nomChance = Math.min((fame - award.fameMin) * 0.02 + blockbusters * 0.05, 0.7);
  if (Math.random() < nomChance) {
    let nominated = await showModal(`🏆 You're nominated for Best Actor at the ${award.name}! Accept nomination?`);
    if (nominated) {
      // Generate 3-5 competing nominees
      const numCompetitors = Math.floor(Math.random() * 3) + 3;
      const competitors = Array.from({ length: numCompetitors }, () => ({
        name: ["Chris Hemsworth", "Viola Davis", "Leonardo DiCaprio", "Lupita Nyong'o", "Ryan Gosling", "Ayo Edebiri", "Tom Hanks", "Angela Bassett"][Math.floor(Math.random() * 8)],
        fame: Math.floor(award.fameMin + Math.random() * (award.fameMin * 0.5))
      }));
      competitors.push({ name: document.getElementById("nameDisplay").textContent.split(" (")[0], fame: fame });

      // Calculate win probability based on relative fame and skill
      const totalFame = competitors.reduce((sum, c) => sum + c.fame, 0);
      let winChance = Math.min((fame + practiceXP * 0.5) / (totalFame + practiceXP * 0.5) * 0.6, 0.5);
      const winner = Math.random() < winChance ? competitors[competitors.length - 1] : competitors[Math.floor(Math.random() * (competitors.length - 1))];

      if (winner.name === competitors[competitors.length - 1].name) {
        let won = await showModal(`🎉 You won Best Actor at the ${award.name}! Accept? (+${award.fameRewardWin} Fame, +${currencySymbol}${award.moneyRewardWin})`);
        if (won) {
          fame += award.fameRewardWin;
          money += award.moneyRewardWin;
          await showInfoModal(`🎉 You won Best Actor at the ${award.name}! +${award.fameRewardWin} Fame, +${currencySymbol}${award.moneyRewardWin}`);
          await generateFollowerReaction(true, true);
        } else {
          fame += 0.25;
          await showInfoModal(`🙅 You declined the award. +0.25 Fame`);
        }
      } else {
        fame += award.fameRewardNom;
        await showInfoModal(`😕 You didn't win at the ${award.name}. ${winner.name} (Fame: ${winner.fame}) won Best Actor. Nomination boosts your fame! +${award.fameRewardNom} Fame`);
        await generateFollowerReaction(true);
      }
    } else {
      await showInfoModal(`🙅 You declined the nomination.`);
    }
  } else {
    await showInfoModal(`😕 You attended the ${award.name} but weren't nominated this time.`);
  }
  fame = Math.floor(fame || 1);
  updateStats();
  updateWeekChoices();
  updateLifestyleButtons();
  saveGame();
}

    function updateStats() {
  document.getElementById("money").textContent = formatMoney(money || getStartingMoney(currencySymbol));
  document.getElementById("fame").textContent = fame || 1;
  document.getElementById("followers").textContent = followers || 10;
  document.getElementById("skill").textContent = skill || "Beginner";
  document.getElementById("energy").textContent = energy || 100;
  document.getElementById("currencySymbol").textContent = currencySymbol || "$";
  document.getElementById("blockbusters").textContent = blockbusters || 0;
  document.getElementById("scripts").textContent = scripts || 0;
  document.getElementById("ageDisplay").textContent = age || 17;
  document.getElementById("weekNum").textContent = `Year ${year || 1}, Week ${week || 1}`; // Updated to display year and week

  const marriageStatus = document.getElementById("marriageStatus");
  if (marriageStatus) {
    marriageStatus.textContent = isMarried ? `💍 Married to ${spouseName}` : "💍 Single";
  }

  if (!isTikTokMonetized && followers >= 10000) {
    isTikTokMonetized = true;
    tiktokIncome = convertCurrency(Math.min(50 + Math.floor((followers - 10000) * 0.01), 500));
    tiktokMonetizationWeeks = 12;
    showInfoModal(`🎉 Your TikTok account is now monetized through the Creator Fund! You'll earn ${currencySymbol}${tiktokIncome}/week for ${tiktokMonetizationWeeks} weeks.`);
  } else if (isTikTokMonetized && tiktokMonetizationWeeks === 0 && followers >= 10000) {
    tiktokIncome = convertCurrency(Math.min(50 + Math.floor((followers - 10000) * 0.01), 500));
    tiktokMonetizationWeeks = 12;
    showInfoModal(`📱 Your TikTok Creator Fund monetization has been renewed! You'll earn ${currencySymbol}${tiktokIncome}/week for ${tiktokMonetizationWeeks} weeks.`);
  } else if (isTikTokMonetized && followers < 10000) {
    isTikTokMonetized = false;
    tiktokIncome = 0;
    tiktokMonetizationWeeks = 0;
    showInfoModal(`😕 Your TikTok account is no longer monetized due to low followers. Reach 10,000 followers to monetize again.`);
  }

  updateWeekChoices(); // Update action buttons
}

    function checkEnergy() {
  const minActionEnergy = 15;
  if (energy < minActionEnergy) {
    document.querySelectorAll(".choice-btn:not([onclick^='buyLifestyleItem'])").forEach(btn => btn.disabled = true);
  } else {
    enableButtons();
  }
  updateWeekChoices(); // Update action buttons
  updateLifestyleButtons();
}

    function disableButtons() {
      document.querySelectorAll(".choice-btn:not([onclick^='buyLifestyleItem'])").forEach(btn => btn.disabled = true);
    }

    function enableButtons() {
  document.querySelectorAll(".choice-btn:not([onclick^='buyLifestyleItem'])").forEach(btn => {
    // Only enable buttons for actions that don't have specific availability checks
    if (!["writeScriptBtn", "blockbusterBtn", "aListPartyBtn", "voiceActBtn", "endorsementBtn", "networkingBtn", "merchLineBtn"].includes(btn.id)) {
      btn.disabled = false;
    }
  });
  updateWeekChoices(); // Handle specific action buttons
}

    function resetGame() {
      localStorage.removeItem("actorSimSave");
      location.reload();
    }
    
window.onload = () => {
  if (localStorage.getItem("actorSimSave")) {
    if (loadGame()) {
      document.getElementById("game").style.display = "block";
      document.getElementById("profileForm").style.display = "none";
    } else {
      document.getElementById("profileForm").style.display = "block";
      document.getElementById("game").style.display = "none";
      money = getStartingMoney(currencySymbol);
      console.log("Starting new game due to load failure.");
    }
  } else {
    document.getElementById("profileForm").style.display = "block";
    document.getElementById("game").style.display = "none";
    money = getStartingMoney(currencySymbol);
    console.log("Starting new game.");
  }
};
    
  </script>
</body>
</html>
