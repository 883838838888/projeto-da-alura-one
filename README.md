<!DOCTYPE html>
<html>
<head>
	<title>Jogo da Velha</title>
	<style>
		.board {
			display: flex;
			flex-wrap: wrap;
			width: 300px;
			height: 300px;
			margin: 0 auto;
			border: 1px solid black;
		}
		.square {
			width: 100px;
			height: 100px;
			border: 1px solid black;
			font-size: 72px;
			text-align: center;
			line-height: 100px;
			cursor: pointer;
		}
		.square:hover {
			background-color: #eee;
		}
	</style>
</head>
<body>
	<h1>Jogo da Velha</h1>
	<div class="board"></div>
	<script>
		// variáveis do jogo
		let currentPlayer = 'X';
		let board = ['', '', '', '', '', '', '', '', ''];
		let winningCombos = [
			[0, 1, 2],
			[3, 4, 5],
			[6, 7, 8],
			[0, 3, 6],
			[1, 4, 7],
			[2, 5, 8],
			[0, 4, 8],
			[2, 4, 6]
		];

		// função para desenhar o tabuleiro
		function drawBoard() {
			let squares = '';
			for (let i = 0; i < board.length; i++) {
				squares += `<div class="square" onclick="makeMove(${i})">${board[i]}</div>`;
			}
			document.querySelector('.board').innerHTML = squares;
		}

		// função para fazer uma jogada
		function makeMove(index) {
			if (board[index] === '') {
				board[index] = currentPlayer;
				drawBoard();
				checkForWin();
				currentPlayer = currentPlayer === 'X' ? 'O' : 'X';
			}
		}

		// função para verificar se há um vencedor
		function checkForWin() {
			for (let combo of winningCombos) {
				if (board[combo[0]] !== '' && board[combo[0]] === board[combo[1]] && board[combo[1]] === board[combo[2]]) {
					alert(`${currentPlayer} venceu!`);
					resetGame();
					return;
				}
			}
			if (board.every(square => square !== '')) {
				alert('Empate!');
				resetGame();
			}
		}

		// função para reiniciar o jogo
		function resetGame() {
			currentPlayer = 'X';
			board = ['', '', '', '', '', '', '', '', ''];
			drawBoard();
		}

		// desenha o tabuleiro inicial
		drawBoard();
	</script>
</body>
</html>
