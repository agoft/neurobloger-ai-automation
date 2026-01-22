# neurobloger-ai-automation
🚀 AI-Powered Content Automation Platform for Telegram &amp; VK | Автоматизация контент-маркетинга с ИИ | FastAPI + React + OpenAI GPT-4 + DALL-E | Парсинг, рерайт, автопостинг до 200+ каналов | Реферальная программа | SMM automation, content generation, multi-channel posting
# 🚀 NeuroBloger - AI-Powered Content Automation Platform

> Автоматизируйте контент-маркетинг в Telegram и VK с помощью AI. Масштабируйте до 200+ каналов без команды.

[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Python](https://img.shields.io/badge/python-3.12-blue.svg)](https://www.python.org/)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.100+-green.svg)](https://fastapi.tiangolo.com/)
[![React](https://img.shields.io/badge/React-18.0+-blue.svg)](https://reactjs.org/)

---

## 📋 Содержание

- [О проекте](#-о-проекте)
- [Возможности](#-возможности)
- [Архитектура](#-архитектура)
- [Технологии](#-технологии)
- [Установка](#-установка)
- [Конфигурация](#-конфигурация)
- [API Документация](#-api-документация)
- [Структура проекта](#-структура-проекта)
- [Лицензия](#-лицензия)

---

## 🎯 О проекте

**NeuroBloger** - это SaaS-платформа для автоматизации контент-маркетинга в Telegram и VK с использованием искусственного интеллекта.

### Для кого?

- 🏢 **SMM-агентства** - управление 10-50+ клиентскими каналами
- 📰 **Медиа-холдинги** - сеть тематических каналов
- 💰 **Арбитражники** - быстрый запуск и тест гипотез
- 📚 **Инфобизнес** - автоматизация контента для воронок
- 🛒 **E-commerce** - продвижение через контент-каналы

### Результаты

- ⏱️ **95% экономия времени** vs ручной постинг
- 💵 **ROI за 1-3 месяца**
- 📈 **500+ постов/день** на автомате
- 🤖 **AI-генерация** текста и изображений

---

## ✨ Возможности

### 🤖 AI-генерация контента
- **Рерайт постов** от конкурентов с сохранением смысла (OpenAI GPT)
- **Генерация изображений** под тему поста (DALL-E)
- **Контент-планы** с автопубликацией на недели вперёд
- **Кастомные промты** для брендового стиля (глобальные и на уровне канала)

### 📊 Система доноров
- Парсинг контента из донорских каналов в реальном времени
- Фильтрация по ключевым словам и стоп-словам
- Автоматический рерайт через AI
- Модерация перед публикацией

### 📋 Контент-планы
- AI генерирует темы по вашей нише
- Автоматическая генерация постов с картинками
- Расписание публикаций (09:00, 14:00, 19:00)
- Редактирование и пересоздание контента

### 📱 Мультиплатформенность
- **Telegram** - публикация через Telethon
- **VK** - автоматическое дублирование постов
- Единая панель управления

### 💰 Реферальная программа
- **20% от платежей** приглашённых пользователей (уровень 1)
- **5% от платежей** рефералов второго уровня
- **10% скидка** для реферала на первый платёж
- Красивые реферальные ссылки (`neurobloger.ru?ref=CODE`)
- Личный кабинет с аналитикой и выплатами

### 🛡️ Защита от банов
- Отдельные прокси на каждый аккаунт
- FloodWait handling - защита от лимитов Telegram
- Rate limiting скачивания медиа
- Быстрая замена забаненных аккаунтов

### 🔄 Умный Reload
- Добавили донора → работает через 30 сек
- Изменили настройки → применяется автоматически
- Остальные каналы работают без прерывания

---

## 🏗️ Архитектура

```
┌─────────────────────────────────────────────────────────────┐
│                         NGINX                               │
│  neurobloger.ru | panel.neurobloger.ru | admin.neurobloger.ru │
└────────────┬────────────────────┬───────────────────────────┘
             │                    │
             ▼                    ▼
    ┌────────────────┐   ┌────────────────┐
    │   Landing      │   │  React Apps    │
    │   (Static)     │   │  User + Admin  │
    └────────────────┘   └────────┬───────┘
                                  │
                    ┌─────────────┴─────────────┐
                    ▼                           ▼
         ┌──────────────────┐        ┌──────────────────┐
         │  Backend API     │◄──────►│  Referral API    │
         │  FastAPI :8002   │ Webhook│  FastAPI :8003   │
         └────────┬─────────┘        └──────────────────┘
                  │
         ┌────────┴────────┐
         ▼                 ▼
    ┌─────────┐      ┌──────────┐
    │ SQLite  │      │ Workers  │
    │   DB    │      │ Parser   │
    └─────────┘      │ Publisher│
                     │ Content  │
                     └──────────┘
```

### Микросервисная архитектура

- **Backend API** (8002) - основной API, управление пользователями, каналами, постами
- **Referral API** (8003) - изолированная реферальная система
- **Webhook-based** синхронизация между сервисами
- **Multi-worker** парсинг и публикация
- **Graceful shutdown** и автоматический restart

---

## 🛠️ Технологии

### Backend
- **FastAPI** - современный веб-фреймворк
- **SQLite** - легковесная БД
- **Telethon** - Telegram MTProto API
- **VK API** - интеграция с VK
- **OpenAI API** - GPT-4 для рерайта, DALL-E для изображений
- **Bcrypt** - хеширование паролей
- **JWT** - аутентификация

### Frontend
- **React 18** - UI библиотека
- **TypeScript** - типизация
- **Vite** - сборщик
- **Axios** - HTTP клиент

### DevOps
- **Systemd** - управление сервисами
- **Nginx** - reverse proxy
- **Python 3.12** - runtime

---

## 📦 Установка

### Требования

- Python 3.12+
- Node.js 18+
- SQLite 3
- Nginx
- Systemd (Linux)

### Быстрый старт

```bash
# Клонирование репозитория
git clone https://github.com/yourusername/neurobloger.git
cd neurobloger

# Backend
cd backend
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt

# Referral System
cd ../referral_system
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt

# User Frontend
cd ../user_frontend
npm install
npm run build

# Admin Frontend
cd ../admin
npm install
npm run build

# Инициализация БД
python3 backend/init_db.py
python3 referral_system/init_referral_db.py
```

### Systemd сервисы

```bash
# Копирование systemd unit файлов
sudo cp systemd/*.service /etc/systemd/system/

# Запуск сервисов
sudo systemctl enable --now neurobloger-backend
sudo systemctl enable --now neurobloger-referral
sudo systemctl enable --now neurobloger-frontend
sudo systemctl enable --now neurobloger-admin
sudo systemctl enable --now neurobloger-parser
sudo systemctl enable --now neurobloger-publisher
sudo systemctl enable --now neurobloger-content-plan
```

---

## ⚙️ Конфигурация

### Backend (.env)

```env
# OpenAI
OPENAI_API_KEY=sk-...

# JWT
SECRET_KEY=your-secret-key-here

# Email
SMTP_HOST=smtp.gmail.com
SMTP_PORT=587
SMTP_USER=your-email@gmail.com
SMTP_PASSWORD=your-app-password

# Database
DATABASE_PATH=/home/auto_post_platform/bd/auto_post_database.db
```

### Referral System (referral_config.py)

```python
LEVEL_1_PERCENT = 0.20  # 20%
LEVEL_2_PERCENT = 0.05  # 5%
REFERRAL_DISCOUNT = 0.10  # 10%
```

### Nginx

```nginx
# /etc/nginx/sites-available/neurobloger.conf
server {
    server_name panel.neurobloger.ru;
    
    location /api/ {
        proxy_pass http://localhost:8002/;
    }
    
    location /api/referrals/ {
        proxy_pass http://localhost:8003/;
    }
    
    location / {
        root /home/auto_post_platform/user_frontend/build;
        try_files $uri /index.html;
    }
}
```

---

## 📚 API Документация

### Swagger UI

- Backend: `http://localhost:8002/docs`
- Referral: `http://localhost:8003/docs`

### Основные эндпоинты

#### Аутентификация
```http
POST /users/register
POST /users/login
POST /users/verify-email?token=...
```

#### Каналы
```http
GET    /channels/
POST   /channels/
PATCH  /channels/{id}
DELETE /channels/{id}
```

#### Доноры
```http
GET    /sources/
POST   /sources/
PATCH  /sources/{id}
DELETE /sources/{id}
```

#### Контент-планы
```http
GET    /content-plans/
POST   /content-plans/
POST   /content-plans/{id}/generate
DELETE /content-plans/{id}
```

#### Реферальная программа
```http
GET /referrals/link
GET /referrals/stats
GET /referrals/earnings
POST /referrals/withdraw
```

---

## 📁 Структура проекта

```
neurobloger/
├── backend/                    # Основной API
│   ├── routes/                # API роуты (21 файл)
│   ├── cron/                  # Cron задачи
│   ├── autopost_parser/       # Парсер доноров
│   └── auto_post_main.py      # Точка входа
├── referral_system/           # Реферальная система
│   ├── api/                   # API роуты
│   ├── database/              # БД подключение
│   ├── models/                # Pydantic модели
│   └── referral_main.py       # Точка входа
├── user_frontend/             # Пользовательская панель
│   └── src/pages/             # React страницы
├── admin/                     # Админ-панель
│   └── src/pages/             # React страницы
├── landing/                   # Лендинг
├── bd/                        # SQLite БД
├── docs/                      # Документация
│   ├── PROJECT_STRUCTURE.md   # Подробная структура
│   ├── MARKETING.md           # Маркетинговые материалы
│   └── TZ_*.md                # Технические задания
└── manager_autopost.py        # Менеджер процессов
```

Подробная структура: [PROJECT_STRUCTURE.md](docs/PROJECT_STRUCTURE.md)

---

## 💎 Тарифы

| Тариф | Цена | Каналы | Доноры | AI рерайт | Изображения | Контент-планы |
|-------|------|--------|--------|-----------|-------------|---------------|
| **FREE** | 0₽ | 1 | 3 | 0 | 0 | 0 |
| **STARTER** | 2,990₽ | 3 | 15 | 500 | 500 | 1 |
| **BUSINESS** | 9,990₽ | 10 | 50 | 2,000 | 2,000 | 5 |
| **AGENCY** | 29,990₽ | 50 | 250 | 10,000 | 10,000 | 25 |
| **ENTERPRISE** | от 99,990₽ | ∞ | ∞ | ∞ | ∞ | ∞ |

---

## 🤝 Вклад в проект

Мы приветствуем вклад в проект! Пожалуйста:

1. Fork репозиторий
2. Создайте feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit изменения (`git commit -m 'Add some AmazingFeature'`)
4. Push в branch (`git push origin feature/AmazingFeature`)
5. Откройте Pull Request

---

## 📄 Лицензия

Этот проект лицензирован под MIT License - см. файл [LICENSE](LICENSE) для деталей.

---

## 📞 Контакты

- **Website:** [neurobloger.ru](https://neurobloger.ru)
- **Email:** support@neurobloger.ru
- **Telegram:** [@neurobloger_support](https://t.me/neurobloger_support)

---

## 🙏 Благодарности

- [FastAPI](https://fastapi.tiangolo.com/) - за отличный веб-фреймворк
- [Telethon](https://docs.telethon.dev/) - за Telegram API
- [OpenAI](https://openai.com/) - за GPT и DALL-E
- [React](https://reactjs.org/) - за UI библиотеку

---

<div align="center">

**Сделано с ❤️ командой NeuroBloger**

[⬆ Наверх](#-neurobloger---ai-powered-content-automation-platform)

</div>
