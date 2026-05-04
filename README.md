# 📄 ПОЛНЫЙ ОТЧЁТ ПО УЧЕБНОЙ ПРАКТИКЕ ПМ 04

## Студент: Баталовв Сергей Андреевич
## Группа: 23П-1
## Специальность: 09.02.07 Информационные системы и программирование
## Руководитель: Калинин Арсений Олегович

---

# ДНЕВНИК ПРАКТИКИ

## День 1 — VirtualBox и Ubuntu

### Выполненные задачи:

| № | Задача | Результат |
|---|--------|-----------|
| 1 | Установка Oracle VirtualBox | Установлен (Рисунок 1) |
| 2 | Установка образа Ubuntu | Установлен (Рисунок 2) |
| 3 | Создание пользователя | Создан (Рисунок 3) |
| 4 | Установка антивируса ClamAV | Установлен (Рисунки 4, 5) |
| 5 | Установка архиватора 7zip | Установлен (Рисунок 6) |
| 6 | Установка LibreOffice | Установлен (Рисунок 7) |
| 7 | Установка браузера Firefox | Установлен (Рисунок 8) |
| 8 | Установка Evince (PDF-reader) | Установлен (Рисунок 9) |

### Ключевые команды:

```bash
# Установка VirtualBox
sudo apt update
sudo apt install virtualbox -y

# Установка Ubuntu (через ISO образ)
# Создание пользователя при установке

# Установка ClamAV
sudo apt install clamav clamav-daemon -y
sudo systemctl start clamav-daemon
sudo freshclam

# Установка 7zip
sudo apt install p7zip-full p7zip-rar -y

# Установка LibreOffice
sudo apt install libreoffice -y

# Установка Firefox
sudo apt install firefox -y

# Установка Evince
sudo apt install evince -y
```

---

## День 2 — RedOS и база данных

### Выполненные задачи:

| № | Задача | Результат |
|---|--------|-----------|
| 1 | Обновление системы | Выполнено (Рисунок 1) |
| 2 | Установка LibreOffice | Установлен (Рисунок 2) |
| 3 | Установка PeaZip | Установлен (Рисунок 3) |
| 4 | Установка PDF-reader | Установлен (Рисунок 4) |
| 5 | Установка LMD | Установлен (Рисунок 5) |
| 6 | Установка VS Code | Установлен (Рисунок 6) |
| 7 | Установка RedDataBase | Установлена (Рисунки 7, 8) |
| 8 | Создание и заполнение БД | Выполнено (Рисунок 8) |
| 9 | Установка 1С | ❌ Не удалась |

### Ключевые команды:

```bash
# Обновление системы RedOS
sudo apt update && sudo apt upgrade -y

# Установка LibreOffice
sudo apt install libreoffice -y

# Установка PeaZip
sudo apt install peazip -y

# Установка VS Code
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
sudo sh -c 'echo -e "[code]\nname=Visual Studio Code\nbaseurl=https://packages.microsoft.com/yumrepos/vscode\nenabled=1\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/yum.repos.d/vscode.repo'
sudo apt install code -y

# Установка RedDataBase
# Скачано с официального сайта RedSoft
```

### Создание базы данных (SQL):

```sql
CREATE DATABASE practice_db;
USE practice_db;

CREATE TABLE students (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100),
    group_name VARCHAR(20),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

INSERT INTO students (name, group_name) VALUES 
('Кононов Тимофей', '23П-1'),
('Баталов Сергей', '23П-1');
```

---

## День 3 — Канбан-доска и обработка

### Выполненные задачи:

| № | Задача | Результат |
|---|--------|-----------|
| 1 | Создание регистров сведений | Выполнено |
| 2 | Создание регистров накопления | Выполнено |
| 3 | Разработка обработки пр_ПроверкаКанбан.epf | Разработана |
| 4 | Реализация проверки просрочек | Реализовано |
| 5 | Настройка уведомлений | Настроено |
| 6 | Создание динамической формы настроек | Создана (Рисунки 1, 2) |

### Код обработки (1С):

```1c
// Обработка пр_ПроверкаКанбан.epf

&НаСервере
Процедура ПроверитьПросрочкиНаСервере()
    // Проверка задач с истекшим сроком
    Запрос = Новый Запрос;
    Запрос.Текст = 
    "ВЫБРАТЬ
    |   КанбанЗадачи.Ссылка,
    |   КанбанЗадачи.Название,
    |   КанбанЗадачи.СрокИсполнения,
    |   КанбанЗадачи.Статус
    |ИЗ
    |   РегистрСведений.КанбанЗадачи КАК КанбанЗадачи
    |ГДЕ
    |   КанбанЗадачи.СрокИсполнения < ТЕКУЩАЯДАТА()
    |   И КанбанЗадачи.Статус <> "Выполнена"";
    
    Результат = Запрос.Выполнить();
    
    Если НЕ Результат.Пустой() Тогда
        Сообщение = Новый СообщениеПользователю;
        Сообщение.Текст = "Обнаружены просроченные задачи!";
        Сообщение.Сообщить();
    КонецЕсли;
КонецПроцедуры
```

---

## День 4 — Git и хранилище

### Выполненные задачи:

| № | Задача | Результат |
|---|--------|-----------|
| 1 | Выгрузка базы данных | Выполнено (Рисунок 1) |
| 2 | Загрузка данных в хранилище | Выполнено (Рисунок 2) |
| 3 | Подключение к GitLab | Выполнено (Рисунок 3) |
| 4 | Выгрузка файла .cfe | Выполнено (Рисунок 4) |

### Ключевые команды Git:

```bash
# Инициализация репозитория
git init

# Настройка пользователя
git config --global user.name "Кононов Тимофей"
git config --global user.email "timofey@example.com"

# Добавление файлов
git add .
git commit -m "Добавлена конфигурация 1С"

# Подключение к GitLab
git remote add origin https://gitlab.com/kononov/practice-2026.git

# Выгрузка
git push -u origin main

# Выгрузка конфигурации 1С в файл .cfe
# В 1С: Конфигурация -> Выгрузить конфигурацию в файл
```

---

## День 5 — SMB и файловый сервер

### Выполненные задачи:

| № | Задача | Результат |
|---|--------|-----------|
| 1 | Настройка сети | Выполнено (Рисунок 3) |
| 2 | Создание учётной записи | Создана (Рисунок 4) |
| 3 | Открытие окна сервера | Открыто (Рисунок 5) |
| 4 | Настройка IP | Настроен (Рисунок 6) |
| 5 | Подключение к серверу | Подключено (Рисунок 7) |
| 6 | Создание файловой системы | Создана (Рисунок 8) |
| 7 | Создание общей папки | Создана (Рисунок 9) |
| 8 | Проверка доступности папки | Проверено (Рисунок 10) |
| 9 | Создание пользователя | Создан (Рисунок 11) |
| 10 | Настройка SMB | Настроено (Рисунки 12, 13) |
| 11 | Загрузка файлов в папку | Загружены (Рисунок 14) |

### Конфигурация SMB (/etc/samba/smb.conf):

```ini
[global]
   workgroup = WORKGROUP
   server string = %h server (Samba, Ubuntu)
   server role = standalone server
   map to guest = Bad User

[shared]
   path = /srv/samba/shared
   browseable = yes
   read only = no
   guest ok = no
   create mask = 0755
   valid users = @sambashare
```

### Команды для настройки SMB:

```bash
# Установка Samba
sudo apt install samba -y

# Создание общей папки
sudo mkdir -p /srv/samba/shared
sudo chmod 777 /srv/samba/shared

# Настройка пользователя
sudo smbpasswd -a timofey

# Перезапуск сервера
sudo systemctl restart smbd

# Проверка подключения
smbclient -L localhost -U timofey
```

---

## День 6 — Redis, API и веб-сервер

### Выполненные задачи:

| № | Задача | Результат |
|---|--------|-----------|
| 1 | Установка Ubuntu | Выполнено (Рисунок 1) |
| 2 | Установка PuTTY и подключение | Выполнено (Рисунок 3) |
| 3 | Проверка статуса сервера | Проверено (Рисунок 4) |
| 4 | Задание пароля | Задан (Рисунок 5) |
| 5 | Пинг и аутентификация | Пройдены (Рисунок 6) |
| 6 | Подключение через Redis Desktop Manager | Подключено (Рисунок 7) |
| 7 | Создание начального тела сайта | Создано (Рисунок 8) |
| 8 | Настройка окна авторизации | Настроено (Рисунок 9) |
| 9 | Настройка API | Настроено (Рисунок 10) |
| 10 | Создание итогового тела сайта | Создано (Рисунок 11) |
| 11 | Установка нейросети | Установлена (Рисунок 12) |

### Установка Redis и API:

```bash
# Установка Redis
sudo apt install redis-server -y
sudo systemctl enable redis-server
sudo systemctl start redis-server

# Настройка пароля
sudo sed -i 's/# requirepass foobared/requirepass mypassword/' /etc/redis/redis.conf
sudo systemctl restart redis-server

# Проверка
redis-cli -a mypassword ping
```

### API на FastAPI (main.py):

```python
from fastapi import FastAPI
import redis
import json

app = FastAPI(title="API Сервер")

r = redis.Redis(host='localhost', port=6379, password='mypassword', decode_responses=True)

@app.get("/")
async def root():
    return {"message": "API работает", "status": "ok"}

@app.get("/users")
async def get_users():
    return {"users": ["Кононов Тимофей", "Баталов Сергей"]}

@app.get("/health")
async def health():
    return {"status": "healthy"}
```

```bash
# Запуск API
pip install fastapi uvicorn redis
uvicorn main:app --host 0.0.0.0 --port 8000 &
```

---

## День 7 — LAMP-стек и WordPress

### Выполненные задачи:

| № | Задача | Результат |
|---|--------|-----------|
| 1 | Установка Nginx | Установлен (Рисунок 1) |
| 2 | Установка MySQL | Установлен (Рисунок 2) |
| 3 | Установка PHP | Установлен (Рисунок 3) |
| 4 | Создание БД и пользователя | Созданы (Рисунок 4) |
| 5 | Подключение к WordPress | Подключено (Рисунок 5) |
| 6 | Запуск готового сайта | Запущен (Рисунки 6, 7, 8) |

### Установка LAMP-стека:

```bash
# Установка Nginx
sudo apt install nginx -y
sudo systemctl start nginx
sudo systemctl enable nginx

# Установка MySQL
sudo apt install mysql-server -y
sudo mysql_secure_installation

# Установка PHP
sudo apt install php-fpm php-mysql php-curl php-zip php-gd php-xml php-mbstring -y

# Создание базы данных для WordPress
sudo mysql -e "CREATE DATABASE wordpress;"
sudo mysql -e "CREATE USER 'wpuser'@'localhost' IDENTIFIED BY 'wppassword';"
sudo mysql -e "GRANT ALL PRIVILEGES ON wordpress.* TO 'wpuser'@'localhost';"
sudo mysql -e "FLUSH PRIVILEGES;"
```

### Установка WordPress:

```bash
# Скачивание WordPress
cd /tmp
wget https://ru.wordpress.org/latest-ru_RU.tar.gz
tar -xzf latest-ru_RU.tar.gz
sudo cp -r wordpress/* /var/www/html/
sudo chown -R www-data:www-data /var/www/html/
sudo chmod -R 755 /var/www/html/
```

### Конфигурация Nginx (/etc/nginx/sites-available/wordpress):

```nginx
server {
    listen 80;
    server_name _;
    root /var/www/html;
    index index.php index.html;

    location / {
        try_files $uri $uri/ /index.php?$args;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php8.1-fpm.sock;
    }
}
```

---

# ИТОГИ ПРАКТИКИ

## Выполненные задачи:

| День | Тема | Статус |
|------|------|--------|
| День 1 | VirtualBox и Ubuntu | ✅ Выполнено |
| День 2 | RedOS и база данных | ✅ Выполнено (кроме 1С) |
| День 3 | Канбан-доска и обработка | ✅ Выполнено |
| День 4 | Git и хранилище | ✅ Выполнено |
| День 5 | SMB и файловый сервер | ✅ Выполнено |
| День 6 | Redis, API и веб-сервер | ✅ Выполнено |
| День 7 | LAMP-стек и WordPress | ✅ Выполнено |

## Освоенные навыки:

1. **Виртуализация:** VirtualBox, создание и настройка ВМ
2. **Операционные системы:** Ubuntu Server, RedOS
3. **Сетевые технологии:** SMB, файловый сервер, настройка сети
4. **Базы данных:** MySQL, Redis, RedDataBase
5. **API разработка:** FastAPI, REST API
6. **Веб-технологии:** Nginx, LAMP-стек, WordPress
7. **Системы контроля версий:** Git, GitLab
8. **Разработка на 1С:** Обработки, регистры, Канбан-доска
9. **Контейнеризация:** Docker (в процессе)

## Проблемы и решения:

| Проблема | Решение |
|----------|---------|
| Установка 1С на RedOS не удалась | Использована альтернативная платформа |
| Проблемы с подключением к Redis | Настроен пароль и права доступа |
| Ошибки при настройке SMB | Проверены права на папку и файл конфигурации |

## Заключение:

За 7 дней учебной практики я:

- ✅ Освоил VirtualBox, Ubuntu Server, RedOS
- ✅ Настроил SMB, Redis, LAMP-стек, WordPress
- ✅ Разработал внешнюю обработку для Канбан-доски
- ✅ Закрепил навыки работы с Git, GitLab, БД, API
- ✅ Создал работающий веб-сервер с WordPress
- ✅ Настроил файловый сервер и общие папки

**Практика пройдена успешно!**

---

# ПРИЛОЖЕНИЯ

## Список рисунков:

| Рисунок | Описание |
|---------|----------|
| 1 | Установка VirtualBox |
| 2 | Установка Ubuntu |
| 3 | Создание пользователя |
| 4-5 | Установка ClamAV |
| 6 | Установка 7zip |
| 7 | Установка LibreOffice |
| 8 | Установка Firefox |
| 9 | Установка Evince |
| 1-5 (День 2) | Установка ПО на RedOS |
| 6 (День 2) | Установка VS Code |
| 7-8 (День 2) | Установка RedDataBase |
| 1-2 (День 3) | Динамическая форма настроек |
| 1-4 (День 4) | Git и хранилище |
| 3-14 (День 5) | Настройка SMB |
| 1-12 (День 6) | Redis и API |
| 1-8 (День 7) | LAMP и WordPress |

---

**Студент:** _________________ Баталов Сергей Андреевич

**Руководитель:** _________________ Калинин Арсений Олегович

**Дата:** 2026 год
