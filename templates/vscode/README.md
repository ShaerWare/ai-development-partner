# Интеграция с VS Code через Continue

[Continue](https://continue.dev) - это расширение для VS Code, которое позволяет использовать AI прямо в редакторе.

## Установка:

1. Установите расширение Continue из VS Code Marketplace
2. Откройте настройки Continue (Ctrl/Cmd + Shift + P → "Continue: Open config.json")
3. Замените содержимое файла на содержимое `continue-config.json`
4. В поле `systemMessage` вставьте содержимое `/prompts/system_prompt_full.md`
5. Добавьте ваши API ключи или настройте локальную модель

## Конфигурация:

### Для Claude API:
```json
{
  "title": "AI Dev Partner (Claude)",
  "provider": "anthropic",
  "model": "claude-3-opus-20240229",
  "apiKey": "sk-ant-...",
  "systemMessage": "ВАША_СИСТЕМА_ПРОМПТ"
}
```

### Для OpenAI API:
```json
{
  "title": "AI Dev Partner (GPT-4)",
  "provider": "openai",
  "model": "gpt-4-turbo",
  "apiKey": "sk-...",
  "systemMessage": "ВАША_СИСТЕМА_ПРОМПТ"
}
```

### Для локальных моделей (Ollama):
```json
{
  "title": "AI Dev Partner (Local)",
  "provider": "ollama",
  "model": "deepseek-coder:33b",
  "apiBase": "http://localhost:11434",
  "systemMessage": "ВАША_СИСТЕМА_ПРОМПТ"
}
```

## Использование:

### Быстрые команды:
- `Ctrl/Cmd + L` - Открыть чат с AI
- `Ctrl/Cmd + I` - Редактировать выделенный код
- `Ctrl/Cmd + Shift + R` - Использовать контекст проекта

### В чате можно использовать команды:
```
/tz для функции авторизации
/sprints для проекта интернет-магазина
/help
```

### Контекстное редактирование:
1. Выделите код
2. Нажмите `Ctrl/Cmd + I`
3. Опишите изменения: "Добавь валидацию", "Оптимизируй запрос"
4. AI применит изменения с учетом системного промпта

## Рекомендуемые настройки:

```json
{
  "models": [...],
  "contextProviders": [
    {
      "name": "code",
      "params": {}
    },
    {
      "name": "terminal",
      "params": {}
    },
    {
      "name": "problems",
      "params": {}
    },
    {
      "name": "folder",
      "params": {}
    }
  ],
  "slashCommands": [
    {
      "name": "edit",
      "description": "Edit highlighted code"
    },
    {
      "name": "comment",
      "description": "Write comments for code"
    },
    {
      "name": "test",
      "description": "Generate tests"
    }
  ]
}
```

## Tips:

1. **Используйте контекст проекта** - Continue автоматически передает контекст файлов
2. **Команды из промпта работают** - можете писать `/tz`, `/sprints` прямо в чате
3. **Настройте горячие клавиши** - для частых операций
4. **Используйте локальную модель** - для конфиденциальных проектов

## Troubleshooting:

**Проблема:** AI не следует промпту
- Проверьте, что `systemMessage` заполнен правильно
- Перезапустите VS Code

**Проблема:** Медленная работа
- Используйте меньшую модель для автодополнения
- Для чата оставьте мощную модель

**Проблема:** Ошибка API
- Проверьте API ключи
- Убедитесь, что у вас есть доступ к модели
