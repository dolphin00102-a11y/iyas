<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>I have a question for you...</title>
  <style>
    /* --- Base Styles --- */
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    body {
      font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
      background: #fff5f7;
      display: flex;
      justify-content: center;
      align-items: center;
      min-height: 100vh;
      overflow: hidden;
      text-align: center;
    }

    .container {
      background: #ffffff;
      padding: 40px 30px;
      border-radius: 16px;
      box-shadow: 0 10px 30px rgba(255, 182, 193, 0.3);
      max-width: 400px;
      width: 90%;
      position: relative;
      z-index: 10;
    }

    h1 {
      color: #ff4d6d;
      font-size: 2rem;
      margin-bottom: 30px;
      line-height: 1.3;
    }

    .btn-container {
      display: flex;
      justify-content: center;
      gap: 20px;
      height: 60px;
      align-items: center;
      position: relative;
    }

    button {
      padding: 14px 32px;
      font-size: 1.1rem;
      font-weight: bold;
      border: none;
      border-radius: 50px;
      cursor: pointer;
      transition: transform 0.1s ease, background-color 0.2s ease;
    }

    #yesBtn {
      background-color: #ff4d6d;
      color: #fff;
    }

    #yesBtn:hover {
      background-color: #c9184a;
      transform: scale(1.05);
    }

    #noBtn {
      background-color: #ffb703;
      color: #fff;
      position: relative;
    }

    /* --- Success Message Screen --- */
    .hidden {
      display: none;
    }

    .success-container {
      animation: fadeIn 1s ease forwards;
    }

    .success-container h1 {
      color: #ff2a5f;
      font-size: 2.2rem;
      margin-bottom: 15px;
    }

    .success-container p {
      color: #555;
      font-size: 1.1rem;
      line-height: 1.5;
    }

    .heart-icon {
      font-size: 3.5rem;
      color: #ff4d6d;
      margin-bottom: 10px;
      animation: pulse 1.5s infinite;
    }

    /* --- Floating Hearts Animation --- */
    .floating-heart {
      position: absolute;
      color: #ffb3c1;
      font-size: 1.5rem;
      animation: floatUp 4s linear infinite;
      opacity: 0;
      z-index: 1;
    }

    /* --- Keyframes --- */
    @keyframes fadeIn {
      from { opacity: 0; transform: scale(0.9); }
      to { opacity: 1; transform: scale(1); }
    }

    @keyframes pulse {
      0%, 100% { transform: scale(1); }
      50% { transform: scale(1.15); }
    }

    @keyframes floatUp {
      0% {
        transform: translateY(100vh) translateX(0);
        opacity: 0;
      }
      10% {
        opacity: 0.8;
      }
      100% {
        transform: translateY(-10vh) translateX(50px);
        opacity: 0;
      }
    }
  </style>
</head>
<body>

  <div id="background-hearts"></div>

  <div class="container" id="proposal-box">
    <h1>Will you be my girlfriend? 💖</h1>
    <div class="btn-container">
      <button id="yesBtn" onclick="acceptProposal()">Yes</button>
      <button id="noBtn" onmouseover="dodgeButton()" onclick="dodgeButton()">No</button>
    </div>
  </div>

  <div class="container hidden" id="success-box">
    <div class="success-container">
      <div class="heart-icon">💖</div>
      <h1>Yay! 🥰</h1>
      <p>Thanks for being my GF!</p>
    </div>
  </div>

  <script>
    // Dodging function for the "No" button
    function dodgeButton() {
      const noBtn = document.getElementById('noBtn');
      
      // Calculate random positions within the visible window
      const maxX = window.innerWidth - noBtn.offsetWidth - 40;
      const maxY = window.innerHeight - noBtn.offsetHeight - 40;

      const randomX = Math.max(20, Math.floor(Math.random() * maxX));
      const randomY = Math.max(20, Math.floor(Math.random() * maxY));

      // Make the button absolute so it can jump around the entire screen
      noBtn.style.position = 'fixed';
      noBtn.style.left = randomX + 'px';
      noBtn.style.top = randomY + 'px';
    }

    // Success function when clicking "Yes"
    function acceptProposal() {
      document.getElementById('proposal-box').classList.add('hidden');
      document.getElementById('success-box').classList.remove('hidden');
      
      // Keep creating floating background hearts
      for (let i = 0; i < 25; i++) {
        setTimeout(createHeart, i * 150);
      }
    }

    // Function to create falling/floating background hearts
    function createHeart() {
      const heart = document.createElement('div');
      heart.classList.add('floating-heart');
      heart.innerHTML = '❤️';
      heart.style.left = Math.random() * 100 + 'vw';
      heart.style.animationDuration = (Math.random() * 2 + 3) + 's'; // 3-5 seconds
      heart.style.fontSize = (Math.random() * 1 + 1) + 'rem';
      
      document.getElementById('background-hearts').appendChild(heart);

      // Clean up the element after it floats away
      setTimeout(() => {
        heart.remove();
      }, 5000);
    }
  </script>

</body>
</html>
