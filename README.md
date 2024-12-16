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
            "목표를 세웠을 때, 계획을 세우는 것을 좋아하나요?",
            "혼자서 달리는 것보다 사람들과 함께하는 것을 선호하나요?",
            "러닝을 통해 내면적으로 성장하고 싶다고 느끼나요?",
            "즉흥적으로 달리기보다 루틴을 따르는 것을 좋아하나요?",
            "달리기를 통해 새로운 도전을 즐기고 싶나요?",
            "긴 시간을 달리는 것보다 짧은 시간을 집중해서 달리는 것을 선호하나요?",
            "달리기 전에 충분한 준비 운동을 하는 편인가요?",
            "새로운 훈련 방법을 시도하는 것을 좋아하나요?",
            "러닝을 통해 목표를 달성하고자 하는 강한 욕구가 있나요?",
            "운동 중에 다른 사람들의 피드백을 중요하게 생각하나요?",
            "달리기 중에 자주 자신과 대화를 나누는 편인가요?",
            "혼자 달리는 것보다 그룹 러닝을 선호하나요?",
            "주기적으로 자신의 성과를 체크하나요?",
            "러닝을 할 때, 환경이나 분위기를 중요하게 생각하나요?",
            "기록을 세우는 것을 중요한 목표로 삼나요?",
            "도전적인 목표를 설정하고 달성하려는 경향이 있나요?",
            "달리기에서 즐거움을 느끼기보다는 목표 달성에 집중하는 편인가요?",
            "경쟁을 좋아하는 편인가요?",
            "비교적 빠르게 달리기를 시작하고 끝까지 유지하는 편인가요?",
            "러닝 후에 성취감을 느끼는 편인가요?",
            "운동 후 몸의 상태를 체크하는 편인가요?",
            "달리기 중 다른 사람을 의식하지 않고 자신의 페이스를 유지하나요?",
            "실패해도 다시 도전하려는 의지가 강한가요?",
            "달리기를 통해 체력 향상에 관심이 있나요?",
            "루틴을 따르기보다는 자유롭게 달리기를 선호하나요?",
            "특정 목표를 설정하고 그 목표를 이루기 위해 달리나요?",
            "자신의 러닝 스타일에 대해 자주 고민하나요?",
            "주변 사람들의 반응을 중요한 요소로 생각하나요?",
            "주어진 환경에서 최선의 결과를 끌어내려고 노력하나요?",
            "팀을 이끄는 역할을 맡아본 적이 있나요?"
        ];

        const results = {
            ISTJ: {
                image: "images/거북이.png",
                description: "ISTJ - 꾸준한 루틴형 거북이 🐢: 매일의 루틴을 철저히 지켜나가는 성실한 러너입니다."
            },
            ISFJ: {
                image: "images/양.png",
                description: "ISFJ - 배려형 동반 주자 양 🐑: 주변 사람들과 함께 달리며 배려를 실천하는 러너입니다."
            },
            INFJ: {
                image: "images/비둘기.png",
                description: "INFJ - 내적 성장형 비둘기 🕊️: 내면의 평화와 성장을 추구하는 철학자형 러너입니다."
            },
            INTJ: {
                image: "images/부엉이.png",
                description: "INTJ - 전략적 목표 달성형 부엉이 🦉: 장기 목표를 설정하고 효율적으로 달리는 러너입니다."
            },
            ISTP: {
                image: "images/치타.png",
                description: "ISTP - 즉흥적 단거리 주자 치타 🐆: 순간적인 스피드와 민첩함을 자랑하는 즉흥 스프린터입니다."
            },
            ISFP: {
                image: "images/사슴.png",
                description: "ISFP - 감성적 자연 러너 사슴 🦌: 자연을 누비며 힐링을 즐기는 감성적인 러너입니다."
            },
            INFP: {
                image: "images/고양이.png",
                description: "INFP - 감정 이입형 도전가 고양이 🐱: 자유롭고 유연하게 달리는 감성적인 러너입니다."
            },
            INTP: {
                image: "images/두더지.png",
                description: "INTP - 분석형 효율 추구자 두더지 🦔: 데이터를 분석해 최적의 러닝 전략을 찾는 탐구형 러너입니다."
            },
            ESTP: {
                image: "images/뱀.png",
                description: "ESTP - 에너지 폭발형 스프린터 뱀 🐍: 날렵하게 기회를 노리는 에너지 넘치는 러너입니다."
            },
            ESFP: {
                image: "images/강아지.png",
                description: "ESFP - 흥겨운 이벤트형 강아지 🐶: 사람들과 함께 달리는 것을 즐기는 밝은 러너입니다."
            },
            ENFP: {
                image: "images/돌고래.png",
                description: "ENFP - 자유로운 도전형 돌고래 🐬: 새로운 것을 개척하며 활기차게 달리는 러너입니다."
            },
            ENTP: {
                image: "images/여우.png",
                description: "ENTP - 창의적 전략 러너 여우 🦊: 기발한 전략으로 새로운 훈련 방법을 시도하는 러너입니다."
            },
            ESTJ: {
                image: "images/사자.png",
                description: "ESTJ - 목표 달성형 리더 사자 🦁: 팀을 이끄는 강한 추진력의 리더형 러너입니다."
            },
            ESFJ: {
                image: "images/펭귄.png",
                description: "ESFJ - 사회적 응원 주자 펭귄 🐧: 주변을 응원하며 팀워크를 중시하는 긍정적인 러너입니다."
            },
            ENFJ: {
                image: "images/코끼리.png",
                description: "ENFJ - 동기 부여형 멘토 코끼리 🐘: 사람들에게 동기를 주며 든든하게 이끄는 멘토형 러너입니다."
            },
            ENTJ: {
                image: "images/호랑이.png",
                description: "ENTJ - 목표 지향적 리더 호랑이 🐯: 강력한 목표 지향성과 리더십을 발휘하는 러너입니다."
            }
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
            
            // 'yes'의 개수에 따라 결과를 다르게 할 수 있어
            if (yesCount >= 28) return "ENTJ";
            if (yesCount >= 24) return "ENFJ";
            if (yesCount >= 20) return "ESTJ";
            if (yesCount >= 16) return "ESFJ";
            if (yesCount >= 12) return "ISTJ";
            if (yesCount >= 8) return "ISFJ";
            if (yesCount >= 4) return "INTJ";
            return "INFP";  // 'yes'가 4개 이하일 경우
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

background-image: url('images/배경.png');
