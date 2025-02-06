# Telegram Logger

Telegram Logger — это библиотека для отправки логов в Telegram-чат с поддержкой кеширования, троттлинга и форматирования сообщений.

## ✨ Возможности

- ✅ Логирование ошибок, предупреждений и информационных сообщений в Telegram
- ✅ Кеширование отправленных сообщений для избежания дублирования
- ✅ Ограничение частоты отправки (Throttle)
- ✅ Поддержка форматирования текста (жирный, курсив, код и т. д.)
- ✅ Гибкая настройка

## 🔧 Установка

```sh
npm install telegram-logger
```

## 💪 Использование

### 1. Создание логгера

```ts
import { TelegramLogger } from 'telegram-logger'

const logger = new TelegramLogger({
  clientOptions: {
    chatId: '<YOUR_CHAT_ID>',
    token: '<YOUR_BOT_TOKEN>',
    cache: {
      maxSize: 10_000,
      ttl: Date.now() + 300 * 1000, // 5 минут
    },
    throttle: {
      interval: 1000 * 10, // 10 секунд
      limit: 20,
      maxSize: 10_000,
    },
    debug: true,
  },
})
```

### 2. Отправка сообщений

```ts
logger.log('Hello, Telegram!')
```

### 3. Форматирование сообщений

```ts
import { TelegramLoggerMessageBuilder } from 'telegram-logger'

const error = new TelegramLoggerMessageBuilder()
  .bold('❗ Ошибка')
  .enter(2)
  .underline('Описание:')
  .enter()
  .code('Ошибка 429: Слишком много запросов')
  .get()

logger.log(error)
```

## 🌟 Пример

```ts
const warn = new TelegramLoggerMessageBuilder()
  .bold('⚠️ Предупреждение')
  .enter(2)
  .underline('Сообщение:')
  .enter()
  .code('Загруженность сервера высокая!')
  .get()

logger.log(warn)
```

## 🔧 Опции

### TelegramLoggerOptions

| Опция      | Тип       | Описание                               |
| ---------- | --------- | -------------------------------------- |
| `chatId`   | `string`  | ID чата Telegram                       |
| `token`    | `string`  | Токен Telegram-бота                    |
| `cache`    | `object`  | Настройки кеширования                  |
| `throttle` | `object`  | Настройки ограничения частоты отправки |
| `debug`    | `boolean` | Включение режима отладки               |

## 🚀 Разработка

1. Клонируйте репозиторий:
   ```sh
   git clone https://github.com/your-repo/telegram-logger.git
   ```
2. Установите зависимости:
   ```sh
   npm install
   ```
3. Запустите тесты:
   ```sh
   npm test
   ```
