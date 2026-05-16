---
title: "Интеграция Bootstrap 5 в приложение с Luxon. Этап 3"
date: 2026-04-25
draft: false
---

# Интеграция Bootstrap 5 в приложение с Luxon. Этап 3

## Цель работы

Создать новый проект с использованием сборщика Vite, подключить Bootstrap 5 через npm, интегрировать библиотеку Luxon и реализовать интерфейс, аналогичный этапу 2.

## Использованные технологии

- HTML
- JavaScript
- Vite
- Bootstrap 5
- Sass
- Luxon
- npm

## Ход работы

1. Был создан новый npm-проект.
2. Была установлена зависимость Vite для сборки проекта.
3. Были установлены Bootstrap 5, Popper и Sass.
4. Была установлена библиотека Luxon для работы с датой и временем.
5. Была создана структура проекта с папками `src`, `js` и `scss`.
6. В файле `vite.config.js` был указан корень проекта `src`, папка для сборки `dist` и порт `8080`.
7. В файле `styles.scss` был импортирован Bootstrap через Sass.
8. В файле `main.js` были импортированы стили Bootstrap, модальный компонент Bootstrap и `DateTime` из Luxon.
9. В файле `index.html` был реализован интерфейс из трёх колонок в соотношении `2-8-2`.
10. В центральной колонке была размещена зелёная кнопка `Показать время`.
11. При нажатии на кнопку открывается модальное окно Bootstrap.
12. В модальном окне отображается текущая дата и время, сформированные с помощью Luxon.

## Структура проекта

![Структура проекта](/images/vite-stage3-structure.png)

## Файл vite.config.js

```js
import { resolve } from 'path'

export default {
  root: resolve(__dirname, 'src'),
  build: {
    outDir: '../dist',
    emptyOutDir: true
  },
  server: {
    port: 8080
  },
  css: {
    preprocessorOptions: {
      scss: {
        silenceDeprecations: [
          'import',
          'mixed-decls',
          'color-functions',
          'global-builtin',
        ],
      },
    },
  },
}
```

![Файл vite.config.js](/images/vite-stage3-config.png)

## Файл package.json

В файл `package.json` были добавлены команды для запуска, сборки и просмотра проекта.

```json
"scripts": {
  "start": "vite",
  "build": "vite build",
  "preview": "vite preview --host 0.0.0.0 --port 8080",
  "test": "echo \"Error: no test specified\" && exit 1"
}
```

![Файл package.json](/images/vite-stage3-package.png)

## HTML-код страницы

В файле `src/index.html` была создана сетка Bootstrap, кнопка и модальное окно.

![Файл index.html](/images/vite-stage3-html.png)

## JavaScript-код

В файле `src/js/main.js` были подключены стили Bootstrap, модальное окно Bootstrap и библиотека Luxon.

```js
import '../scss/styles.scss'

import 'bootstrap/js/dist/modal'

import { DateTime } from 'luxon'

const timeElement = document.getElementById('hh')

function showCurrentTime() {
  timeElement.textContent = DateTime
    .local()
    .setLocale('ru')
    .toFormat('dd.LL.y HH:mm:ss')
}

showCurrentTime()
setInterval(showCurrentTime, 1000)
```

![Файл main.js](/images/vite-stage3-main.png)

## Команды для запуска проекта

```bash
npm install
npm start
```

После запуска проект доступен по адресу:

```text
http://localhost:8080
```

## Команда для сборки проекта

```bash
npm run build
```

## Размер полученного бандла

После выполнения команды `npm run build` были получены следующие файлы:

```text
dist/index.html                    1.86 kB
dist/assets/index-0BmDVrxS.css     224.90 kB
dist/assets/index-CfSUXA8i.js      93.62 kB
```

Размер полученного бандла:

```text
HTML: 1.86 kB
CSS: 224.90 kB
JS: 93.62 kB
```

![Результат сборки](/images/vite-stage3-build.png)

## Результат работы приложения

В результате было создано приложение с использованием Vite, Bootstrap 5 и Luxon. Bootstrap подключается не через CDN, а как npm-зависимость и собирается вместе с проектом. Приложение отображает текущее время во всплывающем модальном окне Bootstrap.

![Внешний вид приложения](/images/vite-stage3-result.png)