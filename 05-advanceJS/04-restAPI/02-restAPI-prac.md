# Методи REST API у JavaScript

Цей документ описує приклади використання методів REST API (POST, DELETE, GET, PUT) для взаємодії з сервером за допомогою JavaScript.

## Константа базового URL

```javascript
const BASE_URL = "https://68598953138a18086dfec534.mockapi.io/prac";
```

## POST: Створення нового користувача

Створює нового користувача, відправляючи дані з форми на сервер.

```javascript
const btnPOST = document.querySelector("#post");

const createUserPOST = async () => {
  const users = {
    name: document.querySelector("#nickname").value,
    age: document.querySelector("#age").value,
  };

  try {
    const response = await fetch(BASE_URL, {
      method: "POST",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify(users),
    });

    if (!response.ok) {
      throw new Error(`HTTP error! status: ${response.status}`);
    }

    const data = await response.json();
  } catch (error) {
    console.log(error);
  }
};

btnPOST.addEventListener("click", (e) => {
  e.preventDefault();
  createUserPOST();
});
```

## DELETE: Видалення користувача

Видаляє користувача за вказаним ідентифікатором.

```javascript
const deleteUser = async () => {
  try {
    const response = await fetch(`${BASE_URL}/3`, {
      method: "DELETE",
    });

    const data = await response.json();
  } catch (error) {
    console.log(error);
  }
};
deleteUser();
```

## GET: Отримання користувача за ID

Отримує дані користувача за вказаним ID і відображає їх на сторінці.

```javascript
const articleGETid = document.querySelector("#contentForId");
const btnGETid = document.querySelector("#getID");

const getUserByIdGET = async () => {
  try {
    const response = await fetch(`${BASE_URL}/1`);
    const { name, age } = await response.json();
    const div = articleGETid.querySelector("div");
    div.innerHTML += `
      <div class="name">${name}</div>
      <div class="age">${age}</div>
     `;

    articleGETid.appendChild(div);
  } catch (error) {
    console.log(error);
  }
};

btnGETid.addEventListener("click", (e) => {
  e.preventDefault();
  getUserByIdGET();
});
```

## PUT: Оновлення даних користувача

Оновлює дані користувача за вказаним ID, відправляючи нові значення на сервер.

```javascript
const articlePUT = document.querySelector("#contentPUT");

const changeUserPUT = async () => {
  try {
    const response = await fetch(`${BASE_URL}/1`, {
      method: "PUT",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify({
        name: "yuri - change",
        age: "21 - change",
      }),
    });

    const { name, age } = await response.json();
    const div = articlePUT.querySelector("div");
    div.innerHTML += `
      <div class="name">${name}</div>
      <div class="age">${age}</div>
     `;

    articlePUT.appendChild(div);
  } catch (error) {
    console.log(error);
  }
};

btnPOST.addEventListener("click", (e) => {
  e.preventDefault();
  changeUserPUT();
});
```

## GET: Отримання всіх користувачів

Отримує список всіх користувачів і відображає їх на сторінці.

```javascript
const articleGET = document.querySelector("#contentAllUser");
const btnGET = document.querySelector("button[type='button']");

const fetchUsersGET = async () => {
  try {
    const response = await fetch(BASE_URL);
    const data = await response.json();
    data.forEach(({ name, age }) => {
      const div = articleGET.querySelector("div");

      div.innerHTML += `
      <div class="name">${name}</div>
      <div class="age">${age}</div>
     `;

      articleGET.appendChild(div);
    });
  } catch (error) {
    console.log(error);
  }
};

btnGET.addEventListener("click", (e) => {
  e.preventDefault();
  fetchUsersGET();
});
```
