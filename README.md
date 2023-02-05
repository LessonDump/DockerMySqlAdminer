# MySQL + Adminer на базе docker-compose

## Требования:

- docker
- docker-compose

## Команды:

- поднять контейнер: `$ docker-compose --compatibility up -d`
- остановить запущенный контейнер: `$ docker-compose --compatibility stop`
- запустить остановленный контейнер: `$ docker-compose --compatibility start`
- остановить и удалить контейнер и сеть: `$ docker-compose --compatibility down`
- удалить директорию 'mysql': `$ sudo rm -r mysql`

## Доступ к MySQL:

- **Root password:** `root`
- **URL:** `localhost:3306`
- **Database:** `database`
- **Username:** `admin`
- **Password:** `admin`

## Доступ к Adminer:

- **URL:** `http://localhost:8080`

## Коннект к MySQL из Adminer

- **System** `MySQL`
- **Server:** `mysql_container:3306`
- **Username:** `admin`
- **Password:** `admin`
- **Database:** `database`

## Переменные окружения:

- `LANG`: C.UTF-8
- `MYSQL_ROOT_PASSWORD`: по умолчанию — **root**
- `MYSQL_USER`: по умолчанию — **admin**
- `MYSQL_PASSWORD`: по умолчанию — **admin**
- `MYSQL_DATABASE`: по умолчанию — **database**
- `ADMINER_DEFAULT_DB_DRIVER`: **mysql**
- `ADMINER_DEFAULT_DB_HOST`: **mysql_container:3306**
- `ADMINER_DEFAULT_DB_NAME`: **database**

## Первичная инициализация структуры БД:

- При выполнении команды `docker-compose up` будут выполнены все скрипты из директории `initdb`.
- Любые `*.sql` или `*.sh` файлы в этом каталоге будут рассматриваться как скрипты для инициализации БД.
- Если БД уже была проинициализирована ранее, то никакие изменения к ней применяться не будут.
- Если в каталоге присутствует несколько файлов, то они будут отсортированы по имени с использованием текущей локали (по умолчанию en_US.utf8).
- Если инициализация не нужна, достаточно очистить каталок `initdb` перед выполнением команды `docker-compose up`.

## Размещение данных БД:

- При выполнении команды `docker-compose up` рядом со скриптом создайтся директория `mysql`, где будут располагаться файлы БД.
- При новой инициализации БД директорию `mysql` можно удалить: `$ sudo rm -r mysql`

## Параметры контейнера:

- В блоке кода `healthcheck:` задана периодическая проверка состояния/работоспособности БД и перезапуск контейнера при неполадках.
- Для отмены такой проверки достаточно удалить блок кода `healthcheck:`.

<!-- -->

- В блоке кода `deploy:` заданы ограничения ресурсов для контейнера с БД.
- Для отмены ограничений достаточно удалить блок кода `deploy:`.
