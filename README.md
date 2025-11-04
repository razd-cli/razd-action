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
      - uses: razd-cli/razd-action@v1.0.1
        with:
          mise-version: '2025.11.2'
          checkout-repository: 'true'
      
      - name: Use razd
        run: razd --version
```

## Входные параметры

| Параметр | Описание | Обязательный | По умолчанию |
|----------|----------|--------------|--------------|
| `mise-version` | Версия mise для установки | Да | `2025.11.2` |
| `checkout-repository` | Выполнить checkout репозитория | Нет | `true` |

## Что делает это действие

1. Выполняет checkout кода (если `checkout-repository` = `true`)
2. Устанавливает mise используя `jdx/mise-action`
3. Добавляет razd плагин
4. Устанавливает razd глобально
5. Проверяет установку

## Примеры использования

### Базовое использование
```yaml
- uses: razd-cli/razd-action@v1.0.1
```

### Минимальный workflow
```yaml
on: [push, pull_request]
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: razd-cli/razd-action@v1.0.1
      - run: razd install && razd build
```

### С кастомными параметрами
```yaml
- uses: razd-cli/razd-action@v1.0.1
  with:
    mise-version: '2025.11.2'
    checkout-repository: 'false'  # если checkout уже выполнен
```