<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <title>隨機撲克牌抽取器</title>
    <style>
        body { text-align: center; font-family: Arial, sans-serif; background-color: #2d5a27; color: white; }
        .card-container { display: flex; justify-content: center; gap: 20px; margin-top: 50px; min-height: 250px; }
        .card {
            width: 150px; height: 220px; background: white; border-radius: 10px;
            display: flex; flex-direction: column; justify-content: center; align-items: center;
            font-size: 2rem; color: black; box-shadow: 0 4px 8px rgba(0,0,0,0.5);
        }
        .red { color: #d12d36; }
        button {
            padding: 15px 30px; font-size: 1.2rem; cursor: pointer;
            background-color: #f1c40f; border: none; border-radius: 5px; margin-top: 30px;
        }
        button:hover { background-color: #e6b800; }
    </style>
</head>
<body>

    <h1>🃏 試試你的手氣</h1>
    <div class="card-container" id="display">
        </div>
    <button onclick="drawCards()">點我抽兩張牌！</button>

    <script>
        const suits = ['♠', '♥', '♦', '♣'];
        const values = ['A', '2', '3', '4', '5', '6', '7', '8', '9', '10', 'J', 'Q', 'K'];

        function drawCards() {
            const container = document.getElementById('display');
            container.innerHTML = ''; // 清空目前的牌

            for (let i = 0; i < 2; i++) {
                const suit = suits[Math.floor(Math.random() * suits.length)];
                const value = values[Math.floor(Math.random() * values.length)];
                const isRed = suit === '♥' || suit === '♦';

                const cardDiv = document.createElement('div');
                cardDiv.className = `card ${isRed ? 'red' : ''}`;
                cardDiv.innerHTML = `<div>${suit}</div><div>${value}</div>`;
                
                container.appendChild(cardDiv);
            }
        }
    </script>
</body>
</html>
