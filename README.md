# kids-video
<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Весёлый мир детей</title>
  <style>
    * { box-sizing: border-box; }
    body {
      margin: 0;
      font-family: Arial, sans-serif;
      background: #f0f8ff;
      color: #26344a;
    }
    header {
      background: linear-gradient(120deg, #6c63ff, #ff78b7);
      color: white;
      padding: 28px 16px;
      text-align: center;
      border-radius: 0 0 28px 28px;
    }
    header h1 { margin: 0 0 10px; font-size: 30px; }
    header p { margin: 0; }
    .search {
      display: block;
      width: calc(100% - 32px);
      margin: 20px auto;
      padding: 14px;
      border: 1px solid #ddd;
      border-radius: 14px;
      font-size: 16px;
    }
    main { padding: 0 16px 30px; }
    h2 { margin-top: 25px; }
    .videos {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(145px, 1fr));
      gap: 14px;
    }
    .card {
      background: white;
      border-radius: 18px;
      overflow: hidden;
      box-shadow: 0 3px 12px #26344a12;
    }
    .cover {
      min-height: 120px;
      display: grid;
      place-items: center;
      font-size: 55px;
      background: #ffebad;
    }
    .card:nth-child(2) .cover { background: #c8f7dc; }
    .card:nth-child(3) .cover { background: #dcd5ff; }
    .card:nth-child(4) .cover { background: #ffd6e7; }
    .info { padding: 12px; }
    .info h3 { margin: 0 0 8px; font-size: 17px; }
    .info p { font-size: 13px; color: #667085; }
    button {
      width: 100%;
      padding: 11px;
      background: #6c63ff;
      color: white;
      border: 0;
      border-radius: 10px;
      font-size: 15px;
      cursor: pointer;
    }
    #player { width: 100%; margin-top: 20px; }
    #player iframe {
      width: 100%;
      aspect-ratio: 16 / 9;
      border: 0;
      border-radius: 16px;
    }
    footer {
      text-align: center;
      padding: 22px;
      color: #667085;
      font-size: 13px;
    }
  </style>
</head>
<body>
  <header>
    <h1>🌈 Весёлый мир детей</h1>
    <p>Учимся, играем и смотрим вместе!</p>
  </header>

  <input class="search" id="search"
    placeholder="🔎 Найди любимое видео..."
    aria-label="Поиск видео">

  <main>
    <h2>🎬 Наши видео</h2>
    <p>Выбери видео, чтобы посмотреть его.</p>

    <div class="videos" id="videos"></div>

    <div id="player" aria-live="polite"></div>
  </main>

  <footer>
    🌟 Весёлый мир детей · Сайт для всей семьи
  </footer>

  <script>
    const videos = [
      {
        title: "Весёлые песенки",
        emoji: "🎵",
        description: "Песни и музыка для детей",
        url: ""
      },
      {
        title: "Мир животных",
        emoji: "🦁",
        description: "Знакомимся с животными",
        url: ""
      },
      {
        title: "Учимся считать",
        emoji: "🔢",
        description: "Считаем и учимся играя",
        url: ""
      },
      {
        title: "Сказки на ночь",
        emoji: "🧸",
        description: "Добрые сказки для малышей",
        url: ""
      }
    ];

    const container = document.getElementById("videos");

    function render(list) {
      container.innerHTML = "";

      list.forEach(video => {
        const card = document.createElement("article");
        card.className = "card";

        const cover = document.createElement("div");
        cover.className = "cover";
        cover.textContent = video.emoji;

        const info = document.createElement("div");
        info.className = "info";

        const title = document.createElement("h3");
        title.textContent = video.title;

        const desc = document.createElement("p");
        desc.textContent = video.description;

        const btn = document.createElement("button");
        btn.textContent = video.url ? "▶ Смотреть" : "▶ Скоро";

        btn.addEventListener("click", () => {
          if (!video.url) {
            alert("Видео пока не добавлено. Скоро здесь появятся мультфильмы!");
            return;
          }

          const player = document.getElementById("player");
          player.replaceChildren();

          const frame = document.createElement("iframe");
          frame.src = video.url;
          frame.title = video.title;
          frame.allowFullscreen = true;
          frame.allow =
            "accelerometer; autoplay; encrypted-media; picture-in-picture";
          player.appendChild(frame);
          player.scrollIntoView({ behavior: "smooth" });
        });

        info.append(title, desc, btn);
        card.append(cover, info);
        container.appendChild(card);
      });
    }

    document.getElementById("search").addEventListener("input", event => {
      const query = event.target.value.toLowerCase();
      render(videos.filter(video =>
        (video.title + " " + video.description)
          .toLowerCase().includes(query)
      ));
    });

    render(videos);
  </script>
</body>
</html>

my kids video website
