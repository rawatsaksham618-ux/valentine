<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Will You Be My Valentine?</title>

  <style>
    * {
      box-sizing: border-box;
    }

    body {
      margin: 0;
      height: 100vh;
      background: linear-gradient(135deg, #ff9a9e, #fad0c4);
      overflow: hidden;
      font-family: 'Comic Sans MS', cursive, sans-serif;
      display: flex;
      justify-content: center;
      align-items: center;
      text-align: center;
    }

    .container {
      width: 90%;
      max-width: 360px;
      background: white;
      padding: 30px 20px 40px;
      border-radius: 20px;
      box-shadow: 0 10px 25px rgba(0,0,0,0.2);
      z-index: 2;
    }

    h1 {
      color: #ff4d6d;
      font-size: 1.6rem;
      margin-bottom: 25px;
      line-height: 1.4;
    }

    .buttons {
      display: flex;
      justify-content: space-between;
      margin-top: 20px;
      position: relative;
      height: 70px;
    }

    button {
      width: 45%;
      font-size: 1.1rem;
      padding: 14px 0;
      border: none;
      border-radius: 30px;
      cursor: pointer;
      transition: transform 0.2s ease;
    }

    #yes {
      background-color: #ff4d6d;
      color: white;
    }

    #yes:active {
      transform: scale(1.1);
    }

    #no {
      background-color: #ccc;
      color: #333;
      position: absolute;
      right: 0;
    }

    /* Floating hearts */
    .heart {
      position: absolute;
      bottom: -20px;
      color: rgba(255, 77, 109, 0.6);
      animation: floatUp 5s linear forwards;
      pointer-events: none;
    }

    @keyframes floatUp {
      from {
        transform: translateY(0) scale(0.6);
        opacity: 1;
      }
      to {
        transform: translateY(-120vh) scale(1.4);
        opacity: 0;
      }
    }

    iframe {
      display: none;
    }
  </style>
</head>

<body onclick="playMusic()">

  <!-- Background Music -->
  <iframe
    id="music"
    src="https://www.youtube.com/embed/1JY8mFZ8uC8?enablejsapi=1&loop=1&playlist=1JY8mFZ8uC8"
    allow="autoplay">
  </iframe>

  <div class="container">
    <h1>Iti 💖<br>Will you be my Valentine?</h1>

    <div class="buttons">
      <button id="yes" onclick="yesClicked()">Yes 💘</button>
      <button id="no">No 💔</button>
    </div>
  </div>

  <script>
    const noButton = document.getElementById("no");

    // Move NO button on touch (mobile-friendly)
    function moveNoButton() {
      const container = document.querySelector(".container");
      const rect = container.getBoundingClientRect();

      const x = Math.random() * (rect.width - 100);
      const y = Math.random() * 40;

      noButton.style.left = x + "px";
      noButton.style.top = y + "px";
    }

    noButton.addEventListener("touchstart", moveNoButton);
    noButton.addEventListener("click", moveNoButton);

    function yesClicked() {
      document.body.innerHTML = `
        <div style="
          height:100vh;
          display:flex;
          justify-content:center;
          align-items:center;
          background:linear-gradient(135deg,#ff9a9e,#fad0c4);
          font-family:'Comic Sans MS', cursive;
          text-align:center;
          padding:20px;
        ">
          <h1 style="color:#ff4d6d; font-size:1.8rem;">
            Yayyy Iti 💖💖💖<br><br>
            You’re officially my Valentine 😍<br><br>
            I Love You 💘
          </h1>
        </div>
      `;
    }

    // Heart animation (lighter for mobile)
    setInterval(() => {
      const heart = document.createElement("div");
      heart.className = "heart";
      heart.innerHTML = "💖";
      heart.style.left = Math.random() * window.innerWidth + "px";
      heart.style.fontSize = Math.random() * 18 + 12 + "px";
      document.body.appendChild(heart);

      setTimeout(() => heart.remove(), 5000);
    }, 400);

    function playMusic() {
      const iframe = document.getElementById("music");
      iframe.contentWindow.postMessage(
        '{"event":"command","func":"playVideo","args":""}',
        '*'
      );
    }
  </script>

</body>
</html>
