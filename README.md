<!DOCTYPE html>
<html lang="uk">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Вікторина для Адріани</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            background-color: #ffe4e1;
            padding: 20px;
        }
        .question {
            font-size: 1.5em;
            margin-bottom: 20px;
        }
        .options {
            display: flex;
            flex-direction: column;
            gap: 10px;
        }
        button {
            font-size: 1.2em;
            padding: 10px;
            border: none;
            cursor: pointer;
            background-color: #ff69b4;
            color: white;
            transition: 0.3s;
        }
        #loveMessage {
            display: none;
            font-size: 2em;
            color: red;
            margin-top: 20px;
        }
        #valentineImage {
            display: none;
            width: 200px;
            margin-top: 20px;
        }
    </style>
</head>
<body>
    <h1>Привіт, Адріана!</h1>
    <p>Це твій коханий Таросік, і щоб отримати свою валентинку тобі треба відповісти правильно на 5 запитань. (за підсказками можеш звертатись до мене на пряму)</p>
    
    <div id="quiz">
        <div id="questionContainer">
            <p class="question" id="questionText">1. Де ми познайомились?</p>
            <div class="options" id="optionsContainer"></div>
        </div>
        <p id="feedback" style="color: red; font-size: 1.2em; display: none;">Неправильно, подумай краще</p>
    </div>
    
    <p id="loveMessage">Я також тебе кохаю ❤️</p>
    <img id="valentineImage" src="https://i.imgur.com/YjRl6kD.png" alt="Валентинка">
    
    <script>
        const questions = [
            { 
                text: "1. Де ми познайомились?", 
                correct: "в UNIT.City", 
                options: ["в мене на день народженні", "на озері", "в парку", "в UNIT.City"]
            },
            { 
                text: "2. Як я був тобі на перший погляд?", 
                correct: "не сподобався", 
                options: ["дуже сподобався", "відразу боготворила", "стошнило", "не сподобався"]
            },
            { 
                text: "3. В яку подорож ми вперше поїхали?", 
                correct: "в Луцьк", 
                options: ["в Буковель", "за кордон", "фіг а не подорож кудись", "в Луцьк"]
            },
            { 
                text: "4. Де я зробив тобі пропозицію?", 
                correct: "на катку на Зимовій Країні", 
                options: ["вдома", "в Буковелі", "на Новий Рік", "на катку на Зимовій Країні"]
            },
            { 
                text: "5. Чи ти мене кохаєш?", 
                correct: "Так", 
                options: ["Ні", "Я не знаю", "Так"]
            }
        ];
        
        let currentQuestion = 0;
        let yesMoves = 0;
        const questionText = document.getElementById("questionText");
        const optionsContainer = document.getElementById("optionsContainer");
        const feedback = document.getElementById("feedback");
        const loveMessage = document.getElementById("loveMessage");
        const valentineImage = document.getElementById("valentineImage");
        
        function loadQuestion() {
            feedback.style.display = "none";
            questionText.innerText = questions[currentQuestion].text;
            optionsContainer.innerHTML = "";
            
            let shuffledOptions = [...questions[currentQuestion].options].sort(() => Math.random() - 0.5);
            shuffledOptions.forEach(option => {
                let btn = document.createElement("button");
                btn.innerText = option;
                btn.onclick = () => checkAnswer(option);
                if (currentQuestion === 4 && option === "Так") {
                    btn.id = "yesButton";
                    btn.style.position = "absolute";
                }
                optionsContainer.appendChild(btn);
            });
        }
        
        function checkAnswer(answer) {
            if (answer === questions[currentQuestion].correct) {
                currentQuestion++;
                if (currentQuestion < questions.length) {
                    loadQuestion();
                } else {
                    showLoveMessage();
                }
            } else {
                feedback.style.display = "block";
            }
        }
        
        function showLoveMessage() {
            document.getElementById("quiz").style.display = "none";
            loveMessage.style.display = "block";
            valentineImage.style.display = "block";
        }
        
        document.body.addEventListener("mouseover", function(event) {
            if (event.target.id === "yesButton" && yesMoves < 3) {
                let x = Math.random() * (window.innerWidth - 100);
                let y = Math.random() * (window.innerHeight - 100);
                event.target.style.left = `${x}px`;
                event.target.style.top = `${y}px`;
                yesMoves++;
            }
        });
        
        loadQuestion();
    </script>
</body>
</html>
