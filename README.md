<meta name='viewport' content='width=device-width, initial-scale=1'
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no, viewport-fit=cover">
    <title>Кликер PRO</title>
    <style>
        * {
            user-select: none;
            -webkit-tap-highlight-color: transparent;
            box-sizing: border-box;
        }

        body {
            margin: 0;
            min-height: 100vh;
            background: radial-gradient(circle at 10% 20%, #0a1f1a, #030c12);
            font-family: -apple-system, 'Segoe UI', 'Roboto', sans-serif;
            padding: 12px;
        }

        .app {
            max-width: 550px;
            width: 100%;
            margin: 0 auto;
            background: rgba(8, 22, 28, 0.85);
            backdrop-filter: blur(16px);
            border-radius: 42px;
            padding: 16px 14px 20px;
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.5);
            border: 1px solid rgba(255, 200, 100, 0.35);
        }

        .balance-header {
            background: #00000066;
            border-radius: 70px;
            padding: 10px 20px;
            margin-bottom: 18px;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 12px;
            border: 1px solid #ffcd7e;
        }

        .balance-icon {
            font-size: 1.8rem;
        }

        .balance-value {
            font-size: 2.5rem;
            font-weight: 800;
            background: linear-gradient(135deg, #FFE6A3, #FFB347);
            background-clip: text;
            -webkit-background-clip: text;
            color: transparent;
            line-height: 1;
        }

        .tabs {
            display: flex;
            gap: 8px;
            margin-bottom: 20px;
            background: #07161fe0;
            border-radius: 60px;
            padding: 5px;
        }

        .tab-btn {
            flex: 1;
            text-align: center;
            padding: 12px 6px;
            font-weight: bold;
            font-size: 0.85rem;
            border-radius: 50px;
            background: transparent;
            border: none;
            color: #cae3ff;
            cursor: pointer;
            font-family: inherit;
            transition: 0.1s;
        }

        .tab-btn.active {
            background: #ffb347;
            color: #1f2c1a;
            box-shadow: 0 2px 8px black;
        }

        .tab-content {
            display: none;
        }

        .tab-content.active-tab {
            display: block;
        }

        .clicker-area {
            display: flex;
            justify-content: center;
            margin: 10px 0 12px;
        }

        .mega-clicker {
            width: 70vw;
            height: 70vw;
            max-width: 260px;
            max-height: 260px;
            min-width: 200px;
            min-height: 200px;
            background: radial-gradient(circle at 35% 30%, #ffaa44, #d84300);
            border-radius: 50%;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            box-shadow: 0 20px 30px rgba(0,0,0,0.5), inset 0 -6px 0 rgba(0,0,0,0.2);
            transition: transform 0.03s;
            border: 3px solid #ffdd99;
            cursor: pointer;
        }

        .mega-clicker:active {
            transform: scale(0.96);
        }

        .click-icon {
            font-size: 4rem;
            margin-bottom: 8px;
            pointer-events: none;
        }

        .click-power-info {
            background: #000000aa;
            padding: 4px 12px;
            border-radius: 40px;
            font-size: 0.8rem;
            font-weight: bold;
            color: #ffefbf;
            text-align: center;
            pointer-events: none;
        }

        .upgrades-grid {
            display: flex;
            flex-direction: column;
            gap: 12px;
            max-height: 55vh;
            overflow-y: auto;
            padding-right: 4px;
        }

        .upgrade-card {
            background: #0e2a32dd;
            border-radius: 28px;
            padding: 10px 12px;
            border: 1px solid #ffb65e;
        }

        .upgrade-title {
            font-size: 0.95rem;
            font-weight: bold;
            color: #ffda99;
            display: flex;
            justify-content: space-between;
            flex-wrap: wrap;
            gap: 6px;
        }

        .upgrade-stats {
            font-size: 0.7rem;
            color: #c2e4ff;
            display: flex;
            gap: 10px;
            flex-wrap: wrap;
            margin: 5px 0;
        }

        .multibuy-panel {
            display: flex;
            flex-wrap: wrap;
            gap: 6px;
            margin: 8px 0 2px;
        }

        .multibtn {
            background: #2a4b55;
            border: none;
            padding: 6px 12px;
            border-radius: 40px;
            font-weight: bold;
            font-size: 0.75rem;
            cursor: pointer;
            color: #ffeaac;
            flex: 1;
            min-width: 45px;
        }

        .multibtn:active {
            transform: scale(0.96);
            background: #ffae42;
        }

        .price-tag {
            background: #00000099;
            padding: 3px 10px;
            border-radius: 30px;
            font-size: 0.75rem;
        }

        .level-progress {
            background: #2a414d;
            border-radius: 20px;
            height: 6px;
            width: 100%;
            margin: 6px 0;
            overflow: hidden;
        }
        .level-fill {
            background: linear-gradient(90deg, #ffb347, #ffdd77);
            height: 100%;
        }

        .casino-panel {
            background: #0a1820cc;
            border-radius: 32px;
            padding: 16px;
            margin-bottom: 16px;
        }
        .game-selector {
            display: flex;
            gap: 10px;
            margin-bottom: 20px;
        }
        .game-btn {
            flex: 1;
            background: #2a4b55;
            border: none;
            padding: 12px;
            border-radius: 40px;
            color: #ffeaac;
            font-weight: bold;
            cursor: pointer;
            font-size: 0.9rem;
        }
        .game-btn.active {
            background: #ffb347;
            color: #1f2c1a;
        }
        .game-content {
            display: none;
        }
        .game-content.active-game {
            display: block;
        }
        
        .casino-numbers {
            display: flex;
            justify-content: center;
            gap: 20px;
            margin: 15px 0;
            align-items: center;
        }
        .number-card {
            background: linear-gradient(145deg, #2a414d, #1a2f38);
            padding: 15px 25px;
            border-radius: 30px;
            min-width: 80px;
            text-align: center;
        }
        .number-value {
            font-size: 2rem;
            font-weight: bold;
        }
        .first-number .number-value { color: #ffd966; }
        .second-number .number-value { color: #ffaa66; }
        .prediction-buttons {
            display: flex;
            gap: 15px;
            justify-content: center;
            margin: 15px 0;
        }
        .prediction-btn {
            background: #ffb347;
            border: none;
            padding: 10px 20px;
            border-radius: 50px;
            font-weight: bold;
            font-size: 1rem;
            cursor: pointer;
        }
        
        .color-buttons {
            display: flex;
            gap: 12px;
            justify-content: center;
            margin: 15px 0;
            flex-wrap: wrap;
        }
        .color-btn {
            border: none;
            padding: 12px 24px;
            border-radius: 50px;
            font-weight: bold;
            font-size: 1rem;
            cursor: pointer;
            transition: transform 0.05s;
        }
        .color-btn:active { transform: scale(0.96); }
        .red-btn { background: #dc3545; color: white; box-shadow: 0 0 10px rgba(220,53,69,0.5); }
        .black-btn { background: #2c2c2c; color: white; box-shadow: 0 0 10px rgba(0,0,0,0.5); }
        .green-btn { background: #28a745; color: white; box-shadow: 0 0 10px rgba(40,167,69,0.5); }
        
        .bet-controls {
            display: flex;
            gap: 10px;
            justify-content: center;
            align-items: center;
            margin: 15px 0;
            flex-wrap: wrap;
        }
        .bet-input {
            background: #1a2f38;
            border: 2px solid #ffb347;
            padding: 10px;
            border-radius: 50px;
            font-size: 1rem;
            color: white;
            text-align: center;
            width: 120px;
            font-weight: bold;
        }
        .play-btn {
            background: #3a6b6b;
            border: none;
            padding: 10px 20px;
            border-radius: 50px;
            color: white;
            font-weight: bold;
            cursor: pointer;
        }
        .casino-status {
            margin-top: 15px;
            padding: 10px;
            border-radius: 40px;
            font-weight: bold;
            text-align: center;
        }
        .waiting { background: #3a6b6baa; color: #ffeaac; }
        .win { background: #2a6b2acc; color: #aaffaa; }
        .lose { background: #8b3a3acc; color: #ffaaaa; }
        
        .income-badge {
            background: #000000aa;
            border-radius: 40px;
            padding: 6px 12px;
            text-align: center;
            margin-bottom: 12px;
            font-size: 0.8rem;
        }
        footer {
            font-size: 0.55rem;
            text-align: center;
            margin-top: 14px;
            color: #7b9aac;
        }
        .floating-number {
            position: fixed;
            pointer-events: none;
            font-weight: bold;
            font-size: 1.3rem;
            color: gold;
            z-index: 1000;
            animation: floatUp 0.5s forwards;
        }
        @keyframes floatUp {
            0% { opacity: 1; transform: translateY(0px); }
            100% { opacity: 0; transform: translateY(-70px); }
        }
        @keyframes numberPop {
            0% { transform: scale(0); opacity: 0; }
            100% { transform: scale(1); opacity: 1; }
        }
        .animate-number { animation: numberPop 0.4s ease-out forwards; }
    </style>
</head>
<body>
<div class="app">
    <div class="balance-header">
        <span class="balance-icon">💎</span>
        <span class="balance-value" id="balansDisplay">0</span>
    </div>

    <div class="tabs">
        <button class="tab-btn active" data-tab="clickTab">⚡ КЛИКЕР</button>
        <button class="tab-btn" data-tab="upgradesTab">📈 УЛУЧШЕНИЯ</button>
        <button class="tab-btn" data-tab="casinoTab">🎲 КАЗИНО</button>
    </div>

    <div id="clickTab" class="tab-content active-tab">
        <div class="clicker-area">
            <div class="mega-clicker" id="clickBomb">
                <div class="click-icon">💎</div>
                <div class="click-power-info" id="powerInfo">Сила: 1</div>
            </div>
        </div>
        <div style="text-align:center;"><span style="background:#00000077; padding:4px 16px; border-radius:60px; font-size:0.7rem;">👆 Нажми на 💎</span></div>
    </div>

    <div id="upgradesTab" class="tab-content">
        <div class="income-badge" id="totalIncomeDisplay">💸 Пассивный доход: 0/сек</div>
        <div class="upgrades-grid" id="allUpgradesContainer"></div>
    </div>

    <div id="casinoTab" class="tab-content">
        <div class="casino-panel">
            <div class="game-selector">
                <button class="game-btn active" data-game="guess">🎲 УГАДАЙ ЧИСЛО</button>
                <button class="game-btn" data-game="color">🎨 КРАСНОЕ/ЧЁРНОЕ</button>
            </div>
            
            <div id="guessGame" class="game-content active-game">
                <div class="casino-numbers">
                    <div class="number-card first-number"><div class="number-value" id="firstNum">?</div></div>
                    <span style="font-size:1.5rem;">⚖️</span>
                    <div class="number-card second-number" style="opacity:0.5;"><div class="number-value" id="secondNum">?</div></div>
                </div>
                <div class="bet-controls">
                    <input type="number" id="guessBet" class="bet-input" placeholder="ставка" value="100" step="100" min="1">
                    <button class="play-btn" id="startGuessBtn">🎮 ИГРАТЬ</button>
                </div>
                <div class="prediction-buttons" id="guessPredictionBtns" style="display: none;">
                    <button class="prediction-btn" id="lessBtn">📉 МЕНЬШЕ</button>
                    <button class="prediction-btn" id="moreBtn">📈 БОЛЬШЕ</button>
                </div>
                <div id="guessStatus" class="casino-status waiting">🎲 Нажмите «ИГРАТЬ»</div>
            </div>
            
            <div id="colorGame" class="game-content">
                <div style="text-align:center; margin:10px 0; font-size:1.2rem;">🎲 Вращение рулетки</div>
                <div style="text-align:center; margin:10px 0; font-size:2rem;" id="rouletteResult">❓</div>
                <div class="color-buttons">
                    <button class="color-btn red-btn" id="redBtn">🔴 КРАСНОЕ (x2)</button>
                    <button class="color-btn black-btn" id="blackBtn">⚫ ЧЁРНОЕ (x2)</button>
                    <button class="color-btn green-btn" id="greenBtn">🟢 ЗЕЛЁНОЕ (x14)</button>
                </div>
                <div class="bet-controls">
                    <input type="number" id="colorBet" class="bet-input" placeholder="ставка" value="100" step="100" min="1">
                </div>
                <div id="colorStatus" class="casino-status waiting">🎨 Выберите цвет</div>
            </div>
        </div>
    </div>
    <footer>⭐ Сохранение автоматическое | Красный/Чёрный x2, Зелёный x14</footer>
</div>

<script>
    // ФИКСИРОВАННОЕ ИМЯ ДЛЯ СОХРАНЕНИЙ
    const SAVE_KEY = "clicker_final_save";
    
    let balansCoins = 0;
    
    const clickUpgrades = [
        { id: "c1", name: "✊ Усиленный палец", basePrice: 12, bonus: 1, level: 0, maxLvl: 50 },
        { id: "c2", name: "⚡ Молниеносный тап", basePrice: 90, bonus: 2, level: 0, maxLvl: 30 },
        { id: "c3", name: "🌀 Гипертап", basePrice: 380, bonus: 5, level: 0, maxLvl: 15 },
        { id: "c4", name: "🏆 Длань Бога", basePrice: 1500, bonus: 12, level: 0, maxLvl: Infinity },
        { id: "c5", name: "💠 Кибер-импульс", basePrice: 5500, bonus: 28, level: 0, maxLvl: Infinity }
    ];
    
    const incomeUpgrades = [
        { id: "i1", name: "🏭 Мелкая ферма", basePrice: 55, income: 1, level: 0, maxLvl: 100 },
        { id: "i2", name: "⚙️ Авто-тапёр", basePrice: 320, income: 4, level: 0, maxLvl: 100 },
        { id: "i3", name: "🤖 Робо-ферма", basePrice: 1800, income: 12, level: 0, maxLvl: 100 },
        { id: "i4", name: "💎 Кристальный ген.", basePrice: 7800, income: 35, level: 0, maxLvl: Infinity },
        { id: "i5", name: "🌌 Нейросетевой банк", basePrice: 32000, income: 95, level: 0, maxLvl: Infinity }
    ];
    
    let guessGameActive = false;
    let guessCurrentFirst = null;
    let guessCurrentBet = 0;
    let waitingForPrediction = false;
    
    function getClickPower() {
        let bonus = 0;
        for (let u of clickUpgrades) bonus += u.level * u.bonus;
        return 1 + bonus;
    }
    
    function getTotalIncome() {
        let total = 0;
        for (let u of incomeUpgrades) total += u.level * u.income;
        return total;
    }
    
    function getClickPrice(up) {
        if (up.level >= up.maxLvl) return Infinity;
        let price = Math.floor(up.basePrice + up.level * up.basePrice * 0.6);
        if (up.id === "c1") return Math.min(price, 38000);
        if (up.id === "c2") return Math.min(price, 120000);
        if (up.id === "c3") return Math.min(price, 280000);
        return Math.min(price, 2500000);
    }
    
    function getIncomePrice(up) {
        if (up.level >= up.maxLvl) return Infinity;
        let mult = 1 + (up.level / 25);
        let price = Math.floor(up.basePrice * Math.pow(mult, 1.4));
        if (up.id === "i1" || up.id === "i2" || up.id === "i3") return Math.min(price, 950000);
        return Math.min(price, 5000000);
    }
    
    function buyUpgrade(up, isIncome, amount) {
        if (amount <= 0) return false;
        let canBuy = 0, totalCost = 0, tempLvl = up.level;
        for (let i = 0; i < amount; i++) {
            if (tempLvl >= up.maxLvl) break;
            let price = isIncome ? getIncomePrice({ ...up, level: tempLvl }) : getClickPrice({ ...up, level: tempLvl });
            if (price === Infinity) break;
            totalCost += price;
            tempLvl++;
            canBuy++;
        }
        if (canBuy === 0) { showMessage(`🏁 ${up.name} максимум!`, "#ffaa77"); return false; }
        if (balansCoins >= totalCost) {
            balansCoins -= totalCost;
            up.level += canBuy;
            showMessage(`🚀 +${canBuy} ур.`, "#aaffcc");
            updateUI();
            saveGame();
            return true;
        } else {
            showMessage(`💔 Нужно еще ${Math.floor(totalCost - balansCoins)}`, "#ff8888");
            return false;
        }
    }
    
    function renderUpgrades() {
        const container = document.getElementById("allUpgradesContainer");
        if (!container) return;
        container.innerHTML = "";
        
        const h1 = document.createElement("div"); h1.style.fontSize="1rem"; h1.style.fontWeight="bold"; h1.style.color="#ffcf8a"; h1.innerText="💢 УСИЛЕНИЕ КЛИКА"; container.appendChild(h1);
        for (let up of clickUpgrades) {
            const price = getClickPrice(up);
            const maxed = up.level >= up.maxLvl;
            const maxShow = up.maxLvl === Infinity ? "∞" : up.maxLvl;
            const percent = (up.maxLvl === Infinity) ? 0 : (up.level / up.maxLvl) * 100;
            const card = document.createElement("div"); card.className="upgrade-card";
            card.innerHTML = `<div class="upgrade-title"><span>${up.name} [${up.level}/${maxShow}]</span><span class="price-tag">💰 ${maxed?"MAX":Math.floor(price)}</span></div><div class="upgrade-stats"><span>⚡ +${up.bonus}/ур</span><span>📈 +${up.level*up.bonus}</span></div>${up.maxLvl!==Infinity?`<div class="level-progress"><div class="level-fill" style="width:${percent}%"></div></div>`:'<div style="font-size:0.7rem;">✨ Безлимит</div>'}<div class="multibuy-panel" data-id="${up.id}" data-type="click"></div>`;
            container.appendChild(card);
        }
        const h2 = document.createElement("div"); h2.style.fontSize="1rem"; h2.style.fontWeight="bold"; h2.style.marginTop="14px"; h2.style.color="#ffcf8a"; h2.innerText="💸 ДЕНЬГИ В СЕКУНДУ"; container.appendChild(h2);
        for (let up of incomeUpgrades) {
            const price = getIncomePrice(up);
            const maxed = up.level >= up.maxLvl;
            const maxShow = up.maxLvl === Infinity ? "∞" : up.maxLvl;
            const percent = (up.maxLvl === Infinity) ? 0 : (up.level / up.maxLvl) * 100;
            const card = document.createElement("div"); card.className="upgrade-card";
            card.innerHTML = `<div class="upgrade-title"><span>${up.name} [${up.level}/${maxShow}]</span><span class="price-tag">💰 ${maxed?"MAX":Math.floor(price)}</span></div><div class="upgrade-stats"><span>💸 +${up.income}/сек</span><span>📊 +${up.level*up.income}/сек</span></div>${up.maxLvl!==Infinity?`<div class="level-progress"><div class="level-fill" style="width:${percent}%"></div></div>`:'<div style="font-size:0.7rem;">✨ Безлимитный доход</div>'}<div class="multibuy-panel" data-id="${up.id}" data-type="income"></div>`;
            container.appendChild(card);
        }
        
        document.querySelectorAll('.multibuy-panel').forEach(panel => {
            const id = panel.getAttribute('data-id');
            const type = panel.getAttribute('data-type');
            const buttons = ['x1','x2','x5','x10','x50','x100','MAX'];
            panel.innerHTML = '';
            buttons.forEach(btnText => {
                const btn = document.createElement('button'); btn.className='multibtn'; btn.innerText=btnText;
                btn.onclick = (e) => {
                    e.stopPropagation();
                    let amount = 1;
                    if (btnText === 'x2') amount = 2;
                    else if (btnText === 'x5') amount = 5;
                    else if (btnText === 'x10') amount = 10;
                    else if (btnText === 'x50') amount = 50;
                    else if (btnText === 'x100') amount = 100;
                    else if (btnText === 'MAX') {
                        let upgrade = type==='click'?clickUpgrades.find(u=>u.id===id):incomeUpgrades.find(u=>u.id===id);
                        if(!upgrade) return;
                        let steps=0,tmpLvl=upgrade.level,costSum=0;
                        for(let i=0;i<500;i++){
                            if(tmpLvl>=upgrade.maxLvl) break;
                            let p = type==='click'?getClickPrice({...upgrade,level:tmpLvl}):getIncomePrice({...upgrade,level:tmpLvl});
                            if(balansCoins>=costSum+p){ costSum+=p; tmpLvl++; steps++; } else break;
                        }
                        amount = steps;
                        if(amount===0){ showMessage("Не хватает на MAX","#ffaa88"); return; }
                    }
                    let upgrade = type==='click'?clickUpgrades.find(u=>u.id===id):incomeUpgrades.find(u=>u.id===id);
                    if(upgrade) buyUpgrade(upgrade, type==='income', amount);
                };
                panel.appendChild(btn);
            });
        });
    }
    
    function updateUI() {
        document.getElementById("balansDisplay").innerText = Math.floor(balansCoins);
        document.getElementById("powerInfo").innerHTML = `Сила: ${getClickPower()}`;
        document.getElementById("totalIncomeDisplay").innerHTML = `💸 Пассивный доход: ${getTotalIncome()}/сек`;
        renderUpgrades();
    }
    
    function showMessage(text, color) {
        const msg = document.createElement("div");
        msg.className = "floating-number";
        msg.innerText = text;
        msg.style.color = color;
        msg.style.left = window.innerWidth/2 - 60 + "px";
        msg.style.top = window.innerHeight/2 - 40 + "px";
        document.body.appendChild(msg);
        setTimeout(() => msg.remove(), 500);
    }
    
    function startGuessGame() {
        if (guessGameActive) { showMessage("Сначала завершите игру!", "#ffaa88"); return; }
        const bet = parseInt(document.getElementById("guessBet").value);
        if (isNaN(bet) || bet <= 0) { showMessage("Ставка > 0", "#ff8888"); return; }
        if (bet > balansCoins) { showMessage("Не хватает монет!", "#ff8888"); return; }
        
        guessCurrentBet = bet;
        guessGameActive = true;
        waitingForPrediction = true;
        guessCurrentFirst = Math.floor(Math.random() * 51) + 75;
        
        const firstEl = document.getElementById("firstNum");
        firstEl.classList.remove("animate-number");
        void firstEl.offsetWidth;
        firstEl.classList.add("animate-number");
        firstEl.innerText = guessCurrentFirst;
        
        document.getElementById("secondNum").innerText = "?";
        document.getElementById("secondNum").parentElement.parentElement.style.opacity = "0.5";
        document.getElementById("guessPredictionBtns").style.display = "flex";
        document.getElementById("startGuessBtn").style.display = "none";
        
        const statusDiv = document.getElementById("guessStatus");
        statusDiv.className = "casino-status waiting";
        statusDiv.innerHTML = `🎲 Первое: ${guessCurrentFirst}. Угадай: БОЛЬШЕ или МЕНЬШЕ? Ставка: ${guessCurrentBet}`;
    }
    
    function makeGuessPrediction(prediction) {
        if (!guessGameActive || !waitingForPrediction) { showMessage("Игра не активна!", "#ffaa88"); return; }
        waitingForPrediction = false;
        
        const secondNum = Math.floor(Math.random() * 200) + 1;
        const secondEl = document.getElementById("secondNum");
        secondEl.classList.remove("animate-number");
        void secondEl.offsetWidth;
        secondEl.classList.add("animate-number");
        secondEl.innerText = secondNum;
        document.getElementById("secondNum").parentElement.parentElement.style.opacity = "1";
        
        const isWin = (prediction === 'less' && secondNum < guessCurrentFirst) || 
                      (prediction === 'more' && secondNum > guessCurrentFirst);
        
        const statusDiv = document.getElementById("guessStatus");
        setTimeout(() => {
            if (isWin) {
                balansCoins += guessCurrentBet;
                statusDiv.className = "casino-status win";
                statusDiv.innerHTML = `🎉 ПОБЕДА! ${secondNum} ${prediction==='less'?'<':'>'} ${guessCurrentFirst}. +${guessCurrentBet}! 🎉`;
                showMessage(`+${guessCurrentBet}`, "#aaffaa");
            } else {
                balansCoins -= guessCurrentBet;
                statusDiv.className = "casino-status lose";
                statusDiv.innerHTML = `😭 ПРОИГРЫШ! ${secondNum} ${prediction==='less'?'>':'<'} ${guessCurrentFirst}. -${guessCurrentBet}. 😭`;
                showMessage(`-${guessCurrentBet}`, "#ff8888");
            }
            updateUI();
            saveGame();
            guessGameActive = false;
            document.getElementById("guessPredictionBtns").style.display = "none";
            document.getElementById("startGuessBtn").style.display = "block";
        }, 400);
    }
    
    function playColorGame(color) {
        const bet = parseInt(document.getElementById("colorBet").value);
        if (isNaN(bet) || bet <= 0) { showMessage("Ставка > 0", "#ff8888"); return; }
        if (bet > balansCoins) { showMessage("Не хватает монет!", "#ff8888"); return; }
        
        const result = Math.floor(Math.random() * 15);
        let resultColor = "";
        let multiplier = 0;
        
        if (result === 0) {
            resultColor = "green";
            multiplier = 14;
        } else if (result >= 1 && result <= 7) {
            resultColor = "red";
            multiplier = 2;
        } else {
            resultColor = "black";
            multiplier = 2;
        }
        
        let resultEmoji = result === 0 ? "🟢 0" : (result <= 7 ? "🔴 " + result : "⚫ " + result);
        document.getElementById("rouletteResult").innerHTML = resultEmoji;
        
        const statusDiv = document.getElementById("colorStatus");
        const winAmount = bet * multiplier;
        
        if (color === resultColor) {
            balansCoins += winAmount;
            statusDiv.className = "casino-status win";
            statusDiv.innerHTML = `🎉 ПОБЕДА! ${resultEmoji}. Выигрыш ${winAmount} (x${multiplier})! 🎉`;
            showMessage(`+${winAmount}`, "#aaffaa");
        } else {
            balansCoins -= bet;
            statusDiv.className = "casino-status lose";
            statusDiv.innerHTML = `😭 ПРОИГРЫШ! ${resultEmoji}. Потеряно ${bet}. 😭`;
            showMessage(`-${bet}`, "#ff8888");
        }
        updateUI();
        saveGame();
        
        setTimeout(() => {
            document.getElementById("rouletteResult").style.animation = "none";
            void document.getElementById("rouletteResult").offsetWidth;
            document.getElementById("rouletteResult").style.animation = "numberPop 0.4s ease-out";
        }, 10);
    }
    
    function onTap(event) {
        event.preventDefault();
        let gain = getClickPower();
        if (Math.random() < 0.1) {
            gain = gain * 2;
            showMessage(`🔥 КРИТ! +${gain}`, "#ff6666");
        } else {
            showMessage(`+${gain}`, "#ffd966");
        }
        balansCoins += gain;
        updateUI();
        saveGame();
        if (navigator.vibrate) navigator.vibrate(10);
    }
    
    function saveGame() {
        const save = {
            coins: balansCoins,
            clickLvls: clickUpgrades.map(u => u.level),
            incomeLvls: incomeUpgrades.map(u => u.level)
        };
        localStorage.setItem(SAVE_KEY, JSON.stringify(save));
    }
    
    function loadGame() {
        const raw = localStorage.getItem(SAVE_KEY);
        if (!raw) return;
        try {
            const data = JSON.parse(raw);
            if (typeof data.coins === "number") balansCoins = data.coins;
            if (data.clickLvls && data.clickLvls.length === clickUpgrades.length) {
                for (let i = 0; i < clickUpgrades.length; i++) clickUpgrades[i].level = data.clickLvls[i];
            }
            if (data.incomeLvls && data.incomeLvls.length === incomeUpgrades.length) {
                for (let i = 0; i < incomeUpgrades.length; i++) incomeUpgrades[i].level = data.incomeLvls[i];
            }
        } catch(e) {}
    }
    
    let passiveInterval = null;
    function startPassive() {
        if (passiveInterval) clearInterval(passiveInterval);
        passiveInterval = setInterval(() => {
            const inc = getTotalIncome();
            if (inc > 0) {
                balansCoins += inc;
                updateUI();
                saveGame();
            }
        }, 1000);
    }
    
    function switchGame(gameId) {
        document.querySelectorAll(".game-content").forEach(el => el.classList.remove("active-game"));
        document.getElementById(gameId + "Game").classList.add("active-game");
        document.querySelectorAll(".game-btn").forEach(btn => btn.classList.remove("active"));
        document.querySelector(`.game-btn[data-game="${gameId}"]`).classList.add("active");
    }
    
    function initTabs() {
        const tabs = document.querySelectorAll(".tab-btn");
        const contents = document.querySelectorAll(".tab-content");
        tabs.forEach(btn => {
            btn.addEventListener("click", () => {
                const tabId = btn.getAttribute("data-tab");
                tabs.forEach(b => b.classList.remove("active"));
                contents.forEach(c => c.classList.remove("active-tab"));
                btn.classList.add("active");
                document.getElementById(tabId).classList.add("active-tab");
                if (tabId === "upgradesTab") renderUpgrades();
            });
        });
    }
    
    function init() {
        loadGame();
        updateUI();
        
        const clicker = document.getElementById("clickBomb");
        if (clicker) {
            const newClicker = clicker.cloneNode(true);
            clicker.parentNode.replaceChild(newClicker, clicker);
            newClicker.addEventListener("touchstart", onTap, { passive: false });
            newClicker.addEventListener("mousedown", onTap);
        }
        
        document.getElementById("startGuessBtn")?.addEventListener("click", startGuessGame);
        document.getElementById("lessBtn")?.addEventListener("click", () => makeGuessPrediction('less'));
        document.getElementById("moreBtn")?.addEventListener("click", () => makeGuessPrediction('more'));
        
        document.getElementById("redBtn")?.addEventListener("click", () => playColorGame("red"));
        document.getElementById("blackBtn")?.addEventListener("click", () => playColorGame("black"));
        document.getElementById("greenBtn")?.addEventListener("click", () => playColorGame("green"));
        
        document.querySelectorAll(".game-btn").forEach(btn => {
            btn.addEventListener("click", () => switchGame(btn.getAttribute("data-game")));
        });
        
        initTabs();
        startPassive();
    }
    
    init();
</script>
</body>
</html>
