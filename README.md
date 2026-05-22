# ИИ-Воронка — Лендинг для коучей и онлайн-курсов

Готовый лендинг с квизом, калькулятором выручки, схемой ИИ-воронки и формой захвата контактов. Один HTML-файл без зависимостей — деплоится в один клик.

---

## Структура проекта

```
/
├── index.html      # Весь лендинг (HTML + CSS + JS в одном файле)
└── README.md       # Этот файл
```

---

## Что внутри лендинга

| Секция | Описание |
|---|---|
| **NAV** | Sticky-навигация с кнопкой «Получить расчёт» |
| **HERO** | Заголовок, подзаголовок, CTA-кнопки |
| **STATS** | Три ключевые метрики (×4.8 конверсия, −73% рутина, 24/7) |
| **PAIN / SOL** | Сравнение «сейчас» vs «с ИИ-воронкой» |
| **КВИЗ** | 3 вопроса → персональный тип воронки |
| **КАЛЬКУЛЯТОР** | Ввод трафика / чека / конверсии → расчёт выручки |
| **СХЕМА** | Визуальные этапы воронки с % и ИИ-инструментом на каждом |
| **ПРОГРАММА** | 4 блока: квалификатор, прогрев, чат, CRM |
| **ФОРМА** | Захват: имя, Telegram, ниша, чек, трафик |
| **FOOTER** | Контакты, дисклеймер |

---

## Быстрый деплой

### Netlify Drop (30 секунд, бесплатно)
1. Открой [app.netlify.com/drop](https://app.netlify.com/drop)
2. Перетащи папку с `index.html` в браузер
3. Получи ссылку вида `https://random-name.netlify.app`

### GitHub Pages (бесплатно, постоянный URL)
```bash
# 1. Создай репозиторий на github.com
# 2. Загрузи index.html и README.md
# 3. Settings → Pages → Deploy from branch → main → Save
# URL: https://username.github.io/repo-name/
```

### Vercel (через CLI)
```bash
npm install -g vercel
cd папка-с-проектом
vercel
# Войти через браузер → ссылка готова за ~1 минуту
```

### Netlify Drop через CLI
```bash
npm install -g netlify-cli
netlify deploy --prod --dir .
```

---

## Подключение формы

В `index.html` найди функцию `submitLead()` — там комментарий с местом для замены.

### Formspree (проще всего, бесплатно до 50 заявок/мес)
1. Зарегистрируйся на [formspree.io](https://formspree.io)
2. Создай форму → скопируй ID (вида `xkgwabcd`)
3. Замени в `submitLead()`:

```javascript
fetch('https://formspree.io/f/xkgwabcd', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({
    name: name,
    contact: contact,
    niche: niche,
    check: check,
    traffic: traffic
  })
}).then(function() {
  document.getElementById('the-lead-form').style.display = 'none';
  document.getElementById('lead-success').classList.add('show');
});
```

### Telegram Bot (заявки прямо в Telegram)
```javascript
var TOKEN   = 'YOUR_BOT_TOKEN';   // от @BotFather
var CHAT_ID = 'YOUR_CHAT_ID';     // твой chat_id

var text = '🆕 Новая заявка!\n\n'
  + '👤 Имя: ' + name + '\n'
  + '📱 Контакт: ' + contact + '\n'
  + '🎯 Ниша: ' + niche + '\n'
  + '💰 Чек: ' + check + '\n'
  + '👥 Трафик: ' + traffic;

fetch('https://api.telegram.org/bot' + TOKEN + '/sendMessage', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({ chat_id: CHAT_ID, text: text })
});
```

### Make / n8n / Zapier (webhook)
```javascript
fetch('https://hook.eu1.make.com/YOUR_WEBHOOK_ID', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({ name, contact, niche, check, traffic })
});
```

---

## Кастомизация

### Поменять цвет акцента
В начале `<style>` в `index.html`:
```css
:root {
  --neon: #00FFB2;  /* ← поменяй на любой цвет */
}
```

### Поменять тексты квиза
В `<script>` найди объект `QZ_RES` — там три варианта результата (A, B, C). Меняй `title`, `desc`, `feats` под свои формулировки.

### Поменять этапы воронки
Найди массив `funnelData` в `<script>`:
```javascript
var funnelData = [
  { label: '1. Трафик',     pct: 100, ai: 'Реклама / SEO / Соцсети' },
  // ... добавь или измени этапы
];
```

### Поменять контакты в футере
```html
<a href="mailto:hello@example.com">hello@example.com</a>
<a href="https://t.me/your_username">Telegram</a>
```

---

## Технический стек

- **HTML5** — семантическая разметка
- **CSS3** — переменные, grid, анимации (без фреймворков)
- **Vanilla JS** — квиз, калькулятор, форма (без jQuery и библиотек)
- **Google Fonts** — Space Mono + Syne (загружаются из CDN)
- **Размер файла** — ~38 КБ (один файл, без зависимостей)

---

## Чеклист перед публикацией

- [ ] Заменить `hello@example.com` на реальный email
- [ ] Заменить `https://t.me/your_username` на реальный Telegram
- [ ] Подключить реальную отправку формы (Formspree / Telegram / webhook)
- [ ] Проверить на мобильном устройстве
- [ ] Поставить реальный домен в настройках Netlify/Vercel
- [ ] Добавить Google Analytics или Яндекс.Метрику (опционально)

---

## Аналитика (опционально)

Вставь перед закрывающим `</head>`:

```html
<!-- Яндекс.Метрика -->
<script type="text/javascript">
  (function(m,e,t,r,i,k,a){m[i]=m[i]||function(){(m[i].a=m[i].a||[]).push(arguments)};
  var z=new Date();k=e.createElement(t),a=e.getElementsByTagName(t)[0],k.async=1,
  k.src=r,a.parentNode.insertBefore(k,a)})
  (window,document,"script","https://mc.yandex.ru/metrika/tag.js","ym");
  ym(YOUR_ID,"init",{clickmap:true,trackLinks:true,accurateTrackBounce:true});
</script>
```

---

*Создано с помощью Claude (Anthropic) · Дизайн-система: тёмный tech-стиль (Space Mono + Syne)*
