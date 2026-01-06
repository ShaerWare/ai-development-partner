# AI Development Partner - Полная версия для Claude

Это шаблон для использования с Claude (Anthropic). Скопируйте содержимое промта из `/prompts/system_prompt_full.md` и вставьте в Custom Instructions.

## Как установить:

1. Откройте [Claude.ai](https://claude.ai)
2. Нажмите на ваш профиль (правый верхний угол)
3. Выберите `Settings` → `Profile` → `Custom Instructions`
4. Скопируйте полное содержимое файла `/prompts/system_prompt_full.md`
5. Вставьте в поле Custom Instructions
6. Нажмите `Save`

## Настройка под ваш проект:

Отредактируйте следующие секции в промпте:

### Технический Стек
```yaml
OS: Ubuntu / Windows / macOS
Backend: PHP Laravel / Node.js / Python Django
Database: MySQL / PostgreSQL / MongoDB
```

### Стратегические Цели
```yaml
Automation: Заменить N сотрудников
Business Model: SaaS / E-commerce / API
Financial Goal: XXXк₽/мес
```

### Финансовые Параметры
```yaml
Developer Rate: XXXXк₽/неделя или XXX₽/час
Risk Buffer: 20%
ROI Period: X месяцев
```

## Проверка установки:

После установки отправьте команду:
```
/help
```

Если промпт установлен правильно, вы получите таблицу всех доступных команд.

## Что дальше:

1. Попробуйте простую команду: `/tz для системы авторизации`
2. Ознакомьтесь с [примерами использования](../../examples/)
3. Прочитайте [руководство по интеграции](../../docs/INTEGRATION_GUIDE.md)
