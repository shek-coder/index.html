from IPython.display import HTML

html_content = """
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Luxury Quiz Game</title>
  <style>
    :root {
      --bg1: #6a11cb;
      --bg2: #2575fc;
      --panel: rgba(255,255,255,0.08);
      --gold: #ffd700;
    }
    body {
      margin:0;
      font-family: 'Segoe UI', sans-serif;
      background: linear-gradient(135deg,var(--bg1),var(--bg2));
      color: #fff;
      height:100vh;
      display:flex;
      align-items:center;
      justify-content:center;
      overflow:hidden;
    }
    .container {
      width:90%;
      max-width:540px;
      background: var(--panel);
      padding:28px;
      border-radius:18px;
      box-shadow: 0 10px 30px rgba(0,0,0,0.45);
      text-align:center;
      animation: fadeIn 0.8s ease;
    }
    @keyframes fadeIn {
      from {opacity:0; transform:scale(0.9);}
      to {opacity:1; transform:scale(1);}
    }
    h1 { color:var(--gold); margin-bottom:18px; }
    h2 { margin:12px 0; }
    .category-btn {
      display:block;
      width:84%;
      margin:12px auto;
      padding:12px;
      background: linear-gradient(45deg,rgba(255,255,255,0.08),rgba(255,255,255,0.02));
      border:1px solid rgba(255,255,255,0.1);
      border-radius:12px;
      color:#fff;
      font-weight:bold;
      text-align:left;
      cursor:pointer;
      transition:all 0.3s ease;
    }
    .category-btn .icon {margin-right:10px;}
    .category-btn:hover {
      transform:scale(1.05);
      box-shadow:0 6px 20px rgba(0,0,0,0.35);
    }
    #quiz {display:none;}
    .timer {
      display:inline-block;
      background: rgba(0,0,0,0.3);
      padding:6px 14px;
      border-radius:12px;
      font-weight:bold;
      color:var(--gold);
      margin-bottom:12px;
    }
    #question {
      font-size:18px;
      min-height:48px;
      animation: slideIn 0.8s ease;
    }
    @keyframes slideIn {
      from {opacity:0; transform:translateY(15px);}
      to {opacity:1; transform:translateY(0);}
    }
    .options-wrap {max-height:240px; overflow:auto;}
    .option {
      background: rgba(255,255,255,0.08);
      margin:10px auto;
      padding:12px;
      border-radius:10px;
      cursor:pointer;
      text-align:left;
      transition:0.3s;
      animation: fadeIn 0.6s ease;
    }
    .option:hover {background: rgba(255,255,255,0.18);}
    .option.correct {background:#2ecc71 !important; color:#fff;}
    .option.wrong {background:#e74c3c !important; color:#fff;}
    #result {display:none;}
    .result-box {
      padding:20px;
      border-radius:14px;
      animation: fadeIn 1s ease;
    }
    .pass {
      background: rgba(46, 204, 113, 0.2);
      box-shadow:0 0 20px #2ecc71;
      color:#2ecc71;
    }
    .fail {
      background: rgba(231, 76, 60, 0.2);
      box-shadow:0 0 20px #e74c3c;
      color:#e74c3c;
    }
    .small-btn {
      margin:10px;
      padding:10px 16px;
      border:none;
      border-radius:10px;
      background: linear-gradient(45deg,rgba(255,255,255,0.08),rgba(255,255,255,0.02));
      color:#fff;
      cursor:pointer;
      font-weight:bold;
      transition:0.3s;
    }
    .small-btn:hover {transform:scale(1.05);}
  </style>
</head>
<body>
  <div class="container" id="categories">
    <h1>Choose Category</h1>
    <button class="category-btn" onclick="startQuiz('java')"><span class="icon">☕</span>java</button>
    <button class="category-btn" onclick="startQuiz('python')"><span class="icon">🐍</span>python</button>
    <button class="category-btn" onclick="startQuiz('html')"><span class="icon">🟠</span>html</button>
    <button class="category-btn" onclick="startQuiz('js')"><span class="icon">🌐</span>js</button>
</div>

  <div class="container" id="quiz">
    <div class="timer" id="timer">15s</div>
    <h2 id="question">Question</h2>
    <div class="options-wrap"><div id="options"></div></div>
    <div>
      <button class="small-btn" onclick="goToCategories()">⬅ Categories</button>
      <button class="small-btn" onclick="restartQuiz()">🔄 Restart</button>
    </div>
  </div>

  <div class="container" id="result">
    <div id="resultBox" class="result-box">
      <h2 id="resultText"></h2>
      <p id="scoreText"></p>
    </div>
    <button class="small-btn" onclick="restartQuiz()">🔄 Restart</button>
    <button class="small-btn" onclick="goToCategories()">⬅ Categories</button>
  </div>

<script>
  const quizData = {
    java: [
      {q:"What does CPU stand for?", opts:["Central Processing Unit","Control Process Unit","Central Power Unit","Compute Power Utility"], answer:0},
      {q:"What is the size of an int in Java?", opts:["2 bytes","4 bytes","8 bytes","None"], answer:1},
      {q:"Which is a programming language?", opts:["HTTP","Python","USB","HTML"], answer:1},
      {q:"Which keyword is used to inherit a class in Java?", opts:["extends","inherits","implements","instanceof"], answer:0},
      {q:"Which company created Windows?", opts:["Apple","Google","Microsoft","IBM"], answer:2},
      {q:"JVM stands for?", opts:["Java Virtual Machine","Java Variable Machine","Java Verified Machine","Java Visual Method"], answer:0},
      {q:"Which of the following is not a Java keyword?", opts:["Static","try","include","final"], answer:2},
      {q:"Which access modifier makes a member accessible within the same package only?", opts:["public","private","default","protected"], answer:2},
      {q:"Which is an operating system?", opts:["Linux","Oracle","C++","MySQL"], answer:0},
      {q:"RAM stands for?", opts:["Random Access Memory","Read All Memory","Run Active Memory","Rapid Access Mode"], answer:0}
    ],
    python: [
      {q:"Which keyword defines a function?", opts:["def","Key","name"], answer:0},
      {q:"What is the output of len('Hello')?", opts:["3","5","6"], answer:1},
      {q:"Which type is returned by input()?", opts:["str","int","double"], answer:0},
      {q:"What is the keyword for conditional branching?", opts:["if","else","switch"], answer:0},
      {q:"What symbol starts a comment in Python?", opts:["//","#","*/"], answer:1},
      {q:"What is the output of 3 // 2?", opts:["3","2","1"], answer:2},
      {q:"What data type is [1, 2, 3]?", opts:["int","list","string"], answer:1},
      {q:"Which statement is used to handle exceptions?", opts:["try-except","catch-except","default"], answer:0},
      {q:"Python supports multiple inheritance", opts:["Yes","No"], answer:0},
      {q:"Python is not a programming language?", opts:["TRUE","FALSE"], answer:1}
    ],
    html: [
      {q:"What does HTML stand for?", opts:["Hypertext Markup Language","Hidden Marked Language","Hyper Model Language"], answer:0},
      {q:"Which tag is used to create a hyperlink?", opts:["<href>","<a>","<src>"], answer:1},
      {q:"Which attribute is used for image sources?", opts:["src","href","img"], answer:0},
      {q:"How to create a numbered list?", opts:["<ol>","<ul>","<li>"], answer:0},
      {q:"What tag defines a table row?", opts:["<tr>","<td>","<tt>"], answer:0},
      {q:"What is the correct doctype for HTML5?", opts:["<html><html>","<!DOCTYPE html>","DOCTYPE html>"], answer:1},
      {q:"Which tag is used for the largest heading?", opts:["<h1>","<h6>","<h3>"], answer:0},
      {q:"Which tag defines a form input field?", opts:["<input>","<output>","<IP field>"], answer:0},
      {q:"What is the default method for a form?", opts:["DISPLAY","GET","SHOW"], answer:1},
      {q:"Which tag is used for the smallest heading?", opts:["<h1>","<h6>","<h2>"], answer:1}
    ],
    js: [
      {q:"Which of the following is NOT a primitive type in JS?", opts:["String","Number","Object","Boolean"], answer:2},
      {q:"What will typeof NaN return?", opts:["NaN","number","undefined","object"], answer:1},
      {q:"What keyword declares a constant in JavaScript?", opts:["const","let","static","var"], answer:0},
      {q:"How do you create a function in JS?", opts:["function myFunc()","def myFunc()","fun myFunc()","method myFunc()"], answer:0},
      {q:"Which symbol is used for single-line comments?", opts:["<!--","//","/*","#"], answer:1},
      {q:"What is the result of null == undefined?", opts:["true","false","TypeError","NaN"], answer:0},
      {q:"Which of these is a falsy value?", opts:["1","0","[]","0"], answer:1},
      {q:"What does === check for?", opts:["Value only","Type only","Value and type","None"], answer:2},
      {q:"Which object is used to parse JSON?", opts:["JSON","Parse","Math","String"], answer:0},
      {q:"How to write an arrow function?", opts:["(x) => x+1","function(x){ return x+1 }","def x(x): return x+1","x -> x+1"], answer:0}
    ],

  };

  let currentSet = [];
  let idx = 0;
  let score = 0;
  let timerId = null;
  let timeLeft = 15;

  const elCategories=document.getElementById('categories');
  const elQuiz=document.getElementById('quiz');
  const elResult=document.getElementById('result');
  const elQuestion=document.getElementById('question');
  const elOptions=document.getElementById('options');
  const elTimer=document.getElementById('timer');
  const elResultBox=document.getElementById('resultBox');
  const elResultText=document.getElementById('resultText');
  const elScoreText=document.getElementById('scoreText');

  function showPanel(id){
    elCategories.style.display="none";
    elQuiz.style.display="none";
    elResult.style.display="none";
    document.getElementById(id).style.display="block";
  }
function startQuiz(cat){
  const key = cat.toLowerCase(); // normalize to lowercase
  currentSet = quizData[key];

  if (!currentSet) {
    alert("No questions available for " + cat);
    return;
  }

  idx = 0;
  score = 0;
  showPanel('quiz');
  loadQuestion();
}

  function loadQuestion(){
    if (idx >= currentSet.length) { endQuiz(); return; }
    clearInterval(timerId);
    timeLeft = 15;
    elTimer.textContent = timeLeft + "s";
    const item = currentSet[idx];
    elQuestion.textContent = item.q;
    elOptions.innerHTML = "";
    item.opts.forEach((opt,i)=>{
      const d = document.createElement('div');
      d.className = "option";
      d.textContent = opt;
      d.onclick = () => choose(i,d);
      elOptions.appendChild(d);
    });
    timerId = setInterval(()=>{
      timeLeft--;
      elTimer.textContent = timeLeft + "s";
      if (timeLeft <= 0) {
        clearInterval(timerId);
        revealCorrect();
        setTimeout(()=>{ idx++; loadQuestion(); }, 1200);
      }
    },1000);
  }

  function choose(i,el){
    clearInterval(timerId);
    const correct = currentSet[idx].answer;
    if (i === correct) {
      el.classList.add('correct');
      score++;
    } else {
      el.classList.add('wrong');
      [...elOptions.children].forEach((c,j)=>{
        if (j === correct) c.classList.add('correct');
      });
    }
    setTimeout(()=>{ idx++; loadQuestion(); }, 1200);
  }

  function revealCorrect(){
    const correct = currentSet[idx].answer;
    [...elOptions.children].forEach((c,j)=>{
      if (j === correct) c.classList.add('correct');
    });
  }

  function endQuiz(){
    clearInterval(timerId);
    showPanel('result');
    elScoreText.textContent = `Score: ${score} / ${currentSet.length}`;
    if (score >= Math.ceil(currentSet.length / 2)) {
      elResultBox.className = "result-box pass";
      elResultText.textContent = "🎉 You Passed!";
    } else {
      elResultBox.className = "result-box fail";
      elResultText.textContent = "❌ You Failed!";
    }
  }

  function restartQuiz(){
    idx = 0;
    score = 0;
    showPanel('quiz');
    loadQuestion();
  }
  function goToCategories(){
    clearInterval(timerId);
    showPanel('categories');
  }

  showPanel('categories');
</script>
</body>
</html>
"""

display(HTML(html_content))

from IPython.display import HTML

html_content = """
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Luxury Quiz Game</title>
  <style>
    :root {
      --bg1: #6a11cb;
      --bg2: #2575fc;
      --panel: rgba(255,255,255,0.08);
      --gold: #ffd700;
    }
    body {
      margin:0;
      font-family: 'Segoe UI', sans-serif;
      background: linear-gradient(135deg,var(--bg1),var(--bg2));
      color: #fff;
      height:100vh;
      display:flex;
      align-items:center;
      justify-content:center;
      overflow:hidden;
    }
    .container {
      width:90%;
      max-width:540px;
      background: var(--panel);
      padding:28px;
      border-radius:18px;
      box-shadow: 0 10px 30px rgba(0,0,0,0.45);
      text-align:center;
      animation: fadeIn 0.8s ease;
    }
    @keyframes fadeIn {
      from {opacity:0; transform:scale(0.9);}
      to {opacity:1; transform:scale(1);}
    }
    h1 { color:var(--gold); margin-bottom:18px; }
    h2 { margin:12px 0; }
    .category-btn {
      display:block;
      width:84%;
      margin:12px auto;
      padding:12px;
      background: linear-gradient(45deg,rgba(255,255,255,0.08),rgba(255,255,255,0.02));
      border:1px solid rgba(255,255,255,0.1);
      border-radius:12px;
      color:#fff;
      font-weight:bold;
      text-align:left;
      cursor:pointer;
      transition:all 0.3s ease;
    }
    .category-btn .icon {margin-right:10px;}
    .category-btn:hover {
      transform:scale(1.05);
      box-shadow:0 6px 20px rgba(0,0,0,0.35);
    }
    #quiz {display:none;}
    .timer {
      display:inline-block;
      background: rgba(0,0,0,0.3);
      padding:6px 14px;
      border-radius:12px;
      font-weight:bold;
      color:var(--gold);
      margin-bottom:12px;
    }
    #question {
      font-size:18px;
      min-height:48px;
      animation: slideIn 0.8s ease;
    }
    @keyframes slideIn {
      from {opacity:0; transform:translateY(15px);}
      to {opacity:1; transform:translateY(0);}
    }
    .options-wrap {max-height:240px; overflow:auto;}
    .option {
      background: rgba(255,255,255,0.08);
      margin:10px auto;
      padding:12px;
      border-radius:10px;
      cursor:pointer;
      text-align:left;
      transition:0.3s;
      animation: fadeIn 0.6s ease;
    }
    .option:hover {background: rgba(255,255,255,0.18);}
    .option.correct {background:#2ecc71 !important; color:#fff;}
    .option.wrong {background:#e74c3c !important; color:#fff;}
    #result {display:none;}
    .result-box {
      padding:20px;
      border-radius:14px;
      animation: fadeIn 1s ease;
    }
    .pass {
      background: rgba(46, 204, 113, 0.2);
      box-shadow:0 0 20px #2ecc71;
      color:#2ecc71;
    }
    .fail {
      background: rgba(231, 76, 60, 0.2);
      box-shadow:0 0 20px #e74c3c;
      color:#e74c3c;
    }
    .small-btn {
      margin:10px;
      padding:10px 16px;
      border:none;
      border-radius:10px;
      background: linear-gradient(45deg,rgba(255,255,255,0.08),rgba(255,255,255,0.02));
      color:#fff;
      cursor:pointer;
      font-weight:bold;
      transition:0.3s;
    }
    .small-btn:hover {transform:scale(1.05);}
  </style>
</head>
<body>
  <div class="container" id="categories">
    <h1>Choose Category</h1>
<button class="category-btn" onclick="startQuiz('css')"><span class="icon">🎨</span>css</button>
    <button class="category-btn" onclick="startQuiz('php')"><span class="icon">🐘</span>php</button>
    <button class="category-btn" onclick="startQuiz('go')"><span class="icon">🌀</span>go</button>
    <button class="category-btn" onclick="startQuiz('ruby')"><span class="icon">💎</span>ruby</button>


    </div>

  <div class="container" id="quiz">
    <div class="timer" id="timer">15s</div>
    <h2 id="question">Question</h2>
    <div class="options-wrap"><div id="options"></div></div>
    <div>
      <button class="small-btn" onclick="goToCategories()">⬅ Categories</button>
      <button class="small-btn" onclick="restartQuiz()">🔄 Restart</button>
    </div>
  </div>

  <div class="container" id="result">
    <div id="resultBox" class="result-box">
      <h2 id="resultText"></h2>
      <p id="scoreText"></p>
    </div>
    <button class="small-btn" onclick="restartQuiz()">🔄 Restart</button>
    <button class="small-btn" onclick="goToCategories()">⬅ Categories</button>
  </div>

<script>
  const quizData = {
css: [
  { q: "What does CSS stand for?", opts: ["Cascading Style Sheets", "Colorful Style Syntax", "Computer Style Sheet", "Creative Style Sheets"], answer: 0 },
  { q: "Which property controls the text color of an element?", opts: ["font-color", "text-color", "color", "fgcolor"], answer: 2 },
  { q: "How do you select elements with class 'menu' in CSS?", opts: [".menu", "#menu", "menu", "*menu"], answer: 0 },
  { q: "Which CSS property is used to change the background of an element?", opts: ["bgcolor", "background-color", "color", "backgroundImage"], answer: 1 },
  { q: "What is the correct CSS syntax to make every <p> element have 10px margin?", opts: ["p {margin:10px;}", "p margin=10px;", "p {margin= 10px}", "<p style='margin:10px;'>"], answer: 0 },
  { q: "Which property is used to change the font of an element?", opts: ["font-style", "text-style", "font-family", "font-weight"], answer: 2 },
  { q: "How can you make a list that is not styled with bullets?", opts: ["list-style: none;", "list: no-bullet;", "list-style-type: none;", "bullet: none;"], answer: 0 },
  { q: "Which CSS property controls the space between lines of text?", opts: ["line-height", "text-height", "line-spacing", "letter-spacing"], answer: 0 },
  { q: "How do you make the text bold in CSS?", opts: ["font-weight: bold;", "text-weight: bold;", "font: bold;", "text: bold;"], answer: 0 },
  { q: "Which CSS property is used to position an element relative to its normal position?", opts: ["position: static;", "position: relative;", "position: absolute;", "position: fixed;"], answer: 1 }
],
php: [
  { q: "What does PHP stand for?", opts: ["Preprocessor Home Page", "PHP: Hypertext Preprocessor", "Private Home Page", "Personal Hypertext Processor"], answer: 1 },
  { q: "Which one is the correct way to start a PHP block?", opts: ["<?php", "<php>", "<?", "<script>php"], answer: 0 },
  { q: "How do you write a comment in PHP?", opts: ["// This is a comment", "# This is a comment", "/* This is a comment */", "All of the above"], answer: 3 },
  { q: "Which superglobal contains form data sent with POST method?", opts: ["$_GET", "$_POST", "$_REQUEST", "$_DATA"], answer: 1 },
  { q: "Which of the following is used to connect to MySQL in PHP (modern)?", opts: ["mysql_connect()", "mysqli_connect()", "connect()", "pdo_connect()"], answer: 1 },
  { q: "What does echo do in PHP?", opts: ["Outputs one or more strings", "Defines a constant", "Starts a loop", "Includes a file"], answer: 0 },
  { q: "How do you define a function in PHP?", opts: ["function myFunc() { }", "def myFunc() { }", "func myFunc() { }", "function:myFunc() { }"], answer: 0 },
  { q: "Which operator is used for string concatenation in PHP?", opts: ["+", ".", "&", "&&"], answer: 1 },
  { q: "Which statement is used to end a loop immediately in PHP?", opts: ["exit", "break", "stop", "end"], answer: 1 },
  { q: "Which one is a way to include another PHP file?", opts: ["#include 'file.php';", "include 'file.php';", "import 'file.php';", "requirefile 'file.php';"], answer: 1 }
],
go: [
  { q: "Who developed Go programming language?", opts: ["Google", "Microsoft", "Apple", "IBM"], answer: 0 },
  { q: "What is the file extension for Go source files?", opts: [".go", ".golang", ".g", ".gocode"], answer: 0 },
  { q: "Which keyword is used to define a function in Go?", opts: ["func", "function", "def", "fn"], answer: 0 },
  { q: "Which package is used to format I/O in Go?", opts: ["fmt", "io", "console", "stdio"], answer: 0 },
  { q: "How do you declare a variable in Go?", opts: ["var x int", "x := int", "declare x int", "x = int"], answer: 0 },
  { q: "What does Go use for concurrency?", opts: ["threads", "goroutines", "coroutines", "fibers"], answer: 1 },
  { q: "What is the zero value of a boolean in Go?", opts: ["true", "false", "0", "nil"], answer: 1 },
  { q: "Which symbol is used to import packages in Go?", opts: ["import", "#include", "require", "use"], answer: 0 },
  { q: "What is the starting point of a Go program?", opts: ["main()", "start()", "run()", "init()"], answer: 0 },
  { q: "How do you write a comment in Go?", opts: ["// comment", "/* comment */", "# comment", "-- comment"], answer: 0 }
],
ruby: [
  { q: "Who created Ruby?", opts: ["Yukihiro Matsumoto", "Guido van Rossum", "Dennis Ritchie", "James Gosling"], answer: 0 },
  { q: "What is the file extension of Ruby files?", opts: [".rb", ".ruby", ".r", ".ru"], answer: 0 },
  { q: "How do you define a method in Ruby?", opts: ["def methodName", "function methodName", "method methodName", "func methodName"], answer: 0 },
  { q: "What keyword ends a method in Ruby?", opts: ["end", "close", "return", "finish"], answer: 0 },
  { q: "What is used for string interpolation in Ruby?", opts: ["#{ }", "${ }", "{{ }}", "<%= %>"], answer: 0 },
  { q: "Which symbol is used for comments in Ruby?", opts: ["#", "//", "/* */", "--"], answer: 0 },
  { q: "Which method prints output in Ruby?", opts: ["puts", "echo", "print", "console.log"], answer: 0 },
  { q: "What is the boolean false value in Ruby?", opts: ["false", "0", "null", "none"], answer: 0 },
  { q: "What type is returned by gets() in Ruby?", opts: ["String", "Integer", "Boolean", "Array"], answer: 0 },
  { q: "What is the keyword to create a class in Ruby?", opts: ["class", "Class", "define", "struct"], answer: 0 }
]

  };

  let currentSet = [];
  let idx = 0;
  let score = 0;
  let timerId = null;
  let timeLeft = 15;

  const elCategories=document.getElementById('categories');
  const elQuiz=document.getElementById('quiz');
  const elResult=document.getElementById('result');
  const elQuestion=document.getElementById('question');
  const elOptions=document.getElementById('options');
  const elTimer=document.getElementById('timer');
  const elResultBox=document.getElementById('resultBox');
  const elResultText=document.getElementById('resultText');
  const elScoreText=document.getElementById('scoreText');

  function showPanel(id){
    elCategories.style.display="none";
    elQuiz.style.display="none";
    elResult.style.display="none";
    document.getElementById(id).style.display="block";
  }
function startQuiz(cat){
  const key = cat.toLowerCase(); // normalize to lowercase
  currentSet = quizData[key];

  if (!currentSet) {
    alert("No questions available for " + cat);
    return;
  }

  idx = 0;
  score = 0;
  showPanel('quiz');
  loadQuestion();
}

  function loadQuestion(){
    if (idx >= currentSet.length) { endQuiz(); return; }
    clearInterval(timerId);
    timeLeft = 15;
    elTimer.textContent = timeLeft + "s";
    const item = currentSet[idx];
    elQuestion.textContent = item.q;
    elOptions.innerHTML = "";
    item.opts.forEach((opt,i)=>{
      const d = document.createElement('div');
      d.className = "option";
      d.textContent = opt;
      d.onclick = () => choose(i,d);
      elOptions.appendChild(d);
    });
    timerId = setInterval(()=>{
      timeLeft--;
      elTimer.textContent = timeLeft + "s";
      if (timeLeft <= 0) {
        clearInterval(timerId);
        revealCorrect();
        setTimeout(()=>{ idx++; loadQuestion(); }, 1200);
      }
    },1000);
  }

  function choose(i,el){
    clearInterval(timerId);
    const correct = currentSet[idx].answer;
    if (i === correct) {
      el.classList.add('correct');
      score++;
    } else {
      el.classList.add('wrong');
      [...elOptions.children].forEach((c,j)=>{
        if (j === correct) c.classList.add('correct');
      });
    }
    setTimeout(()=>{ idx++; loadQuestion(); }, 1200);
  }

  function revealCorrect(){
    const correct = currentSet[idx].answer;
    [...elOptions.children].forEach((c,j)=>{
      if (j === correct) c.classList.add('correct');
    });
  }

  function endQuiz(){
    clearInterval(timerId);
    showPanel('result');
    elScoreText.textContent = `Score: ${score} / ${currentSet.length}`;
    if (score >= Math.ceil(currentSet.length / 2)) {
      elResultBox.className = "result-box pass";
      elResultText.textContent = "🎉 You Passed!";
    } else {
      elResultBox.className = "result-box fail";
      elResultText.textContent = "❌ You Failed!";
    }
  }

  function restartQuiz(){
    idx = 0;
    score = 0;
    showPanel('quiz');
    loadQuestion();
  }
  function goToCategories(){
    clearInterval(timerId);
    showPanel('categories');
  }

  showPanel('categories');
</script>
</body>
</html>
"""

display(HTML(html_content))

from IPython.display import HTML

html_content = """
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Luxury Quiz Game</title>
  <style>
    :root {
      --bg1: #6a11cb;
      --bg2: #2575fc;
      --panel: rgba(255,255,255,0.08);
      --gold: #ffd700;
    }
    body {
      margin:0;
      font-family: 'Segoe UI', sans-serif;
      background: linear-gradient(135deg,var(--bg1),var(--bg2));
      color: #fff;
      height:100vh;
      display:flex;
      align-items:center;
      justify-content:center;
      overflow:hidden;
    }
    .container {
      width:90%;
      max-width:540px;
      background: var(--panel);
      padding:28px;
      border-radius:18px;
      box-shadow: 0 10px 30px rgba(0,0,0,0.45);
      text-align:center;
      animation: fadeIn 0.8s ease;
    }
    @keyframes fadeIn {
      from {opacity:0; transform:scale(0.9);}
      to {opacity:1; transform:scale(1);}
    }
    h1 { color:var(--gold); margin-bottom:18px; }
    h2 { margin:12px 0; }
    .category-btn {
      display:block;
      width:84%;
      margin:12px auto;
      padding:12px;
      background: linear-gradient(45deg,rgba(255,255,255,0.08),rgba(255,255,255,0.02));
      border:1px solid rgba(255,255,255,0.1);
      border-radius:12px;
      color:#fff;
      font-weight:bold;
      text-align:left;
      cursor:pointer;
      transition:all 0.3s ease;
    }
    .category-btn .icon {margin-right:10px;}
    .category-btn:hover {
      transform:scale(1.05);
      box-shadow:0 6px 20px rgba(0,0,0,0.35);
    }
    #quiz {display:none;}
    .timer {
      display:inline-block;
      background: rgba(0,0,0,0.3);
      padding:6px 14px;
      border-radius:12px;
      font-weight:bold;
      color:var(--gold);
      margin-bottom:12px;
    }
    #question {
      font-size:18px;
      min-height:48px;
      animation: slideIn 0.8s ease;
    }
    @keyframes slideIn {
      from {opacity:0; transform:translateY(15px);}
      to {opacity:1; transform:translateY(0);}
    }
    .options-wrap {max-height:240px; overflow:auto;}
    .option {
      background: rgba(255,255,255,0.08);
      margin:10px auto;
      padding:12px;
      border-radius:10px;
      cursor:pointer;
      text-align:left;
      transition:0.3s;
      animation: fadeIn 0.6s ease;
    }
    .option:hover {background: rgba(255,255,255,0.18);}
    .option.correct {background:#2ecc71 !important; color:#fff;}
    .option.wrong {background:#e74c3c !important; color:#fff;}
    #result {display:none;}
    .result-box {
      padding:20px;
      border-radius:14px;
      animation: fadeIn 1s ease;
    }
    .pass {
      background: rgba(46, 204, 113, 0.2);
      box-shadow:0 0 20px #2ecc71;
      color:#2ecc71;
    }
    .fail {
      background: rgba(231, 76, 60, 0.2);
      box-shadow:0 0 20px #e74c3c;
      color:#e74c3c;
    }
    .small-btn {
      margin:10px;
      padding:10px 16px;
      border:none;
      border-radius:10px;
      background: linear-gradient(45deg,rgba(255,255,255,0.08),rgba(255,255,255,0.02));
      color:#fff;
      cursor:pointer;
      font-weight:bold;
      transition:0.3s;
    }
    .small-btn:hover {transform:scale(1.05);}
  </style>
</head>
<body>
  <div class="container" id="categories">
    <h1>Choose Category</h1>
    <button class="category-btn" onclick="startQuiz('c++')"><span class="icon">💻</span>C++</button>
    <button class="category-btn" onclick="startQuiz('c#')"><span class="icon">🎯</span>C#</button>
    <button class="category-btn" onclick="startQuiz('node.js')"><span class="icon">🌐</span>Node.js</button>
    <button class="category-btn" onclick="startQuiz('react.js')"><span class="icon">⚛️</span>React.js</button>
  </div>

  <div class="container" id="quiz">
    <div class="timer" id="timer">15s</div>
    <h2 id="question">Question</h2>
    <div class="options-wrap"><div id="options"></div></div>
    <div>
      <button class="small-btn" onclick="goToCategories()">⬅ Categories</button>
      <button class="small-btn" onclick="restartQuiz()">🔄 Restart</button>
    </div>
  </div>

  <div class="container" id="result">
    <div id="resultBox" class="result-box">
      <h2 id="resultText"></h2>
      <p id="scoreText"></p>
    </div>
    <button class="small-btn" onclick="restartQuiz()">🔄 Restart</button>
    <button class="small-btn" onclick="goToCategories()">⬅ Categories</button>
  </div>

<script>
const quizData = {
  "c++": [
    { q: "Who created C++?", opts: ["Bjarne Stroustrup", "Dennis Ritchie", "James Gosling", "Ken Thompson"], answer: 0 },
    { q: "What is the file extension of a C++ file?", opts: [".cpp", ".c", ".ccp", ".c++"], answer: 0 },
    { q: "Which concept allows multiple functions with the same name?", opts: ["Function Overloading", "Inheritance", "Polymorphism", "Encapsulation"], answer: 0 },
    { q: "Which symbol is used to denote a pointer?", opts: ["*", "&", "#", "@"], answer: 0 },
    { q: "Which keyword creates an object in C++?", opts: ["new", "create", "make", "malloc"], answer: 0 },
    { q: "What is the default access modifier for class members?", opts: ["private", "public", "protected", "static"], answer: 0 },
    { q: "Which operator is overloaded for output in C++?", opts: ["<<", ">>", "==", "::"], answer: 0 },
    { q: "Which of the following is a loop in C++?", opts: ["for", "foreach", "loop", "repeat"], answer: 0 },
    { q: "Which function is the starting point of a C++ program?", opts: ["main()", "start()", "init()", "run()"], answer: 0 },
    { q: "What does OOP stand for?", opts: ["Object Oriented Programming", "Open Operation Program", "Overload Oriented Process", "Optional Output Print"], answer: 0 }
  ],
  "c#": [
    { q: "C# is developed by?", opts: ["Microsoft", "Apple", "Google", "Oracle"], answer: 0 },
    { q: "Which symbol is used for namespaces in C#?", opts: ["using", "import", "include", "namespace"], answer: 0 },
    { q: "What is the extension of a C# file?", opts: [".cs", ".c#", ".c", ".cpp"], answer: 0 },
    { q: "What is used to define a class in C#?", opts: ["class", "Class", "define", "struct"], answer: 0 },
    { q: "Which method is the entry point in C#?", opts: ["Main()", "Start()", "Run()", "Begin()"], answer: 0 },
    { q: "What is the default access modifier for class in C#?", opts: ["internal", "public", "private", "protected"], answer: 0 },
    { q: "Which keyword is used to inherit a class?", opts: [":", "extends", "inherits", "->"], answer: 0 },
    { q: "How do you write a comment in C#?", opts: ["// comment", "/* comment */", "/// comment", "All of the above"], answer: 3 },
    { q: "What is used to handle exceptions in C#?", opts: ["try-catch", "error", "exception", "trap"], answer: 0 },
    { q: "Which is a value type in C#?", opts: ["int", "object", "string", "class"], answer: 0 }
  ],
  "node.js": [
    { q: "Node.js is built on which engine?", opts: ["V8", "SpiderMonkey", "Chakra", "Rhino"], answer: 0 },
    { q: "What is the file extension for a Node.js module?", opts: [".js", ".node", ".mod", ".json"], answer: 0 },
    { q: "Which method is used to read a file in Node.js?", opts: ["fs.readFile()", "read()", "readFile()", "getFile()"], answer: 0 },
    { q: "Which module is used for creating a server?", opts: ["http", "url", "fs", "net"], answer: 0 },
    { q: "What does npm stand for?", opts: ["Node Package Manager", "New Programming Method", "Network Protocol Manager", "None"], answer: 0 },
    { q: "Which keyword is used to export a module?", opts: ["module.exports", "export", "return", "require"], answer: 0 },
    { q: "Which is not a core module?", opts: ["express", "http", "fs", "path"], answer: 0 },
    { q: "Which function is used to include modules?", opts: ["require()", "include()", "import()", "use()"], answer: 0 },
    { q: "Which type of environment is Node.js?", opts: ["Asynchronous", "Synchronous", "Single-threaded", "Both A & C"], answer: 3 },
    { q: "How do you handle exceptions in Node.js?", opts: ["try-catch", "throw", "error", "All of the above"], answer: 3 }
  ],
  "react.js": [
    { q: "Who developed React.js?", opts: ["Facebook", "Google", "Microsoft", "Amazon"], answer: 0 },
    { q: "What is JSX?", opts: ["JavaScript XML", "Java Syntax Extension", "JSON-like Syntax", "None"], answer: 0 },
    { q: "Which hook is used for state management?", opts: ["useState", "useEffect", "useReducer", "useRef"], answer: 0 },
    { q: "Which command creates a new React app?", opts: ["npx create-react-app", "npm install react", "react-new", "create-react"], answer: 0 },
    { q: "What is a component in React?", opts: ["Reusable UI block", "CSS file", "Function only", "HTML tag"], answer: 0 },
    { q: "Which lifecycle method is replaced by useEffect?", opts: ["componentDidMount", "constructor", "render", "shouldComponentUpdate"], answer: 0 },
    { q: "How to pass data to child component?", opts: ["props", "state", "emit", "context"], answer: 0 },
    { q: "What does React use to identify elements?", opts: ["key", "id", "ref", "class"], answer: 0 },
    { q: "React is mainly used for?", opts: ["Building UI", "Database", "Networking", "Testing"], answer: 0 },
    { q: "Which of the following is a hook?", opts: ["useState", "setInterval", "setTimeout", "addEventListener"], answer: 0 }
  ]
};

let currentSet = [], idx = 0, score = 0, timerId = null, timeLeft = 15;
const elCategories = document.getElementById('categories');
const elQuiz = document.getElementById('quiz');
const elResult = document.getElementById('result');
const elQuestion = document.getElementById('question');
const elOptions = document.getElementById('options');
const elTimer = document.getElementById('timer');
const elResultBox = document.getElementById('resultBox');
const elResultText = document.getElementById('resultText');
const elScoreText = document.getElementById('scoreText');

function showPanel(id) {
  elCategories.style.display = "none";
  elQuiz.style.display = "none";
  elResult.style.display = "none";
  document.getElementById(id).style.display = "block";
}

function startQuiz(cat) {
  const key = cat.toLowerCase();
  currentSet = quizData[key];
  if (!currentSet) { alert("No questions available for " + cat); return; }
  idx = 0; score = 0; // Added missing assignment
  showPanel('quiz');
  loadQuestion();
}

function loadQuestion() {
  if (idx >= currentSet.length) { endQuiz(); return; }
  clearInterval(timerId);
  timeLeft = 15;
  elTimer.textContent = timeLeft + "s";
  const item = currentSet[idx];
  elQuestion.textContent = item.q;
  elOptions.innerHTML = "";
  item.opts.forEach((opt, i) => {
    const d = document.createElement('div');
    d.className = "option";
    d.textContent = opt;
    d.onclick = () => choose(i, d);
    elOptions.appendChild(d);
  });
  timerId = setInterval(() => {
    timeLeft--;
    elTimer.textContent = timeLeft + "s";
    if (timeLeft <= 0) {
      clearInterval(timerId);
      revealCorrect();
      setTimeout(() => { idx++; loadQuestion(); }, 1200);
    }
  }, 1000);
}

function choose(i, el) {
  clearInterval(timerId);
  const correct = currentSet[idx].answer;
  if (i === correct) {
    el.classList.add('correct');
    score++;
  } else {
    el.classList.add('wrong');
    [...elOptions.children].forEach((c, j) => {
      if (j === correct) c.classList.add('correct');
    });
  }
  setTimeout(() => { idx++; loadQuestion(); }, 1200);
}

function revealCorrect() {
  const correct = currentSet[idx].answer;
  [...elOptions.children].forEach((c, j) => {
    if (j === correct) c.classList.add('correct');
  });
}

function endQuiz() {
  clearInterval(timerId);
  showPanel('result');
  elScoreText.textContent = `Score: ${score} / ${currentSet.length}`;
  if (score >= Math.ceil(currentSet.length / 2)) {
    elResultBox.className = "result-box pass";
    elResultText.textContent = "🎉 You Passed!";
  } else {
    elResultBox.className = "result-box fail";
    elResultText.textContent = "❌ You Failed!";
  }
}

function restartQuiz() {
  idx = 0;
  score = 0;
  showPanel('quiz');
  loadQuestion();
}
function goToCategories() {
  clearInterval(timerId);
  showPanel('categories');
}

showPanel('categories');
</script>
</body>
</html>
"""

display(HTML(html_content))
