---
title: "HTTP Lab"
date: 2026-04-01
draft: false
---

# Отчёт по лабораторной работе
## Протокол HTTP. Клиент-серверное взаимодействие

## 1. GET-запрос через ncat (Dog API)

```bash
ncat --ssl dogapi.dog 443
```

```http
GET /api/v2/facts?limit=2 HTTP/1.1
Host: dogapi.dog

```

![GET через ncat](/images/get-ncat.png)

## 2. POST-запрос через ncat (httpbin)

```bash
ncat --ssl httpbin.org 443
```

```http
POST /post HTTP/1.1
Host: httpbin.org
Content-Type: application/json
Content-Length: 18

{"name":"Bach"}
```

![POST через ncat](/images/post-ncat.png)

## 3. GET-запрос через curl

```bash
curl "https://dogapi.dog/api/v2/facts?limit=2"
```

![GET через curl](/images/get-curl.png)

## 4. POST-запрос через curl

```bash
curl -X POST "https://httpbin.org/post" \
-H "Content-Type: application/json" \
-d '{"name":"Bach"}'
```

![POST через curl](/images/post-curl.png)

## 5. Запрос к API Банка России через Postman

```text
https://www.cbr.ru/scripts/XML_dynamic.asp?date_req1=01/01/2025&date_req2=01/02/2025&VAL_NM_RQ=R01235
```

![API Банка России](/images/cbr.png)

## Вывод

В ходе лабораторной работы были изучены HTTP-запросы и ответы, методы GET и POST, а также работа с публичными API с помощью ncat, curl и Postman.