<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Dreamcore 15°</title>

<style>
body{
  margin:0;
  padding:30px;
  font-family:Arial;
  background:#14192B;
  color:#EAEAFF;
  overflow-x:hidden;
}

/* sparkle background */
body::before{
  content:"";
  position:fixed;
  inset:0;
  background-image:
    radial-gradient(2px 2px at 20% 30%, white, transparent),
    radial-gradient(1px 1px at 70% 60%, white, transparent),
    radial-gradient(1px 1px at 40% 80%, white, transparent),
    radial-gradient(1px 1px at 80% 20%, white, transparent);
  animation:sparkle 6s linear infinite;
  pointer-events:none;
}

@keyframes sparkle{
  0%{transform:translateY(0);}
  100%{transform:translateY(-30px);}
}

h1{font-size:28px;}
h2{margin-top:30px;}

.clickable{
  cursor:pointer;
  text-decoration:underline;
}

.section{
  display:none;
  border:1px solid rgba(255,255,255,0.3);
  padding:10px;
  margin-top:10px;
}

.item{
  border:1px solid rgba(255,255,255,0.2);
  margin:8px 0;
  padding:8px;
  cursor:pointer;
}

.item-content{
  display:none;
  margin-top:5px;
  opacity:0.9;
  line-height:1.4;
}

/* stars */
.stars span{
  font-size:28px;
  cursor:pointer;
  color:silver;
  transition:0.3s;
}

.stars span.active{
  color:gold;
  transform:scale(1.2);
}

/* input */
textarea{
  width:100%;
  max-width:500px;
  height:90px;
  padding:10px;
  background:transparent;
  color:white;
  border:1px solid rgba(255,255,255,0.5);
}

button{
  margin-top:10px;
  padding:8px 14px;
  background:transparent;
  color:white;
  border:1px solid rgba(255,255,255,0.5);
  cursor:pointer;
}

</style>
</head>

<body>

<h1>Dream your core in Dreamcore 15°</h1>

<hr>

<!-- ================= SECTOR 1 ================= -->
<h2>Sector 1</h2>

<p>Type your dream definition</p>

<textarea id="input"></textarea><br>
<button onclick="findDream()">Find my Dream Level out of 15</button>

<p id="result"></p>

<hr>

<!-- ================= SECTOR 2 ================= -->
<h2>Sector 2</h2>

<div class="clickable" onclick="toggle('levels')">
Know more about your dream levels
</div>

<div id="levels" class="section"></div>

<br>

<div class="clickable" onclick="toggle('stars')">
Know more about stars
</div>

<div id="stars" class="section">

  <div class="clickable" onclick="toggle('const')">
    All 88 Constellations
  </div>

  <div id="const" class="section"></div>

</div>

<!-- ================= STAR RATING ================= -->
<h2>Rate your experience</h2>

<div class="stars">
  <span data-v="1">★</span>
  <span data-v="2">★</span>
  <span data-v="3">★</span>
  <span data-v="4">★</span>
  <span data-v="5">★</span>
</div>

<h6>Credits: ChatGPT + Sriparna</h6>

<script>

/* ================= 15 DREAM LEVELS ================= */
const dreamLevels = [
{
n:"Level 81 — Bubble world",
d:"Bubbles, soft pink lilac liminal space",
t:"You don't wanna wake up"
},
{
n:"Level 54 — Circles in the wild",
d:"Creepy circles everywhere",
t:"You have to wake up"
},
{
n:"Level 34 — Layers in glitters",
d:"Sparkling glitter layers",
t:"You don't wanna wake up"
},
{
n:"Level 990 — Liminal places",
d:"Infinite empty buildings",
t:"You have to wake up"
},
{
n:"Level 18 — Flowers lifting",
d:"Floating flowers everywhere",
t:"You don't wanna wake up"
},
{
n:"Level 344 — Unending chaos",
d:"Black red blue chaos void",
t:"You have to wake up"
},
{
n:"Level 111 — Lucky guessed",
d:"Perfect ideal reality",
t:"You don't wanna wake up"
},
{
n:"Level 999 — All in the shades",
d:"Colour chaos reality",
t:"You have to wake up"
},
{
n:"Level 45 — Core",
d:"Personal interest reality",
t:"You have to wake up"
},
{
n:"Level 8888 — Unlimited",
d:"Infinite unknown void",
t:"You have to wake up"
},
{
n:"Level 3590 — Instance",
d:"Broken glitch reality",
t:"You can't wake up"
},
{
n:"Level 000 — Backrooms",
d:"Yellow endless hallways",
t:"You have to wake up"
},
{
n:"Level 4440 — Gates",
d:"Endless glowing gates",
t:"You have to wake up"
},
{
n:"Level 0000000 — Playground",
d:"Creepy nostalgic playground",
t:"You have to wake up"
},
{
n:"Level 15 — Dream Match",
d:"System matched dream level",
t:"AI generated"
}
];

/* ================= 88 CONSTELLATIONS ================= */
const constellations = [
"Andromeda","Aquarius","Aries","Auriga","Boötes","Cancer","Cassiopeia","Cygnus",
"Draco","Gemini","Leo","Orion","Pegasus","Perseus","Pisces","Scorpius",
"Taurus","Virgo","Ursa Major","Ursa Minor","Hydra","Lyra","Hercules",
"Aquila","Cetus","Lepus","Lupus","Phoenix","Fornax","Columba","Crux",
"Carina","Centaurus","Delphinus","Dorado","Eridanus","Grus","Horologium",
"Indus","Lacerta","Monoceros","Musca","Norma","Octans","Pavo","Pyxis",
"Reticulum","Sculptor","Telescopium","Triangulum","Vela","Volans","Vulpecula",
"Apus","Chamaeleon","Circinus","Camelopardalis","Coma Berenices","Corona Borealis",
"Corvus","Crater","Equuleus","Sagitta","Serpens","Scutum","Antlia","Caelum",
"Hydrus","Mensa","Microscopium","Sextans","Tucana","Ursa Major","Ursa Minor",
"Leo Minor","Vulpecula","Serpens Cauda","Serpens Caput","Triangulum Australe"
];

/* ================= TOGGLE ================= */
function toggle(id){
  let el=document.getElementById(id);
  el.style.display = el.style.display==="block"?"none":"block";
}

/* ================= BUILD DREAM LEVELS ================= */
let levelsBox=document.getElementById("levels");

dreamLevels.forEach(l=>{
  let div=document.createElement("div");
  div.className="item";
  div.innerHTML="<b>"+l.n+"</b><div class='item-content'>"+l.d+"<br>"+l.t+"</div>";

  div.onclick=()=>{
    let c=div.querySelector(".item-content");
    c.style.display=c.style.display==="block"?"none":"block";
  };

  levelsBox.appendChild(div);
});

/* ================= BUILD CONSTELLATIONS ================= */
let constBox=document.getElementById("const");

constellations.forEach(c=>{
  let div=document.createElement("div");
  div.className="item";
  div.innerHTML="<b>"+c+"</b><div class='item-content'>Constellation in the night sky, part of 88 official star patterns.</div>";

  div.onclick=()=>{
    let c2=div.querySelector(".item-content");
    c2.style.display=c2.style.display==="block"?"none":"block";
  };

  constBox.appendChild(div);
});

/* ================= DREAM MATCH (ALL 15) ================= */
function findDream(){
  let input=document.getElementById("input").value.toLowerCase();

  let best=null;
  let score=-1;

  dreamLevels.forEach(l=>{
    let text=(l.n+" "+l.d+" "+l.t).toLowerCase();
    let s=0;

    input.split(" ").forEach(w=>{
      if(text.includes(w) && w.length>2) s++;
    });

    if(input.includes("bubble")) s+=3;
    if(input.includes("circle")) s+=3;
    if(input.includes("glitter")) s+=3;
    if(input.includes("flower")) s+=3;
    if(input.includes("chaos")) s+=3;
    if(input.includes("liminal")) s+=3;
    if(input.includes("backrooms")) s+=3;
    if(input.includes("perfect")) s+=3;

    if(s>score){
      score=s;
      best=l;
    }
  });

  document.getElementById("result").innerHTML =
    "✨ Closest Dream Level: <b>"+best.n+"</b>";
}

/* ================= STARS ================= */
document.querySelectorAll(".stars span").forEach(s=>{
  s.onclick=()=>{
    let v=s.dataset.v;
    document.querySelectorAll(".stars span").forEach(x=>{
      x.classList.toggle("active",x.dataset.v<=v);
    });
  };
});

</script>

</body>
</html>