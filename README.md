# repository-name-1

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Tic Tac Toe</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      text-align: center;
      padding: 20px;
    }
    h1 {
      margin-bottom: 20px;
    }
    #board {
      display: grid;
      grid-template-columns: repeat(3, 100px);
      grid-template-rows: repeat(3, 100px);
      gap: 5px;
      margin: 0 auto 20px auto;
    }
    .cell {
      width: 100px;
      height: 100px;
      font-size: 3rem;
      display: flex;
      align-items: center;
      justify-content: center;
      background-color: #f0f0f0;
      cursor: pointer;
      user-select: none;
    }
    .cell:hover {
      background-color: #ddd;
    }
    #message {
      font-size: 1.2rem;
      margin-bottom: 10px;
    }
    #resetBtn {
      padding: 8px 16px;
      font-size: 1rem;
    }
  </style>
</head>
<body>
  <h1>Tic Tac Toe</h1>
  <div id="message">Player X's turn</div>
  <div id="board">
    <div class="cell" data-index="0"></div>
    <div class="cell" data-index="1"></div>
    <div class="cell" data-index="2"></div>
    <div class="cell" data-index="3"></div>
    <div class="cell" data-index="4"></div>
    <div class="cell" data-index="5"></div>
    <div class="cell" data-index="6"></div>
    <div class="cell" data-index="7"></div>
    <div class="cell" data-index="8"></div>
  </div>
  <button id="resetBtn">Reset Game</button>

  <script>
    const boardEl = document.getElementById('board');
    const messageEl = document.getElementById('message');
    const resetBtn = document.getElementById('resetBtn');
    const cells = Array.from(document.querySelectorAll('.cell'));

    let board = ['', '', '', '', '', '', '', '', ''];
    let currentPlayer = 'X';
    let gameActive = true;

    const winningCombinations = [
      [0,1,2],
      [3,4,5],
      [6,7,8],
      [0,3,6],
      [1,4,7],
      [2,5,8],
      [0,4,8],
      [2,4,6]
    ];

    function handleCellClick(e) {
      const idx = e.target.dataset.index;
      if (board[idx] !== '' || !gameActive) return;

      board[idx] = currentPlayer;
      e.target.textContent = currentPlayer;

      if (checkWin()) {
        messageEl.textContent = `Player ${currentPlayer} wins!`;
        gameActive = false;
      } else if (board.every(cell => cell !== '')) {
        messageEl.textContent = `It's a draw!`;
        gameActive = false;
      } else {
        currentPlayer = currentPlayer === 'X' ? 'O' : 'X';
        messageEl.textContent = `Player ${currentPlayer}'s turn`;
      }
    }

    function checkWin() {
      return winningCombinations.some(combination => {
        const [a,b,c] = combination;
        return board[a] && board[a] === board[b] && board[a] === board[c];
      });
    }

    function resetGame() {
      board = ['', '', '', '', '', '', '', '', ''];
      currentPlayer = 'X';
      gameActive = true;
      messageEl.textContent = `Player ${currentPlayer}'s turn`;
      cells.forEach(cell => cell.textContent = '');
    }

    cells.forEach(cell => cell.addEventListener('click', handleCellClick));
    resetBtn.addEventListener('click', resetGame);
  </script>
</body>
</html>
