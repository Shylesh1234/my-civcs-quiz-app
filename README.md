<!DOCTYPE html>
<html>
<head>
  <link rel="stylesheet" type="text/css" href="styles.css">
</head>
<body>
  <div id="quiz-container">
    <h1>Multiple Choice Quiz</h1>
    <div id="question"></div>
    <div id="options"></div>
    <button id="next-btn">Next</button>
    <div id="score">Score: 0</div>
  </div>
  <script src="script.js"></script>
</body>
</html>
body {
  font-family: Arial, sans-serif;
}

#quiz-container {
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
  text-align: center;
}

button {
  padding: 10px 20px;
  background-color: #007bff;
  color: white;
  border: none;
  cursor: pointer;
}

button:hover {
  background-color: #0056b3;
}
const questionElement = document.getElementById("question");
const optionsElement = document.getElementById("options");
const nextButton = document.getElementById("next-btn");
const scoreElement = document.getElementById("score");

const questions = [
  {
    question: "What is the capital of France?",
    options: ["Berlin", "Paris", "Rome", "Madrid"],
    answer: 1
  },
  {
    question: "Which amendment grants freedom of speech?",
    options: ["First Amendment", "Second Amendment", "Fourth Amendment", "Tenth Amendment"],
    answer: 0
  }
];

let currentQuestionIndex = 0;
let score = 0;

function showQuestion(question) {
  questionElement.innerText = question.question;
  optionsElement.innerHTML = "";

  question.options.forEach((option, index) => {
    const button = document.createElement("button");
    button.innerText = option;
    button.addEventListener("click", () => selectOption(index));
    optionsElement.appendChild(button);
  });
}

function selectOption(selectedIndex) {
  if (selectedIndex === questions[currentQuestionIndex].answer) {
    score++;
  }

  currentQuestionIndex++;

  if (currentQuestionIndex < questions.length) {
    showQuestion(questions[currentQuestionIndex]);
  } else {
    showScore();
  }
}

function showScore() {
  questionElement.innerText = "Quiz completed!";
  optionsElement.innerHTML = "";
  scoreElement.innerText = `Score: ${score} / ${questions.length}`;
  nextButton.style.display = "none";
}

nextButton.addEventListener("click", () => selectOption(-1));

showQuestion(questions[currentQuestionIndex]);
