# CICD Learning Project

Цей проект містить комплексні приклади використання GitHub Actions для вивчення CI/CD процесів. Включає 13 різних workflow файлів, що демонструють різні аспекти автоматизації.

## Структура проекту

```
CICD Learning/
├── .github/workflows/
│   ├── actions_checkout.yml         # Робота з checkout action
│   ├── comand_git_copy_files.yml    # Git команди та копіювання файлів
│   ├── context_and_expresion.yml    # Контексти та вирази GitHub Actions
│   ├── filters_action_workflow.yml  # Фільтри для тригерів workflow
│   ├── first_workflow.yml           # Базовий workflow
│   ├── manual_workkflow.yml         # Ручний запуск workflow
│   ├── parallel_workflow_first.yml  # Перший паралельний workflow
│   ├── parallel_workflow_second.yml # Другий паралельний workflow
│   ├── parallel_workflow.yml        # Паралельне виконання jobs
│   ├── repo_workflow.yml            # Repository dispatch workflow
│   ├── workflof_start_if.yml        # Workflow з помилкою (для тестування)
│   ├── workflow_dispatch.yml        # Workflow з користувацькими входами
│   └── workflow_if_start.yml        # Умовне виконання на основі статусу
└── index.html                       # Простий HTML файл
```

## GitHub Actions Workflows

### Базові Workflows

#### 1. First Workflow (`first_workflow.yml`)
**Тригер:** Push до репозиторію  
**Призначення:** Базовий приклад workflow  
**Що робить:**
- Виводить текст
- Показує версії Node.js та npm

#### 2. Manual Workflow (`manual_workkflow.yml`)
**Тригер:** Ручний запуск (`workflow_dispatch`)  
**Призначення:** Демонструє ручний запуск  
**Що робить:**
- Виводить текст про ручний запуск
- Показує версію Node.js

### Actions та Git

#### 3. Actions Checkout (`actions_checkout.yml`)
**Тригер:** Push до репозиторію  
**Призначення:** Демонструє роботу з `actions/checkout`  
**Що робить:**
- Показує файли до checkout
- Виконує checkout коду
- Показує файли після checkout

#### 4. Command Git Copy Files (`comand_git_copy_files.yml`)
**Тригер:** Push до репозиторію  
**Призначення:** Демонструє Git команди  
**Що робить:**
- Показує файли в директорії
- Ініціалізує Git репозиторій
- Додає remote origin
- Виконує fetch та checkout

### Контексти та Вирази

#### 5. Context and Expression (`context_and_expresion.yml`)
**Тригер:** Push до репозиторію  
**Призначення:** Демонструє використання контекстів  
**Що робить:**
- Виводить `github` контекст (метадані репозиторію)
- Виводить `runner` контекст (система виконання)
- Виводить `job` контекст (поточне завдання)
- Виводить `steps` контекст (кроки workflow)

### Фільтри та Умови

#### 6. Filters Action Workflow (`filters_action_workflow.yml`)
**Тригер:** Push з фільтрами  
**Призначення:** Демонструє фільтрацію подій  
**Умови запуску:**
- Гілки: `main`, `page/*`, `page/**`
- Виключення: `page/blog`
- Теги: `v1.*` (виключення `v2.1.2`)

#### 7. Workflow If Start (`workflow_if_start.yml`)
**Тригер:** Після завершення `Workflow Start If`  
**Призначення:** Умовне виконання на основі статусу  
**Що робить:**
- Запускається при успішному завершенні попереднього workflow
- Запускається при помилці попереднього workflow

### Паралельне виконання

#### 8. Parallel Workflow (`parallel_workflow.yml`)
**Тригер:** Push до репозиторію  
**Призначення:** Демонструє паралельне виконання jobs  
**Jobs:**
- `run-first-command` (Ubuntu) - показує версію Node.js
- `run-parallel-command` (Windows) - показує версію Node.js
- `run-second-command` (macOS) - залежить від першого job

#### 9. Parallel Workflow First (`parallel_workflow_first.yml`)
**Тригер:** Push до репозиторію  
**Призначення:** Перший workflow в ланцюжку  
**Що робить:**
- Виводить текст "First workflow"

#### 10. Parallel Workflow Second (`parallel_workflow_second.yml`)
**Тригер:** Після завершення `Parallel Workflow First`  
**Призначення:** Другий workflow в ланцюжку  
**Що робить:**
- Виводить текст "Second workflow"

### Зовнішні події

#### 11. Repository Workflow (`repo_workflow.yml`)
**Тригер:** `repository_dispatch` з типом `hello`  
**Призначення:** Демонструє роботу з зовнішніми подіями  
**Що робить:**
- Отримує кастомний заголовок з payload події

#### 12. Workflow Dispatch (`workflow_dispatch.yml`)
**Тригер:** Ручний запуск з входами  
**Призначення:** Демонструє користувацькі входи  
**Входи:**
- `title_custom` (string) - кастомний заголовок
- `select_custom` (choice) - вибір з опцій
- `checkbox_custom` (boolean) - чекбокс

### Тестування помилок

#### 13. Workflow Start If (`workflof_start_if.yml`)
**Тригер:** Push до репозиторію  
**Призначення:** Workflow з навмисною помилкою  
**Що робить:**
- Намагається виконати неіснуючу команду `lshggha`
- Виводить статус workflow

## Як використовувати

### Базові команди

1. **Клонуйте репозиторій:**
   ```bash
   git clone <repository-url>
   cd "CICD Learning"
   ```

2. **Запустіть різні типи workflows:**
   
   **Автоматичні workflows (при push):**
   - `first_workflow.yml` - базовий приклад
   - `actions_checkout.yml` - робота з checkout
   - `parallel_workflow.yml` - паралельне виконання
   - `context_and_expresion.yml` - контексти
   - `filters_action_workflow.yml` - з фільтрами (тільки main, page/*)
   
   **Ручні workflows:**
   - `manual_workkflow.yml` - простий ручний запуск
   - `workflow_dispatch.yml` - з користувацькими входами
   
   **Зовнішні події:**
   - `repo_workflow.yml` - через repository_dispatch API

### Приклади запуску

#### Repository Dispatch
```bash
curl -X POST \
  -H "Authorization: token YOUR_TOKEN" \
  -H "Accept: application/vnd.github.v3+json" \
  https://api.github.com/repos/OWNER/REPO/dispatches \
  -d '{"event_type":"hello","client_payload":{"title_custom":"My Custom Title"}}'
```

#### Тегування для фільтрів
```bash
git tag v1.0.0
git push origin v1.0.0
```

### Перегляд результатів

1. Відкрийте вкладку **Actions** у GitHub
2. Оберіть відповідний workflow run
3. Перегляньте логи виконання
4. Для паралельних workflows - переглядайте окремо кожен job

## Категорії Workflows

### 🚀 Базові
- `first_workflow.yml` - найпростіший приклад
- `manual_workkflow.yml` - ручний запуск

### 🔧 Actions та Git
- `actions_checkout.yml` - робота з кодом
- `comand_git_copy_files.yml` - Git команди

### 📊 Контексти та Дані
- `context_and_expresion.yml` - доступ до метаданих

### 🎯 Фільтри та Умови
- `filters_action_workflow.yml` - фільтрація подій
- `workflow_if_start.yml` - умовне виконання

### ⚡ Паралельність
- `parallel_workflow.yml` - одночасне виконання
- `parallel_workflow_first.yml` + `parallel_workflow_second.yml` - ланцюжок

### 🌐 Зовнішні події
- `repo_workflow.yml` - API тригери
- `workflow_dispatch.yml` - користувацькі входи

### 🐛 Тестування
- `workflof_start_if.yml` - workflow з помилкою

## Корисні посилання

- [GitHub Actions Documentation](https://docs.github.com/en/actions)
- [Workflow Syntax](https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions)
- [Contexts and Expression Syntax](https://docs.github.com/en/actions/learn-github-actions/contexts)
- [Events that trigger workflows](https://docs.github.com/en/actions/using-workflows/triggering-a-workflow)
- [Using conditions](https://docs.github.com/en/actions/using-workflows/using-conditions)
- [Using concurrency](https://docs.github.com/en/actions/using-workflows/using-concurrency)

## Примітки

- **Runners:** Ubuntu, Windows, macOS (залежно від workflow)
- **Призначення:** Навчальний проект для вивчення CI/CD
- **Складність:** Від базових до середніх прикладів
- **HTML файл:** Містить базову інформацію про GitHub Actions
