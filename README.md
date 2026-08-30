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
    font-family:Arial, sans-serif;
}

body{
    background:#08090d;
    color:white;
    min-height:100vh;
}

header{
    padding:18px 22px;
    display:flex;
    justify-content:space-between;
    align-items:center;
    border-bottom:1px solid #252733;
    background:#0d0f15;
    position:sticky;
    top:0;
    z-index:10;
}

.logo{
    font-size:25px;
    font-weight:800;
    letter-spacing:.5px;
}

.logo span{
    color:#9b7cff;
}

.premium{
    border:0;
    padding:10px 16px;
    border-radius:25px;
    background:linear-gradient(135deg,#8d5cff,#d66cff);
    color:white;
    font-weight:bold;
}

.hero{
    padding:35px 20px 20px;
    text-align:center;
}

.hero h1{
    font-size:34px;
    margin-bottom:10px;
}

.hero h1 span{
    color:#a47cff;
}

.hero p{
    color:#a8abb8;
    line-height:1.5;
}

.editor{
    max-width:900px;
    margin:auto;
    padding:20px;
}

.upload-box{
    border:2px dashed #3b3d4b;
    border-radius:22px;
    padding:35px 20px;
    text-align:center;
    background:#10121a;
    transition:.3s;
}

.upload-box:hover{
    border-color:#9b7cff;
}

.upload-icon{
    font-size:45px;
    margin-bottom:12px;
}

.upload-box h2{
    margin-bottom:8px;
}

.upload-box p{
    color:#888c99;
    margin-bottom:20px;
}

.upload-btn{
    display:inline-block;
    padding:13px 22px;
    border-radius:25px;
    background:#9b7cff;
    color:white;
    font-weight:bold;
    cursor:pointer;
}

#mediaInput{
    display:none;
}

.preview{
    margin-top:20px;
    background:#10121a;
    border-radius:22px;
    padding:15px;
    display:none;
}

#mediaPreview{
    width:100%;
    max-height:480px;
    object-fit:contain;
    border-radius:15px;
    background:#050505;
}

.prompt-box{
    margin-top:20px;
    background:#10121a;
    padding:18px;
    border-radius:20px;
}

.prompt-box label{
    display:block;
    margin-bottom:10px;
    font-weight:bold;
}

.prompt-area{
    display:flex;
    gap:10px;
}

#prompt{
    flex:1;
    background:#08090d;
    color:white;
    border:1px solid #303341;
    outline:none;
    padding:14px;
    border-radius:14px;
}

.ai-btn{
    border:0;
    background:linear-gradient(135deg,#765cff,#c75cff);
    color:white;
    padding:0 18px;
    border-radius:14px;
    font-weight:bold;
}

.section{
    margin-top:25px;
}

.section-title{
    display:flex;
    justify-content:space-between;
    margin-bottom:14px;
}

.section-title h2{
    font-size:20px;
}

.badge{
    color:#c8b9ff;
    font-size:13px;
}

.effects{
    display:grid;
    grid-template-columns:repeat(4,1fr);
    gap:10px;
}

.effect{
    padding:15px 8px;
    background:#12141c;
    border:1px solid #252834;
    border-radius:15px;
    color:#ddd;
    cursor:pointer;
    text-align:center;
    transition:.2s;
}

.effect:hover{
    transform:translateY(-2px);
    border-color:#9b7cff;
}

.effect.active{
    background:#28203d;
    border-color:#a47cff;
}

.tools{
    display:grid;
    grid-template-columns:repeat(3,1fr);
    gap:10px;
}

.tool{
    background:#12141c;
    border:1px solid #252834;
    padding:16px;
    border-radius:15px;
    text-align:center;
}

.tool div{
    font-size:25px;
    margin-bottom:7px;
}

.export{
    margin-top:25px;
    width:100%;
    padding:17px;
    border:0;
    border-radius:17px;
    background:linear-gradient(135deg,#9b7cff,#e05cff);
    color:white;
    font-size:17px;
    font-weight:bold;
}

.status{
    text-align:center;
    color:#9296a5;
    margin-top:12px;
    min-height:20px;
}

footer{
    text-align:center;
    color:#686b78;
    padding:35px 20px;
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

    .prompt-area{
        flex-direction:column;
    }

    .ai-btn{
        padding:13px;
    }
}
</style>
</head>

<body>

<header>
    <div class="logo">Sanzora <span>AI</span></div>
    <button class="premium" onclick="premiumMessage()">💎 Premium</button>
</header>

<section class="hero">
    <h1>Create. Edit. <span>Imagine.</span></h1>
    <p>AI powered photo & video editing — simple, fast and creative.</p>
</section>

<main class="editor">

    <!-- UPLOAD -->
    <div class="upload-box">

        <div class="upload-icon">🎬</div>

        <h2>Start Creating</h2>

        <p>
            Upload a photo or video and tell Sanzora AI what you want.
        </p>

        <label class="upload-btn" for="mediaInput">
            📁 Select Photo / Video
        </label>

        <input
            id="mediaInput"
            type="file"
            accept="image/*,video/*"
        >

    </div>

    <!-- PREVIEW -->
    <div class="preview" id="previewBox">
        <img id="mediaPreview" alt="Preview">
        <video id="videoPreview" controls style="display:none;width:100%;max-height:480px;border-radius:15px;"></video>
    </div>

    <!-- AI PROMPT -->
    <div class="prompt-box">

        <label>🤖 Tell Sanzora AI what to do</label>

        <div class="prompt-area">

            <input
                id="prompt"
                type="text"
                placeholder="Example: Make this photo cinematic..."
            >

            <button class="ai-btn" onclick="runAI()">
                ✨ AI Edit
            </button>

        </div>

        <div class="status" id="status"></div>

    </div>

    <!-- EFFECTS -->
    <section class="section">

        <div class="section-title">
            <h2>✨ Effects</h2>
            <span class="badge">Free Preview</span>
        </div>

        <div class="effects">

            <div class="effect" onclick="selectEffect(this,'Cinematic')">🎬<br>Cinematic</div>

            <div class="effect" onclick="selectEffect(this,'Glow')">✨<br>Glow</div>

            <div class="effect" onclick="selectEffect(this,'Vintage')">📸<br>Vintage</div>

            <div class="effect" onclick="selectEffect(this,'Dream')">🌙<br>Dream</div>

            <div class="effect" onclick="selectEffect(this,'Vivid')">🌈<br>Vivid</div>

            <div class="effect" onclick="selectEffect(this,'Retro')">📼<br>Retro</div>

            <div class="effect" onclick="selectEffect(this,'Blur')">💫<br>Soft Blur</div>

            <div class="effect" onclick="selectEffect(this,'B&W')">⚫<br>B&W</div>

            <div class="effect" onclick="selectEffect(this,'Warm')">🔥<br>Warm</div>

            <div class="effect" onclick="selectEffect(this,'Cool')">❄️<br>Cool</div>

            <div class="effect" onclick="selectEffect(this,'Neon')">💜<br>Neon</div>

            <div class="effect" onclick="selectEffect(this,'Film')">🎞️<br>Film</div>

        </div>

    </section>

    <!-- TOOLS -->
    <section class="section">

        <div class="section-title">
            <h2>🛠️ Editing Tools</h2>
        </div>

        <div class="tools">

            <div class="tool">
                <div>✂️</div>
                Trim
            </div>

            <div class="tool">
                <div>🎵</div>
                Music
            </div>

            <div class="tool">
                <div>📝</div>
                Text
            </div>

            <div class="tool">
                <div>🎨</div>
                Filters
            </div>

            <div class="tool">
                <div>🪄</div>
                Background
            </div>

            <div class="tool">
                <div>⚡</div>
                Animation
            </div>

        </div>

    </section>

    <button class="export" onclick="exportMessage()">
        🚀 Export Creation
    </button>

</main>

<footer>
    © 2026 Sanzora AI — AI Photo & Video Creator
</footer>


<script>

const input = document.getElementById("mediaInput");
const previewBox = document.getElementById("previewBox");
const imagePreview = document.getElementById("mediaPreview");
const videoPreview = document.getElementById("videoPreview");
const statusText = document.getElementById("status");

input.addEventListener("change", function(){

    const file = this.files[0];

    if(!file) return;

    const url = URL.createObjectURL(file);

    previewBox.style.display = "block";

    if(file.type.startsWith("image/")){

        imagePreview.style.display = "block";
        videoPreview.style.display = "none";

        imagePreview.src = url;

    }else if(file.type.startsWith("video/")){

        imagePreview.style.display = "none";
        videoPreview.style.display = "block";

        videoPreview.src = url;
    }

    statusText.innerText = "Media loaded successfully ✅";
});


function runAI(){

    const prompt = document.getElementById("prompt").value.trim();

    if(!input.files[0]){

        statusText.innerText = "पहिले photo किंवा video select कर. 📁";
        return;
    }

    if(!prompt){

        statusText.innerText = "AI ला काय edit करायचं ते लिही. 🤖";
        return;
    }

    statusText.innerText =
        "✨ Sanzora AI तुमचा edit plan तयार करत आहे...";

    setTimeout(function(){

        statusText.innerText =
            "✅ AI edit instruction तयार! पुढच्या version मध्ये actual AI rendering जोडू.";

    },1500);
}


function selectEffect(element,name){

    document.querySelectorAll(".effect")
    .forEach(e => e.classList.remove("active"));

    element.classList.add("active");

    statusText.innerText =
        "✨ " + name + " effect selected.";
}


function premiumMessage(){

    alert(
        "💎 Sanzora AI Premium\n\n" +
        "Coming Soon!\n\n" +
        "Premium मध्ये 1000+ effects, animations, AI tools आणि advanced editing मिळेल."
    );
}


function exportMessage(){

    if(!input.files[0]){

        alert("पहिले photo किंवा video select कर.");
        return;
    }

    alert(
        "🚀 Export system पुढच्या phase मध्ये जोडणार आहोत.\n\n" +
        "आपण नंतर high-quality photo/video rendering जोडू."
    );
}

</script>

</body>
</html>
