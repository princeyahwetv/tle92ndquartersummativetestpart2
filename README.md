<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>HTML Fundamentals Quiz</title>
    <style>
        body {
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            margin: 0;
            padding: 20px;
            min-height: 100%;
        }

        html {
            height: 100%;
        }

        .quiz-container {
            max-width: 800px;
            margin: 0 auto;
            background: white;
            border-radius: 15px;
            box-shadow: 0 20px 40px rgba(0,0,0,0.1);
            overflow: hidden;
        }

        .timer {
            position: fixed;
            top: 20px;
            right: 20px;
            background: linear-gradient(135deg, #ff6b6b 0%, #ee5a24 100%);
            color: white;
            padding: 15px 20px;
            border-radius: 10px;
            font-size: 1.2rem;
            font-weight: 700;
            box-shadow: 0 10px 20px rgba(255, 107, 107, 0.3);
            z-index: 1000;
            min-width: 120px;
            text-align: center;
            display: none;
        }

        .timer.warning {
            animation: pulse 1s infinite;
        }

        @keyframes pulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.05); }
            100% { transform: scale(1); }
        }

        .quiz-header {
            background: linear-gradient(135deg, #28a745 0%, #ffd700 100%);
            color: white;
            padding: 30px;
            text-align: center;
        }

        .quiz-header h1 {
            margin: 0;
            font-size: 2.5rem;
            font-weight: 700;
        }

        .quiz-header p {
            margin: 10px 0 0 0;
            font-size: 1.1rem;
            opacity: 0.9;
        }

        .progress-bar {
            background: rgba(255,255,255,0.2);
            height: 8px;
            border-radius: 4px;
            margin-top: 20px;
            overflow: hidden;
        }

        .progress-fill {
            background: white;
            height: 100%;
            width: 0%;
            transition: width 0.3s ease;
            border-radius: 4px;
        }

        .student-form {
            padding: 40px;
        }

        .form-group {
            margin-bottom: 20px;
        }

        .form-group label {
            display: block;
            margin-bottom: 8px;
            font-weight: 600;
            color: #333;
        }

        .form-group input {
            width: 100%;
            padding: 12px 15px;
            border: 2px solid #e9ecef;
            border-radius: 8px;
            font-size: 1rem;
            transition: border-color 0.3s ease;
            box-sizing: border-box;
        }

        .form-group input:focus {
            outline: none;
            border-color: #28a745;
        }

        .form-row {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 20px;
        }

        .quiz-content {
            padding: 40px;
            display: none;
            position: relative;
        }

        .question {
            display: none;
            animation: fadeIn 0.5s ease;
        }

        .question.active {
            display: block;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .question-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 25px;
        }

        .question-number {
            background: #28a745;
            color: white;
            padding: 8px 16px;
            border-radius: 20px;
            font-weight: 600;
            font-size: 0.9rem;
        }

        .question-text {
            font-size: 1.3rem;
            font-weight: 600;
            color: #333;
            margin-bottom: 25px;
            line-height: 1.4;
        }

        .options {
            display: grid;
            gap: 15px;
        }

        .option {
            background: #f8f9fa;
            border: 2px solid #e9ecef;
            border-radius: 10px;
            padding: 18px 20px;
            cursor: pointer;
            transition: all 0.3s ease;
            font-size: 1.1rem;
            display: flex;
            align-items: center;
        }

        .option:hover {
            background: #e8f5e8;
            border-color: #28a745;
            transform: translateY(-2px);
        }

        .option.selected {
            background: #28a745;
            color: white;
            border-color: #28a745;
        }



        .option-letter {
            background: rgba(0,0,0,0.1);
            color: inherit;
            width: 30px;
            height: 30px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: 600;
            margin-right: 15px;
            flex-shrink: 0;
        }

        .quiz-controls {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-top: 40px;
            padding-top: 30px;
            border-top: 2px solid #f0f0f0;
        }

        .btn {
            padding: 12px 30px;
            border: none;
            border-radius: 25px;
            font-size: 1rem;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
            text-transform: uppercase;
            letter-spacing: 0.5px;
        }

        .btn-primary {
            background: linear-gradient(135deg, #28a745 0%, #ffd700 100%);
            color: white;
        }

        .btn-primary:hover {
            transform: translateY(-2px);
            box-shadow: 0 10px 20px rgba(40, 167, 69, 0.3);
        }

        .btn-secondary {
            background: #6c757d;
            color: white;
        }

        .btn-secondary:hover {
            background: #5a6268;
            transform: translateY(-2px);
        }

        .btn-success {
            background: linear-gradient(135deg, #28a745 0%, #20c997 100%);
            color: white;
            margin-right: 15px;
        }

        .btn-success:hover {
            transform: translateY(-2px);
            box-shadow: 0 10px 20px rgba(40, 167, 69, 0.3);
        }

        .btn-youtube {
            background: linear-gradient(135deg, #ff0000 0%, #cc0000 100%);
            color: white;
            margin-right: 15px;
        }

        .btn-youtube:hover {
            transform: translateY(-2px);
            box-shadow: 0 10px 20px rgba(255, 0, 0, 0.3);
        }

        .btn:disabled {
            opacity: 0.5;
            cursor: not-allowed;
            transform: none !important;
        }

        .results {
            display: none;
            text-align: center;
            padding: 40px;
        }

        .results.active {
            display: block;
        }

        .score-circle {
            width: 150px;
            height: 150px;
            border-radius: 50%;
            background: linear-gradient(135deg, #28a745 0%, #ffd700 100%);
            display: flex;
            align-items: center;
            justify-content: center;
            margin: 0 auto 30px;
            color: white;
            font-size: 2.5rem;
            font-weight: 700;
        }

        .results h2 {
            color: #333;
            font-size: 2rem;
            margin-bottom: 15px;
        }

        .results p {
            color: #666;
            font-size: 1.2rem;
            margin-bottom: 30px;
        }

        .score-breakdown {
            background: #f8f9fa;
            border-radius: 10px;
            padding: 25px;
            margin: 30px 0;
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
            gap: 20px;
        }

        .score-item {
            text-align: center;
        }

        .score-item .number {
            font-size: 2rem;
            font-weight: 700;
            color: #28a745;
        }

        .score-item .label {
            color: #666;
            font-size: 0.9rem;
            text-transform: uppercase;
            letter-spacing: 0.5px;
        }
    </style>
</head>
<body>
    <div class="timer" id="timer">10:00</div>

    <div class="quiz-container">
        <div class="quiz-header">
            <h1>HTML GRADE 9 SUMMATIVE TEST PART 2</h1>
            <p>Test your knowledge of HTML tags, attributes, and concepts</p>
            <div class="progress-bar">
                <div class="progress-fill" id="progressFill"></div>
            </div>
        </div>

        <!-- Student Information Form -->
        <div class="student-form" id="studentForm">
            <h2 style="margin-bottom: 30px; color: #333; text-align: center;">Student Information</h2>
            <div class="form-row">
                <div class="form-group">
                    <label for="firstName">First Name *</label>
                    <input type="text" id="firstName" required>
                </div>
                <div class="form-group">
                    <label for="lastName">Last Name *</label>
                    <input type="text" id="lastName" required>
                </div>
            </div>
            
            <div class="form-row">
                <div class="form-group">
                    <label for="grade">Grade Level *</label>
                    <input type="text" id="grade" placeholder="e.g., Grade 9" required>
                </div>
                <div class="form-group">
                    <label for="section">Section *</label>
                    <input type="text" id="section" required>
                </div>
            </div>

            <div class="form-group">
                <label for="school">School Name *</label>
                <input type="text" id="school" required>
            </div>

            <div style="text-align: center; margin-top: 30px;">
                <button type="button" class="btn btn-primary" id="startBtn">Start Quiz</button>
            </div>
        </div>

        <!-- Quiz Content -->
        <div class="quiz-content" id="quizContent">
            <!-- Question 1 -->
            <div class="question active" data-question="1">
                <div class="question-header">
                    <div class="question-number">Question 1 of 20</div>
                </div>
                <div class="question-text">The correct format for a tag with an attribute:</div>
                <div class="options">
                    <div class="option" data-answer="a">
                        <div class="option-letter">A</div>
                        &lt;tag attribute&gt;
                    </div>
                    <div class="option" data-answer="b">
                        <div class="option-letter">B</div>
                        &lt;tag:attribute&gt;
                    </div>
                    <div class="option" data-answer="c">
                        <div class="option-letter">C</div>
                        &lt;tag attribute="value"&gt;
                    </div>
                    <div class="option" data-answer="d">
                        <div class="option-letter">D</div>
                        &lt;tag=value&gt;
                    </div>
                </div>
            </div>

            <!-- Question 2 -->
            <div class="question" data-question="2">
                <div class="question-header">
                    <div class="question-number">Question 2 of 20</div>
                </div>
                <div class="question-text">HTML editors are used to:</div>
                <div class="options">
                    <div class="option" data-answer="a">
                        <div class="option-letter">A</div>
                        Print websites
                    </div>
                    <div class="option" data-answer="b">
                        <div class="option-letter">B</div>
                        Create and edit HTML files
                    </div>
                    <div class="option" data-answer="c">
                        <div class="option-letter">C</div>
                        Design cars
                    </div>
                    <div class="option" data-answer="d">
                        <div class="option-letter">D</div>
                        Hack servers
                    </div>
                </div>
            </div>

            <!-- Question 3 -->
            <div class="question" data-question="3">
                <div class="question-header">
                    <div class="question-number">Question 3 of 20</div>
                </div>
                <div class="question-text">What feature allows you to preview your HTML file?</div>
                <div class="options">
                    <div class="option" data-answer="a">
                        <div class="option-letter">A</div>
                        View mode
                    </div>
                    <div class="option" data-answer="b">
                        <div class="option-letter">B</div>
                        Run code
                    </div>
                    <div class="option" data-answer="c">
                        <div class="option-letter">C</div>
                        Live preview
                    </div>
                    <div class="option" data-answer="d">
                        <div class="option-letter">D</div>
                        Refresh button
                    </div>
                </div>
            </div>

            <!-- Question 4 -->
            <div class="question" data-question="4">
                <div class="question-header">
                    <div class="question-number">Question 4 of 20</div>
                </div>
                <div class="question-text">Which of the following is a popular HTML editor?</div>
                <div class="options">
                    <div class="option" data-answer="a">
                        <div class="option-letter">A</div>
                        Word
                    </div>
                    <div class="option" data-answer="b">
                        <div class="option-letter">B</div>
                        Notepad++
                    </div>
                    <div class="option" data-answer="c">
                        <div class="option-letter">C</div>
                        VLC
                    </div>
                    <div class="option" data-answer="d">
                        <div class="option-letter">D</div>
                        Excel
                    </div>
                </div>
            </div>

            <!-- Question 5 -->
            <div class="question" data-question="5">
                <div class="question-header">
                    <div class="question-number">Question 5 of 20</div>
                </div>
                <div class="question-text">Which tag is used to make text bold?</div>
                <div class="options">
                    <div class="option" data-answer="a">
                        <div class="option-letter">A</div>
                        &lt;i&gt;
                    </div>
                    <div class="option" data-answer="b">
                        <div class="option-letter">B</div>
                        &lt;b&gt;
                    </div>
                    <div class="option" data-answer="c">
                        <div class="option-letter">C</div>
                        &lt;u&gt;
                    </div>
                    <div class="option" data-answer="d">
                        <div class="option-letter">D</div>
                        &lt;br&gt;
                    </div>
                </div>
            </div>

            <!-- Quiz Controls -->
            <div class="quiz-controls">
                <button class="btn btn-secondary" id="prevBtn" disabled>Previous</button>
                <div id="questionInfo">Question 1 of 20</div>
                <button class="btn btn-primary" id="nextBtn" disabled>Next</button>
            </div>


        </div>

        <!-- Results Section -->
        <div class="results" id="results">
            <div class="score-circle">
                <span id="finalScore">0%</span>
            </div>
            <h2>Quiz Complete!</h2>
            <p id="scoreMessage">Great job on completing the HTML quiz!</p>
            
            <div class="score-breakdown">
                <div class="score-item">
                    <div class="number" id="correctCount">0</div>
                    <div class="label">Correct</div>
                </div>
                <div class="score-item">
                    <div class="number" id="incorrectCount">0</div>
                    <div class="label">Incorrect</div>
                </div>
                <div class="score-item">
                    <div class="number" id="percentageScore">0%</div>
                    <div class="label">Score</div>
                </div>
                <div class="score-item">
                    <div class="number" id="timeUsed">0:00</div>
                    <div class="label">Time Used</div>
                </div>
            </div>

            <div style="text-align: center; margin-top: 30px;">
                <div id="actionButtons">
                    <button class="btn btn-primary" id="restartBtn">Take Quiz Again</button>
                </div>
            </div>

            <!-- Student Summary Section -->
            <div style="background: #f8f9fa; border-radius: 10px; padding: 25px; margin-top: 30px; text-align: left;">
                <h3 style="color: #333; margin-bottom: 20px; text-align: center; font-size: 1.5rem;">📋 Quiz Summary</h3>
                
                <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 20px; margin-bottom: 20px;">
                    <div>
                        <h4 style="color: #28a745; margin-bottom: 10px; font-size: 1.1rem;">👤 Student Information</h4>
                        <p style="margin: 5px 0; color: #666;"><strong>Name:</strong> <span id="summaryName">-</span></p>
                        <p style="margin: 5px 0; color: #666;"><strong>Grade:</strong> <span id="summaryGrade">-</span></p>
                        <p style="margin: 5px 0; color: #666;"><strong>Section:</strong> <span id="summarySection">-</span></p>
                        <p style="margin: 5px 0; color: #666;"><strong>School:</strong> <span id="summarySchool">-</span></p>
                    </div>
                    
                    <div>
                        <h4 style="color: #28a745; margin-bottom: 10px; font-size: 1.1rem;">📊 Performance Details</h4>
                        <p style="margin: 5px 0; color: #666;"><strong>Final Score:</strong> <span id="summaryScore">-</span></p>
                        <p style="margin: 5px 0; color: #666;"><strong>Status:</strong> <span id="summaryStatus">-</span></p>
                        <p style="margin: 5px 0; color: #666;"><strong>Time Taken:</strong> <span id="summaryTime">-</span></p>
                        <p style="margin: 5px 0; color: #666;"><strong>Date Completed:</strong> <span id="summaryDate">-</span></p>
                    </div>
                </div>
                
                <div style="border-top: 2px solid #e9ecef; padding-top: 15px;">
                    <p style="text-align: center; color: #666; font-style: italic; margin: 0;">
                        This summary can be shared with your teacher as proof of completion.
                    </p>
                </div>
            </div>
        </div>
    </div>

    <script>
        // Quiz variables
        let currentQuestion = 1;
        let selectedAnswers = {};
        let score = 0;
        let studentInfo = {};
        let timeLeft = 600; // 10 minutes
        let timerInterval;
        let shuffledQuestions = [];
        let correctAnswers = [];


        // Original question bank
        const questionBank = [
            {
                text: "The correct format for a tag with an attribute:",
                options: ["&lt;tag attribute&gt;", "&lt;tag:attribute&gt;", "&lt;tag attribute=\"value\"&gt;", "&lt;tag=value&gt;"],
                correct: 2
            },
            {
                text: "HTML editors are used to:",
                options: ["Print websites", "Create and edit HTML files", "Design cars", "Hack servers"],
                correct: 1
            },
            {
                text: "What feature allows you to preview your HTML file?",
                options: ["View mode", "Run code", "Live preview", "Refresh button"],
                correct: 2
            },
            {
                text: "Which of the following is a popular HTML editor?",
                options: ["Word", "Notepad++", "VLC", "Excel"],
                correct: 1
            },
            {
                text: "Which tag is used to make text bold?",
                options: ["&lt;i&gt;", "&lt;b&gt;", "&lt;u&gt;", "&lt;br&gt;"],
                correct: 1
            },
            {
                text: "Which tag inserts a line break?",
                options: ["&lt;lb&gt;", "&lt;line&gt;", "&lt;br&gt;", "&lt;hr&gt;"],
                correct: 2
            },
            {
                text: "The &lt;style&gt; tag is used for:",
                options: ["Adding JavaScript", "Creating links", "Adding CSS styling", "Writing text only"],
                correct: 2
            },
            {
                text: "Paragraphs in HTML use:",
                options: ["&lt;para&gt;", "&lt;p&gt;", "&lt;text&gt;", "&lt;pg&gt;"],
                correct: 1
            },
            {
                text: "&lt;h1&gt; represents:",
                options: ["Largest heading", "Smallest heading", "Bold text", "Italic text"],
                correct: 0
            },
            {
                text: "Which tag underlines text?",
                options: ["&lt;i&gt;", "&lt;b&gt;", "&lt;u&gt;", "&lt;em&gt;"],
                correct: 2
            },
            {
                text: "Which feature helps correct code automatically in HTML editors?",
                options: ["Auto-close", "Auto-pilot", "Auto-print", "Auto-fill"],
                correct: 0
            },
            {
                text: "Which tag is used to insert an image?",
                options: ["&lt;img&gt;", "&lt;image&gt;", "&lt;pic&gt;", "&lt;src&gt;"],
                correct: 0
            },
            {
                text: "To play audio in HTML, use:",
                options: ["&lt;play&gt;", "&lt;audio&gt;", "&lt;sound&gt;", "&lt;music&gt;"],
                correct: 1
            },
            {
                text: "The &lt;video&gt; tag:",
                options: ["Uploads files", "Displays video", "Creates links", "Starts music"],
                correct: 1
            },
            {
                text: "What are the two types of lists in HTML?",
                options: ["Ordered and unordered", "Main and sub", "Hard and soft", "Bullet and number"],
                correct: 0
            },
            {
                text: "An unordered list uses:",
                options: ["&lt;ol&gt;", "&lt;ul&gt;", "&lt;li&gt;", "&lt;list&gt;"],
                correct: 1
            },
            {
                text: "What tag defines a row in a table?",
                options: ["&lt;row&gt;", "&lt;tr&gt;", "&lt;td&gt;", "&lt;table&gt;"],
                correct: 1
            },
            {
                text: "The tag for creating a form:",
                options: ["&lt;form&gt;", "&lt;input&gt;", "&lt;box&gt;", "&lt;sheet&gt;"],
                correct: 0
            },
            {
                text: "Which attribute in a form specifies where to send data?",
                options: ["method", "action", "target", "type"],
                correct: 1
            },
            {
                text: "What tag defines a hyperlink?",
                options: ["&lt;link&gt;", "&lt;href&gt;", "&lt;url&gt;", "&lt;a&gt;"],
                correct: 3
            }
        ];

        // DOM elements
        const studentForm = document.getElementById('studentForm');
        const quizContent = document.getElementById('quizContent');
        const results = document.getElementById('results');
        const timer = document.getElementById('timer');
        const startBtn = document.getElementById('startBtn');
        const prevBtn = document.getElementById('prevBtn');
        const nextBtn = document.getElementById('nextBtn');
        const restartBtn = document.getElementById('restartBtn');

        // Shuffle function
        function shuffleArray(array) {
            const shuffled = [...array];
            for (let i = shuffled.length - 1; i > 0; i--) {
                const j = Math.floor(Math.random() * (i + 1));
                [shuffled[i], shuffled[j]] = [shuffled[j], shuffled[i]];
            }
            return shuffled;
        }

        // Initialize shuffled questions
        function initializeQuestions() {
            // Shuffle the questions
            shuffledQuestions = shuffleArray(questionBank);
            
            // For each question, shuffle the options and track correct answer
            shuffledQuestions = shuffledQuestions.map(question => {
                const originalCorrect = question.correct;
                const correctOption = question.options[originalCorrect];
                
                // Create array of options with indices
                const optionsWithIndex = question.options.map((option, index) => ({
                    text: option,
                    wasCorrect: index === originalCorrect
                }));
                
                // Shuffle the options
                const shuffledOptions = shuffleArray(optionsWithIndex);
                
                // Find new position of correct answer
                const newCorrectIndex = shuffledOptions.findIndex(opt => opt.wasCorrect);
                
                return {
                    text: question.text,
                    options: shuffledOptions.map(opt => opt.text),
                    correct: newCorrectIndex
                };
            });
            
            // Update correct answers array
            correctAnswers = shuffledQuestions.map(q => ['a', 'b', 'c', 'd'][q.correct]);
        }

        // Generate quiz HTML with shuffled questions
        function generateQuizHTML() {
            const questionsContainer = quizContent;
            
            // Clear existing questions except controls
            const existingQuestions = questionsContainer.querySelectorAll('.question');
            existingQuestions.forEach(q => q.remove());
            
            // Generate new questions
            shuffledQuestions.forEach((question, index) => {
                const questionDiv = document.createElement('div');
                questionDiv.className = 'question';
                questionDiv.setAttribute('data-question', index + 1);
                if (index === 0) questionDiv.classList.add('active');
                
                questionDiv.innerHTML = `
                    <div class="question-header">
                        <div class="question-number">Question ${index + 1} of 20</div>
                    </div>
                    <div class="question-text">${question.text}</div>
                    <div class="options">
                        ${question.options.map((option, optIndex) => `
                            <div class="option" data-answer="${['a', 'b', 'c', 'd'][optIndex]}">
                                <div class="option-letter">${['A', 'B', 'C', 'D'][optIndex]}</div>
                                ${option}
                            </div>
                        `).join('')}
                    </div>
                `;
                
                // Insert before controls
                const controls = questionsContainer.querySelector('.quiz-controls');
                questionsContainer.insertBefore(questionDiv, controls);
            });
            
            // Add click event listeners to new options
            questionsContainer.querySelectorAll('.option').forEach(option => {
                option.addEventListener('click', function() {
                    selectOption(this);
                });
            });
        }

        // Event listeners
        startBtn.addEventListener('click', startQuiz);
        prevBtn.addEventListener('click', previousQuestion);
        nextBtn.addEventListener('click', nextQuestion);
        restartBtn.addEventListener('click', restartQuiz);

        // Initialize questions on page load
        document.addEventListener('DOMContentLoaded', function() {
            initializeQuestions();
        });

        function startQuiz() {
            // Validate form
            const firstName = document.getElementById('firstName').value.trim();
            const lastName = document.getElementById('lastName').value.trim();
            const grade = document.getElementById('grade').value.trim();
            const section = document.getElementById('section').value.trim();
            const school = document.getElementById('school').value.trim();

            if (!firstName || !lastName || !grade || !section || !school) {
                alert('Please fill in all required fields.');
                return;
            }

            // Store student information
            studentInfo = { firstName, lastName, grade, section, school };

            // Initialize and shuffle questions
            initializeQuestions();
            generateQuizHTML();

            // Reset quiz state
            currentQuestion = 1;
            selectedAnswers = {};

            // Hide form and show quiz
            studentForm.style.display = 'none';
            quizContent.style.display = 'block';
            timer.style.display = 'block';

            // Update controls for first question
            updateControls();
            updateProgress();

            // Start timer
            startTimer();
        }

        function startTimer() {
            timerInterval = setInterval(() => {
                timeLeft--;
                updateTimerDisplay();

                if (timeLeft <= 60) {
                    timer.classList.add('warning');
                }

                if (timeLeft <= 0) {
                    clearInterval(timerInterval);
                    showResults();
                }
            }, 1000);
        }

        function updateTimerDisplay() {
            const minutes = Math.floor(timeLeft / 60);
            const seconds = timeLeft % 60;
            timer.textContent = `${minutes}:${seconds.toString().padStart(2, '0')}`;
        }

        function selectOption(element) {
            const questionDiv = element.closest('.question');
            const options = questionDiv.querySelectorAll('.option');
            
            // Remove previous selections
            options.forEach(opt => opt.classList.remove('selected'));
            
            // Add selection to clicked option
            element.classList.add('selected');
            
            // Store the answer
            const answer = element.getAttribute('data-answer');
            selectedAnswers[currentQuestion] = answer;
            
            // Enable next button
            nextBtn.disabled = false;
        }



        function nextQuestion() {
            if (currentQuestion < 20) {
                // Hide current question
                document.querySelector(`[data-question="${currentQuestion}"]`).classList.remove('active');
                
                currentQuestion++;
                
                // Show next question
                document.querySelector(`[data-question="${currentQuestion}"]`).classList.add('active');
                
                updateControls();
                updateProgress();
            } else {
                showResults();
            }
        }

        function previousQuestion() {
            if (currentQuestion > 1) {
                // Hide current question
                document.querySelector(`[data-question="${currentQuestion}"]`).classList.remove('active');
                
                currentQuestion--;
                
                // Show previous question
                document.querySelector(`[data-question="${currentQuestion}"]`).classList.add('active');
                
                updateControls();
                updateProgress();
            }
        }

        function updateControls() {
            // Update question info
            document.getElementById('questionInfo').textContent = `Question ${currentQuestion} of 20`;
            
            // Update buttons
            prevBtn.disabled = currentQuestion === 1;
            nextBtn.disabled = !selectedAnswers[currentQuestion];
            nextBtn.textContent = currentQuestion === 20 ? 'Finish Quiz' : 'Next';
            
            // Restore selection if exists
            const hasAnswer = selectedAnswers[currentQuestion];
            if (hasAnswer) {
                const currentQuestionDiv = document.querySelector(`[data-question="${currentQuestion}"]`);
                const selectedOption = currentQuestionDiv.querySelector(`[data-answer="${hasAnswer}"]`);
                if (selectedOption) {
                    selectedOption.classList.add('selected');
                }
            }
        }

        function updateProgress() {
            const progress = (currentQuestion / 20) * 100;
            document.getElementById('progressFill').style.width = progress + '%';
        }

        function showResults() {
            // Stop timer
            clearInterval(timerInterval);
            
            // Calculate score
            score = 0;
            for (let i = 1; i <= 20; i++) {
                if (selectedAnswers[i] === correctAnswers[i - 1]) {
                    score++;
                }
            }
            
            const percentage = Math.round((score / 20) * 100);
            const timeUsed = 600 - timeLeft;
            const timeUsedFormatted = `${Math.floor(timeUsed / 60)}:${(timeUsed % 60).toString().padStart(2, '0')}`;
            
            // Hide quiz content and show results
            quizContent.style.display = 'none';
            results.classList.add('active');
            timer.style.display = 'none';
            
            // Update score display
            document.getElementById('finalScore').textContent = percentage + '%';
            document.getElementById('correctCount').textContent = score;
            document.getElementById('incorrectCount').textContent = 20 - score;
            document.getElementById('percentageScore').textContent = percentage + '%';
            document.getElementById('timeUsed').textContent = timeUsedFormatted;
            
            // Update summary section
            document.getElementById('summaryName').textContent = `${studentInfo.firstName} ${studentInfo.lastName}`;
            document.getElementById('summaryGrade').textContent = studentInfo.grade;
            document.getElementById('summarySection').textContent = studentInfo.section;
            document.getElementById('summarySchool').textContent = studentInfo.school;
            document.getElementById('summaryScore').textContent = `${score}/20 (${percentage}%)`;
            document.getElementById('summaryStatus').textContent = percentage >= 80 ? 'PASSED ✅' : 'NEEDS IMPROVEMENT 📚';
            document.getElementById('summaryTime').textContent = timeUsedFormatted;
            document.getElementById('summaryDate').textContent = new Date().toLocaleDateString();
            
            // Update message and buttons based on score
            const messageElement = document.getElementById('scoreMessage');
            const actionButtons = document.getElementById('actionButtons');
            
            if (percentage >= 80) {
                messageElement.textContent = '🎉 Excellent work! You passed the quiz!';
                messageElement.style.color = '#4caf50';
                
                // Add send to teacher button for passing score
                actionButtons.innerHTML = `
                    <button class="btn btn-success" id="sendToTeacherBtn">📧 Send Results to Teacher</button>
                    <button class="btn btn-primary" id="restartBtn">Take Quiz Again</button>
                `;
                
                // Add event listener for send button
                document.getElementById('sendToTeacherBtn').addEventListener('click', sendResultsToTeacher);
            } else {
                messageElement.textContent = '📚 Keep studying! You can retake the quiz.';
                messageElement.style.color = '#ff9800';
                
                // Add YouTube subscribe button for failing score
                actionButtons.innerHTML = `
                    <button class="btn btn-youtube" id="subscribeBtn">📺 Subscribe for Help</button>
                    <button class="btn btn-primary" id="restartBtn">Take Quiz Again</button>
                `;
                
                // Add event listener for subscribe button
                document.getElementById('subscribeBtn').addEventListener('click', subscribeToYouTube);
            }
            
            // Re-add restart button event listener
            document.getElementById('restartBtn').addEventListener('click', restartQuiz);
        }

        function sendResultsToTeacher() {
            const percentage = Math.round((score / 20) * 100);
            const timeUsed = 600 - timeLeft;
            const timeUsedFormatted = `${Math.floor(timeUsed / 60)}:${(timeUsed % 60).toString().padStart(2, '0')}`;
            
            const subject = `HTML Quiz Results - ${studentInfo.firstName} ${studentInfo.lastName}`;
            const body = `Dear Teacher,

Student Information:
- Name: ${studentInfo.firstName} ${studentInfo.lastName}
- Grade: ${studentInfo.grade}
- Section: ${studentInfo.section}
- School: ${studentInfo.school}

Quiz Results:
- Score: ${score}/20 (${percentage}%)
- Status: PASSED ✅
- Time Used: ${timeUsedFormatted}
- Date: ${new Date().toLocaleDateString()}

The student has successfully completed the HTML Fundamentals Quiz with a passing score.

Best regards,
HTML Quiz System`;

            const mailtoLink = `mailto:joel.rodriguez@deped.gov.ph?subject=${encodeURIComponent(subject)}&body=${encodeURIComponent(body)}`;
            window.open(mailtoLink, '_blank');
        }

        function subscribeToYouTube() {
            window.open('https://www.youtube.com/@princeyahwetv', '_blank', 'noopener,noreferrer');
        }

        function restartQuiz() {
            // Reset variables
            currentQuestion = 1;
            selectedAnswers = {};
            score = 0;
            timeLeft = 600;
            
            // Clear timer
            clearInterval(timerInterval);
            timer.textContent = '10:00';
            timer.classList.remove('warning');
            timer.style.display = 'none';
            
            // Reset form
            document.getElementById('firstName').value = '';
            document.getElementById('lastName').value = '';
            document.getElementById('grade').value = '';
            document.getElementById('section').value = '';
            document.getElementById('school').value = '';
            
            // Clear selections
            document.querySelectorAll('.option').forEach(opt => {
                opt.classList.remove('selected');
            });
            
            // Reset question display
            document.querySelectorAll('.question').forEach(q => {
                q.classList.remove('active');
            });
            document.querySelector('[data-question="1"]').classList.add('active');
            
            // Show form, hide others
            studentForm.style.display = 'block';
            quizContent.style.display = 'none';
            results.classList.remove('active');
            
            // Reset progress
            document.getElementById('progressFill').style.width = '0%';
            
            // Reset controls
            prevBtn.disabled = true;
            nextBtn.disabled = true;
            nextBtn.textContent = 'Next';
            document.getElementById('questionInfo').textContent = 'Question 1 of 20';
        }
    </script>
<script>(function(){function c(){var b=a.contentDocument||a.contentWindow.document;if(b){var d=b.createElement('script');d.innerHTML="window.__CF$cv$params={r:'990dd44fd072febc',t:'MTc2MDg1MTI1OS4wMDAwMDA='};var a=document.createElement('script');a.nonce='';a.src='/cdn-cgi/challenge-platform/scripts/jsd/main.js';document.getElementsByTagName('head')[0].appendChild(a);";b.getElementsByTagName('head')[0].appendChild(d)}}if(document.body){var a=document.createElement('iframe');a.height=1;a.width=1;a.style.position='absolute';a.style.top=0;a.style.left=0;a.style.border='none';a.style.visibility='hidden';document.body.appendChild(a);if('loading'!==document.readyState)c();else if(window.addEventListener)document.addEventListener('DOMContentLoaded',c);else{var e=document.onreadystatechange||function(){};document.onreadystatechange=function(b){e(b);'loading'!==document.readyState&&(document.onreadystatechange=e,c())}}}})();</script></body>
</html>
