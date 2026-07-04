<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Advance Happy Birthday My Love!</title>
    <style>
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }

        body {
            background: linear-gradient(135deg, #ffe3e3, #ffd1d1);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            overflow: hidden;
            position: relative;
        }

        /* Background falling elements */
        .falling-item {
            position: absolute;
            top: -50px;
            font-size: 24px;
            pointer-events: none;
            animation: fall linear infinite;
        }

        @keyframes fall {
            0% {
                transform: translateY(0) rotate(0deg);
                opacity: 1;
            }
            100% {
                transform: translateY(110vh) rotate(360deg);
                opacity: 0;
            }
        }

        /* Container styling */
        .container {
            text-align: center;
            z-index: 10;
            padding: 20px;
        }

        h1 {
            color: #d63031;
            font-size: 2.5rem;
            margin-bottom: 30px;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.1);
            animation: heartbeat 1.5s infinite;
        }

        @keyframes heartbeat {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.05); }
        }

        /* Interactive Gift Box */
        .gift-box-wrapper {
            position: relative;
            width: 150px;
            height: 150px;
            margin: 0 auto;
            cursor: pointer;
            transition: transform 0.3s;
        }

        .gift-box-wrapper:hover {
            transform: scale(1.1);
        }

        .gift-box {
            width: 100%;
            height: 100%;
            background-color: #ff4757;
            position: relative;
            border-radius: 10px;
            box-shadow: 0 10px 20px rgba(0,0,0,0.15);
        }

        /* Box Lid */
        .gift-box::before {
            content: '';
            position: absolute;
            top: -20px;
            left: -5px;
            width: 160px;
            height: 30px;
            background-color: #ff6b81;
            border-radius: 5px;
            box-shadow: 0 5px 10px rgba(0,0,0,0.1);
            transition: transform 0.5s ease;
        }

        /* Horizontal Ribbon */
        .gift-box::after {
            content: '';
            position: absolute;
            top: 0;
            left: 70px;
            width: 10px;
            height: 100%;
            background-color: #eccc68;
        }

        /* Vertical Ribbon Ribbon */
        .ribbon-v {
            position: absolute;
            top: 70px;
            left: 0;
            width: 100%;
            height: 10px;
            background-color: #eccc68;
            z-index: 2;
        }

        /* Opened State for Gift Box */
        .gift-box-wrapper.open .gift-box::before {
            transform: translateY(-80px) rotate(-20deg);
            opacity: 0;
        }

        .gift-box-wrapper.open {
            transform: scale(0);
            opacity: 0;
            transition: all 0.5s ease;
            pointer-events: none;
        }

        /* Proposal Card Hidden initially */
        .proposal-card {
            display: none;
            background: rgba(255, 255, 255, 0.95);
            padding: 40px;
            border-radius: 20px;
            box-shadow: 0 15px 35px rgba(0,0,0,0.1);
            max-width: 400px;
            width: 90%;
            margin: 0 auto;
            transform: scale(0.8);
            opacity: 0;
            transition: all 0.5s ease;
        }

        .proposal-card.show {
            display: block;
            transform: scale(1);
            opacity: 1;
        }

        .proposal-card h2 {
            color: #ff4757;
            margin-bottom: 25px;
            font-size: 1.8rem;
            line-height: 1.4;
        }

        /* Action Buttons */
        .btn-group {
            display: flex;
            justify-content: center;
            gap: 20px;
            position: relative;
            height: 50px;
        }

        .btn {
            padding: 12px 35px;
            font-size: 1.1rem;
            border: none;
            border-radius: 25px;
            cursor: pointer;
            font-weight: bold;
            transition: all 0.2s ease;
        }

        .btn-yes {
            background-color: #2ed573;
            color: white;
            box-shadow: 0 5px 15px rgba(46, 213, 115, 0.3);
        }

        .btn-yes:hover {
            transform: scale(1.1);
        }

        .btn-maybe {
            background-color: #ffa502;
            color: white;
            position: absolute;
            box-shadow: 0 5px 15px rgba(255, 165, 2, 0.3);
        }
    </style>
</head>
<body>

    <div class="container">
        <h1 id="main-title">Advance Happy Birthday My Love! <br> Love u more... ❤️</h1>
        
        <!-- Clickable Gift Box -->
        <div class="gift-box-wrapper" id="giftBox" onclick="openGift()">
            <div class="gift-box">
                <div class="ribbon-v"></div>
            </div>
        </div>

        <!-- Proposal Card Box -->
        <div class="proposal-card" id="proposalCard">
            <h2>Will you love me forever? 🥺</h2>
            <div class="btn-group">
                <button class="btn btn-yes" onclick="accepted()">Yes!</button>
                <button class="btn btn-maybe" id="maybeBtn" onmouseover="moveButton()">Maybe</button>
            </div>
        </div>
    </div>

    <script>
        // Array of falling elements (Hearts, Balloons, Flowers)
        const elements = ['🎈', '❤️', '🌸', '💖', '🌹', '✨', '💐'];

        function createFallingItem() {
            const item = document.createElement('div');
            item.classList.add('falling-item');
            
            // Randomly select emoji
            item.innerText = elements[Math.floor(Math.random() * elements.length)];
            
            // Random position and timing
            item.style.left = Math.random() * 100 + 'vw';
            item.style.animationDuration = Math.random() * 3 + 2 + 's'; 
            item.style.fontSize = Math.random() * 20 + 15 + 'px';
            
            document.body.appendChild(item);

            // Clean up elements after animation ends
            setTimeout(() => {
                item.remove();
            }, 5000);
        }

        // Spawn falling elements continuously
        setInterval(createFallingItem, 150);

        // Open gift box trigger
        function openGift() {
            const giftBox = document.getElementById('giftBox');
            const proposalCard = document.getElementById('proposalCard');
            
            giftBox.classList.add('open');
            
            setTimeout(() => {
                giftBox.style.display = 'none';
                proposalCard.classList.add('show');
            }, 500);
        }

        // Runaway "Maybe" button logic
        function moveButton() {
            const btn = document.getElementById('maybeBtn');
            const x = Math.random() * 160 - 80; 
            const y = Math.random() * 100 - 50;
            
            btn.style.transform = `translate(${x}px, ${y}px)`;
        }

        // Handle "Yes" selection with your custom message
        function accepted() {
            document.getElementById('proposalCard').innerHTML = "<h2>chandu loves u more ❤️💋 <br><br> vennkat</h2>";
            // Double the falling celebration speed
            setInterval(createFallingItem, 40);
        }
    </script>
</body>
</html>


