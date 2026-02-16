<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tateti Lotto | Cyrcle Labs</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/ethers/5.7.2/ethers.umd.min.js"></script>
    <style>
        body { background: #0b0e11; color: #f0b90b; font-family: 'Segoe UI', Arial, sans-serif; text-align: center; padding: 20px; margin: 0; }
        .container { max-width: 550px; margin: 40px auto; background: #1e2329; border: 2px solid #f0b90b; border-radius: 20px; padding: 30px; box-shadow: 0px 0px 30px rgba(240, 185, 11, 0.15); }
        h1 { font-size: 2.2em; margin-bottom: 10px; letter-spacing: 1px; }
        .subtitle { color: #929aa5; margin-bottom: 25px; font-size: 1.1em; }
        
        .stats-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 15px; margin-bottom: 25px; }
        .stat-card { background: #2b3139; padding: 15px; border-radius: 12px; border: 1px solid #474d57; }
        .stat-val { display: block; font-size: 1.3em; font-weight: bold; color: white; }

        .board { display: grid; grid-template-columns: repeat(3, 100px); gap: 12px; justify-content: center; margin: 25px auto; }
        .cell { width: 100px; height: 100px; background: #2b3139; border: 1px solid #474d57; display: flex; align-items: center; justify-content: center; font-size: 2.5em; cursor: pointer; border-radius: 12px; transition: 0.3s; color: white; }
        .cell:hover { background: #363c44; border-color: #f0b90b; }

        .btn-connect { background: #f0b90b; color: #000; border: none; padding: 14px 28px; border-radius: 10px; font-weight: bold; cursor: pointer; font-size: 1em; width: 100%; margin-bottom: 20px; transition: 0.3s; }
        .btn-connect:hover { background: #d9a608; }
        .btn-play { background: #2ebd85; color: white; border: none; padding: 18px; border-radius: 12px; font-size: 1.3em; font-weight: bold; cursor: pointer; width: 100%; box-shadow: 0 4px 15px rgba(46, 189, 133, 0.3); }
        .btn-play:hover { background: #26a675; transform: translateY(-2px); }

        .footer { margin-top: 25px; font-size: 0.85em; color: #707a8a; line-height: 1.6; }
    </style>
</head>
<body>

<div class="container">
    <div style="font-size: 3em; margin-bottom: 10px;">🎰</div>
    <h1>TATETI LOTTO</h1>
    <p class="subtitle">By Cyrcle Labs</p>

    <button id="connectBtn" class="btn-connect" onclick="connectWallet()">🔗 CONECTAR METAMASK</button>

    <div class="stats-grid">
        <div class="stat-card">
            <small>META SUPPLY</small>
            <span class="stat-val">100M TTC</span>
        </div>
        <div class="stat-card">
            <small>QUEMA POR JUEGO</small>
            <span class="stat-val" style="color: #2ebd85;">🔥 5%</span>
        </div>
    </div>

    <div class="board" id="board">
        <div class="cell" onclick="selectCell(0)"></div>
        <div class="cell" onclick="selectCell(1)"></div>
        <div class="cell" onclick="selectCell(2)"></div>
        <div class="cell" onclick="selectCell(3)"></div>
        <div class="cell" onclick="selectCell(4)"></div>
        <div class="cell" onclick="selectCell(5)"></div>
        <div class="cell" onclick="selectCell(6)"></div>
        <div class="cell" onclick="selectCell(7)"></div>
        <div class="cell" onclick="selectCell(8)"></div>
    </div>

    <p style="margin-bottom: 15px;">Costo: 0.5 BNB / 0.4 CYR</p>
    <button class="btn-play" onclick="initGame()">🚀 ¡JUGAR Y PARTICIPAR!</button>

    <div class="footer">
        <b>EL PACTO:</b> Reducción de 1B a 100M de tokens circulantes.<br>
        CA: 0x15663c244381e5633e66f3053eaa42697f56ffff
    </div>
</div>

<script>
    let userAddress = null;

    async function connectWallet() {
        if (window.ethereum) {
            try {
                const accounts = await window.ethereum.request({ method: 'eth_requestAccounts' });
                userAddress = accounts[0];
                const btn = document.getElementById('connectBtn');
                btn.innerText = "✅ " + userAddress.substring(0, 6) + "..." + userAddress.substring(38);
                btn.style.background = "#2ebd85";
                btn.style.color = "white";
            } catch (error) {
                alert("Conexión cancelada.");
            }
        } else {
            alert("Instalá MetaMask para poder jugar en el boliche.");
        }
    }

    function selectCell(id) {
        const cells = document.getElementsByClassName('cell');
        if (!userAddress) {
            alert("Jorge, primero conectá la billetera.");
            return;
        }
        if (cells[id].innerText === "") {
            cells[id].innerText = "X";
            cells[id].style.color = "#f0b90b";
        }
    }

    function initGame() {
        if (!userAddress) {
            alert("Conectá tu MetaMask para enviar la apuesta.");
            return;
        }
        alert("Enviando apuesta al contrato... ¡Mucha suerte!");
    }
</script>

</body>
</html>
