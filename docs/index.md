# :clock1: **Literature Clock**

<div id="image-container" style="text-align:center; margin-top: 2rem;"></div>

<script>
  const canvas = document.createElement("canvas");
  canvas.width = 800;
  canvas.height = 500;
  const ctx = canvas.getContext("2d");

  const background = new Image();
  background.src = "assets/how_to_build_it/hello_world.png"; // TODO change to final image

  background.onload = () => {
    ctx.drawImage(background, 0, 0, canvas.width, canvas.height); // Draw the background

    // Translate the context
    const centerX = canvas.width / 2;
    const centerY = canvas.height / 2;
    ctx.translate(centerX, centerY);

    // Tilt the context
    const skewX = -0.8; // horizontal skew
    const skewY = 0.2; // vertical skew
    ctx.transform(1, skewY, skewX, 1, 0, 0); // skew matrix
    ctx.rotate(-15 * Math.PI / 180); // slight rotation

    // Draw white box onto the translated-and-tilted context
    const boxWidth = 500;
    const boxHeight = 300;
    ctx.fillStyle = "#f8f9fa"; // text box background color TODO change to correct color
    ctx.fillRect(-boxWidth / 2, -boxHeight / 2, boxWidth, boxHeight);

    // Draw text inside the drawn box
    ctx.font = "bold 50px sans-serif";
    ctx.textAlign = "center";
    ctx.textBaseline = "middle";
    ctx.fillStyle = "#222222"; // text color TODO change to correct color
    ctx.fillText("This is a quote.", 0, 0);

    // Export to image and show
    const img = new Image();
    img.src = canvas.toDataURL("image/png");
    img.alt = "Literature clock.";
    img.style.maxWidth = "100%";

    document.getElementById("image-container").appendChild(img);
  };
</script>