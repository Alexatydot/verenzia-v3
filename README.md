<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>University of Verenizia</title>
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@600;700&family=Inter:wght@300;400;600&display=swap" rel="stylesheet">
<style>

:root{
--navy:#0b1628;
--gold:#c6a94c;
--light:#f4f4f4;
}

body{
margin:0;
font-family:'Inter',sans-serif;
background:var(--light);
color:#111;
}

header{
background:var(--navy);
color:white;
padding:20px 8%;
display:flex;
justify-content:space-between;
align-items:center;
}

header h1{
font-family:'Playfair Display',serif;
}

nav a{
color:white;
margin-left:20px;
text-decoration:none;
}

nav a:hover{color:var(--gold);}

.hero{
background:linear-gradient(rgba(11,22,40,.9),rgba(11,22,40,.9)),
url('https://images.unsplash.com/photo-1498243691581-b145c3f54a5a');
background-size:cover;
color:white;
padding:120px 8%;
text-align:center;
}

.section{
padding:60px 8%;
}

.card{
background:white;
padding:20px;
border-radius:10px;
margin:15px 0;
box-shadow:0 5px 20px rgba(0,0,0,.05);
}

button{
background:var(--gold);
border:none;
padding:10px 20px;
cursor:pointer;
border-radius:5px;
margin-top:10px;
font-weight:bold;
}

input,textarea,select{
width:100%;
padding:10px;
margin:10px 0;
}

.houseTag{
padding:5px 10px;
border-radius:5px;
color:white;
display:inline-block;
margin-top:10px;
}

.Aurelius{background:#8b0000;}
.Valentis{background:#003366;}
.Caelestis{background:#006400;}
.Ignivar{background:#4b0082;}

footer{
background:var(--navy);
color:white;
text-align:center;
padding:20px;
}

.hidden{display:none;}

</style>
</head>
<body>

<header>
<h1>University of Verenizia</h1>
<nav>
<a href="#apply">Apply</a>
<a href="#scholarship">Scholarship</a>
<a href="#newspaper">Newspaper</a>
<a href="#alumni">Alumni</a>
<a href="#society">Society</a>
</nav>
</header>

<div class="hero">
<h2>Lux et Veritas</h2>
<p>Acceptance Rate: 12% | Established 1894 | Ranked #1 in Northern Southern Italy</p>
</div>

<!-- APPLICATION -->
<div class="section" id="apply">
<h2>Undergraduate Application</h2>
<input id="name" placeholder="Full Name">
<input id="gpa" type="number" placeholder="GPA (0-4.0)">
<textarea id="essay" placeholder="Statement of Purpose"></textarea>
<button onclick="apply()">Submit Application</button>
<div id="result"></div>
</div>

<!-- SCHOLARSHIP INTERVIEW -->
<div class="section" id="scholarship">
<h2>Merit Scholarship Interview</h2>
<p>"Why should Verenizia invest in you?"</p>
<textarea id="scholarAnswer"></textarea>
<button onclick="evaluateScholarship()">Submit Interview</button>
<div id="scholarResult"></div>
</div>

<!-- LEADERBOARD -->
<div class="section">
<h2>House Rankings</h2>
<div id="leaderboard"></div>
</div>

<!-- NEWSPAPER -->
<div class="section" id="newspaper">
<h2>The Verenizia Chronicle</h2>

<div class="card">
<h3>Midnight Gala Ends in Mysterious Power Outage</h3>
<p>Witnesses report chanting heard beneath the Grand Hall.</p>
</div>

<div class="card">
<h3>Professor Morveau Denies Building Sentient AI</h3>
<p>"The machines merely calculate," she insists.</p>
</div>

<div class="card">
<h3>House Ignivar Accused of Academic Sabotage</h3>
<p>Leaderboard points under investigation.</p>
</div>

</div>

<!-- ALUMNI -->
<div class="section" id="alumni">
<h2>Distinguished Alumni</h2>

<div class="card">
<h3>Lorenzo Vale</h3>
<p>Tech Billionaire. Founder of an unnamed AI empire.</p>
</div>

<div class="card">
<h3>Amara Solenne</h3>
<p>Youngest Prime Minister in modern European history.</p>
</div>

<div class="card">
<h3>Dr. Elias Kael</h3>
<p>Nobel Laureate. Claims his research began in the Verenizia catacombs.</p>
</div>

</div>

<!-- SECRET SOCIETY -->
<div class="section" id="society">
<h2>The Obsidian Circle</h2>
<p>An invitation-only society founded in 1897.</p>
<button onclick="revealSociety()">Request Access</button>
<div id="societyResult"></div>
</div>

<footer>
© 2026 University of Verenizia | Lux et Veritas
</footer>

<script>

let houses=["Aurelius","Valentis","Caelestis","Ignivar"];
let scores={
Aurelius:0,
Valentis:0,
Caelestis:0,
Ignivar:0
};

function randomHouse(){
return houses[Math.floor(Math.random()*houses.length)];
}

function generateLetter(name,house){
let letters=[
`Dear ${name},<br><br>
It is with formal distinction that we welcome you to House ${house}. Verenizia recognizes rare intellect.`,
`${name},<br><br>
The Council has spoken. You are admitted to House ${house}. Guard this honor carefully.`,
`To ${name},<br><br>
Among thousands, you were selected. House ${house} awaits your ambition.`
];
return letters[Math.floor(Math.random()*letters.length)];
}

function apply(){
let name=document.getElementById("name").value;
let gpa=parseFloat(document.getElementById("gpa").value);
let essay=document.getElementById("essay").value;

if(!name||!gpa||!essay){alert("Complete all fields.");return;}

let accepted=Math.random()<0.12 && gpa>=3.2;
let output=document.getElementById("result");

if(accepted){
let house=randomHouse();
scores[house]+=Math.floor(gpa*10);
updateBoard();
output.innerHTML=generateLetter(name,house)+
`<div class="houseTag ${house}">${house}</div>`;
}else{
output.innerHTML=`Dear ${name},<br><br>
Admission denied. The standards of Verenizia remain uncompromising.`;
}
}

function updateBoard(){
let html="";
for(let h in scores){
html+=`<div class="card">
<h3>${h}</h3>
Points: ${scores[h]}
</div>`;
}
document.getElementById("leaderboard").innerHTML=html;
}

function evaluateScholarship(){
let answer=document.getElementById("scholarAnswer").value;
let result=document.getElementById("scholarResult");

if(answer.length>120){
result.innerHTML="Scholarship Granted. Full Tuition Covered.";
}else{
result.innerHTML="Scholarship Denied. Excellence requires depth.";
}
}

function revealSociety(){
let chance=Math.random();
let result=document.getElementById("societyResult");

if(chance>.85){
result.innerHTML="Invitation Accepted. The Obsidian Circle will contact you at midnight.";
}else{
result.innerHTML="Request Denied. The Circle does not reveal itself lightly.";
}
}

updateBoard();

</script>
</body>
</html>
