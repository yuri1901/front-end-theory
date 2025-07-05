# Конспект: Основи роботи з Git та SSH

**Git** — це система контролю версій для відстеження змін у коді та спільної роботи. Цей конспект охоплює основні команди Git, налаштування SSH для роботи з віддаленими репозиторіями (наприклад, GitHub) та пояснення ключових понять, таких як `.gitignore`, `staging area`, `origin` тощо. Він підходить для підготовки до співбесіди та роботи в Data Science.

## 🔹 Налаштування Git

### Перевірка встановлення

Переконайтеся, що Git встановлено:

```bash
git --version
# Виведе: git version 2.x.x
```

### Налаштування користувача

Встановіть ім’я та email для комітів:

```bash
git config --global user.name "Nikita"
git config --global user.email "nik@gmail.com"
```

### Перевірка налаштувань

Перегляньте всі налаштування:

```bash
git config --list
# Виведе: user.name=Nikita, user.email=nik@gmail.com, ...
```

### Встановлення редактора

Налаштуйте редактор для повідомлень комітів:

```bash
git config --global core.editor "notepad"
# Або для VS Code:
git config --global core.editor "code --wait"
```

### Довідка Git

Отримайте довідку:

```bash
git --help
```

## 🔹 Налаштування SSH для GitHub

### 1. Генерація SSH-ключа

Створіть SSH-ключ для безпечного доступу:

```bash
ssh-keygen -t ed25519 -C "nik@gmail.com"
# Якщо ed25519 недоступний:
ssh-keygen -t rsa -b 4096 -C "nik@gmail.com"
```

- Натисніть Enter для стандартного розташування (`~/.ssh/id_ed25519` або `id_rsa`).
- Парольна фраза необов’язкова (Enter для пропуску).

### 2. Запуск агента SSH

Переконайтеся, що агент SSH працює:

```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
# Для Windows, якщо помилка:
Get-Service ssh-agent | Set-Service -StartupType Manual
Start-Service ssh-agent
```

### 3. Копіювання публічного ключа

Скопіюйте ключ:

```bash
cat ~/.ssh/id_ed25519.pub
# Або для RSA:
cat ~/.ssh/id_rsa.pub
```

### 4. Додавання ключа до GitHub

1. Перейдіть до **Settings → SSH and GPG keys → New SSH key**.
2. У полі **Title** введіть назву (наприклад, "My Laptop").
3. Вставте скопійований ключ у поле **Key**.
4. Натисніть **Add SSH Key**.

### 5. Тестування з’єднання

Перевірте підключення:

```bash
ssh -T git@github.com
# Виведе: Hi username! You've successfully authenticated...
```

- Підтвердіть додавання GitHub до `known_hosts` (`yes`), якщо потрібно.

### 6. Перегляд SSH-файлів

Перегляньте файли в `~/.ssh`:

```bash
ls -al ~/.ssh
# Виведе: id_ed25519  id_ed25519.pub  known_hosts
```

Відкрийте директорію (macOS):

```bash
open ~/.ssh
```

## 🔹 Робота з Git-репозиторієм

### `git init`

Ініціалізує новий репозиторій, створюючи папку `.git`.

```bash
git init --initial-branch=main
ls -a
# Виведе: .git
```

**Примітка**: Папка `.git` містить метадані та історію. Не змінюйте її вручну!

### `git clone`

Клонує віддалений репозиторій.

```bash
git clone git@github.com:username/repository.git
```

### `git status`

Показує статус: змінені, додані чи невідстежувані файли.

```bash
git status
# Виведе: On branch main, modified files, untracked files
```

### `git add`

Додає файли до **staging area**.

```bash
touch file_name.txt
git add file_name.txt
git add .
# Додає всі змінені файли
```

### Staging Area

Проміжна область для підготовки змін до коміту.

### `.gitignore`

Вказує файли/папки, які Git ігнорує.

```
.DS_Store
.idea
dist
node_modules
```

- **Пояснення**:
  - `.DS_Store`: Метадані macOS.
  - `.idea`: Налаштування IntelliJ IDEA.
  - `dist`: Зібрані файли.
  - `node_modules`: Залежності npm.

### `git commit`

Фіксує зміни зі стейджингу.

```bash
git commit -m "Add file_name.txt"
git commit  # Відкриває редактор
```

### `git commit --amend`

Редагує останній коміт.

```bash
git add file.txt
git commit --amend --no-edit
```

### `git log`

Показує історію комітів.

```bash
git log
git log --oneline  # Компактний вигляд
git log -p  # Показує зміни (вийти: q)
```

### `git diff`

Показує відмінності.

```bash
git diff
git diff --cached  # Зміни в стейджингу
```

### `git restore`

Відновлює файли.

```bash
rm file.txt
git restore file.txt
# Відновлює з останнього коміту
git restore --source=abc123 file.txt
# Відновлює з коміту abc123
```

### `git rm`

Видаляє файл із робочої директорії та індексу.

```bash
git rm file.txt
git commit -m "Remove file.txt"
```

### `git clean`

Видаляє невідстежувані файли.

```bash
git clean -n  # Показує, що буде видалено
git clean -f  # Видаляє
```

### `git reset`

Скидає зміни зі стейджингу або історії.

```bash
git add file1.txt
git reset file1.txt  # Видаляє зі стейджингу
git reset --hard  # Скидає до останнього коміту
git reset --soft abc123  # Зберігає зміни, скидає історію
```

### `git show`

Показує зміни в коміті.

```bash
git show abc123
```

## 🔹 Робота з гілками

### `git branch`

Показує або створює гілки.

```bash
git branch
# Виведе: * main
git branch feature
```

### `git checkout`

Перемикається на гілку.

```bash
git checkout feature
```

### `git checkout -b`

Створює та перемикається на гілку.

```bash
git checkout -b new_branch_name
```

### `git merge`

Об’єднує гілки.

```bash
git checkout main
git merge feature
```

### `git rebase`

Переносить коміти на нову базу.

```bash
git checkout feature
git rebase main
git rebase --continue  # Після вирішення конфліктів
```

### `git branch -d` / `-D`

Видаляє гілку.

```bash
git branch -d feature
git branch -D feature  # Примусове видалення
```

## 🔹 Робота з віддаленим репозиторієм

### `git remote`

Керує віддаленими репозиторіями.

```bash
git remote -v
git remote add origin git@github.com:username/repository.git
```

### `git push`

Відправляє коміти до віддаленого репозиторію.

```bash
git push
git push origin main
```

- **Різниця**:

  - `git push`: Відправляє зміни з поточної гілки (якщо зв’язок налаштовано).
  - `git push origin main`: Явно вказує репозиторій і гілку.

- **Усунення помилки "Updates were rejected"**:
  ```bash
  git pull --rebase origin main
  git push origin main
  # Або (небезпечно!):
  git push --force origin main
  ```

### `git pull`

Завантажує та об’єднує зміни.

```bash
git pull origin main
```

### `origin`

Стандартна назва віддаленого репозиторію.

## 🔹 Скасування змін

### `git revert`

Створює коміт, що скасовує попередній.

```bash
git revert abc123
git revert --continue  # Після вирішення конфліктів
```

### `git restore --staged`

Видаляє файл зі стейджингу.

```bash
git add file1.txt
git restore --staged file1.txt
```

## 🔹 Тимчасове збереження змін

### `git stash`

Зберігає незакомічені зміни.

```bash
echo "Temp change" > file.txt
git stash
```

### `git stash pop`

Відновлює та видаляє зміни зі стека.

```bash
git stash pop
```

## 🔹 Типові запитання на співбесіді

### Теоретичні питання

1. Для чого потрібні `user.name` і `user.email` у Git?
2. Як налаштувати SSH для GitHub?
3. У чому різниця між `git merge` і `git rebase`?
4. Що таке `.gitignore`? Які файли додають?
5. Що таке staging area?
6. Як скасувати зміни за допомогою `git reset` і `git revert`?
7. Що робить `git stash`? Як відновити зміни?
8. Що означає `origin`?
9. Як вирішити конфлікт під час `git merge` чи `git rebase`?
10. Що виведе `git log --oneline`?

### Практичні питання

1. Налаштуйте Git для нового користувача.
2. Створіть SSH-ключ і підключіть до GitHub.
3. Клонуйте репозиторій і створіть гілку.
4. Напишіть `.gitignore`.
5. Зробіть зміни та коміт.
6. Об’єднайте гілку `feature` у `main`.
7. Збережіть і відновіть зміни.
8. Скасуйте останній коміт.
9. Відновіть файл із коміту.
10. Вирішіть конфлікт після `git pull`.

### Відповіді

#### Теоретичні

1. Ідентифікують автора комітів.
2. `ssh-keygen`, додати ключ до GitHub, перевірити `ssh -T`.
3. `merge` створює коміт злиття, `rebase` — лінійну історію.
4. Файл для ігнорування файлів/папок (наприклад, `.DS_Store`, `node_modules`).
5. Проміжна область для підготовки комітів.
6. `reset` видаляє коміти, `revert` створює коміт для скасування.
7. Зберігає зміни, відновлюється через `git stash pop`.
8. Назва віддаленого репозиторію.
9. Відредагуйте файли, `git add`, виконайте `git merge --continue` або `git rebase --continue`.
10. Скорочену історію комітів.

#### Практичні

1. ```bash
   git config --global user.name "Nikita"
   git config --global user.email "nik@gmail.com"
   ```
2. ```bash
   ssh-keygen -t ed25519 -C "nik@gmail.com"
   eval "$(ssh-agent -s)"
   ssh-add ~/.ssh/id_ed25519
   cat ~/.ssh/id_ed25519.pub
   ssh -T git@github.com
   ```
3. ```bash
   git clone git@github.com:username/repo.git
   cd repo
   git checkout -b feature
   ```
4. ```
   .DS_Store
   .idea
   dist
   node_modules
   ```
5. ```bash
   touch file.txt
   echo "Hello" > file.txt
   git add file.txt
   git commit -m "Add file.txt"
   ```
6. ```bash
   git checkout main
   git merge feature
   ```
7. ```bash
   git stash
   git stash pop
   ```
8. ```bash
   git reset HEAD^
   ```
9. ```bash
   git restore --source=abc123 file.txt
   git add file.txt
   git commit -m "Restore file.txt"
   ```
10. Відредагуйте файли, потім:
    ```bash
    git add .
    git merge --continue
    ```
