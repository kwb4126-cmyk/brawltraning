<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>브롤스타즈 무빙 & 에임 트레이너</title>
    <style>
        * {
            box-sizing: border-box;
            user-select: none;
        }
        body {
            margin: 0;
            padding: 0;
            background-color: #1a1a1a;
            color: #ffffff;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            height: 100vh;
            overflow: hidden;
        }
        h1 {
            margin: 5px 0;
            font-size: 24px;
            color: #ffd700;
        }
        #menu, #game-container {
            display: flex;
            flex-direction: column;
            align-items: center;
        }
        .btn-group {
            display: flex;
            gap: 15px;
            margin-top: 15px;
        }
        button {
            padding: 12px 24px;
            font-size: 16px;
            font-weight: bold;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            transition: 0.2s;
        }
        .btn-dodge { background-color: #ff4757; color: white; }
        .btn-aim { background-color: #2ed573; color: white; }
        .btn-back { background-color: #747d8c; color: white; margin-top: 10px; }
        button:hover { opacity: 0.85; transform: scale(1.05); }
        
        canvas {
            background-color: #2f3542;
            border: 4px solid #57606f;
            border-radius: 12px;
            box-shadow: 0 10px 20px rgba(0,0,0,0.5);
            cursor: crosshair;
        }
        #ui-panel {
            display: flex;
            justify-content: space-between;
            width: 600px;
            margin-bottom: 8px;
            font-size: 16px;
            font-weight: bold;
        }
        .hidden {
            display: none !important;
        }
    </style>
</head>
<body>

    <!-- 메인 메뉴 -->
    <div id="menu">
        <h1>BRAWL TRAINER</h1>
        <p>원하는 훈련 모드를 선택하세요</p>
        <div class="btn-group">
            <button class="btn-dodge" onclick="startGame('dodge')">무빙 훈련 (회피)</button>
            <button class="btn-aim" onclick="startGame('aim')">에임 훈련 (사격)</button>
        </div>
    </div>

    <!-- 게임 화면 -->
    <div id="game-container" class="hidden">
        <div id="ui-panel">
            <span id="score-board">점수: 0</span>
            <span id="life-board">생명: ❤️❤️❤️</span>
        </div>
        <canvas id="canvas" width="600" height="400"></canvas>
        <button class="btn-back" onclick="returnToMenu()">메뉴로 돌아가기</button>
    </div>

    <script>
        const menu = document.getElementById('menu');
        const gameContainer = document.getElementById('game-container');
        const canvas = document.getElementById('canvas');
        const ctx = canvas.getContext('2d');
        const scoreBoard = document.getElementById('score-board');
        const lifeBoard = document.getElementById('life-board');

        let currentMode = null;
        let animationFrameId = null;
        let score = 0;
        let lives = 3;
        let gameRunning = false;

        // 플레이어 객체
        let player = {
            x: 300,
            y: 200,
            radius: 15,
            speed: 4,
            color: '#1e90ff'
        };

        // 입력 키 상태
        let keys = { w: false, a: false, s: false, d: false };

        // 오브젝트 배열 (탄환 또는 표적)
        let entities = [];
        let spawnTimer = 0;

        window.addEventListener('keydown', (e) => {
            if (['w', 'W', 'ㅈ'].includes(e.key)) keys.w = true;
            if (['a', 'W', 'ㅁ'].includes(e.key)) keys.a = true; // a키 처리
            if (e.key.toLowerCase() === 'a') keys.a = true;
            if (e.key.toLowerCase() === 's') keys.s = true;
            if (e.key.toLowerCase() === 'd') keys.d = true;
        });

        window.addEventListener('keyup', (e) => {
            if (e.key.toLowerCase() === 'w') keys.w = false;
            if (e.key.toLowerCase() === 'a') keys.a = false;
            if (e.key.toLowerCase() === 's') keys.s = false;
            if (e.key.toLowerCase() === 'd') keys.d = false;
        });

        // 마우스 클릭 (에임 모드용)
        canvas.addEventListener('click', (e) => {
            if (!gameRunning || currentMode !== 'aim') return;
            const rect = canvas.getBoundingClientRect();
            const mouseX = e.clientX - rect.left;
            const mouseY = e.clientY - rect.top;

            let hit = false;
            for (let i = entities.length - 1; i >= 0; i--) {
                let target = entities[i];
                let dist = Math.hypot(target.x - mouseX, target.y - mouseY);
                if (dist <= target.radius) {
                    entities.splice(i, 1);
                    score += 100;
                    hit = true;
                    break;
                }
            }
            if (!hit) {
                score = Math.max(0, score - 30); // 빗나감 펜널티
            }
        });

        function startGame(mode) {
            currentMode = mode;
            menu.classList.add('hidden');
            gameContainer.classList.remove('hidden');
            
            score = 0;
            lives = 3;
            player.x = canvas.width / 2;
            player.y = canvas.height / 2;
            entities = [];
            spawnTimer = 0;
            gameRunning = true;

            if (animationFrameId) cancelAnimationFrame(animationFrameId);
            gameLoop();
        }

        function returnToMenu() {
            gameRunning = false;
            cancelAnimationFrame(animationFrameId);
            gameContainer.classList.add('hidden');
            menu.classList.remove('hidden');
        }

        function gameLoop() {
            if (!gameRunning) return;

            update();
            draw();

            animationFrameId = requestAnimationFrame(gameLoop);
        }

        function update() {
            // 플레이어 이동
            if (keys.w && player.y - player.radius > 0) player.y -= player.speed;
            if (keys.s && player.y + player.radius < canvas.height) player.y += player.speed;
            if (keys.a && player.x - player.radius > 0) player.x -= player.speed;
            if (keys.d && player.x + player.radius < canvas.width) player.x += player.speed;

            spawnTimer++;

            if (currentMode === 'dodge') {
                // 무빙 훈련: 주변에서 탄환 생성
                if (spawnTimer % 35 === 0) {
                    let side = Math.floor(Math.random() * 4);
                    let x, y;
                    if (side === 0) { x = Math.random() * canvas.width; y = 0; }
                    else if (side === 1) { x = Math.random() * canvas.width; y = canvas.height; }
                    else if (side === 2) { x = 0; y = Math.random() * canvas.height; }
                    else { x = canvas.width; y = Math.random() * canvas.height; }

                    let angle = Math.atan2(player.y - y, player.x - x);
                    let speed = 2.5 + Math.random() * 1.5;

                    entities.push({
                        x: x,
                        y: y,
                        vx: Math.cos(angle) * speed,
                        vy: Math.sin(angle) * speed,
                        radius: 8
                    });
                }

                // 탄환 업데이트 및 충돌 체크
                for (let i = entities.length - 1; i >= 0; i--) {
                    let b = entities[i];
                    b.x += b.vx;
                    b.y += b.vy;

                    // 플레이어와 충돌
                    let dist = Math.hypot(player.x - b.x, player.y - b.y);
                    if (dist < player.radius + b.radius) {
                        entities.splice(i, 1);
                        lives--;
                        if (lives <= 0) {
                            alert(`게임 오버! 최종 점수: ${score}`);
                            returnToMenu();
                        }
                    } 
                    // 화면 밖으로 나가면 제거
                    else if (b.x < 0 || b.x > canvas.width || b.y < 0 || b.y > canvas.height) {
                        entities.splice(i, 1);
                        score += 10;
                    }
                }

            } else if (currentMode === 'aim') {
                // 에임 훈련: 랜덤 위치에 표적 생성
                if (spawnTimer % 60 === 0 && entities.length < 5) {
                    entities.push({
                        x: Math.random() * (canvas.width - 60) + 30,
                        y: Math.random() * (canvas.height - 60) + 30,
                        radius: 20,
                        lifeTime: 0
                    });
                }

                // 표적 수명 체크 (시간 지나면 사라짐)
                for (let i = entities.length - 1; i >= 0; i--) {
                    entities[i].lifeTime++;
                    if (entities[i].lifeTime > 90) { // 약 1.5초 유지
                        entities.splice(i, 1);
                        lives--;
                        if (lives <= 0) {
                            alert(`게임 오버! 최종 점수: ${score}`);
                            returnToMenu();
                        }
                    }
                }
            }

            // UI 업데이트
            scoreBoard.innerText = `점수: ${score}`;
            let hearts = '';
            for (let i = 0; i < lives; i++) hearts += '❤️';
            lifeBoard.innerText = `생명: ${hearts}`;
        }

        function draw() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);

            // 플레이어 그리기 (에임 모드에서는 미표시 또는 은은하게)
            ctx.beginPath();
            ctx.arc(player.x, player.y, player.radius, 0, Math.PI * 2);
            ctx.fillStyle = player.color;
            ctx.fill();
            ctx.lineWidth = 2;
            ctx.strokeStyle = '#ffffff';
            ctx.stroke();
            ctx.closePath();

            // 엔티티(탄환 또는 표적) 그리기
            if (currentMode === 'dodge') {
                for (let b of entities) {
                    ctx.beginPath();
                    ctx.arc(b.x, b.y, b.radius, 0, Math.PI * 2);
                    ctx.fillStyle = '#ff4757';
                    ctx.fill();
                    ctx.closePath();
                }
            } else if (currentMode === 'aim') {
                for (let t of entities) {
                    ctx.beginPath();
                    ctx.arc(t.x, t.y, t.radius, 0, Math.PI * 2);
                    ctx.fillStyle = '#ff6b81';
                    ctx.fill();
                    ctx.lineWidth = 3;
                    ctx.strokeStyle = '#ffffff';
                    ctx.stroke();
                    ctx.closePath();
                }
            }
        }
    </script>
</body>
</html>
