<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>For You 💌</title>
    <style>
        body {
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            background: linear-gradient(135deg, #ff9a9e 0%, #fecfef 99%, #fecfef 100%);
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            overflow: hidden;
        }

        /* Envelope Styles */
        .envelope-wrapper {
            cursor: pointer;
            transition: transform 0.3s ease;
        }
        
        .envelope-wrapper:hover {
            transform: scale(1.05);
        }

        .envelope {
            position: relative;
            width: 300px;
            height: 200px;
            background: #f08080;
            border-radius: 0 0 10px 10px;
            box-shadow: 0 8px 20px rgba(0,0,0,0.15);
        }

        .envelope-flap {
            position: absolute;
            top: 0;
            width: 0;
            height: 0;
            border-left: 150px solid transparent;
            border-right: 150px solid transparent;
            border-top: 120px solid #f08080;
            transform-origin: top;
            transition: transform 0.6s ease, z-index 0s 0.3s;
            z-index: 10;
        }

        .envelope-body {
            position: absolute;
            bottom: 0;
            width: 100%;
            height: 100%;
            background: #e67373;
            border-radius: 0 0 10px 10px;
        }

        .letter {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            width: 260px;
            height: 140px;
            background: #fff;
            border-radius: 8px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.2);
            transition: transform 0.6s cubic-bezier(0.175, 0.885, 0.32, 1.275), opacity 0.3s;
            z-index: 5;
            padding: 20px;
            box-sizing: border-box;
            text-align: center;
            opacity: 0;
        }

        .letter h2 {
            margin-top: 5px;
            color: #ff4757;
            font-size: 22px;
        }

        .letter p {
            color: #57606f;
            font-size: 14px;
            line-height: 1.5;
        }

        /* Opened State */
        .open .envelope-flap {
            transform: rotateX(180deg);
            z-index: 0;
        }

        .open .letter {
            transform: translate(-50%, -110%);
            opacity: 1;
        }

        /* Buttons */
        .btn-group {
            display: flex;
            justify-content: center;
            gap: 20px;
            margin-top: 15px;
        }

        .btn {
            padding: 8px 20px;
            border: none;
            border-radius: 20px;
            font-size: 16px;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.2s;
        }

        .btn-yes {
            background-color: #2ed573;
            color: white;
            box-shadow: 0 4px 15px rgba(46, 213, 115, 0.4);
        }

        .btn-yes:hover {
            transform: scale(1.1);
        }

        .btn-no {
            position: absolute; /* Absolute positioning allows it to dodge smoothly */
            background-color: #ff4757;
            color: white;
            box-shadow: 0 4px 15px rgba(255, 71, 87, 0.4);
        }

        /* Success Message */
        .success-msg {
            display: none;
            text-align: center;
            color: white;
        }

        .success-msg h1 {
            font-size: 40px;
            margin: 0;
        }

        .success-msg p {
            font-size: 20px;
        }
    </style>
</head>
<body>

    <div class="envelope-wrapper" id="envelopeWrapper" onclick="openEnvelope()">
        <div class="envelope">
            <div class="envelope-flap"></div>
            <div class="envelope-body"></div>
            
            <div class="letter" id="letter">
                <h2>Will you be mine? 🥺💖</h2>
                <p>You are the absolute best, and I can't imagine my life without you. Will you make me the happiest?</p>
                <div class="btn-group">
                    <button class="btn btn-yes" onclick="sayYes(event)">Yes! ✨</button>
                    <button class="btn btn-no" id="noBtn" onmouseover="moveNoButton()" onclick="moveNoButton()">No 💔</button>
                </div>
            </div>
        </div>
    </div>

    <div class="success-msg" id="successMsg">
        <h1>Yay! 🎉❤️</h1>
        <p>I love you so much!</p>
    </div>

    <script>
        function openEnvelope() {
            const wrapper = document.getElementById('envelopeWrapper');
            wrapper.classList.add('open');
        }

        function sayYes(event) {
            event.stopPropagation(); // Prevents the envelope wrapper click event from firing
            document.getElementById('envelopeWrapper').style.display = 'none';
            document.getElementById('successMsg').style.display = 'block';
        }

        function moveNoButton() {
            const noBtn = document.getElementById('noBtn');
            const letter = document.querySelector('.letter');
            
            // Get boundaries of the letter box
            const letterRect = letter.getBoundingClientRect();
            
            // Generate random coordinates inside the letter box
            const randomX = Math.floor(Math.random() * (letterRect.width - 100));
            const randomY = Math.floor(Math.random() * (letterRect.height - 50));

            // Apply new position
            noBtn.style.position = 'absolute';
            noBtn.style.left = randomX + 'px';
            noBtn.style.top = randomY + 'px';
        }
    </script>
</body>
</html>
