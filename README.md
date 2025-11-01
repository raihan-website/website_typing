<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Typing Test Sederhana</title>
  <style>
    body {
      background-color: #f8f9fa;
      font-family: "Poppins", sans-serif;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      margin: 0;
    }
    .container {
      background: #fff;
      padding: 2rem 3rem;
      border-radius: 10px;
      box-shadow: 0 4px 15px rgba(0,0,0,0.1);
      max-width: 600px;
      text-align: center;
    }
    h1 {
      margin-bottom: 10px;
    }
    #quote {
      font-size: 1.2rem;
      margin-bottom: 20px;
      color: #333;
    }
    #input {
      width: 100%;
      height: 100px;
      padding: 10px;
      font-size: 1rem;
      border: 2px solid #ccc;
      border-radius: 5px;
      resize: none;
      transition: border-color 0.2s;
    }
    #input:focus {
      border-color: #007bff;
      outline: none;
    }
    .stats {
      display: flex;
      justify-content: space-around;
      margin-top: 20px;
    }
    .stat-box {
      background: #f1f3f5;
      padding: 10px;
      border-radius: 8px;
      min-width: 80px;
    }
    button {
      margin-top: 20px;
      padding: 10px 20px;
      background: #007bff;
      color: white;
      border: none;
      border-radius: 5px;
      cursor: pointer;
      font-size: 1rem;
      transition: background 0.2s;
    }
    button:hover {
      background: #0056b3;
    }
    footer {
      margin-top: 20px;
      font-size: 0.9rem;
      color: #666;
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>Typing Speed Test</h1>
    <p id="quote">Klik tombol "Mulai Tes" untuk memulai.</p>
    <textarea id="input" placeholder="Mulai mengetik di sini..." disabled></textarea>

    <div class="stats">
      <div class="stat-box">
        <p>Waktu</p>
        <h3><span id="time">60</span>s</h3>
      </div>
      <div class="stat-box">
        <p>WPM</p>
        <h3><span id="wpm">0</span></h3>
      </div>
      <div class="stat-box">
        <p>Akurasi</p>
        <h3><span id="accuracy">0</span>%</h3>
      </div>
    </div>

    <button id="start-btn">Mulai Tes</button>
    <footer>Made by Raihan, Aqil</footer>
  </div>

  <script>
    const quotes = [
      "Cepat dan tepat adalah kunci sukses mengetik.",
      "Latihan membuat kemampuan mengetik semakin sempurna.",
      "Mengetik dengan sepuluh jari adalah keahlian yang berguna.",
      "Konsistensi adalah rahasia peningkatan kecepatan mengetik.",
      "Jangan takut salah, yang penting terus berlatih."
    ];

    const quoteDisplay = document.getElementById("quote");
    const inputField = document.getElementById("input");
    const startBtn = document.getElementById("start-btn");
    const timeDisplay = document.getElementById("time");
    const wpmDisplay = document.getElementById("wpm");
    const accuracyDisplay = document.getElementById("accuracy");

    let time = 60;
    let timer = null;
    let totalTyped = 0;
    let errors = 0;
    let quote = "";

    function newQuote() {
      quote = quotes[Math.floor(Math.random() * quotes.length)];
      quoteDisplay.textContent = quote;
    }

    function startTest() {
      newQuote();
      inputField.value = "";
      inputField.disabled = false;
      inputField.focus();
      startBtn.disabled = true;
      time = 60;
      totalTyped = 0;
      errors = 0;
      timeDisplay.textContent = time;
      wpmDisplay.textContent = 0;
      accuracyDisplay.textContent = 0;

      clearInterval(timer);

      timer = setInterval(() => {
        time--;
        timeDisplay.textContent = time;
        if (time === 0) finishTest();
      }, 1000);
    }

    function finishTest() {
      clearInterval(timer);
      inputField.disabled = true;
      startBtn.disabled = false;

      const elapsedTime = (60 - time) / 60; // menit
      const wpm = Math.round((totalTyped / 5) / elapsedTime);
      const accuracy = Math.max(0, Math.round(((totalTyped - errors) / totalTyped) * 100));

      wpmDisplay.textContent = isNaN(wpm) ? 0 : wpm;
      accuracyDisplay.textContent = isNaN(accuracy) ? 0 : accuracy;
    }

    inputField.addEventListener("input", () => {
      const typedText = inputField.value;
      totalTyped++;

      if (quote.startsWith(typedText)) {
        inputField.style.borderColor = "#28a745";
      } else {
        inputField.style.borderColor = "#dc3545";
        errors++;
      }

      if (typedText === quote) {
        newQuote();
        inputField.value = "";
      }
    });

    startBtn.addEventListener("click", startTest);
  </script>
</body>
</html>
