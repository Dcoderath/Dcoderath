<!-- Centered Quote Box -->
<div align="center">
  <div style="background-color: white; padding: 20px; border-radius: 10px; width: fit-content; box-shadow: 0 0 10px rgba(0,0,0,0.1);">
    <blockquote>
      <em>“Exploration and curiosity are the fuels of creation.”</em><br>
      — <span style="color:green;"><strong>D.code.rath</strong></span>
    </blockquote>
  </div>
</div>

# Bishop Tilting (Perspective)

A simple pixel-based bishop tilt animation using HTML, CSS, and JavaScript.

---

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>Bishop Tilting (Perspective)</title>
  <link rel="stylesheet" href="style.css">
  <style>
    body {
      background: #f0f0f0;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      margin: 0;
    }

    #grid {
      display: grid;
      grid-template-columns: repeat(20, 20px);
      grid-template-rows: repeat(20, 20px);
      gap: 0; /* no gap, we use border instead */
    }

    .pixel {
      width: 20px;
      height: 20px;
      background-color: #ccc;
      border: 1px solid #eee;  /* 👈 small box effect */
      box-sizing: border-box;
      transition: background-color 0.2s ease;
    }

    .pixel.on {
      background-color: black;
    }
  </style>
</head>
<body>
  <div id="grid"></div>
  <script>
    const bishopNeutral = [
      "00000000010000000000",
      "00000000111000000000",
      "00000001101100000000",
      "00000011000110000000",
      "00000110000011000000",
      "00000100000001000000",
      "00001100000001100000",
      "00011110000011110000",
      "00001110000011100000",
      "00001110000011100000",
      "00000111000111000000",
      "00000011111110000000",
      "00000001111100000000",
      "00000001111100000000",
      "00000001111100000000",
      "00000011111110000000",
      "00000011111110000000",
      "00000001111100000000",
      "00000000111000000000",
      "00000111111111000000"
    ];

    // Shift pixels left or right by 1 column to simulate tilt
    function shiftPattern(pattern, direction) {
      return pattern.map(row => {
        if (direction === 'left') return row.slice(1) + "0";
        if (direction === 'right') return "0" + row.slice(0, -1);
        return row;
      });
    }

    const container = document.getElementById("grid");
    const pixelDivs = [];

    // Build static 20x20 grid
    for (let i = 0; i < 400; i++) {
      const pixel = document.createElement("div");
      pixel.classList.add("pixel");
      container.appendChild(pixel);
      pixelDivs.push(pixel);
    }

    let state = 0;
    setInterval(() => {
      let pattern;
      if (state === 0) pattern = shiftPattern(bishopNeutral, 'left');
      else if (state === 1) pattern = bishopNeutral;
      else pattern = shiftPattern(bishopNeutral, 'right');

      for (let row = 0; row < 20; row++) {
        for (let col = 0; col < 20; col++) {
          const i = row * 20 + col;
          if (pattern[row][col] === "1") {
            pixelDivs[i].classList.add("on");
          } else {
            pixelDivs[i].classList.remove("on");
          }
        }
      }

      state = (state + 1) % 3; // left → center → right → repeat
    }, 800);
  </script>
</body>
</html>
