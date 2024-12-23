# Meteora Position Manager

Автоматизированный менеджер позиций для Meteora DeFi на Solana.

## 🛠 Предварительные требования

- установите Node.js

## 📝 Конфигурация

### Настройка конфига (src/config/index.js)

```javascript
// Настройки RPC и прокси
const RPC_CONFIG = {
    USE_MULTI_RPC: 1,    // 0 - один RPC, 1 - несколько RPC
    USE_MULTI_PROXY: 1,  // 0 - без прокси, 1 - с прокси
    POOL_SIZE: 5         // Количество одновременных соединений (рекомендуется 5-10)
};

// Вставьте свои RPC URL
const RPC_ENDPOINTS = [
    "https://your-rpc-1.com",
    "https://your-rpc-2.com"
    // Можно добавить больше RPC
];

// Вставьте свои прокси в формате: "ip:port:username:password"
const PROXY_LIST = [
    "11.99.99.99:9999:user:pass",
    "55.99.99.99:9999:user:pass"
    // Можно добавить больше прокси
];

export const WALLETS = {
    "1": {
        privateKey: "Your Private Key",
        description: "Your Wallet Address"
    },
    "2": {
        privateKey: "Your Private Key2",
        description: "Your Wallet Address2"
    },
    // Добавьте дополнительные кошельки по необходимости
};

export const TOTAL_RANGE_INTERVAL = 68; // Диапазон для позиций (максимальное значение 69)
```

### Подробная настройка RPC и прокси

1. **Настройка режима работы:**
   - `USE_MULTI_RPC: 0` - Использовать только один RPC (первый из списка)
   - `USE_MULTI_RPC: 1` - Использовать все RPC по очереди
   - `USE_MULTI_PROXY: 0` - Не использовать прокси
   - `USE_MULTI_PROXY: 1` - Использовать прокси
   - `POOL_SIZE` - количество одновременных соединений:
     - 5 - для обычной работы
     - 10 - для интенсивной работы
     - 3 - для легкой нагрузки

2. **Добавление RPC:**
   ```javascript
   const RPC_ENDPOINTS = [
       "https://mainnet.helius-rpc.com/?api-key=ваш-ключ-1",
       "https://mainnet.helius-rpc.com/?api-key=ваш-ключ-2"
   ];
   ```
   - Арендуйте RPC на сайтах:
     - [Helius](https://helius.xyz/)
     - [QuickNode](https://quicknode.com/)

3. **Добавление прокси:**
   ```javascript
   const PROXY_LIST = [
       "ip:port:username:password",
       "ip:port:username:password"
   ];
   ```
   - Формат: "IP:ПОРТ:ЛОГИН:ПАРОЛЬ"
   - Пример: "192.168.1.1:8080:user123:pass456"
   - Рекомендуется использовать приватные прокси

4. **Примеры настройки:**
   
   Только один RPC без прокси:
   ```javascript
   const RPC_CONFIG = {
       USE_MULTI_RPC: 0,
       USE_MULTI_PROXY: 0,
       POOL_SIZE: 3
   };
   const RPC_ENDPOINTS = ["https://ваш-rpc-url"];
   const PROXY_LIST = [];
   ```

   Несколько RPC с прокси:
   ```javascript
   const RPC_CONFIG = {
       USE_MULTI_RPC: 1,
       USE_MULTI_PROXY: 1,
       POOL_SIZE: 5
   };
   const RPC_ENDPOINTS = [
       "https://rpc1.com/?api-key=ключ1",
       "https://rpc2.com/?api-key=ключ2"
   ];
   const PROXY_LIST = [
       "11.22.33.44:8080:user1:pass1",
       "55.66.77.88:8080:user2:pass2"
   ];
   ```

## 🚀 Использование

Запустите программу находясь в директории проекта:
```bash
node main
```

### Основные функции:

1. **Добавить ликвидность**
   - В токенах (Открывает BidAsk позицию в токенах)
   - В SOL (Открывает BidAsk позицию в SOL)

2. **Удалить ликвидность**
   - Закрытие выбранных позиций

3. **Переоткрыть позицию**
   - Закрытие и открытие позиции в новом диапазоне

4. **Кошельки**
   - Проверка позиций (Проверяет все позиции в кошельке)
   - Проверка баланса (Проверяет баланс кошельков)
   - Консолидация (Консолидирует токены/SOL на основной кошелек)
   - Распределение SOL (Распределяет SOL на все кошельки)

5. **Чекер пулов**
   - Ищет пуллы по контракту токена

6. **Авточекер позиций**
   - При выходе из ренжа закрывает позиции и продает токены
   - При выходе из ренжа открывает новые позиции в токенах

## 📊 Мониторинг позиций

### Авточекер имеет два режима работы:

1. **Закрытие и продажа**
   - Закрывает позиции при выходе из ренжа
   - Консолидирует токены на основной кошелек
   - Продает все токены

2. **Переоткрытие позиций**
   - Закрывает позиции при выходе из ренжа
   - Автоматически открывает новые позиции в токенах
   - Продолжает мониторинг новых позиций

## ⚠️ Важное замечание

Лучше дважды делайте проверки перед повторными закрытиями/открытиями позиций, так как апишка метеоры может подтупливать


## Саппорт
По всем вопросам обращайтесь:
- Telegram: @sectordot

Телеграм канал: 
- Telegram: @sectormoves
