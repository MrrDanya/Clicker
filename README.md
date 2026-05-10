<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no, viewport-fit=cover">
    <title>Кликер PRO | Соревнуйся с друзьями!</title>
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
        /* Модальное окно регистрации */
        .modal {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,0.95);
            backdrop-filter: blur(12px);
            display: flex;
            justify-content: center;
            align-items: center;
            z-index: 2000;
        }
        .modal-content {
            background: #0e2a32;
            border-radius: 56px;
            padding: 30px 24px;
            text-align: center;
            max-width: 320px;
            width: 90%;
            border: 2px solid #ffb347;
        }
        .modal-content h2 { color: #ffd966; margin-bottom: 20px; }
        .modal-content input {
            width: 100%;
            padding: 14px;
            border-radius: 60px;
            border: none;
            background: #1a2f38;
            color: white;
            font-size: 1.1rem;
            text-align: center;
            margin-bottom: 20px;
        }
        .modal-content button {
            background: #ffb347;
            border: none;
            padding: 12px 28px;
            border-radius: 60px;
            font-weight: bold;
            font-size: 1.1rem;
            cursor: pointer;
            width: 100%;
        }
        .error-msg { color: #ff8888; margin-top: 10px; font-size: 0.8rem; }
        .app {
            max-width: 550px;
            width: 100%;
            margin: 0 auto;
            background: rgba(8, 22, 28, 0.85);
            backdrop-filter: blur(16px);
            border-radius: 42px;
            padding: 16px 14px 20px;
            border: 1px solid rgba(255, 200, 100, 0.35);
        }
        .top-bar { display: flex; justify-content: space-between; align-items: center; gap: 10px; margin-bottom: 12px; flex-wrap: wrap; }
        .balance-header {
            background: #00000066;
            border-radius: 70px;
            padding: 8px 16px;
            display: flex;
            align-items: baseline;
            gap: 8px;
            border: 1px solid #ffcd7e;
            flex: 1;
            justify-content: center;
        }
        .player-name {
            background: #ffb34733;
            border-radius: 60px;
            padding: 8px 16px;
            color: #ffd966;
            font-weight: bold;
            border: 1px solid #ffb347;
            max-width: 140px;
            overflow: hidden;
            text-overflow: ellipsis;
            white-space: nowrap;
        }
        .balance-value { font-size: 1.8rem; font-weight: 800; background: linear-gradient(135deg, #FFE6A3, #FFB347); background-clip: text; -webkit-background-clip: text; color: transparent; }
        .tabs { display: flex; gap: 8px; margin-bottom: 20px; background: #07161fe0; border-radius: 60px; padding: 5px; }
        .tab-btn { flex: 1; text-align: center; padding: 12px 6px; font-weight: bold; font-size: 0.85rem; border-radius: 50px; background: transparent; border: none; color: #cae3ff; cursor: pointer; }
        .tab-btn.active { background: #ffb347; color: #1f2c1a; }
        .tab-content { display: none; }
        .tab-content.active-tab { display: block; }
        .clicker-area { display: flex; justify-content: center; margin: 10px 0 12px; }
        .mega-clicker {
            width: 70vw; height: 70vw; max-width: 260px; max-height: 260px; min-width: 200px; min-height: 200px;
            background: radial-gradient(circle at 35% 30%, #ffaa44, #d84300);
            border-radius: 50%; display: flex; flex-direction: column; align-items: center; justify-content: center;
            box-shadow: 0 20px 30px rgba(0,0,0,0.5), inset 0 -6px 0 rgba(0,0,0,0.2);
            transition: transform 0.03s; border: 3px solid #ffdd99; cursor: pointer;
        }
        .mega-clicker:active { transform: scale(0.96); }
        .click-icon { font-size: 3.5rem; margin-bottom: 8px; pointer-events: none; }
        .click-power-info { background: #000000aa; padding: 4px 12px; border-radius: 40px; font-size: 0.75rem; font-weight: bold; color: #ffefbf; }
        .upgrades-grid { display: flex; flex-direction: column; gap: 12px; max-height: 55vh; overflow-y: auto; }
        .upgrade-card { background: #0e2a32dd; border-radius: 28px; padding: 10px 12px; border: 1px solid #ffb65e; }
        .upgrade-title { font-size: 0.95rem; font-weight: bold; color: #ffda99; display: flex; justify-content: space-between; flex-wrap: wrap; }
        .upgrade-stats { font-size: 0.7rem; color: #c2e4ff; margin: 5px 0; display: flex; gap: 12px; flex-wrap: wrap; }
        .multibuy-panel { display: flex; flex-wrap: wrap; gap: 6px; margin: 8px 0 2px; }
        .multibtn { background: #2a4b55; border: none; padding: 6px 12px; border-radius: 40px; font-weight: bold; font-size: 0.75rem; cursor: pointer; color: #ffeaac; flex: 1; min-width: 45px; }
        .price-tag { background: #00000099; padding: 3px 10px; border-radius: 30px; font-size: 0.75rem; }
        .level-progress { background: #2a414d; border-radius: 20px; height: 6px; width: 100%; margin: 6px 0; overflow: hidden; }
        .level-fill { background: linear-gradient(90deg, #ffb347, #ffdd77); height: 100%; }
        .leaderboard { background: #0a1820cc; border-radius: 32px; padding: 16px; }
        .leaderboard h3 { color: #ffd966; text-align: center; margin: 0 0 12px 0; }
        .leader-list { max-height: 55vh; overflow-y: auto; }
        .leader-row { display: flex; justify-content: space-between; padding: 10px 12px; border-bottom: 1px solid #ffb34755; color: #e0e0e0; font-size: 0.9rem; }
        .leader-rank { font-weight: bold; color: #ffb347; width: 40px; }
        .leader-name { flex: 1; overflow: hidden; text-overflow: ellipsis; white-space: nowrap; }
        .leader-score { font-weight: bold; color: #ffd966; }
        .casino-panel { background: #0a1820cc; border-radius: 32px; padding: 16px; margin-bottom: 16px; text-align: center; }
        .game-selector { display: flex; gap: 10px; margin-bottom: 20px; }
        .game-btn { flex: 1; background: #2a4b55; border: none; padding: 12px; border-radius: 40px; color: #ffeaac; font-weight: bold; cursor: pointer; }
        .game-btn.active { background: #ffb347; color: #1f2c1a; }
        .game-content { display: none; }
        .game-content.active-game { display: block; }
        .casino-numbers { display: flex; justify-content: center; gap: 20px; margin: 15px 0; align-items: center; }
        .number-card { background: linear-gradient(145deg, #2a414d, #1a2f38); padding: 15px 25px; border-radius: 30px; min-width: 80px; text-align: center; }
        .number-value { font-size: 2rem; font-weight: bold; }
        .first-number .number-value { color: #ffd966; }
        .second-number .number-value { color: #ffaa66; }
        .prediction-buttons { display: flex; gap: 15px; justify-content: center; margin: 15px 0; }
        .prediction-btn { background: #ffb347; border: none; padding: 10px 20px; border-radius: 50px; font-weight: bold; cursor: pointer; }
        .color-buttons { display: flex; gap: 12px; justify-content: center; margin: 15px 0; flex-wrap: wrap; }
        .color-btn { border: none; padding: 12px 24px; border-radius: 50px; font-weight: bold; cursor: pointer; }
        .red-btn { background: #dc3545; color: white; }
        .black-btn { background: #2c2c2c; color: white; }
        .green-btn { background: #28a745; color: white; }
        .bet-controls { display: flex; gap: 10px; justify-content: center; margin: 15px 0; flex-wrap: wrap; }
        .bet-input { background: #1a2f38; border: 2px solid #ffb347; padding: 10px; border-radius: 50px; color: white; text-align: center; width: 120px; }
        .play-btn { background: #3a6b6b; border: none; padding: 10px 20px; border-radius: 50px; color: white; cursor: pointer; }
        .casino-status { margin-top: 15px; padding: 10px; border-radius: 40px; font-weight: bold; text-align: center; }
        .waiting { background: #3a6b6baa; color: #ffeaac; }
        .win { background: #2a6b2acc; color: #aaffaa; }
        .lose { background: #8b3a3acc; color: #ffaaaa; }
        .income-badge { background: #000000aa; border-radius: 40px; padding: 6px 12px; text-align: center; margin-bottom: 12px; font-size: 0.8rem; }
        footer { font-size: 0.55rem; text-align: center; margin-top: 14px; color: #7b9aac; }
        .floating-number { position: fixed; pointer-events: none; font-weight: bold; font-size: 1.3rem; color: gold; z-index: 1000; animation: floatUp 0.5s forwards; }
        @keyframes floatUp { 0% { opacity: 1; transform: translateY(0px); } 100% { opacity: 0; transform: translateY(-70px); } }
        @keyframes numberPop { 0% { transform: scale(0); opacity: 0; } 100% { transform: scale(1); opacity: 1; } }
        .animate-number { animation: numberPop 0.4s ease-out forwards; }
        .copy-link-btn { background: #2c464f; border: none; padding: 8px 16px; border-radius: 60px; color: #ffcf9a; font-size: 0.7rem; margin-top: 10px; cursor: pointer; }
    </style>
</head>
<body>
<div id="registerModal" class="modal">
    <div class="modal-content">
        <h2>🎮 Введите ваш ник</h2>
        <input type="text" id="nicknameInput" maxlength="20" placeholder="Игрок" autocomplete="off">
        <button id="startGameBtn">Начать игру</button>
        <div id="regError" class="error-msg"></div>
        <div style="margin-top: 15px; font-size: 12px; color: #aaa;">🏆 Соревнуйтесь с друзьями! Ваш прогресс сохранится.</div>
    </div>
</div>

<div class="app" id="gameApp" style="display: none;">
    <div class="top-bar">
        <div class="player-name" id="playerNameDisplay">Игрок</div>
        <div class="balance-header">
            <span style="font-size:1.2rem;">💎</span>
            <span class="balance-value" id="balansDisplay">0</span>
        </div>
    </div>

    <div class="tabs">
        <button class="tab-btn active" data-tab="clickTab">⚡ КЛИКЕР</button>
        <button class="tab-btn" data-tab="upgradesTab">📈 УЛУЧШЕНИЯ</button>
        <button class="tab-btn" data-tab="casinoTab">🎲 КАЗИНО</button>
        <button class="tab-btn" data-tab="leaderTab">🏆 ЛИДЕРЫ</button>
    </div>

    <div id="clickTab" class="tab-content active-tab">
        <div class="clicker-area"><div class="mega-clicker" id="clickBomb"><div class="click-icon">💎</div><div class="click-power-info" id="powerInfo">Сила: 1</div></div></div>
        <div style="text-align:center;"><span style="background:#00000077; padding:4px 16px; border-radius:60px; font-size:0.7rem;">👆 Нажми на 💎 чтобы заработать</span></div>
        <button class="copy-link-btn" id="copyLinkBtn" style="width:100%; margin-top:12px;">🔗 Скопировать ссылку для друзей</button>
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
                <div class="casino-numbers"><div class="number-card first-number"><div class="number-value" id="firstNum">?</div></div><span>⚖️</span><div class="number-card second-number" style="opacity:0.5;"><div class="number-value" id="secondNum">?</div></div></div>
                <div class="bet-controls"><input type="number" id="guessBet" class="bet-input" value="100" step="100" min="1"><button class="play-btn" id="startGuessBtn">🎮 ИГРАТЬ</button></div>
                <div class="prediction-buttons" id="guessPredictionBtns" style="display:none;"><button class="prediction-btn" id="lessBtn">📉 МЕНЬШЕ</button><button class="prediction-btn" id="moreBtn">📈 БОЛЬШЕ</button></div>
                <div id="guessStatus" class="casino-status waiting">🎲 Нажмите «ИГРАТЬ»</div>
            </div>
            <div id="colorGame" class="game-content">
                <div style="margin:10px 0;">🎲 Вращение рулетки</div>
                <div style="margin:10px 0; font-size:2rem;" id="rouletteResult">❓</div>
                <div class="color-buttons"><button class="color-btn red-btn" id="redBtn">🔴 КРАСНОЕ (x2)</button><button class="color-btn black-btn" id="blackBtn">⚫ ЧЁРНОЕ (x2)</button><button class="color-btn green-btn" id="greenBtn">🟢 ЗЕЛЁНОЕ (x14)</button></div>
                <div class="bet-controls"><input type="number" id="colorBet" class="bet-input" value="100" step="100" min="1"></div>
                <div id="colorStatus" class="casino-status waiting">🎨 Выберите цвет</div>
            </div>
        </div>
    </div>

    <div id="leaderTab" class="tab-content">
        <div class="leaderboard">
            <h3>🏆 ТАБЛИЦА ЛИДЕРОВ 🏆</h3>
            <div class="leader-list" id="leaderList"></div>
            <div style="font-size:0.7rem; text-align:center; margin-top:12px; color:#aaa;">Соревнуйтесь с друзьями! Кто больше накликает?</div>
        </div>
    </div>
    <footer>⭐ Ваш прогресс сохраняется в браузере. Пришлите ссылку друзьям — соревнуйтесь в таблице лидеров!</footer>
</div>

<script>
    const SAVE_KEY = "clicker_final_save";
    const LEADER_KEY = "clicker_leaderboard";
    
    let currentPlayer = null;
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
    
    function loadLeaderboard() { const raw = localStorage.getItem(LEADER_KEY); return raw ? JSON.parse(raw) : []; }
    function saveLeaderboard(leaders) { localStorage.setItem(LEADER_KEY, JSON.stringify(leaders)); }
    function updateLeaderboard(playerName, score) {
        let leaders = loadLeaderboard();
        const existing = leaders.find(l => l.name === playerName);
        if (existing) existing.score = Math.max(existing.score, score);
        else leaders.push({ name: playerName, score: score });
        leaders.sort((a,b) => b.score - a.score);
        leaders = leaders.slice(0, 50);
        saveLeaderboard(leaders);
        renderLeaderboard();
    }
    function renderLeaderboard() {
        const container = document.getElementById("leaderList");
        if (!container) return;
        const leaders = loadLeaderboard();
        container.innerHTML = "";
        if (leaders.length === 0) { container.innerHTML = "<div style='text-align:center; padding:20px; color:#aaa'>Нет игроков</div>"; return; }
        leaders.forEach((l, idx) => { const row = document.createElement("div"); row.className = "leader-row"; row.innerHTML = `<div class="leader-rank">${idx+1}</div><div class="leader-name">${escapeHtml(l.name)}</div><div class="leader-score">${Math.floor(l.score)}</div>`; container.appendChild(row); });
    }
    function escapeHtml(str) { return str.replace(/[&<>]/g, function(m){ if(m==='&') return '&amp;'; if(m==='<') return '&lt;'; if(m==='>') return '&gt;'; return m;}); }
    
    function saveGame() {
        if (!currentPlayer) return;
        const save = { coins: balansCoins, clickLvls: clickUpgrades.map(u => u.level), incomeLvls: incomeUpgrades.map(u => u.level) };
        localStorage.setItem(`${SAVE_KEY}_${currentPlayer}`, JSON.stringify(save));
        updateLeaderboard(currentPlayer, balansCoins);
    }
    function loadGameForPlayer() {
        if (!currentPlayer) return;
        const raw = localStorage.getItem(`${SAVE_KEY}_${currentPlayer}`);
        if (!raw) { balansCoins = 0; clickUpgrades.forEach(u => u.level = 0); incomeUpgrades.forEach(u => u.level = 0); return; }
        try { const data = JSON.parse(raw); if (typeof data.coins === "number") balansCoins = data.coins; if (data.clickLvls) data.clickLvls.forEach((v,i)=>clickUpgrades[i].level=v); if (data.incomeLvls) data.incomeLvls.forEach((v,i)=>incomeUpgrades[i].level=v); } catch(e) {}
    }
    
    function getClickPower() { let b=0; clickUpgrades.forEach(u=>b+=u.level*u.bonus); return 1+b; }
    function getTotalIncome() { let t=0; incomeUpgrades.forEach(u=>t+=u.level*u.income); return t; }
    function getClickPrice(up) { if(up.level>=up.maxLvl) return Infinity; let p=Math.floor(up.basePrice+up.level*up.basePrice*0.6); if(up.id==="c1") return Math.min(p,38000); if(up.id==="c2") return Math.min(p,120000); if(up.id==="c3") return Math.min(p,280000); return Math.min(p,2500000); }
    function getIncomePrice(up) { if(up.level>=up.maxLvl) return Infinity; let mult=1+(up.level/25); let p=Math.floor(up.basePrice*Math.pow(mult,1.4)); if(up.id==="i1"||up.id==="i2"||up.id==="i3") return Math.min(p,950000); return Math.min(p,5000000); }
    
    function buyUpgrade(up, isIncome, amount) {
        if(amount<=0) return false;
        let canBuy=0,totalCost=0,tempLvl=up.level;
        for(let i=0;i<amount;i++){ if(tempLvl>=up.maxLvl) break; let p=isIncome?getIncomePrice({...up,level:tempLvl}):getClickPrice({...up,level:tempLvl}); if(p===Infinity) break; totalCost+=p; tempLvl++; canBuy++; }
        if(canBuy===0){ showMessage(`🏁 ${up.name} максимум!`,"#ffaa77"); return false; }
        if(balansCoins>=totalCost){ balansCoins-=totalCost; up.level+=canBuy; showMessage(`🚀 +${canBuy} ур.`,"#aaffcc"); updateUI(); saveGame(); return true; }
        else{ showMessage(`💔 Нужно еще ${totalCost-balansCoins}`,"#ff8888"); return false; }
    }
    
    function renderUpgrades() {
        const container = document.getElementById("allUpgradesContainer");
        if(!container) return;
        container.innerHTML = "";
        const h1=document.createElement("div"); h1.style.cssText="font-size:1rem;font-weight:bold;color:#ffcf8a"; h1.innerText="💢 УСИЛЕНИЕ КЛИКА"; container.appendChild(h1);
        for(let up of clickUpgrades){
            const price=getClickPrice(up); const maxed=up.level>=up.maxLvl; const maxShow=up.maxLvl===Infinity?"∞":up.maxLvl; const percent=up.maxLvl===Infinity?0:(up.level/up.maxLvl)*100;
            const card=document.createElement("div"); card.className="upgrade-card";
            card.innerHTML=`<div class="upgrade-title"><span>${up.name} [${up.level}/${maxShow}]</span><span class="price-tag">💰 ${maxed?"MAX":Math.floor(price)}</span></div><div class="upgrade-stats"><span>⚡ +${up.bonus}/ур</span><span>📈 +${up.level*up.bonus}</span></div>${up.maxLvl!==Infinity?`<div class="level-progress"><div class="level-fill" style="width:${percent}%"></div></div>`:'<div style="font-size:0.7rem;">✨ Безлимит</div>'}<div class="multibuy-panel" data-id="${up.id}" data-type="click"></div>`;
            container.appendChild(card);
        }
        const h2=document.createElement("div"); h2.style.cssText="font-size:1rem;font-weight:bold;margin-top:14px;color:#ffcf8a"; h2.innerText="💸 ДЕНЬГИ В СЕКУНДУ"; container.appendChild(h2);
        for(let up of incomeUpgrades){
            const price=getIncomePrice(up); const maxed=up.level>=up.maxLvl; const maxShow=up.maxLvl===Infinity?"∞":up.maxLvl; const percent=up.maxLvl===Infinity?0:(up.level/up.maxLvl)*100;
            const card=document.createElement("div"); card.className="upgrade-card";
            card.innerHTML=`<div class="upgrade-title"><span>${up.name} [${up.level}/${maxShow}]</span><span class="price-tag">💰 ${maxed?"MAX":Math.floor(price)}</span></div><div class="upgrade-stats"><span>💸 +${up.income}/сек</span><span>📊 +${up.level*up.income}/сек</span></div>${up.maxLvl!==Infinity?`<div class="level-progress"><div class="level-fill" style="width:${percent}%"></div></div>`:'<div style="font-size:0.7rem;">✨ Безлимитный доход</div>'}<div class="multibuy-panel" data-id="${up.id}" data-type="income"></div>`;
            container.appendChild(card);
        }
        document.querySelectorAll('.multibuy-panel').forEach(panel=>{
            const id=panel.getAttribute('data-id'); const type=panel.getAttribute('data-type');
            const btns=['x1','x2','x5','x10','x50','x100','MAX']; panel.innerHTML='';
            btns.forEach(btnText=>{ const btn=document.createElement('button'); btn.className='multibtn'; btn.innerText=btnText;
            btn.onclick=(e)=>{ e.stopPropagation(); let amount=1;
                if(btnText==='x2') amount=2; else if(btnText==='x5') amount=5; else if(btnText==='x10') amount=10; else if(btnText==='x50') amount=50; else if(btnText==='x100') amount=100;
                else if(btnText==='MAX'){ let upgrade=type==='click'?clickUpgrades.find(u=>u.id===id):incomeUpgrades.find(u=>u.id===id); if(!upgrade) return; let steps=0,tmpLvl=upgrade.level,costSum=0; for(let i=0;i<500;i++){ if(tmpLvl>=upgrade.maxLvl) break; let p=type==='click'?getClickPrice({...upgrade,level:tmpLvl}):getIncomePrice({...upgrade,level:tmpLvl}); if(balansCoins>=costSum+p){ costSum+=p; tmpLvl++; steps++; }else break; } amount=steps; if(amount===0){ showMessage("Не хватает на MAX","#ffaa88"); return; } }
                let upgrade=type==='click'?clickUpgrades.find(u=>u.id===id):incomeUpgrades.find(u=>u.id===id); if(upgrade) buyUpgrade(upgrade, type==='income', amount);
            }; panel.appendChild(btn); });
        });
    }
    
    function updateUI() { document.getElementById("balansDisplay").innerText = Math.floor(balansCoins); document.getElementById("powerInfo").innerHTML = `Сила: ${getClickPower()}`; document.getElementById("totalIncomeDisplay").innerHTML = `💸 Пассивный доход: ${getTotalIncome()}/сек`; renderUpgrades(); renderLeaderboard(); }
    function showMessage(text,color){ const msg=document.createElement("div"); msg.className="floating-number"; msg.innerText=text; msg.style.color=color; msg.style.left=window.innerWidth/2-60+"px"; msg.style.top=window.innerHeight/2-40+"px"; document.body.appendChild(msg); setTimeout(()=>msg.remove(),500); }
    
    function onTap(e){ e.preventDefault(); let gain=getClickPower(); if(Math.random()<0.1){ gain*=2; showMessage(`🔥 КРИТ! +${gain}`,"#ff6666"); }else{ showMessage(`+${gain}`,"#ffd966"); } balansCoins+=gain; updateUI(); saveGame(); if(navigator.vibrate) navigator.vibrate(10); }
    
    let guessGameActive=false, guessCurrentFirst, guessCurrentBet, waitingForPrediction=false;
    function startGuessGame(){ if(guessGameActive){ showMessage("Сначала завершите игру!","#ffaa88"); return; } let bet=parseInt(document.getElementById("guessBet").value); if(isNaN(bet)||bet<=0){ showMessage("Ставка > 0","#ff8888"); return; } if(bet>balansCoins){ showMessage("Не хватает монет!","#ff8888"); return; } guessCurrentBet=bet; guessGameActive=true; waitingForPrediction=true; guessCurrentFirst=Math.floor(Math.random()*51)+75; document.getElementById("firstNum").innerText=guessCurrentFirst; document.getElementById("secondNum").innerText="?"; document.getElementById("secondNum").parentElement.parentElement.style.opacity="0.5"; document.getElementById("guessPredictionBtns").style.display="flex"; document.getElementById("startGuessBtn").style.display="none"; document.getElementById("guessStatus").className="casino-status waiting"; document.getElementById("guessStatus").innerHTML=`🎲 Первое: ${guessCurrentFirst}. Угадай: БОЛЬШЕ или МЕНЬШЕ? Ставка: ${guessCurrentBet}`; }
    function makeGuessPrediction(prediction){ if(!guessGameActive||!waitingForPrediction) return; waitingForPrediction=false; let secondNum=Math.floor(Math.random()*200)+1; document.getElementById("secondNum").innerText=secondNum; document.getElementById("secondNum").parentElement.parentElement.style.opacity="1"; let isWin=(prediction==='less'&&secondNum<guessCurrentFirst)||(prediction==='more'&&secondNum>guessCurrentFirst); let statusDiv=document.getElementById("guessStatus"); setTimeout(()=>{ if(isWin){ balansCoins+=guessCurrentBet; statusDiv.className="casino-status win"; statusDiv.innerHTML=`🎉 ПОБЕДА! ${secondNum} ${prediction==='less'?'<':'>'} ${guessCurrentFirst}. +${guessCurrentBet}! 🎉`; showMessage(`+${guessCurrentBet}`,"#aaffaa"); }else{ balansCoins-=guessCurrentBet; statusDiv.className="casino-status lose"; statusDiv.innerHTML=`😭 ПРОИГРЫШ! ${secondNum} ${prediction==='less'?'>':'<'} ${guessCurrentFirst}. -${guessCurrentBet}. 😭`; showMessage(`-${guessCurrentBet}`,"#ff8888"); } updateUI(); saveGame(); guessGameActive=false; document.getElementById("guessPredictionBtns").style.display="none"; document.getElementById("startGuessBtn").style.display="block"; },400); }
    
    function playColorGame(color){ let bet=parseInt(document.getElementById("colorBet").value); if(isNaN(bet)||bet<=0){ showMessage("Ставка > 0","#ff8888"); return; } if(bet>balansCoins){ showMessage("Не хватает монет!","#ff8888"); return; } let result=Math.floor(Math.random()*15); let resultColor="",mult=0; if(result===0){ resultColor="green"; mult=14; }else if(result<=7){ resultColor="red"; mult=2; }else{ resultColor="black"; mult=2; } let emoji=result===0?"🟢 0":(result<=7?"🔴 "+result:"⚫ "+result); document.getElementById("rouletteResult").innerHTML=emoji; let statusDiv=document.getElementById("colorStatus"); let win=bet*mult; if(color===resultColor){ balansCoins+=win; statusDiv.className="casino-status win"; statusDiv.innerHTML=`🎉 ПОБЕДА! ${emoji}. Выигрыш ${win} (x${mult})! 🎉`; showMessage(`+${win}`,"#aaffaa"); }else{ balansCoins-=bet; statusDiv.className="casino-status lose"; statusDiv.innerHTML=`😭 ПРОИГРЫШ! ${emoji}. Потеряно ${bet}. 😭`; showMessage(`-${bet}`,"#ff8888"); } updateUI(); saveGame(); }
    
    let passiveInterval=null;
    function startPassive(){ if(passiveInterval) clearInterval(passiveInterval); passiveInterval=setInterval(()=>{ let inc=getTotalIncome(); if(inc>0){ balansCoins+=inc; updateUI(); saveGame(); } },1000); }
    
    function initTabs(){ document.querySelectorAll(".tab-btn").forEach(btn=>{ btn.addEventListener("click",()=>{ let tabId=btn.getAttribute("data-tab"); document.querySelectorAll(".tab-btn").forEach(b=>b.classList.remove("active")); document.querySelectorAll(".tab-content").forEach(c=>c.classList.remove("active-tab")); btn.classList.add("active"); document.getElementById(tabId).classList.add("active-tab"); if(tabId==="upgradesTab") renderUpgrades(); if(tabId==="leaderTab") renderLeaderboard(); }); }); }
    
    function switchGame(gameId){ document.querySelectorAll(".game-content").forEach(el=>el.classList.remove("active-game")); document.getElementById(gameId+"Game").classList.add("active-game"); document.querySelectorAll(".game-btn").forEach(btn=>btn.classList.remove("active")); document.querySelector(`.game-btn[data-game="${gameId}"]`).classList.add("active"); }
    
    document.getElementById("startGameBtn")?.addEventListener("click",()=>{ let nick=document.getElementById("nicknameInput").value.trim(); if(nick===""){ document.getElementById("regError").innerText="Введите ник!"; return; } if(nick.length>20){ document.getElementById("regError").innerText="Ник не длиннее 20 символов"; return; } currentPlayer=nick; document.getElementById("playerNameDisplay").innerText=nick; loadGameForPlayer(); updateUI(); updateLeaderboard(currentPlayer, balansCoins); document.getElementById("registerModal").style.display="none"; document.getElementById("gameApp").style.display="block"; let clicker=document.getElementById("clickBomb"); if(clicker){ let newClicker=clicker.cloneNode(true); clicker.parentNode.replaceChild(newClicker,clicker); newClicker.addEventListener("touchstart",onTap,{passive:false}); newClicker.addEventListener("mousedown",onTap); } initTabs(); startPassive(); document.querySelectorAll(".game-btn").forEach(btn=>btn.addEventListener("click",()=>switchGame(btn.getAttribute("data-game")))); document.getElementById("startGuessBtn")?.addEventListener("click",startGuessGame); document.getElementById("lessBtn")?.addEventListener("click",()=>makeGuessPrediction('less')); document.getElementById("moreBtn")?.addEventListener("click",()=>makeGuessPrediction('more')); document.getElementById("redBtn")?.addEventListener("click",()=>playColorGame("red")); document.getElementById("blackBtn")?.addEventListener("click",()=>playColorGame("black")); document.getElementById("greenBtn")?.addEventListener("click",()=>playColorGame("green")); });
    document.getElementById("nicknameInput")?.addEventListener("keypress",(e)=>{ if(e.key==="Enter") document.getElementById("startGameBtn").click(); });
    document.getElementById("copyLinkBtn")?.addEventListener("click",()=>{ let url=window.location.href; navigator.clipboard.writeText(url); showMessage("🔗 Ссылка скопирована! Отправь друзьям!","#aaffaa"); });
</script>
</body>
</html>
