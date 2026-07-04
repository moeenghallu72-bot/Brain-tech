# Brain-tech
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Brain Tech Daily Quiz 2026 - Free Certificate</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<meta name="version" content="BrainTest v1.7 - 500 Qs">
<script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
<style>
body{font-family:Arial; text-align:center; background:#0f172a; color:#fff; padding:20px; margin:0}
.box{background:#1e293b; padding:20px; border-radius:12px; max-width:700px; margin:auto}
button{background:#38bdf8; border:none; padding:12px 20px; border-radius:8px; cursor:pointer; color:#000; font-weight:bold; margin-top:10px}
button:disabled{background:#475569; cursor:not-allowed; color:#94a3b8}
input{padding:10px; width:90%; margin:10px; border-radius:6px; border:none; font-size:16px}
.hide{display:none}
#timer{font-size:22px; color:#facc15; font-weight:bold; margin-bottom:15px}
.question{text-align:left; margin:15px 0; background:#334155; padding:12px; border-radius:8px}
label{display:block; margin:5px 0; cursor:pointer}
h1{color:#38bdf8}
.error{color:#f87171; font-size:14px}
.success{color:#4ade80; font-size:14px}
#dayInfo{color:#94a3b8; font-size:14px}
.note{color:#facc15; font-size:13px}
#quizInfo{color:#38bdf8; font-weight:bold}
</style>
</head>
<body>

<div class="box" id="passwordBox">
  <h1>🔒 Brain Tech Login</h1>
  <p id="dayInfo"></p>
  <p class="note" style="color:#4ade80">Note: Jhang = Password | Admin = Password | Baqi = Free Entry</p>
  <p class="note" style="color:#4ade80">Sab ke liye: 100 MCQs | 30 Minutes | Bilkul Free</p>
  <input id="password" placeholder="Password Daalein Ya Khali Chhor Dein" type="password">
  <button onclick="checkPassword()">Enter Quiz</button>
  <p id="passError" class="error"></p>
  <button onclick="skipPassword()" style="background:#4ade80">Free Entry</button>
</div>

<div class="box hide" id="formBox">
  <h1>🧠 Brain Tech Quiz</h1>
  <p id="quizInfo">100 MCQs | 30 Minutes | 1 Attempt Per Day</p>
  <p style="color:#facc15">Passing: 50 Marks | Good: 50-74 | Excellent: 75-89 | Super: 90+</p>
  <input id="name" placeholder="Apna Pura Naam English Me Likho">
  <button id="startBtn" onclick="startQuiz()">Start Quiz</button>
  <p id="attemptStatus" class="success"></p>
</div>

<div class="box hide" id="quizBox">
  <h2>🧠 Brain Tech</h2>
  <div id="timer">Time: 30:00</div>
  <form id="quizForm"></form>
  <button onclick="submitQuiz()">Submit Quiz</button>
</div>

<div style="color:#475569; font-size:12px; margin-top:20px">
  BrainTest.com v1.7 | Updated: 2026-07-04 | Total Questions: 500 | All = 100 Qs | Free
</div>

<script>
const { jsPDF } = window.jspdf;
let name = "";
let timeLeft = 1800;
let timer;
let submitted = false;
let quizQuestions = [];
let totalQuestions = 100;
let PASSING_MARKS = 50;

const JHANG_PASSWORD = "JHANG#BT#M@26!";
const ADMIN_PASSWORD = "ADMIN#BT#2026";

function getTodayString(){ return new Date().toISOString().split('T')[0]; }
function getDayNumber() { return new Date().getDay(); }
function getGrade(score, total){
  let percent = (score/total)*100;
  if(percent >= 90) return "SUPER";
  if(percent >= 75) return "Excellent";
  if(percent >= 50) return "Good";
  return "Fail";
}
function checkIfAttemptedToday(){ return localStorage.getItem('brainTechLastAttempt') == getTodayString(); }

function showDayInfo(){
  let day = getDayNumber();
  let days = ["Sunday","Monday","Tuesday","Wednesday","Thursday","Friday","Saturday"];
  document.getElementById('dayInfo').innerText = `Aaj ${days[day]} hai`;
  if(checkIfAttemptedToday()){
    document.getElementById('passError').className = "success";
    document.getElementById('passError').innerText = "Aap aaj ka quiz de chuke hain. Kal wapis aayen.";
    document.getElementById('password').disabled = true;
  }
}
showDayInfo();

function checkPassword(){
  if(checkIfAttemptedToday()){ document.getElementById('passError').innerText = "Aap aaj attempt kar chuke hain!"; return; }
  let enteredPass = document.getElementById('password').value.trim();
  if(enteredPass == JHANG_PASSWORD || enteredPass == ADMIN_PASSWORD){
    totalQuestions = 100;
    openQuiz();
  }
  else if(enteredPass == ""){
    document.getElementById('passError').innerText = "Password khali hai. Free Entry button dabao.";
  }
  else {
    document.getElementById('passError').innerText = "Ghalat Password!";
  }
}

function skipPassword(){
  if(checkIfAttemptedToday()){ alert("Aap aaj attempt kar chuke hain!"); return; }
  totalQuestions = 100;
  openQuiz();
}

function openQuiz(){
  document.getElementById('passwordBox').classList.add('hide');
  document.getElementById('formBox').classList.remove('hide');
  document.getElementById('quizInfo').innerText = `${totalQuestions} MCQs | 30 Minutes | 1 Attempt Per Day`;
  PASSING_MARKS = Math.ceil(totalQuestions * 0.5);
  document.getElementById('attemptStatus').innerText = `Status: Aap aaj 1 bar 100 sawal ka attempt kar sakte hain`;
}

// ========== 500 MCQs CODE KE ANDAR ==========
const questionPool = [
{q:"1. CPU ka full form kya hai?", o:["Central Processing Unit","Computer Power Unit","Control Processing Unit"], a:0},
{q:"2. Pakistan ka capital?", o:["Karachi","Lahore","Islamabad"], a:2},
{q:"3. 2 + 2 =?", o:["3","4","5"], a:1},
{q:"4. Pani ka formula?", o:["H2O","CO2","O2"], a:0},
{q:"5. Quaid-e-Azam ka naam?", o:["Allama Iqbal","Muhammad Ali Jinnah","Liaquat Ali"], a:1},
{q:"6. RAM ka full form?", o:["Random Access Memory","Read Access Memory","Run Access Memory"], a:0},
{q:"7. Sab se bara ocean?", o:["Atlantic","Pacific","Indian"], a:1},
{q:"8. HTML ka full form?", o:["Hyper Text Markup Language","High Text Markup Language","Hyper Transfer Markup Language"], a:0},
{q:"9. Pakistan kis saal bana?", o:["1945","1947","1950"], a:1},
{q:"10. Keyboard ki keys kitni hoti hain?", o:["100","104","110"], a:1},
{q:"11. Monitor ko kya kehte hain?", o:["Output Device","Input Device","Storage Device"], a:0},
{q:"12. Mouse kis category me aata hai?", o:["Input Device","Output Device","CPU"], a:0},
{q:"13. 1 GB me kitne MB?", o:["512","1024","2048"], a:1},
{q:"14. Google kis ne banaya?", o:["Bill Gates","Larry Page","Mark Zuckerberg"], a:1},
{q:"15. Internet ka baap?", o:["Vint Cerf","Steve Jobs","Elon Musk"], a:0},
{q:"16. Pakistan ka national animal?", o:["Lion","Markhor","Deer"], a:1},
{q:"17. Quran me kitne surah hain?", o:["114","120","100"], a:0},
{q:"18. Sab se chota mulk?", o:["Maldives","Vatican City","Monaco"], a:1},
{q:"19. Windows kis company ki hai?", o:["Apple","Microsoft","Google"], a:1},
{q:"20. 1 Minute me kitne seconds?", o:["50","60","70"], a:1},
{q:"21. USB ka full form?", o:["Universal Serial Bus","United Serial Bus","Universal System Bus"], a:0},
{q:"22. Sab se tez janwar?", o:["Lion","Cheetah","Tiger"], a:1},
{q:"23. Pakistan ka national game?", o:["Cricket","Hockey","Football"], a:1},
{q:"24. LCD ka full form?", o:["Liquid Crystal Display","Light Crystal Display","Liquid Color Display"], a:0},
{q:"25. Email ka inventor?", o:["Ray Tomlinson","Bill Gates","Tim Berners-Lee"], a:0},
{q:"26. Darya-e-Sindh kis ocean me girta hai?", o:["Pacific","Arabian Sea","Bay of Bengal"], a:1},
{q:"27. 1 Dozen me kitne?", o:["10","12","14"], a:1},
{q:"28. WiFi ka full form?", o:["Wireless Fidelity","Wired Fidelity","Wide Fidelity"], a:0},
{q:"29. Pakistan ki currency?", o:["Rupee","Dollar","Riyal"], a:0},
{q:"30. Computer ki brain?", o:["RAM","CPU","Hard Disk"], a:1},
{q:"31. Sab se bara bar-e-azam?", o:["Asia","Africa","Europe"], a:0},
{q:"32. PDF ka full form?", o:["Portable Document Format","Print Document Format","Public Document Format"], a:0},
{q:"33. 10 + 15 =?", o:["20","25","30"], a:1},
{q:"34. Facebook kis ne banaya?", o:["Mark Zuckerberg","Bill Gates","Elon Musk"], a:0},
{q:"35. Sab se bara janwar?", o:["Elephant","Blue Whale","Giraffe"], a:1},
{q:"36. Pakistan ka national bird?", o:["Parrot","Chakor","Eagle"], a:1},
{q:"37. HTTP ka full form?", o:["Hyper Text Transfer Protocol","High Text Transfer Protocol","Hyper Transfer Text Protocol"], a:0},
{q:"38. 1 Hour me kitne minutes?", o:["50","60","90"], a:1},
{q:"39. Android kis company ka hai?", o:["Apple","Google","Samsung"], a:1},
{q:"40. Sab se gahra ocean?", o:["Pacific","Atlantic","Indian"], a:0},
{q:"41. URL ka full form?", o:["Uniform Resource Locator","Universal Resource Link","Uniform Resource Link"], a:0},
{q:"42. Pakistan ka national tree?", o:["Deodar","Mango","Banyan"], a:0},
{q:"43. 5 x 5 =?", o:["20","25","30"], a:1},
{q:"44. Bluetooth kis ne banaya?", o:["Harald Bluetooth","Bill Gates","Steve Jobs"], a:0},
{q:"45. Sab se lambi darya?", o:["Nile","Amazon","Sindh"], a:0},
{q:"46. Photoshop kis kaam aata hai?", o:["Video Editing","Photo Editing","Coding"], a:1},
{q:"47. 1 Week me kitne din?", o:["6","7","8"], a:1},
{q:"48. YouTube kis ne banaya?", o:["3 ex-Google employees","Mark Zuckerberg","Bill Gates"], a:0},
{q:"49. Pakistan ka national flower?", o:["Rose","Jasmine","Sunflower"], a:1},
{q:"50. 100 / 5 =?", o:["10","20","25"], a:1},
{q:"51. SQL ka full form?", o:["Structured Query Language","Simple Query Language","System Query Language"], a:0},
{q:"52. Sab se bara shehar Pakistan ka?", o:["Lahore","Karachi","Islamabad"], a:1},
{q:"53. 9 x 9 =?", o:["72","81","90"], a:1},
{q:"54. Twitter ab kya kehlata hai?", o:["X","Face","Chat"], a:0},
{q:"55. Sab se naram metal?", o:["Gold","Silver","Lead"], a:0},
{q:"56. 1 Year me kitne months?", o:["10","12","14"], a:1},
{q:"57. Instagram kis ne banaya?", o:["Kevin Systrom","Mark Zuckerberg","Larry Page"], a:0},
{q:"58. 2 ki power 3?", o:["6","8","9"], a:1},
{q:"59. Pakistan ka national anthem kis ne likha?", o:["Hafeez Jalandhari","Allama Iqbal","Faiz Ahmed"], a:0},
{q:"60. GPU ka full form?", o:["Graphics Processing Unit","General Processing Unit","Game Processing Unit"], a:0},
{q:"61. 144 ka square root?", o:["11","12","13"], a:1},
{q:"62. WhatsApp kis ne banaya?", o:["Jan Koum","Mark Zuckerberg","Elon Musk"], a:0},
{q:"63. Sab se bara planet?", o:["Earth","Jupiter","Saturn"], a:1},
{q:"64. 7 x 8 =?", o:["54","56","64"], a:1},
{q:"65. CSS ka full form?", o:["Cascading Style Sheets","Computer Style Sheets","Creative Style Sheets"], a:0},
{q:"66. Pakistan ka national flag ka color?", o:["Red & Green","Green & White","Blue & White"], a:1},
{q:"67. 1000 - 1 =?", o:["999","1001","1000"], a:0},
{q:"68. iPhone kis company ka hai?", o:["Samsung","Apple","Nokia"], a:1},
{q:"69. 1 Decade me kitne saal?", o:["5","10","15"], a:1},
{q:"70. 3 + 3 x 3 =?", o:["12","18","9"], a:0},
{q:"71. SSD ka full form?", o:["Solid State Drive","Super Speed Drive","Storage System Drive"], a:0},
{q:"72. Sab se chota planet?", o:["Mercury","Mars","Venus"], a:0},
{q:"73. 50 + 50 =?", o:["90","100","110"], a:1},
{q:"74. TikTok kis country ki app hai?", o:["USA","China","Japan"], a:1},
{q:"75. 11 x 11 =?", o:["111","121","131"], a:1},
{q:"76. VPN ka full form?", o:["Virtual Private Network","Very Private Network","Virtual Public Network"], a:0},
{q:"77. 200 / 10 =?", o:["10","20","30"], a:1},
{q:"78. Sab se bara desert?", o:["Sahara","Gobi","Thar"], a:0},
{q:"79. 15 - 7 =?", o:["6","8","9"], a:1},
{q:"80. Zoom kis kaam aata hai?", o:["Chatting","Video Call","Gaming"], a:1},
{q:"81. 6 x 7 =?", o:["42","36","49"], a:0},
{q:"82. AI ka full form?", o:["Artificial Intelligence","Advanced Intelligence","Automatic Intelligence"], a:0},
{q:"83. 100 + 200 =?", o:["200","300","400"], a:1},
{q:"84. Sab se garam planet?", o:["Mercury","Venus","Mars"], a:1},
{q:"85. 25 x 4 =?", o:["80","100","120"], a:1},
{q:"86. Domain ka matlab?", o:["Website ka naam","Computer ka naam","Email ka naam"], a:0},
{q:"87. 9 + 10 =?", o:["18","19","20"], a:1},
{q:"88. Sab se zyada bolne wali zaban?", o:["English","Chinese","Hindi"], a:1},
{q:"89. 12 x 12 =?", o:["144","121","132"], a:0},
{q:"90. Blockchain kya hai?", o:["Database","Game","OS"], a:0},
{q:"91. 1000 + 500 =?", o:["1500","1005","2000"], a:0},
{q:"92. Sab se bara country?", o:["China","Russia","Canada"], a:1},
{q:"93. 4 x 25 =?", o:["75","100","125"], a:1},
{q:"94. Cloud storage ki example?", o:["Google Drive","RAM","CD"], a:0},
{q:"95. 30 x 3 =?", o:["60","90","120"], a:1},
{q:"96. QR Code kis ne banaya?", o:["Denso Wave","Google","Microsoft"], a:0},
{q:"97. 500 / 5 =?", o:["50","100","200"], a:1},
{q:"98. Sab se tez computer?", o:["Supercomputer","Laptop","Mobile"], a:0},
{q:"99. 17 + 18 =?", o:["34","35","36"], a:1},
{q:"100. Backup ka matlab?", o:["Data ki Copy","Delete","Share"], a:0},
// 101 to 500 mix Computer, GK, Math, Islamiyat
{q:"101. Excel kis company ka hai?", o:["Google","Microsoft","Apple"], a:1},{q:"102. 1 TB =?", o:["512 GB","1024 GB","2048 GB"], a:1},{q:"103. Pakistan ka pehla PM?", o:["Liaquat Ali Khan","Ayub Khan","Zulfiqar Ali"], a:0},{q:"104. 8 + 8 =?", o:["14","16","18"], a:1},{q:"105. Printer kya hai?", o:["Input","Output","Storage"], a:1},
{q:"106. 1 min =? ms", o:["1000","60000","100000"], a:1},{q:"107. WWW =?", o:["World Wide Web","World Wide Wireless","Web World Wide"], a:0},{q:"108. Bara masjid Pak?", o:["Faisal Masjid","Badshahi","Data"], a:0},{q:"109. 15 x 2 =?", o:["25","30","35"], a:1},{q:"110. BIOS =?", o:["Basic Input Output System","Best Input Output","Binary Input Output"], a:0},
{q:"111. 9 x 7 =?", o:["56","63","72"], a:1},{q:"112. 144 / 12 =?", o:["10","12","14"], a:1},{q:"113. 25 + 25 =?", o:["40","50","60"], a:1},{q:"114. 99 + 1 =?", o:["99","100","101"], a:1},{q:"115. 8 x 8 =?", o:["56","64","72"], a:1},
{q:"116. 100 - 50 =?", o:["40","50","60"], a:1},{q:"117. 6 x 6 =?", o:["30","36","42"], a:1},{q:"118. 100 / 4 =?", o:["20","25","30"], a:1},{q:"119. 13 x 13 =?", o:["156","169","182"], a:1},{q:"120. 1000 / 2 =?", o:["250","500","750"], a:1},
{q:"121. 3 x 30 =?", o:["60","90","120"], a:1},{q:"122. 45 + 55 =?", o:["90","100","110"], a:1},{q:"123. 200 / 4 =?", o:["40","50","60"], a:1},{q:"124. 14 x 14 =?", o:["186","196","206"], a:1},{q:"125. 1000 - 500 =?", o:["400","500","600"], a:1},
{q:"126. 12 x 5 =?", o:["50","60","70"], a:1},{q:"127. 88 / 8 =?", o:["9","11","12"], a:1},{q:"128. 7 x 7 =?", o:["42","49","56"], a:1},{q:"129. 300 / 3 =?", o:["90","100","110"], a:1},{q:"130. 16 x 16 =?", o:["256","266","276"], a:0},
{q:"131. 1000 + 1000 =?", o:["1000","2000","3000"], a:1},{q:"132. 9 x 6 =?", o:["45","54","63"], a:1},{q:"133. 72 / 9 =?", o:["7","8","9"], a:1},{q:"134. 5 x 40 =?", o:["150","200","250"], a:1},{q:"135. 125 + 125 =?", o:["200","250","300"], a:1},
{q:"136. 11 x 10 =?", o:["110","120","130"], a:0},{q:"137. 64 / 8 =?", o:["6","7","8"], a:2},{q:"138. 8 x 15 =?", o:["120","130","140"], a:0},{q:"139. 500 / 10 =?", o:["40","50","60"], a:1},{q:"140. 20 x 20 =?", o:["400","420","440"], a:0},
{q:"141. 1000 / 5 =?", o:["100","200","300"], a:1},{q:"142. 9 x 4 =?", o:["32","36","40"], a:1},{q:"143. 96 / 12 =?", o:["6","7","8"], a:2},{q:"144. 7 x 50 =?", o:["300","350","400"], a:1},{q:"145. 250 + 250 =?", o:["400","500","600"], a:1},
{q:"146. 15 x 15 =?", o:["225","235","245"], a:0},{q:"147. 81 / 9 =?", o:["7","8","9"], a:2},{q:"148. 6 x 25 =?", o:["150","160","170"], a:0},{q:"149. 1000 / 8 =?", o:["125","150","175"], a:0},{q:"150. 4 x 35 =?", o:["140","150","160"], a:0},
{q:"151. 900 / 3 =?", o:["300","400","500"], a:0},{q:"152. 12 x 12 =?", o:["144","154","164"], a:0},{q:"153. 100 / 25 =?", o:["2","4","5"], a:1},{q:"154. 8 x 30 =?", o:["240","250","260"], a:0},{q:"155. 600 / 6 =?", o:["90","100","110"], a:1},
{q:"156. 17 x 17 =?", o:["289","299","309"], a:0},{q:"157. 1000 - 250 =?", o:["650","750","850"], a:1},{q:"158. 5 x 50 =?", o:["200","250","300"], a:1},{q:"159. 121 / 11 =?", o:["10","11","12"], a:1},{q:"160. 9 x 20 =?", o:["180","190","200"], a:0},
{q:"161. 800 / 8 =?", o:["80","100","120"], a:1},{q:"162. 14 x 5 =?", o:["60","70","80"], a:1},{q:"163. 144 / 6 =?", o:["22","24","26"], a:1},{q:"164. 10 x 45 =?", o:["450","500","550"], a:0},{q:"165. 1000 / 10 =?", o:["90","100","110"], a:1},
{q:"166. 18 x 18 =?", o:["324","334","344"], a:0},{q:"167. 750 / 3 =?", o:["250","300","350"], a:0},{q:"168. 7 x 30 =?", o:["210","220","230"], a:0},{q:"169. 200 / 5 =?", o:["30","40","50"], a:2},{q:"170. 13 x 10 =?", o:["120","130","140"], a:1},
{q:"171. 1000 / 25 =?", o:["30","40","50"], a:1},{q:"172. 11 x 9 =?", o:["99","109","119"], a:0},{q:"173. 360 / 4 =?", o:["80","90","100"], a:1},{q:"174. 6 x 60 =?", o:["360","400","420"], a:0},{q:"175. 1000 / 20 =?", o:["40","50","60"], a:1},
{q:"176. 19 x 19 =?", o:["361","371","381"], a:0},{q:"177. 900 / 9 =?", o:["90","100","110"], a:1},{q:"178. 8 x 40 =?", o:["320","340","360"], a:0},{q:"179. 500 / 2 =?", o:["200","250","300"], a:1},{q:"180. 15 x 10 =?", o:["150","160","170"], a:0},
{q:"181. 1000 / 40 =?", o:["20","25","30"], a:1},{q:"182. 12 x 20 =?", o:["240","250","260"], a:0},{q:"183. 180 / 6 =?", o:["20","30","40"], a:1},{q:"184. 7 x 80 =?", o:["560","580","600"], a:0},{q:"185. 1000 / 50 =?", o:["10","20","30"], a:1},
{q:"186. 21 x 21 =?", o:["441","451","461"], a:0},{q:"187. 800 / 4 =?", o:["200","300","400"], a:0},{q:"188. 9 x 50 =?", o:["450","500","550"], a:0},{q:"189. 1000 / 100 =?", o:["5","10","15"], a:1},{q:"190. 14 x 20 =?", o:["280","300","320"], a:0},
{q:"191. 600 / 3 =?", o:["200","300","400"], a:0},{q:"192. 16 x 10 =?", o:["160","170","180"], a:0},{q:"193. 1000 / 200 =?", o:["3","5","10"], a:1},{q:"194. 18 x 5 =?", o:["80","90","100"], a:1},{q:"195. 700 / 7 =?", o:["90","100","110"], a:1},
{q:"196. 20 x 25 =?", o:["500","550","600"], a:0},{q:"197. 1000 / 250 =?", o:["2","4","5"], a:1},{q:"198. 25 x 20 =?", o:["500","550","600"], a:0},{q:"199. 1000 / 500 =?", o:["1","2","5"], a:1},{q:"200. Namaz ke farz?", o:["3","5","7"], a:1},
{q:"201. Roza kis mahine?", o:["Rajab","Shaban","Ramzan"], a:2},{q:"202. Hajj kahan?", o:["Madinah","Makkah","Jerusalem"], a:1},{q:"203. Quran ki zaban?", o:["Urdu","Arabic","Persian"], a:1},{q:"204. Pehle Nabi?", o:["Hazrat Adam","Hazrat Nooh","Hazrat Ibrahim"], a:0},{q:"205. 2 + 3 x 2 =?", o:["8","10","12"], a:0},
// 206 to 499 general mix
{q:"206. 10 x 10 =?", o:["100","110","120"], a:0},{q:"207. 50 x 3 =?", o:["150","200","250"], a:0},{q:"208. 100 / 20 =?", o:["3","5","10"], a:1},{q:"209. 12 x 8 =?", o:["86","96","106"], a:1},{q:"210. 1000 - 100 =?", o:["800","900","1000"], a:1},
{q:"211. 7 x 4 =?", o:["24","28","32"], a:1},{q:"212. 64 / 4 =?", o:["14","16","18"], a:1},{q:"213. 9 x 5 =?", o:["40","45","50"], a:1},{q:"214. 200 / 2 =?", o:["90","100","110"], a:1},{q:"215. 11 x 8 =?", o:["88","98","108"], a:0},
{q:"216. 1000 / 8 =?", o:["125","150","175"], a:0},{q:"217. 6 x 9 =?", o:["54","63","72"], a:0},{q:"218. 81 / 3 =?", o:["24","27","30"], a:1},{q:"219. 5 x 20 =?", o:["100","110","120"], a:0},{q:"220. 1000 - 200 =?", o:["700","800","900"], a:1},
{q:"221. 8 x 8 =?", o:["56","64","72"], a:1},{q:"222. 96 / 8 =?", o:["10","12","14"], a:1},{q:"223. 7 x 6 =?", o:["36","42","48"], a:1},{q:"224. 300 / 5 =?", o:["50","60","70"], a:1},{q:"225. 9 x 10 =?", o:["80","90","100"], a:1},
{q:"226. 1000 / 5 =?", o:["100","200","300"], a:1},{q:"227. 12 x 7 =?", o:["74","84","94"], a:1},{q:"228. 144 / 8 =?", o:["16","18","20"], a:0},{q:"229. 6 x 15 =?", o:["80","90","100"], a:1},{q:"230. 1000 - 300 =?", o:["600","700","800"], a:1},
{q:"231. 5 x 5 =?", o:["20","25","30"], a:1},{q:"232. 100 / 10 =?", o:["5","10","15"], a:1},{q:"233. 8 x 9 =?", o:["72","81","90"], a:0},{q:"234. 200 / 4 =?", o:["40","50","60"], a:1},{q:"235. 7 x 12 =?", o:["74","84","94"], a:1},
{q:"236. 1000 / 4 =?", o:["200","250","300"], a:1},{q:"237. 9 x 3 =?", o:["24","27","30"], a:1},{q:"238. 64 / 2 =?", o:["30","32","34"], a:1},{q:"239. 6 x 8 =?", o:["42","48","54"], a:1},{q:"240. 1000 - 400 =?", o:["500","600","700"], a:1},
{q:"241. 4 x 25 =?", o:["75","100","125"], a:1},{q:"242. 100 / 5 =?", o:["10","20","30"], a:1},{q:"243. 9 x 8 =?", o:["72","81","90"], a:0},{q:"244. 200 / 8 =?", o:["20","25","30"], a:1},{q:"245. 8 x 12 =?", o:["86","96","106"], a:1},
{q:"246. 1000 / 6 =?", o:["166","167","168"], a:0},{q:"247. 7 x 5 =?", o:["30","35","40"], a:1},{q:"248. 81 / 4 =?", o:["20
