<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Poetry Analysis Game</title>

<style>
:root{
  --baby:#b9e6ff;
  --winter:#5aaee8;
  --deep:#143d63;
  --emerald:#087f5b;
  --yellow:#ffd95a;
  --white:#ffffff;
  --soft:#eef9ff;
}
*{box-sizing:border-box}
body{
  font-family:Arial, sans-serif;
  background:linear-gradient(135deg,var(--baby),var(--white),#d9f7ec);
  margin:0;
  color:var(--deep);
  user-select:none;
}
.page{display:none;min-height:100vh;padding:25px 15px 80px;animation:fade .4s ease}
.active{display:block}
@keyframes fade{from{opacity:0;transform:translateY(10px)}to{opacity:1;transform:translateY(0)}}
.card{
  background:rgba(255,255,255,.96);
  padding:26px;
  border-radius:24px;
  max-width:1000px;
  margin:auto;
  border:4px solid var(--baby);
  box-shadow:0 14px 30px rgba(20,61,99,.18);
}
h1{text-align:center;font-size:3.2rem;color:var(--deep);text-shadow:3px 3px 0 var(--yellow);margin-bottom:10px}
h2{color:var(--emerald);border-left:9px solid var(--yellow);padding-left:12px}
h3{color:var(--deep)}
.subtitle{text-align:center;font-size:1.2rem;line-height:1.5;font-weight:bold;max-width:800px;margin:0 auto 25px}
button{padding:12px 18px;margin:8px 5px;border:none;border-radius:999px;background:linear-gradient(135deg,var(--emerald),var(--winter));color:white;font-weight:bold;cursor:pointer;font-size:1rem}
button:hover{transform:translateY(-2px)}
input, textarea{width:100%;padding:12px;border:2px solid var(--winter);border-radius:14px;font-size:1rem;margin-top:8px;font-family:Arial;background:white;user-select:text}
textarea{height:105px;resize:vertical}
.poem{white-space:pre-line;background:#f7fcff;border-left:8px solid var(--emerald);padding:18px;border-radius:16px;line-height:1.7}
.grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(220px,1fr));gap:14px;margin:18px 0}
.tile{background:linear-gradient(160deg,#f7fcff,#ffffff);border:2px solid var(--baby);border-radius:18px;padding:16px;box-shadow:0 7px 15px rgba(20,61,99,.08);animation:float 3s infinite ease-in-out}
.tile:nth-child(2){animation-delay:.3s}.tile:nth-child(3){animation-delay:.6s}.tile:nth-child(4){animation-delay:.9s}
@keyframes float{0%,100%{transform:translateY(0)}50%{transform:translateY(-6px)}}
.icon{font-size:2.3rem;display:block;text-align:center;margin-bottom:5px}
.noteBox{background:#fff9db;border:2px dashed var(--yellow);border-radius:18px;padding:15px;margin-top:18px;white-space:pre-wrap}
.question{background:#f8fdff;border:2px solid var(--baby);border-radius:18px;padding:16px;margin:18px 0}
.option{display:block;background:white;border:2px solid #d7eefb;border-radius:12px;margin:8px 0;padding:10px;cursor:pointer}
.option:hover{border-color:var(--yellow)}
.feedback{font-weight:bold;margin-top:10px}.correct{color:green}.incorrect{color:#b42318}
#confetti{position:fixed;top:0;left:0;width:100%;height:100%;pointer-events:none;z-index:5}
.badge-glow{animation:glow 1s infinite alternate;text-align:center;color:var(--emerald)}
@keyframes glow{from{text-shadow:0 0 8px gold}to{text-shadow:0 0 25px gold}}
.certificate{border:8px double var(--emerald);padding:30px;text-align:center;border-radius:20px;background:linear-gradient(#ffffff,#fff9db);margin-top:20px}
.small{font-size:.95rem;line-height:1.45}
.footer{text-align:center;font-weight:bold;color:var(--emerald);margin-top:25px}
.hidden-print-note{font-size:.9rem;color:#666}
@media print{
  button{display:none}
  body{background:white;user-select:text}
  .page{display:block;min-height:auto;page-break-after:always}
  .card{box-shadow:none;border:2px solid #ccefff}
  #confetti{display:none}
}
</style>
</head>

<body oncontextmenu="return false">
<canvas id="confetti"></canvas>

<div class="page active" id="p0">
<div class="card">
<h1>Poetry Analysis</h1>
<p class="subtitle">For those who don’t know, for those who think they know, but don’t know they don’t know, and for those who genuinely don’t know but want to learn.</p>
<div class="grid">
<div class="tile"><span class="icon">❄️</span><b>Structure Detective</b><br>Look closely at form, rhyme, and shifts.</div>
<div class="tile"><span class="icon">🌧️</span><b>Mood Tracker</b><br>Notice the feeling the poem creates for the reader.</div>
<div class="tile"><span class="icon">🌿</span><b>Figurative Language Finder</b><br>Analyze metaphors, personification, symbols, and imagery.</div>
<div class="tile"><span class="icon">💛</span><b>Theme Builder</b><br>Connect evidence to the deeper message.</div>
</div>
<p><b>Enter your name to begin:</b></p>
<input id="studentName" placeholder="Type your full name here" autocomplete="off">
<button type="button" onclick="start()">Start</button>
<p class="footer">Created by Dwaynna Ramsay Morgan</p>
</div>
</div>

<div class="page" id="p1">
<div class="card">
<h2>Step 1: Read the Poem Carefully</h2>
<p><b>Before we analyze, we read.</b> Read the poem carefully. Do not rush to answer questions yet. Notice repeated images, emotional words, punctuation, and where the poem seems to shift.</p>
<h3>Instruction Poem: “What lips my lips have kissed, and where, and why” by Edna St. Vincent Millay</h3>
<div class="poem">What lips my lips have kissed, and where, and why,
I have forgotten, and what arms have lain
Under my head till morning; but the rain
Is full of ghosts tonight, that tap and sigh
Upon the glass and listen for reply,
And in my heart there stirs a quiet pain
For unremembered lads that not again
Will turn to me at midnight with a cry.

Thus in the winter stands the lonely tree,
Nor knows what birds have vanished one by one,
Yet knows its boughs more silent than before:
I cannot say what loves have come and gone,
I only know that summer sang in me
A little while, that in me sings no more.</div>
<div class="noteBox">
<h3>Your Reading Notes</h3>
<textarea id="note1" placeholder="What words, images, or emotions stand out to you first?"></textarea>
</div>
<button type="button" onclick="nextPage()">Next: Line-by-Line Analysis</button>
</div>
</div>

<div class="page" id="p2">
<div class="card">
<h2>Step 2: Literal and Figurative Meaning</h2>
<p><b>Now that we have read the poem carefully, let’s slow down and look at what the lines mean.</b> A strong poetry reader asks: What is happening literally? What deeper meaning is created through figurative language?</p>
<div class="grid">
<div class="tile"><b>Lines 1–3</b><br>Literal: The speaker has forgotten specific past lovers.<br><br>Figurative Meaning: Memory is fading, but the emotional impact remains. The speaker may not remember every person clearly, but she still feels the weight of what has been lost.</div>
<div class="tile"><b>Lines 3–5</b><br>Literal: Rain taps against the window.<br><br>Device: Personification. The rain becomes “ghosts” that “tap and sigh,” making the memories feel alive, haunting, and impossible to fully ignore.</div>
<div class="tile"><b>Lines 6–8</b><br>Literal: The speaker feels quiet pain for lovers who will not return.<br><br>Meaning: The phrase “quiet pain” shows that the speaker is not loudly upset. Her sadness is controlled, reflective, and deeply lonely.</div>
<div class="tile"><b>Lines 9–14</b><br>Literal: A tree stands in winter after birds have left.<br><br>Device: Extended metaphor. The tree represents the speaker; the birds represent vanished love; summer represents youth, warmth, joy, and passion that no longer remain.</div>
</div>
<div class="noteBox">
<h3>Figurative Language Notes</h3>
<textarea id="note3" placeholder="Explain one figurative device and what it reveals."></textarea>
</div>
<button type="button" onclick="prevPage()">Back</button><button type="button" onclick="nextPage()">Next: Let Us Look at Structure</button>
</div>
</div>

<div class="page" id="p3">
<div class="card">
<h2>Step 3: Let Us Look at Its Structure</h2>
<p><b>After we understand the meaning of the lines, we can study how the poem is built.</b> Structure helps us see how the poet organizes ideas and creates a shift in meaning.</p>
<div class="grid">
<div class="tile"><span class="icon">🏛️</span><b>Form</b><br>This poem is a sonnet because it has 14 lines. Sonnets often explore one focused emotional problem or reflection.</div>
<div class="tile"><span class="icon">🔁</span><b>Rhyme Scheme</b><br>The rhyme pattern is ABBAABBACDEDCE. The pattern gives the poem control, even while the speaker discusses painful memories.</div>
<div class="tile"><span class="icon">↪️</span><b>Shift</b><br>The word “Thus” signals a turn from personal memory to a winter tree metaphor. This is where the speaker moves from remembering people to understanding her emotional condition.</div>
<div class="tile"><span class="icon">🌳</span><b>Meaning</b><br>The structure moves from forgotten love to a symbolic image of loneliness. The final image helps readers feel the silence left behind after love has gone.</div>
</div>
<p class="small"><b>Why structure matters:</b> The first eight lines focus on the speaker’s memories and pain. The final six lines compare the speaker to a lonely winter tree. This shift helps the reader understand that the speaker is not only remembering past love; she is realizing how empty life feels after that love and youthful joy have passed.</p>
<div class="noteBox">
<h3>Structure Notes</h3>
<textarea id="note2" placeholder="What do you notice about the sonnet form, rhyme scheme, or shift?"></textarea>
</div>
<button type="button" onclick="prevPage()">Back</button><button type="button" onclick="nextPage()">Next: Tone, Mood, and Theme</button>
</div>
</div>

<div class="page" id="p4">
<div class="card">
<h2>Step 4: How Tone, Mood, and Theme Are Developed</h2>
<div class="grid">
<div class="tile"><span class="icon">🎙️</span><b>Tone Development</b><br>The speaker’s tone begins reflective because she admits she has forgotten details of past love. It becomes mournful as the rain, ghosts, quiet pain, winter tree, and silent boughs reveal emotional emptiness.</div>
<div class="tile"><span class="icon">🌫️</span><b>Mood Development</b><br>The mood is shown through setting and imagery. Night, rain, ghosts, winter, and silence make the reader feel a haunting, lonely, and somber atmosphere.</div>
<div class="tile"><span class="icon">🌳</span><b>Theme Development</b><br>The theme develops as the poem moves from forgotten names to a deeper realization: love and youth may pass, but their absence can still be deeply felt.</div>
<div class="tile"><span class="icon">🔍</span><b>Evidence to Watch</b><br>“quiet pain,” “lonely tree,” “birds have vanished,” and “summer sang in me... no more” all build the tone, mood, and theme.</div>
</div>
<div class="noteBox">
<h3>Tone, Mood, and Theme Notes</h3>
<textarea id="note4" placeholder="How is the tone developed? How is the mood shown?"></textarea>
</div>
<button type="button" onclick="prevPage()">Back</button><button type="button" onclick="nextPage()">Next: Practice Poem</button>
</div>
</div>

<div class="page" id="p5">
<div class="card">
<h2>Practice Poem: “When You Are Old” by William Butler Yeats</h2>
<p>Now apply the same thinking. Read carefully first. Then analyze structure, figurative language, tone, mood, and theme.</p>
<div class="poem">When you are old and grey and full of sleep,
And nodding by the fire, take down this book,
And slowly read, and dream of the soft look
Your eyes had once, and of their shadows deep;

How many loved your moments of glad grace,
And loved your beauty with love false or true,
But one man loved the pilgrim soul in you,
And loved the sorrows of your changing face;

And bending down beside the glowing bars,
Murmur, a little sadly, how Love fled
And paced upon the mountains overhead
And hid his face amid a crowd of stars.</div>
<div class="noteBox">
<h3>Practice Poem Notes</h3>
<textarea id="note5" placeholder="What do you notice about structure, tone, mood, or theme in Yeats’s poem?"></textarea>
</div>
<button type="button" onclick="prevPage()">Back</button><button type="button" onclick="goToQuestions()">Next: Questions</button>
</div>
</div>

<div class="page" id="p6">
<div class="card">
<h2>8 Multiple Choice Questions</h2>
<p><b>Competency Goal:</b> Students must answer at least <b>6 out of 8</b> questions correctly to earn the completion certificate.</p>
<p><b>Important:</b> You will not see whether your answers are right or wrong until the end of the game. Read carefully and choose the best answer.</p>
<form id="quiz"></form>
<button type="button" onclick="prevPage()">Back</button><button type="button" onclick="submitQuiz()">Lock In Multiple Choice Answers</button><button type="button" onclick="goToShortAnswer()">Next: Short Answers</button>
</div>
</div>

<div class="page" id="p7">
<div class="card">
<h2>Short Answer Questions</h2>
<div class="question">
<h3>Short Answer 1</h3>
<p>Compare how both poems use images of time, age, seasons, or memory to develop a theme about love and loss. Use evidence from both poems.</p>
<textarea id="sa1" placeholder="Write your response here."></textarea>
</div>
<div class="question">
<h3>Short Answer 2</h3>
<p>Analyze how structure helps develop meaning in both poems. Discuss the shift in Millay’s poem and the stanza progression in Yeats’s poem.</p>
<textarea id="sa2" placeholder="Write your response here."></textarea>
</div>
<button type="button" onclick="prevPage()">Back</button><button type="button" onclick="finish()">Finish</button>
</div>
</div>

<div class="page" id="p8">
<div class="card">
<h2>Results and Certificate</h2>
<div id="result"></div>
<div id="certificate"></div>
<h2>Accumulated Notes</h2>
<div id="notes" class="noteBox"></div>
<p class="hidden-print-note">Use the buttons below to download student notes or print the results, notes, and certificate.</p>
<button type="button" onclick="downloadNotes()">Download Notes</button>
<button type="button" onclick="window.print()">Print Results, Notes, and Certificate</button>
</div>
</div>

<script>
(function(){
  'use strict';

  function byId(id){
    return document.getElementById(id);
  }

  function getValue(id){
    const element = byId(id);
    return element && typeof element.value === 'string' ? element.value : '';
  }

  function setHTML(id, html){
    const element = byId(id);
    if(element){ element.innerHTML = html; }
  }

  function setText(id, text){
    const element = byId(id);
    if(element){ element.innerText = text; }
  }

  document.addEventListener('copy', function(e){ e.preventDefault(); });
  document.addEventListener('cut', function(e){ e.preventDefault(); });
  document.addEventListener('paste', function(e){ e.preventDefault(); });
  document.addEventListener('keydown', function(e){
    if((e.ctrlKey || e.metaKey) && ['c','v','x','a'].includes(e.key.toLowerCase())){
      e.preventDefault();
    }
  });

  let page = 0;
  let score = 0;
  let submitted = false;
  const pages = Array.from(document.querySelectorAll('.page'));

  const questions = [
    {q:'1. Which statement best explains how Millay’s structure develops meaning?',a:['The sonnet begins with forgotten personal experiences and shifts into a metaphor that deepens the speaker’s loneliness.','The sonnet uses rhyme mainly to make the poem sound cheerful despite the speaker’s sadness.','The poem avoids a clear shift so the speaker’s emotions remain unchanged throughout.','The poem’s structure proves the speaker remembers every past relationship in exact detail.'],c:0},
    {q:'2. Which evidence best supports the idea that Millay’s mood is haunting rather than simply sad?',a:['“the rain / Is full of ghosts tonight, that tap and sigh”','“what arms have lain / Under my head”','“I have forgotten”','“what loves have come and gone”'],c:0},
    {q:'3. In Yeats’s poem, what does “pilgrim soul” most strongly suggest about the beloved?',a:['The speaker values the beloved’s inner journey, depth, and changing identity more than surface beauty.','The speaker thinks the beloved should travel more and experience the world.','The speaker only remembers the beloved’s beauty from youth.','The speaker believes the beloved’s sadness makes her impossible to love.'],c:0},
    {q:'4. Which claim best compares tone in the two poems?',a:['Both tones are reflective, but Millay’s is more haunted by absence while Yeats’s is more tender and regretful.','Both tones are angry because both speakers blame someone else for losing love.','Millay’s tone is humorous while Yeats’s tone is completely unemotional.','Both tones are joyful because the speakers celebrate memories without pain.'],c:0},
    {q:'5. Which answer best explains how mood is shown in Yeats’s poem?',a:['The quiet fire, old age, slow reading, and Love hiding among stars create a soft but sorrowful mood.','The poem’s mountain and star imagery makes the mood adventurous and exciting.','The repeated word “loved” creates a mood of complete happiness with no regret.','The speaker’s command to read the book creates a harsh and threatening mood.'],c:0},
    {q:'6. Which pair of evidence best supports a shared theme about love and the passing of time?',a:['“summer sang in me / A little while” and “When you are old and grey”','“Upon the glass” and “take down this book”','“what arms have lain” and “glad grace”','“winter stands” and “glowing bars”'],c:0},
    {q:'7. Which statement best analyzes the personification of Love in Yeats’s final stanza?',a:['Love becomes distant and unreachable, showing the pain of recognizing sincere love too late.','Love becomes playful and childish, showing that the speaker no longer cares.','Love becomes a villain, proving the beloved was intentionally cruel.','Love becomes realistic and ordinary, removing mystery from the poem.'],c:0},
    {q:'8. Which comparative thesis would be strongest for analyzing both poems?',a:['Both poems show that love gains emotional power through memory, absence, and the painful awareness of time passing.','Both poems prove that nature is more important than relationships because both mention outdoor images.','Both poems argue that people should forget the past completely in order to be happy.','Both poems suggest that beauty is the only reason love matters.'],c:0}
  ];

  function shuffleQuestions(){
    questions.forEach(function(q){
      const correct = q.a[q.c];
      for(let i = q.a.length - 1; i > 0; i--){
        const j = Math.floor(Math.random() * (i + 1));
        const temp = q.a[i];
        q.a[i] = q.a[j];
        q.a[j] = temp;
      }
      q.c = q.a.indexOf(correct);
    });
  }

  function showPage(index){
    if(index < 0 || index >= pages.length){ return; }
    pages[page].classList.remove('active');
    page = index;
    pages[page].classList.add('active');
    window.scrollTo(0,0);
  }

  window.start = function(){
    const studentName = getValue('studentName').trim();
    if(!studentName){
      alert('Enter your name.');
      return;
    }
    showPage(1);
  };

  window.nextPage = function(){
    showPage(page + 1);
  };

  window.prevPage = function(){
    showPage(page - 1);
  };

  window.goToQuestions = function(){
    window.render();
    showPage(6);
  };

  window.goToShortAnswer = function(){
    if(!submitted){
      alert('Please submit your multiple choice answers first.');
      return;
    }
    showPage(7);
  };

  window.render = function(){
    const quiz = byId('quiz');
    if(!quiz){ return; }
    if(quiz.innerHTML.trim()){ return; }

    const html = questions.map(function(q, i){
      const options = q.a.map(function(option, j){
        return '<label class="option"><input type="radio" name="q' + i + '" value="' + j + '"> ' + String.fromCharCode(65 + j) + '. ' + option + '</label>';
      }).join('');
      return '<div class="question"><h3>' + q.q + '</h3>' + options + '<div id="fb' + i + '" class="feedback"></div></div>';
    }).join('');

    quiz.innerHTML = html;
  };

  window.submitQuiz = function(){
    window.render();
    score = 0;
    let unanswered = 0;

    questions.forEach(function(q, i){
      const selected = document.querySelector('input[name="q' + i + '"]:checked');
      const feedback = byId('fb' + i);
      if(!feedback){ return; }

      if(!selected){
        unanswered++;
        feedback.innerHTML = '<span class="incorrect">Please answer this question.</span>';
      }else{
        if(Number(selected.value) === q.c){ score++; }
        feedback.innerHTML = '';
      }
    });

    if(unanswered > 0){
      submitted = false;
      alert('Please answer all 8 questions before moving on.');
      return;
    }

    submitted = true;
    alert('Your answers have been locked in. You will see your score at the end of the game.');
  };

  function collectNotes(){
    return 'Student: ' + getValue('studentName') + '\n\n' +
      'READING NOTES:\n' + getValue('note1') + '\n\n' +
      'STRUCTURE NOTES:\n' + getValue('note2') + '\n\n' +
      'FIGURATIVE LANGUAGE NOTES:\n' + getValue('note3') + '\n\n' +
      'TONE, MOOD, THEME NOTES:\n' + getValue('note4') + '\n\n' +
      'PRACTICE POEM NOTES:\n' + getValue('note5') + '\n\n' +
      'SHORT ANSWER 1:\n' + getValue('sa1') + '\n\n' +
      'SHORT ANSWER 2:\n' + getValue('sa2');
  }

  window.finish = function(){
    if(!submitted){
      window.submitQuiz();
      if(!submitted){ return; }
    }

    const student = getValue('studentName').trim() || 'Student';
    showPage(8);

    setHTML('result', '<h3>' + student + "'s Score: " + score + '/8</h3><p><b>Competency Requirement:</b> 6 out of 8 correct.</p>');

    if(score >= 6){
      setHTML('certificate', '<div class="certificate badge-glow"><h1>Certificate of Completion</h1><h2>' + student + '</h2><p>has completed the Poetry Analysis learning game and demonstrated understanding of structure, figurative language, tone, mood, and theme.</p><h3>Score: ' + score + '/8</h3><p class="footer">Created by Dwaynna Ramsay Morgan</p></div>');
      launchConfetti();
    }else{
      setHTML('certificate', '<div class="certificate"><h2>Keep Practicing</h2><p>' + student + ', review the instruction sections and try again. You need at least 6 out of 8 correct to earn the certificate.</p><button type="button" onclick="restartGame()">Restart Game</button></div>');
    }

    setText('notes', collectNotes());
  };

  window.restartGame = function(){
    location.reload();
  };

  window.downloadNotes = function(){
    const blob = new Blob([collectNotes()], {type:'text/plain'});
    const link = document.createElement('a');
    link.href = URL.createObjectURL(blob);
    link.download = 'poetry-analysis-notes.txt';
    document.body.appendChild(link);
    link.click();
    link.remove();
    URL.revokeObjectURL(link.href);
  };

  function launchConfetti(){
    const canvas = byId('confetti');
    if(!canvas || !canvas.getContext){ return; }
    const ctx = canvas.getContext('2d');
    canvas.width = window.innerWidth;
    canvas.height = window.innerHeight;
    ctx.clearRect(0, 0, canvas.width, canvas.height);
    for(let i = 0; i < 250; i++){
      ctx.fillStyle = ['gold','#087f5b','#5aaee8','#ffffff'][Math.floor(Math.random()*4)];
      ctx.fillRect(Math.random()*canvas.width, Math.random()*canvas.height, 6, 6);
    }
    setTimeout(function(){ ctx.clearRect(0, 0, canvas.width, canvas.height); }, 3500);
  }

  function runTests(){
    console.assert(!!byId('studentName'), 'Test failed: studentName input exists.');
    console.assert(Array.isArray(pages) && pages.length === 9, 'Test failed: 9 pages should exist.');
    console.assert(questions.length === 8, 'Test failed: quiz should contain 8 questions.');
    console.assert(typeof window.restartGame === 'function', 'Test failed: restartGame function should exist.');
    console.assert(questions.every(function(q){ return q.a.length === 4 && q.c >= 0 && q.c < 4; }), 'Test failed: each question has 4 options and one correct answer.');
    console.assert(getValue('missingElement') === '', 'Test failed: getValue safely handles missing elements.');
  }

  shuffleQuestions();
  runTests();
})();
</script>
</body>
</html>
