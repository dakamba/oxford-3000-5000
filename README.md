<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<title>Oxford 3000 и 5000</title>
<script>
(function () {
  var t = null;
  try { t = localStorage.getItem('oxford3000_p1_theme'); } catch (e) {}
  if (!t) t = window.matchMedia && matchMedia('(prefers-color-scheme: dark)').matches ? 'dark' : 'light';
  document.documentElement.setAttribute('data-theme', t);
})();
</script>
<style>
:root{
  --paper:#eef1ec; --card:#fbfcfa; --ink:#17201c; --muted:#5f6d64; --rule:#c9d3cb;
  --accent:#1f6b5b; --accent-ink:#ffffff; --known:#2f7d4a; --review:#b7791f; --bad:#b4372f;
}
[data-theme="dark"]{
  --paper:#0f1412; --card:#161d1a; --ink:#e5ece7; --muted:#8fa096; --rule:#2c3832;
  --accent:#6cc4aa; --accent-ink:#0f1412; --known:#5fbf86; --review:#e0aa4f; --bad:#ef7a70;
}
*{box-sizing:border-box}
[hidden]{display:none!important}
body{margin:0;min-height:100vh;background:var(--paper);color:var(--ink);font:16px/1.5 system-ui,-apple-system,"Segoe UI",Roboto,sans-serif;-webkit-tap-highlight-color:transparent}
h1,.word,.en,.big{font-family:Georgia,"Iowan Old Style","Palatino Linotype",Palatino,"Times New Roman",serif}
.wrap{max-width:880px;margin:0 auto;padding:20px 16px 36px}
h1{margin:0;font-size:1.6rem;font-weight:700;letter-spacing:-.01em}
.muted{color:var(--muted)}
.head{display:flex;justify-content:space-between;align-items:flex-start;gap:12px;flex-wrap:wrap}
.chips{display:flex;flex-wrap:wrap;gap:6px;margin-top:10px}
.chip{font-size:.8rem;border:1px solid var(--rule);border-radius:6px;padding:3px 8px;color:var(--muted);background:var(--card)}
.chip b{color:var(--ink)}
.meter{height:4px;background:var(--rule);margin:14px 0 4px;border-radius:2px;overflow:hidden}
.meter i{display:block;height:100%;width:0;background:var(--accent);transition:width .4s}
button,input,select{font:inherit;color:var(--ink)}
button{cursor:pointer;border:1px solid var(--rule);background:var(--card);padding:10px 16px;border-radius:8px;transition:transform .08s,opacity .2s}
button:active{transform:scale(.97)}
button:disabled{opacity:.4;cursor:default}
button.solid{background:var(--accent);border-color:var(--accent);color:var(--accent-ink)}
button.known{background:var(--known);border-color:var(--known);color:#fff}
button.review{background:var(--review);border-color:var(--review);color:#1c1c1c}
button.quiet{background:transparent}
input,select{padding:10px 12px;border:1px solid var(--rule);border-radius:8px;background:var(--card)}
:focus-visible{outline:2px solid var(--accent);outline-offset:2px}
@media (prefers-reduced-motion:reduce){*{transition:none!important}}
.tabs{display:flex;gap:4px;border-bottom:1px solid var(--rule);margin:18px 0;overflow-x:auto}
.tab{border:0;border-radius:0;background:transparent;padding:10px 12px;color:var(--muted);border-bottom:2px solid transparent;margin-bottom:-1px;white-space:nowrap}
.tab.active{color:var(--ink);border-bottom-color:var(--accent)}
.panel{display:none}
.panel.active{display:block}
.toolbar{display:flex;flex-wrap:wrap;gap:8px;align-items:center;margin-bottom:16px}
.sheet{background:var(--card);border:1px solid var(--rule);border-radius:12px;padding:20px;min-height:220px}
.bar{height:4px;background:var(--rule);border-radius:2px;overflow:hidden;margin:10px 0 18px}
.bar i{display:block;height:100%;background:var(--accent);transition:width .3s}
.qhead{display:flex;justify-content:space-between;color:var(--muted);font-size:.9rem;gap:12px;flex-wrap:wrap}
.prompt{display:flex;flex-direction:column;align-items:center;gap:6px;text-align:center;margin:10px 0 18px}
.word{font-size:clamp(1.8rem,6vw,2.6rem);font-weight:700;overflow-wrap:anywhere;line-height:1.2}
.opts{display:grid;grid-template-columns:1fr 1fr;gap:10px}
.opt{text-align:left;padding:14px;font-size:1rem;line-height:1.3}
.opt kbd{font:600 .72rem system-ui,sans-serif;color:var(--muted);border:1px solid var(--rule);border-radius:4px;padding:0 5px;margin-right:8px}
.opt.right{background:var(--known);border-color:var(--known);color:#fff}
.opt.wrong{background:var(--bad);border-color:var(--bad);color:#fff}
.opt.right kbd,.opt.wrong kbd{color:#fff;border-color:#fff}
#typeInput{display:block;width:100%;font-size:1.15rem;text-align:center;padding:14px}
.fb{min-height:52px;text-align:center;margin:12px 0;line-height:1.6}
.good{color:var(--known)}
.bad{color:var(--bad)}
.actions{display:flex;gap:10px;justify-content:center;flex-wrap:wrap;margin-top:14px}
.actions button{min-width:120px}
.result{text-align:center;padding:12px 0}
.big{font-size:3.6rem;font-weight:700;color:var(--accent);line-height:1}
.wlist{list-style:none;padding:0;margin:10px auto;max-width:440px;text-align:left;max-height:260px;overflow:auto}
.wlist li{padding:6px 0;border-bottom:1px solid var(--rule)}
.stage{perspective:1400px;margin:4px 0 20px}
.flip{position:relative;height:290px;transform-style:preserve-3d;transition:transform .6s cubic-bezier(.3,.6,.2,1);cursor:pointer;user-select:none}
.flip.is-flipped{transform:rotateY(180deg)}
.face{position:absolute;inset:0;backface-visibility:hidden;-webkit-backface-visibility:hidden;display:flex;flex-direction:column;align-items:center;justify-content:center;gap:12px;padding:28px;text-align:center;border:1px solid var(--rule);border-radius:12px;background:var(--card)}
.face.back{transform:rotateY(180deg);background:var(--accent);border-color:var(--accent);color:var(--accent-ink)}
.face.back .muted{color:inherit;opacity:.8}
.badge{position:absolute;top:14px;left:16px;font-size:.75rem;border-radius:999px;padding:2px 10px;border:1px solid var(--rule);color:var(--muted)}
.badge.known{background:var(--known);border-color:var(--known);color:#fff}
.badge.review{background:var(--review);border-color:var(--review);color:#1c1c1c}
.center{text-align:center}
.letters{display:flex;flex-wrap:wrap;gap:4px;margin-bottom:10px}
.letters button{padding:5px 9px;font-size:.88rem;border-radius:6px}
.letters button.on{background:var(--ink);border-color:var(--ink);color:var(--paper)}
.list{background:var(--card);border:1px solid var(--rule);border-radius:12px;overflow:hidden}
.row{display:grid;grid-template-columns:auto 1fr auto;gap:12px;align-items:center;padding:10px 14px;border-bottom:1px solid var(--rule)}
.row:last-child{border-bottom:0}
.en{font-weight:700;font-size:1.05rem}
.ru{color:var(--muted)}
.stbtn{padding:5px 10px;font-size:.8rem;border-radius:999px;white-space:nowrap}
.speak{padding:6px 10px;border-radius:8px}
.nospeech .speak{display:none}
footer{margin-top:30px;color:var(--muted);font-size:.88rem;display:flex;flex-wrap:wrap;gap:12px;align-items:center;justify-content:space-between}
@media (max-width:600px){
  .opts{grid-template-columns:1fr}
  .row{grid-template-columns:auto 1fr}
  .row .stbtn{grid-column:2;justify-self:start}
  .actions button{flex:1;min-width:0}
  .flip{height:250px}
}
</style>
</head>
<body>
<div class="wrap">
  <header class="head">
    <div>
      <h1>Oxford 3000 и 5000</h1>
      <div class="chips" id="chips"></div>
    </div>
    <button class="quiet" id="themeBtn" type="button"></button>
  </header>
  <div class="meter"><i id="meter"></i></div>

  <nav class="tabs" role="tablist">
    <button class="tab active" data-tab="cards" type="button">Карточки</button>
    <button class="tab" data-tab="quiz" type="button">Тест</button>
    <button class="tab" data-tab="typing" type="button">Ввод</button>
    <button class="tab" data-tab="dict" type="button">Словарь</button>
  </nav>

  <section class="panel active" id="p-cards">
    <div class="toolbar">
      <select id="cardsFilter" aria-label="Какие слова показывать"></select>
      <button class="quiet" id="shuffleBtn" type="button">Перемешать</button>
      <span class="muted" id="cardsCount"></span>
    </div>
    <div class="stage">
      <div class="flip" id="flip" role="button" tabindex="0" aria-label="Перевернуть карточку">
        <div class="face front">
          <span class="badge" id="cardBadge"></span>
          <div class="word" id="cardEn"></div>
          <div class="muted">Нажмите или пробел, чтобы перевернуть</div>
        </div>
        <div class="face back">
          <div class="word" id="cardRu"></div>
          <div id="cardEn2"></div>
        </div>
      </div>
    </div>
    <div class="actions">
      <button class="quiet" id="prevBtn" type="button" aria-label="Предыдущее слово">←</button>
      <button class="review" id="repeatBtn" type="button">Повторить</button>
      <button class="known" id="knowBtn" type="button">Знаю</button>
      <button class="quiet" id="nextBtn" type="button" aria-label="Следующее слово">→</button>
    </div>
    <p class="center"><button class="quiet speak" id="cardSpeak" type="button">🔊 Произнести</button></p>
  </section>

  <section class="panel" id="p-quiz">
    <div class="toolbar">
      <select id="quizPool" aria-label="Набор слов"></select>
      <select id="quizCount" aria-label="Количество вопросов">
        <option>10</option><option selected>20</option><option>50</option><option>100</option>
      </select>
      <select id="quizDir" aria-label="Направление">
        <option value="en-ru">Английский → русский</option>
        <option value="ru-en">Русский → английский</option>
      </select>
      <button class="solid" id="quizStart" type="button">Начать</button>
    </div>
    <div class="sheet" id="quizBox">
      <p class="muted">Выберите набор и нажмите «Начать». Клавиши 1–4 выбирают ответ, Enter переходит дальше.</p>
    </div>
  </section>

  <section class="panel" id="p-typing">
    <div class="toolbar">
      <select id="typePool" aria-label="Набор слов"></select>
      <select id="typeDir" aria-label="Направление">
        <option value="en-ru">Английский → русский</option>
        <option value="ru-en">Русский → английский</option>
      </select>
      <button class="solid" id="typeStart" type="button">Начать</button>
    </div>
    <div class="sheet" id="typeBox">
      <p class="muted">Введите перевод вручную и нажмите Enter. Проверяется написание: регистр и буква ё/е не важны.</p>
    </div>
  </section>

  <section class="panel" id="p-dict">
    <div class="toolbar">
      <input type="search" id="search" placeholder="Поиск по слову или переводу" style="flex:1;min-width:200px">
      <select id="dictStatus" aria-label="Статус"></select>
    </div>
    <div class="letters" id="letters"></div>
    <p class="muted" id="dictCount"></p>
    <div class="list" id="dictList"></div>
  </section>

  <footer>
    <span>Прогресс и статистика хранятся в этом браузере.</span>
    <button class="quiet" id="resetBtn" type="button">Сбросить прогресс</button>
  </footer>
</div>

<script>
const WORDS = [["a","a"],["abandon","покинуть"],["ability","способность"],["able","способный"],["about","о"],["above","выше"],["abroad","за границей"],["absolute","абсолютно"],["absolutely","абсолютно"],["academic","академия"],["accept","принимать"],["acceptable","приемлемый"],["access","доступ"],["accident","авария"],["accommodation","проживание"],["accompany","сопровождать"],["according to","в соответствии с"],["account","счет"],["accurate","точный"],["accuse","обвинять"],["achieve","достижение"],["achievement","достижение"],["acknowledge","признать"],["acquire","приобрести"],["across","через"],["act","действовать"],["action","действие"],["active","активный"],["activity","деятельность"],["actor","актер"],["actress","актриса"],["actual","актуально"],["actually","на самом деле"],["ad","объявление"],["adapt","адаптировать"],["add","добавить"],["addition","добавление"],["additional","дополнительный"],["address","адрес"],["administration","администрация"],["admire","восхищаться"],["admit","признать"],["adopt","усыновить"],["adult","взрослый"],["advance","продвигаться"],["advanced","продвинутый"],["advantage","преимущество"],["adventure","приключение"],["advertise","рекламировать"],["advertisement","реклама"],["advertising","реклама"],["advice","совет"],["advise","совет"],["affair","дело"],["affect","влиять"],["afford","позволить себе"],["afraid","бояться"],["after","после"],["afternoon","после обеда"],["afterwards","после"],["again","снова"],["against","против"],["age","возраст"],["aged","в возрасте"],["agency","агентство"],["agenda","повестка дня"],["agent","агент"],["aggressive","агрессивный"],["ago","давно"],["agree","согласиться"],["agreement","соглашение"],["ah","ах"],["ahead","впереди"],["aid","помощь"],["aim","цель"],["air","воздух"],["aircraft","самолёт"],["airline","авиакомпания"],["airport","аэропорт"],["alarm","сигнализация"],["album","альбом"],["alcohol","алкоголь"],["alcoholic","алкоголь"],["alive","живой"],["all","все"],["all right","в порядке"],["allow","разрешить"],["almost","почти"],["alone","один"],["along","вдоль"],["already","уже"],["also","также"],["alter","изменить"],["alternative","альтернатива"],["although","хотя"],["always","всегда"],["amazed","удивительно"],["amazing","удивительно"],["ambition","амбиции"],["ambitious","амбициозный"],["among","среди"],["amount","количество"],["analyse","анализировать"],["analysis","анализ"],["ancient","древний"],["and","и"],["anger","гнев"],["angle","угол"],["angrily","гневно"],["angry","сердито"],["animal","животное"],["ankle","лодыжка"],["anniversary","юбилей"],["announce","объявление"],["announcement","объявление"],["annoy","раздражать"],["annoyed","надоедливый"],["annoying","надоедливый"],["annual","ежегодный"],["another","другой"],["answer","ответить"],["anxious","беспокойный"],["any","любой"],["any more","ещё"],["anybody","кто-либо"],["anyone","кто-либо"],["anything","что-нибудь"],["anyway","в любом случае"],["anywhere","где угодно"],["apart","отдельно"],["apartment","квартира"],["apologize","извиниться"],["app","приложение"],["apparent","очевидное"],["apparently","очевидно"],["appeal","апеллировать"],["appear","появиться"],["appearance","появление"],["apple","яблоко"],["application","применение"],["apply","подать заявку"],["appointment","назначение"],["appreciate","ценить"],["approach","подходить"],["appropriate","подходящий"],["approval","одобрение"],["approve","одобрить"],["approximately","примерно"],["april","апрель"],["architect","архитектор"],["architecture","архитектура"],["area","область"],["argue","спорить"],["argument","спорить"],["arise","возникнуть"],["arm","рука"],["armed","вооружённый"],["arms","оружие"],["army","армия"],["around","вокруг"],["arrange","организовать"],["arrangement","расположение"],["arrest","арест"],["arrival","прибытие"],["arrive","прибыть"],["art","искусство"],["article","статья"],["artificial","искусственный"],["artist","художник"],["artistic","художественный"],["as","как"],["ashamed","стыдно"],["ask","спросить"],["asleep","спать"],["aspect","аспект"],["assess","оценить"],["assessment","оценка"],["assignment","задание"],["assist","ассистировать"],["assistant","помощник"],["associate","ассоциировать"],["associated","ассоциированный"],["association","ассоциация"],["assume","предполагать"],["at","на"],["athlete","спортсмен"],["atmosphere","атмосфера"],["attach","присоединиться"],["attack","атаковать"],["attempt","попытка"],["attend","посещать"],["attention","внимание"],["attitude","отношение"],["attract","привлекать"],["attraction","привлекательность"],["attractive","привлекательный"],["audience","аудитория"],["august","август"],["aunt","тётя"],["author","автор"],["authority","авторитет"],["autumn","осень"],["available","доступный"],["average","средний"],["avoid","избегать"],["award","награда"],["aware","знать"],["away","прочь"],["awful","ужасно"],["baby","ребенок"],["back","назад"],["background","фон"],["backwards","назад"],["bacteria","бактерии"],["bad","плохо"],["badly","плохо"],["bag","сумка"],["bake","выпечка"],["balance","баланс"],["ball","мяч"],["ban","запрет"],["banana","банан"],["band","группа"],["bank","банк"],["bar","бар"],["barrier","барьер"],["base","база"],["baseball","бейсбол"],["based","базовый"],["basic","базовый"],["basically","основа"],["basis","основа"],["basketball","баскетбол"],["bath","ванна"],["bathroom","ванная"],["battery","батарея"],["battle","битва"],["be","быть"],["beach","пляж"],["bean","боб"],["bear","медведь"],["beat","бить"],["beautiful","красивый"],["beauty","красота"],["because","потому что"],["become","стать"],["bed","кровать"],["bedroom","спальня"],["bee","пчела"],["beef","говядина"],["beer","пиво"],["before","до"],["beg","умолять"],["begin","начинать"],["beginning","начало"],["behave","вести себя"],["behaviour","поведение"],["behind","за"],["being","быть"],["belief","вера"],["believe","верить"],["bell","колокол"],["belong","принадлежать"],["below","ниже"],["belt","пояс"],["bend","сгибаться"],["benefit","выгода"],["bent","согнутый"],["best","лучший"],["bet","ставка"],["better","лучше"],["between","между"],["beyond","за пределами"],["bicycle","велосипед"],["big","большой"],["bike","велосипед"],["bill","билл"],["billion","миллиард"],["bin","бин"],["biology","биология"],["bird","птица"],["birth","рождение"],["birthday","день рождения"],["biscuit","печенье"],["bit","кусочек"],["bite","укус"],["bitter","горький"],["black","чёрный"],["blame","винить"],["blank","пустой"],["blind","слепой"],["block","блок"],["blog","блог"],["blonde","блондинка"],["blood","кровь"],["blow","удар"],["blue","голубой"],["board","доска"],["boat","лодка"],["body","тело"],["boil","кипятить"],["bomb","бомба"],["bond","облигация"],["bone","кость"],["book","книга"],["boot","сапог"],["border","граница"],["bored","скучный"],["boring","скучный"],["born","родиться"],["borrow","одолжить"],["boss","начальник"],["both","оба"],["bother","беспокоить"],["bottle","бутылка"],["bottom","дно"],["bowl","миска"],["box","ящик"],["boy","парень"],["boyfriend","парень"],["brain","мозг"],["branch","ветка"],["brand","бренд"],["brave","храбрый"],["bread","хлеб"],["break","перерыв"],["breakfast","завтрак"],["breast","грудь"],["breath","дышать"],["breathe","дышать"],["breathing","дыхание"],["bride","невеста"],["bridge","мост"],["brief","краткое"],["bright","яркий"],["brilliant","блестящий"],["bring","принести"],["broad","широкий"],["broadcast","вещание"],["broken","сломанный"],["brother","брат"],["brown","коричневый"],["brush","кисть"],["bubble","пузырь"],["budget","бюджет"],["build","построить"],["building","строительство"],["bullet","пуля"],["bunch","куча"],["burn","сжечь"],["bury","хоронить"],["bus","автобус"],["bush","куст"],["business","бизнес"],["businessman","бизнесмен"],["busy","занят"],["but","но"],["butter","масло"],["button","кнопка"],["buy","купить"],["by","по"],["bye","пока"],["cable","кабель"],["cafe","кафе"],["cake","торт"],["calculate","рассчитать"],["call","звонок"],["calm","спокойствие"],["camera","камера"],["camp","лагерь"],["campaign","кампания"],["camping","кемпинг"],["campus","кампус"],["can","можно"],["cancel","отменить"],["cancer","рак"],["candidate","кандидат"],["cannot","нельзя"],["cap","крышка"],["capable","способный"],["capacity","способность"],["capital","столица"],["captain","капитан"],["capture","захват"],["car","автомобиль"],["card","карта"],["care","уход"],["career","карьера"],["careful","осторожно"],["carefully","осторожно"],["careless","небрежность"],["carpet","ковёр"],["carrot","морковь"],["carry","нести"],["cartoon","мультфильм"],["case","чемодан"],["cash","наличные"],["cast","гипс"],["castle","замок"],["cat","кот"],["catch","ловить"],["category","категория"],["cause","причина"],["cd","cd"],["ceiling","потолок"],["celebrate","праздновать"],["celebration","праздник"],["celebrity","знаменитость"],["cell","ячейка"],["cent","цент"],["central","центр"],["centre","центр"],["century","век"],["ceremony","церемония"],["certain","определенно"],["certainly","безусловно"],["chain","цепь"],["chair","кресло"],["chairman","председатель"],["challenge","вызов"],["champion","чемпион"],["chance","шанс"],["change","изменение"],["channel","канал"],["chapter","глава"],["character","персонаж"],["characteristic","характеристика"],["charge","плата"],["charity","благотворительность"],["chart","график"],["chat","чат"],["cheap","дешево"],["cheat","обмануть"],["check","проверить"],["cheerful","веселый"],["cheese","сыр"],["chef","шеф-повар"],["chemical","химия"],["chemistry","химия"],["chest","грудь"],["chicken","курица"],["chief","шеф"],["child","ребенок"],["childhood","детство"],["chip","чип"],["chocolate","шоколад"],["choice","выбор"],["choose","выбрать"],["church","церковь"],["cigarette","сигарета"],["cinema","кинотеатр"],["circle","круг"],["circumstance","обстоятельство"],["cite","цитировать"],["citizen","гражданин"],["city","город"],["civil","гражданин"],["claim","иск"],["class","класс"],["classic","классика"],["classical","классика"],["classroom","класс"],["clause","статья"],["clean","чистый"],["clear","ясно"],["clearly","ясно"],["clever","умный"],["click","нажмите"],["client","клиент"],["climate","климат"],["climb","подняться"],["clock","часы"],["close","закрыть"],["closed","закрыто"],["closely","близко"],["cloth","ткань"],["clothes","одежда"],["clothing","одежда"],["cloud","облако"],["club","клуб"],["clue","подсказка"],["coach","тренер"],["coal","уголь"],["coast","побережье"],["coat","пальто"],["code","код"],["coffee","кофе"],["coin","монета"],["cold","холод"],["collapse","коллапс"],["colleague","коллега"],["collect","собирать"],["collection","коллекция"],["college","колледж"],["colour","цвет"],["coloured","цветной"],["column","колонка"],["combination","комбинация"],["combine","комбинация"],["come","зайти"],["comedy","комедия"],["comfort","комфорт"],["comfortable","комфортный"],["command","командовать"],["comment","комментарий"],["commercial","реклама"],["commission","комиссия"],["commit","обязательство"],["commitment","обязательство"],["committee","комитет"],["common","общий"],["commonly","обычно"],["communicate","общаться"],["communication","общение"],["community","сообщество"],["company","компания"],["compare","сравнить"],["comparison","сравнение"],["compete","конкурировать"],["competition","конкуренция"],["competitive","конкурент"],["competitor","конкурент"],["complain","жаловаться"],["complaint","жалоба"],["complete","полностью"],["completely","полностью"],["complex","сложный"],["complicated","сложный"],["component","компонент"],["computer","компьютер"],["concentrate","концентрация"],["concentration","концентрация"],["concept","концепция"],["concern","озабоченность"],["concerned","озабоченный"],["concert","концерт"],["conclude","заключение"],["conclusion","заключение"],["condition","условие"],["conduct","проводить"],["conference","конференция"],["confidence","уверенность"],["confident","уверенность"],["confirm","подтвердить"],["conflict","конфликт"],["confuse","путать"],["confused","путать"],["confusing","путать"],["connect","соединять"],["connected","соединённый"],["connection","связь"],["conscious","сознание"],["consequence","следствие"],["conservative","консервативный"],["consider","рассматривать"],["consideration","рассмотрение"],["consist","состоять"],["consistent","постоянный"],["constant","постоянный"],["constantly","постоянно"],["construct","строить"],["construction","строительство"],["consume","потреблять"],["consumer","потребитель"],["contact","контакт"],["contain","содержать"],["container","контейнер"],["contemporary","современный"],["content","содержание"],["contest","конкурс"],["context","контекст"],["continent","континент"],["continue","продолжать"],["continuous","продолжение"],["contract","договор"],["contrast","контраст"],["contribute","вклад"],["contribution","вклад"],["control","контроль"],["convenient","удобно"],["conversation","разговор"],["convert","преобразовать"],["convince","убедить"],["convinced","убеждённый"],["cook","готовить"],["cooker","плита"],["cooking","приготовление"],["cool","охлаждать"],["copy","копия"],["core","ядро"],["corner","угол"],["corporate","корпоративный"],["correct","правильно"],["correctly","правильно"],["cost","стоимость"],["costume","костюм"],["cottage","коттедж"],["cotton","хлопок"],["could","можно"],["council","совет"],["count","граф"],["country","деревня"],["countryside","сельская местность"],["county","графство"],["couple","пара"],["courage","мужество"],["course","курс"],["court","суд"],["cousin","двоюродный брат"],["cover","прикрытие"],["covered","покрытый"],["cow","корова"],["crash","авария"],["crazy","сумасшествие"],["cream","крем"],["create","создать"],["creation","творчество"],["creative","креатив"],["creature","создание"],["credit","кредит"],["crew","команда"],["crime","преступление"],["criminal","криминал"],["crisis","кризис"],["criterion","критерий"],["critic","критик"],["critical","критика"],["criticism","критика"],["criticize","критиковать"],["crop","культура"],["cross","скрещивать"],["crowd","толпа"],["crowded","толпа"],["crucial","решающий"],["cruel","жестокий"],["cry","плакать"],["cultural","культура"],["culture","культура"],["cup","чашка"],["cupboard","шкаф"],["cure","вылечить"],["curly","кудрявый"],["currency","валюта"],["current","текущий"],["currently","в настоящее время"],["curtain","занавес"],["curve","кривая"],["curved","изогнутый"],["custom","заказ"],["customer","клиент"],["cut","вырезать"],["cycle","цикл"],["dad","папа"],["daily","ежедневно"],["damage","повреждение"],["dance","танец"],["dancer","танцор"],["dancing","танец"],["danger","опасность"],["dangerous","опасный"],["dark","темнота"],["data","данные"],["date","дата"],["daughter","дочь"],["day","день"],["dead","мёртвый"],["deal","сделка"],["dear","дорогая"],["death","смерть"],["debate","дебаты"],["debt","долг"],["decade","декада"],["december","декабрь"],["decent","достойный"],["decide","решить"],["decision","решение"],["declare","заявить"],["decline","отказаться"],["decorate","украсить"],["decoration","украшение"],["decrease","уменьшаться"],["deep","глубоко"],["deeply","глубоко"],["defeat","поражение"],["defence","оборона"],["defend","защита"],["define","определить"],["definite","определенно"],["definitely","определенно"],["definition","определение"],["degree","степень"],["delay","задержка"],["deliberate","преднамеренный"],["deliberately","преднамеренно"],["delicious","вкусный"],["delight","восторг"],["delighted","восхищённый"],["deliver","доставить"],["delivery","доставка"],["demand","требовать"],["demonstrate","демонстрировать"],["dentist","стоматолог"],["deny","отказать"],["department","отдел"],["departure","отъезд"],["depend","зависеть"],["depressed","депрессия"],["depressing","депрессия"],["depth","глубина"],["describe","описать"],["description","описание"],["desert","пустыня"],["deserve","заслужить"],["design","дизайн"],["designer","дизайнер"],["desire","желание"],["desk","стол"],["desperate","отчаянный"],["despite","несмотря на"],["destination","место назначения"],["destroy","уничтожить"],["detail","деталь"],["detailed","подробно"],["detect","обнаружить"],["detective","детектив"],["determine","определить"],["determined","определенный"],["develop","разработка"],["development","разработка"],["device","устройство"],["diagram","диаграмма"],["dialogue","диалог"],["diamond","бриллиант"],["diary","дневник"],["dictionary","словарь"],["die","умереть"],["diet","диета"],["difference","разница"],["different","разное"],["differently","по-разному"],["difficult","трудность"],["difficulty","трудность"],["dig","копать"],["digital","цифровой"],["dinner","ужин"],["direct","направление"],["direction","направление"],["directly","непосредственно"],["director","директор"],["dirt","грязь"],["dirty","грязный"],["disadvantage","недостаток"],["disagree","не соглашаться"],["disappear","исчезнуть"],["disappointed","разочарованный"],["disappointing","разочарование"],["disaster","катастрофа"],["disc","диск"],["discipline","дисциплина"],["discount","скидка"],["discover","открыть для себя"],["discovery","открытие"],["discuss","обсудить"],["discussion","обсуждение"],["disease","болезнь"],["dish","блюдо"],["dishonest","нечестный"],["dislike","не нравится"],["dismiss","отвергать"],["display","показывать"],["distance","расстояние"],["distribute","распределять"],["distribution","распределение"],["district","район"],["divide","разделить"],["division","разделение"],["divorced","разведен"],["do","делать"],["doctor","врач"],["document","документ"],["documentary","документальный фильм"],["dog","собака"],["dollar","доллар"],["domestic","домашний"],["dominate","доминировать"],["donate","пожертвовать"],["door","дверь"],["double","двойная"],["doubt","сомнение"],["down","вниз"],["download","скачать"],["downstairs","вниз"],["downwards","вниз"],["dozen","дюжина"],["draft","черновик"],["drag","тащить"],["drama","драма"],["dramatic","драматический"],["draw","рисовать"],["drawing","рисунок"],["dream","мечта"],["dress","платье"],["dressed","одеваться"],["drink","пить"],["drive","водить"],["driver","водитель"],["driving","вождение"],["drop","бросить"],["drug","наркотик"],["drum","барабан"],["drunk","пьяный"],["dry","сухой"],["due","из-за"],["during","во время"],["dust","пыль"],["duty","долг"],["dvd","dvd"],["each","каждый"],["ear","ухо"],["early","рано"],["earn","заработать"],["earth","земля"],["earthquake","землетрясение"],["easily","легко"],["east","восток"],["eastern","восток"],["easy","легко"],["eat","есть"],["economic","экономика"],["economy","экономика"],["edge","край"],["edit","редактировать"],["edition","издание"],["editor","редактор"],["educate","просвещать"],["educated","образованный"],["education","образование"],["educational","образование"],["effect","эффект"],["effective","эффективно"],["effectively","эффективно"],["efficient","эффективно"],["effort","усилие"],["egg","яйцо"],["eight","восемь"],["eighteen","восемнадцать"],["eighty","восемьдесят"],["either","либо"],["elderly","пожилой"],["elect","выборы"],["election","выборы"],["electric","электрический"],["electrical","электрический"],["electricity","электричество"],["electronic","электронная"],["element","элемент"],["elephant","слон"],["eleven","одиннадцать"],["else","еще"],["elsewhere","в другом месте"],["email","электронная почта"],["embarrassed","смущенный"],["embarrassing","смущение"],["emerge","появиться"],["emergency","чрезвычайная ситуация"],["emotion","эмоция"],["emotional","эмоциональный"],["emphasis","акцент"],["emphasize","подчеркивать"],["employ","нанимать"],["employee","работник"],["employer","работодатель"],["employment","работа"],["empty","пустой"],["enable","разрешить"],["encounter","встреча"],["encourage","поощрять"],["end","конец"],["ending","конец"],["enemy","враг"],["energy","энергия"],["engage","задействовать"],["engaged","задействован"],["engine","двигатель"],["engineer","инженер"],["engineering","инженерия"],["enhance","улучшать"],["enjoy","наслаждаться"],["enormous","огромный"],["enough","достаточно"],["enquiry","запрос"],["ensure","обеспечить"],["enter","войти"],["entertain","развлекать"],["entertainment","развлечение"],["enthusiasm","энтузиазм"],["enthusiastic","энтузиаст"],["entire","полностью"],["entirely","полностью"],["entrance","вход"],["entry","вход"],["environment","окружающая среда"],["environmental","окружающая среда"],["episode","эпизод"],["equal","равный"],["equally","одинаково"],["equipment","оборудование"],["error","ошибка"],["escape","побег"],["especially","особенно"],["essay","эссе"],["essential","важно"],["establish","создать"],["estate","поместье"],["estimate","оценка"],["ethical","этика"],["euro","евро"],["evaluate","оценить"],["even","даже"],["evening","вечер"],["event","событие"],["eventually","в конце концов"],["ever","когда-либо"],["every","каждый"],["everybody","все"],["everyday","каждый день"],["everyone","все"],["everything","все"],["everywhere","везде"],["evidence","доказательства"],["evil","зло"],["exact","точно"],["exactly","точно"],["exam","экзамен"],["examination","экзамен"],["examine","исследовать"],["example","пример"],["excellent","отлично"],["except","кроме"],["exchange","обмен"],["excited","возбужденный"],["excitement","возбуждение"],["exciting","возбуждающий"],["excuse","оправдание"],["executive","руководитель"],["exercise","упражнение"],["exhibition","выставка"],["exist","существовать"],["existence","существование"],["expand","расширяться"],["expect","ожидать"],["expectation","ожидание"],["expected","ожидание"],["expedition","экспедиция"],["expense","расход"],["expensive","дорого"],["experience","опыт"],["experienced","опытный"],["experiment","эксперимент"],["expert","эксперт"],["explain","объяснить"],["explanation","объяснение"],["explode","взорваться"],["exploration","исследование"],["explore","исследовать"],["explosion","взрыв"],["export","экспорт"],["expose","разоблачить"],["express","экспресс"],["expression","выражение"],["extend","расширять"],["extent","степень"],["external","внешний"],["extra","экстра"],["extraordinary","экстраординарный"],["extreme","экстремальный"],["extremely","чрезвычайно"],["eye","глаз"],["face","лицо"],["facility","объект"],["fact","факт"],["factor","фактор"],["factory","завод"],["fail","провал"],["failure","провал"],["fair","честно"],["fairly","справедливо"],["faith","вера"],["fall","падение"],["FALSE","FALSE"],["familiar","знакомый"],["family","семья"],["famous","знаменитый"],["fan","поклонник"],["fancy","фантазия"],["fantastic","фантастика"],["far","далеко"],["farm","ферма"],["farmer","фермер"],["farming","фермерство"],["fascinating","увлекательно"],["fashion","мода"],["fashionable","мода"],["fast","быстро"],["fasten","закрепить"],["fat","толстый"],["father","отец"],["fault","вина"],["favour","благосклонность"],["favourite","любимый"],["fear","страх"],["feather","перо"],["feature","особенность"],["february","февраль"],["fee","плата"],["feed","кормить"],["feedback","отзывы"],["feel","чувствовать себя"],["feeling","ощущение"],["fellow","коллега"],["female","женщина"],["fence","забор"],["festival","фестиваль"],["few","несколько"],["fiction","фантастика"],["field","поле"],["fifteen","пятнадцать"],["fifth","пятый"],["fifty","пятьдесят"],["fight","бой"],["fighting","бой"],["figure","фигура"],["file","файл"],["fill","заполнить"],["film","фильм"],["final","окончательный"],["finally","наконец"],["finance","финансы"],["financial","финансы"],["find","найти"],["finding","найти"],["fine","штраф"],["finger","палец"],["finish","закончить"],["fire","огонь"],["firm","твердый"],["first","сначала"],["firstly","в первую очередь"],["fish","рыба"],["fishing","рыбалка"],["fit","фитнес"],["fitness","фитнес"],["five","пять"],["fix","исправить"],["fixed","фиксированный"],["flag","флаг"],["flame","пламя"],["flash","вспышка"],["flat","плоский"],["flexible","гибкий"],["flight","полёт"],["float","плавать"],["flood","наводнение"],["floor","пол"],["flour","мука"],["flow","поток"],["flower","цветок"],["flu","грипп"],["fly","муха"],["flying","летать"],["focus","внимание"],["fold","складывать"],["folding","складывание"],["folk","народный"],["follow","следовать"],["following","следовать"],["food","еда"],["foot","нога"],["football","футбол"],["for","для"],["force","сила"],["foreign","иностранный"],["forest","лес"],["forever","навсегда"],["forget","забыть"],["forgive","простить"],["fork","вилка"],["form","форма"],["formal","формальный"],["former","бывший"],["fortunately","к счастью"],["fortune","судьба"],["forty","сорок"],["forward","вперед"],["found","найден"],["four","четыре"],["fourteen","четырнадцать"],["fourth","четвертый"],["frame","кадр"],["free","свобода"],["freedom","свобода"],["freeze","заморозка"],["frequency","частота"],["frequently","часто"],["fresh","свежий"],["friday","пятница"],["fridge","холодильник"],["friend","друг"],["friendly","дружеский"],["friendship","дружба"],["frighten","испугаться"],["frightened","испуганный"],["frightening","испуг"],["frog","лягушка"],["from","с сайта"],["front","перед"],["frozen","замороженный"],["fruit","фрукт"],["fry","жарить"],["fuel","топливо"],["full","полный"],["fully","полностью"],["fun","веселье"],["function","функция"],["fund","фонд"],["fundamental","фундаментальный"],["funding","финансирование"],["funny","смешно"],["fur","мех"],["furniture","мебель"],["further","далее"],["furthermore","далее"],["future","будущее"],["gain","прибыль"],["gallery","галерея"],["game","игра"],["gang","банда"],["gap","пробел"],["garage","гараж"],["garden","сад"],["gas","газ"],["gate","ворота"],["gather","собрать"],["general","общее"],["generally","в целом"],["generate","генерировать"],["generation","поколение"],["generous","щедрый"],["genre","жанр"],["gentle","нежный"],["gentleman","джентльмен"],["geography","география"],["get","получить"],["ghost","призрак"],["giant","гигант"],["gift","подарок"],["girl","девушка"],["girlfriend","девушка"],["give","подарить"],["glad","радость"],["glass","стекло"],["global","мир"],["glove","перчатка"],["go","идти"],["goal","цель"],["god","бог"],["gold","золото"],["golf","гольф"],["good","хорошо"],["goodbye","прощай"],["goods","товары"],["govern","управлять"],["government","правительство"],["grab","хватать"],["grade","оценка"],["gradually","постепенно"],["graduate","выпускник"],["grain","зерно"],["grand","гранд"],["grandfather","дедушка"],["grandmother","бабушка"],["grandparent","дедушка и бабушка"],["grant","грант"],["grass","трава"],["grateful","благодарность"],["great","великий"],["green","зелёный"],["greet","приветствовать"],["grey","серый"],["ground","земля"],["group","группа"],["grow","расти"],["growth","рост"],["guarantee","гарантия"],["guard","охрана"],["guess","угадать"],["guest","гость"],["guide","гид"],["guilty","виновный"],["guitar","гитара"],["gun","пистолет"],["guy","парень"],["gym","спортзал"],["habit","привычка"],["hair","волосы"],["half","половина"],["hall","зал"],["hand","рука"],["handle","ручка"],["hang","повесить"],["happen","случиться"],["happily","счастливо"],["happiness","счастье"],["happy","счастье"],["hard","трудно"],["hardly","вряд ли"],["harm","вред"],["harmful","вредный"],["hat","шляпа"],["hate","ненавидеть"],["have","иметь"],["have to","вынужден"],["he","он"],["head","голова"],["headache","головная боль"],["headline","заголовок"],["health","здоровье"],["healthy","здоровье"],["hear","слышать"],["hearing","слух"],["heart","сердце"],["heat","тепло"],["heating","отопление"],["heaven","небо"],["heavily","сильно"],["heavy","тяжелый"],["heel","каблук"],["height","высота"],["helicopter","вертолет"],["hell","ад"],["hello","привет"],["help","помощь"],["helpful","помощь"],["her","она"],["here","здесь"],["hero","герой"],["hers","ее"],["herself","сама"],["hesitate","колебаться"],["hey","привет"],["hi","привет"],["hide","скрыть"],["high","высоко"],["highlight","выделить"],["highly","очень"],["hill","холм"],["him","он"],["himself","сам"],["hire","нанять"],["his","его"],["historic","исторический"],["historical","исторический"],["history","история"],["hit","хит"],["hobby","хобби"],["hockey","хоккей"],["hold","держать"],["hole","отверстие"],["holiday","праздник"],["hollow","дупло"],["holy","святой"],["home","дом"],["homework","домашнее задание"],["honest","честный"],["honour","честь"],["hope","надежда"],["horrible","ужас"],["horror","ужас"],["horse","лошадь"],["hospital","больница"],["host","хозяин"],["hot","горячий"],["hotel","отель"],["hour","час"],["house","дом"],["household","дом"],["housing","жильё"],["how","как"],["however","однако"],["huge","огромный"],["human","человек"],["humorous","юмористический"],["humour","юмор"],["hundred","сто"],["hungry","голодный"],["hunt","охота"],["hunting","охота"],["hurricane","ураган"],["hurry","спешить"],["hurt","боль"],["husband","муж"],["i","i"],["ice","лёд"],["ice cream","мороженое"],["idea","идея"],["ideal","идеал"],["identify","идентифицировать"],["identity","идентичность"],["if","если"],["ignore","игнорировать"],["ill","болезнь"],["illegal","незаконно"],["illness","болезнь"],["illustrate","иллюстрация"],["illustration","иллюстрация"],["image","изображение"],["imaginary","воображение"],["imagination","воображение"],["imagine","представить"],["immediate","немедленно"],["immediately","немедленно"],["immigrant","иммигрант"],["impact","влияние"],["impatient","нетерпеливый"],["imply","подразумевать"],["import","импорт"],["importance","важность"],["important","важный"],["impose","навязывать"],["impossible","невозможно"],["impress","произвести впечатление"],["impressed","впечатлен"],["impression","впечатление"],["impressive","впечатляющий"],["improve","улучшить"],["improvement","улучшение"],["in","в"],["inch","дюйм"],["incident","инцидент"],["include","включить"],["included","включено"],["including","включая"],["income","доход"],["increase","увеличиваться"],["increasingly","все больше"],["incredible","невероятно"],["incredibly","невероятно"],["indeed","действительно"],["independent","независимый"],["indicate","указывать"],["indirect","косвенный"],["individual","отдельный"],["indoor","в помещении"],["indoors","в помещении"],["industrial","промышленный"],["industry","промышленность"],["infection","инфекция"],["influence","влияние"],["inform","информировать"],["informal","неформальная"],["information","информация"],["ingredient","ингредиент"],["initial","первоначально"],["initially","первоначально"],["initiative","инициатива"],["injure","травма"],["injured","травма"],["injury","травма"],["inner","внутренний"],["innocent","невиновный"],["insect","насекомое"],["inside","внутри"],["insight","проницательность"],["insist","настаивать"],["inspire","вдохновлять"],["install","установить"],["instance","экземпляр"],["instead","вместо"],["institute","институт"],["institution","институт"],["instruction","инструкция"],["instructor","инструктор"],["instrument","инструмент"],["insurance","страхование"],["intelligence","разведка"],["intelligent","интеллект"],["intend","намереваться"],["intended","намерение"],["intense","интенсивный"],["intention","намерение"],["interest","интерес"],["interested","интерес"],["interesting","интересный"],["internal","внутренний"],["international","международный"],["internet","интернет"],["interpret","интерпретировать"],["interrupt","прервать"],["interview","интервью"],["into","в"],["introduce","введение"],["introduction","введение"],["invent","изобретать"],["invention","изобретение"],["invest","инвестировать"],["investigate","расследовать"],["investigation","расследование"],["investment","инвестиция"],["invitation","приглашение"],["invite","приглашение"],["involve","вовлекать"],["involved","вовлечённый"],["iron","железо"],["island","остров"],["issue","выпуск"],["it","это"],["item","пункт"],["its","его"],["itself","сам"],["jacket","куртка"],["jam","варенье"],["january","январь"],["jazz","джаз"],["jeans","джинсы"],["jewellery","ювелирные изделия"],["job","работа"],["join","присоединиться"],["joke","шутка"],["journal","журнал"],["journalist","журналист"],["journey","путешествие"],["joy","радость"],["judge","судья"],["judgement","суждение"],["juice","сок"],["july","июль"],["jump","прыжок"],["june","июнь"],["junior","младший"],["just","просто"],["justice","справедливость"],["justify","оправдать"],["keen","увлечься"],["keep","держать"],["key","ключ"],["keyboard","клавиатура"],["kick","пнуть"],["kid","ребёнок"],["kill","убить"],["killing","убийство"],["kilometre","километр"],["kind","добрый"],["king","король"],["kiss","поцелуй"],["kitchen","кухня"],["knee","колено"],["knife","нож"],["knock","стучать"],["know","знать"],["knowledge","знание"],["lab","лаборатория"],["label","этикетка"],["laboratory","лаборатория"],["labour","труд"],["lack","отсутствие"],["lady","леди"],["lake","озеро"],["lamp","лампа"],["land","земля"],["landscape","пейзаж"],["language","язык"],["laptop","ноутбук"],["large","большой"],["largely","в основном"],["last","последний"],["late","поздно"],["later","позже"],["latest","последний"],["laugh","смеяться"],["laughter","смех"],["launch","запуск"],["law","закон"],["lawyer","адвокат"],["lay","укладывать"],["layer","слой"],["lazy","ленивый"],["lead","вести"],["leader","лидер"],["leadership","лидерство"],["leading","лидерство"],["leaf","лист"],["league","лига"],["lean","бережливый"],["learn","учиться"],["learning","обучение"],["least","меньше всего"],["leather","кожа"],["leave","оставить"],["lecture","лекция"],["left","левый"],["leg","нога"],["legal","юридический"],["leisure","отдых"],["lemon","лимон"],["lend","одолжить"],["length","длина"],["less","меньше"],["lesson","урок"],["let","пусть"],["letter","буква"],["level","уровень"],["library","библиотека"],["licence","лицензия"],["lie","ЛОЖЬ"],["life","жизнь"],["lifestyle","образ жизни"],["lift","лифт"],["light","свет"],["like","как"],["likely","возможно"],["limit","ограничить"],["limited","ограниченный"],["line","линия"],["link","ссылка"],["lion","лев"],["lip","губа"],["liquid","жидкость"],["list","список"],["listen","слушать"],["listener","слушатель"],["literature","литература"],["little","маленький"],["live","жить"],["lively","живой"],["living","жизнь"],["load","груз"],["loan","кредит"],["local","местный"],["locate","местонахождение"],["located","расположенный"],["location","местоположение"],["lock","замок"],["logical","логический"],["lonely","одинокий"],["long","долго"],["long-term","долгосрочный"],["look","смотреть"],["loose","свободный"],["lord","лорд"],["lorry","грузовик"],["lose","потерять"],["loss","потеря"],["lost","потеря"],["lot","лот"],["loud","громко"],["loudly","громко"],["love","любовь"],["lovely","прекрасный"],["low","низкий"],["lower","ниже"],["luck","удача"],["lucky","удача"],["lunch","обед"],["lung","легкое"],["luxury","роскошь"],["machine","машина"],["mad","сумасшедший"],["magazine","журнал"],["magic","магия"],["mail","почта"],["main","главная"],["mainly","в основном"],["maintain","поддерживать"],["major","основной"],["majority","большинство"],["make","делать"],["male","мужчина"],["mall","торговый центр"],["man","мужчина"],["manage","управлять"],["management","управление"],["manager","менеджер"],["manner","манера"],["many","многие"],["map","карта"],["march","март"],["mark","отметить"],["market","рынок"],["marketing","маркетинг"],["marriage","брак"],["married","жениться"],["marry","жениться"],["mass","масса"],["massive","массовый"],["master","хозяин"],["match","совпадение"],["matching","соответствие"],["material","материал"],["mathematics","математика"],["maths","математика"],["matter","материя"],["maximum","максимум"],["may","май"],["maybe","может быть"],["me","я"],["meal","еда"],["mean","значит"],["meaning","значение"],["means","означает"],["meanwhile","между тем"],["measure","измерять"],["measurement","измерение"],["meat","мясо"],["media","СМИ"],["medical","медицинский"],["medicine","медицина"],["medium","среда"],["meet","встреча"],["meeting","встреча"],["melt","расплавить"],["member","член"],["memory","память"],["mental","умственный"],["mention","упоминание"],["menu","меню"],["mess","сообщение"],["message","сообщение"],["metal","металл"],["method","метод"],["metre","метр"],["middle","середина"],["midnight","полночь"],["might","может"],["mild","миля"],["mile","миля"],["military","военный"],["milk","молоко"],["million","миллион"],["mind","ум"],["mine","шахта"],["mineral","минерал"],["minimum","минимум"],["minister","министр"],["minor","меньшинство"],["minority","меньшинство"],["minute","минута"],["mirror","зеркало"],["miss","мисс"],["missing","пропавший"],["mission","миссия"],["mistake","ошибка"],["mix","смешать"],["mixed","смесь"],["mixture","смесь"],["mobile","мобильный"],["model","модель"],["modern","современный"],["modify","модифицировать"],["moment","момент"],["monday","понедельник"],["money","деньги"],["monitor","монитор"],["monkey","обезьяна"],["month","месяц"],["mood","настроение"],["moon","луна"],["moral","мораль"],["more","больше"],["morning","утро"],["most","большинство"],["mostly","в основном"],["mother","мать"],["motor","мотоцикл"],["motorcycle","мотоцикл"],["mount","гора"],["mountain","гора"],["mouse","мышь"],["mouth","рот"],["move","движение"],["movement","движение"],["movie","фильм"],["much","много"],["mud","грязь"],["multiple","несколько"],["multiply","умножить"],["mum","мама"],["murder","убийство"],["muscle","мышца"],["museum","музей"],["music","музыка"],["musical","мюзикл"],["musician","музыкант"],["must","обязательно"],["my","мой"],["myself","сам"],["mysterious","таинственный"],["mystery","тайна"],["nail","ноготь"],["name","имя"],["narrative","повествование"],["narrow","узкий"],["nation","нация"],["national","национальный"],["native","родной"],["natural","естественный"],["naturally","естественно"],["nature","природа"],["near","рядом"],["nearly","почти"],["neat","аккуратно"],["necessarily","обязательно"],["necessary","необходимо"],["neck","шея"],["need","нужно"],["needle","игла"],["negative","негатив"],["neighbour","сосед"],["neighbourhood","соседство"],["neither","ни"],["nerve","нерв"],["nervous","нерв"],["net","сеть"],["network","сеть"],["never","никогда"],["nevertheless","тем не менее"],["new","новый"],["news","новости"],["newspaper","газета"],["next","следующий"],["next to","рядом"],["nice","хороший"],["night","ночь"],["nightmare","кошмар"],["nine","девять"],["nineteen","девятнадцать"],["ninety","девяносто"],["no","нет"],["no one","никто"],["nobody","никто"],["noise","шум"],["noisy","шумный"],["none","никто"],["nor","ни"],["normal","нормально"],["normally","обычно"],["north","север"],["northern","север"],["nose","нос"],["not","не"],["note","заметка"],["nothing","ничего"],["notice","заметить"],["notion","понятие"],["novel","роман"],["november","ноябрь"],["now","сейчас"],["nowhere","нигде"],["nuclear","ядерный"],["number","номер"],["numerous","множество"],["nurse","медсестра"],["nut","орех"],["o'clock","часы"],["obey","слушаться"],["object","объект"],["objective","цель"],["obligation","обязательство"],["observation","наблюдение"],["observe","наблюдать"],["obtain","получить"],["obvious","очевидно"],["obviously","очевидно"],["occasion","случай"],["occasionally","время от времени"],["occur","происходить"],["ocean","океан"],["october","октябрь"],["odd","странный"],["of","из"],["off","от"],["offence","оскорбление"],["offend","обидеть"],["offensive","оскорбление"],["offer","предлагать"],["office","офис"],["officer","офицер"],["official","чиновник"],["often","часто"],["oh","о"],["oil","нефть"],["ok","ок"],["old","старый"],["old-fashioned","старомодный"],["on","на"],["once","однажды"],["one","один"],["onion","лук"],["online","онлайн"],["only","только"],["onto","на"],["open","открыть"],["opening","открытие"],["operate","работать"],["operation","операция"],["opinion","мнение"],["opponent","противник"],["opportunity","возможность"],["oppose","противостоять"],["opposed","противоположный"],["opposite","противоположность"],["opposition","оппозиция"],["option","вариант"],["or","или"],["orange","оранжевый"],["order","заказ"],["ordinary","обычный"],["organ","орган"],["organization","организация"],["organize","организовать"],["organized","организованный"],["organizer","организатор"],["origin","происхождение"],["original","оригинал"],["originally","первоначально"],["other","другой"],["otherwise","иначе"],["ought","должен"],["our","наш"],["ours","наш"],["ourselves","сами"],["out","из"],["outcome","результат"],["outdoor","на открытом воздухе"],["outdoors","на открытом воздухе"],["outer","внешний"],["outline","набросок"],["outside","снаружи"],["oven","печь"],["over","над"],["overall","общий"],["owe","задолжать"],["own","собственный"],["owner","владелец"],["pace","темп"],["pack","упаковать"],["package","пакет"],["page","страница"],["pain","боль"],["painful","болезненный"],["paint","краска"],["painter","художник"],["painting","картина"],["pair","пара"],["palace","дворец"],["pale","бледный"],["pan","пан"],["panel","панель"],["pants","брюки"],["paper","бумага"],["paragraph","параграф"],["parent","родитель"],["park","парк"],["parking","парковка"],["parliament","парламент"],["part","часть"],["participant","участник"],["participate","участвовать"],["particular","частности"],["particularly","особенно"],["partly","частично"],["partner","партнер"],["party","вечеринка"],["pass","проход"],["passage","проход"],["passenger","пассажир"],["passion","страсть"],["passport","паспорт"],["past","прошлое"],["path","путь"],["patient","пациент"],["pattern","схема"],["pay","оплатить"],["payment","оплата"],["peace","мир"],["peaceful","мирный"],["pen","ручка"],["pencil","карандаш"],["penny","пенни"],["pension","пенсия"],["people","люди"],["pepper","перец"],["per","на"],["per cent","процент"],["percentage","процент"],["perfect","идеально"],["perfectly","идеально"],["perform","выполнить"],["performance","производительность"],["perhaps","возможно"],["period","период"],["permanent","постоянный"],["permission","разрешение"],["permit","разрешение"],["person","человек"],["personal","личность"],["personality","личность"],["personally","лично"],["perspective","перспектива"],["persuade","убедить"],["pet","домашнее животное"],["petrol","бензин"],["phase","фаза"],["phenomenon","феномен"],["philosophy","философия"],["phone","телефон"],["photo","фотография"],["photograph","фотография"],["photographer","фотограф"],["photography","фотография"],["phrase","фраза"],["physical","физика"],["physics","физика"],["piano","фортепиано"],["pick","выбрать"],["picture","картинка"],["piece","кусок"],["pig","свинья"],["pile","куча"],["pilot","пилот"],["pin","булавка"],["pink","розовый"],["pipe","труба"],["pitch","шаг"],["place","место"],["plain","простой"],["plan","план"],["plane","плоскость"],["planet","планета"],["planning","планирование"],["plant","растение"],["plastic","пластик"],["plate","пластина"],["platform","платформа"],["play","играть"],["player","плеер"],["pleasant","приятный"],["please","пожалуйста"],["pleased","доволен"],["pleasure","удовольствие"],["plenty","много"],["plot","сюжет"],["plus","плюс"],["pocket","карман"],["poem","поэма"],["poet","поэт"],["poetry","стихи"],["point","точка"],["pointed","острый"],["poison","яд"],["poisonous","ядовитый"],["police","полиция"],["policeman","полицейский"],["policy","политика"],["polite","вежливый"],["political","политика"],["politician","политик"],["politics","политика"],["pollution","загрязнение"],["pool","бассейн"],["poor","бедные"],["pop","поп"],["popular","популярность"],["popularity","популярность"],["population","население"],["port","порт"],["portrait","портрет"],["pose","поза"],["position","позиция"],["positive","положительный"],["possess","обладать"],["possession","обладание"],["possibility","возможность"],["possible","возможно"],["possibly","возможно"],["post","пост"],["poster","плакат"],["pot","горшок"],["potato","картофель"],["potential","потенциал"],["pound","фунт"],["pour","наливать"],["poverty","бедность"],["powder","порошок"],["power","сила"],["powerful","мощный"],["practical","практический"],["practice","практика"],["practise","практиковать"],["praise","хвалить"],["pray","молиться"],["prayer","молитва"],["predict","предсказание"],["prediction","предсказание"],["prefer","предпочесть"],["pregnant","беременная"],["preparation","подготовка"],["prepare","подготовка"],["prepared","подготовленный"],["presence","присутствие"],["present","присутствовать"],["presentation","презентация"],["preserve","сохранить"],["president","президент"],["press","пресса"],["pressure","давление"],["pretend","притвориться"],["pretty","красивый"],["prevent","предотвратить"],["previous","ранее"],["previously","ранее"],["price","цена"],["priest","священник"],["primary","основной"],["prime","прайм"],["prince","принц"],["princess","принцесса"],["principle","принцип"],["print","печать"],["printer","принтер"],["printing","печать"],["priority","приоритет"],["prison","тюрьма"],["prisoner","заключенный"],["privacy","конфиденциальность"],["private","частная"],["prize","приз"],["probably","возможно"],["problem","проблема"],["procedure","процедура"],["process","процесс"],["produce","производить"],["producer","производитель"],["product","продукт"],["production","производство"],["profession","профессия"],["professional","профессионал"],["professor","профессор"],["profile","профиль"],["profit","прибыль"],["program","программа"],["programme","программа"],["progress","прогресс"],["project","проект"],["promise","обещание"],["promote","продвигать"],["pronounce","произносить"],["proof","доказывать"],["proper","правильно"],["properly","должным образом"],["property","собственность"],["proposal","предложение"],["propose","предложение"],["prospect","перспектива"],["protect","защита"],["protection","защита"],["protest","протест"],["proud","гордиться"],["prove","доказать"],["provide","предоставить"],["psychologist","психолог"],["psychology","психология"],["pub","паб"],["public","публика"],["publication","публикация"],["publish","опубликовать"],["pull","тянуть"],["punish","наказать"],["punishment","наказание"],["pupil","ученик"],["purchase","купить"],["pure","чистый"],["purple","фиолетовый"],["purpose","цель"],["pursue","преследовать"],["push","толкать"],["put","ставить"],["qualification","квалификация"],["qualified","квалифицированный"],["qualify","квалифицировать"],["reply","ответ"],["report","отчёт"],["reporter","докладчик"],["represent","представлять"],["representative","представитель"],["reputation","репутация"],["request","запрос"],["require","требовать"],["requirement","требование"],["rescue","спасение"],["research","исследование"],["researcher","исследователь"],["reservation","резервирование"],["reserve","резерв"],["resident","резидент"],["resist","сопротивляться"],["resolve","разрешить"],["resort","курорт"],["resource","ресурс"],["respect","уважение"],["respond","реагировать"],["response","ответ"],["responsibility","ответственность"],["responsible","ответственный"],["rest","отдых"],["restaurant","ресторан"],["result","результат"],["retain","сохранять"],["retire","выйти на пенсию"],["retired","на пенсии"],["return","вернуться"],["reveal","раскрыть"],["review","пересмотреть"],["revise","пересмотреть"],["revolution","революция"],["reward","награда"],["rhythm","ритм"],["rice","рис"],["rich","богатый"],["rid","ехать"],["ride","ехать"],["right","правый"],["ring","кольцо"],["rise","подняться"],["risk","риск"],["river","река"],["road","дорога"],["robot","робот"],["rock","скала"],["role","роль"],["roll","ролл"],["romantic","романтик"],["roof","крыша"],["room","комната"],["root","корень"],["rope","канат"],["rough","грубый"],["round","круглый"],["route","маршрут"],["routine","рутина"],["row","грести"],["royal","королевский"],["rub","тереть"],["rubber","резина"],["rubbish","мусор"],["rude","грубый"],["rugby","регби"],["rule","правило"],["run","бежать"],["runner","бегун"],["running","бег"],["rural","сельская местность"],["rush","спешить"],["sad","грустно"],["sadly","печально"],["safe","безопасность"],["safety","безопасность"],["sail","парус"],["sailing","плавание"],["sailor","моряк"],["salad","салат"],["salary","зарплата"],["sale","продажа"],["salt","соль"],["same","тот же"],["sample","образец"],["sand","песок"],["sandwich","сэндвич"],["satellite","спутник"],["satisfied","удовлетворен"],["satisfy","удовлетворить"],["saturday","суббота"],["sauce","соус"],["save","сохранить"],["saving","экономия"],["say","сказать"],["scale","шкала"],["scan","сканировать"],["scared","страшно"],["scary","страшный"],["scene","сцена"],["schedule","расписание"],["scheme","схема"],["school","школа"],["science","наука"],["scientific","научный"],["scientist","учёный"],["score","оценка"],["scream","крик"],["screen","экран"],["script","сценарий"],["sculpture","скульптура"],["sea","море"],["search","поиск"],["season","сезон"],["seat","место"],["second","второй"],["secondary","вторично"],["secondly","вторично"],["secret","секрет"],["secretary","секретарь"],["section","сектор"],["sector","сектор"],["secure","охрана"],["security","безопасность"],["see","см."],["seed","семя"],["seek","искать"],["seem","кажется"],["select","выбрать"],["selection","выбор"],["self","себя"],["sell","продать"],["send","отправить"],["senior","старший"],["sense","смысл"],["sensible","чувствительный"],["sensitive","чувствительный"],["sentence","предложение"],["separate","отдельный"],["september","сентябрь"],["sequence","последовательность"],["series","серия"],["serious","серьезно"],["seriously","серьезно"],["servant","слуга"],["serve","служить"],["service","служение"],["session","сессия"],["set","установить"],["setting","установка"],["settle","уладить"],["seven","семь"],["seventeen","семнадцать"],["seventy","семьдесят"],["several","несколько"],["severe","суровый"],["sex","секс"],["sexual","секс"],["shade","тень"],["shadow","тень"],["shake","трясти"],["shall","должен"],["shallow","мелкий"],["shame","стыд"],["shape","форма"],["share","поделиться"],["sharp","острый"],["she","она"],["sheep","овца"],["sheet","лист"],["shelf","полка"],["shell","раковина"],["shelter","убежище"],["shift","смена"],["shine","блеск"],["shiny","блеск"],["ship","корабль"],["shirt","рубашка"],["shock","шок"],["shocked","шокирован"],["shoe","ботинок"],["shoot","стрелять"],["shooting","стрельба"],["shop","магазин"],["shopping","магазин"],["short","короткий"],["shot","выстрел"],["should","следует"],["shoulder","плечо"],["shout","кричать"],["show","показать"],["shower","душ"],["shut","закрывать"],["shy","застенчивый"],["sick","больной"],["side","сторона"],["sight","зрение"],["sign","знак"],["signal","сигнал"],["significant","значительный"],["significantly","значительно"],["silence","тишина"],["silent","молчание"],["silk","шелк"],["silly","глупый"],["silver","серебро"],["similar","похожее"],["similarity","сходство"],["similarly","аналогично"],["simple","просто"],["simply","просто"],["since","так как"],["sincere","искренний"],["sing","петь"],["singer","певец"],["singing","петь"],["single","одинокий"],["sink","раковина"],["sir","сэр"],["sister","сестра"],["sit","сидеть"],["site","сайт"],["situation","ситуация"],["six","шесть"],["sixteen","шестнадцать"],["sixty","шестьдесят"],["size","размер"],["ski","лыжи"],["skiing","катание на лыжах"],["skill","навык"],["skin","кожа"],["skirt","юбка"],["sky","небо"],["slave","раб"],["sleep","сон"],["slice","ломтик"],["slide","слайд"],["slight","немного"],["slightly","немного"],["slip","скользить"],["slope","наклон"],["slow","медленно"],["slowly","медленно"],["small","маленький"],["smart","умный"],["smell","запах"],["smile","улыбка"],["smoke","дым"],["smoking","курение"],["smooth","гладкий"],["snake","змея"],["snow","снег"],["so","так"],["soap","мыло"],["soccer","футбол"],["social","общество"],["society","общество"],["sock","носок"],["soft","мягкий"],["software","программное обеспечение"],["soil","почва"],["solar","солнце"],["soldier","солдат"],["solid","твёрдый"],["solution","решение"],["solve","решить"],["some","некоторые"],["somebody","кто-то"],["someone","кто-то"],["something","что-то"],["sometimes","иногда"],["somewhat","несколько"],["somewhere","где-то"],["son","сын"],["song","песня"],["soon","скоро"],["sorry","простите"],["sort","сортировать"],["soul","душа"],["sound","звук"],["soup","суп"],["source","источник"],["south","юг"],["southern","юг"],["space","космос"],["speak","говорить"],["speaker","спикер"],["special","специальный"],["specialist","специалист"],["species","вид"],["specific","особый"],["specifically","специально"],["speech","речь"],["speed","скорость"],["spell","правописание"],["spelling","правописание"],["spend","тратить"],["spending","тратить"],["spicy","острый"],["spider","паук"],["spirit","дух"],["spiritual","спиритический"],["split","раскол"],["spoken","произнесенное"],["sponsor","спонсор"],["spoon","ложка"],["sport","спорт"],["spot","место"],["spread","распространение"],["spring","весна"],["square","квадрат"],["stable","стабильный"],["stadium","стадион"],["staff","персонал"],["stage","сцена"],["stair","лестница"],["stamp","печать"],["stand","трибуна"],["standard","стандарт"],["star","звезда"],["stare","смотреть"],["start","начать"],["state","состояние"],["statement","заявление"],["station","станция"],["statistic","статистика"],["statue","статуя"],["status","состояние"],["stay","оставаться"],["steady","постоянный"],["steal","украсть"],["steel","сталь"],["steep","крутой"],["step","шаг"],["stick","палка"],["sticky","липкий"],["stiff","жёсткий"],["still","всё ещё"],["stock","запас"],["stomach","желудок"],["stone","камень"],["stop","остановиться"],["store","магазин"],["storm","шторм"],["story","история"],["straight","прямо"],["strange","странный"],["stranger","незнакомец"],["strategy","стратегия"],["stream","стрим"],["street","улица"],["strength","сила"],["stress","стресс"],["stretch","растягивать"],["strict","строгий"],["strike","удар"],["string","строка"],["strong","сильный"],["strongly","сильно"],["structure","структура"],["struggle","борьба"],["student","студент"],["studio","студия"],["study","учиться"],["stuff","вещи"],["stupid","глупый"],["style","стиль"],["subject","тема"],["sublist","подсписок"],["submit","отправить"],["substance","содержание"],["succeed","преуспеть"],["success","успех"],["successful","успешный"],["successfully","успешно"],["such","такой"],["sudden","внезапно"],["suddenly","внезапно"],["suffer","страдать"],["sugar","сахар"],["suggest","предлагать"],["suggestion","предложение"],["suit","подходить"],["suitable","подходящий"],["sum","суммировать"],["summarize","подводить итоги"],["summary","резюме"],["summer","лето"],["sun","солнце"],["sunday","воскресенье"],["supermarket","супермаркет"],["supply","поставка"],["support","поддержка"],["supporter","сторонник"],["suppose","предположить"],["sure","конечно"],["surely","конечно"],["surface","поверхность"],["surgery","операция"],["surprise","удивление"],["surprised","удивлен"],["surprising","удивительно"],["surround","окружать"],["surrounding","окружение"],["survey","опрос"],["survive","выжить"],["suspect","подозревать"],["swear","клясться"],["sweater","свитер"],["sweep","подметать"],["sweet","сладкий"],["swim","плавать"],["swimming","плавание"],["switch","переключатель"],["symbol","символ"],["sympathy","симпатия"],["symptom","симптом"],["system","система"],["t-shirt","футболка"],["table","стол"],["tablet","таблетка"],["tail","хвост"],["take","взять"],["tale","сказка"],["talent","талант"],["talented","талантливый"],["talk","говорить"],["tall","высокий"],["tank","танк"],["tape","лента"],["target","цель"],["task","задача"],["taste","вкус"],["tax","налог"],["taxi","такси"],["tea","чай"],["teach","преподавать"],["teacher","учитель"],["teaching","преподавание"],["team","команда"],["tear","разрыв"],["technical","техника"],["technique","техника"],["technology","технология"],["teenage","подросток"],["teenager","подросток"],["telephone","телефон"],["television","телевидение"],["tell","рассказать"],["temperature","температура"],["temporary","временный"],["ten","десять"],["tend","тенденция"],["tennis","теннис"],["tent","палатка"],["term","срок"],["terrible","ужасный"],["test","тест"],["text","текст"],["than","чем"],["thank","спасибо"],["thanks","спасибо"],["that","это"],["the","сайт"],["theatre","театр"],["their","их"],["theirs","их"],["them","они"],["theme","тема"],["themselves","сами"],["then","затем"],["theory","теория"],["therapy","терапия"],["there","там"],["therefore","поэтому"],["they","они"],["thick","толстый"],["thief","вор"],["thin","тонкий"],["thing","вещь"],["think","думать"],["thinking","думать"],["third","третий"],["thirsty","жажда"],["thirteen","тринадцать"],["thirty","тридцать"],["this","это"],["though","хотя"],["thought","думал"],["thousand","тысяча"],["threat","угроза"],["threaten","угроза"],["three","три"],["throat","горло"],["through","через"],["throughout","на протяжении"],["throw","бросок"],["thursday","четверг"],["thus","таким образом"],["ticket","билет"],["tidy","привести в порядок"],["tie","галстук"],["tight","туго"],["till","до"],["time","время"],["tin","жесть"],["tiny","маленький"],["tip","наконечник"],["tired","усталый"],["title","название"],["to","на"],["today","сегодня"],["toe","носок"],["together","вместе"],["toilet","туалет"],["tomato","помидор"],["tomorrow","завтра"],["tone","тон"],["tongue","язык"],["tonight","сегодня"],["too","слишком"],["tool","инструмент"],["tooth","зуб"],["top","верх"],["topic","тема"],["total","полностью"],["totally","полностью"],["touch","касаться"],["tough","жесткий"],["tour","тур"],["tourism","туризм"],["tourist","турист"],["towards","к"],["towel","полотенце"],["tower","башня"],["town","город"],["toy","игрушка"],["track","трек"],["trade","торговля"],["tradition","традиция"],["traditional","традиционный"],["traffic","движение"],["train","поезд"],["trainer","тренер"],["training","обучение"],["transfer","трансфер"],["transform","преобразование"],["transition","переход"],["translate","перевести"],["translation","перевод"],["transport","транспорт"],["travel","путешествие"],["traveller","путешественник"],["treat","лечить"],["treatment","лечение"],["tree","дерево"],["trend","тенденция"],["trial","испытание"],["trick","трюк"],["trip","путешествие"],["tropical","тропический"],["trouble","неприятности"],["trousers","брюки"],["truck","грузовик"],["TRUE","ИСТИННЫЙ"],["truly","правда"],["trust","доверие"],["truth","правда"],["try","попробовать"],["tube","трубка"],["tuesday","вторник"],["tune","настроить"],["tunnel","туннель"],["turn","повернуть"],["tv","телевизор"],["twelve","двенадцать"],["twenty","двадцать"],["twice","дважды"],["twin","близнец"],["two","два"],["type","тип"],["typical","типичный"],["typically","обычно"],["tyre","шина"],["ugly","уродливый"],["ultimately","в конечном итоге"],["umbrella","зонтик"],["unable","неспособный"],["uncle","дядя"],["uncomfortable","неудобно"],["unconscious","бессознательное"],["under","под"],["underground","под землей"],["understand","понять"],["understanding","понимание"],["underwear","нижнее белье"],["unemployed","безработный"],["unemployment","безработица"],["unexpected","неожиданность"],["unfair","несправедливость"],["unfortunately","к сожалению"],["unhappy","несчастный"],["uniform","униформа"],["union","профсоюз"],["unique","уникальный"],["unit","единица"],["united","единый"],["universe","вселенная"],["university","университет"],["unknown","неизвестный"],["unless","если только"],["unlike","в отличие от"],["unlikely","маловероятно"],["unnecessary","ненужный"],["unpleasant","неприятный"],["until","пока"],["unusual","необычный"],["up","вверх"],["update","обновить"],["upon","на"],["upper","верхний"],["upset","расстроенный"],["upstairs","вверх"],["upwards","вверх"],["urban","город"],["urge","стремление"],["us","мы"],["use","использовать"],["used","использовать"],["used to","использованный для"],["useful","полезно"],["user","пользователь"],["usual","обычно"],["usually","обычно"],["vacation","отпуск"],["valley","долина"],["valuable","ценный"],["value","ценность"],["van","ван"],["variety","разнообразие"],["various","разнообразный"],["vary","варьироваться"],["vast","большой"],["vegetable","овощ"],["vehicle","автомобиль"],["venue","место проведения"],["version","версия"],["very","очень"],["via","через"],["week","неделя"],["weekend","выходные"],["weigh","взвеситься"],["weight","вес"],["welcome","добро пожаловать"],["well","хорошо"],["west","запад"],["western","запад"],["wet","мокрый"],["what","что"],["whatever","что угодно"],["wheel","колесо"],["when","когда"],["whenever","когда"],["where","где"],["whereas","тогда как"],["wherever","где бы"],["whether","ли"],["which","что"],["while","в то время как"],["whisper","шептать"],["white","белый"],["who","кто"],["whole","весь"],["whom","кто"],["whose","чей"],["why","почему"],["wide","широко"],["widely","широко"],["wife","жена"],["wild","дикая"],["wildlife","дикая природа"],["will","будет"],["willing","желающий"],["win","победа"],["wind","ветер"],["window","окно"],["wine","вино"],["wing","крыло"],["winner","победитель"],["winter","зима"],["wire","провод"],["wise","мудрый"],["wish","желание"],["with","с"],["within","внутри"],["without","без"],["witness","свидетель"],["woman","женщина"],["wonder","чудо"],["wonderful","чудесный"],["wood","дерево"],["wooden","дерево"],["wool","шерсть"],["word","слово"],["work","работа"],["worker","рабочий"],["working","работа"],["world","мир"],["worldwide","весь мир"],["worried","беспокойство"],["worry","беспокоиться"],["worse","хуже"],["worst","худший"],["worth","стоит"],["would","было бы"],["wound","рана"],["wow","вау"],["wrap","обернуть"],["write","написать"],["writer","писатель"],["writing","письмо"],["written","написано"],["wrong","неправильно"],["yard","двор"],["yeah","да"],["year","год"],["yellow","желтый"],["yes","да"],["yesterday","вчера"],["yet","пока"],["you","вы"],["young","молодой"],["your","твой"],["yours","твой"],["yourself","себя"],["youth","молодежь"],["zero","ноль"],["zone","зона"],["victim","жертва"],["victory","победа"],["video","видео"],["view","смотреть"],["viewer","зритель"],["village","деревня"],["violence","насилие"],["violent","насилие"],["virtual","виртуальный"],["virus","вирус"],["vision","видение"],["visit","посетить"],["visitor","посетитель"],["visual","визуальный"],["vital","жизненно важный"],["vitamin","витамин"],["voice","голос"],["volume","объем"],["volunteer","волонтер"],["vote","голосовать"],["wage","зарплата"],["wait","ждать"],["waiter","официант"],["wake","проснуться"],["walk","ходить"],["wall","стена"],["want","хотеть"],["war","война"],["warm","тепло"],["warn","предупредить"],["warning","предупреждение"],["wash","мыть"],["washing","стирка"],["waste","отходы"],["watch","смотреть"],["water","вода"],["wave","волна"],["way","путь"],["we","мы"],["weak","слабость"],["weakness","слабость"],["wealth","богатство"],["wealthy","богатство"],["weapon","оружие"],["wear","носить"],["weather","погода"],["web","сайт"],["website","сайт"],["wedding","свадьба"],["wednesday","среда"],["quality","качество"],["quantity","количество"],["quarter","квартал"],["queen","королева"],["question","вопрос"],["queue","очередь"],["quick","быстро"],["quickly","быстро"],["quiet","тихо"],["quietly","тихо"],["quit","уйти"],["quite","довольно"],["quotation","цитата"],["quote","цитата"],["race","гонка"],["racing","гонки"],["radio","радио"],["railway","железная дорога"],["rain","дождь"],["raise","поднимать"],["range","диапазон"],["rank","звание"],["rapid","быстро"],["rapidly","быстро"],["rare","редко"],["rarely","редко"],["rate","скорость"],["rather","довольно"],["raw","сырой"],["reach","достичь"],["react","реагировать"],["reaction","реакция"],["read","читать"],["reader","читатель"],["reading","чтение"],["ready","готовый"],["real","реальный"],["realistic","реалистичный"],["reality","реальность"],["realize","осознать"],["really","действительно"],["reason","разум"],["reasonable","разумный"],["recall","вспомнить"],["receipt","получение"],["receive","получить"],["recent","недавно"],["recently","недавно"],["reception","прием"],["recipe","рецепт"],["recognize","узнать"],["recommend","рекомендовать"],["recommendation","рекомендация"],["record","запись"],["recording","запись"],["recover","восстановить"],["recycle","перерабатывать"],["red","красный"],["reduce","сократить"],["reduction","сокращение"],["refer","ссылаться"],["reference","ссылка"],["reflect","отразить"],["refuse","отказаться"],["regard","рассматривать"],["region","регион"],["regional","регион"],["register","регистрировать"],["regret","сожалеть"],["regular","регулярно"],["regularly","регулярно"],["regulation","постановление"],["reject","отвергать"],["relate","относиться"],["related","связанный"],["relation","связь"],["relationship","отношение"],["relative","относительный"],["relatively","относительно"],["relax","расслабиться"],["relaxed","расслабленный"],["relaxing","расслабление"],["release","освобождение"],["relevant","актуально"],["reliable","надежный"],["relief","облегчение"],["religion","религия"],["religious","религия"],["rely","полагаться"],["remain","оставаться"],["remark","замечание"],["remember","помнить"],["remind","напоминать"],["remote","удаленный"],["remove","удалить"],["rent","аренда"],["repair","ремонт"],["repeat","повторить"],["repeated","повтор"],["replace","заменить"],["abolish","отменить"],["abortion","аборт"],["absence","отсутствие"],["absent","отсутствовать"],["absorb","поглотить"],["abstract","абстракция"],["absurd","абсурд"],["abundance","изобилие"],["abuse","злоупотреблять"],["academy","академия"],["accelerate","ускорить"],["accent","акцентировать"],["acceptance","акцепт"],["accessible","доступный"],["accidentally","случайно"],["accommodate","разместить"],["accomplish","свершение"],["accomplishment","свершение"],["accordance","в соответствии"],["accordingly","соответственно"],["accountability","подотчетность"],["accountable","подотчетный"],["accountant","бухгалтер"],["accounting","бухгалтерия"],["accumulate","накапливать"],["accumulation","накопление"],["accuracy","точность"],["accurately","точно"],["accusation","обвинение"],["accused","обвиняемый"],["acid","кислота"],["acquisition","приобретение"],["acre","акр"],["activate","активировать"],["activation","активация"],["activist","активист"],["acute","острый"],["adaptation","адаптация"],["addiction","зависимость"],["additionally","дополнительно"],["adequate","адекватно"],["adequately","адекватно"],["adhere","придерживаться"],["adjacent","прилегающий"],["adjust","регулировать"],["adjustment","регулировка"],["administer","администрировать"],["administrative","администратор"],["administrator","администратор"],["admission","допуск"],["adolescent","подросток"],["adoption","усыновление"],["adverse","неблагоприятный"],["advocate","защитник"],["aesthetic","эстетика"],["affection","привязанность"],["affordable","доступный"],["aftermath","последствия"],["aggression","агрессия"],["agricultural","сельское хозяйство"],["agriculture","сельское хозяйство"],["aide","помощь"],["aids","помощь"],["albeit","хотя"],["alert","предупреждение"],["alien","инопланетянин"],["align","выравнивать"],["alignment","выравнивание"],["alike","одинаковый"],["allegation","утверждение"],["allege","утверждать"],["allegedly","якобы"],["alliance","альянс"],["allocate","распределять"],["allocation","распределение"],["allowance","пособие"],["ally","союзник"],["alongside","рядом"],["altogether","в целом"],["aluminium","алюминий"],["amateur","любитель"],["ambassador","посол"],["ambulance","скорая помощь"],["amend","поправка"],["amendment","поправка"],["amid","среди"],["amusing","забавный"],["analogy","аналогия"],["analyst","аналитик"],["ancestor","предок"],["anchor","якорь"],["angel","ангел"],["animation","анимация"],["annually","ежегодно"],["anonymous","аноним"],["anticipate","предвидеть"],["anxiety","тревога"],["apology","извинение"],["apparatus","аппарат"],["appealing","аппетит"]];
const KEY = 'oxford3000_p1_v1';
const SPEECH = 'speechSynthesis' in window;
const LABEL = { new: 'Новое', known: 'Знаю', review: 'Повторить' };
const NEXT = { new: 'known', known: 'review', review: 'new' };
const FILTERS = [['all', 'Все слова'], ['unknown', 'Не изучены'], ['review', 'Повторить'], ['known', 'Изучены']];
const $ = s => document.querySelector(s);
const esc = s => String(s).replace(/[&<>"']/g, c => ({ '&': '&amp;', '<': '&lt;', '>': '&gt;', '"': '&quot;', "'": '&#39;' }[c]));
const shuffle = a => { a = [...a]; for (let i = a.length - 1; i > 0; i--) { const j = Math.floor(Math.random() * (i + 1)); [a[i], a[j]] = [a[j], a[i]]; } return a; };
const norm = s => s.toLowerCase().replace(/ё/g, 'е').replace(/[.,!?;:"«»()]/g, '').replace(/\s+/g, ' ').trim();
const enOf = i => WORDS[i][0];
const ruOf = i => WORDS[i][1];

/* ---------- storage ---------- */
const fresh = () => ({ status: {}, stats: { quizOk: 0, quizAll: 0, typeOk: 0, typeAll: 0 } });
function load() {
  try {
    const d = JSON.parse(localStorage.getItem(KEY));
    if (d && d.status) return { status: d.status, stats: { ...fresh().stats, ...d.stats } };
  } catch (e) {}
  return fresh();
}
let data = load();
function save() { try { localStorage.setItem(KEY, JSON.stringify(data)); } catch (e) {} }
const st = i => data.status[i] || 'new';
function setSt(i, v) {
  if (v === 'new') delete data.status[i]; else data.status[i] = v;
  save();
  updateChips();
}
function inFilter(f, s) {
  return f === 'all' || (f === 'unknown' ? s !== 'known' : f === 'review' ? s === 'review' : s === 'known');
}
const indicesFor = f => WORDS.map((_, i) => i).filter(i => inFilter(f, st(i)));
function fillFilter(sel, def) {
  sel.innerHTML = FILTERS.map(([v, t]) => `<option value="${v}">${t}</option>`).join('');
  sel.value = def;
}
function updateChips() {
  const c = { new: 0, known: 0, review: 0 };
  WORDS.forEach((_, i) => c[st(i)]++);
  $('#chips').innerHTML = [
    `Всего <b>${WORDS.length}</b>`,
    `Изучено <b>${c.known}</b>`,
    `Повторить <b>${c.review}</b>`,
    `Новых <b>${c.new}</b>`,
    `Тест <b>${data.stats.quizOk}/${data.stats.quizAll}</b>`,
    `Ввод <b>${data.stats.typeOk}/${data.stats.typeAll}</b>`
  ].map(t => `<span class="chip">${t}</span>`).join('');
  $('#meter').style.width = (c.known / WORDS.length * 100) + '%';
}

/* ---------- speech ---------- */
function speak(text) {
  if (!SPEECH || !text) return;
  speechSynthesis.cancel();
  const u = new SpeechSynthesisUtterance(text);
  u.lang = 'en-US';
  u.rate = 0.9;
  const v = speechSynthesis.getVoices().find(x => /^en[-_]/i.test(x.lang));
  if (v) u.voice = v;
  speechSynthesis.speak(u);
}

/* ---------- theme & tabs ---------- */
function setTheme(t) {
  document.documentElement.setAttribute('data-theme', t);
  $('#themeBtn').textContent = t === 'dark' ? 'Светлая тема' : 'Тёмная тема';
  try { localStorage.setItem('oxford3000_p1_theme', t); } catch (e) {}
}
$('#themeBtn').onclick = () => setTheme(document.documentElement.getAttribute('data-theme') === 'dark' ? 'light' : 'dark');

let current = 'cards';
function showTab(t) {
  current = t;
  document.querySelectorAll('.tab').forEach(b => b.classList.toggle('active', b.dataset.tab === t));
  document.querySelectorAll('.panel').forEach(p => p.classList.toggle('active', p.id === 'p-' + t));
  if (t === 'cards') buildDeck();
  if (t === 'dict') renderDict();
}
document.querySelectorAll('.tab').forEach(b => b.onclick = () => showTab(b.dataset.tab));

/* ---------- flashcards ---------- */
const flip = $('#flip');
let deck = [], pos = 0;
function unflip() {
  flip.style.transition = 'none';
  flip.classList.remove('is-flipped');
  void flip.offsetWidth;
  flip.style.transition = '';
}
function buildDeck() {
  const cur = deck[pos];
  deck = indicesFor($('#cardsFilter').value);
  pos = Math.max(0, deck.indexOf(cur));
  unflip();
  renderCard();
}
function renderCard() {
  const empty = !deck.length;
  ['prevBtn', 'nextBtn', 'repeatBtn', 'knowBtn', 'cardSpeak'].forEach(id => $('#' + id).disabled = empty);
  if (empty) {
    $('#cardBadge').textContent = '';
    $('#cardEn').textContent = 'Пусто';
    $('#cardEn2').textContent = '';
    $('#cardRu').textContent = 'В этом списке нет слов';
    $('#cardsCount').textContent = '';
    $('#cardSpeak').removeAttribute('data-say');
    return;
  }
  const i = deck[pos], s = st(i);
  $('#cardEn').textContent = enOf(i);
  $('#cardEn2').textContent = enOf(i);
  $('#cardRu').textContent = ruOf(i);
  $('#cardBadge').textContent = LABEL[s];
  $('#cardBadge').className = 'badge ' + s;
  $('#cardSpeak').dataset.say = enOf(i);
  $('#cardsCount').textContent = `${pos + 1} из ${deck.length}`;
}
function flipCard() { if (deck.length) flip.classList.toggle('is-flipped'); }
function move(d) {
  if (!deck.length) return;
  pos = (pos + d + deck.length) % deck.length;
  unflip();
  renderCard();
}
function mark(v) {
  if (!deck.length) return;
  setSt(deck[pos], v);
  move(1);
}
flip.onclick = flipCard;
$('#prevBtn').onclick = () => move(-1);
$('#nextBtn').onclick = () => move(1);
$('#knowBtn').onclick = () => mark('known');
$('#repeatBtn').onclick = () => mark('review');
$('#shuffleBtn').onclick = () => { deck = shuffle(deck); pos = 0; unflip(); renderCard(); };
$('#cardsFilter').onchange = buildDeck;

/* ---------- quiz ---------- */
let quiz = null;
const qBox = $('#quizBox');
function makeCur(i, askEn) {
  const correct = askEn ? ruOf(i) : enOf(i);
  const opts = [correct];
  while (opts.length < 4) {
    const w = WORDS[Math.floor(Math.random() * WORDS.length)];
    const cand = askEn ? w[1] : w[0];
    if (!opts.some(o => norm(o) === norm(cand))) opts.push(cand);
  }
  return { opts: shuffle(opts), correct };
}
function startQuiz() {
  const pool = shuffle(indicesFor($('#quizPool').value));
  const n = Math.min(+$('#quizCount').value, pool.length);
  if (!n) {
    quiz = null;
    qBox.innerHTML = '<p class="muted">В этом наборе нет слов. Выберите другой.</p>';
    return;
  }
  const askEn = $('#quizDir').value === 'en-ru';
  quiz = { list: pool.slice(0, n), idx: 0, ok: 0, wrong: [], answered: false, askEn, cur: null };
  quiz.cur = makeCur(quiz.list[0], askEn);
  renderQuiz();
}
function renderQuiz() {
  const q = quiz, i = q.list[q.idx];
  const prompt = q.askEn ? enOf(i) : ruOf(i);
  qBox.innerHTML = `
    <div class="qhead"><span>Вопрос ${q.idx + 1} из ${q.list.length}</span><span>Верно: ${q.ok}</span></div>
    <div class="bar"><i style="width:${q.idx / q.list.length * 100}%"></i></div>
    <div class="prompt"><div class="word">${esc(prompt)}</div>${q.askEn ? `<button class="quiet speak" type="button" data-say="${esc(enOf(i))}">🔊 Произнести</button>` : ''}</div>
    <div class="opts">${q.cur.opts.map((o, k) => `<button class="opt" type="button" data-k="${k}"><kbd>${k + 1}</kbd>${esc(o)}</button>`).join('')}</div>
    <div class="fb" id="qFb"></div>
    <div class="actions"><button class="solid" id="qNext" type="button" hidden>${q.idx + 1 < q.list.length ? 'Дальше' : 'Итоги'}</button></div>`;
}
function answerQuiz(k) {
  const q = quiz;
  if (!q || q.answered) return;
  const i = q.list[q.idx];
  q.answered = true;
  const good = q.cur.opts[k] === q.cur.correct;
  data.stats.quizAll++;
  if (good) { q.ok++; data.stats.quizOk++; }
  else { q.wrong.push(i); if (st(i) !== 'known') setSt(i, 'review'); }
  save();
  updateChips();
  qBox.querySelectorAll('.opt').forEach((b, j) => {
    b.disabled = true;
    if (q.cur.opts[j] === q.cur.correct) b.classList.add('right');
    else if (j === k) b.classList.add('wrong');
  });
  $('#qFb').innerHTML = good
    ? '<span class="good">Верно</span>'
    : `<span class="bad">Неверно.</span> Правильно: <b>${esc(q.cur.correct)}</b>`;
  const nb = $('#qNext');
  nb.hidden = false;
  nb.focus();
}
function nextQuiz() {
  const q = quiz;
  q.idx++;
  q.answered = false;
  if (q.idx >= q.list.length) return renderQuizResult();
  q.cur = makeCur(q.list[q.idx], q.askEn);
  renderQuiz();
}
function renderQuizResult() {
  const q = quiz, pct = Math.round(q.ok / q.list.length * 100);
  const msg = pct >= 90 ? 'Отличный результат.' : pct >= 70 ? 'Хорошо, так держать.' : pct >= 50 ? 'Неплохо, есть что повторить.' : 'Стоит повторить слова.';
  qBox.innerHTML = `
    <div class="result">
      <div class="big">${pct}%</div>
      <p>Верно ${q.ok} из ${q.list.length}. ${msg}</p>
      ${q.wrong.length ? `<p class="muted">Ошибки добавлены в «Повторить»:</p><ul class="wlist">${q.wrong.map(i => `<li><span class="en">${esc(enOf(i))}</span> — ${esc(ruOf(i))}</li>`).join('')}</ul>` : ''}
      <div class="actions"><button class="solid" id="quizAgain" type="button">Пройти снова</button></div>
    </div>`;
}

/* ---------- typing ---------- */
let typ = null;
const tBox = $('#typeBox');
function startTyping() {
  const pool = shuffle(indicesFor($('#typePool').value));
  if (!pool.length) {
    typ = null;
    tBox.innerHTML = '<p class="muted">В этом наборе нет слов.</p>';
    return;
  }
  typ = { list: pool, idx: 0, ok: 0, n: 0, answered: false, askEn: $('#typeDir').value === 'en-ru' };
  renderTyping();
}
function renderTyping() {
  const t = typ, i = t.list[t.idx];
  const prompt = t.askEn ? enOf(i) : ruOf(i);
  tBox.innerHTML = `
    <div class="qhead"><span>Слово ${t.idx + 1} из ${t.list.length}</span><span>Верно: ${t.ok} из ${t.n}</span></div>
    <div class="bar"><i style="width:${t.idx / t.list.length * 100}%"></i></div>
    <div class="prompt"><div class="word">${esc(prompt)}</div>${t.askEn ? `<button class="quiet speak" type="button" data-say="${esc(enOf(i))}">🔊 Произнести</button>` : ''}</div>
    <input id="typeInput" autocomplete="off" autocapitalize="off" spellcheck="false" aria-label="Ваш ответ" placeholder="${t.askEn ? 'Перевод на русском' : 'Перевод на английском'}">
    <div class="fb" id="tFb"></div>
    <div class="actions">
      <button class="solid" id="tCheck" type="button">Проверить</button>
      <button class="solid" id="tNext" type="button" hidden>Дальше</button>
    </div>`;
  $('#typeInput').focus();
}
function checkTyping() {
  const t = typ, input = $('#typeInput');
  if (!t || t.answered || !input || !input.value.trim()) return;
  const i = t.list[t.idx], val = input.value;
  const target = t.askEn ? ruOf(i) : enOf(i);
  const variants = [target, ...target.split(/[,;\/]/)].map(norm).filter(Boolean);
  const good = variants.includes(norm(val));
  t.answered = true;
  t.n++;
  data.stats.typeAll++;
  if (good) { t.ok++; data.stats.typeOk++; }
  else if (st(i) !== 'known') setSt(i, 'review');
  save();
  updateChips();
  input.disabled = true;
  $('#tFb').innerHTML = good
    ? `<span class="good">Верно: <b>${esc(target)}</b></span>`
    : `<span class="bad">Неверно.</span> Вы ввели: ${esc(val)}<br>Правильно: <b>${esc(target)}</b>`;
  $('#tCheck').hidden = true;
  const nb = $('#tNext');
  nb.hidden = false;
  nb.focus();
}
function nextTyping() {
  const t = typ;
  t.idx++;
  t.answered = false;
  if (t.idx >= t.list.length) return renderTypingResult();
  renderTyping();
}
function renderTypingResult() {
  const pct = Math.round(typ.ok / typ.list.length * 100);
  tBox.innerHTML = `<div class="result"><div class="big">${pct}%</div><p>Верно ${typ.ok} из ${typ.list.length}.</p><div class="actions"><button class="solid" id="typeAgain" type="button">Новый набор</button></div></div>`;
}

/* ---------- dictionary ---------- */
let letter = 'all';
const LETTERS = [...new Set(WORDS.map(w => w[0][0].toUpperCase()))].sort();
function renderLetters() {
  $('#letters').innerHTML = ['all', ...LETTERS]
    .map(l => `<button type="button" data-l="${l}" class="${l === letter ? 'on' : ''}">${l === 'all' ? 'Все' : l}</button>`)
    .join('');
}
function renderDict() {
  const q = norm($('#search').value), sf = $('#dictStatus').value;
  const rows = [];
  WORDS.forEach((w, i) => {
    const s = st(i);
    if (letter !== 'all' && w[0][0].toUpperCase() !== letter) return;
    if (!inFilter(sf, s)) return;
    if (q && !norm(w[0]).includes(q) && !norm(w[1]).includes(q)) return;
    rows.push(`<div class="row"><button class="quiet speak" type="button" data-say="${esc(w[0])}" aria-label="Произнести">🔊</button><div><div class="en">${esc(w[0])}</div><div class="ru">${esc(w[1])}</div></div><button class="stbtn ${s}" type="button" data-i="${i}">${LABEL[s]}</button></div>`);
  });
  $('#dictCount').textContent = `Найдено: ${rows.length} из ${WORDS.length}`;
  $('#dictList').innerHTML = rows.join('') || '<div class="row"><span class="muted">Ничего не найдено</span></div>';
}
$('#letters').onclick = e => {
  const b = e.target.closest('[data-l]');
  if (!b) return;
  letter = b.dataset.l;
  renderLetters();
  renderDict();
};
$('#dictList').onclick = e => {
  const b = e.target.closest('.stbtn');
  if (!b) return;
  const i = +b.dataset.i;
  setSt(i, NEXT[st(i)]);
  renderDict();
};
$('#search').oninput = renderDict;
$('#dictStatus').onchange = renderDict;

/* ---------- controls ---------- */
qBox.addEventListener('click', e => {
  const opt = e.target.closest('.opt');
  if (opt) return answerQuiz(+opt.dataset.k);
  if (e.target.closest('#qNext')) return nextQuiz();
  if (e.target.closest('#quizAgain')) return startQuiz();
});
tBox.addEventListener('click', e => {
  if (e.target.closest('#tCheck')) return checkTyping();
  if (e.target.closest('#tNext')) return nextTyping();
  if (e.target.closest('#typeAgain')) return startTyping();
});
$('#quizStart').onclick = startQuiz;
$('#typeStart').onclick = startTyping;
$('#resetBtn').onclick = () => {
  if (!confirm('Сбросить весь прогресс и статистику?')) return;
  data = fresh();
  save();
  updateChips();
  buildDeck();
  renderDict();
};
document.addEventListener('click', e => {
  const b = e.target.closest('[data-say]');
  if (b) speak(b.dataset.say);
});
document.addEventListener('mouseup', e => {
  const b = e.target.closest('button');
  if (b) b.blur();
});
document.addEventListener('keydown', e => {
  if (e.ctrlKey || e.metaKey || e.altKey) return;
  const tag = e.target.tagName;
  const field = tag === 'INPUT' || tag === 'SELECT' || tag === 'TEXTAREA';
  if (current === 'cards' && !field) {
    if (e.key === 'ArrowRight') { e.preventDefault(); move(1); }
    else if (e.key === 'ArrowLeft') { e.preventDefault(); move(-1); }
    else if (e.key === ' ' && tag !== 'BUTTON') { e.preventDefault(); flipCard(); }
    else if (e.key === 'Enter' && e.target === flip) { e.preventDefault(); flipCard(); }
  }
  if (current === 'quiz' && quiz && !field && tag !== 'BUTTON' && quiz.idx < quiz.list.length) {
    if (/^[1-4]$/.test(e.key) && !quiz.answered) { e.preventDefault(); answerQuiz(+e.key - 1); }
    else if (e.key === 'Enter' && quiz.answered) { e.preventDefault(); nextQuiz(); }
  }
  if (current === 'typing' && typ && typ.idx < typ.list.length && e.key === 'Enter' && tag !== 'BUTTON') {
    e.preventDefault();
    if (typ.answered) nextTyping(); else checkTyping();
  }
});

/* ---------- init ---------- */
fillFilter($('#cardsFilter'), 'unknown');
fillFilter($('#quizPool'), 'all');
fillFilter($('#typePool'), 'all');
fillFilter($('#dictStatus'), 'all');
renderLetters();
setTheme(document.documentElement.getAttribute('data-theme') || 'light');
if (!SPEECH) document.body.classList.add('nospeech');
updateChips();
buildDeck();
</script>
</body>
</html>
