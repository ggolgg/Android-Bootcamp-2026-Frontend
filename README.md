# 📅 Meet — Планировщик встреч

**Meet** — это современное Android-приложение для управления встречами и командным расписанием. Проект построен на принципах Clean Architecture, использует Jetpack Compose и Ktor, а данные авторизации надёжно шифруются. Meet помогает организовывать встречи, обрабатывать приглашения и синхронизировать расписание в удобном интерфейсе с тремя режимами отображения.

---

## ✨ Возможности

- 🔐 **Авторизация и регистрация** — JWT-токены, восстановление сессии, шифрованное хранилище
- 📋 **Список встреч** — фильтрация, статусы (запланировано/завершено/отменено), приоритеты
- 📆 **Расписание** — три режима: день, неделя, месяц; кастомный календарь без сторонних библиотек
- 👥 **Приглашения** — просмотр активных приглашений, возможность принять или отклонить
- 🔔 **Уведомления** — лента событий, отметка о прочтении
- 👤 **Профиль** — информация о пользователе, статистика встреч, выход из аккаунта
- ➕ **Создание встречи** — форма с выбором даты/времени, приоритета, места и поиском участников
- 🔎 **Поиск сотрудников** — клиентское кэширование с фильтрацией по ФИО, email, должности, отделу

---

## 🛠 Стек технологий

- **Язык**: Kotlin  
- **UI**: Jetpack Compose + Material 3  
- **Асинхронность**: Coroutines, Flow  
- **Навигация**: Navigation Compose  
- **Сеть**: Ktor Client (CIO), Content Negotiation, Logging  
- **Сериализация**: kotlinx.serialization JSON  
- **Безопасное хранилище**: EncryptedSharedPreferences (AES256-GCM)  
- **Локальное хранилище**: DataStore Preferences  
- **Архитектура**: Clean Architecture (Data, Domain, Presentation)  
- **Управление состоянием**: ViewModel, LiveData, sealed classes  
- **Дата и время**: java.time.*

---

## 🧱 Архитектура

Проект чётко разделён на три слоя:

```
📦 app
 ┣ 📂 data          // DTO, мапперы, репозитории (реализации), источники данных
 ┃   ┣ 📂 dto       // AuthDtos, MeetingDTO, InvitationDTO, NotificationDTO, UserDTO
 ┃   ┣ 📂 mapper    // UserMapper
 ┃   ┣ 📂 repository// UserRepositoryImpl
 ┃   ┗ 📂 source    // Network, AuthPrefs, DataLocator, *DataSource
 ┣ 📂 domain        // Бизнес-сущности и интерфейсы репозиториев
 ┃   ┣ 📂 entity    // User, Meeting, Invitation, Notification
 ┃   ┗ 📂 repository// UserRepository, MeetingRepository, ...
 ┣ 📂 ui            // Экраны Compose, ViewModel, навигация, тема
 ┃   ┣ 📂 navigation// AppNavigation, Screen
 ┃   ┣ 📂 screens   // auth, main, list, meetings, profile
 ┃   ┗ 📂 theme     // MeetTheme, Color, Typography
 ┗ 📄 MeetApplication.kt
```

**Взаимодействие**:  
UI → ViewModel → Repository (impl) → DataSource → Network  
Данные передаются через `LiveData` и `State` (sealed class), мапперы изолируют DTO от доменных моделей.

---

## 🚀 Установка и запуск

### Требования
- Android Studio Iguana / Koala (или новее)
- JDK 21
- Android SDK (minSdk 27, targetSdk 35)

### Шаги

1. Клонируйте репозиторий:
   ```bash
   git clone https://github.com/ggolgg/Android-Bootcamp-2026-Frontend.git
   ```

2. Откройте проект в Android Studio.

3. Укажите URL вашего бэкенда в `app/build.gradle.kts`:
   ```kotlin
   buildConfigField("String", "BASE_URL", "\"http://your-server.com\"")
   ```
   > Для эмулятора автоматически подставится `http://10.0.2.2:8080`, если `BASE_URL` содержит `localhost` или `127.0.0.1`.

4. Синхронизируйте Gradle и запустите приложение.

---

## 🌐 Ожидаемые API-эндпоинты

| Метод | Путь                         | Описание                       |
|-------|------------------------------|--------------------------------|
| POST  | `/api/auth/login`            | Авторизация                   |
| POST  | `/api/auth/register`         | Регистрация                   |
| GET   | `/api/users`                 | Список пользователей          |
| GET   | `/api/users/{id}`            | Пользователь по ID            |
| GET   | `/api/meetings`              | Все встречи                   |
| GET   | `/api/meetings/user/{id}`    | Встречи конкретного участника |
| POST  | `/api/meetings`              | Создание встречи              |
| GET   | `/api/invitations`           | Приглашения                   |
| PUT   | `/api/invitations/{id}`      | Ответ на приглашение          |
| GET   | `/api/notifications`         | Уведомления                   |
| PUT   | `/api/notifications/{id}`    | Отметить как прочитанное      |

Запросы, требующие авторизации, включают заголовок `Authorization: Bearer <token>`.

---

## 🧭 Планы по развитию

- [ ] **Offline First** — кэширование через Room, работа без интернета  
- [ ] **Dependency Injection** — внедрение Hilt для чистоты кода  
- [ ] **Push-уведомления** — Firebase Cloud Messaging  
- [ ] **Повторяющиеся встречи** — поддержка recurrence-правил  
- [ ] **Тёмная тема** — уже заложены цвета, осталось доделать  
- [ ] **Локализация** — английский / русский / арабский / китайский / хинди  

---

## 👨‍💻 Автор

**Олег**  
- 🥇 Призёр хакатонов  
- 🛠 Участник региональных чемпионатов «Профессионалы» и WorldSkills  
- 📱 Android-разработчик
- ✉️ [Telegram](https://t.me/ilove_dev) | [GitHub](https://github.com/ggolgg)

---

## 📄 Лицензия

Проект распространяется под лицензией **MIT**.  
Вы можете свободно использовать его в учебных и коммерческих целях.

---

⭐ _Спасибо за просмотр!_