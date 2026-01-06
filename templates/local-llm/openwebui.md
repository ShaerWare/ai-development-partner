# AI Development Partner для Open WebUI

Open WebUI - это интерфейс для работы с локальными LLM (Ollama, LM Studio и др.).

## Предварительные требования:

- Установленный [Open WebUI](https://github.com/open-webui/open-webui)
- Локальная LLM (рекомендуется: Llama 3, Mixtral, DeepSeek Coder)
- Минимум 16GB RAM (для моделей 7B-13B)

## Установка промпта:

### Способ 1: System Prompt для модели

1. Откройте Open WebUI
2. Перейдите в `Settings` (иконка шестеренки)
3. Выберите `Models`
4. Найдите вашу модель и нажмите на иконку редактирования
5. В поле `System Prompt` вставьте содержимое:
   - `/prompts/system_prompt_full.md` (для мощных моделей 30B+)
   - `/prompts/system_prompt_mini.md` (для моделей 7B-13B)
6. Сохраните изменения

### Способ 2: Modelfile (рекомендуется)

Создайте файл `Modelfile`:

```dockerfile
FROM llama3:latest

# Загружаем системный промпт
SYSTEM """
[Вставьте сюда содержимое system_prompt_full.md]
"""

# Параметры для лучшей работы с кодом
PARAMETER temperature 0.7
PARAMETER top_p 0.9
PARAMETER top_k 40
PARAMETER num_ctx 8192

# Настройки для технических задач
PARAMETER stop "<|endoftext|>"
PARAMETER stop "<|im_end|>"
```

Создайте модель:
```bash
ollama create ai-dev-partner -f Modelfile
```

Используйте в Open WebUI:
```bash
# В чате выберите модель "ai-dev-partner"
```

### Способ 3: Custom Personality (Персона)

1. В Open WebUI перейдите в `Workspace` → `Prompts`
2. Нажмите `+ Create Prompt`
3. Заполните:
   - **Name:** AI Development Partner
   - **Content:** Содержимое `system_prompt_full.md`
   - **Type:** System Prompt
4. Сохраните и активируйте для нужных чатов

## Рекомендуемые модели:

### Для разработки кода:
```bash
# DeepSeek Coder (лучший для кода)
ollama pull deepseek-coder:33b

# CodeLlama (специализирован на коде)
ollama pull codellama:34b

# Llama 3 (универсальный)
ollama pull llama3:70b
```

### Для ограниченных ресурсов:
```bash
# Llama 3 8B (хорошее качество, 16GB RAM)
ollama pull llama3:8b

# Mixtral 8x7B (качественный, 32GB RAM)
ollama pull mixtral:8x7b
```

## Настройка параметров генерации:

В Open WebUI → Settings → Models → Advanced:

```yaml
Temperature: 0.7          # Баланс креативности/точности
Top P: 0.9               # Nucleus sampling
Top K: 40                # Разнообразие токенов
Context Length: 8192     # Размер контекста (увеличьте для больших задач)
Max Tokens: 4096         # Максимальная длина ответа
```

## Проверка работы:

Отправьте в чат:
```
/help
```

Если модель отвечает таблицей команд - промпт работает корректно.

## Оптимизация производительности:

### Для GPU (NVIDIA):
```bash
# Используйте GPU для ускорения
docker run -d --gpus all -p 3000:8080 \
  -v open-webui:/app/backend/data \
  --name open-webui ghcr.io/open-webui/open-webui:cuda
```

### Для CPU:
```bash
# Включите оптимизации для CPU
OLLAMA_NUM_GPU=0 ollama serve
```

### Для Apple Silicon (M1/M2/M3):
```bash
# Metal acceleration работает автоматически
ollama pull llama3:70b
# Модель будет использовать unified memory
```

## Интеграция с vLLM:

Если используете vLLM для высокой производительности:

```bash
# Запуск vLLM сервера
python -m vllm.entrypoints.openai.api_server \
  --model deepseek-ai/deepseek-coder-33b-instruct \
  --trust-remote-code \
  --tensor-parallel-size 2

# Подключите в Open WebUI через OpenAI API endpoint
# Settings → Connections → OpenAI API → http://localhost:8000/v1
```

## Troubleshooting:

**Проблема:** Модель не следует промпту
- **Решение:** Убедитесь, что промпт в System Prompt, а не в User Message

**Проблема:** Слишком медленная генерация
- **Решение:** Используйте модель меньшего размера или vLLM

**Проблема:** Модель забывает контекст
- **Решение:** Увеличьте `num_ctx` в Modelfile до 16384 или 32768

## Дополнительные ресурсы:

- [Open WebUI Documentation](https://docs.openwebui.com)
- [Ollama Model Library](https://ollama.com/library)
- [vLLM Documentation](https://docs.vllm.ai)
