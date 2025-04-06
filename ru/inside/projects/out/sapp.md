---
title: SApp
description: 
published: true
date: 2025-04-06T23:03:53.833Z
tags: 
editor: markdown
dateCreated: 2025-04-06T23:03:53.833Z
---

```markdown
# Техническое задание: Реализация мессенджера с сквозным шифрованием на основе криптокошельков с использованием FSD и Next.js

## Цель проекта
Разработать децентрализованное веб-приложение (dApp) — мессенджер с поддержкой сквозного шифрования сообщений, использующий криптокошельки пользователей (например, MetaMask) для обеспечения безопасности. Приложение должно быть:
- Удобным
- Производительным
- Современным
- С быстрой сборкой и горячей перезагрузкой

**Архитектура:** Feature-Sliced Design (FSD) + Next.js

## Основные требования
### Шифрование
- Сообщения шифруются публичным ключом получателя
- Расшифровка через приватный ключ кошелька
- Использование сессионного ключа для UX

### Удобство
- Однократное подтверждение доступа за сессию
- Интуитивный интерфейс

### Совместимость
- Поддержка MetaMask-совместимых кошельков:
  - Trust Wallet
  - SafePal
  - Другие EVM-кошельки

### Безопасность
- Приватные ключи хранятся исключительно в кошельке
- Нет доступа к sensitive-данным из приложения

### Производительность
- Турбо-сборка Next.js (`next dev --turbo`)
- Оптимизированные продакшен-билды

## Техническая архитектура
### Стек технологий (2023)
| Категория       | Технологии                                                                 
|-----------------|----------------------------------------------------------------------------|
| Фронтенд        | Next.js, TypeScript, FSD                                                   |
| Кошельки        | ethers.js , @metamask/eth-sig-util                                         |
| Шифрование      | ECIES, Web Crypto API (AES-GCM)                                            |
| Хранение данных | IPFS через Infura                                                          |
| Состояние       | Effector, Next.js App Router                                               |
| Стили           | Styled-components                                                          |
| Тестирование    | Jest, Cypress                                                              |
| Инфраструктура  | Node.js , pnpm                                                             |

## Механика работы
### 1. Подключение кошелька
```typescript
// src/shared/lib/wallet.ts
import { ethers } from 'ethers';

export async function connectWallet() {
  const provider = new ethers.BrowserProvider(window.ethereum);
  await provider.send('eth_requestAccounts', []);
  const signer = await provider.getSigner();
  return {
    address: await signer.getAddress(),
    encryptionPublicKey: await window.ethereum.request({
      method: 'eth_getEncryptionPublicKey',
      params: [address]
    })
  };
}
```

### 2. Генерация сессионного ключа
```typescript
// src/shared/lib/crypto.ts
export async function generateSessionKey(publicKey: string) {
  const key = await crypto.subtle.generateKey(
    { name: 'AES-GCM', length: 256 }, 
    true, 
    ['encrypt', 'decrypt']
  );
  const exportedKey = await crypto.subtle.exportKey('raw', key);
  return {
    encryptedKey: encrypt({ publicKey, data: Buffer.from(exportedKey).toString('base64') }),
    key
  };
}
```

### 3. Шифрование сообщения
```typescript
// src/features/chat/lib/encrypt.ts
export async function encryptMessage(sessionKey: CryptoKey, message: string) {
  const iv = crypto.getRandomValues(new Uint8Array(12));
  const encrypted = await crypto.subtle.encrypt(
    { name: 'AES-GCM', iv }, 
    sessionKey, 
    new TextEncoder().encode(message)
  );
  return JSON.stringify({
    encryptedMessage: Buffer.from(encrypted).toString('base64'),
    iv: Buffer.from(iv).toString('base64')
  });
}
```

### 4. Отправка сообщения в IPFS
```typescript
// src/shared/lib/ipfs.ts
import { create } from 'ipfs-http-client';

export async function sendMessage(encryptedMessage: string) {
  const { cid } = await ipfs.add(encryptedMessage);
  return cid.toString();
}
```

## Структура проекта (FSD)
```
messenger-dapp/
├── src/
│   ├── app/               # Глобальные настройки
│   ├── features/          # Функциональные модули
│   │   └── chat/          # Модуль чата
│   ├── entities/          # Бизнес-сущности
│   ├── shared/            # Общие ресурсы
│   └── widgets/           # Композитные компоненты
├── tests/                 # Юниты и E2E тесты
└── конфигурационные файлы
```

## Оптимизация разработки
- **Инкрементальная сборка TS:** `tsconfig.json → "incremental": true`
- **Кэширование pnpm:** `pnpm install --frozen-lockfile`


---
*Все примеры кода приведены в сокращенном виде. Полная реализация требует дополнительной обработки ошибок и оптимизаций.*
```