---
title: "Интеграция Bootstrap 5 в приложение с Luxon. Этап 2"
date: 2026-05-16
draft: false
---

# Интеграция Bootstrap 5 в приложение с Luxon. Этап 2

## Цель работы

Встроить приложение с библиотекой Luxon в шаблон Bootstrap 5 и реализовать вывод текущей даты и времени во всплывающем окне.

## Использованные технологии

- HTML
- Bootstrap 5
- JavaScript
- Luxon
- Webpack
- npm

## Ход работы

1. Был использован проект из первого этапа с Webpack и библиотекой Luxon.
2. В файл `index.html` был подключён Bootstrap 5 через CDN.
3. На странице была создана сетка Bootstrap из трёх колонок в соотношении `2-8-2`.
4. В центральную колонку была добавлена зелёная кнопка `Показать время`.
5. Кнопка занимает всю свободную ширину центральной колонки.
6. Было создано модальное окно Bootstrap.
7. При нажатии на кнопку открывается модальное окно.
8. В заголовке модального окна указаны имя и фамилия выполнившего задание.
9. В основной части модального окна отображается текущая дата и время, сформированные с помощью библиотеки Luxon.
10. Окно можно закрыть с помощью крестика в правом верхнем углу и кнопки `Закрыть`.

## HTML-код страницы

```html
<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Bootstrap demo</title>

  <link
    href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css"
    rel="stylesheet"
  >
</head>

<body>
  <div class="container mt-4">
    <div class="row">

      <div class="col-2"></div>

      <div class="col-8">
        <button
          type="button"
          class="btn btn-success w-100"
          data-bs-toggle="modal"
          data-bs-target="#timeModal"
        >
          Показать время
        </button>
      </div>

      <div class="col-2"></div>

    </div>
  </div>

  <div
    class="modal fade"
    id="timeModal"
    tabindex="-1"
    aria-labelledby="timeModalLabel"
    aria-hidden="true"
  >
    <div class="modal-dialog">
      <div class="modal-content">

        <div class="modal-header">
          <h5 class="modal-title" id="timeModalLabel">
            Выполнил: Доан Суан Бач
          </h5>

          <button
            type="button"
            class="btn-close"
            data-bs-dismiss="modal"
            aria-label="Закрыть"
          ></button>
        </div>

        <div class="modal-body text-center">
          <h1 id="hh" class="display-5 fw-bold"></h1>
        </div>

        <div class="modal-footer">
          <button
            type="button"
            class="btn btn-secondary"
            data-bs-dismiss="modal"
          >
            Закрыть
          </button>
        </div>

      </div>
    </div>
  </div>

  <script src="./dist/main.js"></script>

  <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/js/bootstrap.bundle.min.js"></script>
</body>
</html>
```

## JavaScript-код

```js
import { DateTime } from 'luxon';

const timeElement = document.getElementById('hh');

function showCurrentTime() {
  timeElement.textContent = DateTime
    .local()
    .setLocale('ru')
    .toFormat('dd.LL.y HH:mm:ss');
}

showCurrentTime();

setInterval(showCurrentTime, 1000);
```

## Результат

В результате было создано приложение с использованием Bootstrap 5, Webpack и Luxon. Приложение отображает текущее время во всплывающем окне Bootstrap. Кнопка расположена в центральной колонке сетки Bootstrap и занимает всю её ширину.

## Скриншоты результата

### HTML-код страницы

![HTML-код страницы](/images/bootstrap-luxon-code.png)

### Внешний вид приложения

![Внешний вид приложения](/images/bootstrap-luxon-result.png)