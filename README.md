# Задание 1. Вёрстка шаблонов Stories

В этом репозитории находятся материалы тестового задания «Шаблоны Stories» для [17-й Школы разработки интерфейсов](https://yandex.ru/promo/academy/shri) (лето-2021, Москва).

В тестовом задании вы будете работать над приложением, которое позволяет просмотреть информацию о работе команды над проектом в виде stories. Каждый слайд истории визуализирует небольшой объём информации при помощи одного из пяти шаблонов.

## Шаблоны

1. Лидеры спринта — позволяет увидеть участников команды, лидирующих в разных номинациях. Также используется для отображения результатов голосования.
2. Голосование за участника команды — выводит список участников команды постранично и позволяет проголосовать за участника в одной из номинаций.
3. Статистика по спринтам — визуализирует статистику текущего спринта по сравнению с предыдущими спринтами, например показывает количество коммитов в текущем и предыдущих спринтах.
4. Статистика внутри спринта — визуализирует статистику внутри спринта по качественным характеристикам, например размеру коммитов в спринте, и разницу с предыдущим спринтом.
5. Активность участников — визуализирует активность команды в виде тепловой карты по дням и часам.

## Задание

В первом задании необходимо сверстать шаблоны по [макетам](https://www.figma.com/file/0HYYteSLpxex9QeAka6JGr/IDC-2021-test-work?node-id=138%3A1981). В макетах представлена вертикальная ориентация, адаптированная горизонтальная версия и светлая тема. На отдельный арт-борд вынесены [спецификации](https://www.figma.com/file/0HYYteSLpxex9QeAka6JGr/IDC-2021-test-work?node-id=711%3A12033). Если при отображении макетов в приложении Figma возникают проблемы, можно использовать альтернативный способ работы с макетами. Мы подготовили [HTML-версию макетов](https://yndx-shri.github.io/shri-2021-task-1) и экспортировали [изображения](/assets/images) в разных форматах и размерах, чтобы вы могли выбрать необходимые.

Шаблоны должны отображаться на весь экран и соответствовать макетам в представленном размере. Стили, например тени и скругления в шаблоне с круговой диаграммой, могут отличаться от макета. Полное соответствие круговой диаграммы макетам считается дополнительным заданием.

Пожалуйста, напишите скрипт `build/stories.js`, реализующий код формирования HTML-разметки шаблонов и функцию шаблонизации `renderTemplate`, которая принимает строку с алиасом шаблона `alias` и данные для шаблона `data`. Ожидаемый результат функции `renderTemplate` — строка с HTML-разметкой слайда. Данные для шаблонов представлены в файле `data.json` в каталоге `data`, [описание формата](/data). Функция должна быть доступна глобально, для этого присвойте функцию `renderTemplate` в качестве метода объекта `window` внутри скрипта.

```js
// Пример скрипта stories.js
window.renderTemplate = function(alias, data) {
   // ...
   return '<HTML-разметка отдельного слайда в виде строки>';
}
```

Приложение должно запускаться на локальном хосте командой `npm start` и быть доступным по адресу http://localhost:8080, при переходе по которому должен отобразиться слайд с индексом 0 из данных. Вы можете использовать `express.js` в качестве веб-сервера. Чтобы при проверке мы могли переключаться между слайдами и темой, пожалуйста, добавьте поддержку параметров адресной строки:

* `?slide=1` — переключение слайдов с 1 по 11, 1 соответствует индексу 0 в массиве слайдов в файле `data.json`;
* `&theme=light` — тема, `light` или `dark`, без параметра шаблоны должны рендериться в тёмной теме.

Тема приложения должна устанавливаться при помощи класса `theme_dark` или `theme_light` у элемента, который содержит HTML-разметку, сформированную функцией `renderTemplate`. Например, на тег `body` может быть установлен класс `theme_light`. Если класс темы не задан, шаблон должен отображаться в тёмной теме.

```html
// Пример index.html, возвращаемого сервером
// Cодержит подключение stories.js, stories.css, вызов renderTemplate, установку содержимого body
// Алиас и данные передаются в функцию из data.json в соответствии с параметром адресной строки
// Тема устанавливается в соответствии с параметром адресной строки
<html>
    <head>
        <link rel="stylesheet" href="stories.css">
    </head>
    <body class="theme_<тема приложения>">
        <script type="text/javascript" src="stories.js"></script>
        <script>
            const body = document.querySelector('body');
            body.innerHTML = window.renderTemplate(<алиас шаблона>, <данные шаблона>);
        </script>
    </body>
</html>
```

В качестве результата выполнения задания укажите ссылку на репозиторий c исходным кодом и собранными файлами. Обратите внимание: сделайте репозиторий приватным, чтобы другие кандидаты не могли скопировать ваш код. В корне репозитория должен находиться каталог `build` с собранными файлами `stories.css`, `stories.js`, необходимыми изображениями и шрифтами. Размер каждого файла — не более 1 МБ. Файлы `stories.css`, `stories.js` не должны требовать подключения дополнительных зависимостей и должны содержать весь код, необходимый для их работы. Если `stories.js`, `stories.css` являются результатом сборки, то предоставьте также исходный код, из которого они были собраны.

* `stories.css` — содержит стили для всех элементов;
* `stories.js` — содержит код формирования HTML-разметки и функцию шаблонизации `renderTemplate`. 

## Интерактивность

В этом задании мы не просим реализовать интерактивность. В шаблоне со статистикой по спринтам навигацию по значениям разных спринтов в виде горизонтального скролла реализовывать не нужно. В шаблоне голосования выбор участника и переключение между страницами будет частью третьего задания. Мы ожидаем, что интерактивные элементы в шаблоне голосования будут иметь состояния, соответствующие данным и действиям пользователя.

Для корректной работы интерактивности в третьем задании необходимо правильно разметить атрибуты `data-action` и `data-params` интерактивных элементов в шаблоне голосования. В них будет содержаться информация о действии, которое нужно совершить, если нажать элемент. В атрибут `data-action` необходимо установить событие `update`. В атрибут `data-params` необходимо установить сериализованный объект с данными события, в виде:

```js
// Событие выбора участника в шаблоне голосования
{
  alias: 'leaders',     // Подставить 'leaders', в этом шаблоне мы отобразим результаты голосования
  data: {
    selectedUserId: 1   // Подставить ID выбранного пользователя
  }
}
```

```js
// Событие переключения страницы на предыдущую или следующую в шаблоне голосования
{
  alias: 'vote',        // Подставить 'vote', в этом шаблоне мы отобразим следующую страницу 
  data: {
    offset: 10          // Подставить индекс пользователя, с которого должна начинаться страница
  }
}
```

## Критерии

Мы ожидаем, что вёрстка будет соответствовать макетам в представленном размере. Могут быть незначительные отличия, важно, чтобы вёрстка проходила наши автоматизированные тесты. Приложение должно корректно работать в последних версиях Chrome, Mozilla Firefox, iOS, Android. Также используйте [шрифт](/assets/fonts), приложенный в репозитории.

Макеты представлены в размере 376 × 668, размер iPhone 8 + 1 px. Мы добавили 1 px, чтобы избежать неточностей из-за нечётного количества пикселей. Это позволит вам точно видеть отступы по правому и левому краю. При разработке не забудьте добавить пользовательский размер экрана в средствах разработчика. Также для удобства работы с макетами вы можете отключить мультикурсор в приложении Figma.

Мы не задаём фиксированного поведения адаптивности, в спецификации указаны только некоторые характеристики. Мы ожидаем, что макеты при этом отобразятся корректно и на экранах устройств других размеров, а контент будет удобен для пользователя.

При проверке вашего задания мы также будем смотреть вёрстку на размерах 320 × 568, 414 × 736, 768 × 1024 в вертикальной и горизонтальной ориентации и 1366 × 768, 1920 × 1080 в горизонтальной ориентации. Адаптированный интерфейс под десктопное разрешение позволит выводить наши stories на большие экраны, например телевизоры. 

Мы не ограничиваем вас в использовании сторонних инструментов и библиотек, но ждём комментария — что и зачем вы использовали. Опишите в файле `README.md` ход ваших мыслей при выборе, любые другие важные детали о выбранных способах решения. Также, пожалуйста, уделите внимание организации и оформлению кода.