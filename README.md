<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Will You Be My Valentine 💖</title>

<style>
*{
    margin:0;
    padding:0;
    box-sizing:border-box;
    font-family: 'Georgia', serif;
}

body{
    background: linear-gradient(135deg,#ffd1dc,#ffe6f0);
    min-height:100vh;
    display:flex;
    justify-content:center;
    align-items:center;
    overflow:hidden;
}

.screen{
    display:none;
    text-align:center;
    padding:30px;
    width:100%;
    max-width:500px;
    animation: fade 1s ease;
}

.screen.active{
    display:block;
}

h1,h2{
    margin-bottom:20px;
    color:#b8003d;
}

p{
    color:#4d0033;
    font-size:17px;
    line-height:1.6;
}

button{
    padding:12px 25px;
    font-size:16px;
    border:none;
    border-radius:25px;
    background:#ff4d6d;
    color:white;
    cursor:pointer;
    margin:15px;
}

button:hover{
    transform:scale(1.05);
}

@keyframes fade{
    from{opacity:0;}
    to{opacity:1;}
}

/* Countdown */
#count{
    font-size:60px;
    color:#ff4d6d;
}

/* Floating hearts */
.heart{
    position:fixed;
    bottom:-20px;
    font-size:24px;
    animation: float 6s linear infinite;
}

@keyframes float{
    from{transform:translateY(0);opacity:1;}
    to{transform:translateY(-100vh);opacity:0;}
}
</style>
</head>

<body>

<!-- BACKGROUND MUSIC -->
<audio id="bg-music" loop>
  <source src="darkhaast.mp3" type="audio/mpeg">
</audio>

<script>
/* Mobile autoplay fix */
document.addEventListener("click", () => {
    const music = document.getElementById("bg-music");
    if (music.paused) {
        music.volume = 0.7;
        music.play();
    }
});
</script>

<!-- SCREEN 1 -->
<div class="screen active">
    <h1>Hey You 🌸</h1>
    <p>
        Someone made this little space,<br>
        just to see you smile today 💕
    </p>
    <button onclick="nextScreen()">Next 💖</button>
</div>

<!-- SCREEN 2 -->
<div class="screen">
    <h2>Just wait a moment 😍</h2>
    <div id="count">3</div>
</div>

<!-- SCREEN 3 -->
<div class="screen">
    <h2>Just a few lines ✨</h2>
    <p>
        “Tumhari ek muskaan se hi din ban jaata hai,<br>
        Tum paas ho toh har pal khaas lag jaata hai.”
    </p>
    <button onclick="nextScreen()">One Last Thing 🌹</button>
</div>

<!-- SCREEN 4 -->
<div class="screen">
    <h1>Will You Be My Valentine? 💘</h1>
    <button onclick="yes()">Yes ❤️</button>
    <button id="no">No 😳</button>
</div>

<!-- SCREEN 5 -->
<div class="screen">
    <h1>Yay! You Said Yes! 🎉</h1>
    <p>This is the beginning of something beautiful ✨</p>
    <p><b>“You are my today and all of my tomorrows.”</b></p>
    <button onclick="share()">Share This Moment 💌</button>
</div>

<script>
let screens = document.querySelectorAll('.screen');
let current = 0;

function nextScreen(){
    const music = document.getElementById("bg-music");
    if (music.paused) {
        music.volume = 0.7;
        music.play();
    }

    screens[current].classList.remove('active');
    current++;
    screens[current].classList.add('active');

    if(current === 1){
        startCountdown();
    }
}


function startCountdown(){
    let c = 3;
    let el = document.getElementById('count');
    let timer = setInterval(()=>{
        c--;
        el.innerText = c;
        if(c === 0){
            clearInterval(timer);
            nextScreen();
        }
    },1000);
}

/* NO button escape */
const noBtn = document.getElementById('no');
noBtn.addEventListener('mouseover',()=>{
    noBtn.style.position='absolute';
    noBtn.style.left=Math.random()*80+'%';
    noBtn.style.top=Math.random()*80+'%';
});

/* YES */
function yes(){
    nextScreen();
    fireworks();
}

/* Hearts celebration */
function fireworks(){
    for(let i=0;i<35;i++){
        let h=document.createElement('div');
        h.className='heart';
        h.innerHTML='❤️';
        h.style.left=Math.random()*100+'%';
        h.style.fontSize=(20+Math.random()*20)+'px';
        document.body.appendChild(h);
        setTimeout(()=>h.remove(),6000);
    }
}

/* Share */
function share(){
    const text = "I said YES 💖 Will you be my Valentine?";
    const url = window.location.href;
    window.open(`https://wa.me/?text=${encodeURIComponent(text+" "+url)}`);
}
</script>

</body>
</html>
