<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Sanzora AI - Photo & Video Editor</title>

<style>
*{
  box-sizing:border-box;
  margin:0;
  padding:0;
  font-family:Arial,sans-serif;
}

body{
  background:#08090d;
  color:#fff;
  min-height:100vh;
}

header{
  height:70px;
  padding:0 18px;
  display:flex;
  align-items:center;
  justify-content:space-between;
  background:#10121a;
  border-bottom:1px solid #292c38;
  position:sticky;
  top:0;
  z-index:10;
}

.logo{
  font-size:25px;
  font-weight:800;
}

.logo span{
  color:#a477ff;
}

.premium{
  border:0;
  padding:11px 17px;
  border-radius:25px;
  color:white;
  font-weight:bold;
  background:linear-gradient(135deg,#805cff,#d25cff);
}

.container{
  max-width:950px;
  margin:auto;
  padding:25px 16px 50px;
}

.hero{
  text-align:center;
  padding:20px 0 25px;
}

.hero h1{
  font-size:34px;
  margin-bottom:10px;
}

.hero h1 span{
  color:#a477ff;
}

.hero p{
  color:#969aa8;
}

.upload{
  border:2px dashed #3a3d4b;
  background:#11131b;
  border-radius:22px;
  padding:35px 15px;
  text-align:center;
}

.upload-icon{
  font-size:48px;
  margin-bottom:10px;
}

.upload h2{
  margin-bottom:8px;
}

.upload p{
  color:#858997;
  margin-bottom:20px;
}

.select{
  display:inline-block;
  padding:14px 24px;
  border-radius:25px;
  background:#9873ff;
  font-weight:bold;
  cursor:pointer;
}

#fileInput{
  display:none;
}

.editor{
  display:none;
  margin-top:20px;
}

.preview{
  background:#050505;
  border-radius:20px;
  padding:10px;
  text-align:center;
}

#canvas{
  width:100%;
  max-height:550px;
  object-fit:contain;
  border-radius:14px;
  background:#000;
}

.panel{
  background:#11131b;
  border-radius:20px;
  margin-top:15px;
  padding:18px;
}

.panel h2{
  margin-bottom:15px;
}

.sliders{
  display:grid;
  gap:15px;
}

.slider label{
  display:flex;
  justify-content:space-between;
  margin-bottom:7px;
  color:#ddd;
}

input[type=range]{
  width:100%;
  accent-color:#9b78ff;
}

.tools{
  display:grid;
  grid-template-columns:repeat(4,1fr);
  gap:9px;
  margin-top:18px;
}

.tool{
  padding:13px 5px;
  border:1px solid #303340;
  border-radius:13px;
  background:#171922;
  color:white;
  cursor:pointer;
}

.tool:hover{
  border-color:#a477ff;
}

.effects{
  display:grid;
  grid-template-columns:repeat(4,1fr);
  gap:9px;
}

.effect{
  padding:14px 5px;
  border:1px solid #303340;
  border-radius:13px;
  background:#171922;
  color:#ddd;
  cursor:pointer;
}

.effect.active{
  border-color:#a477ff;
  background:#29203f;
}

.prompt{
  margin-top:15px;
  background:#11131b;
  padding:18px;
  border-radius:20px;
}

.prompt h2{
  margin-bottom:10px;
}

.prompt-row{
  display:flex;
  gap:8px;
}

#prompt{
  flex:1;
  padding:14px;
  border-radius:13px;
  border:1px solid #343744;
  background:#08090d;
  color:white;
  outline:none;
}

.ai{
  padding:0 18px;
  border:0;
  border-radius:13px;
  color:white;
  font-weight:bold;
  background:linear-gradient(135deg,#765cff,#d05cff);
}

.status{
  text-align:center;
  color:#9c9fac;
  margin-top:10px;
  min-height:20px;
}

.actions{
  display:grid;
  grid-template-columns:1fr 1fr;
  gap:10px;
  margin-top:15px;
}

.reset,
.download{
  padding:15px;
  border-radius:15px;
  font-weight:bold;
  cursor:pointer;
}

.reset{
  background:#171922;
  border:1px solid #353845;
  color:white;
}

.download{
  border:0;
  color:white;
  background:linear-gradient(135deg,#9873ff,#d25cff);
}

.premium-box{
  margin-top:20px;
  padding:22px;
  text-align:center;
  border-radius:20px;
  background:#171226;
  border:1px solid #45356b;
}

.premium-box h2{
  margin-bottom:8px;
}

.premium-box p{
  color:#aaa5b7;
  line-height:1.5;
}

footer{
  text-align:center;
  padding:30px;
  color:#626572;
  font-size:13px;
}

@media(max-width:600px){

  .hero h1{
    font-size:28px;
  }

  .effects{
    grid-template-columns:repeat(2,1fr);
  }

  .tools{
    grid-template-columns:repeat(2,1fr);
  }

  .prompt-row{
    flex-direction:column;
  }

  .ai{
    padding:13px;
  }
}
</style>
</head>

<body>

<header>
  <div class="logo">Sanzora <span>AI</span></div>

  <button class="premium" onclick="showPremium()">
    💎 Premium
  </button>
</header>

<div class="container">

<section class="hero">
  <h1>Create with <span>Sanzora AI</span></h1>
  <p>Powerful photo editing made simple.</p>
</section>

<section class="upload">

  <div class="upload-icon">🖼️</div>

  <h2>Start Editing</h2>

  <p>Select a photo from your phone.</p>

  <label for="fileInput" class="select">
    📁 Select Photo
  </label>

  <input
    id="fileInput"
    type="file"
    accept="image/*">

</section>

<section class="editor" id="editor">

  <div class="preview">
    <canvas id="canvas"></canvas>
  </div>

  <div class="panel">

    <h2>🎨 Adjust</h2>

    <div class="sliders">

      <div class="slider">
        <label>
          <span>Brightness</span>
          <span id="brightnessValue">100%</span>
        </label>

        <input
          id="brightness"
          type="range"
          min="0"
          max="200"
          value="100">
      </div>

      <div class="slider">
        <label>
          <span>Contrast</span>
          <span id="contrastValue">100%</span>
        </label>

        <input
          id="contrast"
          type="range"
          min="0"
          max="200"
          value="100">
      </div>

      <div class="slider">
        <label>
          <span>Saturation</span>
          <span id="saturationValue">100%</span>
        </label>

        <input
          id="saturation"
          type="range"
          min="0"
          max="200"
          value="100">
      </div>

    </div>

    <div class="tools">

      <button class="tool" onclick="rotateLeft()">
        ↶ Rotate
      </button>

      <button class="tool" onclick="rotateRight()">
        ↷ Rotate
      </button>

      <button class="tool" onclick="flipImage()">
        ↔️ Flip
      </button>

      <button class="tool" onclick="resetEdit()">
        🔄 Reset
      </button>

    </div>

  </div>

  <div class="panel">

    <h2>✨ Effects</h2>

    <div class="effects">

      <button class="effect active"
        onclick="applyEffect(this,'normal')">
        Original
      </button>

      <button class="effect"
        onclick="applyEffect(this,'cinematic')">
        🎬 Cinematic
      </button>

      <button class="effect"
        onclick="applyEffect(this,'vintage')">
        📸 Vintage
      </button>

      <button class="effect"
        onclick="applyEffect(this,'bw')">
        ⚫ B&W
      </button>

      <button class="effect"
        onclick="applyEffect(this,'warm')">
        🔥 Warm
      </button>

      <button class="effect"
        onclick="applyEffect(this,'cool')">
        ❄️ Cool
      </button>

      <button class="effect"
        onclick="applyEffect(this,'dream')">
        🌙 Dream
      </button>

      <button class="effect"
        onclick="applyEffect(this,'vivid')">
        🌈 Vivid
      </button>

      <button class="effect"
        onclick="applyEffect(this,'retro')">
        📼 Retro
      </button>

      <button class="effect"
        onclick="applyEffect(this,'neon')">
        💜 Neon
      </button>

      <button class="effect"
        onclick="applyEffect(this,'fade')">
        🌫️ Fade
      </button>

      <button class="effect"
        onclick="applyEffect(this,'dramatic')">
        🎞️ Dramatic
      </button>

    </div>

  </div>

  <div class="prompt">

    <h2>🤖 AI Prompt Editing</h2>

    <div class="prompt-row">

      <input
        id="prompt"
        type="text"
        placeholder="Example: Make my photo cinematic">

      <button class="ai" onclick="aiEdit()">
        ✨ AI Edit
      </button>

    </div>

    <div class="status" id="status"></div>

  </div>

  <div class="actions">

    <button class="reset" onclick="resetEdit()">
      🔄 Reset
    </button>

    <button class="download" onclick="downloadImage()">
      💾 Download
    </button>

  </div>

  <div class="premium-box">

    <h2>💎 Sanzora AI Premium</h2>

    <p>
      1000+ Effects • Advanced AI • Animations •
      Premium Templates • High Quality Export
    </p>

  </div>

</section>

</div>

<footer>
  © 2026 Sanzora AI — Photo & Video Editor
</footer>

<script>

const fileInput =
document.getElementById("fileInput");

const editor =
document.getElementById("editor");

const canvas =
document.getElementById("canvas");

const ctx =
canvas.getContext("2d");

const status =
document.getElementById("status");

let image = new Image();

let rotation = 0;

let flipX = 1;

let currentEffect = "normal";


fileInput.addEventListener("change", function(){

  const file = this.files[0];

  if(!file){
    return;
  }

  if(!file.type.startsWith("image/")){
    alert("Please select an image.");
    return;
  }

  const url =
  URL.createObjectURL(file);

  image.onload = function(){

    editor.style.display = "block";

    rotation = 0;

    flipX = 1;

    currentEffect = "normal";

    resetControlsOnly();

    draw();

    status.innerText =
    "✅ Photo loaded successfully.";

    URL.revokeObjectURL(url);
  };

  image.src = url;

});


document
.getElementById("brightness")
.addEventListener("input", function(){

  document
  .getElementById("brightnessValue")
  .innerText = this.value + "%";

  draw();

});


document
.getElementById("contrast")
.addEventListener("input", function(){

  document
  .getElementById("contrastValue")
  .innerText = this.value + "%";

  draw();

});


document
.getElementById("saturation")
.addEventListener("input", function(){

  document
  .getElementById("saturationValue")
  .innerText = this.value + "%";

  draw();

});


function filterString(){

  const brightness =
  document.getElementById("brightness").value;

  const contrast =
  document.getElementById("contrast").value;

  const saturation =
  document.getElementById("saturation").value;

  let filter =
  "brightness(" + brightness + "%) " +
  "contrast(" + contrast + "%) " +
  "saturate(" + saturation + "%)";


  if(currentEffect === "cinematic"){
    filter +=
    " contrast(115%) saturate(110%)";
  }

  if(currentEffect === "vintage"){
    filter +=
    " sepia(45%) contrast(90%)";
  }

  if(currentEffect === "bw"){
    filter +=
    " grayscale(100%)";
  }

  if(currentEffect === "warm"){
    filter +=
    " sepia(25%) saturate(130%)";
  }

  if(currentEffect === "cool"){
    filter +=
    " hue-rotate(20deg) saturate(115%)";
  }

  if(currentEffect === "dream"){
    filter +=
    " brightness(110%) saturate(120%)";
  }

  if(currentEffect === "vivid"){
    filter +=
    " saturate(170%) contrast(110%)";
  }

  if(currentEffect === "retro"){
    filter +=
    " sepia(50%) contrast(105%)";
  }

  if(currentEffect === "neon"){
    filter +=
    " saturate(200%) contrast(125%)";
  }

  if(currentEffect === "fade"){
    filter +=
    " brightness(110%) contrast(80%) saturate(75%)";
  }

  if(currentEffect === "dramatic"){
    filter +=
    " contrast(150%) saturate(120%)";
  }

  return filter;
}


function draw(){

  if(!image.src){
    return;
  }

  const w =
  image.naturalWidth;

  const h =
  image.naturalHeight;


  if(rotation % 180 === 0){

    canvas.width = w;
    canvas.height = h;

  }else{

    canvas.width = h;
    canvas.height = w;

  }


  ctx.save();

  ctx.clearRect(
    0,
    0,
    canvas.width,
    canvas.height
  );


  ctx.translate(
    canvas.width / 2,
    canvas.height / 2
  );


  ctx.rotate(
    rotation * Math.PI / 180
  );


  ctx.scale(
    flipX,
    1
  );


  ctx.filter =
  filterString();


  ctx.drawImage(
    image,
    -w / 2,
    -h / 2,
    w,
    h
  );


  ctx.restore();
}


function applyEffect(button,effectName){

  document
  .querySelectorAll(".effect")
  .forEach(function(item){
    item.classList.remove("active");
  });


  button.classList.add("active");

  currentEffect =
  effectName;

  draw();

  status.innerText =
  "✨ " +
  button.innerText.trim() +
  " applied.";
}


function rotateLeft(){

  rotation -= 90;

  draw();

  status.innerText =
  "↶ Rotated left.";
}


function rotateRight(){

  rotation += 90;

  draw();

  status.innerText =
  "↷ Rotated right.";
}


function flipImage(){

  flipX *= -1;

  draw();

  status.innerText =
  "↔️ Image flipped.";
}


function resetControlsOnly(){

  document
  .getElementById("brightness")
  .value = 100;

  document
  .getElementById("contrast")
  .value = 100;

  document
  .getElementById("saturation")
  .value = 100;

  document
  .getElementById("brightnessValue")
  .innerText = "100%";

  document
  .getElementById("contrastValue")
  .innerText = "100%";

  document
  .getElementById("saturationValue")
  .innerText = "100%";

}


function resetEdit(){

  rotation = 0;

  flipX = 1;

  currentEffect = "normal";

  resetControlsOnly();


  document
  .querySelectorAll(".effect")
  .forEach(function(item){
    item.classList.remove("active");
  });


  document
  .querySelector(".effect")
  .classList.add("active");


  draw();

  status.innerText =
  "🔄 Editing reset.";
}


function downloadImage(){

  if(!image.src){

    alert(
      "पहिले photo select कर."
    );

    return;
  }


  const link =
  document.createElement("a");


  link.download =
  "Sanzora-AI-Edited.png";


  link.href =
  canvas.toDataURL(
    "image/png"
  );


  link.click();


  status.innerText =
  "✅ Edited photo downloaded.";
}


function aiEdit(){

  if(!image.src){

    status.innerText =
    "📁 पहिले photo select कर.";

    return;
  }


  const text =
  document
  .getElementById("prompt")
  .value
  .toLowerCase()
  .trim();


  if(!text){

    status.innerText =
    "🤖 AI prompt लिही.";

    return;
  }


  if(
    text.includes("cinematic") ||
    text.includes("movie")
  ){

    currentEffect =
    "cinematic";

  }else if(
    text.includes("vintage") ||
    text.includes("old")
  ){

    currentEffect =
    "vintage";

  }else if(
    text.includes("black") ||
    text.includes("white") ||
    text.includes("b&w")
  ){

    currentEffect =
    "bw";

  }else if(
    text.includes("warm")
  ){

    currentEffect =
    "warm";

  }else if(
    text.includes("cool")
  ){

    currentEffect =
    "cool";

  }else if(
    text.includes("vivid") ||
    text.includes("colorful")
  ){

    currentEffect =
    "vivid";

  }else if(
    text.includes("retro")
  ){

    currentEffect =
    "retro";

  }else if(
    text.includes("neon")
  ){

    currentEffect =
    "neon";

  }else{

    currentEffect =
    "cinematic";
  }


  document
  .querySelectorAll(".effect")
  .forEach(function(item){
    item.classList.remove("active");
  });


  draw();


  status.innerText =
  "✨ Sanzora AI applied your prompt.";
}


function showPremium(){

  alert(
    "💎 Sanzora AI Premium\n\n" +
    "1000+ Effects\n" +
    "Advanced AI Editing\n" +
    "Animations\n" +
    "Premium Templates\n" +
    "High Quality Export\n\n" +
    "Premium system coming soon!"
  );
}

</script>

</body>
</html>
