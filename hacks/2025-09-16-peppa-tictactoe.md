---
title: "Welcome to Peppa Pig's Tic Tac Toe! 🐽"
comments: false
layout: default
permalink: /tictactoe
author: Akshara, Ruchika, Laya
---

<style>
    <style>
        body {
            font-family: 'Comic Sans MS', cursive, sans-serif;
            background: linear-gradient(135deg, #ff9a9e 0%, #fecfef 50%, #fecfef 100%);
            min-height: 100vh;
            margin: 0;
            padding: 20px;
        }

        .header {
            text-align: center;
            background: white;
            border-radius: 20px;
            box-shadow: 0 8px 32px rgba(0,0,0,0.1);
            padding: 30px;
            margin-bottom: 30px;
            max-width: 800px;
            margin: 0 auto 30px auto;
        }

        .header h1 {
            color: #e91e63;
            font-size: 3em;
            margin-bottom: 10px;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.1);
        }

        .authors {
            color: #666;
            font-size: 1.2em;
            margin-bottom: 20px;
        }

        .section {
            background: white;
            border-radius: 20px;
            box-shadow: 0 8px 32px rgba(0,0,0,0.1);
            padding: 30px;
            margin-bottom: 30px;
            max-width: 800px;
            margin: 0 auto 30px auto;
        }

        .section h2 {
            color: #e91e63;
            font-size: 2em;
            margin-bottom: 20px;
            border-bottom: 3px solid #ff9a9e;
            padding-bottom: 10px;
        }

        .browser-game-container {
            background: linear-gradient(135deg, #ff9a9e 0%, #fecfef 50%, #fecfef 100%);
            border-radius: 15px;
            padding: 20px;
            margin: 20px 0;
        }

        .game-container {
            background: white;
            border-radius: 15px;
            padding: 20px;
            text-align: center;
            max-width: 500px;
            margin: 0 auto;
        }

        .game-info {
            display: flex;
            justify-content: space-around;
            margin-bottom: 20px;
            padding: 15px;
            background: #f8f9fa;
            border-radius: 10px;
        }

        .player-info {
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 5px;
        }

        .player-name {
            font-weight: bold;
            color: #333;
        }

        .player-symbol {
            font-size: 2em;
        }

        .current-turn {
            background: #e3f2fd;
            border: 2px solid #2196f3;
            border-radius: 10px;
            transform: scale(1.05);
        }

        #game-board {
            display: grid;
            grid-template-columns: repeat(3, 100px);
            grid-gap: 8px;
            justify-content: center;
            margin: 20px 0;
        }

        .cell {
            width: 100px;
            height: 100px;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            border: none;
            border-radius: 15px;
            font-size: 2.5rem;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(0,0,0,0.2);
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .cell:hover:not(:disabled) {
            transform: translateY(-3px);
            box-shadow: 0 6px 20px rgba(0,0,0,0.3);
            background: linear-gradient(135deg, #764ba2 0%, #667eea 100%);
        }

        .cell:disabled {
            cursor: not-allowed;
            opacity: 0.7;
        }

        #status {
            font-size: 1.3em;
            font-weight: bold;
            color: #333;
            margin: 15px 0;
            min-height: 1.5em;
        }

        .controls {
            display: flex;
            gap: 10px;
            justify-content: center;
            margin-top: 15px;
        }

        button.control-btn {
            background: linear-gradient(135deg, #ff6b6b, #ee5a52);
            color: white;
            border: none;
            padding: 10px 20px;
            border-radius: 20px;
            font-size: 1em;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(0,0,0,0.2);
        }

        button.control-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(0,0,0,0.3);
        }

        .winner-animation {
            animation: celebration 1s ease-in-out;
        }

        @keyframes celebration {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.1); }
        }

        .code-container {
            background: #f8f9fa;
            border: 2px solid #dee2e6;
            border-radius: 10px;
            padding: 20px;
            margin: 20px 0;
            overflow-x: auto;
        }

        .code-container pre {
            color: #000000;
            font-family: 'Courier New', monospace;
            font-size: 14px;
            line-height: 1.4;
            margin: 0;
            white-space: pre-wrap;
        }

        .code-header {
            background: #6c757d;
            color: white;
            padding: 10px 20px;
            border-radius: 10px 10px 0 0;
            font-weight: bold;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .copy-btn {
            background: #4CAF50;
            color: white;
            border: none;
            padding: 5px 15px;
            border-radius: 5px;
            cursor: pointer;
            font-size: 12px;
        }

        .copy-btn:hover {
            background: #45a049;
        }

        .features-list {
            background: #f8f9fa;
            border-radius: 10px;
            padding: 20px;
            margin: 20px 0;
        }

        .features-list ul {
            margin: 0;
            padding-left: 20px;
        }

        .features-list li {
            margin-bottom: 8px;
            color: #333;
        }

        @media (max-width: 600px) {
            #game-board {
                grid-template-columns: repeat(3, 80px);
            }
            
            .cell {
                width: 80px;
                height: 80px;
                font-size: 2rem;
            }
            
            .header h1 {
                font-size: 2em;
            }
        }
    </style>
</head>
<body>
    <!-- Header Section -->
    <div class="header">
        <h1>🐷 Peppa Pig's Tic Tac Toe</h1>
        <p class="authors">Assignment by: <strong>Akshara, Ruchika, Laya</strong></p>
        <p>This assignment demonstrates both browser-based and console-based implementations of Tic Tac Toe with a fun Peppa Pig theme!</p>
    </div>

    <!-- Browser Version Section -->
    <div class="section">
        <h2>🌐 Browser Version - Play Online!</h2>
        <p>Click the squares below to play our interactive browser version:</p>
        
        <div class="browser-game-container">
            <div class="game-container">
                <h3 style="color: #e91e63; margin-top: 0;">🐷 Interactive Game</h3>
                <p style="color: #666; margin-bottom: 20px;">Play with Peppa and George!</p>
                
                <div class="game-info">
                    <div class="player-info" id="peppa-info">
                        <div class="player-name">Peppa</div>
                        <div class="player-symbol">🐷</div>
                    </div>
                    <div class="player-info" id="george-info">
                        <div class="player-name">George</div>
                        <div class="player-symbol">🦕</div>
                    </div>
                </div>
                
                <div id="game-board"></div>
                <div id="status">Peppa's turn! 🐷</div>
                
                <div class="controls">
                    <button class="control-btn" onclick="resetGame()">New Game</button>
                    <button class="control-btn" onclick="showInstructions()">How to Play</button>
                </div>
            </div>
        </div>

        <div class="features-list">
            <h4>🎨 Browser Version Features:</h4>
            <ul>
                <li>Interactive clickable game board with hover effects</li>
                <li>Visual turn indicators showing current player</li>
                <li>Animated winner celebrations and game feedback</li>
                <li>Responsive design that works on mobile devices</li>
                <li>New Game and How to Play buttons</li>
                <li>Beautiful Peppa Pig themed design with gradients</li>
            </ul>
        </div>
    </div>

    <!-- Console Version Section -->
    <div class="section">
        <h2>💻 Python Console Version</h2>
        <p>Below is our complete Python implementation that runs in the terminal:</p>
        
        <div class="code-header">
            <span>📁 peppa_tictactoe.py</span>
            <button class="copy-btn" onclick="copyCode()">Copy Code</button>
        </div>
        <div class="code-container">
            <pre id="python-code"># Tic Tac Toe - Console Version
class Player:
    def __init__(self, name, symbol):
        self.name = name
        self.symbol = symbol

class Board:
    def __init__(self):
        self.grid = [" "] * 9

    def display(self):
        print("\n")
        print(" " + self.grid[0] + " | " + self.grid[1] + " | " + self.grid[2])
        print("---+---+---")
        print(" " + self.grid[3] + " | " + self.grid[4] + " | " + self.grid[5])
        print("---+---+---")
        print(" " + self.grid[6] + " | " + self.grid[7] + " | " + self.grid[8])
        print("\n")

    def display_reference(self):
        reference = ["1","2","3","4","5","6","7","8","9"]
        print("Board positions:\n")
        print(" " + reference[0] + " | " + reference[1] + " | " + reference[2])
        print("---+---+---")
        print(" " + reference[3] + " | " + reference[4] + " | " + reference[5])
        print("---+---+---")
        print(" " + reference[6] + " | " + reference[7] + " | " + reference[8])
        print("\n")

    def is_full(self):
        return " " not in self.grid

    def make_move(self, position, symbol):
        index = position - 1
        if index < 0 or index > 8:
            print("Invalid position. Choose a number between 1 and 9.")
            return False
        if self.grid[index] != " ":
            print("That spot is already taken. Try again.")
            return False
        self.grid[index] = symbol
        return True

    def check_winner(self, symbol):
        win_combinations = [
            [0,1,2],[3,4,5],[6,7,8],
            [0,3,6],[1,4,7],[2,5,8],
            [0,4,8],[2,4,6]
        ]
        for combo in win_combinations:
            if (self.grid[combo[0]]==symbol and
                self.grid[combo[1]]==symbol and
                self.grid[combo[2]]==symbol):
                return True
        return False

class TicTacToe:
    def __init__(self, player1, player2):
        self.board = Board()
        self.players = [player1, player2]
        self.current_player = player1

    def switch_player(self):
        self.current_player = (
            self.players[1] if self.current_player == self.players[0] else self.players[0]
        )

    def play(self):
        print("Welcome to Peppa Pig Tic Tac Toe! 🐷")
        print(f"{self.players[0].name} is '{self.players[0].symbol}'")
        print(f"{self.players[1].name} is '{self.players[1].symbol}'")
        self.board.display_reference()
        self.board.display()

        while True:
            try:
                move = int(input(f"{self.current_player.name} ({self.current_player.symbol}), enter your move (1-9): "))
            except ValueError:
                print("Invalid input. Enter 1-9.")
                continue

            if not self.board.make_move(move, self.current_player.symbol):
                continue

            self.board.display()

            if self.board.check_winner(self.current_player.symbol):
                print(f"🎉 {self.current_player.name} wins! 🎉")
                break

            if self.board.is_full():
                print("It's a tie! Good game! 🤝")
                break

            self.switch_player()

        # Ask if they want to play again
        play_again = input("\nWould you like to play again? (y/n): ").lower().strip()
        if play_again == 'y' or play_again == 'yes':
            # Reset the board and start new game
            self.board = Board()
            self.current_player = self.players[0]  # Peppa starts again
            self.play()
        else:
            print("Thanks for playing Peppa Pig Tic Tac Toe! Goodbye! 👋")

# Main game execution
if __name__ == "__main__":
    print("🐷 Welcome to Peppa Pig's Tic Tac Toe Adventure! 🐷")
    print("=" * 50)
    
    # Create players
    player1 = Player("Peppa", "🐷")
    player2 = Player("George", "🦕")  # Using dinosaur emoji for George
    
    # Start the game
    game = TicTacToe(player1, player2)
    game.play()</pre>
        </div>

        <div class="features-list">
            <h4>🐍 Console Version Features:</h4>
            <ul>
                <li>Object-oriented design with Player, Board, and TicTacToe classes</li>
                <li>Input validation and error handling</li>
                <li>Clear board display with position reference guide</li>
                <li>Play again functionality for multiple games</li>
                <li>Win detection for all possible combinations</li>
                <li>Peppa Pig themed with fun emojis (🐷 and 🦕)</li>
            </ul>
        </div>

        <div style="background: #e8f5e8; border-radius: 10px; padding: 15px; margin: 20px 0;">
            <h4 style="color: #2e7d2e; margin-top: 0;">🚀 How to Run the Python Version:</h4>
            <ol style="color: #2e7d2e; margin: 0;">
                <li>Copy the code above and save it as <code>peppa_tictactoe.py</code></li>
                <li>Open your terminal/command prompt</li>
                <li>Navigate to the file location</li>
                <li>Run: <code>python peppa_tictactoe.py</code></li>
                <li>Follow the on-screen prompts to play!</li>
            </ol>
        </div>
    </div>

    <!-- Assignment Summary -->
    <div class="section">
        <h2>📋 Assignment Summary</h2>
        <p>This project demonstrates our understanding of:</p>
        <div class="features-list">
            <ul>
                <li><strong>Object-Oriented Programming:</strong> Classes, methods, and encapsulation in Python</li>
                <li><strong>Web Development:</strong> HTML, CSS, and JavaScript for interactive web applications</li>
                <li><strong>Game Logic:</strong> Win detection, turn management, and input validation</li>
                <li><strong>User Experience:</strong> Visual feedback, animations, and responsive design</li>
                <li><strong>Code Organization:</strong> Clean, readable, and well-commented code</li>
                <li><strong>Creative Theming:</strong> Fun Peppa Pig theme to engage users</li>
            </ul>
        </div>
        
        <p style="text-align: center; color: #666; margin-top: 30px;">
            <em>Both versions are fully functional and demonstrate different programming paradigms working together!</em>
        </p>
    </div>

    <!-- Changes Made Section -->
    <div class="section">
        <h2>🎯 Changes Made from Typical Tic Tac Toe</h2>
        <p>Here are the unique features we added to make our Tic Tac Toe special:</p>
        
        <div class="features-list">
            <h4>🐷 Peppa Pig Theme:</h4>
            <ul>
                <li><strong>Custom Characters:</strong> Peppa (🐷) and George (🦕) instead of X and O</li>
                <li><strong>Fun Messaging:</strong> "Welcome to Peppa Pig Tic Tac Toe!" and character-specific win messages</li>
                <li><strong>Themed Colors:</strong> Pink and purple gradients matching Peppa Pig's world</li>
                <li><strong>Child-Friendly Design:</strong> Comic Sans font and rounded corners for a playful feel</li>
            </ul>
        </div>

        <div class="features-list">
            <h4>🌐 Enhanced Browser Features:</h4>
            <ul>
                <li><strong>Visual Turn Indicators:</strong> Player info boxes highlight whose turn it is</li>
                <li><strong>Hover Effects:</strong> Buttons lift up when you hover over them</li>
                <li><strong>Click Animations:</strong> Pieces scale down then up when placed</li>
                <li><strong>Winner Celebrations:</strong> Bouncing animation when someone wins</li>
                <li><strong>Responsive Design:</strong> Game scales down for mobile devices</li>
                <li><strong>Control Buttons:</strong> New Game and How to Play buttons for better UX</li>
            </ul>
        </div>

        <div class="features-list">
            <h4>💻 Enhanced Console Features:</h4>
            <ul>
                <li><strong>Play Again Functionality:</strong> Ask players if they want another round</li>
                <li><strong>Position Reference:</strong> Show numbered grid before game starts</li>
                <li><strong>Better Input Validation:</strong> Handle invalid inputs gracefully</li>
                <li><strong>Emoji Integration:</strong> Fun emojis in console output for celebrations</li>
                <li><strong>Object-Oriented Design:</strong> Clean separation with Player, Board, and Game classes</li>
                <li><strong>Enhanced Messaging:</strong> Clear game flow with welcome messages and goodbye</li>
            </ul>
        </div>

        <div class="features-list">
            <h4>🚀 Technical Improvements:</h4>
            <ul>
                <li><strong>Code Organization:</strong> Well-structured classes and functions</li>
                <li><strong>Error Handling:</strong> Robust input validation and edge case management</li>
                <li><strong>Modern Web Features:</strong> CSS Grid, Flexbox, and CSS animations</li>
                <li><strong>Accessibility:</strong> Proper semantic HTML and keyboard support</li>
                <li><strong>Cross-Platform:</strong> Works on desktop, mobile, and in terminal</li>
                <li><strong>Local Storage:</strong> Could be extended to save high scores (foundation ready)</li>
            </ul>
        </div>

        <div style="background: linear-gradient(135deg, #ff9a9e 0%, #fecfef 100%); border-radius: 15px; padding: 20px; margin: 20px 0; text-align: center;">
            <h4 style="color: #e91e63; margin-top: 0;">✨ What Makes This Special</h4>
            <p style="color: #333; font-size: 1.1em; margin: 0;">
                Unlike typical Tic Tac Toe games that use simple X's and O's, our version creates an 
                <strong>immersive Peppa Pig experience</strong> that's both educational and entertaining. 
                We've combined solid programming fundamentals with creative design to make learning fun!
            </p>
        </div>
    </div>

    <script>
        let board = Array(9).fill("");
        let currentPlayer = "🐷"; // Peppa starts
        let gameActive = true;
        let gameBoard = document.getElementById("game-board");
        let status = document.getElementById("status");

        const players = {
            "🐷": "Peppa",
            "🦕": "George"
        };

        function initializeBoard() {
            gameBoard.innerHTML = "";
            for (let i = 0; i < 9; i++) {
                const cell = document.createElement("button");
                cell.className = "cell";
                cell.setAttribute("data-index", i);
                cell.addEventListener("click", () => makeMove(i));
                gameBoard.appendChild(cell);
            }
            updateTurnIndicator();
        }

        function updateTurnIndicator() {
            const peppaInfo = document.getElementById("peppa-info");
            const georgeInfo = document.getElementById("george-info");
            
            peppaInfo.classList.remove("current-turn");
            georgeInfo.classList.remove("current-turn");
            
            if (currentPlayer === "🐷") {
                peppaInfo.classList.add("current-turn");
            } else {
                georgeInfo.classList.add("current-turn");
            }
        }

        function makeMove(index) {
            if (board[index] !== "" || !gameActive) {
                return;
            }

            board[index] = currentPlayer;
            const cell = document.querySelector(`[data-index="${index}"]`);
            cell.textContent = currentPlayer;
            cell.disabled = true;

            // Add a little animation
            cell.style.transform = "scale(0.8)";
            setTimeout(() => {
                cell.style.transform = "scale(1)";
            }, 150);

            if (checkWinner(currentPlayer)) {
                status.textContent = `🎉 ${players[currentPlayer]} wins! 🎉`;
                status.classList.add("winner-animation");
                gameActive = false;
                disableAllCells();
                
                // Remove turn indicators
                document.getElementById("peppa-info").classList.remove("current-turn");
                document.getElementById("george-info").classList.remove("current-turn");
                
                setTimeout(() => {
                    status.classList.remove("winner-animation");
                }, 1000);
            } else if (board.every(cell => cell !== "")) {
                status.textContent = "It's a tie! Good game! 🤝";
                gameActive = false;
                
                // Remove turn indicators
                document.getElementById("peppa-info").classList.remove("current-turn");
                document.getElementById("george-info").classList.remove("current-turn");
            } else {
                currentPlayer = currentPlayer === "🐷" ? "🦕" : "🐷";
                status.textContent = `${players[currentPlayer]}'s turn! ${currentPlayer}`;
                updateTurnIndicator();
            }
        }

        function checkWinner(symbol) {
            const winPatterns = [
                [0, 1, 2], [3, 4, 5], [6, 7, 8], // Rows
                [0, 3, 6], [1, 4, 7], [2, 5, 8], // Columns
                [0, 4, 8], [2, 4, 6] // Diagonals
            ];

            return winPatterns.some(pattern => 
                pattern.every(index => board[index] === symbol)
            );
        }

        function disableAllCells() {
            const cells = document.querySelectorAll(".cell");
            cells.forEach(cell => cell.disabled = true);
        }

        function resetGame() {
            board = Array(9).fill("");
            currentPlayer = "🐷";
            gameActive = true;
            status.textContent = "Peppa's turn! 🐷";
            status.classList.remove("winner-animation", "game-over");
            initializeBoard();
        }

        function showInstructions() {
            alert(`🐷 How to Play Peppa Pig's Tic Tac Toe:

1. Players take turns placing their symbol
2. Peppa (🐷) goes first, then George (🦕)
3. Get 3 in a row (horizontal, vertical, or diagonal) to win!
4. If all 9 spaces are filled with no winner, it's a tie

Click on any empty square to make your move!`);
        }

        function copyCode() {
            const codeElement = document.getElementById("python-code");
            const textArea = document.createElement("textarea");
            textArea.value = codeElement.textContent;
            document.body.appendChild(textArea);
            textArea.select();
            document.execCommand("copy");
            document.body.removeChild(textArea);
            
            const copyBtn = document.querySelector(".copy-btn");
            const originalText = copyBtn.textContent;
            copyBtn.textContent = "Copied! ✓";
            copyBtn.style.background = "#4CAF50";
            
            setTimeout(() => {
                copyBtn.textContent = originalText;
                copyBtn.style.background = "#4CAF50";
            }, 2000);
        }

        // Initialize the game when page loads
        initializeBoard();
    </script>