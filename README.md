<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>For My Favorite Person 🤍</title>
    <link href="https://fonts.googleapis.com/css2?family=Dancing+Script:wght@600&family=Montserrat:wght@300;400&family=Gaegu:wght@400;700&display=swap" rel="stylesheet">
    <style>
        :root { --pink: #ffafcc; --dark-pink: #ff85a1; --soft: #fffafb; --peach: #ffcad4; }
        body { margin: 0; font-family: 'Montserrat', sans-serif; background: var(--soft); color: #555; overflow-x: hidden; text-align: center; }
        
        /* Lock Screen */
        #lock { position: fixed; inset: 0; background: white; z-index: 100; display: flex; flex-direction: column; justify-content: center; align-items: center; }
        .lock-card { background: white; padding: 30px; border-radius: 30px; box-shadow: 0 10px 40px rgba(255, 175, 204, 0.2); border: 3px solid var(--peach); }
        input { padding: 15px; border: 2px solid var(--pink); border-radius: 20px; margin: 15px 0; outline: none; text-align: center; font-size: 16px; background: #fff5f7; }

        .container { max-width: 600px; margin: 0 auto; padding: 40px 20px; }
        h1 { font-family: 'Dancing Script', cursive; font-size: 2.8rem; color: var(--dark-pink); margin-bottom: 10px; }
        
        /* Buttons */
        .btn { background: var(--dark-pink); color: white; border: none; padding: 15px 40px; border-radius: 50px; font-weight: bold; cursor: pointer; font-size: 1.1rem; box-shadow: 0 6px 0 #e6738e; transition: 0.2s; font-family: 'Gaegu', cursive; }
        .btn:active { transform: translateY(4px); box-shadow: 0 2px 0 #e6738e; }

        /* Cute Envelope */
        #envelope-wrapper { display: none; margin-top: 50px; cursor: pointer; }
        .envelope { position: relative; width: 180px; height: 120px; background: var(--peach); margin: 0 auto; border-radius: 0 0 15px 15px; transition: 0.5s; box-shadow: 0 10px 20px rgba(0,0,0,0.05); }
        .envelope::before { content: ""; position: absolute; top: 0; left: 0; border-left: 90px solid transparent; border-right: 90px solid transparent; border-top: 70px solid #f8adbc; transform-origin: top; transition: 0.5s; z-index: 2; }
        .envelope.open::before { transform: rotateX(180deg); }
        .heart-seal { position: absolute; top: 40%; left: 50%; transform: translate(-50%, -50%); font-size: 40px; z-index: 3; filter: drop-shadow(0 2px 5px rgba(0,0,0,0.1)); }

        #content { display: none; opacity: 0; transition: 1s; }
        
        /* Washi Tape Letter */
        .letter-paper { 
            background: white; 
            padding: 40px 30px; 
            border-radius: 5px; 
            box-shadow: 0 10px 30px rgba(0,0,0,0.05); 
            text-align: left; 
            line-height: 1.8; 
            font-family: 'Gaegu', cursive; 
            font-size: 1.5rem; 
            white-space: pre-line; 
            margin-top: 50px; 
            position: relative;
            background-image: radial-gradient(#f1f1f1 1px, transparent 1px);
            background-size: 20px 20px;
        }
        .washi-tape { position: absolute; top: -15px; left: 50%; transform: translateX(-50%) rotate(-2deg); width: 120px; height: 35px; background: rgba(255, 175, 204, 0.5); border-left: 5px dotted #fff; border-right: 5px dotted #fff; }
        
        /* Playful Loves */
        #thousand-loves { margin-top: 50px; display: flex; flex-wrap: wrap; justify-content: center; gap: 10px; padding: 20px; }
        .love-note { display: inline-block; animation: popIn 0.6s cubic-bezier(0.175, 0.885, 0.32, 1.275) forwards; opacity: 0; font-family: 'Gaegu', cursive; background: white; padding: 5px 12px; border-radius: 15px; box-shadow: 0 4px 8px rgba(0,0,0,0.05); }

        @keyframes popIn { from { transform: scale(0) rotate(-10deg); opacity: 0; } to { transform: scale(1) rotate(0deg); opacity: 1; } }

        .floating-heart { position: fixed; pointer-events: none; z-index: 50; animation: float 4s linear infinite; }
        @keyframes float { 0% { transform: translateY(100vh) rotate(0deg); opacity: 1; } 100% { transform: translateY(-10vh) rotate(360deg); opacity: 0; } }
    </style>
</head>
<body>

    <div id="lock">
        <div class="lock-card">
            <h1>Hi, Beautiful! ✨</h1>
            <p style="font-family: 'Gaegu'; font-size: 1.2rem;">Enter our secret word:</p>
            <input type="password" id="pass" placeholder="••••••••">
            <br>
            <button class="btn" onclick="unlock()">Unlock My Heart 🤍</button>
        </div>
    </div>

    <div class="container">
        <div id="question-area" style="display:none;">
            <h1>Will you be my Valentine? 🧸</h1>
            <p style="font-family: 'Gaegu'; font-size: 1.4rem;">I have something to tell you...</p>
            <br>
            <button class="btn" onclick="showEnvelope()">Yes, I'm ready! ✨</button>
        </div>

        <div id="envelope-wrapper" onclick="revealLetter()">
            <div class="envelope" id="env">
                <div class="heart-seal">💌</div>
            </div>
            <p style="font-family: 'Gaegu'; font-size: 1.3rem; margin-top: 20px;">(Tap to open the letter)</p>
        </div>

        <div id="content">
            <div class="letter-paper" id="letterText">
                <div class="washi-tape"></div>
            </div>
            
            <div style="margin-top: 80px;">
                <h2 style="font-family: 'Dancing Script'; color: var(--dark-pink); font-size: 2.2rem;">A million times over...</h2>
                <div id="thousand-loves"></div>
            </div>
        </div>
    </div>

    <script>
        const fullLetter = `My love,\n\nI’ve been thinking about you a lot lately, about how you walked into my life in the most unexpected way and somehow made everything feel lighter. There are days when the world feels loud and heavy, and then there’s you—your laugh, your presence, the calm you bring even when things get messy. I don’t always say this out loud, but having you in my life is one of the things I’m most grateful for. You remind me that love doesn’t have to be perfect to be real. It just has to be honest.\n\nThank you for choosing me every day, even on the days when I’m not at my best. Thank you for being patient when I’m moody, tired, or quiet. Thank you for listening to my stories, even the random ones that don’t always make sense. Thank you for caring about the small details—how I’m feeling, what made me smile, what made my day hard. Those little things might seem simple, but they mean so much to me. They make me feel seen, heard, and understood.\n\nI love how you make ordinary moments feel special. The simple talks, the jokes we share, the times we just sit and exist together—those moments are my favorite. They remind me that love isn’t only about big gestures. It’s about choosing to show up, choosing to care, choosing to stay kind even when things aren’t easy. With you, I’ve learned that comfort can be beautiful. I’ve learned that peace can feel like home.\n\nYou inspire me to be better—not in a pressured way, but in a gentle way. You make me want to grow, to be more patient, to be more understanding, to be braver with my feelings. When I doubt myself, you remind me of my worth. When I’m scared to try, you encourage me to take the step anyway. You don’t just love me; you believe in me, and that’s something I hold close to my heart.\n\nI know we’re both still learning. We’re learning how to communicate, how to handle misunderstandings, how to be there for each other when life gets tough. There will be days when we don’t agree, days when we’re tired, days when emotions run high. But I want you to know that I choose to work through those days with you. I choose patience over pride. I choose honesty over silence. I choose us, not because we’re perfect, but because we’re willing to grow together.\n\nIf I ever get quiet, please know it doesn’t mean I love you any less. Sometimes my heart just needs a moment to breathe. And if you ever feel unsure, I hope you remember this: you matter to me. Your feelings matter to me. Your dreams matter to me. I care about the things that make you excited, the things that worry you, and the things you’re still figuring out. I want to be someone who supports you, not someone who holds you back.\n\nI admire your strength, even when you don’t see it in yourself. I admire how you try, how you keep going, how you show up for the people you care about. You don’t have to be perfect for me to love you. I love you for who you are, for the effort you give, for the heart you carry. And on the days you feel like you’re not enough, I hope you hear my voice in your mind telling you that you are more than enough.\n\nBeing with you makes me hopeful about the future—not in a pressured way, but in a gentle, steady way. I imagine more shared laughs, more late-night talks, more quiet moments where everything feels okay because we’re together. I don’t know exactly what tomorrow will bring, but I know I want to face it with you by my side, learning, growing, and choosing each other again and again.\n\nThank you for being my safe place. Thank you for being my comfort. Thank you for being my favorite person to talk to when my day has been long. Thank you for reminding me that love can be kind, patient, and real. I promise to keep trying to be someone who listens, who understands, and who shows love not just with words, but with actions.\n\nNo matter how busy life gets, no matter how loud the world becomes, I hope you always remember this: you are important to me. You are valued. You are cared for deeply. I’m proud of you for who you are and for who you’re becoming. And I’m grateful that out of all the people in this world, I get to walk this part of life with you.\n\nWith all my love,\nAlways yours 🤍`;

        function unlock() {
            if(document.getElementById('pass').value.toLowerCase() === "mylove") {
                document.getElementById('lock').style.display = "none";
                document.getElementById('question-area').style.display = "block";
            } else { alert("Try again, love! 🌸"); }
        }

        function showEnvelope() {
            document.getElementById('question-area').style.display = "none";
            document.getElementById('envelope-wrapper').style.display = "block";
        }

        function revealLetter() {
            document.getElementById('env').classList.add('open');
            setTimeout(() => {
                document.getElementById('envelope-wrapper').style.display = "none";
                document.getElementById('content').style.display = "block";
                setTimeout(() => document.getElementById('content').style.opacity = "1", 50);
                
                setInterval(createHeart, 400);
                typeWriter();
                generateLoves();
            }, 600);
        }

        let charIdx = 0;
        function typeWriter() {
            if (charIdx < fullLetter.length) {
                document.getElementById('letterText').innerHTML += fullLetter.charAt(charIdx);
                charIdx++;
                setTimeout(typeWriter, 25);
            }
        }

        function generateLoves() {
            const container = document.getElementById('thousand-loves');
            const icons = ['✨', '💖', '🧸', '🌸', '🎀'];
            let count = 0;
            const interval = setInterval(() => {
                if (count >= 1000) { clearInterval(interval); return; }
                const span = document.createElement('span');
                span.className = 'love-note';
                span.textContent = `I love you ${icons[count % icons.length]}`;
                span.style.color = count % 2 === 0 ? '#ff85a1' : '#ffafcc';
                container.appendChild(span);
                count++;
            }, 40);
        }

        function createHeart() {
            const h = document.createElement('div');
            h.classList.add('floating-heart');
            h.innerHTML = ['🍓', '🎀', '☁️', '💖', '🧸'][Math.floor(Math.random() * 5)];
            h.style.left = Math.random() * 100 + "vw";
            h.style.fontSize = (Math.random() * 20 + 20) + "px";
            document.body.appendChild(h);
            setTimeout(() => h.remove(), 4000);
        }
    </script>
</body>
</html>
