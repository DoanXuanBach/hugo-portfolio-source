---

title: "Создание проекта с использованием Webpack и Docker"

date: 2026-04-25

draft: false

---



# Создание проекта с использованием Webpack и Docker



## 1. Цель работы



Цель работы — создать базовый проект с использованием Webpack, подключить библиотеку Luxon, добавить Bootstrap через CDN, выполнить сборку проекта, а также запустить приложение внутри Docker-контейнера.



В ходе работы были использованы:



- Node.js;

- npm;

- Webpack;

- Luxon;

- Bootstrap CDN;

- Docker;

- образ `node:24-alpine`.



---



## 2. Установка Node.js



Node.js был установлен на Windows через официальный установщик.



После установки была выполнена проверка версий:



```cmd

node -v

v24.15.0



npm -v

11.12.1

```



Это подтверждает, что Node.js и npm были успешно установлены и доступны из командной строки.



---



## 3. Создание проекта



Для создания проекта была создана отдельная папка проекта.



Затем были выполнены команды:



```cmd

npm init -y

npm i luxon

npm i -D webpack webpack-cli serve

```



Команда `npm init -y` создала файл `package.json`.



Библиотека `luxon` используется для работы с датой и временем.



Пакеты `webpack`, `webpack-cli` и `serve` были установлены как dev-зависимости.



---



## 4. Файл `src/index.js`



В папке `src` был создан файл `index.js`.



Содержимое файла:



```js

const { DateTime } = require('luxon');



setInterval(() => {

&#x20; hh.textContent = DateTime

&#x20;   .local()

&#x20;   .setLocale('ru')

&#x20;   .toFormat('dd.LL.y HH:mm:ss');

}, 1000);

```



В этом коде библиотека Luxon используется для получения текущей даты и времени.



Функция `setInterval` обновляет значение на странице каждую секунду.



---



## 5. Сборка проекта с помощью Webpack



Для сборки проекта была выполнена команда:



```cmd

npx webpack

```



Результат сборки:



![Результат сборки Webpack](/images/webpack-docker/webpack-build.png)



На скриншоте видно, что Webpack успешно собрал файл `main.js`.



---



## 6. Подключение Bootstrap CDN и вывод Luxon на страницу



В файл `index.html` был добавлен Bootstrap через CDN.



Фрагмент подключения Bootstrap:



```html

<link

&#x20; href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css"

&#x20; rel="stylesheet"

>

```



Также на странице был реализован крупный вывод даты и времени, построенный с помощью библиотеки Luxon.



Внешний вид страницы:



![Страница с Bootstrap и Luxon](/images/webpack-docker/luxon-page.png)



На странице отображается крупный блок с текущей датой и временем.



---



## 7. Dockerfile



Для запуска приложения в Docker был создан файл `Dockerfile`.



Содержимое `Dockerfile`:



```dockerfile

FROM node:24-alpine



WORKDIR /app



COPY package\*.json ./



RUN npm install



COPY . .



RUN npx webpack



EXPOSE 3000



CMD \["npx", "serve", ".", "-l", "3000"]

```



В данном файле используется образ `node:24-alpine`.



Команда `RUN npm install` устанавливает зависимости проекта.



Команда `RUN npx webpack` выполняет сборку проекта внутри контейнера.



Команда `CMD \["npx", "serve", ".", "-l", "3000"]` запускает приложение на порту 3000.



---



## 8. Сборка и запуск Docker-контейнера



Для сборки Docker-образа была выполнена команда:



```cmd

docker build -t webpack2026-app .

```



Для запуска контейнера была выполнена команда:



```cmd

docker run --rm -p 3000:3000 webpack2026-app

```



После запуска приложение стало доступно по адресу:



```text

http://localhost:3000/

```



Скриншот запуска приложения с помощью Docker:



![Запуск приложения через Docker](/images/webpack-docker/docker-run.png)



На скриншоте видно, что контейнер был запущен, сервер принимает соединения на `http://localhost:3000`, а приложение успешно открывается в браузере.



---



## 9. Последовательность действий для запуска



Для запуска проекта локально необходимо выполнить команды:



```cmd

npm install

npx webpack

npx serve .

```



Для запуска проекта через Docker необходимо выполнить команды:



```cmd

docker build -t webpack2026-app .

docker run --rm -p 3000:3000 webpack2026-app

```



После этого приложение открывается в браузере по адресу:



```text

http://localhost:3000/

```



---



## 10. Вывод



В результате работы был создан проект с использованием Webpack.



Была подключена библиотека Luxon для вывода текущей даты и времени.



Bootstrap был подключен через CDN для оформления страницы.



Также был создан Dockerfile на основе образа `node:24-alpine`, после чего приложение было собрано и запущено внутри Docker-контейнера.

