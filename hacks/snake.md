---
layout: default
title: Snake
permalink: /snake/
---

<style>
/* General body and background styling */
body {
    margin: 0;
    font-family: Arial, sans-serif;
    background-color: #D8BFD8; /* Light purple background */
    color: #fff;
    text-align: center; /* Center all content */
}

/* Canvas styling with glowing border */
canvas {
    display: none;
    border: 10px solid #FFFFFF;
    background-color: #000000;
    margin: 20px auto; /* Center the canvas horizontally */
    display: block;
    box-shadow: 0 0 20px #00ff00, 0 0 40px #00ff00; /* Glowing effect */
}

/* Enhanced UI for screens */
#menu, #gameover, #setting {
    text-align: center;
    margin: 50px auto;
    max-width: 600px;
    background: linear-gradient(135deg, rgba(0,0,0,0.8), rgba(50,50,100,0.8));
    padding: 40px;
    border-radius: 20px;
    border: 2px solid #fff;
    box-shadow: 0 0 30px rgba(255,255,255,0.5), inset 0 0 20px rgba(255,255,255,0.1);
}

#menu h3, #gameover h3, #setting h3 {
    color: #fff;
    font-size: 2.5em;
    margin-bottom: 20px;
    text-shadow: 0 0 10px #fff;
}

a {
    font-size: 20px;
    text-decoration: none;
    color: #fff;
    margin: 15px 10px;
    cursor: pointer;
    padding: 12px 25px;
    border: 2px solid #fff;
    border-radius: 25px;
    display: inline-block;
    background: linear-gradient(135deg, rgba(255,255,255,0.1), rgba(255,255,255,0.05));
    transition: all 0.3s ease;
    text-shadow: 0 0 5px #fff;
    box-shadow: 0 0 15px rgba(255,255,255,0.3);
}

a:hover {
    background: rgba(255,255,255,0.2);
    box-shadow: 0 0 25px rgba(255,255,255,0.6);
    transform: translateY(-3px);
}

/* Enhanced settings buttons */
input[type="radio"] {
    display: none;
}

label {
    cursor: pointer;
    padding: 10px 18px;
    border: 2px solid #fff;
    margin: 0 8px 10px 8px;
    display: inline-block;
    background: linear-gradient(135deg, rgba(255,255,255,0.1), rgba(255,255,255,0.05));
    color: #fff;
    border-radius: 15px;
    transition: all 0.3s ease;
    text-shadow: 0 0 5px #fff;
    box-shadow: 0 0 10px rgba(255,255,255,0.2);
}

label:hover {
    box-shadow: 0 0 20px rgba(255,255,255,0.5);
    transform: translateY(-2px);
}

input[type="radio"]:checked + label {
    background: linear-gradient(135deg, rgba(255,255,255,0.3), rgba(255,255,255,0.2));
    color: #000;
    font-weight: bold;
    box-shadow: 0 0 25px rgba(255,255,255,0.8);
}

.setting-section {
    margin: 30px 0;
    padding: 20px;
    background: rgba(255,255,255,0.05);
    border-radius: 15px;
    border: 1px solid rgba(255,255,255,0.2);
}

.setting-section p {
    font-size: 1.2em;
    font-weight: bold;
    margin-bottom: 15px;
    color: #fff;
    text-shadow: 0 0 5px #fff;
}

/* Enhanced game over stats */
.game-over-stats {
    background: rgba(255,255,255,0.1);
    border-radius: 15px;
    padding: 20px;
    margin: 25px 0;
    border: 1px solid rgba(255,255,255,0.3);
}

.high-score {
    font-size: 1.5em;
    color: #ffff00;
    text-shadow: 0 0 15px #ffff00;
    margin-top: 20px;
}

/* Footer styling */
footer {
    margin-top: 50px;
    font-size: 14px;
    color: #fff;
    text-align: center;
}

footer a {
    color: #fff;
    text-decoration: underline;
}
</style>

<h2>Snake</h2>
<div class="container">
    <header class="pb-3 mb-4 border-bottom border-primary text-dark">
        <p class="fs-4">Score: <span id="score_value">0</span></p>
    </header>
    <div class="container bg-secondary" style="text-align:center;">
        <!-- Enhanced Main Menu -->
        <div id="menu" class="py-4 text-light">
            <h3>🐍 Welcome to Snake</h3>
            <p>Press <span style="background-color: #FFFFFF; color: #000000; padding: 5px 10px; border-radius: 5px; font-weight: bold;">SPACE</span> to begin</p>
            <p style="margin: 10px 0;">Use <span style="background-color: #FFFFFF; color: #000000; padding: 3px 8px; border-radius: 3px;">Arrow Keys</span> or <span style="background-color: #FFFFFF; color: #000000; padding: 3px 8px; border-radius: 3px;">WASD</span> to move</p>
            <a id="new_game" class="link-alert">🎮 New Game</a>
            <a id="setting_menu" class="link-alert">⚙️ Settings</a>
        </div>

        <!-- Enhanced Game Over -->
        <div id="gameover" class="py-4 text-light" style="display:none;">
            <h3>💀 Game Over!</h3>
            <p>Press <span style="background-color: #FFFFFF; color: #000000; padding: 5px 10px; border-radius: 5px; font-weight: bold;">SPACE</span> to try again</p>
            
            <div class="game-over-stats">
                <p style="color: #fff; font-size: 1.1em;">🎯 Your Performance</p>
                <p style="color: #00ff00;">Final Score: <span id="final_score">0</span></p>
            </div>
            
            <a id="new_game1" class="link-alert">🎮 New Game</a>
            <a id="setting_menu1" class="link-alert">⚙️ Settings</a>
            
            <div class="high-score">
                🏆 High Score: <span id="high_score_value">0</span>
            </div>
        </div>

        <!-- Play Screen -->
        <canvas id="snake" class="wrap" width="480" height="480" tabindex="1"></canvas>

        <!-- Enhanced Settings Screen -->
        <div id="setting" class="py-4 text-light" style="display:none;">
            <h3>⚙️ Game Settings</h3>
            <p>Press <span style="background-color: #FFFFFF; color: #000000; padding: 5px 10px; border-radius: 5px; font-weight: bold;">SPACE</span> to return to game</p>
            <a id="new_game2" class="link-alert">🎮 New Game</a>
            
            <div class="setting-section">
                <p>🚀 Game Speed</p>
                <input id="speed1" type="radio" name="speed" value="120" checked/>
                <label for="speed1">🐌 Slow</label>
                <input id="speed2" type="radio" name="speed" value="75"/>
                <label for="speed2">🚶 Normal</label>
                <input id="speed3" type="radio" name="speed" value="35"/>
                <label for="speed3">⚡ Fast</label>
            </div>

            <div class="setting-section">
                <p>🧱 Wall Behavior</p>
                <input id="wallon" type="radio" name="wall" value="1" checked/>
                <label for="wallon">🔒 Solid Walls</label>
                <input id="walloff" type="radio" name="wall" value="0"/>
                <label for="walloff">🌊 Wrap Around</label>
            </div>

            <div class="setting-section">
                <p>📏 Block Size</p>
                <input id="block_small" type="radio" name="blocksize" value="10" checked/>
                <label for="block_small">🔸 Small</label>
                <input id="block_medium" type="radio" name="blocksize" value="20"/>
                <label for="block_medium">🔹 Medium</label>
                <input id="block_large" type="radio" name="blocksize" value="30"/>
                <label for="block_large">🔶 Large</label>
            </div>
        </div>
    </div>
</div>

<script>
(function () {
    /* Game Variables */
    const canvas = document.getElementById("snake");
    const ctx = canvas.getContext("2d");
    let BLOCK = 20; // Increased block size from 10 to 20 pixels
    let SCREEN;
    let snake = [];
    let snake_dir, snake_next_dir;
    let snake_speed = 120;
    let food = {
        x: 0,
        y: 0,
        image: new Image(),
        width: 512, // Set the width in pixels
        height: 512 // Set the height in pixels
    };
    let score = 0;
    let highScore = localStorage.getItem("highScore") || 0;

    /* Screen Constants */
    const SCREEN_MENU = -1, SCREEN_GAME_OVER = 1, SCREEN_SNAKE = 0, SCREEN_SETTING = 2;
    const screen_menu = document.getElementById("menu");
    const screen_game_over = document.getElementById("gameover");
    const screen_setting = document.getElementById("setting");
    const ele_score = document.getElementById("score_value");
    const ele_high_score = document.getElementById("high_score_value");

    /* Utility Functions */
    
    // Function to show/hide different game screens
    const showScreen = (screen) => {
        SCREEN = screen;
        // Hide all screens first, then show the requested one
        screen_menu.style.display = screen === SCREEN_MENU ? "block" : "none";
        screen_game_over.style.display = screen === SCREEN_GAME_OVER ? "block" : "none";
        screen_setting.style.display = screen === SCREEN_SETTING ? "block" : "none";
        canvas.style.display = screen === SCREEN_SNAKE ? "block" : "none";
    };

    // Function to randomly place food on the grid
    const addFood = () => {
        const fruitEmojis = ["🍎", "🍌", "🍉", "🍇", "🍒", "🍓", "🍍", "🥭"];
        // Calculate random position within grid boundaries
        food.x = Math.floor(Math.random() * (canvas.width / BLOCK)) * BLOCK / BLOCK;
        food.y = Math.floor(Math.random() * (canvas.height / BLOCK)) * BLOCK / BLOCK;
        // Select random fruit emoji for the food
        foodemoji = fruitEmojis[Math.floor(Math.random() * fruitEmojis.length)];
    };

    // Function to draw emojis at specific grid coordinates
    const activeDot = (x, y, emoji) => {
        ctx.font = `${BLOCK}px Arial`; // Set font size to match block size
        ctx.textAlign = "center"; // Center the emoji horizontally in the block
        ctx.textBaseline = "middle"; // Center the emoji vertically in the block
        // Draw the emoji at the center of the grid cell
        ctx.fillText(emoji, x * BLOCK + BLOCK / 2, y * BLOCK + BLOCK / 2);
    };

    // Function called when game ends
    const gameOver = () => {
        // Check if current score beats the high score
        if (score > highScore) {
            highScore = score;
            localStorage.setItem("highScore", highScore); // Save new high score to browser storage
        }
        // Update the final score display on game over screen
        document.getElementById("final_score").innerText = score;
        showScreen(SCREEN_GAME_OVER);
    };

    // Function to change block size and restart game
    const applyBlockSize = (newSize) => {
        BLOCK = newSize;
        canvas.width = 480;
        canvas.height = 480;
        addFood(); // Generate new food position
        clearTimeout(gameLoop); // Stop current game loop
        newGame(); // Restart the game with new block size
    };

    let gameLoop; // Variable to store the game loop timeout
    
    // Main game loop function - runs continuously during gameplay
    const mainLoop = () => {
        // Clear the entire canvas for the next frame
        ctx.clearRect(0, 0, canvas.width, canvas.height);

        // Draw grid lines for visual reference
        ctx.strokeStyle = "#444"; // Dark gray grid lines
        // Draw vertical grid lines
        for (let x = 0; x < canvas.width; x += BLOCK) {
            ctx.beginPath();
            ctx.moveTo(x, 0);
            ctx.lineTo(x, canvas.height);
            ctx.stroke();
        }
        // Draw horizontal grid lines
        for (let y = 0; y < canvas.height; y += BLOCK) {
            ctx.beginPath();
            ctx.moveTo(0, y);
            ctx.lineTo(canvas.width, y);
            ctx.stroke();
        }

        // Calculate snake's new head position
        let head = { ...snake[0] }; // Copy current head position
        if (snake_next_dir !== undefined) snake_dir = snake_next_dir; // Update direction if new input received

        // Move head based on current direction
        if (snake_dir === 0) head.y--; // Up
        if (snake_dir === 1) head.x++; // Right
        if (snake_dir === 2) head.y++; // Down
        if (snake_dir === 3) head.x--; // Left

        // Check for wall collisions (duplicate check - could be optimized)
        if (head.x < 0 || head.y < 0 || head.x >= canvas.width / BLOCK || head.y >= canvas.height / BLOCK) return gameOver();

        // Add new head to snake
        snake.unshift(head);

        // Handle wall collision based on wall setting
        if (wall_on) {
            // Snake hits the wall - game over
            if (head.x < 0 || head.y < 0 || head.x >= canvas.width / BLOCK || head.y >= canvas.height / BLOCK) {
                return gameOver();
            }
        } else {
            // Snake wraps around screen edges
            if (head.x < 0) head.x = canvas.width / BLOCK - 1;
            if (head.y < 0) head.y = canvas.height / BLOCK - 1;
            if (head.x >= canvas.width / BLOCK) head.x = 0;
            if (head.y >= canvas.height / BLOCK) head.y = 0;
        }

        // Check for self-collision (snake hitting its own body)
        for (let i = 1; i < snake.length; i++) {
            if (snake[i].x === head.x && snake[i].y === head.y) {
                return gameOver(); // End game if snake collides with itself
            }
        }

        // Check if snake ate food
        if (head.x === food.x && head.y === food.y) {
            score++; // Increase score
            ele_score.innerText = score; // Update score display
            addFood(); // Generate new food
            // Don't remove tail (snake grows)
        } else {
            snake.pop(); // Remove tail (snake doesn't grow)
        }

        // Draw food and snake on canvas
        activeDot(food.x, food.y, foodemoji); // Draw food
        snake.forEach(part => activeDot(part.x, part.y, "🐍")); // Draw each snake segment

        // Schedule next frame
        gameLoop = setTimeout(mainLoop, snake_speed);
    };

    // Function to start a new game
    const newGame = () => {
        showScreen(SCREEN_SNAKE); // Switch to game screen
        score = 0; // Reset score
        ele_score.innerText = score; // Update score display
        // Initialize snake at center of grid
        snake = [{ x: Math.floor(canvas.width / (2 * BLOCK)), y: Math.floor(canvas.height / (2 * BLOCK)) }];
        snake_dir = 1; // Start moving right
        snake_next_dir = undefined; // Clear any queued direction changes
        addFood(); // Place initial food
        mainLoop(); // Start game loop
    };

    /* Event Listeners */
    
    // Handle keyboard input for game controls
    window.addEventListener("keydown", (e) => {
        e.preventDefault(); // Prevent default browser behavior
        
        // Start new game if space is pressed and not currently playing
        if (e.code === "Space" && SCREEN !== SCREEN_SNAKE) newGame();
        
        // Arrow Key Controls
        if (e.code === "ArrowUp" && snake_dir !== 2) snake_next_dir = 0;    // Up (can't reverse into down)
        if (e.code === "ArrowRight" && snake_dir !== 3) snake_next_dir = 1; // Right (can't reverse into left)
        if (e.code === "ArrowDown" && snake_dir !== 0) snake_next_dir = 2;  // Down (can't reverse into up)
        if (e.code === "ArrowLeft" && snake_dir !== 1) snake_next_dir = 3;  // Left (can't reverse into right)
        
        // WASD Controls (alternative movement keys)
        if ((e.key === "w" || e.key === "W") && snake_dir !== 2) snake_next_dir = 0; // W = Up
        if ((e.key === "d" || e.key === "D") && snake_dir !== 3) snake_next_dir = 1; // D = Right
        if ((e.key === "s" || e.key === "S") && snake_dir !== 0) snake_next_dir = 2; // S = Down
        if ((e.key === "a" || e.key === "A") && snake_dir !== 1) snake_next_dir = 3; // A = Left
    });

    // Button click handlers for starting new games
    document.getElementById("new_game").onclick = newGame;   // Main menu new game button
    document.getElementById("new_game1").onclick = newGame;  // Game over new game button

    // Settings menu navigation
    document.getElementById("setting_menu").onclick = () => showScreen(SCREEN_SETTING);   // Main menu settings
    document.getElementById("setting_menu1").onclick = () => showScreen(SCREEN_SETTING);  // Game over settings

    // Speed setting handlers
    document.getElementById("speed1").onclick = () => snake_speed = 120; // Slow speed
    document.getElementById("speed2").onclick = () => snake_speed = 75;  // Normal speed
    document.getElementById("speed3").onclick = () => snake_speed = 35;  // Fast speed

    // Wall behavior setting
    let wall_on = true; // Default to walls enabled
    document.getElementById("wallon").onclick = () => wall_on = true;   // Enable walls
    document.getElementById("walloff").onclick = () => wall_on = false; // Disable walls (wrap around)

    // Block size setting handlers
    document.getElementById("block_small").onclick = () => applyBlockSize(10);  // Small blocks
    document.getElementById("block_medium").onclick = () => applyBlockSize(20); // Medium blocks  
    document.getElementById("block_large").onclick = () => applyBlockSize(30);  // Large blocks

    // Additional wall setting event listeners (redundant but kept for compatibility)
    document.getElementById("wallon").addEventListener("click", () => {
        wall_on = true;
        console.log("Wall is ON"); // Debug log
    });

    document.getElementById("walloff").addEventListener("click", () => {
        wall_on = false;
        console.log("Wall is OFF"); // Debug log
    });

    // Initialize high score display from localStorage
    ele_high_score.innerText = highScore;
})();
</script>