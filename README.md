# Nitro--Highway--racer-.-GitHub.io

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>🏁 Nitro Highway Racer - Ultimate Edition</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            overflow: hidden;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            touch-action: none;
        }

        #gameContainer {
            position: relative;
            width: 100vw;
            height: 100vh;
        }

        #gameCanvas {
            display: block;
            width: 100%;
            height: 100%;
            filter: contrast(1.1);
        }

        #ui {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 10;
        }

        #score {
            position: absolute;
            top: 20px;
            left: 20px;
            color: white;
            font-size: 24px;
            font-weight: bold;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.5);
            background: rgba(0,0,0,0.3);
            padding: 10px 20px;
            border-radius: 10px;
            backdrop-filter: blur(10px);
        }

        #distance {
            position: absolute;
            top: 20px;
            left: 50%;
            transform: translateX(-50%);
            color: white;
            font-size: 24px;
            font-weight: bold;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.5);
            background: rgba(0,0,0,0.3);
            padding: 10px 20px;
            border-radius: 10px;
            backdrop-filter: blur(10px);
        }

        #combo {
            position: absolute;
            top: 70px;
            left: 20px;
            color: #FFD700;
            font-size: 20px;
            font-weight: bold;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.5);
            background: rgba(0,0,0,0.3);
            padding: 8px 15px;
            border-radius: 10px;
            backdrop-filter: blur(10px);
            display: none;
            animation: comboFlash 0.5s ease;
        }

        @keyframes comboFlash {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.1); }
        }

        #speedometer {
            position: absolute;
            top: 20px;
            right: 20px;
            width: 150px;
            height: 150px;
            background: radial-gradient(circle, rgba(0,0,0,0.8), rgba(0,0,0,0.4));
            border-radius: 50%;
            border: 3px solid #fff;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            box-shadow: 0 0 20px rgba(0,0,0,0.5);
            transition: all 0.3s ease;
        }

        #speedometer.nitro {
            box-shadow: 0 0 30px rgba(255,0,255,0.8);
            border-color: #FF00FF;
        }

        #speedValue {
            color: #00ff00;
            font-size: 36px;
            font-weight: bold;
            text-shadow: 0 0 10px #00ff00;
            transition: all 0.3s ease;
        }

        #speedometer.nitro #speedValue {
            color: #FF00FF;
            text-shadow: 0 0 15px #FF00FF;
        }

        #speedLabel {
            color: white;
            font-size: 12px;
            margin-top: 5px;
        }

        #nitroBar {
            position: absolute;
            bottom: 160px;
            left: 50%;
            transform: translateX(-50%);
            width: 300px;
            height: 30px;
            background: rgba(0,0,0,0.5);
            border: 2px solid #fff;
            border-radius: 15px;
            overflow: hidden;
            pointer-events: all;
        }

        #nitroFill {
            height: 100%;
            background: linear-gradient(90deg, #FF00FF, #00FFFF);
            width: 100%;
            transition: width 0.3s ease;
            box-shadow: 0 0 10px rgba(255,0,255,0.5);
        }

        #nitroLabel {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            color: white;
            font-weight: bold;
            font-size: 14px;
            text-shadow: 1px 1px 2px rgba(0,0,0,0.8);
        }

        #powerUpIndicator {
            position: absolute;
            top: 70px;
            right: 20px;
            color: white;
            font-size: 18px;
            font-weight: bold;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.5);
            background: rgba(0,0,0,0.3);
            padding: 10px 20px;
            border-radius: 10px;
            backdrop-filter: blur(10px);
            display: none;
        }

        #highScore {
            position: absolute;
            top: 120px;
            left: 20px;
            color: #FFD700;
            font-size: 18px;
            font-weight: bold;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.5);
            background: rgba(0,0,0,0.3);
            padding: 8px 15px;
            border-radius: 10px;
            backdrop-filter: blur(10px);
        }

        #gameOver {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background: linear-gradient(135deg, rgba(0,0,0,0.9), rgba(50,50,50,0.9));
            padding: 40px;
            border-radius: 20px;
            text-align: center;
            color: white;
            display: none;
            pointer-events: all;
            box-shadow: 0 10px 40px rgba(0,0,0,0.5);
            backdrop-filter: blur(10px);
        }

        #gameOver h2 {
            font-size: 48px;
            margin-bottom: 20px;
            background: linear-gradient(45deg, #ff6b6b, #ffd93d);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }

        #finalScore {
            font-size: 24px;
            margin-bottom: 10px;
            color: #ffd93d;
        }

        #finalDistance {
            font-size: 24px;
            margin-bottom: 10px;
            color: #ffd93d;
        }

        #finalCombo {
            font-size: 20px;
            margin-bottom: 30px;
            color: #FF69B4;
        }

        #restartBtn {
            background: linear-gradient(45deg, #667eea, #764ba2);
            color: white;
            border: none;
            padding: 15px 40px;
            font-size: 20px;
            border-radius: 50px;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(102, 126, 234, 0.4);
        }

        #restartBtn:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(102, 126, 234, 0.6);
        }

        #startScreen {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            z-index: 20;
        }

        #startScreen h1 {
            font-size: 72px;
            color: white;
            margin-bottom: 20px;
            text-shadow: 3px 3px 6px rgba(0,0,0,0.3);
            animation: pulse 2s infinite;
        }

        @keyframes pulse {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.05); }
        }

        #instructions {
            color: white;
            font-size: 18px;
            margin-bottom: 30px;
            text-align: center;
            line-height: 1.6;
        }

        #startBtn {
            background: white;
            color: #667eea;
            border: none;
            padding: 20px 60px;
            font-size: 24px;
            font-weight: bold;
            border-radius: 50px;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(0,0,0,0.2);
        }

        #startBtn:hover {
            transform: translateY(-3px);
            box-shadow: 0 6px 25px rgba(0,0,0,0.3);
        }

        /* Left Steering Button */
        #leftSteerBtn {
            position: absolute;
            left: 30px;
            top: 50%;
            transform: translateY(-50%);
            width: 100px;
            height: 100px;
            background: linear-gradient(145deg, rgba(255,165,0,0.3), rgba(255,165,0,0.1));
            border: 4px solid rgba(255,165,0,0.5);
            border-radius: 50%;
            color: white;
            font-size: 48px;
            font-weight: bold;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            transition: all 0.2s ease;
            backdrop-filter: blur(10px);
            box-shadow: 0 4px 20px rgba(255,165,0,0.4);
            user-select: none;
            -webkit-user-select: none;
            -webkit-tap-highlight-color: transparent;
            pointer-events: all;
        }

        #leftSteerBtn:hover {
            background: linear-gradient(145deg, rgba(255,165,0,0.4), rgba(255,165,0,0.2));
            transform: translateY(-50%) scale(1.05);
            box-shadow: 0 6px 25px rgba(255,165,0,0.6);
        }

        #leftSteerBtn:active {
            background: linear-gradient(145deg, rgba(255,165,0,0.5), rgba(255,165,0,0.3));
            transform: translateY(-50%) scale(0.95);
            box-shadow: 0 2px 15px rgba(255,165,0,0.4);
        }

        #leftSteerBtn.pressed {
            background: linear-gradient(145deg, rgba(255,140,0,0.8), rgba(255,165,0,0.6));
            border-color: rgba(255,255,255,0.7);
            transform: translateY(-50%) scale(0.9);
        }

        /* Right Steering Button */
        #rightSteerBtn {
            position: absolute;
            right: 30px;
            top: 50%;
            transform: translateY(-50%);
            width: 100px;
            height: 100px;
            background: linear-gradient(145deg, rgba(255,165,0,0.3), rgba(255,165,0,0.1));
            border: 4px solid rgba(255,165,0,0.5);
            border-radius: 50%;
            color: white;
            font-size: 48px;
            font-weight: bold;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            transition: all 0.2s ease;
            backdrop-filter: blur(10px);
            box-shadow: 0 4px 20px rgba(255,165,0,0.4);
            user-select: none;
            -webkit-user-select: none;
            -webkit-tap-highlight-color: transparent;
            pointer-events: all;
        }

        #rightSteerBtn:hover {
            background: linear-gradient(145deg, rgba(255,165,0,0.4), rgba(255,165,0,0.2));
            transform: translateY(-50%) scale(1.05);
            box-shadow: 0 6px 25px rgba(255,165,0,0.6);
        }

        #rightSteerBtn:active {
            background: linear-gradient(145deg, rgba(255,165,0,0.5), rgba(255,165,0,0.3));
            transform: translateY(-50%) scale(0.95);
            box-shadow: 0 2px 15px rgba(255,165,0,0.4);
        }

        #rightSteerBtn.pressed {
            background: linear-gradient(145deg, rgba(255,140,0,0.8), rgba(255,165,0,0.6));
            border-color: rgba(255,255,255,0.7);
            transform: translateY(-50%) scale(0.9);
        }

        /* Brake Button */
        #brakeBtn {
            position: absolute;
            left: 50px;
            bottom: 50px;
            width: 120px;
            height: 120px;
            background: linear-gradient(145deg, rgba(255,0,0,0.3), rgba(255,0,0,0.1));
            border: 4px solid rgba(255,0,0,0.5);
            border-radius: 50%;
            color: white;
            font-size: 48px;
            font-weight: bold;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            transition: all 0.2s ease;
            backdrop-filter: blur(10px);
            box-shadow: 0 4px 20px rgba(255,0,0,0.4);
            user-select: none;
            -webkit-user-select: none;
            -webkit-tap-highlight-color: transparent;
            pointer-events: all;
        }

        #brakeBtn:hover {
            background: linear-gradient(145deg, rgba(255,0,0,0.4), rgba(255,0,0,0.2));
            transform: scale(1.05);
            box-shadow: 0 6px 25px rgba(255,0,0,0.6);
        }

        #brakeBtn:active {
            background: linear-gradient(145deg, rgba(255,0,0,0.5), rgba(255,0,0,0.3));
            transform: scale(0.95);
            box-shadow: 0 2px 15px rgba(255,0,0,0.4);
        }

        #brakeBtn.pressed {
            background: linear-gradient(145deg, rgba(220,0,0,0.8), rgba(255,0,0,0.6));
            border-color: rgba(255,255,255,0.7);
            transform: scale(0.9);
        }

        /* Accelerator Button */
        #accelerateBtn {
            position: absolute;
            right: 50px;
            bottom: 50px;
            width: 120px;
            height: 120px;
            background: linear-gradient(145deg, rgba(0,255,0,0.3), rgba(0,255,0,0.1));
            border: 4px solid rgba(0,255,0,0.5);
            border-radius: 50%;
            color: white;
            font-size: 48px;
            font-weight: bold;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            transition: all 0.2s ease;
            backdrop-filter: blur(10px);
            box-shadow: 0 4px 20px rgba(0,255,0,0.4);
            user-select: none;
            -webkit-user-select: none;
            -webkit-tap-highlight-color: transparent;
            pointer-events: all;
        }

        #accelerateBtn:hover {
            background: linear-gradient(145deg, rgba(0,255,0,0.4), rgba(0,255,0,0.2));
            transform: scale(1.05);
            box-shadow: 0 6px 25px rgba(0,255,0,0.6);
        }

        #accelerateBtn:active {
            background: linear-gradient(145deg, rgba(0,255,0,0.5), rgba(0,255,0,0.3));
            transform: scale(0.95);
            box-shadow: 0 2px 15px rgba(0,255,0,0.4);
        }

        #accelerateBtn.pressed {
            background: linear-gradient(145deg, rgba(0,220,0,0.8), rgba(0,255,0,0.6));
            border-color: rgba(255,255,255,0.7);
            transform: scale(0.9);
        }

        /* Nitro Button */
        #nitroBtn {
            position: absolute;
            left: 50%;
            bottom: 50px;
            transform: translateX(-50%);
            width: 100px;
            height: 100px;
            background: linear-gradient(145deg, rgba(255,0,255,0.3), rgba(0,255,255,0.1));
            border: 4px solid rgba(255,0,255,0.5);
            border-radius: 50%;
            color: white;
            font-size: 36px;
            font-weight: bold;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            transition: all 0.2s ease;
            backdrop-filter: blur(10px);
            box-shadow: 0 4px 20px rgba(255,0,255,0.4);
            user-select: none;
            -webkit-user-select: none;
            -webkit-tap-highlight-color: transparent;
            pointer-events: all;
        }

        #nitroBtn:hover {
            background: linear-gradient(145deg, rgba(255,0,255,0.4), rgba(0,255,255,0.2));
            transform: translateX(-50%) scale(1.05);
            box-shadow: 0 6px 25px rgba(255,0,255,0.6);
        }

        #nitroBtn:active {
            background: linear-gradient(145deg, rgba(255,0,255,0.5), rgba(0,255,255,0.3));
            transform: translateX(-50%) scale(0.95);
            box-shadow: 0 2px 15px rgba(255,0,255,0.4);
        }

        #nitroBtn.pressed {
            background: linear-gradient(145deg, rgba(220,0,255,0.8), rgba(0,255,255,0.6));
            border-color: rgba(255,255,255,0.7);
            transform: translateX(-50%) scale(0.9);
        }

        /* Steering button labels */
        .steerLabel {
            position: absolute;
            bottom: -25px;
            left: 50%;
            transform: translateX(-50%);
            color: white;
            font-size: 12px;
            font-weight: bold;
            text-shadow: 1px 1px 2px rgba(0,0,0,0.8);
            white-space: nowrap;
        }

        /* Control button labels */
        .controlLabel {
            position: absolute;
            bottom: -25px;
            left: 50%;
            transform: translateX(-50%);
            color: white;
            font-size: 12px;
            font-weight: bold;
            text-shadow: 1px 1px 2px rgba(0,0,0,0.8);
            white-space: nowrap;
        }

        /* Mobile responsiveness */
        @media (max-width: 768px) {
            #leftSteerBtn, #rightSteerBtn {
                width: 80px;
                height: 80px;
                font-size: 36px;
            }
            
            #leftSteerBtn {
                left: 15px;
            }
            
            #rightSteerBtn {
                right: 15px;
            }
            
            #brakeBtn, #accelerateBtn {
                width: 90px;
                height: 90px;
                font-size: 36px;
            }
            
            #brakeBtn {
                left: 30px;
                bottom: 30px;
            }
            
            #accelerateBtn {
                right: 30px;
                bottom: 30px;
            }
            
            #nitroBtn {
                width: 80px;
                height: 80px;
                font-size: 28px;
                bottom: 30px;
            }
            
            #speedometer {
                width: 120px;
                height: 120px;
                top: 15px;
                right: 15px;
            }
            
            #speedValue {
                font-size: 28px;
            }
            
            #score, #distance {
                font-size: 20px;
                padding: 8px 15px;
            }

            #nitroBar {
                width: 250px;
                bottom: 140px;
            }
        }

        /* Floating text animation */
        .floatingText {
            position: absolute;
            color: #FFD700;
            font-size: 24px;
            font-weight: bold;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.8);
            pointer-events: none;
            animation: floatUp 1s ease-out forwards;
        }

        @keyframes floatUp {
            0% {
                transform: translateY(0);
                opacity: 1;
            }
            100% {
                transform: translateY(-50px);
                opacity: 0;
            }
        }
    </style>
</head>
<body>
    <div id="gameContainer">
        <canvas id="gameCanvas"></canvas>
        
        <div id="ui">
            <div id="score">Score: 0</div>
            <div id="distance">Distance: 0m</div>
            <div id="combo">COMBO x<span id="comboValue">0</span></div>
            <div id="highScore">High Score: 0</div>
            
            <div id="speedometer">
                <div id="speedValue">0</div>
                <div id="speedLabel">KM/H</div>
            </div>
            
            <div id="powerUpIndicator"></div>
            
            <div id="nitroBar">
                <div id="nitroFill"></div>
                <div id="nitroLabel">NITRO</div>
            </div>
            
            <!-- Left Steering Button -->
            <button id="leftSteerBtn" class="steerBtn">
                ◀️
                <span class="steerLabel">LEFT</span>
            </button>
            
            <!-- Right Steering Button -->
            <button id="rightSteerBtn" class="steerBtn">
                ▶️
                <span class="steerLabel">RIGHT</span>
            </button>
            
            <!-- Brake Button -->
            <button id="brakeBtn" class="controlBtn">
                🛑
                <span class="controlLabel">BRAKE</span>
            </button>
            
            <!-- Accelerator Button -->
            <button id="accelerateBtn" class="controlBtn">
                🚀
                <span class="controlLabel">GAS</span>
            </button>
            
            <!-- Nitro Button -->
            <button id="nitroBtn" class="controlBtn">
                ⚡
                <span class="controlLabel">NITRO</span>
            </button>
            
            <div id="gameOver">
                <h2>Game Over!</h2>
                <div id="finalScore">Final Score: 0</div>
                <div id="finalDistance">Distance: 0m</div>
                <div id="finalCombo">Max Combo: x0</div>
                <button id="restartBtn">Play Again</button>
            </div>
        </div>
        
        <div id="startScreen">
            <h1>🏁 Nitro Highway Racer</h1>
            <div id="instructions">
                Use arrow keys or on-screen buttons to control<br>
                ◀️ ▶️ buttons on sides to steer left and right<br>
                🚀 GAS on right, 🛑 BRAKE on left<br>
                ⚡ NITRO in the center for insane speed!<br>
                Collect power-ups and build combos!<br>
                Avoid obstacles and survive as long as you can!
            </div>
            <button id="startBtn">Start Game</button>
        </div>
    </div>

    <script>
        // Game variables
        const canvas = document.getElementById('gameCanvas');
        const ctx = canvas.getContext('2d');
        const scoreElement = document.getElementById('score');
        const distanceElement = document.getElementById('distance');
        const comboElement = document.getElementById('combo');
        const comboValueElement = document.getElementById('comboValue');
        const highScoreElement = document.getElementById('highScore');
        const speedValueElement = document.getElementById('speedValue');
        const speedometerElement = document.getElementById('speedometer');
        const powerUpIndicator = document.getElementById('powerUpIndicator');
        const nitroFillElement = document.getElementById('nitroFill');
        const gameOverScreen = document.getElementById('gameOver');
        const finalScoreElement = document.getElementById('finalScore');
        const finalDistanceElement = document.getElementById('finalDistance');
        const finalComboElement = document.getElementById('finalCombo');
        const restartBtn = document.getElementById('restartBtn');
        const startScreen = document.getElementById('startScreen');
        const startBtn = document.getElementById('startBtn');

        // Control buttons
        const leftSteerBtn = document.getElementById('leftSteerBtn');
        const rightSteerBtn = document.getElementById('rightSteerBtn');
        const accelerateBtn = document.getElementById('accelerateBtn');
        const brakeBtn = document.getElementById('brakeBtn');
        const nitroBtn = document.getElementById('nitroBtn');

        // Set canvas size
        function resizeCanvas() {
            canvas.width = window.innerWidth;
            canvas.height = window.innerHeight;
        }
        resizeCanvas();
        window.addEventListener('resize', resizeCanvas);

        // Game state
        let gameRunning = false;
        let score = 0;
        let distance = 0;
        let speed = 0;
        let maxSpeed = 300;
        let acceleration = 0.5;
        let deceleration = 0.3;
        let roadOffset = 0;
        let frameCount = 0;
        let raceStartTime = 0;
        
        // Time-based animation variables
        let lastTime = 0;
        let deltaTime = 0;
        const targetFPS = 60;
        const frameDelay = 1000 / targetFPS;
        let accumulator = 0;

        // New dynamic features
        let combo = 0;
        let maxCombo = 0;
        let nitro = 100;
        let nitroActive = false;
        let screenShake = 0;
        let powerUpActive = null;
        let powerUpTimer = 0;
        let highScore = localStorage.getItem('highScore') || 0;
        let nearMissTimer = 0;
        let speedTrails = [];
        let particles = [];

        // Performance optimization - limit objects
        const MAX_TREES = 20;
        const MAX_FLAG_POLES = 8;
        const MAX_OBSTACLES = 6;
        const MAX_POWERUPS = 3;

        // Player car
        const playerCar = {
            x: 0,
            y: 0,
            width: 40,
            height: 60,
            lane: 1, // 0, 1, 2 (left, middle, right)
            targetX: 0,
            color: '#ff4444',
            invulnerable: false,
            invulnerableTimer: 0
        };

        // Road properties
        const road = {
            width: 400,
            laneWidth: 120,
            x: 0,
            y: 0
        };

        // Obstacles array
        let obstacles = [];

        // Power-ups array
        let powerUps = [];

        // Trees array
        let trees = [];

        // Flag poles array
        let flagPoles = [];

        // Road segments for perspective
        let roadSegments = [];

        // Particle class
        class Particle {
            constructor(x, y, color, velocity) {
                this.x = x;
                this.y = y;
                this.color = color;
                this.velocity = velocity;
                this.life = 1.0;
                this.decay = 0.02;
                this.size = Math.random() * 3 + 1;
            }

            update(deltaTime) {
                this.x += this.velocity.x * (deltaTime / 16);
                this.y += this.velocity.y * (deltaTime / 16);
                this.life -= this.decay * (deltaTime / 16);
                this.velocity.y += 0.2; // Gravity
            }

            draw() {
                ctx.save();
                ctx.globalAlpha = this.life;
                ctx.fillStyle = this.color;
                ctx.beginPath();
                ctx.arc(this.x, this.y, this.size, 0, Math.PI * 2);
                ctx.fill();
                ctx.restore();
            }
        }

        // Speed trail class
        class SpeedTrail {
            constructor(x, y, width, height) {
                this.x = x;
                this.y = y;
                this.width = width;
                this.height = height;
                this.life = 1.0;
                this.decay = 0.05;
            }

            update(deltaTime) {
                this.life -= this.decay * (deltaTime / 16);
                this.y += 2 * (deltaTime / 16);
            }

            draw() {
                ctx.save();
                ctx.globalAlpha = this.life * 0.3;
                const gradient = ctx.createLinearGradient(this.x, this.y, this.x, this.y + this.height);
                gradient.addColorStop(0, nitroActive ? '#FF00FF' : '#00FFFF');
                gradient.addColorStop(1, 'transparent');
                ctx.fillStyle = gradient;
                ctx.fillRect(this.x, this.y, this.width, this.height);
                ctx.restore();
            }
        }

        // Initialize road segments
        function initRoadSegments() {
            roadSegments = [];
            for (let i = 0; i < 30; i++) {
                roadSegments.push({
                    y: i * 20,
                    width: 0
                });
            }
        }

        // Initialize trees
        function initTrees() {
            trees = [];
            for (let i = 0; i < MAX_TREES; i++) {
                createTree(i * 50);
            }
        }

        // Initialize flag poles
        function initFlagPoles() {
            flagPoles = [];
            for (let i = 0; i < MAX_FLAG_POLES; i++) {
                createFlagPole(i * 200 + 100);
            }
        }

        // Create tree at specific y position
        function createTree(y) {
            if (trees.length >= MAX_TREES) return;
            
            const horizonY = canvas.height * 0.35;
            const side = Math.random() < 0.5 ? 'left' : 'right';
            const treeTypes = ['pine', 'oak', 'birch'];
            const type = treeTypes[Math.floor(Math.random() * treeTypes.length)];
            
            trees.push({
                y: y,
                side: side,
                type: type,
                baseSize: 20 + Math.random() * 15,
                color: getTreeColor(type),
                swayOffset: Math.random() * Math.PI * 2
            });
        }

        // Create flag pole at specific y position
        function createFlagPole(y) {
            if (flagPoles.length >= MAX_FLAG_POLES) return;
            
            const side = Math.random() < 0.5 ? 'left' : 'right';
            const flagColors = ['#FF0000', '#FFFFFF', '#0000FF', '#FFFF00', '#00FF00'];
            const flagColor = flagColors[Math.floor(Math.random() * flagColors.length)];
            
            flagPoles.push({
                y: y,
                side: side,
                baseHeight: 150 + Math.random() * 50,
                flagColor: flagColor,
                waveOffset: Math.random() * Math.PI * 2,
                flagWidth: 40 + Math.random() * 20,
                flagHeight: 25 + Math.random() * 10
            });
        }

        // Create power-up
        function createPowerUp() {
            if (powerUps.length >= MAX_POWERUPS) return;
            
            const lane = Math.floor(Math.random() * 3);
            const types = ['shield', 'turbo', 'points'];
            const type = types[Math.floor(Math.random() * types.length)];
            
            powerUps.push({
                lane: lane,
                y: canvas.height * 0.35,
                width: 30,
                height: 30,
                type: type,
                color: getPowerUpColor(type),
                rotation: 0
            });
        }

        // Get power-up color
        function getPowerUpColor(type) {
            switch(type) {
                case 'shield': return '#00FF00';
                case 'turbo': return '#FF00FF';
                case 'points': return '#FFD700';
                default: return '#FFFFFF';
            }
        }

        // Get tree color based on type
        function getTreeColor(type) {
            switch(type) {
                case 'pine': return '#0d4f0d';
                case 'oak': return '#2d5016';
                case 'birch': return '#4a5d23';
                default: return '#2d5016';
            }
        }

        // Create explosion particles
        function createExplosion(x, y, color) {
            for (let i = 0; i < 20; i++) {
                const angle = (Math.PI * 2 * i) / 20;
                const velocity = {
                    x: Math.cos(angle) * (Math.random() * 5 + 2),
                    y: Math.sin(angle) * (Math.random() * 5 + 2)
                };
                particles.push(new Particle(x, y, color, velocity));
            }
        }

        // Create speed trail
        function createSpeedTrail() {
            if (speed > 150 && frameCount % 2 === 0) {
                const carX = canvas.width / 2 + playerCar.x - playerCar.width / 2;
                const carY = canvas.height - 150;
                speedTrails.push(new SpeedTrail(carX, carY + playerCar.height, playerCar.width, 20));
            }
        }

        // Show floating text
        function showFloatingText(x, y, text, color = '#FFD700') {
            const floatingText = document.createElement('div');
            floatingText.className = 'floatingText';
            floatingText.textContent = text;
            floatingText.style.left = x + 'px';
            floatingText.style.top = y + 'px';
            floatingText.style.color = color;
            document.getElementById('ui').appendChild(floatingText);
            
            setTimeout(() => {
                floatingText.remove();
            }, 1000);
        }

        // Input handling
        const keys = {};
        
        // Keyboard events
        document.addEventListener('keydown', (e) => {
            keys[e.key] = true;
        });
        document.addEventListener('keyup', (e) => {
            keys[e.key] = false;
        });

        // Button event handlers
        function handleButtonPress(button, key) {
            button.addEventListener('mousedown', () => {
                keys[key] = true;
                button.classList.add('pressed');
            });
            
            button.addEventListener('mouseup', () => {
                keys[key] = false;
                button.classList.remove('pressed');
            });
            
            button.addEventListener('mouseleave', () => {
                keys[key] = false;
                button.classList.remove('pressed');
            });
            
            // Touch events for mobile
            button.addEventListener('touchstart', (e) => {
                e.preventDefault();
                keys[key] = true;
                button.classList.add('pressed');
            });
            
            button.addEventListener('touchend', (e) => {
                e.preventDefault();
                keys[key] = false;
                button.classList.remove('pressed');
            });
        }

        // Initialize button controls
        handleButtonPress(leftSteerBtn, 'ArrowLeft');
        handleButtonPress(rightSteerBtn, 'ArrowRight');
        handleButtonPress(accelerateBtn, 'ArrowUp');
        handleButtonPress(brakeBtn, 'ArrowDown');
        handleButtonPress(nitroBtn, ' ');

        // Calculate lane position at a specific y coordinate
        function getLanePosition(lane, y) {
            const horizonY = canvas.height * 0.35;
            const playerY = canvas.height - 150;
            const progress = (y - horizonY) / (playerY - horizonY);
            
            const roadTopWidth = 50;
            const roadBottomWidth = road.width;
            const roadWidthAtY = roadTopWidth + (roadBottomWidth - roadTopWidth) * Math.pow(progress, 0.7);
            
            const lanePositions = [-1/3, 0, 1/3];
            return roadWidthAtY * lanePositions[lane];
        }

        // Create obstacle at the horizon
        function createObstacle() {
            if (obstacles.length >= MAX_OBSTACLES) return;
            
            const lane = Math.floor(Math.random() * 3);
            const types = ['car', 'truck', 'motorcycle'];
            const type = types[Math.floor(Math.random() * types.length)];
            
            let width, height, color;
            switch(type) {
                case 'car':
                    width = 40;
                    height = 60;
                    color = `hsl(${Math.random() * 60 + 180}, 70%, 50%)`;
                    break;
                case 'truck':
                    width = 50;
                    height = 80;
                    color = `hsl(${Math.random() * 60 + 30}, 70%, 40%)`;
                    break;
                case 'motorcycle':
                    width = 25;
                    height = 40;
                    color = `hsl(${Math.random() * 60 + 270}, 70%, 60%)`;
                    break;
            }
            
            obstacles.push({
                lane: lane,
                y: canvas.height * 0.35,
                width: width,
                height: height,
                color: color,
                type: type,
                speed: 0
            });
        }

        // Update game with time-based animation
        function update(deltaTime) {
            if (!gameRunning) return;

            deltaTime = Math.min(deltaTime, 50);
            frameCount++;

            // Handle steering
            if (keys['ArrowLeft'] && playerCar.lane > 0) {
                playerCar.lane = 0;
            } else if (keys['ArrowRight'] && playerCar.lane < 2) {
                playerCar.lane = 2;
            } else if (!keys['ArrowLeft'] && !keys['ArrowRight']) {
                if (playerCar.lane === 0 || playerCar.lane === 2) {
                    playerCar.lane = 1;
                }
            }

            playerCar.targetX = getLanePosition(playerCar.lane, canvas.height - 150);

            // Handle speed controls
            const currentMaxSpeed = nitroActive ? maxSpeed * 1.5 : maxSpeed;
            const currentAcceleration = nitroActive ? acceleration * 2 : acceleration;
            
            if (keys['ArrowUp']) {
                speed = Math.min(speed + currentAcceleration * (deltaTime / 16), currentMaxSpeed);
            } else if (keys['ArrowDown']) {
                speed = Math.max(speed - deceleration * 2 * (deltaTime / 16), 0);
            } else {
                speed = Math.max(speed - deceleration * (deltaTime / 16), 50);
            }

            // Handle nitro
            if (keys[' '] && nitro > 0 && !nitroActive) {
                nitroActive = true;
                speedometerElement.classList.add('nitro');
            } else if (!keys[' '] || nitro <= 0) {
                nitroActive = false;
                speedometerElement.classList.remove('nitro');
            }

            if (nitroActive) {
                nitro = Math.max(0, nitro - 0.5 * (deltaTime / 16));
                createSpeedTrail();
            } else {
                nitro = Math.min(100, nitro + 0.1 * (deltaTime / 16));
            }

            // Update nitro bar
            nitroFillElement.style.width = nitro + '%';

            // Smooth lane transition
            playerCar.x += (playerCar.targetX - playerCar.x) * 0.15 * (deltaTime / 16);

            // Update road offset
            roadOffset += speed * 0.1 * (deltaTime / 16);
            if (roadOffset > 40) {
                roadOffset = 0;
            }

            // Update distance
            distance += speed * 0.01 * (deltaTime / 16);

            // Update road segments
            roadSegments.forEach(segment => {
                segment.y += speed * 0.1 * (deltaTime / 16);
                if (segment.y > canvas.height) {
                    segment.y = -20;
                }
            });

            // Update trees
            trees = trees.filter(tree => {
                tree.y += speed * 0.1 * (deltaTime / 16);
                tree.swayOffset += 0.02 * (deltaTime / 16);
                return tree.y < canvas.height + 100;
            });

            // Update flag poles
            flagPoles = flagPoles.filter(pole => {
                pole.y += speed * 0.1 * (deltaTime / 16);
                pole.waveOffset += 0.05 * (deltaTime / 16);
                return pole.y < canvas.height + 100;
            });

            // Update obstacles
            obstacles = obstacles.filter(obstacle => {
                obstacle.y += speed * 0.06 * (deltaTime / 16);
                obstacle.x = getLanePosition(obstacle.lane, obstacle.y);
                
                const horizonY = canvas.height * 0.35;
                const playerY = canvas.height - 150;
                const progress = (obstacle.y - horizonY) / (playerY - horizonY);
                
                if (progress > 0) {
                    obstacle.width = obstacle.width * (0.5 + 0.5 * progress);
                    obstacle.height = obstacle.height * (0.5 + 0.5 * progress);
                }
                
                // Check collision
                if (!playerCar.invulnerable && checkCollision(playerCar, obstacle)) {
                    if (powerUpActive === 'shield') {
                        playerCar.invulnerable = true;
                        playerCar.invulnerableTimer = 60;
                        powerUpActive = null;
                        powerUpIndicator.style.display = 'none';
                        createExplosion(canvas.width / 2 + obstacle.x, obstacle.y, '#00FF00');
                        screenShake = 10;
                        return false;
                    } else {
                        createExplosion(canvas.width / 2 + playerCar.x, canvas.height - 150, '#FF0000');
                        screenShake = 20;
                        gameOver();
                    }
                }
                
                // Check near miss
                if (Math.abs(obstacle.y - (canvas.height - 150)) < 100 && 
                    Math.abs(obstacle.lane - playerCar.lane) === 1 && 
                    nearMissTimer <= 0) {
                    combo++;
                    score += 50 * combo;
                    nearMissTimer = 30;
                    comboElement.style.display = 'block';
                    comboValueElement.textContent = combo;
                    showFloatingText(canvas.width / 2, canvas.height / 2, `NEAR MISS! x${combo}`, '#FF69B4');
                    maxCombo = Math.max(maxCombo, combo);
                }
                
                if (obstacle.y > canvas.height + 100) {
                    score += 10;
                    return false;
                }
                
                return true;
            });

            // Update power-ups
            powerUps = powerUps.filter(powerUp => {
                powerUp.y += speed * 0.06 * (deltaTime / 16);
                powerUp.x = getLanePosition(powerUp.lane, powerUp.y);
                powerUp.rotation += 0.05 * (deltaTime / 16);
                
                // Check collection
                if (checkCollision(playerCar, powerUp)) {
                    collectPowerUp(powerUp);
                    return false;
                }
                
                return powerUp.y < canvas.height + 100;
            });

            // Update particles
            particles = particles.filter(particle => {
                particle.update(deltaTime);
                return particle.life > 0;
            });

            // Update speed trails
            speedTrails = speedTrails.filter(trail => {
                trail.update(deltaTime);
                return trail.life > 0;
            });

            // Update timers
            if (nearMissTimer > 0) nearMissTimer -= deltaTime / 16;
            if (playerCar.invulnerableTimer > 0) {
                playerCar.invulnerableTimer -= deltaTime / 16;
                if (playerCar.invulnerableTimer <= 0) {
                    playerCar.invulnerable = false;
                }
            }
            if (powerUpTimer > 0) {
                powerUpTimer -= deltaTime / 16;
                if (powerUpTimer <= 0) {
                    powerUpActive = null;
                    powerUpIndicator.style.display = 'none';
                }
            }
            if (screenShake > 0) {
                screenShake -= deltaTime / 16;
            }

            // Create new objects
            if (frameCount % 40 === 0 && trees.length < MAX_TREES) {
                createTree(canvas.height * 0.35);
            }
            if (frameCount % 80 === 0 && flagPoles.length < MAX_FLAG_POLES) {
                createFlagPole(canvas.height * 0.35);
            }
            if (frameCount % Math.max(60 - Math.floor(speed / 30), 20) === 0) {
                createObstacle();
            }
            if (frameCount % 180 === 0 && powerUps.length < MAX_POWERUPS) {
                createPowerUp();
            }

            // Update score
            score += Math.floor(speed / 50 * (deltaTime / 16));

            // Update UI
            if (frameCount % 5 === 0) {
                scoreElement.textContent = `Score: ${score}`;
                distanceElement.textContent = `Distance: ${Math.floor(distance)}m`;
                speedValueElement.textContent = Math.floor(speed);
                highScoreElement.textContent = `High Score: ${highScore}`;
            }
        }

        // Collect power-up
        function collectPowerUp(powerUp) {
            createExplosion(canvas.width / 2 + powerUp.x, powerUp.y, powerUp.color);
            
            switch(powerUp.type) {
                case 'shield':
                    powerUpActive = 'shield';
                    powerUpTimer = 300; // 5 seconds at 60 FPS
                    powerUpIndicator.textContent = '🛡️ SHIELD ACTIVE';
                    powerUpIndicator.style.display = 'block';
                    showFloatingText(canvas.width / 2, canvas.height / 2, 'SHIELD!', '#00FF00');
                    break;
                case 'turbo':
                    speed = Math.min(speed + 100, maxSpeed);
                    showFloatingText(canvas.width / 2, canvas.height / 2, 'TURBO!', '#FF00FF');
                    break;
                case 'points':
                    score += 500;
                    showFloatingText(canvas.width / 2, canvas.height / 2, '+500', '#FFD700');
                    break;
            }
        }

        // Check collision
        function checkCollision(car1, car2) {
            const car1Left = canvas.width / 2 + car1.x - car1.width / 2;
            const car1Right = car1Left + car1.width;
            const car1Top = canvas.height - 150;
            const car1Bottom = car1Top + car1.height;

            const car2Left = canvas.width / 2 + car2.x - car2.width / 2;
            const car2Right = car2Left + car2.width;
            const car2Top = car2.y;
            const car2Bottom = car2Top + car2.height;

            return !(car1Left > car2Right || 
                    car1Right < car2Left || 
                    car1Top > car2Bottom || 
                    car1Bottom < car2Top);
        }

        // Draw tree
        function drawTree(tree) {
            const horizonY = canvas.height * 0.35;
            const playerY = canvas.height - 150;
            const progress = (tree.y - horizonY) / (playerY - horizonY);
            
            if (progress <= 0) return;
            
            const treeSize = tree.baseSize * progress;
            const vanishingPointX = canvas.width / 2;
            const roadTopWidth = 50;
            const roadBottomWidth = road.width;
            const roadWidthAtY = roadTopWidth + (roadBottomWidth - roadTopWidth) * Math.pow(progress, 0.7);
            
            let treeX;
            if (tree.side === 'left') {
                treeX = vanishingPointX - roadWidthAtY / 2 - 50 * progress - treeSize;
            } else {
                treeX = vanishingPointX + roadWidthAtY / 2 + 50 * progress;
            }
            
            const sway = Math.sin(tree.swayOffset) * 2;
            
            ctx.fillStyle = 'rgba(0,0,0,0.3)';
            ctx.beginPath();
            ctx.ellipse(treeX + sway + 5, tree.y + 5, treeSize * 0.8, treeSize * 0.3, 0, 0, Math.PI * 2);
            ctx.fill();
            
            ctx.fillStyle = '#4a3c28';
            ctx.fillRect(treeX + sway - treeSize * 0.15, tree.y - treeSize * 0.3, treeSize * 0.3, treeSize * 0.6);
            
            ctx.fillStyle = tree.color;
            
            if (tree.type === 'pine') {
                ctx.beginPath();
                ctx.moveTo(treeX + sway, tree.y - treeSize);
                ctx.lineTo(treeX + sway - treeSize * 0.6, tree.y);
                ctx.lineTo(treeX + sway + treeSize * 0.6, tree.y);
                ctx.closePath();
                ctx.fill();
            } else if (tree.type === 'oak') {
                ctx.beginPath();
                ctx.arc(treeX + sway, tree.y - treeSize * 0.5, treeSize * 0.7, 0, Math.PI * 2);
                ctx.fill();
            } else if (tree.type === 'birch') {
                ctx.beginPath();
                ctx.ellipse(treeX + sway, tree.y - treeSize * 0.5, treeSize * 0.5, treeSize * 0.8, 0, 0, Math.PI * 2);
                ctx.fill();
            }
        }

        // Draw flag pole
        function drawFlagPole(pole) {
            const horizonY = canvas.height * 0.35;
            const playerY = canvas.height - 150;
            const progress = (pole.y - horizonY) / (playerY - horizonY);
            
            if (progress <= 0) return;
            
            const poleHeight = pole.baseHeight * progress;
            const poleWidth = 4 * progress;
            const vanishingPointX = canvas.width / 2;
            const roadTopWidth = 50;
            const roadBottomWidth = road.width;
            const roadWidthAtY = roadTopWidth + (roadBottomWidth - roadTopWidth) * Math.pow(progress, 0.7);
            
            let poleX;
            if (pole.side === 'left') {
                poleX = vanishingPointX - roadWidthAtY / 2 - 30 * progress;
            } else {
                poleX = vanishingPointX + roadWidthAtY / 2 + 30 * progress;
            }
            
            ctx.fillStyle = 'rgba(0,0,0,0.3)';
            ctx.fillRect(poleX + 5, pole.y + 5, poleWidth, poleHeight);
            
            ctx.fillStyle = '#8B4513';
            ctx.fillRect(poleX, pole.y - poleHeight, poleWidth, poleHeight);
            
            ctx.fillStyle = '#FFD700';
            ctx.beginPath();
            ctx.arc(poleX + poleWidth/2, pole.y - poleHeight, poleWidth * 1.5, 0, Math.PI * 2);
            ctx.fill();
            
            const flagWidth = pole.flagWidth * progress;
            const flagHeight = pole.flagHeight * progress;
            const wave = Math.sin(pole.waveOffset) * 3 * progress;
            
            ctx.fillStyle = 'rgba(0,0,0,0.3)';
            ctx.beginPath();
            ctx.moveTo(poleX + poleWidth, pole.y - poleHeight + 5);
            ctx.quadraticCurveTo(
                poleX + poleWidth + flagWidth/2 + wave, 
                pole.y - poleHeight + flagHeight/2 + 5, 
                poleX + poleWidth + flagWidth, 
                pole.y - poleHeight + flagHeight + 5
            );
            ctx.lineTo(poleX + poleWidth, pole.y - poleHeight + flagHeight + 5);
            ctx.closePath();
            ctx.fill();
            
            ctx.fillStyle = pole.flagColor;
            ctx.beginPath();
            ctx.moveTo(poleX + poleWidth, pole.y - poleHeight);
            ctx.quadraticCurveTo(
                poleX + poleWidth + flagWidth/2 + wave, 
                pole.y - poleHeight + flagHeight/2, 
                poleX + poleWidth + flagWidth, 
                pole.y - poleHeight + flagHeight
            );
            ctx.lineTo(poleX + poleWidth, pole.y - poleHeight + flagHeight);
            ctx.closePath();
            ctx.fill();
            
            ctx.fillStyle = 'rgba(255,255,255,0.5)';
            const checkSize = 5 * progress;
            for (let i = 0; i < flagWidth / checkSize; i++) {
                for (let j = 0; j < flagHeight / checkSize; j++) {
                    if ((i + j) % 2 === 0) {
                        ctx.fillRect(
                            poleX + poleWidth + i * checkSize, 
                            pole.y - poleHeight + j * checkSize, 
                            checkSize, 
                            checkSize
                        );
                    }
                }
            }
        }

        // Draw power-up
        function drawPowerUp(powerUp) {
            const x = canvas.width / 2 + powerUp.x;
            const y = powerUp.y;
            
            ctx.save();
            ctx.translate(x, y);
            ctx.rotate(powerUp.rotation);
            
            // Glow effect
            ctx.shadowColor = powerUp.color;
            ctx.shadowBlur = 20;
            
            // Draw power-up
            ctx.fillStyle = powerUp.color;
            ctx.fillRect(-powerUp.width/2, -powerUp.height/2, powerUp.width, powerUp.height);
            
            // Draw icon
            ctx.fillStyle = 'white';
            ctx.font = '20px Arial';
            ctx.textAlign = 'center';
            ctx.textBaseline = 'middle';
            
            switch(powerUp.type) {
                case 'shield':
                    ctx.fillText('🛡️', 0, 0);
                    break;
                case 'turbo':
                    ctx.fillText('⚡', 0, 0);
                    break;
                case 'points':
                    ctx.fillText('💎', 0, 0);
                    break;
            }
            
            ctx.restore();
        }

        // Draw race track
        function drawRaceTrack() {
            // Apply screen shake
            if (screenShake > 0) {
                ctx.save();
                const shakeX = (Math.random() - 0.5) * screenShake;
                const shakeY = (Math.random() - 0.5) * screenShake;
                ctx.translate(shakeX, shakeY);
            }
            
            // Sky gradient with dynamic colors based on speed
            const skyGradient = ctx.createLinearGradient(0, 0, 0, canvas.height);
            if (nitroActive) {
                skyGradient.addColorStop(0, '#1a0033');
                skyGradient.addColorStop(0.4, '#330066');
                skyGradient.addColorStop(1, '#4d0099');
            } else {
                skyGradient.addColorStop(0, '#87CEEB');
                skyGradient.addColorStop(0.4, '#98D8E8');
                skyGradient.addColorStop(1, '#B0E0E6');
            }
            ctx.fillStyle = skyGradient;
            ctx.fillRect(0, 0, canvas.width, canvas.height);

            // Draw distant mountains
            ctx.fillStyle = '#8B7355';
            ctx.beginPath();
            ctx.moveTo(0, canvas.height * 0.3);
            ctx.lineTo(canvas.width * 0.3, canvas.height * 0.25);
            ctx.lineTo(canvas.width * 0.5, canvas.height * 0.28);
            ctx.lineTo(canvas.width * 0.7, canvas.height * 0.22);
            ctx.lineTo(canvas.width, canvas.height * 0.3);
            ctx.lineTo(canvas.width, canvas.height * 0.4);
            ctx.lineTo(0, canvas.height * 0.4);
            ctx.closePath();
            ctx.fill();

            const horizonY = canvas.height * 0.35;
            const vanishingPointX = canvas.width / 2;

            ctx.fillStyle = '#228B22';
            ctx.fillRect(0, horizonY, canvas.width, canvas.height - horizonY);

            // Draw trees (behind)
            trees.forEach(tree => {
                if (tree.y < canvas.height * 0.6) {
                    drawTree(tree);
                }
            });

            // Draw flag poles (behind)
            flagPoles.forEach(pole => {
                if (pole.y < canvas.height * 0.6) {
                    drawFlagPole(pole);
                }
            });

            // Draw road
            const roadTop = horizonY;
            const roadBottom = canvas.height;
            const roadTopWidth = 50;
            const roadBottomWidth = road.width;

            const segments = 10;
            for (let i = 0; i < segments; i++) {
                const y1 = roadTop + (roadBottom - roadTop) * (i / segments);
                const y2 = roadTop + (roadBottom - roadTop) * ((i + 1) / segments);
                
                const progress1 = (i / segments);
                const progress2 = ((i + 1) / segments);
                const width1 = roadTopWidth + (roadBottomWidth - roadTopWidth) * Math.pow(progress1, 0.7);
                const width2 = roadTopWidth + (roadBottomWidth - roadTopWidth) * Math.pow(progress2, 0.7);
                
                ctx.fillStyle = nitroActive ? '#1a1a2e' : '#2C2C2C';
                ctx.beginPath();
                ctx.moveTo(vanishingPointX - width1 / 2, y1);
                ctx.lineTo(vanishingPointX + width1 / 2, y1);
                ctx.lineTo(vanishingPointX + width2 / 2, y2);
                ctx.lineTo(vanishingPointX - width2 / 2, y2);
                ctx.closePath();
                ctx.fill();
            }

            // Draw track edges
            ctx.strokeStyle = nitroActive ? '#FF00FF' : '#FFFFFF';
            ctx.lineWidth = 8;
            ctx.beginPath();
            ctx.moveTo(vanishingPointX - roadTopWidth / 2, roadTop);
            ctx.lineTo(vanishingPointX - roadBottomWidth / 2, roadBottom);
            ctx.moveTo(vanishingPointX + roadTopWidth / 2, roadTop);
            ctx.lineTo(vanishingPointX + roadBottomWidth / 2, roadBottom);
            ctx.stroke();

            ctx.strokeStyle = '#FF0000';
            ctx.lineWidth = 4;
            ctx.beginPath();
            ctx.moveTo(vanishingPointX - roadTopWidth / 2 + 5, roadTop);
            ctx.lineTo(vanishingPointX - roadBottomWidth / 2 + 20, roadBottom);
            ctx.moveTo(vanishingPointX + roadTopWidth / 2 - 5, roadTop);
            ctx.lineTo(vanishingPointX + roadBottomWidth / 2 - 20, roadBottom);
            ctx.stroke();

            // Draw lane markings
            ctx.strokeStyle = nitroActive ? '#00FFFF' : '#FFFFFF';
            ctx.lineWidth = 6;
            ctx.setLineDash([30, 20]);
            ctx.lineDashOffset = -roadOffset;

            const lanePositions = [-1/3, 0, 1/3];
            
            lanePositions.forEach(lanePos => {
                ctx.beginPath();
                ctx.moveTo(vanishingPointX + roadTopWidth * lanePos, roadTop);
                ctx.lineTo(vanishingPointX + roadBottomWidth * lanePos, roadBottom);
                ctx.stroke();
            });

            ctx.setLineDash([]);

            // Draw barriers
            ctx.fillStyle = '#FF6600';
            for (let i = 0; i < 10; i++) {
                const y = roadTop + (roadBottom - roadTop) * (i / 10);
                const progress = i / 10;
                const width = 10 + (30 - 10) * Math.pow(progress, 0.7);
                
                const roadWidthAtY = roadTopWidth + (roadBottomWidth - roadTopWidth) * Math.pow(progress, 0.7);
                ctx.fillRect(vanishingPointX - roadWidthAtY / 2 - width - 5, y - 10, width, 20);
                ctx.fillRect(vanishingPointX + roadWidthAtY / 2 + 5, y - 10, width, 20);
            }

            // Draw start/finish line
            const finishLineY = canvas.height * 0.7;
            const finishProgress = (finishLineY - roadTop) / (roadBottom - roadTop);
            const finishLineWidth = roadTopWidth + (roadBottomWidth - roadTopWidth) * Math.pow(finishProgress, 0.7);
            ctx.fillStyle = '#FFFFFF';
            for (let i = 0; i < 10; i++) {
                if (i % 2 === 0) {
                    ctx.fillRect(
                        vanishingPointX - finishLineWidth / 2 + (finishLineWidth / 10) * i,
                        finishLineY,
                        finishLineWidth / 10,
                        20
                    );
                }
            }

            // Draw trees (in front)
            trees.forEach(tree => {
                if (tree.y >= canvas.height * 0.6) {
                    drawTree(tree);
                }
            });

            // Draw flag poles (in front)
            flagPoles.forEach(pole => {
                if (pole.y >= canvas.height * 0.6) {
                    drawFlagPole(pole);
                }
            });

            if (screenShake > 0) {
                ctx.restore();
            }
        }

        // Draw car
        function drawCar(x, y, width, height, color, isPlayer = false) {
            const carX = canvas.width / 2 + x - width / 2;
            const carY = y;

            // Draw shadow
            ctx.fillStyle = 'rgba(0,0,0,0.4)';
            ctx.fillRect(carX + 3, carY + 3, width, height);

            // Draw car body
            if (isPlayer && playerCar.invulnerable) {
                ctx.fillStyle = `rgba(255,255,255,${0.5 + Math.sin(frameCount * 0.3) * 0.5})`;
            } else {
                ctx.fillStyle = color;
            }
            ctx.fillRect(carX, carY, width, height);

            // Draw car roof
            ctx.fillStyle = 'rgba(0,0,0,0.2)';
            ctx.fillRect(carX + 5, carY + 10, width - 10, 20);

            // Draw windshield
            ctx.fillStyle = '#4A90E2';
            ctx.fillRect(carX + 8, carY + 15, width - 16, 10);

            // Draw racing stripes
            if (isPlayer) {
                ctx.fillStyle = '#FFFFFF';
                ctx.fillRect(carX + width / 2 - 2, carY, 4, height);
            }

            // Draw lights
            if (isPlayer) {
                ctx.fillStyle = nitroActive ? '#FF00FF' : '#FFFF00';
                ctx.fillRect(carX + 5, carY + height - 8, 10, 6);
                ctx.fillRect(carX + width - 15, carY + height - 8, 10, 6);
            } else {
                ctx.fillStyle = '#FF0000';
                ctx.fillRect(carX + 5, carY + 2, 10, 6);
                ctx.fillRect(carX + width - 15, carY + 2, 10, 6);
            }

            // Draw side mirrors
            ctx.fillStyle = '#333';
            ctx.fillRect(carX - 3, carY + 15, 3, 8);
            ctx.fillRect(carX + width, carY + 15, 3, 8);
        }

        // Render game
        function render() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);

            // Draw race track
            drawRaceTrack();

            // Draw speed trails
            speedTrails.forEach(trail => trail.draw());

            // Draw power-ups
            powerUps.forEach(powerUp => drawPowerUp(powerUp));

            // Draw obstacles
            obstacles.forEach(obstacle => {
                drawCar(obstacle.x, obstacle.y, obstacle.width, obstacle.height, obstacle.color, false);
            });

            // Draw player car
            drawCar(playerCar.x, canvas.height - 150, playerCar.width, playerCar.height, playerCar.color, true);

            // Draw particles
            particles.forEach(particle => particle.draw());
        }

        // Game loop
        function gameLoop(timestamp) {
            if (!lastTime) lastTime = timestamp;
            
            const currentTime = timestamp;
            const elapsed = currentTime - lastTime;
            lastTime = currentTime;
            
            accumulator += elapsed;
            
            while (accumulator >= frameDelay) {
                update(frameDelay);
                accumulator -= frameDelay;
            }
            
            render();
            
            requestAnimationFrame(gameLoop);
        }

        // Start game
        function startGame() {
            gameRunning = true;
            score = 0;
            distance = 0;
            speed = 50;
            combo = 0;
            maxCombo = 0;
            nitro = 100;
            nitroActive = false;
            screenShake = 0;
            powerUpActive = null;
            powerUpTimer = 0;
            nearMissTimer = 0;
            obstacles = [];
            powerUps = [];
            trees = [];
            flagPoles = [];
            particles = [];
            speedTrails = [];
            playerCar.lane = 1;
            playerCar.x = 0;
            playerCar.targetX = getLanePosition(1, canvas.height - 150);
            playerCar.invulnerable = false;
            playerCar.invulnerableTimer = 0;
            frameCount = 0;
            raceStartTime = Date.now();
            lastTime = 0;
            accumulator = 0;
            initRoadSegments();
            initTrees();
            initFlagPoles();
            gameOverScreen.style.display = 'none';
            startScreen.style.display = 'none';
            comboElement.style.display = 'none';
            powerUpIndicator.style.display = 'none';
            speedometerElement.classList.remove('nitro');
        }

        // Game over
        function gameOver() {
            gameRunning = false;
            
            // Update high score
            if (score > highScore) {
                highScore = score;
                localStorage.setItem('highScore', highScore);
            }
            
            finalScoreElement.textContent = `Final Score: ${score}`;
            finalDistanceElement.textContent = `Distance: ${Math.floor(distance)}m`;
            finalComboElement.textContent = `Max Combo: x${maxCombo}`;
            gameOverScreen.style.display = 'block';
        }

        // Event listeners
        restartBtn.addEventListener('click', startGame);
        startBtn.addEventListener('click', startGame);

        // Initialize and start
        initRoadSegments();
        highScoreElement.textContent = `High Score: ${highScore}`;
        requestAnimationFrame(gameLoop);
    </script>
</body>
</html>