<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=yes">
    <title>Simulado PF - 20 Questões</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'Arial', 'Helvetica', sans-serif;
            background: #0b2b3d;
            min-height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
            padding: 15px;
        }
        
        .quiz-container {
            width: 100%;
            max-width: 650px;
            background: #FFFFFF;
            border-radius: 30px;
            padding: 25px;
            box-shadow: 0 20px 40px rgba(0,0,0,0.4);
            border: 4px solid #ffcc00;
        }
        
        .quiz-header {
            text-align: center;
            margin-bottom: 20px;
        }
        
        .quiz-title {
            color: #0b2b3d;
            font-size: 28px;
            font-weight: 800;
            margin-bottom: 5px;
            text-transform: uppercase;
        }
        
        .quiz-subtitle {
            color: #0b2b3d;
            font-size: 16px;
            font-weight: 600;
            border-top: 2px solid #ffcc00;
            border-bottom: 2px solid #ffcc00;
            display: inline-block;
            padding: 5px 15px;
        }
        
        .progress-container {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin: 15px 0;
            padding: 8px 12px;
            background: #e6f0fa;
            border-radius: 50px;
            border: 2px solid #ffcc00;
        }
        
        .question-counter {
            background: #0b2b3d;
            color: white;
            font-size: 16px;
            font-weight: bold;
            padding: 6px 15px;
            border-radius: 30px;
            border: 2px solid #ffcc00;
            min-width: 70px;
            text-align: center;
        }
        
        .progress-bar {
            flex: 1;
            height: 16px;
            background: #b0c4de;
            border-radius: 20px;
            margin: 0 12px;
            overflow: hidden;
            border: 1px solid #ffcc00;
        }
        
        .progress-fill {
            height: 100%;
            background: linear-gradient(90deg, #0b2b3d, #ffcc00);
            width: 0%;
            transition: width 0.3s ease;
        }
        
        .category-badge {
            background: #0b2b3d;
            color: white;
            font-size: 12px;
            font-weight: bold;
            padding: 5px 10px;
            border-radius: 30px;
            border: 2px solid #ffcc00;
            min-width: 90px;
            text-align: center;
        }
        
        .timer-container {
            text-align: center;
            margin: 10px 0;
        }
        
        .timer {
            display: inline-block;
            background: #0b2b3d;
            color: white;
            font-size: 28px;
            font-weight: bold;
            padding: 8px 20px;
            border-radius: 50px;
            border: 3px solid #ffcc00;
        }
        
        .question-area {
            background: #f0f5fa;
            border-radius: 15px;
            padding: 20px 15px;
            margin-bottom: 20px;
            border-left: 4px solid #0b2b3d;
            border-right: 4px solid #ffcc00;
        }
        
        .question-text {
            color: #0b2b3d;
            font-size: 18px;
            font-weight: 600;
            text-align: left;
            line-height: 1.4;
        }
        
        .options-container {
            display: flex;
            flex-direction: row;
            justify-content: center;
            gap: 20px;
            margin-bottom: 20px;
            flex-wrap: wrap;
        }
        
        .option-btn-ce {
            background: white;
            border: 3px solid #0b2b3d;
            border-radius: 50px;
            padding: 15px 35px;
            color: #0b2b3d;
            font-size: 22px;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.2s ease;
            min-width: 130px;
        }
        
        .option-btn-ce:hover:not(:disabled) {
            background: #0b2b3d;
            color: white;
            transform: translateY(-2px);
        }
        
        .option-btn-ce.selected {
            background: #0b2b3d;
            color: white;
            border-color: #ffcc00;
        }
        
        .option-btn-ce.correct {
            background: #2e7d32;
            border-color: #ffcc00;
            color: white;
        }
        
        .option-btn-ce.incorrect {
            background: #c62828;
            border-color: #ffcc00;
            color: white;
        }
        
        .option-btn-ce:disabled {
            opacity: 0.9;
            cursor: default;
            transform: none;
        }
        
        .loading-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(255,255,255,0.95);
            display: flex;
            align-items: center;
            justify-content: center;
            z-index: 1000;
            display: none;
        }
        
        .loading-content {
            background: white;
            padding: 30px;
            border-radius: 30px;
            text-align: center;
            border: 4px solid #0b2b3d;
        }
        
        .loading-spinner {
            width: 50px;
            height: 50px;
            border: 5px solid #b0c4de;
            border-top-color: #0b2b3d;
            border-radius: 50%;
            animation: spin 1s linear infinite;
            margin: 15px auto;
        }
        
        @keyframes spin {
            to { transform: rotate(360deg); }
        }
        
        .result-screen {
            text-align: center;
        }
        
        .final-score {
            background: linear-gradient(135deg, #0b2b3d, #1a4b6d);
            border-radius: 20px;
            padding: 25px;
            margin: 15px 0;
            color: white;
            border: 4px solid #ffcc00;
        }
        
        .score-number {
            font-size: 60px;
            font-weight: bold;
            margin: 10px 0;
        }
        
        .score-label {
            font-size: 22px;
        }
        
        .level-result {
            font-size: 20px;
            margin: 15px 0;
            padding: 10px;
            background: rgba(255,204,0,0.2);
            border-radius: 50px;
            border: 2px solid #ffcc00;
        }
        
        .action-btn {
            background: white;
            border: none;
            border-radius: 15px;
            padding: 15px;
            color: #0b2b3d;
            font-size: 18px;
            font-weight: bold;
            cursor: pointer;
            width: 100%;
            margin: 8px 0;
            border: 3px solid #ffcc00;
            transition: all 0.2s ease;
        }
        
        .action-btn:hover {
            transform: translateY(-2px);
            background: #f0f5fa;
        }
        
        .name-input {
            width: 100%;
            padding: 12px;
            font-size: 16px;
            border-radius: 15px;
            border: 3px solid #ffcc00;
            margin: 8px 0;
            color: #0b2b3d;
        }
        
        .name-input::placeholder {
            color: #95a5a6;
        }
        
        .stats-container {
            display: flex;
            justify-content: space-around;
            margin: 10px 0;
            padding: 8px;
            background: #e6f0fa;
            border-radius: 10px;
            font-weight: bold;
        }
        
        .stats-correct { color: #2e7d32; }
        .stats-wrong { color: #c62828; }
        
        @media (max-width: 480px) {
            .quiz-title { font-size: 22px; }
            .question-text { font-size: 16px; }
            .option-btn-ce { 
                font-size: 20px; 
                padding: 12px 25px;
                min-width: 110px;
            }
            .progress-container { 
                flex-direction: column; 
                gap: 8px; 
            }
            .progress-bar { 
                width: 100%; 
                margin: 8px 0; 
            }
            .category-badge { 
                min-width: 100%; 
            }
        }
    </style>
</head>
<body>
    <div class="quiz-container">
        <div id="quizContent"></div>
    </div>

    <div id="loading" class="loading-overlay">
        <div class="loading-content">
            <div class="loading-spinner"></div>
            <div style="font-size: 18px; color: #0b2b3d;">Carregando...</div>
        </div>
    </div>

    <script>
        const CONCURSO_LINK = "https://s.shopee.com.br/8pgTuA2wJ7";

        // 20 QUESTÕES BASEADAS NO PDF DA PF
        const questions = [
            // LÍNGUA PORTUGUESA (1-5)
            {
                question: "📝 'No texto 'Ninguém sabe o bastante para ser um pessimista', a palavra 'bastante' é um advérbio e, portanto, invariável.'",
                options: ["CERTO", "ERRADO"],
                answer: 1, // CERTO
                category: "PORTUGUÊS"
            },
            {
                question: "📝 'Nas comunicações oficiais, deve-se evitar o emprego de palavras e expressões simples, assim como o de frases curtas.'",
                options: ["CERTO", "ERRADO"],
                answer: 2, // ERRADO (deve-se usar linguagem clara)
                category: "PORTUGUÊS"
            },
            {
                question: "📝 'No corpo do texto de uma correspondência oficial, os pronomes de tratamento podem ser empregados em sua forma abreviada ou por extenso.'",
                options: ["CERTO", "ERRADO"],
                answer: 1, // CERTO
                category: "PORTUGUÊS"
            },
            
            // RACIOCÍNIO LÓGICO (4-6)
            {
                question: "🧮 'A proposição P: 'Não quero debate, mas não tenho receio de debater' tem tabela-verdade com mais de 5 linhas.'",
                options: ["CERTO", "ERRADO"],
                answer: 2, // ERRADO (tem 4 linhas)
                category: "LÓGICA"
            },
            {
                question: "🧮 'A proposição P é equivalente à negação de 'Se não quero debate, então tenho receio de debater.''",
                options: ["CERTO", "ERRADO"],
                answer: 1, // CERTO
                category: "LÓGICA"
            },
            
            // ÉTICA (7-9)
            {
                question: "⚖️ 'Advertência, suspensão e demissão são penas aplicáveis ao servidor público pela comissão de ética.'",
                options: ["CERTO", "ERRADO"],
                answer: 2, // ERRADO (comissão aplica censura)
                category: "ÉTICA"
            },
            {
                question: "⚖️ 'O Código de Ética estabelece como dever do servidor a imediata comunicação a seus superiores de qualquer ato contrário ao interesse público.'",
                options: ["CERTO", "ERRADO"],
                answer: 1, // CERTO
                category: "ÉTICA"
            },
            {
                question: "⚖️ 'A moralidade é princípio que rege a atuação da administração pública.'",
                options: ["CERTO", "ERRADO"],
                answer: 1, // CERTO
                category: "ÉTICA"
            },
            
            // LEI 8.112 (10-11)
            {
                question: "📋 'A penalidade de suspensão não pode exceder o prazo de 90 dias.'",
                options: ["CERTO", "ERRADO"],
                answer: 1, // CERTO
                category: "LEI 8.112"
            },
            {
                question: "📋 'Zelar pela economia do material utilizado no exercício de suas funções é dever do servidor público.'",
                options: ["CERTO", "ERRADO"],
                answer: 1, // CERTO
                category: "LEI 8.112"
            },
            
            // INFORMÁTICA (12-14)
            {
                question: "💻 'LAN é uma rede restrita a um único ambiente físico, como escritório ou escola.'",
                options: ["CERTO", "ERRADO"],
                answer: 1, // CERTO
                category: "INFORMÁTICA"
            },
            {
                question: "💻 'No Windows 10, o recurso Visão de Tarefas permite visualizar tarefas em segundo plano do Gerenciador de Tarefas.'",
                options: ["CERTO", "ERRADO"],
                answer: 2, // ERRADO
                category: "INFORMÁTICA"
            },
            {
                question: "💻 'No Excel, a fórmula =CONT.SE(A2:A200;'furto') conta quantas vezes 'furto' aparece no intervalo.'",
                options: ["CERTO", "ERRADO"],
                answer: 1, // CERTO
                category: "INFORMÁTICA"
            },
            
            // GESTÃO PÚBLICA (15-17)
            {
                question: "🏛️ 'A departamentalização funcional gera eficiência mediante especialização das atividades.'",
                options: ["CERTO", "ERRADO"],
                answer: 1, // CERTO
                category: "GESTÃO"
            },
            {
                question: "🏛️ 'A terceira etapa do ciclo PDCA associa-se à coleta de informações sobre resultados obtidos (verificar).'",
                options: ["CERTO", "ERRADO"],
                answer: 1, // CERTO
                category: "GESTÃO"
            },
            {
                question: "🏛️ 'Ambiente de trabalho agradável contribui para a motivação e alcance de objetivos.'",
                options: ["CERTO", "ERRADO"],
                answer: 1, // CERTO
                category: "GESTÃO"
            },
            
            // LICITAÇÕES (18-20)
            {
                question: "📑 'A planilha de custos é base para análise da exequibilidade da proposta de preços em serviços de limpeza.'",
                options: ["CERTO", "ERRADO"],
                answer: 1, // CERTO
                category: "LICITAÇÕES"
            },
            {
                question: "📑 'Sanções em contratações públicas restringem-se a advertência, multa e impedimento de licitar.'",
                options: ["CERTO", "ERRADO"],
                answer: 2, // ERRADO
                category: "LICITAÇÕES"
            },
            {
                question: "📦 'Itens natalinos apresentam demanda de natureza irregular.'",
                options: ["CERTO", "ERRADO"],
                answer: 1, // CERTO
                category: "LOGÍSTICA"
            }
        ];

        const TOTAL_QUESTIONS = questions.length;
        let current = 0;
        let score = 0;
        let answered = false;
        let userAnswers = [];
        let timer;
        let timeLeft = 60;

        function startTimer() {
            clearInterval(timer);
            timeLeft = 60;
            updateTimerDisplay();
            
            timer = setInterval(() => {
                timeLeft--;
                updateTimerDisplay();
                if (timeLeft <= 0) {
                    clearInterval(timer);
                    if (!answered) {
                        userAnswers.push(0);
                        nextQuestion();
                    }
                }
            }, 1000);
        }

        function updateTimerDisplay() {
            const timerEl = document.getElementById('timer');
            if (timerEl) timerEl.textContent = `⏳ ${timeLeft}s`;
        }

        function showQuestion() {
            answered = false;
            const q = questions[current];
            
            let html = `
                <div class="quiz-header">
                    <div class="quiz-title">SIMULADO PF</div>
                    <div class="quiz-subtitle">AGENTE ADMINISTRATIVO</div>
                    
                    <div class="progress-container">
                        <div class="question-counter">${current + 1}/${TOTAL_QUESTIONS}</div>
                        <div class="progress-bar">
                            <div class="progress-fill" style="width: ${((current + 1) / TOTAL_QUESTIONS) * 100}%"></div>
                        </div>
                        <div class="category-badge">${q.category}</div>
                    </div>
                    
                    <div class="timer-container">
                        <div class="timer" id="timer">⏳ 60s</div>
                    </div>
                </div>
                
                <div class="question-area">
                    <div class="question-text">${q.question}</div>
                </div>
                
                <div class="options-container">
                    <button class="option-btn-ce" onclick="selectOption(1)" id="btn-c">C - CERTO</button>
                    <button class="option-btn-ce" onclick="selectOption(2)" id="btn-e">E - ERRADO</button>
                </div>
            `;
            
            document.getElementById('quizContent').innerHTML = html;
            startTimer();
        }

        function selectOption(selected) {
            if (answered) return;
            answered = true;
            clearInterval(timer);
            
            const correct = questions[current].answer;
            const btnC = document.getElementById('btn-c');
            const btnE = document.getElementById('btn-e');
            
            btnC.classList.remove('selected', 'correct', 'incorrect');
            btnE.classList.remove('selected', 'correct', 'incorrect');
            
            if (selected === 1) {
                btnC.classList.add('selected');
            } else {
                btnE.classList.add('selected');
            }
            
            setTimeout(() => {
                if (correct === 1) {
                    btnC.classList.add('correct');
                    if (selected !== 1) btnE.classList.add('incorrect');
                } else {
                    btnE.classList.add('correct');
                    if (selected !== 2) btnC.classList.add('incorrect');
                }
                
                btnC.disabled = true;
                btnE.disabled = true;
                
                userAnswers.push(selected);
                if (selected === correct) {
                    score++;
                    if (typeof confetti !== 'undefined') {
                        confetti({ particleCount: 20, spread: 40, colors: ['#0b2b3d', '#ffcc00'] });
                    }
                }
                
                setTimeout(nextQuestion, 800);
            }, 300);
        }

        function nextQuestion() {
            current++;
            if (current < questions.length) {
                showQuestion();
            } else {
                showFinalScreen();
            }
        }

        function showFinalScreen() {
            let levelMessage = "";
            if (score >= 16) levelMessage = "APROVADO - Excelente! 🌟";
            else if (score >= 12) levelMessage = "CLASSIFICADO - Muito bem! 👍";
            else if (score >= 8) levelMessage = "HABILITADO - Bom desempenho! 💪";
            else levelMessage = "ESTUDE MAIS - Continue praticando! 📖";
            
            let html = `
                <div class="quiz-header">
                    <div class="quiz-title">SIMULADO PF</div>
                </div>
                
                <div class="result-screen">
                    <div class="final-score">
                        <div class="score-label">RESULTADO</div>
                        <div class="score-number">${score}/${TOTAL_QUESTIONS}</div>
                        <div class="stats-container">
                            <span class="stats-correct">✅ ${score} acertos</span>
                            <span class="stats-wrong">❌ ${TOTAL_QUESTIONS - score} erros</span>
                        </div>
                        <div class="level-result">${levelMessage}</div>
                    </div>
                    
                    <button class="action-btn" onclick="window.open('${CONCURSO_LINK}', '_blank')">
                        🔗 VER GABARITO
                    </button>
                    
                    <input type="text" class="name-input" id="participantName" 
                           placeholder="Digite seu nome">
                    <button class="action-btn" onclick="sendResults()">
                        💾 SALVAR NOTA
                    </button>
                </div>
            `;
            
            document.getElementById('quizContent').innerHTML = html;
        }

        function sendResults() {
            const name = document.getElementById('participantName')?.value.trim();
            if (!name) {
                alert('Digite seu nome!');
                return;
            }
            document.getElementById('loading').style.display = 'flex';
            setTimeout(() => {
                document.getElementById('loading').style.display = 'none';
                alert(`Parabéns ${name}! Você acertou ${score}/${TOTAL_QUESTIONS} questões.`);
            }, 1000);
        }

        // Inicia
        function start() {
            if (typeof confetti === 'undefined') {
                const script = document.createElement('script');
                script.src = 'https://cdn.jsdelivr.net/npm/canvas-confetti@1.6.0/dist/confetti.browser.min.js';
                script.onload = () => showQuestion();
                document.head.appendChild(script);
            } else {
                showQuestion();
            }
        }
        start();
    </script>
</body>
</html>
