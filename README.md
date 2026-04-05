# Liquibase MySQL RGR

Розрахунково-графічна робота з дисципліни «Інженерія програмного забезпечення».  
Демонстрація версіонування бази даних MySQL за допомогою Liquibase.

## Опис проєкту

У проєкті реалізовано три changeset'и для бази даних `mydb`:
1. Створення таблиці `users` з полями `id`, `username`, `email`
2. Вставка початкових записів (`alice`, `bob`)
3. Додавання стовпця `created_at` з автоматичною датою

## Технології

- Java 21
- Liquibase 4.30.0
- MySQL 8
- Docker


## Запуск

### 1. Запустити MySQL у Docker

```bash
docker run -d --name mysql-rgr -e MYSQL_ROOT_PASSWORD=rootpass -e MYSQL_DATABASE=mydb -e MYSQL_USER=myuser -e MYSQL_PASSWORD=mypassword -p 3307:3306 mysql:8
```

### 2. Перевірити версію Liquibase

```bash
java -cp "liquibase-core-4.30.0.jar;lib/mysql-connector-j-9.6.0.jar;lib/commons-io-2.15.1.jar;lib/commons-lang3-3.14.0.jar;lib/snakeyaml-2.2.jar" liquibase.integration.commandline.Main version
```

Очікуваний результат: `Liquibase Version 4.30.0`

### 3. Перевірити стан бази даних (status)

```bash
java -cp "liquibase-core-4.30.0.jar;lib/mysql-connector-j-9.6.0.jar;lib/commons-io-2.15.1.jar;lib/commons-lang3-3.14.0.jar;lib/snakeyaml-2.2.jar" liquibase.integration.commandline.Main --defaultsFile="liquibase.properties" status
```

Очікуваний результат: `3 changesets have not been applied`

### 4. Застосувати зміни (update)

```bash
java -cp "liquibase-core-4.30.0.jar;lib/mysql-connector-j-9.6.0.jar;lib/commons-io-2.15.1.jar;lib/commons-lang3-3.14.0.jar;lib/snakeyaml-2.2.jar" liquibase.integration.commandline.Main --defaultsFile="liquibase.properties" update
```

Очікуваний результат: `Update has been successful. Rows affected: 5`

### 5. Перевірити стан після оновлення (status)

```bash
java -cp "liquibase-core-4.30.0.jar;lib/mysql-connector-j-9.6.0.jar;lib/commons-io-2.15.1.jar;lib/commons-lang3-3.14.0.jar;lib/snakeyaml-2.2.jar" liquibase.integration.commandline.Main --defaultsFile="liquibase.properties" status
```

Очікуваний результат: `database is up to date`

### 6. Встановити тег (tag)

```bash
java -cp "liquibase-core-4.30.0.jar;lib/mysql-connector-j-9.6.0.jar;lib/commons-io-2.15.1.jar;lib/commons-lang3-3.14.0.jar;lib/snakeyaml-2.2.jar" liquibase.integration.commandline.Main --defaultsFile="liquibase.properties" tag version1
```

Очікуваний результат: `Tag 'version1' wurde erfolgreich gesetzt`

### 7. Повернутися до попередньої версії (rollback)

```bash
java -cp "liquibase-core-4.30.0.jar;lib/mysql-connector-j-9.6.0.jar;lib/commons-io-2.15.1.jar;lib/commons-lang3-3.14.0.jar;lib/snakeyaml-2.2.jar" liquibase.integration.commandline.Main --defaultsFile="liquibase.properties" rollback version1
```

Очікуваний результат: `Rollback war erfolgreich`

## Автор

Гужов Андрій — група KI-222
