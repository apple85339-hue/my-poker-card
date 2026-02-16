<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>連續抽牌器</title>
    <style>
        body { 
            text-align: center; 
            font-family: -apple-system, sans-serif;
            background-color: #1a472a; 
            color: white; 
            margin: 0;
            padding: 20px;
            display: flex;
            flex-direction: column;
            height: 100vh;
            box-sizing: border-box;
        }

        /* 讓卡片區域可以橫向捲動 */
        .card-wrapper {
            width: 100%;
            overflow-x: auto;
            padding: 20px 0;
            display: flex;
            justify-content: flex-start; /* 讓牌從左邊開始排 */
            min-height: 220px;
            -webkit-overflow-scrolling: touch; /* iOS 順滑捲動 */
        }

        .card-container { 
            display: flex; 
            gap: 10px; 
            padding: 0 20px;
        }
        
        .card {
            flex: 0 0 100px; /* 固定寬度，不被壓縮 */
            height: 150px; 
            background: white; 
            border-radius: 8px;
            display: flex; 
            flex-direction: column; 
            justify-content: center; 
            align-items: center;
            color: black; 
            box-shadow: 2px 4px 10px rgba(0,0,0,0.3);
            animation: popIn 0.3s ease-out; /* 出場動畫 */
        }
        
        @keyframes popIn {
            0% { transform: scale(0.5); opacity: 0; }
            100% { transform: scale(1); opacity: 1; }
        }

        .red { color: #d12d36; }
        .card-suit { font-size: 1.2rem; }
        .card-value { font-size: 1.8rem; font-weight: bold; }

        .btn-group {
            margin-top: auto; /* 把按鈕推到底部 */
            padding-bottom: 30px;
            display: flex;
            flex-direction: column;
            gap: 15px;
            width: 100%;
            align-items: center;
        }

        button {
            width: 80%;
            max-width: 300px;
            padding: 18px; 
            font-size: 1.2rem; 
            font-weight: bold;
            border: none; 
            border-radius: 50px; 
            box-shadow: 0 4px 0 rgba(0,0,0,0.2);
        }

        .btn-draw { background-color: #f1c40f; color: #333; }
        .btn-reset { background-color: #e74c3c; color: white; font-size: 1rem; padding: 10px; }
        
        button:active { transform: translateY(3px); box-shadow: none; }
    </style>
</head>
<body>

    <h1>🃏 撲克加牌器</h1>
    
    <div class="card-wrapper" id="scroll-area">
        <div class="card-container" id="display">
            </div>
    </div>

    <div class="btn-group">
        <button class="btn-draw" onclick="addOneCard()">➕ 再抽一張</button>
        <button class="btn-reset" onclick="resetGame()">🧹 清空重來</button>
    </div>

    <script>
        const suits = ['♠', '♥', '♦', '♣'];
        const values = ['A', '2', '3', '4', '5', '6', '7', '8', '9', '10', 'J', 'Q', 'K'];

        function addOneCard() {
            const container = document.getElementById('display');
            const wrapper = document.getElementById('scroll-area');

            const suit = suits[Math.floor(Math.random() * suits.length)];
            const value = values[Math.floor(Math.random() * values.length)];
            const isRed = suit === '♥' || suit === '♦';

            const cardDiv = document.createElement('div');
            cardDiv.className = `card ${isRed ? 'red' : ''}`;
            cardDiv.innerHTML = `
                <div class="card-suit">${suit}</div>
                <div class="card-value">${value}</div>
            `;
            
            container.appendChild(cardDiv);

            // 自動捲動到最右邊，看到最新抽到的牌
            setTimeout(() => {
                wrapper.scrollTo({
                    left: wrapper.scrollWidth,
                    behavior: 'smooth'
                });
            }, 100);

            if (navigator.vibrate) navigator.vibrate(30);
        }

        function resetGame() {
            document.getElementById('display').innerHTML = '';
        }
    </script>
</body>
</html>
