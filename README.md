# valentine
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Uvi ❤️</title>
<style>
body{
  margin:0;
  font-family:cursive;
  text-align:center;
  overflow:hidden;
  background:linear-gradient(135deg,#ff9acb,#ffc0cb,#ffd6ec);
}
h1{
  margin-top:50px;
  color:white;
  font-size:40px;
  text-shadow:0 0 10px #ff2e7a;
}
button{
  padding:15px 35px;
  font-size:20px;
  border:none;
  border-radius:40px;
  margin:15px;
  cursor:pointer;
  transition:.3s;
}
button:hover{transform:scale(1.1);}
#yes{background:#ff2e7a;color:white;}
#no{background:white;}
#more{background:#ff69b4;color:white; display:none;}
img{
  display:block;
  margin:30px auto;
}
#gif{width:300px;}
#startImage{width:300px; margin-top:20px;} 
#letterText{
  display:none;
  padding:20px;
  width:90%;
  margin:30px auto;
  border-radius:20px;
  font-size:22px;
  line-height:1.6;
  color:#ff2e7a;
}
#finalContainer{
  display:none;
  width:90%;
  margin:auto;
  display:flex;
  justify-content:center;
  gap:20px;
  align-items:center;
}
#finalContainer img{
  width:45%;
  display:block;
  margin:0;
}
.heart{
  position:absolute;
  color:#ff2e7a;
  animation:float 7s linear infinite;
}
@keyframes float{
  from{transform:translateY(100vh);}
  to{transform:translateY(-10vh);}
}
</style>
</head>
<body>

<h1 id="question">Will You Be My Valentine Uvi? 💖</h1>

<!-- Starting image -->
<img id="startImage" src="https://i.postimg.cc/G2C958fj/ce41533e-b624-44e5-93e8-51d993049589.jpg" alt="Valentine Image">

<!-- GIF container with overlay text at bottom -->
<div id="gifContainer" style="position:relative; width:300px; margin:30px auto;">
  <img id="gif" src="" style="width:100%; display:block;">
  <div id="gifText" style="
      position:absolute;
      bottom:10px; 
      left:50%;
      transform:translateX(-50%); 
      color:white;
      font-size:20px;
      font-weight:bold;
      text-shadow: 2px 2px 8px #000;
      width:90%;
      text-align:center;
  "></div>
</div>

<br>
<button id="no">No 💔</button>
<button id="yes">Yes 💞</button>
<button id="more">More for you 💖</button>

<!-- Letter text -->
<div id="letterText">
Happy valentine day 💖<br>
Thank you for choosing me Uvi. I am so blessed to have you in my life. I wish from here we spend every valentine and every day together with so much love. You really mean so much to me. I really love you so much &lt;3
</div>

<!-- Final GIFs side by side -->
<div id="finalContainer">
  <img id="kissingGif" src="https://i.postimg.cc/gLvPmk0j/updated-happy.gif" alt="Kissing Cat GIF" style="display:none;">
  <img id="happyGif" src="https://i.postimg.cc/4Khfqws1/love-letter.png" alt="Happy GIF" style="display:none;">
</div>

<script>
let gif = document.getElementById("gif");
let gifText = document.getElementById("gifText");
let noBtn = document.getElementById("no");
let yesBtn = document.getElementById("yes");
let moreBtn = document.getElementById("more");
let letterText = document.getElementById("letterText");
let finalContainer = document.getElementById("finalContainer");
let question = document.getElementById("question");
let happyGif = document.getElementById("happyGif");
let kissingGif = document.getElementById("kissingGif");
let startImage = document.getElementById("startImage");

// Counter for No clicks
let count = 0;

// GIFs for No clicks
const gifs = [
  "https://i.postimg.cc/2qBhzPng/cry-cat.gif",
  "https://i.postimg.cc/FfJr8GNT/banana-cat.gif",
  "https://i.postimg.cc/3yD8V9Yn/sad-cat.gif"
];

// Texts overlay for each No GIF
const noTexts = [
  "Think again babe 🥺!!",
  "Don't do this babe 🥺🥺",
  "Don't you love me 😭😭"
];

// She said Yes GIF
const yesGif = "https://i.postimg.cc/QKNFWPWm/final-yes.gif";

// 🎵 Background music — Google Drive direct link
const music = new Audio("https://drive.google.com/uc?export=download&id=1SdG8u_WDtuS6LDYv9p3wswNlPniWvwm_");
music.loop = true;

// Play immediately, or on first click if blocked
window.addEventListener("load", () => {
    music.play().catch(() => {
        const startHandler = () => { music.play(); window.removeEventListener("click", startHandler); };
        window.addEventListener("click", startHandler);
    });
});

// Move No button randomly
function moveNoButton(){
  noBtn.style.position = "absolute";
  noBtn.style.top = Math.random()*80 + "%";
  noBtn.style.left = Math.random()*80 + "%";
}

noBtn.addEventListener("click",()=>{
  startImage.style.display = "none"; 
  if(count < 3){
    gif.src = gifs[count];
    gif.style.display = "block";
    gifText.innerHTML = noTexts[count]; 
    count++;
    if(count==3){ moveNoButton(); }
  } else { moveNoButton(); }
});

yesBtn.addEventListener("click",()=>{
  gif.src = yesGif;
  gif.style.display = "block";
  gifText.innerHTML = "";
  yesBtn.style.display = "none";
  noBtn.style.display = "none";
  moreBtn.style.display = "inline-block";
  question.style.display = "none";
  startImage.style.display = "none";
  launchHearts();
});

moreBtn.addEventListener("click",()=>{
  gif.style.display = "none";
  moreBtn.style.display = "none";
  letterText.style.display = "block";
  finalContainer.style.display = "flex";
  kissingGif.style.display = "block";
  happyGif.style.display = "block";
});

// Floating hearts
setInterval(()=>{
  let h = document.createElement("div");
  h.className = "heart";
  h.innerHTML = "💗";
  h.style.left = Math.random()*100+"vw";
  h.style.fontSize = (Math.random()*20+15)+"px";
  document.body.appendChild(h);
  setTimeout(()=>h.remove(),7000);
},300);

// Hearts explosion
function launchHearts(){
  for(let i=0;i<60;i++){
    let h=document.createElement("div");
    h.innerHTML="💖";
    h.style.position="absolute";
    h.style.left="50%";
    h.style.top="50%";
    h.style.fontSize=Math.random()*30+20+"px";
    h.style.transform=`translate(${(Math.random()-0.5)*800}px,${(Math.random()-0.5)*600}px)`;
    h.style.transition="1s";
    document.body.appendChild(h);
    setTimeout(()=>h.remove(),1000);
  }
}
</script>

</body>
</html>
