<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Mental Health Check</title>
    <style>
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
        }

        body {
            background-color: #f0f2f5;
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
            padding: 20px;
        }

        .container {
            flex-grow: 1;
            display: flex;
            justify-content: center;
            align-items: center;
            position: relative;
            overflow: hidden;
        }

        .card {
            background: white;
            border-radius: 8px;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
            width: 100%;
            max-width: 600px;
            padding: 24px;
            position: relative;
            z-index: 1;
        }

        .welcome {
            text-align: center;
            margin-bottom: 30px;
        }

        .welcome h1 {
            font-size: 28px;
            color: #1a1a1a;
            margin-bottom: 15px;
        }

        .welcome p {
            font-size: 18px;
            color: #666;
            margin-bottom: 25px;
        }

        .button-group {
            display: flex;
            gap: 15px;
            justify-content: center;
            margin-top: 20px;
        }

        .button {
            padding: 12px 30px;
            border-radius: 25px;
            border: none;
            font-size: 16px;
            cursor: pointer;
            transition: transform 0.2s, background-color 0.2s;
        }

        .button:hover {
            transform: scale(1.05);
        }

        .button-primary {
            background-color: #0066cc;
            color: white;
        }

        .button-secondary {
            background-color: #e0e0e0;
            color: #333;
        }

        .heart {
            position: absolute;
            font-size: 20px;
            animation: falling linear infinite;
            z-index: 0;
        }

        @keyframes falling {
            0% {
                transform: translateY(-100vh) rotate(0deg);
            }
            100% {
                transform: translateY(100vh) rotate(360deg);
            }
        }

        .tiktok-credit {
            text-align: center;
            padding: 15px;
            background-color: white;
            color: #666;
            font-size: 14px;
            box-shadow: 0 -2px 4px rgba(0, 0, 0, 0.1);
            position: fixed;
            bottom: 0;
            left: 0;
            right: 0;
        }

        #confirmDialog {
            display: none;
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background: white;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
            z-index: 2;
            text-align: center;
        }

        .overlay {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: rgba(0, 0, 0, 0.5);
            z-index: 1;
        }

        /* Quiz styles */
        .card-title {
            font-size: 24px;
            font-weight: bold;
            text-align: center;
            margin-bottom: 24px;
            color: #1a1a1a;
        }

        .question-counter {
            font-size: 18px;
            margin-bottom: 16px;
            color: #666;
        }

        .question-text {
            font-size: 18px;
            margin-bottom: 24px;
            color: #1a1a1a;
        }

        .options {
            display: flex;
            flex-direction: column;
            gap: 12px;
        }

        .option-button {
            width: 100%;
            padding: 12px 16px;
            border: 1px solid #ddd;
            border-radius: 6px;
            background: white;
            text-align: left;
            font-size: 16px;
            cursor: pointer;
            transition: all 0.2s;
        }

        .option-button:hover {
            background: #f5f5f5;
            border-color: #999;
        }

        .result {
            background: #f8f9fa;
            border: 1px solid #ddd;
            border-radius: 6px;
            padding: 20px;
            margin-bottom: 20px;
        }

        .hidden {
            display: none;
        }
    </style>
</head>
<body>
    <audio id="bgMusic" loop>
        <source src="https://cdnjs.cloudflare.com/audio/blue-yung-kai.mp3" type="audio/mp3">
    </audio>

    <div class="container">
        <div class="card" id="welcome-container">
            <div class="welcome">
                <h1>Apakah kamu merasa lelah? 😔</h1>
                <p>Ingin cek mental health kamu?</p>
                <div class="button-group">
                    <button class="button button-primary" onclick="startQuiz()">Ya</button>
                    <button class="button button-secondary" onclick="showConfirmDialog()">Tidak</button>
                </div>
            </div>
        </div>

        <div class="card hidden" id="quiz-container">
            <h1 class="card-title">Tes Skrining Depresi</h1>
            <div class="question-counter">
                Pertanyaan <span id="current-question">1</span> dari <span id="total-questions">5</span>
            </div>
            <div id="question-text" class="question-text"></div>
            <div id="options" class="options"></div>
        </div>

        <div class="card hidden" id="result-container">
            <div class="result">
                <div class="result-title">Hasil Tes</div>
                <div id="result-message" class="result-message"></div>
            </div>
            <button class="button button-primary" onclick="restartQuiz()">Mulai Ulang Tes</button>
        </div>
    </div>

    <div id="confirmDialog">
        <h2>Yakin dek? 🥺</h2>
        <div class="button-group">
            <button class="button button-primary" onclick="startQuiz()">Ya, saya mau cek</button>
            <button class="button button-secondary" onclick="hideConfirmDialog()">Nanti saja</button>
        </div>
    </div>

    <div class="overlay" id="overlay"></div>

    <div class="tiktok-credit">
        @kaitosen1412 ❤️
    </div>

    <script>
        const questions = [
            {
                text: "Selama 2 minggu terakhir, seberapa sering Anda merasa tidak berminat atau tidak bergairah dalam melakukan apapun?",
                options: [
                    { text: "Tidak pernah", score: 0 },
                    { text: "Beberapa hari", score: 1 },
                    { text: "Lebih dari seminggu", score: 2 },
                    { text: "Hampir setiap hari", score: 3 }
                ]
            },
            {
                text: "Selama 2 minggu terakhir, seberapa sering Anda merasa murung, sedih, atau putus asa?",
                options: [
                    { text: "Tidak pernah", score: 0 },
                    { text: "Beberapa hari", score: 1 },
                    { text: "Lebih dari seminggu", score: 2 },
                    { text: "Hampir setiap hari", score: 3 }
                ]
            },
            {
                text: "Selama 2 minggu terakhir, seberapa sering Anda mengalami kesulitan tidur atau tidur terlalu banyak?",
                options: [
                    { text: "Tidak pernah", score: 0 },
                    { text: "Beberapa hari", score: 1 },
                    { text: "Lebih dari seminggu", score: 2 },
                    { text: "Hampir setiap hari", score: 3 }
                ]
            },
            {
                text: "Selama 2 minggu terakhir, seberapa sering Anda merasa lelah atau kurang bertenaga?",
                options: [
                    { text: "Tidak pernah", score: 0 },
                    { text: "Beberapa hari", score: 1 },
                    { text: "Lebih dari seminggu", score: 2 },
                    { text: "Hampir setiap hari", score: 3 }
                ]
            },
            {
                text: "Selama 2 minggu terakhir, seberapa sering Anda kehilangan nafsu makan atau makan berlebihan?",
                options: [
                    { text: "Tidak pernah", score: 0 },
                    { text: "Beberapa hari", score: 1 },
                    { text: "Lebih dari seminggu", score: 2 },
                    { text: "Hampir setiap hari", score: 3 }
                ]
            }
        ];

        let currentQuestion = 0;
        let score = 0;

        // Create falling hearts
        function createHeart() {
            const heart = document.createElement('div');
            heart.className = 'heart';
            heart.innerHTML = '❤️';
            heart.style.left = Math.random() * 100 + 'vw';
            heart.style.animationDuration = Math.random() * 3 + 2 + 's';
            document.body.appendChild(heart);

            heart.addEventListener('animationend', () => {
                heart.remove();
            });
        }

        // Create hearts periodically
        setInterval(createHeart, 300);

        // Music control
        const bgMusic = document.getElementById('bgMusic');
        document.addEventListener('click', () => {
            bgMusic.play().catch(err => console.log('Autoplay prevented'));
        });

        function showConfirmDialog() {
            document.getElementById('confirmDialog').style.display = 'block';
            document.getElementById('overlay').style.display = 'block';
        }

        function hideConfirmDialog() {
            document.getElementById('confirmDialog').style.display = 'none';
            document.getElementById('overlay').style.display = 'none';
        }

        function startQuiz() {
            document.getElementById('welcome-container').style.display = 'none';
            document.getElementById('confirmDialog').style.display = 'none';
            document.getElementById('overlay').style.display = 'none';
            document.getElementById('quiz-container').classList.remove('hidden');
            showQuestion();
        }

        function showQuestion() {
            document.getElementById('current-question').textContent = currentQuestion + 1;
            document.getElementById('total-questions').textContent = questions.length;
            document.getElementById('question-text').textContent = questions[currentQuestion].text;
            
            const optionsContainer = document.getElementById('options');
            optionsContainer.innerHTML = '';
            
            questions[currentQuestion].options.forEach((option, index) => {
                const button = document.createElement('button');
                button.className = 'option-button';
                button.textContent = option.text;
                button.onclick = () => handleAnswer(option.score);
                optionsContainer.appendChild(button);
            });
        }

        function handleAnswer(optionScore) {
            score += optionScore;
            
            if (currentQuestion + 1 < questions.length) {
                currentQuestion++;
                showQuestion();
            } else {
                showResult();
            }
        }

        function getResultMessage() {
            if (score <= 4) {
                return {
                    severity: "Minimal",
                    message: "Anda memiliki gejala depresi minimal. Tetap jaga kesehatan mental Anda dengan menerapkan pola hidup sehat."
                };
            } else if (score <= 9) {
                return {
                    severity: "Ringan",
                    message: "Anda memiliki gejala depresi ringan. Pertimbangkan untuk berbicara dengan profesional kesehatan mental."
                };
            } else if (score <= 14) {
                return {
                    severity: "Sedang",
                    message: "Anda memiliki gejala depresi sedang. Disarankan untuk berkonsultasi dengan profesional kesehatan mental."
                };
            } else {
                return {
                    severity: "Berat",
                    message: "Anda memiliki gejala depresi berat. Segera cari bantuan profesional kesehatan mental."
                };
            }
        }

        function showResult() {
            document.getElementById('quiz-container').classList.add('hidden');
            document.getElementById('result-container').classList.remove('hidden');
            
            const result = getResultMessage();
            document.getElementById('result-message').innerHTML = `
                <p><strong>Tingkat Depresi: ${result.severity}</strong></p>
                <p style="margin-top: 12px">${result.message}</p>
            `;
        }

        function restartQuiz() {
            currentQuestion = 0;
            score = 0;
            document.getElementById('welcome-container').style.display = 'block';
            document.getElementById('result-container').classList.add('hidden');
            document.getElementById('quiz-container').classList.add('hidden');
        }
    </script>
</body>
</html>
