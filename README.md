# valentine
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Will You Be My Valentine?</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; font-family: 'Arial Rounded MT Bold', 'Arial', sans-serif; }
        body { background-color: #ffebee; min-height: 100vh; display: flex; flex-direction: column; justify-content: center; align-items: center; overflow: hidden; position: relative; }
        .container { text-align: center; padding: 30px; background: linear-gradient(145deg, #ffcdd2, #f8bbd0); border-radius: 25px; box-shadow: 0 15px 35px rgba(233, 30, 99, 0.3); max-width: 700px; width: 90%; position: relative; z-index: 2; border: 8px solid white; transition: transform 0.3s; }
        .container:hover { transform: translateY(-5px); }
        h1 { color: #d81b60; font-size: 3.5rem; margin-bottom: 30px; text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.1); padding: 10px; position: relative; }
        h1:after { content: "💖"; position: absolute; top: -10px; right: 10px; font-size: 2rem; animation: float 3s ease-in-out infinite; }
        .buttons-container { display: flex; justify-content: center; gap: 30px; flex-wrap: wrap; margin-top: 40px; position: relative; min-height: 120px; }
        #yesButton { background-color: #e91e63; color: white; border: none; padding: 20px 50px; font-size: 1.8rem; border-radius: 50px; cursor: pointer; box-shadow: 0 10px 20px rgba(233, 30, 99, 0.4); transition: all 0.3s ease; font-weight: bold; letter-spacing: 1px; min-width: 180px; }
        #yesButton:hover { background-color: #d81b60; transform: scale(1.05); }
        #noButton { background-color: #4a4a4a; color: white; border: none; padding: 15px 30px; font-size: 1.5rem; border-radius: 50px; cursor: pointer; transition: all 0.2s ease; position: relative; font-weight: bold; min-width: 150px; }
        #noButton:hover { background-color: #333; }
        .comment { position: absolute; bottom: -40px; left: 50%; transform: translateX(-50%); background-color: white; padding: 8px 15px; border-radius: 20px; color: #e91e63; font-weight: bold; box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1); opacity: 0; transition: opacity 0.3s; white-space: nowrap; }
        .comment.show { opacity: 1; }
        .hearts-container { position: fixed; top: 0; left: 0; width: 100%; height: 100%; pointer-events: none; z-index: 1; }
        .heart { position: absolute; color: rgba(233, 30, 99, 0.7); font-size: 24px; animation: floatUp 5s linear forwards; }
        .love-message { margin-top: 40px; font-size: 3rem; color: #d81b60; opacity: 0; transition: opacity 0.5s; font-weight: bold; text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.1); padding: 20px; }
        .love-message.show { opacity: 1; }
        .footer { margin-top: 30px; color: #d81b60; font-size: 1.2rem; font-weight: bold; }
        @keyframes float { 0%, 100% { transform: translateY(0); } 50% { transform: translateY(-15px); } }
        @keyframes floatUp { 0% { transform: translateY(100vh) rotate(0deg); opacity: 1; } 100% { transform: translateY(-100px) rotate(360deg); opacity: 0; } }
        @keyframes pulse { 0%, 100% { transform: scale(1); } 50% { transform: scale(1.05); } }
        .pulse { animation: pulse 1s infinite; }
        @media (max-width: 600px) { h1 { font-size: 2.5rem; } #yesButton { font-size: 1.5rem; padding: 15px 30px; } #noButton { font-size: 1.2rem; padding: 12px 25px; } .buttons-container { gap: 15px; } .love-message { font-size: 2.2rem; } }
    </style>
</head>
<body>
    <div class="hearts-container" id="heartsContainer"></div>
    <div class="container">
        <h1>Will You Be My Valentine? 💝</h1>
        <div class="buttons-container">
            <button id="yesButton">YES</button>
            <button id="noButton">NO</button>
            <div class="comment" id="comment"></div>
        </div>
        <div class="love-message" id="loveMessage">i love u sm sweetheart 💖</div>
        <div class="footer">Made with <i class="fas fa-heart" style="color:#e91e63;"></i> for you</div>
    </div>
    <script>
        document.addEventListener('DOMContentLoaded', function() {
            const yesButton = document.getElementById('yesButton');
            const noButton = document.getElementById('noButton');
            const comment = document.getElementById('comment');
            const loveMessage = document.getElementById('loveMessage');
            const heartsContainer = document.getElementById('heartsContainer');
            const comments = ["Are you sure?", "Baby u sure?", "Babyyyyyy...", "Just say yes baby", "Baby pleaseeee", "Think again!", "My heart is breaking 💔", "Please don't say no!", "I'll be so sad...", "One more chance?", "Pretty please?", "With a cherry on top? 🍒"];
            let clickCount = 0, yesSize = 1;
            function createHeart() {
                const heart = document.createElement('div');
                heart.classList.add('heart');
                heart.innerHTML = '❤️';
                heart.style.left = Math.random() * 100 + 'vw';
                heart.style.fontSize = (Math.random() * 20 + 15) + 'px';
                heart.style.animationDuration = (Math.random() * 3 + 4) + 's';
                heartsContainer.appendChild(heart);
                setTimeout(() => heart.remove(), 5000);
            }
            setInterval(createHeart, 300);
            noButton.addEventListener('click', function() {
                yesSize += 0.3;
                yesButton.style.transform = `scale(${yesSize})`;
                comment.textContent = comments[clickCount % comments.length];
                comment.classList.add('show');
                const container = document.querySelector('.buttons-container');
                const maxX = container.offsetWidth - noButton.offsetWidth;
                const maxY = container.offsetHeight - noButton.offsetHeight;
                noButton.style.position = 'absolute';
                noButton.style.left = `${Math.max(0, Math.random() * maxX)}px`;
                noButton.style.top = `${Math.max(0, Math.random() * maxY)}px`;
                clickCount++;
                setTimeout(() => comment.classList.remove('show'), 1500);
                yesButton.classList.add('pulse');
                setTimeout(() => yesButton.classList.remove('pulse'), 1000);
                for (let i = 0; i < 5; i++) setTimeout(createHeart, i * 100);
            });
            yesButton.addEventListener('click', function() {
                loveMessage.classList.add('show');
                yesButton.style.display = noButton.style.display = 'none';
                for (let i = 0; i < 50; i++) setTimeout(() => {
                    const heart = document.createElement('div');
                    heart.classList.add('heart');
                    heart.innerHTML = '💖';
                    heart.style.left = Math.random() * 100 + 'vw';
                    heart.style.fontSize = (Math.random() * 20 + 20) + 'px';
                    heart.style.animationDuration = (Math.random() * 2 + 3) + 's';
                    heartsContainer.appendChild(heart);
                    setTimeout(() => heart.remove(), 5000);
                }, i * 50);
                const celebration = document.createElement('div');
                celebration.innerHTML = "Yay! You made me the happiest person! 🎉💕";
                celebration.style.color = "#e91e63";
                celebration.style.fontSize = "1.8rem";
                celebration.style.fontWeight = "bold";
                celebration.style.marginTop = "20px";
                celebration.style.animation = "float 2s infinite";
                document.querySelector('.buttons-container').appendChild(celebration);
            });
            noButton.addEventListener('mouseover', function() {
                if (clickCount > 3) {
                    const container = document.querySelector('.buttons-container');
                    const maxX = container.offsetWidth - noButton.offsetWidth;
                    const maxY = container.offsetHeight - noButton.offsetHeight;
                    noButton.style.position = 'absolute';
                    noButton.style.left = `${Math.max(0, Math.random() * maxX)}px`;
                    noButton.style.top = `${Math.max(0, Math.random() * maxY)}px`;
                }
            });
        });
    </script>
</body>
</html>