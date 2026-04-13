# Инструкция: интеграция опросника в прототип

## Контекст

Файл `index.html` — статический прототип Code Maestro Analytics (single HTML file, Chart.js, vanilla JS). Задеплоен на Vercel как static site. Сейчас в прототипе есть 4 таба (Dashboard, Insights, Hypothesis Lab, Setup) и Interactive Guided Tour (кнопка "Explain the Interface" в top bar).

Нужно добавить **кнопку "Complete Survey"**, которая открывает ссылку на Google Form в новой вкладке. Также нужен **popup после завершения тура**, предлагающий пройти опрос.

## Google Form URL

Ссылка на Google Form будет вставлена позже. В коде используй placeholder-переменную:

```javascript
const SURVEY_URL = 'https://forms.gle/PLACEHOLDER_REPLACE_ME';
```

Определи эту переменную один раз в начале скрипта. Все кнопки/ссылки на опрос должны использовать `SURVEY_URL`, чтобы при замене ссылки достаточно было поменять одну строку.

---

## Задача 1: Кнопка "Complete Survey" в top bar

### Где

В элементе `.topbar-right` (строка ~287), рядом с period badge и help button.

### Текущая структура topbar-right:

```html
<div class="topbar-right">
  <div class="period-badge">📅 Mar 1–31, 2026</div>
  <button class="help-btn">?</button>
</div>
```

### Что добавить

Кнопку между period-badge и help-btn:

```html
<button class="survey-topbar-btn" onclick="window.open(SURVEY_URL, '_blank')">
  📋 Complete Survey
</button>
```

### Стиль кнопки

Стиль должен привлекать внимание, но НЕ конфликтовать с gold кнопкой тура. Используй violet (accent-violet) как основной цвет:

```css
.survey-topbar-btn {
  display: flex;
  align-items: center;
  gap: 6px;
  padding: 7px 14px;
  border-radius: 6px;
  border: none;
  background: var(--accent-violet);
  color: #fff;
  font-family: 'Inter', sans-serif;
  font-size: 12px;
  font-weight: 600;
  cursor: pointer;
  transition: all .2s;
  white-space: nowrap;
}
.survey-topbar-btn:hover {
  background: var(--accent-violet-light);
  box-shadow: 0 2px 8px rgba(104, 72, 209, .4);
}
```

---

## Задача 2: Таб "Survey" в левом сайдбаре

### Где

В элементе `.sidebar-nav` (строки ~295–311), после таба Setup.

### Текущая структура:

```html
<nav class="sidebar-nav">
  <div class="nav-item active" data-tab="dashboard">...</div>
  <div class="nav-item" data-tab="insights">...</div>
  <div class="nav-item" data-tab="lab">...</div>
  <div class="nav-item" data-tab="setup">...</div>
</nav>
```

### Что добавить

Новый nav-item ПОСЛЕ setup. Этот элемент НЕ переключает таб — он сразу открывает Google Form:

```html
<div class="nav-item survey-nav-item" onclick="window.open(SURVEY_URL, '_blank')">
  <span class="icon">📋</span>
  <span class="label">Complete Survey</span>
</div>
```

### Дополнительный стиль

Чтобы визуально отделить от основной навигации, добавь разделитель перед survey-nav-item:

```css
.survey-nav-item {
  margin-top: 12px;
  padding-top: 12px;
  border-top: 1px solid var(--border);
  color: var(--accent-violet-light) !important;
}
.survey-nav-item:hover {
  background: rgba(104, 72, 209, .1) !important;
  color: var(--accent-violet-light) !important;
}
```

**Важно:** этот nav-item НЕ должен участвовать в системе переключения табов. В текущем JS есть обработчик `document.querySelectorAll('.nav-item').forEach(...)` который переключает табы. Убедись, что survey-nav-item исключён из этой логики. Самый простой способ: добавь проверку `if (item.classList.contains('survey-nav-item')) return;` в начало обработчика кликов по nav-item, ИЛИ не давай ему `data-tab` атрибут и проверяй наличие `data-tab` перед переключением.

---

## Задача 3: Popup после завершения тура

### Когда показывать

После завершения Guided Tour. В текущем коде функция `endTour()` (строка ~1197) вызывается когда тур заканчивается:

```javascript
function endTour() {
  overlay.classList.remove('active');
  spotlight.style.cssText = 'width:0;height:0;border:none;box-shadow:none';
  tooltip.style.display = 'none';
  document.querySelectorAll('.nav-item').forEach(n => n.style.borderLeftColor = '');
  current = -1;
}
```

Добавь вызов `showSurveyPopup()` в конце `endTour()`, НО только если тур был пройден до конца (не закрыт на первых шагах). Логика:

```javascript
function endTour() {
  const wasCompleted = current >= activeSteps.length - 1;
  // ... existing cleanup code ...
  current = -1;
  if (wasCompleted) {
    setTimeout(showSurveyPopup, 500); // небольшая задержка после анимации закрытия тура
  }
}
```

### HTML popup

Добавь перед закрывающим `</body>`:

```html
<div class="survey-popup" id="surveyPopup">
  <div class="survey-popup-card">
    <button class="survey-popup-close" onclick="closeSurveyPopup()">&times;</button>

    <div class="survey-popup-icon">📋</div>

    <h3>Помогите нам сделать аналитику лучше!</h3>

    <p>
      Вы только что посмотрели прототип Code Maestro Analytics.
      Ваш фидбэк напрямую повлияет на то, что мы будем строить.
    </p>

    <div class="survey-popup-meta">
      <div class="survey-meta-item">
        <span class="survey-meta-icon">⏱</span>
        <span>~5 минут</span>
      </div>
      <div class="survey-meta-item">
        <span class="survey-meta-icon">📊</span>
        <span>13 вопросов</span>
      </div>
    </div>

    <div class="survey-popup-btns">
      <button class="survey-popup-btn-primary" onclick="window.open(SURVEY_URL, '_blank'); closeSurveyPopup();">
        Пройти опрос →
      </button>
      <button class="survey-popup-btn-secondary" onclick="closeSurveyPopup()">
        Позже
      </button>
    </div>
  </div>
</div>
```

### CSS popup

```css
/* Survey Popup */
.survey-popup {
  position: fixed;
  inset: 0;
  z-index: 9600;
  display: flex;
  align-items: center;
  justify-content: center;
  background: rgba(0, 0, 0, .7);
  opacity: 0;
  pointer-events: none;
  transition: opacity .3s;
}
.survey-popup.active {
  opacity: 1;
  pointer-events: auto;
}
.survey-popup-card {
  background: var(--bg-card);
  border: 1px solid var(--border);
  border-radius: 16px;
  padding: 36px;
  max-width: 420px;
  text-align: center;
  box-shadow: 0 16px 48px rgba(0, 0, 0, .5);
  position: relative;
}
.survey-popup-close {
  position: absolute;
  top: 12px;
  right: 12px;
  width: 28px;
  height: 28px;
  border-radius: 6px;
  border: 1px solid var(--border);
  background: var(--bg-surface);
  color: var(--text-muted);
  cursor: pointer;
  font-size: 16px;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: all .15s;
}
.survey-popup-close:hover {
  border-color: var(--accent-red);
  color: var(--accent-red);
}
.survey-popup-icon {
  font-size: 40px;
  margin-bottom: 16px;
}
.survey-popup-card h3 {
  font-size: 18px;
  margin-bottom: 10px;
  color: var(--text-primary);
}
.survey-popup-card p {
  font-size: 13px;
  line-height: 1.65;
  color: var(--text-secondary);
  margin-bottom: 20px;
}
.survey-popup-meta {
  display: flex;
  gap: 20px;
  justify-content: center;
  margin-bottom: 24px;
}
.survey-meta-item {
  display: flex;
  align-items: center;
  gap: 6px;
  font-size: 13px;
  color: var(--text-muted);
}
.survey-meta-icon {
  font-size: 16px;
}
.survey-popup-btns {
  display: flex;
  gap: 12px;
  justify-content: center;
}
.survey-popup-btn-primary {
  padding: 12px 28px;
  border-radius: 8px;
  border: none;
  background: var(--accent-violet);
  color: #fff;
  font-family: 'Inter', sans-serif;
  font-size: 14px;
  font-weight: 700;
  cursor: pointer;
  transition: all .2s;
}
.survey-popup-btn-primary:hover {
  background: var(--accent-violet-light);
  box-shadow: 0 4px 16px rgba(104, 72, 209, .4);
}
.survey-popup-btn-secondary {
  padding: 12px 20px;
  border-radius: 8px;
  border: 1px solid var(--border);
  background: transparent;
  color: var(--text-muted);
  font-family: 'Montserrat', sans-serif;
  font-size: 13px;
  cursor: pointer;
  transition: all .15s;
}
.survey-popup-btn-secondary:hover {
  border-color: var(--text-muted);
  color: var(--text-secondary);
}
```

### JavaScript popup

```javascript
const SURVEY_URL = 'https://forms.gle/PLACEHOLDER_REPLACE_ME';

function showSurveyPopup() {
  document.getElementById('surveyPopup').classList.add('active');
}

function closeSurveyPopup() {
  document.getElementById('surveyPopup').classList.remove('active');
}
```

Определи `SURVEY_URL` в самом начале первого `<script>` блока (или в отдельном `<script>` перед остальными), чтобы он был доступен и для `onclick` атрибутов в HTML.

---

## Задача 4: Защита от конфликтов с существующим кодом

### Навигация по табам

Текущий обработчик навигации (строка ~712):

```javascript
document.querySelectorAll('.nav-item').forEach(item => {
  item.addEventListener('click', () => {
    document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active'));
    // ... tab switching logic
  });
});
```

Измени этот обработчик так, чтобы survey-nav-item игнорировался:

```javascript
document.querySelectorAll('.nav-item').forEach(item => {
  item.addEventListener('click', () => {
    if (item.classList.contains('survey-nav-item')) return;
    // ... rest of existing logic
  });
});
```

### Tour steps

В массиве `tourSteps` (или аналогичном) survey-nav-item не должен появляться. Не добавляй никаких шагов тура для survey.

### z-index порядок

- Tour welcome modal: 9500 (существующий)
- **Survey popup: 9600** (выше тура, на случай если оба видны)
- Tour overlay: 9000 (существующий)

---

## Чеклист после реализации

- [ ] `SURVEY_URL` определён в одном месте, все кнопки его используют
- [ ] Кнопка "📋 Complete Survey" видна в top bar рядом с period badge
- [ ] Таб "📋 Complete Survey" есть в сайдбаре, визуально отделён от основных табов
- [ ] Клик на любую из этих кнопок открывает Google Form в новой вкладке
- [ ] Клик на survey-nav-item НЕ переключает активный таб и не ломает навигацию
- [ ] После полного прохождения тура (не раннего выхода) — появляется popup
- [ ] Popup имеет кнопку "Пройти опрос →" (открывает форму) и "Позже" (закрывает popup)
- [ ] Закрытие popup по × работает
- [ ] Дизайн кнопок и popup соответствует стилю прототипа (dark theme, Inter/Montserrat, violet accent)
- [ ] Замена `PLACEHOLDER_REPLACE_ME` на реальную ссылку Google Forms — единственное изменение для активации

---

## Примечания

- Весь код добавляется в один файл `index.html` — без внешних зависимостей
- Popup текст на русском — это сделано намеренно (первая волна респондентов русскоязычная)
- Стиль survey-кнопок — violet, а не gold, чтобы не конфликтовать с кнопкой тура
