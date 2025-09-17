# CRUD_USER_AUTO

Учебный проект для освоения работы с **Hibernate ORM** и построения простого CRUD-приложения без использования сервлетов или Spring.  
Проект демонстрирует работу с сущностями `User` и `Auto`, их сохранение, обновление, удаление и поиск в базе данных PostgreSQL.

---

## 🚀 Возможности
- Создание пользователей и автомобилей
- Чтение данных из базы
- Обновление существующих записей
- Удаление записей
- Работа через слой DAO и сервисы
- Настройка `Hibernate` без дополнительных фреймворков

---

## 🛠️ Технологии
- Java 17+
- Hibernate ORM `6.6.29.Final`
- PostgreSQL `12+`
- Maven (для управления зависимостями)

---

## ⚙️ Установка и запуск

### 1. Клонировать проект
```bash
git clone https://github.com/your-username/CRUD_USER_AUTO.git
cd CRUD_USER_AUTO
```

### 2. Настроить базу данных PostgreSQL
Создать базу и схему (например `crud`):
```sql
CREATE DATABASE crud_db;
CREATE SCHEMA crud;
```

Выполнить миграцию или создать таблицы вручную:
```sql
CREATE TABLE crud.users (
    id SERIAL PRIMARY KEY,
    name VARCHAR(255),
    age INT
);

CREATE TABLE crud.auto (
    id SERIAL PRIMARY KEY,
    model VARCHAR(255),
    user_id INT REFERENCES crud.users(id)
);
```

### 3. Настроить Hibernate
В файле `hibernate.cfg.xml` указать свои настройки:
```xml
<property name="hibernate.connection.url">jdbc:postgresql://localhost:5432/crud_db</property>
<property name="hibernate.connection.username">postgres</property>
<property name="hibernate.connection.password">your_password</property>
<property name="hibernate.default_schema">crud</property>
<property name="hibernate.hbm2ddl.auto">update</property>
```

### 4. Собрать и запустить проект
```bash
mvn clean install
mvn exec:java -Dexec.mainClass="Main"
```

---

## 📂 Структура проекта
```
src/
 ├─ main/
 │   ├─ java/
 │   │   ├─ dao/        -> классы доступа к данным (UserDao, AutoDao)
 │   │   ├─ model/      -> entity-классы (User, Auto)
 │   │   ├─ services/   -> бизнес-логика
 │   │   ├─ utils/      -> подключение к БД
 │   │   └─ Main.java   -> точка входа
 │   └─ resources/
 │       └─ hibernate.cfg.xml
 └─ test/               -> unit-тесты (JUnit)
```

---

## 📝 Пример использования
```java
UserService userService = new UserService();
User user = new User("Alex", 25);
userService.saveUser(user);

User dbUser = userService.findUser(1);
System.out.println(dbUser.getName());

user.setAge(26);
userService.updateUser(user);

userService.deleteUser(user);
```

---

## 📚 Чему я научился
- Подключение Hibernate к PostgreSQL
- Настройка `hibernate.cfg.xml`
- Создание entity-классов с аннотациями (`@Entity`, `@Table`, `@Id`, `@GeneratedValue`)
- Реализация DAO и сервисного слоя
- Работа с транзакциями и сессиями
- Выполнение HQL-запросов

---

## 📌 План на будущее
- Добавить логирование (SLF4J + Logback)
- Подключить Spring Data JPA
- Сделать REST API для работы с пользователями и авто  
