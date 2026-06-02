# razd-action

GitHub Action для установки и настройки mise с razd CLI.

## Использование

```yaml
name: CI
on: [push]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: razd-cli/razd-action@v2
        with:
          mise-version: '2025.6.6'
          razd-version: 'latest'
          checkout-repository: 'true'

      - name: Use razd
        run: razd --version
```

## Входные параметры

| Параметр | Описание | Обязательный | По умолчанию |
|----------|----------|--------------|--------------|
| `mise-version` | Версия mise для установки | Да | `2025.6.6` |
| `razd-version` | Версия razd (`latest` или конкретная, например `1.2.3`) | Нет | `latest` |
| `checkout-repository` | Выполнить checkout репозитория | Нет | `true` |

## Что делает это действие

1. Выполняет checkout кода (если `checkout-repository` = `true`)
2. Устанавливает mise используя `jdx/mise-action`
3. Скачивает и устанавливает razd CLI напрямую из GitHub Releases
4. Проверяет установку

## Примеры использования

### Базовое использование
```yaml
- uses: razd-cli/razd-action@v2
```

### Минимальный workflow
```yaml
on: [push, pull_request]
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: razd-cli/razd-action@v2
      - run: razd install && razd build
```

### С конкретной версией razd
```yaml
- uses: razd-cli/razd-action@v2
  with:
    razd-version: '1.2.3'
```

### Без checkout (если checkout уже выполнен)
```yaml
- uses: razd-cli/razd-action@v2
  with:
    checkout-repository: 'false'
```

### Полный CI пример
```yaml
name: CI
on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: razd-cli/razd-action@v2
        with:
          mise-version: '2025.6.6'
          razd-version: 'latest'

      - name: Install dependencies
        run: razd install

      - name: Build
        run: razd build
```