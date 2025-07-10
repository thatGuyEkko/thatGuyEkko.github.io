<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <title>捡石子小游戏</title>
    <style>
        body { font-family: "微软雅黑", Arial, sans-serif; background: #f5f5f5; }
        .container { max-width: 440px; margin: 40px auto; background: #fff; border-radius: 8px; box-shadow: 0 2px 8px #ccc; padding: 24px; }
        h2 { text-align: center; }
        .info, .winner { text-align: center; margin: 16px 0; }
        .actions { display: flex; justify-content: center; gap: 16px; margin: 16px 0; }
        button { padding: 8px 20px; font-size: 16px; border-radius: 4px; border: 1px solid #888; background: #eee; cursor: pointer; }
        button:disabled { background: #ccc; cursor: not-allowed; }
        .input-row { display: flex; justify-content: center; gap: 8px; margin-bottom: 16px; }
        input[type="number"], input[type="text"] { width: 60px; padding: 4px; }
        .stones-area { display: flex; flex-wrap: wrap; justify-content: center; min-height: 48px; margin: 12px 0 8px 0; }
        .stone { font-size: 28px; margin: 2px; transition: transform 0.3s; }
        .stone.taken { transform: scale(0); opacity: 0.2; }
        .log-area { background: #f9f9f9; border: 1px solid #eee; border-radius: 6px; padding: 8px; height: 90px; overflow-y: auto; font-size: 14px; margin-top: 10px;}
        .log-area strong { color: #2b7; }
        .log-area .ai { color: #09c; }
        .log-area .player { color: #e67e22; }
    </style>
</head>
<body>
<div class="container">
    <h2>捡石子小游戏</h2>
    <div id="setup">
        <div class="input-row">
            <label>对战模式:
                <select id="modeSelect" onchange="onModeChange()">
                    <option value="ai">玩家 vs AI</option>
                    <option value="pvp">玩家 vs 玩家</option>
                </select>
            </label>
        </div>
        <div class="input-row">
            <label>玩家1: <input type="text" id="player1" value="你"></label>
            <label id="player2Label" style="display:none;">玩家2: <input type="text" id="player2" value="对手"></label>
        </div>
        <div class="input-row">
            <label>石子总数: <input type="number" id="totalStones" min="1" value="10"></label>
        </div>
        <button onclick="startGame()">开始游戏</button>
    </div>
    <div id="game" style="display:none;">
        <div class="info" id="status"></div>
        <div class="stones-area" id="stonesArea"></div>
        <div class="info">剩余石子数：<span id="stones"></span></div>
        <div class="actions">
            <button id="pick1" onclick="pickStones(1)">捡1颗</button>
            <button id="pick2" onclick="pickStones(2)">捡2颗</button>
        </div>
        <div class="winner" id="winner" style="color:green;"></div>
        <div class="log-area" id="logArea"></div>
        <button onclick="resetGame()">重新开始</button>
    </div>
</div>
<script>
    let players = [];
    let total = 0;
    let turn = 0; // 0: 玩家1, 1: 玩家2/AI
    let gameOver = false;
    let log = [];
    let stonesArr = [];
    let mode = "ai"; // "ai" or "pvp"
    const AI_NAME = "捡石子大王-邹是好看";

    function onModeChange() {
        mode = document.getElementById('modeSelect').value;
        document.getElementById('player2Label').style.display = (mode === 'pvp') ? '' : 'none';
        document.getElementById('player2').value = (mode === 'pvp') ? '对手' : AI_NAME;
    }

    function startGame() {
        mode = document.getElementById('modeSelect').value;
        const p1 = document.getElementById('player1').value.trim() || '你';
        const p2 = document.getElementById('player2').value.trim() || (mode === 'ai' ? AI_NAME : '对手');
        total = parseInt(document.getElementById('totalStones').value, 10);
        if (isNaN(total) || total < 1) {
            alert('请输入大于0的石子数');
            return;
        }
        players = [p1, p2];
        turn = 0;
        gameOver = false;
        log = [];
        stonesArr = Array(total).fill(0);
        document.getElementById('setup').style.display = 'none';
        document.getElementById('game').style.display = '';
        document.getElementById('winner').textContent = '';
        updateStonesArea();
        updateStatus();
        updateLog();
        if (mode === 'ai' && turn === 1) aiMove();
    }

    function updateStonesArea(takeIdxs=[]) {
        const area = document.getElementById('stonesArea');
        area.innerHTML = '';
        for (let i = 0; i < stonesArr.length; i++) {
            let cls = "stone";
            if (stonesArr[i] === 1) cls += " taken";
            area.innerHTML += `<span class="${cls}" id="stone${i}">🪨</span>`;
        }
        // 动画效果
        takeIdxs.forEach(idx => {
            setTimeout(() => {
                const el = document.getElementById('stone'+idx);
                if (el) el.classList.add('taken');
            }, 80);
        });
        document.getElementById('stones').textContent = stonesArr.filter(x=>x===0).length;
    }

    function updateStatus() {
        document.getElementById('status').textContent = `轮到 ${players[turn]} 捡石子`;
        document.getElementById('pick1').disabled = gameOver || stonesArr.filter(x=>x===0).length < 1 || (mode === 'ai' && turn === 1);
        document.getElementById('pick2').disabled = gameOver || stonesArr.filter(x=>x===0).length < 2 || (mode === 'ai' && turn === 1);
    }

    function updateLog() {
        const logArea = document.getElementById('logArea');
        logArea.innerHTML = log.map(item => {
            let cls = (mode === 'ai' && item.player === 1) ? 'ai' : 'player';
            return `<div class="${cls}"><strong>${item.name}</strong> 捡了 <b>${item.count}</b> 颗石子，剩余 <b>${item.left}</b> 颗</div>`;
        }).join('');
        logArea.scrollTop = logArea.scrollHeight;
    }

    function pickStones(n) {
        if (gameOver || n < 1 || n > 2 || n > stonesArr.filter(x=>x===0).length) return;
        if (mode === 'ai' && turn !== 0) return;
        let taken = [];
        for (let i = 0, cnt = 0; i < stonesArr.length && cnt < n; i++) {
            if (stonesArr[i] === 0) {
                stonesArr[i] = 1;
                taken.push(i);
                cnt++;
            }
        }
        updateStonesArea(taken);
        setTimeout(() => {
            afterPick(n, taken);
        }, 350);
    }

    function afterPick(n, taken) {
        const left = stonesArr.filter(x=>x===0).length;
        log.push({player: turn, name: players[turn], count: n, left: left});
        updateLog();
        if (left === 0) {
            document.getElementById('winner').textContent = `🎉 恭喜，${players[turn]} 获胜！`;
            gameOver = true;
            updateStatus();
        } else {
            turn = 1 - turn;
            updateStatus();
            if (mode === 'ai' && turn === 1) setTimeout(aiMove, 800);
        }
    }

    function aiMove() {
        if (gameOver || turn !== 1) return;
        let left = stonesArr.filter(x=>x===0).length;
        let aiPick;
        // AI必胜策略
        if (left % 3 === 1) {
            aiPick = left >= 2 ? (Math.random() < 0.5 ? 1 : 2) : 1;
        } else {
            aiPick = left % 3 === 0 ? 2 : left % 3;
        }
        let taken = [];
        for (let i = 0, cnt = 0; i < stonesArr.length && cnt < aiPick; i++) {
            if (stonesArr[i] === 0) {
                stonesArr[i] = 1;
                taken.push(i);
                cnt++;
            }
        }
        updateStonesArea(taken);
        setTimeout(() => {
            const leftNow = stonesArr.filter(x=>x===0).length;
            log.push({player: 1, name: players[1], count: aiPick, left: leftNow});
            updateLog();
            if (leftNow === 0) {
                document.getElementById('winner').textContent = `😎 ${AI_NAME} 获胜！`;
                gameOver = true;
                updateStatus();
            } else {
                turn = 0;
                updateStatus();
            }
        }, 350);
    }

    function resetGame() {
        document.getElementById('setup').style.display = '';
        document.getElementById('game').style.display = 'none';
    }
    // 初始化时根据模式显示输入框
    onModeChange();
</script>
</body>
</html>
