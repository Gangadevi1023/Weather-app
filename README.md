#Tic-Tac-Toe web application 
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tic-Tac-Toe</title>
    <style>
        body {
            text-align: center;
            font-family: Arial, sans-serif;
        }
        .board {
            display: grid;
            grid-template-columns: repeat(3, 100px);
            grid-template-rows: repeat(3, 100px);
            gap: 5px;
            justify-content: center;
            margin-top: 20px;
        }
        .cell {
            width: 100px;
            height: 100px;
            display: flex;
            align-items: center;
            justify-content: center;
            border: 1px solid black;
            font-size: 2em;
            cursor: pointer;
        }
    </style>
</head>
<body>
    <h1>Tic-Tac-Toe</h1>
    <div class="board" id="board"></div>
    <p id="status"></p>
    <script>
        const board = document.getElementById("board");
        const status = document.getElementById("status");
        let cells = Array(9).fill(null);
        let currentPlayer = "X";

        function checkWinner() {
            const winningCombinations = [
                [0, 1, 2], [3, 4, 5], [6, 7, 8],
                [0, 3, 6], [1, 4, 7], [2, 5, 8],
                [0, 4, 8], [2, 4, 6]
            ];
            
            for (const combo of winningCombinations) {
                const [a, b, c] = combo;
                if (cells[a] && cells[a] === cells[b] && cells[a] === cells[c]) {
                    status.textContent = `${cells[a]} wins!`;
                    board.removeEventListener("click", handleClick);
                    return;
                }
            }
            
            if (!cells.includes(null)) {
                status.textContent = "It's a draw!";
            }
        }

        function handleClick(event) {
            const index = Array.from(board.children).indexOf(event.target);
            if (cells[index] || status.textContent) return;
            
            cells[index] = currentPlayer;
            event.target.textContent = currentPlayer;
            currentPlayer = currentPlayer === "X" ? "O" : "X";
            checkWinner();
        }

        function createBoard() {
            for (let i = 0; i < 9; i++) {
                const cell = document.createElement("div");
                cell.classList.add("cell");
                cell.addEventListener("click", handleClick);
                board.appendChild(cell);
            }
        }

        createBoard();
    </script>
</body>
</html>
