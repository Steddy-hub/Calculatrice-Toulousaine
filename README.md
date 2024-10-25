<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Quiz Vidéo</title>
    <style>
        body { font-family: Arial, sans-serif; margin: 20px; }
        .question { margin-bottom: 15px; }
        .result { margin-top: 10px; font-weight: bold; }
        input[type="radio"] { margin-right: 10px; }
    </style>
</head>
<body>
    <h1>Quizz Projet1.2</h1>
    <div id="quiz"></div>
    <button id="next">Suivant</button>
    <p id="result" class="result"></p>

    <script>
        const questions = [
            {
                question: "Quel est le jeu vidéo où l'on construit des structures et survit dans un monde en blocs ?",
                answers: ["Minecraft", "Fortnite", "Roblox"],
                correctAnswer: ["Minecraft"]
            },
            {
                question: "Quel est le nom du Youtubeur qui a détrôné Squeezie et devient numéro 1 en France ?",
                answers: ["Tibo inshape", "Cyprien", "Squeezie"],
                correctAnswer: ["Tibo inshape"]
            },
            {
                question: "Dans quel jeu vidéo les joueurs s'affrontent en construisant des ponts et nous force à ragquit ?",
                answers: ["League of Legends", "Fortnite", "Call of Duty"],
                correctAnswer: ["Fortnite"]
            },
            {
                question: "Quel est le personnage ressemblant à un plombier avec une moustache et qui doit sauver la princesse P. du méchant B. ?",
                answers: ["Super Mario", "Luigi", "Donkey Kong"],
                correctAnswer: ["Super Mario", "Mario"]
            },
            {
                question: "Je suis une héroïne de jeux vidéos, je suis forte et intelligente, mais je suis redoutable quand il s’agit de sauter et faire des cascades de malade. Qui suis-je ?",
                answers: ["Lara Croft", "Zelda", "Samus Aran"],
                correctAnswer: ["Tomb Raider", "Lara Croft"]
            },
            {
                question: "Dans quel jeu les joueurs peuvent-ils s’affronter en utilisant des personnages emblématiques d’autres jeux vidéo, comme Mario et Pikachu ?",
                answers: ["Mortal Kombat", "Super Smash Bros", "Street Fighter"],
                correctAnswer: ["Super Smash Bros"]
            },
            {
                question: "Quel est le nom du célèbre jeu de tir en équipe où les joueurs s'affrontent pour capturer des points et éliminer l'équipe adverse ?",
                answers: ["Valorant", "Overwatch", "Battlefield"],
                correctAnswer: ["Overwatch"]
            },
            {
                question: "Quel est le nom du formidable homme qui a créé plein de personnages Marvel mais qui n’est plus malheureusement ?",
                answers: ["Jack Kirby", "Stan Lee", "Joe Simon"],
                correctAnswer: ["Stan Lee"]
            }
        ];

        let currentQuestionIndex = 0;

        function displayQuestion() {
            const quizContainer = document.getElementById("quiz");
            quizContainer.innerHTML = ''; // Réinitialise le conteneur

            const currentQuestion = questions[currentQuestionIndex];
            const questionDiv = document.createElement("div");
            questionDiv.className = "question";
            questionDiv.innerHTML = `<p>${currentQuestion.question}</p>`;

            // Crée des boutons radio pour chaque réponse
            currentQuestion.answers.forEach(answer => {
                const label = document.createElement("label");
                const input = document.createElement("input");
                input.type = "radio";
                input.name = "answer";
                input.value = answer;

                label.appendChild(input);
                label.appendChild(document.createTextNode(answer));
                questionDiv.appendChild(label);
                questionDiv.appendChild(document.createElement("br")); // Ajoute un saut de ligne
            });

            quizContainer.appendChild(questionDiv);
            document.getElementById("result").innerText = ''; // Réinitialise le message de résultat

            document.getElementById("next").onclick = () => checkAnswer();
        }

        function checkAnswer() {
            const selectedAnswer = document.querySelector('input[name="answer"]:checked');
            const resultDisplay = document.getElementById("result");

            if (!selectedAnswer) {
                resultDisplay.innerText = "Veuillez sélectionner une réponse.";
                return;
            }

            const userAnswer = selectedAnswer.value;
            const currentQuestion = questions[currentQuestionIndex];
            const isCorrect = currentQuestion.correctAnswer.some(answer =>
                answer === userAnswer
            );

            if (isCorrect) {
                resultDisplay.innerText = "Correct !";
            } else {
                resultDisplay.innerText = `Incorrect. La réponse était : ${currentQuestion.correctAnswer.join(", ")}`;
            }

            currentQuestionIndex++;
            if (currentQuestionIndex < questions.length) {
                setTimeout(displayQuestion, 2000); // Attend 2 secondes avant de montrer la prochaine question
            } else {
                setTimeout(() => {
                    document.getElementById("quiz").innerHTML = '<p>Quiz terminé ! Merci d\'avoir joué.</p>';
                    document.getElementById("next").style.display = 'none';
                    resultDisplay.innerText = ''; // Réinitialise le message de résultat
                }, 2000);
            }
        }

        displayQuestion();
    </script>
</body>
</html>
