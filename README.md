<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>러닝 타입 테스트</title>

    <style>
        @font-face {
            font-family: 'Uiyeun';
            src: url('https://fastly.jsdelivr.net/gh/projectnoonnu/noonfonts_2105@1.1/Uiyeun.woff') format('woff');
            font-weight: normal;
            font-style: normal;
        }

        html, body {
            font-family: 'Uiyeun'; 
            margin: 0;
            padding: 0;
            height: 100%;  
            overflow-y: auto; 
        }

        body {
            background-color: #f5f5f5;
            background-image: url('images/배경.png');
            background-size: cover;  
            background-position: center center;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            font-size: 18px;  
        }

        .container {
            text-align: center;
            background: white;
            padding: 30px;
            border-radius: 10px;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
            width: 90%;
            max-width: 600px;
            overflow: hidden;  
        }

        h1 {
            color: #333;
            font-size: 36px;  
            margin-bottom: 20px;
        }

        button {
            background-color: #ffb6ea;
            color: rgb(69, 40, 66);
            padding: 20px 40px; 
            border: none;
            border-radius: 8px;
            cursor: pointer;
            font-size: 24px;  
            font-family: 'Uiyeun'; 
        }

        button:hover {
            background-color: #ee4c9a;
        }

        .hidden {
            display: none;
        }

        .result img {
            width: 100%;  
            max-width: 800px;  
            height: auto;  
            margin-bottom: 20px;
        }
    </style>
</head>
<body>
    <div class="container" id="intro">
        <h1>러닝 타입 테스트</h1>
        <p>나의 달리기 타입과 찰떡인 동물은?</p>
        <button onclick="startTest()">테스트 시작하기</button>
    </div>

    <div class="container hidden" id="question">
        <h1 id="question-text">질문</h1>
        <button onclick="answerQuestion('yes')">예</button>
        <button onclick="answerQuestion('no')">아니오</button>
    </div>

    <div class="container hidden" id="result">
        <h1>테스트 결과</h1>
        <div class="result">
            <img id="result-image" src="" alt="결과 이미지">
            <p id="result-description"></p>
        </div>
        <button onclick="restartTest()">다시 테스트하기</button>
    </div>

    <script>
        const questions = [
            // ... your questions here ...
        ];

        const results = {
            // ... your result data here ...
        };

        let currentQuestion = 0;
        let answers = [];

        function startTest() {
            document.getElementById("intro").classList.add("hidden");
            document.getElementById("question").classList.remove("hidden");
            showQuestion();
        }

        function showQuestion() {
            const questionText = document.getElementById("question-text");
            questionText.textContent = questions[currentQuestion];
        }

        function answerQuestion(answer) {
            answers.push(answer);  
            currentQuestion++;  
            if (currentQuestion < questions.length) {
                showQuestion();  
            } else {
                showResult();  
            }
        }

        function showResult() {
            const resultType = calculateResult();  
            const resultData = results[resultType];  

            document.getElementById("question").classList.add("hidden");  
            document.getElementById("result").classList.remove("hidden");  

            document.getElementById("result-image").src = resultData.image;
            document.getElementById("result-description").textContent = resultData.description;
        }

        function calculateResult() {
            const yesCount = answers.filter(a => a === 'yes').length;

            if (yesCount >= 28) return "ENTJ";
            if (yesCount >= 24) return "ENFJ";
            if (yesCount >= 20) return "ESTJ";
            if (yesCount >= 16) return "ESFJ";
            if (yesCount >= 12) return "ISTJ";
            if (yesCount >= 8) return "ISFJ";
            if (yesCount >= 4) return "INTJ";
            return "INFP";  
        }

        function restartTest() {
            answers = [];
            currentQuestion = 0;
            document.getElementById("result").classList.add("hidden");
            document.getElementById("intro").classList.remove("hidden");
        }
    </script>
</body>
</html>
