---
title: SApp
description: 
published: true
date: 2025-04-07T00:40:47.394Z
tags: 
editor: markdown
dateCreated: 2025-04-06T23:03:53.833Z
---


# Техническое задание: Реализация мессенджера с сквозным шифрованием на основе криптокошельков с использованием FSD и Next.js

## Цель проекта
Разработать децентрализованное веб-приложение (dApp) — мессенджер с поддержкой сквозного шифрования сообщений, использующий криптокошельки пользователей (например, MetaMask) для обеспечения безопасности.

### Основной подход
Сквозное шифрование (end-to-end encryption) предполагает, что сообщение шифруется на стороне отправителя и расшифровывается на стороне получателя, причем только получатель, владеющий соответствующим ключом, может получить доступ к содержимому. В нашем случае мы используем криптокошелек пользователя, который хранит приватный ключ, для выполнения этих операций. Для этого подходит асимметричное шифрование, где:

-    **Публичный ключ** получателя используется для шифрования сообщения.
- 	 **Приватный ключ** получателя, хранящийся в его криптокошельке, используется для расшифровки.

В контексте популярных криптокошельков, таких как MetaMask, мы можем использовать существующие методы, предоставляемые их API, для реализации этой механики.

**Приложение должно быть:**
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




## Техническая архитектура
### Стек технологий (2023)
| Категория       | Технологии                                                                 
|-----------------|----------------------------------------------------------------------------|
| Фронтенд        | Next.js, TypeScript, FSD                                                   |
| Кошельки        | ethers.js , @metamask/eth-sig-util                                         |
| Шифрование      | ECIES, Web Crypto API (AES-GCM)                                            |
| Хранение данных | IPFS через Infura                                                          |
| Состояние/Роутинг       | Effector, Next.js App Router                                               |
| Стили           | Styled-components                                                          |
| Тестирование    | Jest/Vitest, Cypress/Playwright                                                              |
| Инфраструктура  | Node.js , pnpm                                                             |

## Mеханика шифрования
Мы будем использовать методы ``eth_getEncryptionPublicKey`` и ``eth_decrypt``, которые поддерживаются MetaMask и совместимыми кошельками, а также JavaScript-библиотеки для шифрования на стороне отправителя. 

**Вот пошаговый процесс:**
**1. Получение публичного ключа пользователя**
Когда пользователь подключает свой криптокошелек к нашему dApp (веб-сайту мессенджера), мы запрашиваем его публичный ключ для шифрования:
- Используем метод ```eth_getEncryptionPublicKey```, который возвращает публичный ключ, пригодный для шифрования данных, связанных с адресом пользователя.
- Этот ключ генерируется на основе приватного ключа пользователя, но само приложение не имеет доступа к приватному ключу.

**Пример кода на JavaScript для получения публичного ключа:**

```typescript
async function getEncryptionPublicKey(userAddress) {
  const encryptionPublicKey = await window.ethereum.request({
    method: 'eth_getEncryptionPublicKey',
    params: [userAddress], // Адрес пользователя из подключенного кошелька
  });
  return encryptionPublicKey;
}
```

- После получения публичный ключ сохраняется в профиле пользователя (например, на сервере или в блокчейне), чтобы другие пользователи могли использовать его для отправки сообщений.

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