---
title: SApp
description: 
published: true
date: 2025-04-07T21:43:22.725Z
tags: 
editor: markdown
dateCreated: 2025-04-06T23:03:53.833Z
---

# Техническое задание SAPP: Мессенджер с сквозным шифрованием на основе криптокошельков

## 1. Цель проекта
Разработать децентрализованное веб-приложение (dApp) — мессенджер с использованием сквозного шифрования сообщений, основанного на криптокошельках пользователей (например, MetaMask, Trust Wallet, SafePal). Приложение должно обеспечивать высокий уровень безопасности, удобство использования, производительность и соответствие самым актуальным технологическим стандартам. Основной акцент делается на:
- **Безопасность**: защита данных с использованием современных методов шифрования и хранения приватных ключей исключительно в кошельках пользователей.
- **Удобство**: минимизация действий пользователя для работы с шифрованием (например, однократное подтверждение доступа за сессию).
- **Децентрализация**: использование IPFS для хранения данных и блокчейна для взаимодействия.
- **Современный стек технологий**: применение актуальных инструментов и библиотек для разработки.

## 2. Основные требования
- **Шифрование**:
  - Сообщения шифруются публичным ключом получателя и расшифровываются только приватным ключом, который остается в криптокошельке пользователя.
  - Использование сессионного ключа для повышения производительности шифрования в рамках одной сессии.
- **Удобство**:
  - Пользователь подтверждает доступ к расшифровке один раз за сессию через криптокошелек.
  - Интуитивно понятный интерфейс с индикаторами загрузки для длительных операций.
- **Совместимость**:
  - Поддержка криптокошельков с MetaMask-совместимым API (MetaMask, Trust Wallet и другие).
- **Безопасность**:
  - Приватные ключи не покидают кошелек пользователя и не доступны приложению.
  - Все данные передаются и хранятся в зашифрованном виде.
- **Хранение данных**:
  - Зашифрованные сообщения и профили пользователей хранятся в децентрализованной файловой системе IPFS (через Infura).
- **Стилизация**:
  - Использование библиотеки `styled-components` для модульной и переиспользуемой стилизации интерфейса.
- **Управление состоянием**:
  - Использование библиотеки `effector` для централизованного и предсказуемого управления состоянием приложения.
- **Взаимодействие с блокчейном**:
  - Использование библиотеки `viem` для подключения к кошелькам, взаимодействия с блокчейном и смарт-контрактами.

## 3. Техническая архитектура

### 3.1 Стек технологий
Для реализации проекта используется современный и актуальный стек технологий, обеспечивающий надежность, масштабируемость и производительность.

#### Фронтенд
- **React (v18.3)**: Библиотека для построения динамического и компонентного интерфейса.
- **TypeScript (v5.4)**: Статическая типизация для повышения надежности и читаемости кода.
- **Next.js (v14.2)**: Фреймворк для серверного рендеринга (SSR), статической генерации (SSG) и упрощения разработки.
- **styled-components (v6.1)**: Инструмент для стилизации компонентов с поддержкой CSS-in-JS.
- **effector (v23.0)**: Управление состоянием приложения с минимальной бойлерплейт-кодом и высокой производительностью.

#### Взаимодействие с кошельками и блокчейном
- **viem (v2.0)**: Легковесная и современная библиотека для работы с блокчейном, кошельками и смарт-контрактами.
- **@metamask/eth-sig-util (v7.0)**: Утилиты для шифрования и расшифровки данных с использованием криптокошельков.

#### Шифрование
- **ECIES (Elliptic Curve Integrated Encryption Scheme)**: Асимметричное шифрование для защиты данных с использованием публичных и приватных ключей.
- **Web Crypto API**: Симметричное шифрование с использованием алгоритма AES-GCM для сессионных ключей.

#### Хранение данных
- **IPFS (via Infura)**: Децентрализованное хранилище для зашифрованных сообщений и профилей пользователей.

#### Маршрутизация
- **Next.js App Router**: Современная система маршрутизации для управления страницами и API-эндпоинтами.

#### Тестирование
- **Jest (v29.7)**: Инструмент для юнит-тестирования логики приложения.
- **Cypress (v13.7)**: Инструмент для энд-ту-энд тестирования пользовательских сценариев.

#### Инфраструктура
- **Node.js (v20)**: Среда выполнения для разработки, сборки и запуска приложения.
- **pnpm (v8.15)**: Быстрый и эффективный менеджер пакетов для управления зависимостями.

### 3.2 Архитектура приложения
Приложение строится по модульной архитектуре **Feature-Sliced Design (FSD)**, которая упрощает масштабирование, поддержку и разделение ответственности.

#### Структура проекта
messenger-dapp/
├── src/
│   ├── app/               # Глобальные стили, layouts, конфигурация приложения
│   │   ├── globals.css    # Глобальные стили (если необходимо)
│   │   └── layout.tsx     # Основной layout приложения
│   ├── features/          # Функциональные модули
│   │   ├── auth/          # Модуль аутентификации (подключение кошелька, регистрация)
│   │   └── chat/          # Модуль чата (сообщения, шифрование, отправка)
│   ├── entities/          # Сущности приложения
│   │   ├── user/          # Модель пользователя (адрес, публичный ключ)
│   │   └── message/       # Модель сообщения (CID, зашифрованный текст)
│   ├── shared/            # Общие утилиты и библиотеки
│   │   ├── wallet/        # Логика работы с кошельками
│   │   ├── crypto/        # Логика шифрования/расшифровки
│   │   └── ipfs/          # Логика работы с IPFS
│   ├── widgets/           # Составные UI-компоненты
│   │   └── ChatWindow.tsx # Компонент окна чата
│   └── pages/             # Страницы приложения (Next.js App Router)
├── tests/                 # Тесты
│   ├── unit/              # Юнит-тесты (Jest)
│   └── e2e/               # Энд-ту-энд тесты (Cypress)
├── next.config.js         # Конфигурация Next.js
└── package.json           # Зависимости и скрипты

## 4. Механика работы
Ниже подробно описаны ключевые процессы работы мессенджера с примерами кода для каждого этапа.

### 4.1 Подключение кошелька
- Пользователь подключает криптокошелек через интерфейс приложения.
- Приложение запрашивает адрес кошелька и публичный ключ шифрования через MetaMask-совместимый API.

#### Пример кода
```typescript
// src/shared/lib/wallet.ts
import { createWalletClient, custom } from 'viem';

export async function connectWallet(): Promise<{ address: string; encryptionPublicKey: string }> {
  const walletClient = createWalletClient({
    transport: custom(window.ethereum),
  });
  const [address] = await walletClient.requestAddresses();
  const encryptionPublicKey = await window.ethereum.request({
    method: 'eth_getEncryptionPublicKey',
    params: [address],
  }) as string;
  return { address, encryptionPublicKey };
}
```

### 4.2 Регистрация пользователя

При первом входе пользователь регистрируется: его адрес и публичный ключ сохраняются в IPFS.
Content Identifier (CID) возвращается и привязывается к адресу пользователя (например, в смарт-контракте или локальном хранилище).

#### Пример кода

```typescript
// src/features/auth/lib/register.ts
import { create } from 'ipfs-http-client';

const ipfs = create({ url: 'https://ipfs.infura.io:5001' });

export async function registerUser(address: string, publicKey: string): Promise<string> {
  const profile = JSON.stringify({ address, publicKey });
  const { cid } = await ipfs.add(profile);
  return cid.toString();
}
```

### 4.3 Генерация сессионного ключа
При входе генерируется симметричный ключ (AES-GCM) для шифрования сообщений в рамках сессии.
Ключ экспортируется, шифруется публичным ключом пользователя и сохраняется в IPFS.

#### Пример кода

```typescript
// src/shared/lib/crypto.ts
import { encrypt } from '@metamask/eth-sig-util';

export async function generateSessionKey(publicKey: string): Promise<{ encryptedKey: string; key: CryptoKey }> {
  const key = await crypto.subtle.generateKey({ name: 'AES-GCM', length: 256 }, true, ['encrypt', 'decrypt']);
  const exportedKey = await crypto.subtle.exportKey('raw', key);
  const keyString = Buffer.from(exportedKey).toString('base64');
  const encryptedKey = encrypt({ publicKey, data: keyString, version: 'x25519-xsalsa20-poly1305' });
  return { encryptedKey: JSON.stringify(encryptedKey), key };
}
```

### 4.4 Шифрование сообщения
Сообщения шифруются сессионным ключом с использованием алгоритма AES-GCM для повышения производительности.
Инициализационный вектор (IV) генерируется для каждого сообщения.

#### Пример кода

```typescript
// src/features/chat/lib/encrypt.ts
export async function encryptMessage(sessionKey: CryptoKey, message: string): Promise<string> {
  const iv = crypto.getRandomValues(new Uint8Array(12));
  const encodedMessage = new TextEncoder().encode(message);
  const encrypted = await crypto.subtle.encrypt({ name: 'AES-GCM', iv }, sessionKey, encodedMessage);
  return JSON.stringify({
    encryptedMessage: Buffer.from(encrypted).toString('base64'),
    iv: Buffer.from(iv).toString('base64'),
  });
}
```

### 4.5 Отправка сообщения
Зашифрованное сообщение сохраняется в IPFS, а полученный CID передается получателю через смарт-контракт или другой механизм доставки.

#### Пример кода
```typescript
// src/shared/lib/ipfs.ts
import { create } from 'ipfs-http-client';

const ipfs = create({ url: 'https://ipfs.infura.io:5001' });

export async function sendMessage(encryptedMessage: string): Promise<string> {
  const { cid } = await ipfs.add(encryptedMessage);
  return cid.toString();
}
```

### 4.6 Расшифровка сообщения
Пользователь загружает сообщение по CID из IPFS.
Сессионный ключ расшифровывается один раз за сессию с использованием приватного ключа из кошелька.
Сообщение расшифровывается с использованием сессионного ключа.

#### Пример кода

```typescript
// src/features/chat/lib/decrypt.ts
export async function decryptSessionKey(encryptedKey: string, address: string): Promise<CryptoKey> {
  const decryptedKeyString = await window.ethereum.request({
    method: 'eth_decrypt',
    params: [encryptedKey, address],
  }) as string;
  const keyBuffer = Buffer.from(decryptedKeyString, 'base64');
  return crypto.subtle.importKey('raw', keyBuffer, { name: 'AES-GCM' }, true, ['encrypt', 'decrypt']);
}

export async function decryptMessage(sessionKey: CryptoKey, encryptedData: string): Promise<string> {
  const { encryptedMessage, iv } = JSON.parse(encryptedData);
  const ivBuffer = Buffer.from(iv, 'base64');
  const encryptedBuffer = Buffer.from(encryptedMessage, 'base64');
  const decrypted = await crypto.subtle.decrypt({ name: 'AES-GCM', iv: ivBuffer }, sessionKey, encryptedBuffer);
  return new TextDecoder().decode(decrypted);
}
```

### 5. Организация хранения и доставки данных в IPFS
Профили пользователей: 
CID публичных ключей и зашифрованных сессионных ключей сохраняются в смарт-контракте или временном централизованном сервере для упрощения поиска.
#### Сообщения: 
Зашифрованные сообщения сохраняются в IPFS.
CID передаются получателю через смарт-контракт с использованием событий.

#### Пример смарт-контракта
```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract Messenger {
    event MessageSent(address indexed from, address indexed to, string cid);

    function sendMessage(address to, string memory cid) external {
        emit MessageSent(msg.sender, to, cid);
    }
}
```
#### Логика работы:
Отправитель вызывает функцию sendMessage с адресом получателя и CID.
Смарт-контракт генерирует событие MessageSent.
Приложение слушает события и уведомляет получателя о новом сообщении.

## 6. Стилизация и управление состоянием
### 6.1 Стилизация с использованием styled-components
Все UI-компоненты стилизуются с помощью styled-components для обеспечения модульности и переиспользуемости стилей.
Стили применяются на уровне компонентов, избегая глобальных CSS-файлов (за исключением минимальных глобальных стилей в app/globals.css).

#### Пример использования
```typescript
// src/widgets/ChatWindow.tsx
import styled from 'styled-components';

export const ChatContainer = styled.div`
  padding: 20px;
  background-color: #f5f5f5;
  border-radius: 8px;
  max-width: 600px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
`;

export const MessageBubble = styled.div<{ isOwn: boolean }>`
  padding: 10px 15px;
  margin: 5px 0;
  background-color: ${({ isOwn }) => (isOwn ? '#007bff' : '#e9ecef')};
  color: ${({ isOwn }) => (isOwn ? '#fff' : '#000')};
  border-radius: 12px;
  max-width: 70%;
  align-self: ${({ isOwn }) => (isOwn ? 'flex-end' : 'flex-start')};
`;
```

### 6.2 Управление состоянием с использованием effector
Состояние приложения (сообщения, сессионные ключи, данные пользователя) централизованно управляется через effector.
Используются события и хранилища для отслеживания изменений.
#### Пример использования

```typescript
// src/features/chat/model.ts
import { createStore, createEvent } from 'effector';

export const setSessionKey = createEvent<CryptoKey>();
export const $sessionKey = createStore<CryptoKey | null>(null).on(setSessionKey, (_, key) => key);

export const addMessage = createEvent<string>();
export const $messages = createStore<string[]>([]).on(addMessage, (state, msg) => [...state, msg]);

export const setUserAddress = createEvent<string>();
export const $userAddress = createStore<string>('').on(setUserAddress, (_, address) => address);
```

#### Пример интеграции с компонентом

```typescript
// src/widgets/ChatWindow.tsx
import { useUnit } from 'effector-react';
import { $messages, addMessage } from '../features/chat/model';

export const ChatWindow: React.FC = () => {
  const messages = useUnit($messages);

  const handleSend = (text: string) => {
    addMessage(text); // Добавление нового сообщения в хранилище
  };

  return (
    <ChatContainer>
      {messages.map((msg, index) => (
        <MessageBubble key={index} isOwn={true}>{msg}</MessageBubble>
      ))}
    </ChatContainer>
  );
};
```

### 7. Оптимизация разработки
Next.js Turbo Mode: Используйте команду next dev --turbo для ускорения сборки и горячей перезагрузки во время разработки.
pnpm: Установите зависимости с помощью pnpm install для быстрой и экономичной работы с пакетами.
TypeScript: Используйте строгие настройки (strict: true в tsconfig.json) для минимизации ошибок.

#### Пример конфигурации next.config.js
```javascript
/** @type {import('next').NextConfig} */
const nextConfig = {
  reactStrictMode: true,
  experimental: {
    appDir: true, // Включение App Router
  },
};

module.exports = nextConfig;
```

### 8. Тестирование
Юнит-тесты:
Используйте Jest для тестирования утилит шифрования, работы с IPFS и логики управления состоянием.
Энд-ту-энд тесты:
Используйте Cypress для проверки сценариев подключения кошелька, отправки и получения сообщений.

#### Пример юнит-теста

```typescript
// tests/unit/crypto.test.ts
import { encryptMessage } from '../src/features/chat/lib/encrypt';

describe('Encryption', () => {
  it('should encrypt a message correctly', async () => {
    const key = await crypto.subtle.generateKey({ name: 'AES-GCM', length: 256 }, true, ['encrypt']);
    const message = 'Hello, world!';
    const encrypted = await encryptMessage(key, message);
    expect(encrypted).toBeDefined();
    expect(typeof encrypted).toBe('string');
  });
});
```
### 9. Дополнительные рекомендации
UI/UX:
Добавьте индикаторы загрузки (спиннеры) для операций шифрования, расшифровки и работы с IPFS.
Используйте адаптивный дизайн с медиа-запросами в styled-components.
Производительность:
Кэшируйте данные из IPFS локально (например, с использованием localStorage) для ускорения загрузки.
Минимизируйте количество запросов к IPFS, группируя данные, где это возможно.
Безопасность:
Регулярно обновляйте зависимости для устранения уязвимостей (используйте pnpm audit).
Проверяйте корректность CID и данных, загружаемых из IPFS, для предотвращения атак.
### 10. Итог
Данное техническое задание представляет собой подробную инструкцию для разработки децентрализованного мессенджера с сквозным шифрованием. Оно включает:
Полное описание требований и механик работы.
Подробный стек технологий с актуальными версиями.
Примеры кода для всех ключевых процессов.

Рекомендации по стилизации (styled-components), управлению состоянием (effector) и взаимодействию с блокчейном (viem).
Советы по оптимизации, тестированию и улучшению UX.
Следуя этому документу, разработчики смогут создать безопасное, удобное и производительное приложение, соответствующее самым высоким стандартам децентрализованных технологий.
