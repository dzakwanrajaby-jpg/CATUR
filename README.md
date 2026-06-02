<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes, maximum-scale=1.5">
  <title>♟️ Catur Dzakwan • Arahkan Langkah</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      background: linear-gradient(145deg, #2e5f3e 0%, #1e3b28 100%);
      min-height: 100vh;
      display: flex;
      justify-content: center;
      align-items: center;
      font-family: 'Segoe UI', 'Roboto', system-ui, sans-serif;
      padding: 20px;
      margin: 0;
    }

    .game-container {
      background: #deb887;
      background-image: radial-gradient(circle at 20% 30%, #f3e1c4, #c8a27a);
      border-radius: 48px;
      box-shadow: 0 30px 50px rgba(0, 0, 0, 0.6), inset 0 2px 8px rgba(255, 255, 200, 0.7);
      padding: 28px 30px 35px;
      display: flex;
      flex-direction: column;
      align-items: center;
      border: 2px solid #b8875b;
    }

    h1 {
      font-size: 2.4rem;
      font-weight: 700;
      color: #2d2416;
      text-shadow: 2px 2px 0 #e7c594;
      margin-bottom: 10px;
      letter-spacing: 2px;
      display: flex;
      align-items: center;
      gap: 12px;
    }
    h1 span {
      background: #fae5c2;
      padding: 5px 20px;
      border-radius: 40px;
      font-size: 1.9rem;
      box-shadow: inset 0 -4px 0 #b29263;
      color: #3b2b15;
    }

    canvas {
      display: block;
      border-radius: 32px;
      box-shadow: 0 20px 30px rgba(0, 0, 0, 0.7), inset 0 0 0 4px #6b4f32;
      background: #e8d5b0;
      width: min(100%, 480px);
      height: auto;
      aspect-ratio: 1 / 1;
      margin: 5px 0 20px;
    }

    .panel-kontrol {
      display: flex;
      flex-wrap: wrap;
      align-items: center;
      justify-content: center;
      gap: 25px;
      margin-top: 5px;
    }

    .tombol-arah {
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 8px;
      background: #6f4e37;
      padding: 14px 16px;
      border-radius: 60px;
      box-shadow: inset 0 -6px 0 #3f2a1b, 0 8px 12px rgba(0,0,0,0.5);
    }

    .baris-arah {
      display: flex;
      gap: 18px;
      justify-content: center;
    }

    .btn-arrow {
      background: #f3e0be;
      border: none;
      font-size: 2.4rem;
      width: 55px;
      height: 55px;
      border-radius: 30px;
      display: flex;
      align-items: center;
      justify-content: center;
      cursor: pointer;
      box-shadow: 0 5px 0 #7b5e3b, 0 8px 12px black;
      color: #3e2c18;
      transition: all 0.08s ease;
      font-weight: bold;
      background: radial-gradient(circle at 30% 30%, #ffefcc, #d6aa6c);
      border: 1px solid #ffe3aa;
      user-select: none;
    }

    .btn-arrow:active {
      transform: translateY(4px);
      box-shadow: 0 2px 0 #5a3e28, 0 5px 8px black;
      background: #ebc07a;
    }

    .info-giliran {
      background: #2d2412;
      color: #ffdead;
      padding: 12px 28px;
      border-radius: 40px;
      font-weight: bold;
      font-size: 1.3rem;
      letter-spacing: 1px;
      box-shadow: inset 0 -4px 0 #5e4a31, 0 8px 10px rgba(0,0,0,0.5);
      display: flex;
      align-items: center;
      gap: 10px;
    }

    .reset-btn {
      background: #c79a6e;
      border: none;
      font-size: 1.3rem;
      font-weight: bold;
      color: #241e12;
      padding: 12px 24px;
      border-radius: 3rem;
      cursor: pointer;
      box-shadow: 0 5px 0 #6b4c34, 0 5px 15px black;
      background: radial-gradient(circle at 20% 30%, #edd3b0, #b37b52);
      transition: 0.08s ease;
      display: flex;
      align-items: center;
      gap: 6px;
      letter-spacing: 0.8px;
    }

    .reset-btn:active {
      transform: translateY(4px);
      box-shadow: 0 2px 0 #5a3b24, 0 5px 10px black;
    }

    .status-text {
      color: #ffd78b;
      font-weight: 600;
    }

    @media (max-width: 500px) {
      .btn-arrow {
        width: 45px;
        height: 45px;
        font-size: 2rem;
      }
      .game-container {
        padding: 15px;
      }
    }
  </style>
</head>
<body>
<div style="display: flex; flex-direction: column; align-items: center;">
  <div class="game-container">
    <h1>
      ♞ <span>DZAKWAN</span> ♞
    </h1>
    <canvas id="papanCatur" width="480" height="480"></canvas>
    
    <div class="panel-kontrol">
      <div class="tombol-arah">
        <div class="baris-arah">
          <button class="btn-arrow" id="arahAtas">⬆️</button>
        </div>
        <div class="baris-arah">
          <button class="btn-arrow" id="arahKiri">⬅️</button>
          <button class="btn-arrow" id="arahBawah">⬇️</button>
          <button class="btn-arrow" id="arahKanan">➡️</button>
        </div>
        <div style="font-size:0.9rem; color:#ffddb0; margin-top:4px;">geser kursor</div>
      </div>
      
      <div class="info-giliran">
        <span id="giliranDisplay">🤍 Giliran Dzakwan (putih)</span>
      </div>
      
      <button class="reset-btn" id="resetGame">
        🔄 Ulang Partai
      </button>
    </div>
    <div style="margin-top: 8px; color: #34200c; font-weight: 500;">
      ⚡ Pilih buah putih lalu arahkan dengan tombol
    </div>
  </div>
</div>

<script>
  (function() {
    const canvas = document.getElementById('papanCatur');
    const ctx = canvas.getContext('2d');

    // Status game
    let board = [];
    let selectedRow = -1, selectedCol = -1; // baris & kolom terpilih (0-7)
    let currentPlayer = 'white'; // putih = Dzakwan (manusia), hitam = AI
    let gameOver = false;
    let winnerMessage = '';

    // Inisialisasi papan
    function initBoard() {
      board = [
        ['r', 'n', 'b', 'q', 'k', 'b', 'n', 'r'], // hitam (baris 0)
        ['p', 'p', 'p', 'p', 'p', 'p', 'p', 'p'],
        [null, null, null, null, null, null, null, null],
        [null, null, null, null, null, null, null, null],
        [null, null, null, null, null, null, null, null],
        [null, null, null, null, null, null, null, null],
        ['P', 'P', 'P', 'P', 'P', 'P', 'P', 'P'], // putih (baris 6)
        ['R', 'N', 'B', 'Q', 'K', 'B', 'N', 'R']  // putih (baris 7)
      ];
      selectedRow = -1;
      selectedCol = -1;
      currentPlayer = 'white';
      gameOver = false;
      winnerMessage = '';
    }

    // Peta unicode buah
    const pieceUnicode = {
      'r': '♜', 'n': '♞', 'b': '♝', 'q': '♛', 'k': '♚', 'p': '♟',
      'R': '♖', 'N': '♘', 'B': '♗', 'Q': '♕', 'K': '♔', 'P': '♙'
    };

    function getPieceColor(piece) {
      if (!piece) return null;
      return piece === piece.toUpperCase() ? 'white' : 'black';
    }

    // Cek dalam bounds
    function isValidCell(row, col) {
      return row >= 0 && row < 8 && col >= 0 && col < 8;
    }

    // Cek langkah valid dasar (tanpa cek skak, akan ditambah filter)
    function isMoveValidBasic(fromRow, fromCol, toRow, toCol, piece, boardState) {
      const targetPiece = boardState[toRow][toCol];
      if (targetPiece && getPieceColor(targetPiece) === getPieceColor(piece)) {
        return false; // tidak bisa makan teman
      }

      const type = piece.toLowerCase();
      const color = getPieceColor(piece);
      const dRow = toRow - fromRow;
      const dCol = toCol - fromCol;
      const absDrow = Math.abs(dRow);
      const absDcol = Math.abs(dCol);

      // Pion
      if (type === 'p') {
        const direction = color === 'white' ? -1 : 1; // putih naik (baris turun), hitam turun
        const startRow = color === 'white' ? 6 : 1;
        
        if (dCol === 0 && !targetPiece) {
          if (dRow === direction) return true;
          if (dRow === 2 * direction && fromRow === startRow && !boardState[fromRow + direction][fromCol] && !targetPiece) {
            return true;
          }
        } else if (absDcol === 1 && dRow === direction && targetPiece && getPieceColor(targetPiece) !== color) {
          return true; // makan diagonal
        }
        return false;
      }

      // Gajah / bishop
      if (type === 'b') {
        if (absDrow !== absDcol || absDrow === 0) return false;
        const stepRow = dRow > 0 ? 1 : -1;
        const stepCol = dCol > 0 ? 1 : -1;
        let r = fromRow + stepRow, c = fromCol + stepCol;
        while (r !== toRow && c !== toCol) {
          if (boardState[r][c] !== null) return false;
          r += stepRow;
          c += stepCol;
        }
        return true;
      }

      // Kuda
      if (type === 'n') {
        return (absDrow === 2 && absDcol === 1) || (absDrow === 1 && absDcol === 2);
      }

      // Benteng
      if (type === 'r') {
        if (dRow !== 0 && dCol !== 0) return false;
        const stepRow = dRow === 0 ? 0 : (dRow > 0 ? 1 : -1);
        const stepCol = dCol === 0 ? 0 : (dCol > 0 ? 1 : -1);
        let r = fromRow + stepRow, c = fromCol + stepCol;
        while (r !== toRow || c !== toCol) {
          if (boardState[r][c] !== null) return false;
          r += stepRow;
          c += stepCol;
        }
        return true;
      }

      // Ratu
      if (type === 'q') {
        if (dRow === 0 || dCol === 0) {
          const stepRow = dRow === 0 ? 0 : (dRow > 0 ? 1 : -1);
          const stepCol = dCol === 0 ? 0 : (dCol > 0 ? 1 : -1);
          let r = fromRow + stepRow, c = fromCol + stepCol;
          while (r !== toRow || c !== toCol) {
            if (boardState[r][c] !== null) return false;
            r += stepRow;
            c += stepCol;
          }
          return true;
        } else if (absDrow === absDcol) {
          const stepRow = dRow > 0 ? 1 : -1;
          const stepCol = dCol > 0 ? 1 : -1;
          let r = fromRow + stepRow, c = fromCol + stepCol;
          while (r !== toRow && c !== toCol) {
            if (boardState[r][c] !== null) return false;
            r += stepRow;
            c += stepCol;
          }
          return true;
        }
        return false;
      }

      // Raja
      if (type === 'k') {
        return absDrow <= 1 && absDcol <= 1 && (absDrow !== 0 || absDcol !== 0);
      }

      return false;
    }

    // Cari posisi raja warna tertentu
    function findKing(boardState, color) {
      const kingChar = color === 'white' ? 'K' : 'k';
      for (let r = 0; r < 8; r++) {
        for (let c = 0; c < 8; c++) {
          if (boardState[r][c] === kingChar) return { row: r, col: c };
        }
      }
      return null;
    }

    // Cek apakah raja warna tertentu dalam skak
    function isKingInCheck(boardState, color) {
      const kingPos = findKing(boardState, color);
      if (!kingPos) return true; // raja hilang (harusnya tidak terjadi)
      const opponentColor = color === 'white' ? 'black' : 'white';
      for (let r = 0; r < 8; r++) {
        for (let c = 0; c < 8; c++) {
          const piece = boardState[r][c];
          if (piece && getPieceColor(piece) === opponentColor) {
            if (isMoveValidBasic(r, c, kingPos.row, kingPos.col, piece, boardState)) {
              return true;
            }
          }
        }
      }
      return false;
    }

    // Cek langkah legal penuh (tidak menyebabkan raja sendiri skak)
    function isMoveLegal(fromRow, fromCol, toRow, toCol, boardState, playerColor) {
      const piece = boardState[fromRow][fromCol];
      if (!piece || getPieceColor(piece) !== playerColor) return false;
      if (!isMoveValidBasic(fromRow, fromCol, toRow, toCol, piece, boardState)) return false;

      // Simulasikan langkah
      const newBoard = boardState.map(row => [...row]);
      newBoard[toRow][toCol] = piece;
      newBoard[fromRow][fromCol] = null;
      return !isKingInCheck(newBoard, playerColor);
    }

    // Dapatkan semua langkah legal untuk pemain
    function getAllLegalMoves(boardState, playerColor) {
      const moves = [];
      for (let r = 0; r < 8; r++) {
        for (let c = 0; c < 8; c++) {
          const piece = boardState[r][c];
          if (piece && getPieceColor(piece) === playerColor) {
            for (let tr = 0; tr < 8; tr++) {
              for (let tc = 0; tc < 8; tc++) {
                if (isMoveLegal(r, c, tr, tc, boardState, playerColor)) {
                  moves.push({ fromRow: r, fromCol: c, toRow: tr, toCol: tc });
                }
              }
            }
          }
        }
      }
      return moves;
    }

    // Cek skakmat atau stalemate
    function checkGameEnd() {
      const moves = getAllLegalMoves(board, currentPlayer);
      if (moves.length === 0) {
        gameOver = true;
        if (isKingInCheck(board, currentPlayer)) {
          winnerMessage = currentPlayer === 'white' ? 'Hitam menang! Dzakwan kalah.' : 'Dzakwan (Putih) menang!';
        } else {
          winnerMessage = 'Stalemate! Remis.';
        }
        return true;
      }
      return false;
    }

    // Eksekusi langkah
    function makeMove(fromRow, fromCol, toRow, toCol) {
      const piece = board[fromRow][fromCol];
      board[toRow][toCol] = piece;
      board[fromRow][fromCol] = null;
      
      // Promosi pion (otomatis jadi ratu)
      if (piece.toLowerCase() === 'p') {
        const color = getPieceColor(piece);
        if ((color === 'white' && toRow === 0) || (color === 'black' && toRow === 7)) {
          board[toRow][toCol] = color === 'white' ? 'Q' : 'q';
        }
      }
    }

    // Giliran AI (hitam) dengan langkah acak sederhana
    function aiMove() {
      if (gameOver || currentPlayer !== 'black') return;
      const moves = getAllLegalMoves(board, 'black');
      if (moves.length === 0) {
        checkGameEnd();
        drawBoard();
        return;
      }
      // Pilih acak
      const randomMove = moves[Math.floor(Math.random() * moves.length)];
      makeMove(randomMove.fromRow, randomMove.fromCol, randomMove.toRow, randomMove.toCol);
      
      selectedRow = -1;
      selectedCol = -1;
      currentPlayer = 'white';
      
      if (!checkGameEnd()) {
        drawBoard();
        updateGiliranDisplay();
      } else {
        drawBoard();
        updateGiliranDisplay();
      }
    }

    // Coba lakukan langkah putih
    function attemptMoveWhite(toRow, toCol) {
      if (gameOver || currentPlayer !== 'white') return false;
      if (selectedRow === -1 || selectedCol === -1) return false;
      
      const piece = board[selectedRow][selectedCol];
      if (!piece || getPieceColor(piece) !== 'white') {
        // Jika tidak valid, bersihkan seleksi
        selectedRow = -1;
        selectedCol = -1;
        drawBoard();
        return false;
      }

      if (isMoveLegal(selectedRow, selectedCol, toRow, toCol, board, 'white')) {
        makeMove(selectedRow, selectedCol, toRow, toCol);
        selectedRow = -1;
        selectedCol = -1;
        currentPlayer = 'black';
        drawBoard();
        updateGiliranDisplay();
        
        if (!checkGameEnd()) {
          // Beri sedikit jeda sebelum AI jalan
          setTimeout(() => {
            if (currentPlayer === 'black' && !gameOver) {
              aiMove();
            }
          }, 80);
        } else {
          drawBoard();
          updateGiliranDisplay();
        }
        return true;
      } else {
        // Langkah ilegal: batalkan seleksi
        selectedRow = -1;
        selectedCol = -1;
        drawBoard();
        return false;
      }
    }

    // Gerakan kursor dengan tombol arah
    function moveSelection(dRow, dCol) {
      if (gameOver || currentPlayer !== 'white') {
        // Jika bukan giliran putih, abaikan atau bersihkan seleksi
        if (currentPlayer !== 'white') {
          selectedRow = -1;
          selectedCol = -1;
          drawBoard();
        }
        return;
      }

      // Jika belum ada yang dipilih, mulai dari posisi awal (default di tengah atau dekat)
      if (selectedRow === -1 || selectedCol === -1) {
        // Inisialisasi kursor ke petak yang ada buah putih, atau default (6,4)
        let found = false;
        for (let r = 0; r < 8; r++) {
          for (let c = 0; c < 8; c++) {
            if (board[r][c] && getPieceColor(board[r][c]) === 'white') {
              selectedRow = r;
              selectedCol = c;
              found = true;
              break;
            }
          }
          if (found) break;
        }
        if (!found) {
          selectedRow = 6;
          selectedCol = 4;
        }
        drawBoard();
        return;
      }

      // Coba pindah ke target langsung? Jika target adalah buah putih, pindah seleksi.
      const newRow = selectedRow + dRow;
      const newCol = selectedCol + dCol;
      if (!isValidCell(newRow, newCol)) return;

      const targetPiece = board[newRow][newCol];
      
      // Jika target adalah buah putih (temannya), pindahkan kursor ke buah itu
      if (targetPiece && getPieceColor(targetPiece) === 'white') {
        selectedRow = newRow;
        selectedCol = newCol;
        drawBoard();
        return;
      }
      
      // Jika target kosong atau buah hitam, artinya kita ingin mencoba langkah ke sana
      if (selectedRow !== -1 && selectedCol !== -1) {
        const moveSuccess = attemptMoveWhite(newRow, newCol);
        if (!moveSuccess) {
          // Jika gagal, kursor tetap di posisi lama (tetap terseleksi)
          drawBoard();
        }
        // jika berhasil, attemptMoveWhite sudah mengurus state
      } else {
        drawBoard();
      }
    }

    // Gambar papan
    function drawBoard() {
      ctx.clearRect(0, 0, 480, 480);
      const squareSize = 60;
      
      // Gambar petak
      for (let r = 0; r < 8; r++) {
        for (let c = 0; c < 8; c++) {
          const x = c * squareSize;
          const y = r * squareSize;
          const isLight = (r + c) % 2 === 0;
          ctx.fillStyle = isLight ? '#f0d9b5' : '#b58863';
          ctx.fillRect(x, y, squareSize, squareSize);
          
          // Highlight seleksi
          if (selectedRow === r && selectedCol === c && !gameOver && currentPlayer === 'white') {
            ctx.fillStyle = 'rgba(255, 235, 120, 0.65)';
            ctx.fillRect(x, y, squareSize, squareSize);
            ctx.strokeStyle = '#f5e56c';
            ctx.lineWidth = 3.5;
            ctx.strokeRect(x+2, y+2, squareSize-5, squareSize-5);
          }
        }
      }

      // Gambar buah
      ctx.font = 'bold 44px "Segoe UI Symbol", "Arial Unicode MS", sans-serif';
      ctx.textAlign = 'center';
      ctx.textBaseline = 'middle';
      for (let r = 0; r < 8; r++) {
        for (let c = 0; c < 8; c++) {
          const piece = board[r][c];
          if (piece) {
            const x = c * squareSize + squareSize/2;
            const y = r * squareSize + squareSize/2;
            ctx.fillStyle = getPieceColor(piece) === 'white' ? '#2b2b2b' : '#1e1e1e';
            ctx.shadowColor = '#ffffff90';
            ctx.shadowBlur = 6;
            ctx.fillText(pieceUnicode[piece], x, y-1);
            ctx.shadowColor = 'transparent';
            ctx.shadowBlur = 0;
            // outline kecil
            ctx.fillStyle = getPieceColor(piece) === 'white' ? '#faf9f6' : '#3a3a3a';
            ctx.fillText(pieceUnicode[piece], x-0.8, y-1.2);
            ctx.fillStyle = getPieceColor(piece) === 'white' ? '#222' : '#0a0a0a';
            ctx.fillText(pieceUnicode[piece], x, y);
          }
        }
      }
      
      if (gameOver) {
        ctx.globalAlpha = 0.8;
        ctx.fillStyle = '#1e2b1a';
        ctx.fillRect(0, 180, 480, 80);
        ctx.globalAlpha = 1;
        ctx.font = 'bold 22px "Segoe UI"';
        ctx.fillStyle = '#ffd78b';
        ctx.fillText(winnerMessage, 240, 225);
      }
    }

    function updateGiliranDisplay() {
      const display = document.getElementById('giliranDisplay');
      if (gameOver) {
        display.innerHTML = '🏁 ' + winnerMessage;
      } else {
        display.innerHTML = currentPlayer === 'white' ? '🤍 Giliran Dzakwan (putih)' : '🖤 Giliran Hitam (AI)';
      }
    }

    function resetGame() {
      initBoard();
      drawBoard();
      updateGiliranDisplay();
    }

    // Event klik pada canvas (sebagai alternatif sentuh)
    canvas.addEventListener('click', (e) => {
      if (gameOver || currentPlayer !== 'white') return;
      const rect = canvas.getBoundingClientRect();
      const scaleX = canvas.width / rect.width;   // faktor skala
      const scaleY = canvas.height / rect.height;
      const mouseX = (e.clientX - rect.left) * scaleX;
      const mouseY = (e.clientY - rect.top) * scaleY;
      const col = Math.floor(mouseX / 60);
      const row = Math.floor(mouseY / 60);
      if (!isValidCell(row, col)) return;
      
      const piece = board[row][col];
      if (selectedRow === -1) {
        if (piece && getPieceColor(piece) === 'white') {
          selectedRow = row;
          selectedCol = col;
          drawBoard();
        }
      } else {
        if (piece && getPieceColor(piece) === 'white') {
          selectedRow = row;
          selectedCol = col;
          drawBoard();
        } else {
          attemptMoveWhite(row, col);
        }
      }
    });

    // Tombol arah
    document.getElementById('arahAtas').addEventListener('click', () => moveSelection(-1, 0));
    document.getElementById('arahBawah').addEventListener('click', () => moveSelection(1, 0));
    document.getElementById('arahKiri').addEventListener('click', () => moveSelection(0, -1));
    document.getElementById('arahKanan').addEventListener('click', () => moveSelection(0, 1));
    document.getElementById('resetGame').addEventListener('click', resetGame);

    // Mulai
    initBoard();
    drawBoard();
    updateGiliranDisplay();
  })();
</script>
</body>
</html>
