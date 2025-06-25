# Методи промісів у JavaScript

Цей документ описує основні методи промісів у JavaScript з прикладами використання.

## Константи URL

```javascript
const usersUrl = "https://jsonplaceholder.typicode.com/users";
const postsUrl = "https://jsonplaceholder.typicode.com/posts";
```

## Promise.all

Очікує виконання всіх переданих промісів. Якщо хоча б один проміс відхиляється, всі проміси відхиляються.

```javascript
const promAll = async () => {
  try {
    const [userResult, postsResult] = await Promise.all([
      fetch(usersUrl),
      fetch(postsUrl),
    ]);

    const userResp = await userResult.json();
    const postsResp = await postsResult.json();

    console.log(postsResp);
    console.log(userResp);
  } catch (error) {
    console.log(error);
  }
};
```

## Promise.resolve

Одразу виконується зі статусом `fulfilled`.

```javascript
const promResolve = async () => {
  try {
    const response = await Promise.resolve(fetch(usersUrl));
    console.log(response);
  } catch (error) {
    console.log(error);
  }
};
```

## Promise.reject

Одразу виконується зі статусом `rejected`.

```javascript
const promReject = async () => {
  try {
    await Promise.reject("Rejected");
  } catch (error) {
    console.log(`Відлов помилки: ${error}`);
  }
};
```

## Promise.allSettled

Повертає масив об’єктів із результатами всіх промісів, незалежно від того, були вони виконані чи відхилені.

```javascript
const promAllSetled = async () => {
  try {
    const result = await Promise.allSettled([fetch(usersUrl), fetch(postsUrl)]);

    for (const res of result) {
      if (res.status === "fulfilled") {
        const data = await res.value.json();
        console.log(data);
      }
      if (res.status === "rejected") {
        throw new Error(`${res.reason}`);
      }
    }
  } catch (error) {
    console.log(`Відлов помилки: ${error}`);
  }
};
```

## Promise.race

Повертає результат першого завершеного промісу (виконаного або відхиленого).

```javascript
const promRace = async () => {
  try {
    const response = await Promise.race([fetch(usersUrl), fetch(postsUrl)]);
    if (!response.ok) {
      throw new Error("error");
    }
    const data = await response.json();
  } catch (error) {
    console.log(error);
  }
};
```

## Promise.any

Повертає перший успішний результат (`fulfilled`). Якщо всі проміси відхилено, повертає `AggregateError`.

```javascript
const promAny = async () => {
  try {
    const response = await Promise.any([fetch(usersUrl), fetch(postsUrl)]);
    if (!response.ok) {
      throw new Error("error");
    }
    const data = await response.json();
    console.log(data);
  } catch (error) {
    console.log(error);
  }
};
promAny();
```
