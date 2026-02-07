<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>A Special Question ❤️</title>
    <link href="https://fonts.googleapis.com/css2?family=Lexend:wght@400;600&display=swap" rel="stylesheet">
    <style>
        :root {
            --accent-blue: #87ceeb;
            --heart-red: #ff4d6d;
        }

        body {
            margin: 0;
            height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
            background-color: #fff0f3;
            background-image: radial-gradient(#ffb3c1 0.8px, transparent 0.8px);
            background-size: 24px 24px;
            font-family: 'Lexend', sans-serif;
            overflow: hidden;
        }

        .card {
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(10px);
            padding: 3rem;
            border-radius: 40px;
            box-shadow: 0 20px 50px rgba(255, 77, 109, 0.15);
            text-align: center;
            width: 450px;
            max-width: 85%;
            position: relative;
            display: flex;
            flex-direction: column;
            align-items: center;
            z-index: 10;
        }

        .gif-wrapper {
            height: 200px;
            display: flex;
            align-items: center;
            justify-content: center;
            margin-bottom: 1rem;
        }

        .display-img {
            width: 200px;
            height: auto;
            border-radius: 20px;
        }

        h1 {
            color: #4a4a4a;
            font-size: 1.6rem;
            margin: 1rem 0 2rem 0;
        }

        .btn-container {
            display: flex;
            justify-content: center;
            align-items: center;
            gap: 20px;
            width: 100%;
            height: 150px;
        }

        .btn {
            padding: 16px 32px;
            border: none;
            border-radius: 20px;
            font-size: 1.1rem;
            font-weight: 600;
            cursor: pointer;
            transition: transform 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275), background-color 0.2s, font-size 0.3s;
            white-space: nowrap;
        }

        #yesBtn {
            background-color: var(--accent-blue);
            color: white;
            z-index: 5; /* Stays below the No button */
            position: relative;
        }

        #noBtn {
            background-color: #f1f3f5;
            color: #868e96;
            z-index: 9999; /* Higher than the Yes button so it's always visible */
            position: relative;
            transition: all 0.4s ease; /* Smoother movement */
        }

        .fade-in {
            animation: fadeIn 0.6s ease-out forwards;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: scale(0.9); }
            to { opacity: 1; transform: scale(1); }
        }
    </style>
</head>
<body>

    <div class="card" id="mainCard">
        <div class="gif-wrapper">
            <img class="display-img" src="https://media1.giphy.com/media/v1.Y2lkPTc5MGI3NjExcG8zZXF5dnllMDlrcmhvcGsyZHAzZ3Q0aHh5aWllb3p1dHZzZm1nMSZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9cw/754u3UNlbbc2tMg97K/giphy.gif" alt="Waving">
        </div>
        
        <h1 id="question">Will you be my Valentine?</h1>

        <div class="btn-container">
            <button class="btn" id="yesBtn" onclick="celebrate()">Yes</button>
            <button class="btn" id="noBtn" onclick="handleNo()">No</button>
        </div>
    </div>

    <script>
        let yesScale = 1;
        let yesFontSize = 1.1;
        let noClickCount = 0;

        const phrases = [
            "No", 
            "Are you sure?", 
            "I'm running away!", 
            "Can't catch me!", 
            "Oops, over here!", 
            "Getting bigger...", 
            "Almost full screen!", 
            "Just click Yes already!"
        ];

        function handleNo() {
            noClickCount++;
            const noBtn = document.getElementById('noBtn');
            const yesBtn = document.getElementById('yesBtn');

            // 1. Grow the Yes button and its text drastically
            yesScale += 1.8;
            yesFontSize += 1.3;
            yesBtn.style.transform = `scale(${yesScale})`;
            yesBtn.style.fontSize = `${yesFontSize}rem`;

            // 2. Change the No button text
            noBtn.innerText = phrases[Math.min(noClickCount, phrases.length - 1)];

            // 3. Move the No button out of the way
            // We switch to fixed so it can travel anywhere on screen
            noBtn.style.position = 'fixed';
            
            // Logic to pick a random spot that is likely NOT in the center 
            // where the Yes button is growing
            const padding = 100;
            const randomX = Math.random() * (window.innerWidth - noBtn.offsetWidth - padding) + (padding / 2);
            const randomY = Math.random() * (window.innerHeight - noBtn.offsetHeight - padding) + (padding / 2);
            
            noBtn.style.left = `${randomX}px`;
            noBtn.style.top = `${randomY}px`;
        }

        function celebrate() {
            const card = document.getElementById('mainCard');
            // Remove the jumping No button for a clean victory
            const noBtn = document.getElementById('noBtn');
            if (noBtn) noBtn.remove();
            
            card.innerHTML = `
                <div class="fade-in">
                    <div class="gif-wrapper">
                        <img class="display-img" src="https://media3.giphy.com/media/v1.Y2lkPTc5MGI3NjExeDlodGFocXR5eDRva2FjbzNrMzR6YXprOG5ocTVxb2dvMWxyMDAxNCZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9cw/YVhpNLN6aBCpczlLGs/giphy.gif" alt="Celebration">
                    </div>
                    <h1 style="color: var(--heart-red); margin-top: 0;">I knew you'd say yes</h1>
                    <p style="color: #666; font-weight: 600;">You made my day! ❤️</p>
                </div>
            `;
            
            document.body.style.backgroundColor = "#ffebf0";
            document.body.style.backgroundImage = "none";
        }
    </script>
</body>
</html>
