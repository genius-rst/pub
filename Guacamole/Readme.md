# Установка Apache Guacamole через Docker Compose

Apache Guacamole — это клиент удалённого доступа, который позволяет пользователям подключаться к различным системам с помощью веб-браузера. Использование Docker Compose для развертывания Apache Guacamole значительно упрощает установку и управление его компонентами.

Вот шаги, чтобы развернуть Apache Guacamole с использованием Docker Compose:

1. **Создайте файл `docker-compose.yml`:**
В этом файле определены три сервиса: `guacamole`, `guacd` и `mysql`.

2. **Запустите Docker Compose:**

   Откройте терминал, перейдите в каталог, где находится ваш файл `docker-compose.yml`, и выполните команду:

   ```sh
   docker-compose up -d
   ```

   Этот процесс загрузит необходимые образы, создаст и запустит контейнеры.

3. **Настройка базы данных:**

   После того как контейнеры будут запущены, необходимо настроить базу данных для использования Apache Guacamole. Это можно сделать, запустив инициализационный скрипт базы данных, предоставляемый Guacamole:

   Скачайте скрипты инициализации базы данных с [официального сайта Apache Guacamole](https://guacamole.apache.org/doc/gug/jdbc-auth.html):

   ```sh
   docker run --rm guacamole/guacamole /opt/guacamole/bin/initdb.sh --mysql > initdb.sql
   ```

   Выполните инициализационный скрипт в контейнере MySQL:

   ```sh
   docker cp initdb.sql mysql:/initdb.sql
   docker exec -it mysql bash
   mysql -u root -p guacamole_db < /initdb.sql
   ```

4. **Доступ к Guacamole:**

   После выполнения всех шагов, Guacamole будет доступен по адресу `http://localhost:8080/guacamole`.

Теперь у вас должно быть работающая установка Apache Guacamole через Docker Compose. Вы можете войти в систему, используя созданную базу данных и управлять своими подключениями через веб-интерфейс.
По умолчанию Apache Guacamole создаёт пользователя с именем guacadmin и паролем guacadmin
