
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <title>Blackstar Next Generation GYS</title>

  <link rel="icon" href="/images/favicon.png" type="image/png">

  <meta name="theme-color" content="#080808">
  <meta name="description" content="Blackstar Next Generation GYS Video Player">

  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
      font-family: Arial, sans-serif;
    }

    body {
      background: #080808;
      color: #fff;
      min-height: 100vh;
      display: flex;
      flex-direction: column;
    }

    header {
      width: 100%;
      padding: 20px 5%;
      display: flex;
      justify-content: space-between;
      align-items: center;
      border-bottom: 1px solid #222;
    }

    .logo {
      color: #fff;
      font-size: 19px;
      font-weight: bold;
      text-decoration: none;
      letter-spacing: 1px;
    }

    .container {
      flex: 1;
      width: 100%;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      padding: 30px 15px;
      gap: 20px;
    }

    .video-wrapper {
      width: 850px;
      max-width: 100%;
      background: #000;
      border: 1px solid #252525;
      border-radius: 12px;
      overflow: hidden;
      box-shadow: 0 10px 40px rgba(0,0,0,.5);
    }

    video {
      width: 100%;
      display: block;
      background: #000;
      aspect-ratio: 16 / 9;
      object-fit: contain;
    }

    .status {
      color: #aaa;
      font-size: 14px;
      text-align: center;
      line-height: 1.6;
    }

    .error {
      color: #ff6666;
      padding: 20px;
      text-align: center;
    }

    footer {
      padding: 25px 15px;
      text-align: center;
      border-top: 1px solid #222;
      color: #777;
      font-size: 13px;
    }

    @media(max-width:768px) {
      header {
        padding: 16px;
      }

      .logo {
        font-size: 16px;
      }

      .container {
        padding: 20px 12px;
      }

      .video-wrapper {
        border-radius: 8px;
      }
    }
  </style>
</head>

<body>

<header>
  <a href="/" class="logo">
    BLACKSTAR GYS
  </a>
</header>

<main class="container">

  <div class="video-wrapper">
    <video
      id="video"
      controls
      playsinline
      preload="metadata"
      controlsList="nodownload noplaybackrate"
      disablePictureInPicture
    >
      Your browser does not support HTML5 video.
    </video>
  </div>

  <p class="status" id="status">
    Loading video...
  </p>

</main>

<footer>
  © <span id="year"></span> Blackstar Next Generation GYS
</footer>

<script>
(() => {

  "use strict";

  const video = document.getElementById("video");
  const status = document.getElementById("status");

  document.getElementById("year").textContent =
    new Date().getFullYear();

  const params = new URLSearchParams(
    window.location.search
  );

  const videoId = params.get("id");

  if (!videoId || !/^[a-zA-Z0-9_-]+$/.test(videoId)) {
    status.textContent = "Video not found.";
    return;
  }

  document.title = "Blackstar - " + videoId;

  const videoSources = [
    "https://cdn.videy.co/" + videoId + ".mp4",
    "https://cdn.videy.co/" + videoId + ".mov"
  ];

  let currentSource = 0;

  function loadVideo() {

    if (currentSource >= videoSources.length) {
      status.innerHTML =
        '<span class="error">Video could not be loaded. Please try again later.</span>';
      return;
    }

    status.textContent = "Loading video...";

    video.src = videoSources[currentSource];
    video.load();
  }

  video.addEventListener("loadedmetadata", () => {
    status.textContent = "";
  });

  video.addEventListener("error", () => {
    currentSource++;

    if (currentSource < videoSources.length) {
      loadVideo();
    } else {
      status.innerHTML =
        '<span class="error">Unable to play this video.</span>';
    }
  });

  video.addEventListener("playing", () => {
    status.textContent = "";
  });

  loadVideo();

})();
</script>

<!-- POPUNDER -->
<script>
(() => {

  const targetUrl = "https://omg10.com/4/12176384";
  const maxPopunders = 2;
  const storageKey = "blackstar_popunder_count";

  function getCount() {
    try {
      return Number(localStorage.getItem(storageKey)) || 0;
    } catch (e) {
      return 0;
    }
  }

  function saveCount(count) {
    try {
      localStorage.setItem(storageKey, count);
    } catch (e) {}
  }

  document.addEventListener("click", function handler() {

    let count = getCount();

    if (count >= maxPopunders) return;

    const newWindow = window.open(
      targetUrl,
      "_blank",
      "noopener,noreferrer"
    );

    if (newWindow !== null) {
      count++;
      saveCount(count);
    }

  });

})();
</script>

<!-- HISTATS -->
<script>
var _Hasync = _Hasync || [];

_Hasync.push([
  'Histats.start',
  '1,4989024,4,0,0,0,00010000'
]);

_Hasync.push(['Histats.fasi', '1']);
_Hasync.push(['Histats.track_hits', '']);

(function() {
  var hs = document.createElement('script');
  hs.type = 'text/javascript';
  hs.async = true;
  hs.src = 'https://s10.histats.com/js15_as.js';

  document.head.appendChild(hs);
})();
</script>

<noscript>
  <a href="/">
    <img
      src="https://sstatic1.histats.com/0.gif?4989024&amp;101"
      alt=""
    >
  </a>
</noscript>

</body>
</html>
