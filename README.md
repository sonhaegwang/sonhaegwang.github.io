<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>숫자 맞히기 게임</title>
    <style>
        body {
            font-family: Arial, sans-serif;
        }
        #guessInput {
            width: 50px;
        }
        #guessSubmit {
            margin-top: 10px;
        }
        #message {
            margin-top: 10px;
        }
    </style>
</head>
<body>

<h1>숫자 맞히기 게임</h1>
<p>1에서 100 사이의 숫자를 추측하세요:</p>

<label for="guessInput">입력: </label>
<input type="text" id="guessInput" class="guessField">
<input type="submit" value="확인" class="guessSubmit" id="guessSubmit">

<div id="message"></div>

<script>
    // 컴퓨터가 선택한 숫자 생성
    const randomNumber = Math.floor(Math.random() * 100) + 1;

    // 게임 상태를 추적하기 위한 변수
    let guesses = [];
    let attempts = 0;
    let isGameOver = false;

    const guessSubmit = document.getElementById('guessSubmit');
    const message = document.getElementById('message');

    function checkGuess() {
        const guess = parseInt(document.getElementById('guessInput').value);

        if (isNaN(guess) || guess < 1 || guess > 100) {
            alert('1에서 100 사이의 숫자를 입력하세요!');
            return;
        }

        // 이전 추측 기록에 추가
        guesses.push(guess);
        attempts++;

        // 추측한 숫자 확인
        if (guess === randomNumber) {
            gameOver(true);
        } else {
            if (attempts === 10) {
                gameOver(false);
            } else {
                displayMessage(`틀렸습니다! 남은 시도 횟수: ${10 - attempts}`);
            }
        }

        document.getElementById('guessInput').value = ''; // 입력 필드 초기화
        document.getElementById('guessInput').focus(); // 입력 필드로 포커스 이동
    }

    function displayMessage(msg) {
        message.textContent = msg;
    }

    function gameOver(win) {
        if (win) {
            displayMessage(`축하합니다! ${randomNumber}을(를) 맞추셨습니다! 시도 횟수: ${attempts}`);
        } else {
            displayMessage(`게임 종료! 정답은 ${randomNumber}입니다.`);
        }

        isGameOver = true;
        guessSubmit.disabled = true;
    }

    guessSubmit.addEventListener('click', function() {
        if (!isGameOver) {
            checkGuess();
        }
    });
</script>

</body>
</html>
