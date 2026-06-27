# jlinnh.github.io
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Happy 3rd Monthsary</title>
    <link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@300;400;600&family=Playfair+Display:ital,wght@0,600;1,600&display=swap" rel="stylesheet">
    <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.6.0/dist/confetti.browser.min.js"></script>
    
    <style>
        :root {
            --dark-blue: #051937;
            --rich-purple: #16222A;
            --rose-gold: #E2D1C3;
            --soft-white: #f8f9fa;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }

        body {
            background: linear-gradient(135deg, var(--dark-blue), var(--rich-purple));
            background-attachment: fixed;
            color: var(--soft-white);
            font-family: 'Montserrat', sans-serif;
            overflow-x: hidden;
            min-height: 100vh;
        }

        h1, h2, h3 {
            font-family: 'Playfair Display', serif;
            color: var(--rose-gold);
            text-align: center;
            margin-bottom: 20px;
            font-weight: 600;
        }

        .hidden {
            display: none !important;
        }

        .fade-in {
            animation: fadeIn 1.5s forwards;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        /* --- THE STARTING STATE --- */
        #start-screen {
            position: fixed;
            top: 0; left: 0; width: 100%; height: 100%;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            z-index: 100;
            background: linear-gradient(135deg, var(--dark-blue), var(--rich-purple));
            transition: opacity 1s ease, visibility 1s ease;
        }

        .heart-wrapper {
            cursor: pointer;
            text-align: center;
            transition: transform 0.3s ease;
        }

        .heart-wrapper:hover {
            transform: scale(1.1);
        }

        .css-heart {
            position: relative;
            width: 100px;
            height: 90px;
            margin-bottom: 30px;
            animation: pulse 2s infinite;
        }

        .css-heart:before,
        .css-heart:after {
            position: absolute;
            content: "";
            left: 50px;
            top: 0;
            width: 50px;
            height: 80px;
            background: var(--rose-gold);
            border-radius: 50px 50px 0 0;
            transform: rotate(-45deg);
            transform-origin: 0 100%;
            box-shadow: 0 0 20px rgba(226, 209, 195, 0.5);
        }

        .css-heart:after {
            left: 0;
            transform: rotate(45deg);
            transform-origin: 100% 100%;
        }

        .shatter {
            animation: shatterAnim 1s forwards !important;
        }

        @keyframes pulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.05); }
            100% { transform: scale(1); }
        }

        @keyframes shatterAnim {
            0% { transform: scale(1); opacity: 1; filter: blur(0); }
            50% { transform: scale(1.5); opacity: 0.8; filter: blur(4px); }
            100% { transform: scale(3) rotate(45deg); opacity: 0; filter: blur(15px); }
        }

        /* --- MAIN CONTENT CONTAINER --- */
        #main-content {
            padding: 50px 20px;
            max-width: 900px;
            margin: 0 auto;
            display: flex;
            flex-direction: column;
            gap: 80px;
        }

        /* --- STAGE 1: TIMELINE --- */
        .timeline-container {
            display: flex;
            align-items: center;
            justify-content: center;
            flex-direction: column;
            position: relative;
        }

        .timeline {
            display: flex;
            flex-direction: column;
            align-items: center;
            position: relative;
            gap: 50px;
            padding: 40px 0;
        }

        .timeline::before {
            content: '';
            position: absolute;
            top: 0; bottom: 0;
            width: 2px;
            border-left: 2px dashed var(--rose-gold);
            opacity: 0.5;
            z-index: 0;
        }

        .node {
            position: relative;
            z-index: 1;
            background: var(--rich-purple);
            border: 2px solid var(--rose-gold);
            color: var(--rose-gold);
            padding: 20px;
            border-radius: 50%;
            width: 90px;
            height: 90px;
            display: flex;
            justify-content: center;
            align-items: center;
            font-family: 'Playfair Display', serif;
            font-size: 14px;
            text-align: center;
            cursor: pointer;
            transition: all 0.4s ease;
            box-shadow: 0 0 15px rgba(226, 209, 195, 0.2);
        }

        .node:hover {
            box-shadow: 0 0 30px rgba(226, 209, 195, 0.8);
            transform: scale(1.1);
        }

        .dimmed {
            opacity: 0.3;
            filter: blur(2px);
        }

        #counter-container {
            margin-top: 30px;
            text-align: center;
            opacity: 0;
            transform: translateY(-20px);
            transition: all 0.6s ease;
        }

        #counter-container.visible {
            opacity: 1;
            transform: translateY(0);
        }

        .countdown-time {
            font-size: 1.5rem;
            letter-spacing: 2px;
            color: var(--soft-white);
            margin-top: 10px;
            font-weight: 300;
        }

        /* --- STAGE 2: CONSTELLATION --- */
        .constellation-wrapper {
            position: relative;
            width: 100%;
            max-width: 500px;
            aspect-ratio: 1/1;
            margin: 0 auto;
            background: radial-gradient(circle, rgba(22,34,42,0.8) 0%, rgba(5,25,55,0.8) 100%);
            border: 1px solid rgba(226, 209, 195, 0.2);
            border-radius: 15px;
            overflow: hidden;
        }

        #star-lines {
            position: absolute;
            top: 0; left: 0; width: 100%; height: 100%;
            pointer-events: none;
        }

        .star {
            position: absolute;
            width: 24px;
            height: 24px;
            background: var(--rich-purple);
            border: 2px solid var(--rose-gold);
            border-radius: 50%;
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 10px;
            color: var(--rose-gold);
            cursor: pointer;
            transform: translate(-50%, -50%);
            transition: all 0.3s ease;
            box-shadow: 0 0 10px rgba(226, 209, 195, 0.4);
            z-index: 2;
        }

        .star.active {
            background: var(--rose-gold);
            color: var(--dark-blue);
            box-shadow: 0 0 20px var(--rose-gold);
        }

        .star.pulsing {
            animation: starPulse 1.5s infinite;
        }

        @keyframes starPulse {
            0% { box-shadow: 0 0 10px rgba(226, 209, 195, 0.4); }
            50% { box-shadow: 0 0 25px rgba(226, 209, 195, 1); }
            100% { box-shadow: 0 0 10px rgba(226, 209, 195, 0.4); }
        }

        /* --- STAGE 3: MESSAGE WALL --- */
        .grid-wall {
            display: grid;
            grid-template-columns: repeat(6, 1fr);
            gap: 10px;
            max-width: 600px;
            margin: 0 auto;
        }

        .flip-card {
            background-color: transparent;
            aspect-ratio: 1/1;
            perspective: 1000px;
            cursor: pointer;
        }

        .flip-card-inner {
            position: relative;
            width: 100%;
            height: 100%;
            text-align: center;
            transition: transform 0.6s cubic-bezier(0.4, 0.2, 0.2, 1);
            transform-style: preserve-3d;
        }

        .flip-card.flipped .flip-card-inner {
            transform: rotateY(180deg);
        }

        .flip-card-front, .flip-card-back {
            position: absolute;
            width: 100%;
            height: 100%;
            -webkit-backface-visibility: hidden;
            backface-visibility: hidden;
            border-radius: 8px;
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 1.5rem;
            font-weight: 600;
        }

        .flip-card-front {
            background-color: var(--rich-purple);
            border: 1px solid rgba(226, 209, 195, 0.1);
        }

        .flip-card-back {
            background-color: var(--rose-gold);
            color: var(--dark-blue);
            transform: rotateY(180deg);
            box-shadow: 0 0 15px rgba(226, 209, 195, 0.4);
        }

        /* --- FINAL INTERACTION --- */
        .celebrate-container {
            text-align: center;
            padding: 40px 0;
        }

        button {
            background: transparent;
            color: var(--rose-gold);
            font-family: 'Montserrat', sans-serif;
            font-size: 1.2rem;
            padding: 15px 40px;
            border: 2px solid var(--rose-gold);
            border-radius: 30px;
            cursor: pointer;
            transition: all 0.3s ease;
            text-transform: uppercase;
            letter-spacing: 2px;
        }

        button:hover {
            background: var(--rose-gold);
            color: var(--dark-blue);
            box-shadow: 0 0 25px var(--rose-gold);
        }

        /* --- MODAL --- */
        #modal {
            position: fixed;
            top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(5, 25, 55, 0.9);
            display: flex;
            justify-content: center;
            align-items: center;
            z-index: 200;
            opacity: 0;
            visibility: hidden;
            transition: all 0.5s ease;
        }

        #modal.show {
            opacity: 1;
            visibility: visible;
        }

        .modal-content {
            background: var(--rich-purple);
            padding: 50px;
            border-radius: 20px;
            border: 1px solid var(--rose-gold);
            text-align: center;
            box-shadow: 0 0 50px rgba(226, 209, 195, 0.3);
            max-width: 80%;
            transform: scale(0.8);
            transition: transform 0.5s ease;
        }

        #modal.show .modal-content {
            transform: scale(1);
        }

        .modal-content h2 {
            margin-bottom: 0;
            line-height: 1.4;
        }

        @media (max-width: 600px) {
            .grid-wall { grid-template-columns: repeat(4, 1fr); }
            .countdown-time { font-size: 1rem; }
            .modal-content { padding: 30px 20px; }
        }
    </style>
</head>
<body>

    <div id="start-screen">
        <div class="heart-wrapper" onclick="startJourney()">
            <div class="css-heart" id="start-heart"></div>
        </div>
        <p style="font-size: 1.2rem; letter-spacing: 2px;">Are you ready?</p>
    </div>

    <div id="main-content" class="hidden">
        
        <section id="stage-1" class="timeline-container fade-in">
            <h2>The Journey Begins</h2>
            <div class="timeline" id="timeline">
                <div class="node">2026</div>
                <div class="node" id="target-node">3 Months</div>
                <div class="node">28th</div>
            </div>
            <div id="counter-container">
                <p>Our time together so far:</p>
                <div class="countdown-time" id="countdown-text">0y 0m 0d 0h 0m 0s</div>
            </div>
        </section>

        <section id="stage-2" class="fade-in">
            <h2>Connect Our Stars</h2>
            <p style="text-align: center; margin-bottom: 20px; opacity: 0.8; font-size: 0.9rem;">Click the stars in order from 1 to 8.</p>
            <div class="constellation-wrapper">
                <svg id="star-lines">
                    </svg>
                <div id="stars-container">
                    </div>
            </div>
        </section>

        <section id="stage-3" class="hidden">
            <h2>A Message For You</h2>
            <p style="text-align: center; margin-bottom: 20px; opacity: 0.8; font-size: 0.9rem;">Hover over the tiles to reveal.</p>
            <div class="grid-wall" id="message-wall">
                </div>
        </section>

        <section id="final-stage" class="celebrate-container hidden">
            <button onclick="triggerFinale()">Celebrate!</button>
        </section>
    </div>

    <div id="modal">
        <div class="modal-content">
            <h2>Three months is just the start.<br>I love you!</h2>
        </div>
    </div>

    <script>
        // --- 1. START SCREEN LOGIC ---
        function startJourney() {
            const startScreen = document.getElementById('start-screen');
            const heart = document.getElementById('start-heart');
            
            heart.classList.add('shatter');
            
            setTimeout(() => {
                startScreen.style.opacity = '0';
                setTimeout(() => {
                    startScreen.style.display = 'none';
                    document.getElementById('main-content').classList.remove('hidden');
                    initTimeline();
                    initConstellation();
                }, 1000);
            }, 800);
        }

        // --- 2. STAGE 1: TIMELINE LOGIC ---
        function initTimeline() {
            const targetNode = document.getElementById('target-node');
            const allNodes = document.querySelectorAll('.node');
            const counterContainer = document.getElementById('counter-container');

            targetNode.addEventListener('mouseenter', () => {
                allNodes.forEach(node => {
                    if (node !== targetNode) node.classList.add('dimmed');
                });
                counterContainer.classList.add('visible');
            });

            targetNode.addEventListener('mouseleave', () => {
                allNodes.forEach(node => node.classList.remove('dimmed'));
            });

            // Start Date: March 28, 2026
            const startDate = new Date('2026-03-28T00:00:00');
            
            function updateTimer() {
                const now = new Date();
                let years = now.getFullYear() - startDate.getFullYear();
                let months = now.getMonth() - startDate.getMonth();
                let days = now.getDate() - startDate.getDate();
                let hours = now.getHours() - startDate.getHours();
                let minutes = now.getMinutes() - startDate.getMinutes();
                let seconds = now.getSeconds() - startDate.getSeconds();

                if (seconds < 0) { seconds += 60; minutes--; }
                if (minutes < 0) { minutes += 60; hours--; }
                if (hours < 0) { hours += 24; days--; }
                if (days < 0) {
                    const prevMonth = new Date(now.getFullYear(), now.getMonth(), 0);
                    days += prevMonth.getDate();
                    months--;
                }
                if (months < 0) { months += 12; years--; }

                document.getElementById('countdown-text').innerHTML = 
                    `${years}y ${months}m ${days}d ${hours}h ${minutes}m ${seconds}s`;
            }

            // Call immediately so the text populates without delay
            updateTimer();
            setInterval(updateTimer, 1000);
        }

        // --- 3. STAGE 2: CONSTELLATION LOGIC ---
        // Coordinates defining a heart shape via percentages
        const starCoords = [
            { id: 1, x: 50, y: 30 }, // Top middle (cleft)
            { id: 2, x: 80, y: 15 }, // Top right
            { id: 3, x: 95, y: 45 }, // Right edge
            { id: 4, x: 75, y: 70 }, // Bottom right
            { id: 5, x: 50, y: 95 }, // Bottom tip
            { id: 6, x: 25, y: 70 }, // Bottom left
            { id: 7, x: 5,  y: 45 }, // Left edge
            { id: 8, x: 20, y: 15 }  // Top left
        ];
        
        let expectedStar = 1;

        function initConstellation() {
            const container = document.getElementById('stars-container');
            
            starCoords.forEach(coord => {
                const star = document.createElement('div');
                star.className = 'star';
                if(coord.id === 1) star.classList.add('pulsing'); // hint to start
                star.style.left = `${coord.x}%`;
                star.style.top = `${coord.y}%`;
                star.innerText = coord.id;
                
                star.addEventListener('click', () => handleStarClick(coord, star));
                container.appendChild(star);
            });
        }

        function handleStarClick(coord, element) {
            if (coord.id === expectedStar) {
                element.classList.add('active');
                element.classList.remove('pulsing');
                
                if (expectedStar > 1) {
                    drawLine(starCoords[expectedStar - 2], coord);
                }

                // NEW: Auto-connect star 8 back to star 1 to close the heart loop
                if (expectedStar === 8) {
                    setTimeout(() => drawLine(coord, starCoords[0]), 300);
                }

                expectedStar++;
                
                if (expectedStar <= 8) {
                    // Make next star pulse
                    const nextStar = document.querySelectorAll('.star')[expectedStar - 1];
                    nextStar.classList.add('pulsing');
                } else {
                    // Game Won
                    document.querySelector('.constellation-wrapper').style.boxShadow = "0 0 40px #E2D1C3";
                    setTimeout(unlockStage3, 1000);
                }
            }
        }

        function drawLine(start, end) {
            const svg = document.getElementById('star-lines');
            const line = document.createElementNS('http://www.w3.org/2000/svg', 'line');
            line.setAttribute('x1', `${start.x}%`);
            line.setAttribute('y1', `${start.y}%`);
            line.setAttribute('x2', `${end.x}%`);
            line.setAttribute('y2', `${end.y}%`);
            line.setAttribute('stroke', '#E2D1C3');
            line.setAttribute('stroke-width', '2');
            line.setAttribute('stroke-dasharray', '4');
            svg.appendChild(line);
        }

        // --- 4. STAGE 3: MESSAGE WALL LOGIC ---
        function unlockStage3() {
            const stage3 = document.getElementById('stage-3');
            stage3.classList.remove('hidden');
            stage3.classList.add('fade-in');
            
            // Scroll to it smoothly
            setTimeout(() => {
                stage3.scrollIntoView({ behavior: 'smooth', block: 'start' });
            }, 100);

            const message = "HAPPY 3 MONTHS MY LOVE ♥"; // Exactly 24 chars
            const wall = document.getElementById('message-wall');
            let flippedCount = 0;

            for (let i = 0; i < message.length; i++) {
                const char = message[i];
                const card = document.createElement('div');
                card.className = 'flip-card';
                
                // Keep spaces invisible on the front
                const isSpace = char === ' ';
                
                card.innerHTML = `
                    <div class="flip-card-inner">
                        <div class="flip-card-front" style="${isSpace ? 'opacity:0;' : ''}"></div>
                        <div class="flip-card-back" style="${isSpace ? 'background:transparent; box-shadow:none;' : ''}">
                            ${char}
                        </div>
                    </div>
                `;

                // If it's a space, pre-flip it essentially or ignore it in counting
                if (!isSpace) {
                    card.addEventListener('mouseenter', () => {
                        if (!card.classList.contains('flipped')) {
                            card.classList.add('flipped');
                            flippedCount++;
                            checkWallComplete(flippedCount, 20); // 20 non-space characters
                        }
                    });
                } else {
                    card.classList.add('flipped'); // Auto-flip spaces
                }

                wall.appendChild(card);
            }
        }

        function checkWallComplete(current, total) {
            if (current === total) {
                setTimeout(() => {
                    const finalStage = document.getElementById('final-stage');
                    finalStage.classList.remove('hidden');
                    finalStage.classList.add('fade-in');
                    finalStage.scrollIntoView({ behavior: 'smooth', block: 'end' });
                }, 500);
            }
        }

        // --- 5. FINAL INTERACTION LOGIC ---
        function triggerFinale() {
            // Launch Confetti
            var duration = 3000;
            var end = Date.now() + duration;

            (function frame() {
                confetti({
                    particleCount: 5,
                    angle: 60,
                    spread: 55,
                    origin: { x: 0 },
                    colors: ['#E2D1C3', '#16222A', '#f8f9fa']
                });
                confetti({
                    particleCount: 5,
                    angle: 120,
                    spread: 55,
                    origin: { x: 1 },
                    colors: ['#E2D1C3', '#16222A', '#f8f9fa']
                });

                if (Date.now() < end) {
                    requestAnimationFrame(frame);
                }
            }());

            // Show Modal
            const modal = document.getElementById('modal');
            modal.classList.add('show');
            
            // Close modal when clicking anywhere on it
            modal.addEventListener('click', () => {
                modal.classList.remove('show');
            });
        }
    </script>
</body>
</html>
