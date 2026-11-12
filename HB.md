# happy-birthday
<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Happy Birthday!</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            background: linear-gradient(135deg, #ff9a9e 0%, #fecfef 99%, #fecfef 100%);
            overflow: hidden;
            text-align: center;
        }

        .container {
            background: rgba(255, 255, 255, 0.85);
            padding: 50px 40px;
            border-radius: 25px;
            box-shadow: 0 15px 35px rgba(0, 0, 0, 0.1);
            backdrop-filter: blur(10px);
            max-width: 90%;
            width: 500px;
            transition: all 0.5s ease;
            z-index: 10;
        }

        h1 {
            font-size: 3rem;
            color: #ff477e;
            margin-bottom: 30px;
            letter-spacing: 2px;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.05);
        }

        .start-btn {
            padding: 15px 45px;
            font-size: 1.5rem;
            font-weight: bold;
            color: white;
            background: linear-gradient(45deg, #ff477e, #ff7096);
            border: none;
            border-radius: 50px;
            cursor: pointer;
            box-shadow: 0 8px 20px rgba(255, 71, 126, 0.4);
            transition: transform 0.2s, box-shadow 0.2s;
        }

        .start-btn:hover {
            transform: translateY(-3px) scale(1.05);
            box-shadow: 0 12px 25px rgba(255, 71, 126, 0.6);
        }

        .start-btn:active {
            transform: translateY(1px);
        }

        /* 隱藏第二頁的樣式 */
        .hidden {
            display: none;
        }

        /* 祝福文字動畫 */
        .celebrate-text {
            font-size: 2.8rem;
            color: #ff2a6d;
            animation: popIn 0.8s cubic-bezier(0.175, 0.885, 0.32, 1.275) forwards;
        }

        .sub-text {
            margin-top: 15px;
            font-size: 1.2rem;
            color: #666;
            animation: fadeIn 1.5s ease forwards;
        }

        @keyframes popIn {
            0% {
                opacity: 0;
                transform: scale(0.5);
            }
            100% {
                opacity: 1;
                transform: scale(1);
            }
        }

        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }

        /* 彩帶畫布 */
        canvas {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 1;
        }
    </style>
</head>
<body>

    <canvas id="confetti"></canvas>

    <!-- 首頁畫面 -->
    <div class="container" id="home-screen">
        <h1>Happy Birthday</h1>
        <button class="start-btn" onclick="startCelebration()">Start</button>
    </div>

    <!-- 點擊 Start 後的畫面 -->
    <div class="container hidden" id="wish-screen">
        <h1 class="celebrate-text">🎂 niuwan 生日快樂！ 🎉</h1>
        <p class="sub-text">願你的每一天都充滿陽光與歡笑 ✨</p>
    </div>

    <script>
        function startCelebration() {
            // 隱藏首頁，顯示祝福畫面
            document.getElementById('home-screen').classList.add('hidden');
            document.getElementById('wish-screen').classList.remove('hidden');
            
            // 啟動彩帶特效
            launchConfetti();
        }

        // 簡易彩帶飄落特效
        function launchConfetti() {
            const canvas = document.getElementById('confetti');
            const ctx = canvas.getContext('2d');
            canvas.width = window.innerWidth;
            canvas.height = window.innerHeight;

            const pieces = [];
            const colors = ['#ff477e', '#ff85a1', '#fbb1bd', '#ffd166', '#06d6a0', '#118ab2'];

            for (let i = 0; i < 120; i++) {
                pieces.push({
                    x: Math.random() * canvas.width,
                    y: Math.random() * canvas.height - canvas.height,
                    w: Math.random() * 10 + 5,
                    h: Math.random() * 10 + 5,
                    color: colors[Math.floor(Math.random() * colors.length)],
                    speed: Math.random() * 3 + 2,
                    angle: Math.random() * 360
                });
            }

            function update() {
                ctx.clearRect(0, 0, canvas.width, canvas.height);
                pieces.forEach(p => {
                    p.y += p.speed;
                    p.angle += 2;
                    if (p.y > canvas.height) p.y = -10;

                    ctx.save();
                    ctx.translate(p.x, p.y);
                    ctx.rotate(p.angle * Math.PI / 180);
                    ctx.fillStyle = p.color;
                    ctx.fillRect(-p.w / 2, -p.h / 2, p.w, p.h);
                    ctx.restore();
                });
                requestAnimationFrame(update);
            }
            update();
        }
    </script>
</body>
</html>
