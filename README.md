<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Опрос по ПК</title>
<style>
  body {
    font-family: Arial, sans-serif;
    background: linear-gradient(135deg,#6e8efb,#a777e3);
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    margin:0;
  }
  .quiz-container {
    background: #fff;
    padding: 30px 40px;
    border-radius: 15px;
    box-shadow: 0 15px 30px rgba(0,0,0,0.3);
    width: 450px;
    max-width: 90%;
    text-align: center;
  }
  h2 {
    margin-bottom: 25px;
    transition: opacity 0.3s ease;
  }
  button {
    display: block;
    margin: 12px 0;
    padding: 12px;
    width: 100%;
    border: none;
    border-radius: 8px;
    background: #4CAF50;
    color: #fff;
    font-size: 16px;
    cursor: pointer;
    transition: all 0.2s ease;
  }
  button:hover {
    background: #45a049;
    transform: translateY(-2px);
    box-shadow: 0 5px 10px rgba(0,0,0,0.2);
  }
  .result {
    font-size: 22px;
    font-weight: bold;
    color: #333;
    margin-top: 20px;
  }
</style>
</head>
<body>
<div class="quiz-container">
  <h2 id="question">Вопрос</h2>
  <div id="answers"></div>
  <div class="result" id="result" style="display:none;"></div>
</div>

<script>
const quiz = [
  {q:"Что такое GPU?", a:["Процессор для графики","Процессор для сети","Процессор для звука"], correct:0},
  {q:"Что такое CPU?", a:["Центральный процессор","Видеокарта","Оперативная память"], correct:0},
  {q:"Что обозначает GHz в процессоре?", a:["Частоту","Объём памяти","Мощность видеокарты"], correct:0},
  {q:"Для чего нужна видеокарта?", a:["Обработка графики","Хранение данных","Управление сетью"], correct:0},
  {q:"Что такое VRAM?", a:["Память видеокарты","Оперативная память","Процессорная кэш-память"], correct:0},
  {q:"Что лучше для игр?", a:["Быстрый GPU","Быстрая клавиатура","Большой монитор"], correct:0},
  {q:"Что такое ядро CPU?", a:["Один процессорный блок","Оперативная память","Разъём на материнской плате"], correct:0},
  {q:"Что ускоряет работу компьютера?", a:["Больше RAM","Мышка","Клавиатура"], correct:0},
  {q:"Что делает кулер в ПК?", a:["Охлаждает компоненты","Ускоряет интернет","Включает светодиоды"], correct:0},
  {q:"Что такое разгон (overclocking)?", a:["Увеличение частоты компонентов","Снижение температуры","Очистка диска"], correct:0}
];

let current = 0;
let score = 0;

function shuffleArray(arr){
  for(let i = arr.length - 1; i > 0; i--){
    const j = Math.floor(Math.random()*(i+1));
    [arr[i], arr[j]] = [arr[j], arr[i]];
  }
  return arr;
}

function showQuestion(){
  const q = quiz[current];
  document.getElementById('question').style.opacity = 0;
  setTimeout(()=>{ 
    document.getElementById('question').innerText = q.q;
    document.getElementById('question').style.opacity = 1;

    const answersDiv = document.getElementById('answers');
    answersDiv.innerHTML = '';

    let options = q.a.map((text,index)=>({text, index}));
    options = shuffleArray(options);

    options.forEach(opt=>{
      const btn = document.createElement('button');
      btn.innerText = opt.text;
      btn.onclick = ()=>answer(opt.index);
      answersDiv.appendChild(btn);
    });
  }, 200);
}

function answer(idx){
  if(idx === quiz[current].correct) score++;
  current++;
  if(current < quiz.length){
    showQuestion();
  } else {
    document.getElementById('answers').style.display = 'none';
    document.getElementById('question').style.display = 'none';
    const result = document.getElementById('result');
    result.style.display = 'block';
    result.innerText = `Вы ответили правильно на ${score} из ${quiz.length} вопросов.`;
  }
}

showQuestion();
</script>
</body>
</html>
