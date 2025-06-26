# :clock1: **Literature Clock**

<div id="image-container" style="text-align:center; margin-top: 2rem;"></div>

<script>
const canvas = document.createElement("canvas");
const ctx = canvas.getContext("2d");

const background = new Image();
background.src = "assets/how_to_build_it/lc-in-sita.jpg"; // TODO change to final image

background.onload = () => {
  const aspectRatio = background.naturalWidth / background.naturalHeight;
  const desiredWidth = 1000;
  const desiredHeight = desiredWidth / aspectRatio;

  canvas.width = desiredWidth;
  canvas.height = desiredHeight;

  ctx.drawImage(background, 0, 0, canvas.width, canvas.height);

  // Define 4 corners of the desired quadrilateral (in clockwise order)
  const topLeft = { x: 320, y: 203 };
  const topRight = { x: 647, y: 211 };
  const bottomRight = { x: 611, y: 460 };
  const bottomLeft = { x: 273, y: 409 };

  // Create an offscreen canvas with the box content
  const boxWidth = 500;
  const boxHeight = 300;
  const boxCanvas = document.createElement("canvas");
  boxCanvas.width = boxWidth;
  boxCanvas.height = boxHeight;
  const boxCtx = boxCanvas.getContext("2d");

  // Fill white background
  boxCtx.fillStyle = "#c3c3c3";
  boxCtx.fillRect(0, 0, boxWidth, boxHeight);

  // Draw the text in the center
  boxCtx.fillStyle = "#222222";
  boxCtx.font = "bold 30px sans-serif";
  boxCtx.textAlign = "center";
  boxCtx.textBaseline = "middle";
  boxCtx.fillText("This is a quote.", boxWidth / 2, boxHeight / 2);

  // Use perspective transform via 3rd party lib (epistemex/perspective-transform)
  // Or do basic triangle warping (split into two triangles)

  function drawTriangle(src, sx0, sy0, sx1, sy1, sx2, sy2, dx0, dy0, dx1, dy1, dx2, dy2) {
    // Calculate affine transform
    ctx.save();
    ctx.beginPath();
    ctx.moveTo(dx0, dy0);
    ctx.lineTo(dx1, dy1);
    ctx.lineTo(dx2, dy2);
    ctx.closePath();
    ctx.clip();

    const denom = (sx0 * (sy1 - sy2) + sx1 * (sy2 - sy0) + sx2 * (sy0 - sy1));
    const a = ((dx0 * (sy1 - sy2) + dx1 * (sy2 - sy0) + dx2 * (sy0 - sy1)) / denom);
    const b = ((dx0 * (sx2 - sx1) + dx1 * (sx0 - sx2) + dx2 * (sx1 - sx0)) / denom);
    const c = ((dx0 * (sx1 * sy2 - sx2 * sy1) + dx1 * (sx2 * sy0 - sx0 * sy2) + dx2 * (sx0 * sy1 - sx1 * sy0)) / denom);
    const d = ((dy0 * (sy1 - sy2) + dy1 * (sy2 - sy0) + dy2 * (sy0 - sy1)) / denom);
    const e = ((dy0 * (sx2 - sx1) + dy1 * (sx0 - sx2) + dy2 * (sx1 - sx0)) / denom);
    const f = ((dy0 * (sx1 * sy2 - sx2 * sy1) + dy1 * (sx2 * sy0 - sx0 * sy2) + dy2 * (sx0 * sy1 - sx1 * sy0)) / denom);

    ctx.transform(a, d, b, e, c, f);
    ctx.drawImage(src, 0, 0);
    ctx.restore();
  }

  // Split the box into two triangles
  drawTriangle(
    boxCanvas,
    0, 0,                      // top-left
    boxWidth, 0,              // top-right
    0, boxHeight,             // bottom-left
    topLeft.x, topLeft.y,
    topRight.x, topRight.y,
    bottomLeft.x, bottomLeft.y
  );

  drawTriangle(
    boxCanvas,
    boxWidth, 0,
    boxWidth, boxHeight,
    0, boxHeight,
    topRight.x, topRight.y,
    bottomRight.x, bottomRight.y,
    bottomLeft.x, bottomLeft.y
  );

  // Export to image
  const img = new Image();
  img.src = canvas.toDataURL("image/png");
  img.alt = "Literature clock.";
  img.style.maxWidth = "100%";
  document.getElementById("image-container").appendChild(img);
};
</script>