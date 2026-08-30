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
    display:flex;
    align-items:center;
    justify-content:space-between;
    padding:0 18px;
    background:#10121a;
    border-bottom:1px solid #292c38;
    position:sticky;
    top:0;
    z-index:20;
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
    border-radius:25px;
    padding:11px 17px;
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
    padding:30px 15px;
    text-align:center;
}

.upload-icon{
    font-size:45px;
}

.upload h2{
    margin:10px 0 8px;
}

.upload p{
    color:#858997;
    margin-bottom:18px;
}

.select{
    display:inline-block;
    padding:13px 22px;
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

.controls{
    background:#11131b;
    border-radius:20px;
    margin-top:15px;
    padding:18px;
}

.controls h2{
    margin-bottom:15px;
}

.sliders{
    display:grid;
    gap:15px;
}

.slider label{
    display:flex;
    justify-content:space-between;
    color:#d8d9df;
    margin-bottom:6px;
}

input[type="range"]{
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
    border:1px solid #2d303c;
    background:#171922;
    color:white;
    padding:13px 5px;
    border-radius:13px;
    font-size:13px;
    cursor:pointer;
}

.tool:hover{
    border-color:#9b78ff;
}

.effects{
    display:grid;
    grid-template-columns:repeat(4,1fr);
    gap:9px;
}

.effect{
    border:1px solid #2d303c;
    background:#171922;
    color:#ddd;
    padding:14px 5px;
    border-radius:13px;
    cursor:pointer;
}

.effect.active{
    border-color:#a477ff;
    background:#29203f;
}

.prompt{
    margin-top:18px;
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
    background:#08090d;
    color:#fff;
    border:1px solid #343744;
    border-radius:13px;
    padding:13px;
    outline:none;
}

.ai{
    border:0;
    background:linear-gradient(135deg,#765cff,#d05cff);
    color:#fff;
    border-radius:13px;
    padding:0 18px;
    font-weight:bold;
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

.reset{
    padding:15px;
    border:1px solid #353845;
    background:#171922;
    color:#fff;
    border-radius:15px;
    font-weight:bold;
}

.download{
    padding:15px;
    border:0;
    background:linear-gradient(135deg,#9873ff,#d25cff);
    color:#fff;
    border-radius:15px;
    font-weight:bold;
}

.premium-box{
    margin-top:20px;
    padding:22px;
    text-align:center;
    border-radius:20px;
    background:linear-gradient(135deg,#171226,#21162d);
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

    <button class="premium" onclick="premium()">
        💎 Premium
    </button>
</header>

<div class="container">

<section class="hero">
    <h1>Create with <span>Sanzora AI</span></h1>
    <p>AI powered photo editing made simple.</p>
</section>

<section class="upload" id="uploadBox">

    <div class="upload-icon">🖼️</div>

    <h2>Start Editing</h2>

    <p>Select a photo from your device.</p>

    <label for="fileInput" class="select">
        📁 Select Photo
    </label>

    <input id="fileInput" type="file" accept="image/*">

</section>


<section class="editor" id="editor">

    <div class="preview">
        <canvas id="canvas"></canvas>
    </div>


    <div class="controls">

        <h2>🎨 Adjust</h2>

        <div class="sliders">

            <div class="slider">
                <label>
                    Brightness
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
                    Contrast
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
                    Saturation
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

            <button class="tool" onclick="rotateLeft()">↶ Rotate</button>

            <button class="tool" onclick="rotateRight()">↷ Rotate</button>

            <button class="tool" onclick="flip()">↔️ Flip</button>

            <button class="tool" onclick="resetEdit()">🔄 Reset</button>

        </div>

    </div>


    <div class="controls">

        <h2>✨ Effects</h2>

        <div class="effects">

            <button class="effect active"
            onclick="effect(this,'normal')">
            Original
            </button>

            <button class="effect"
            onclick="effect(this,'cinematic')">
            🎬 Cinematic
            </button>

            <button class="effect"
            onclick="effect(this,'vintage')">
            📸 Vintage
            </button>

            <button class="effect"
            onclick="effect(this,'bw')">
            ⚫ B&W
            </button>

            <button class="effect"
            onclick="effect(this,'warm')">
            🔥 Warm
            </button>

            <button class="effect"
            onclick="effect(this,'cool')">
            ❄️ Cool
            </button>

            <button class="effect"
            onclick="effect(this,'dream')">
            🌙 Dream
            </button>

            <button class="effect"
            onclick="effect(this,'vivid')">
            🌈 Vivid
            </button>

            <button class="effect"
            onclick="effect(this,'retro')">
            📼 Retro
            </button>

            <button class="effect"
            onclick="effect(this,'neon')">
            💜 Neon
            </button>

            <button class="effect"
            onclick="effect(this,'fade')">
            🌫️ Fade
            </button>

            <button class="effect"
            onclick="effect(this,'dramatic')">
            🎞️ Dramatic
            </button>

        </div>

    </div>


    <div class="prompt">

        <h2>🤖 AI Prompt</h2>

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
            💾 Download Photo
        </button>

    </div>


    <div class="premium-box">

        <h2>💎 Sanzora AI Premium</h2>

        <p>
            1000+ effects, advanced AI tools,
            animations, premium templates and
            high-quality export — coming soon.
        </p>

    </div>

</section>

</div>


<footer>
    © 2026 Sanzora AI — AI Photo & Video Editor
</footer>


<script>

const fileInput =
document.getElementById("fileInput");

const canvas =
document.getElementById("canvas");

const ctx =
canvas.getContext("2d");

const editor =
document.getElementById("editor");

let image = new Image();

let rotation = 0;

let flipX = 1;

let selectedEffect = "normal";


fileInput.addEventListener("change",function(){

    const file = this.files[0];

    if(!file) return;

    const url = URL.createObjectURL(file);

    image.onload = function(){

        rotation = 0;
        flipX = 1;

        editor.style.display = "block";

        draw();

    };

    image.src = url;

});


document
.getElementById("brightness")
.addEventListener("input",function(){

    document.getElementById("brightnessValue")
    .innerText = this.value + "%";

    draw();

});


document
.getElementById("contrast")
.addEventListener("input",function(){

    document.getElementById("contrastValue")
    .innerText = this.value + "%";

    draw();

});


document
.getElementById("saturation")
.addEventListener("input",function(){

    document.getElementById("saturationValue")
    .innerText = this.value + "%";

    draw();

});


function getFilter(){

    let b =
    document.getElementById("brightness").value;

    let c =
    document.getElementById("contrast").value;

    let s =
    document.getElementById("saturation").value;

    let filter =
    `brightness(${b}%) contrast(${c}%) saturate(${s}%)`;

    if(selectedEffect === "cinematic")
        filter += " contrast(115%) saturate(110%)";

    if(selectedEffect === "vintage")
        filter += " sepia(35%) contrast(90%)";

    if(selectedEffect === "bw")
        filter += " grayscale(100%)";

    if(selectedEffect === "warm")
        filter += " sepia(25%) saturate(125%)";

    if(selectedEffect === "cool")
        filter += " hue-rotate(15deg) saturate(110%)";

    if(selectedEffect === "dream")
        filter += " brightness(110%) saturate(115%) blur(.3px)";

    if(selectedEffect === "vivid")
        filter += " saturate(155%) contrast(110%)";

    if(selectedEffect === "retro")
        filter += " sepia(45%) contrast(105%)";

    if(selectedEffect === "neon")
        filter += " saturate(190%) contrast(125%)";

    if(selectedEffect === "fade")
        filter += " brightness(110%) contrast(80%) saturate(75%)";

    if(selectedEffect === "dramatic")
        filter += " contrast(145%) saturate(115%)";

    return filter;
}


function draw(){

    if(!image.src) return;

    const w = image.naturalWidth;
    const h = image.naturalHeight;

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

    ctx.scale(flipX,1);

    ctx.filter = getFilter();

    ctx.drawImage(
        image,
        -w/2,
        -h/2,
        w,
        h
    );

    ctx.restore();
}


function effect(button,name){

    document
    .querySelectorAll(".effect")
    .forEach(e =>
        e.classList.remove("active")
    );

    button.classList.add("active");

    selectedEffect = name;

    draw();

    document.getElementById("status")
    .innerText =
    "✨ " + button.innerText.trim() +
    " applied.";
}


function rotateLeft(){

    rotation -= 90;

    draw();
}


function rotateRight(){

    rotation += 90;

    draw();
}


function flip(){

    flipX *= -1;

    draw();
}


function resetEdit(){

    document.getElementById("brightness").value = 100;
    document.getElementById("contrast").value = 100;
    document.getElementById("saturation").value = 100;

    document.getElementById("brightnessValue").innerText = "100%";
    document.getElementById("contrastValue").innerText = "100%";
    document.getElementById("saturationValue").innerText = "100%";

    rotation = 0;
    flipX = 1;
    selectedEffect = "normal";

    document
    .querySelectorAll(".effect")
    .forEach(e =>
        e.classList.remove("active")
    );

    document
    .querySelector(".effect")
    .classList.add("active");

    draw();

    document.getElementById("status")
    .innerText = "🔄 Edit reset.";
}


function downloadImage(){

    if(!image.src){

        alert("पहिले photo select कर.");

        return;
    }

    const link =
    document.createElement("a");

    link.download =
    "Sanzora-AI-Edited.png";

    link.href =
    canvas.toDataURL("image/png");

    link.click();

    document.getElementById("status")
    .innerText =
    "✅ Photo downloaded.";
}


function aiEdit(){

    const text =
    document.getElementById("prompt").value
    .toLowerCase();

    if(!image.src){

        document.getElementById("status")
        .innerText =
        "📁 पहिले photo select कर.";

        return;
    }

    if(!text){

        document.getElementById("status")
        .innerText =
        "🤖 AI ला काय करायचं ते लिही.";

        return;
    }


    if(text.includes("cinematic")){

        selectedEffect = "cinematic";

    }else if(text.includes("vintage")){

        selectedEffect = "vintage";

    }else if(text.includes("black") ||
             text.includes("white")){

        selectedEffect = "bw";

    }else if(text.includes("warm")){

        selectedEffect = "warm";

    }else if(text.includes("cool")){

        selectedEffect = "cool";

    }else if(text.includes("vivid")){

        selectedEffect = "vivid";

    }else{

        selectedEffect = "cinematic";

    }

    draw();

    document.getElementById("status")
    .innerText =
    "✨ Sanzora AI applied your editing instruction.";
}


function premium(){

    alert(
        "💎 Sanzora AI Premium\n\n" +
        "1000+ Effects & Animations\n" +
        "Advanced AI Editing\n" +
        "Premium Templates\n" +
        "High Quality Export\n\n" +
        "Premium system — coming soon!"
    );
}

</script>

</body>
</html>
