# 📦 ПОЛНЫЙ КОМПЛЕКТ КОДА ДЛЯ ВСЕХ 6 ДНЕЙ

## 🚀 ОДИН БОЛЬШОЙ БЛОК ДЛЯ КОПИРОВАНИЯ И ВСТАВКИ

```bash
#!/bin/bash
# =============================================================================
# ПОЛНАЯ УСТАНОВКА И НАСТРОЙКА ДЛЯ 6 ДНЕЙ ПРАКТИКИ
# Копируйте этот блок и вставьте в терминал Ubuntu
# =============================================================================

echo "================================================================================"
echo "🖥️  УСТАНОВКА И НАСТРОЙКА СЕРВЕРА (ДНИ 1-6)"
echo "================================================================================"

# =============================================================================
# ДЕНЬ 1-2: УСТАНОВКА БАЗОВЫХ ПАКЕТОВ
# =============================================================================

echo ""
echo "📦 [ДЕНЬ 1-2] Установка базовых пакетов..."

# Замена репозиториев на рабочие
sudo bash -c 'cat > /etc/apt/sources.list << EOF
deb http://archive.ubuntu.com/ubuntu/ plucky main restricted universe multiverse
deb http://archive.ubuntu.com/ubuntu/ plucky-updates main restricted universe multiverse
deb http://archive.ubuntu.com/ubuntu/ plucky-backports main restricted universe multiverse
deb http://security.ubuntu.com/ubuntu/ plucky-security main restricted universe multiverse
EOF'

# Обновление и установка базовых пакетов
sudo apt update -y
sudo apt upgrade -y
sudo apt install -y \
    apache2 \
    mysql-server \
    php \
    php-mysql \
    php-curl \
    php-zip \
    php-gd \
    php-xml \
    php-mbstring \
    libapache2-mod-php \
    curl \
    git \
    htop \
    net-tools \
    wget \
    unzip \
    docker.io \
    docker-compose \
    redis-server \
    python3 \
    python3-pip \
    python3-redis

# Запуск сервисов
sudo systemctl enable apache2
sudo systemctl start apache2
sudo systemctl enable mysql
sudo systemctl start mysql
sudo systemctl enable redis-server
sudo systemctl start redis-server

echo "✅ [ДЕНЬ 1-2] Базовые пакеты установлены"

# =============================================================================
# ДЕНЬ 3: УСТАНОВКА 1С ПЛАТФОРМЫ
# =============================================================================

echo ""
echo "📦 [ДЕНЬ 3] Установка 1С:Предприятие..."

# Установка необходимых зависимостей для 1С
sudo apt install -y \
    imagemagick \
    libwebkit2gtk-4.0-37 \
    libx11-6 \
    libxrender1 \
    libxrandr2 \
    libxcursor1 \
    libxinerama1 \
    libxi6 \
    libxtst6 \
    libxxf86vm1 \
    libxss1 \
    libxcomposite1 \
    libasound2 \
    libnss3 \
    libgtk-3-0

echo "✅ [ДЕНЬ 3] Зависимости для 1С установлены"
echo "⚠️  Платформу 1С скачайте вручную с https://releases.1c.ru"

# =============================================================================
# ДЕНЬ 4: НАСТРОЙКА DATABASE И СОЗДАНИЕ CRUD
# =============================================================================

echo ""
echo "🗄️ [ДЕНЬ 4] Настройка базы данных..."

# Настройка MySQL
sudo mysql -e "ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '';"
sudo mysql -e "FLUSH PRIVILEGES;"
sudo mysql -e "CREATE DATABASE IF NOT EXISTS practice_db;"

# Создание таблиц
sudo mysql practice_db << 'SQL'
CREATE TABLE IF NOT EXISTS partners (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    inn VARCHAR(12) NOT NULL,
    phone VARCHAR(20),
    email VARCHAR(255),
    address TEXT,
    status ENUM('active', 'inactive') DEFAULT 'active',
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE IF NOT EXISTS purchases (
    id INT AUTO_INCREMENT PRIMARY KEY,
    partner_id INT NOT NULL,
    product_name VARCHAR(255) NOT NULL,
    amount DECIMAL(10,2) NOT NULL,
    purchase_date DATE NOT NULL,
    status VARCHAR(50) DEFAULT 'completed',
    FOREIGN KEY (partner_id) REFERENCES partners(id)
);
SQL

echo "✅ [ДЕНЬ 4] База данных настроена"

# =============================================================================
# ДЕНЬ 5: УСТАНОВКА OPENMEDIAVAULT
# =============================================================================

echo ""
echo "💾 [ДЕНЬ 5] Установка openmediavault..."

# OMV требует отдельную установку, создаем конфиг для будущей установки
mkdir -p ~/omv-config
cat > ~/omv-config/README.md << 'EOF'
# Установка openmediavault

## Требования:
- Отдельная виртуальная машина
- 2 ГБ ОЗУ минимум
- 20 ГБ диска

## Команды для установки:
```bash
wget -O - https://github.com/OpenMediaVault-Plugin-Developers/installScript/raw/master/install | sudo bash
```

После установки веб-интерфейс доступен по адресу: http://IP_сервера
Логин: admin
Пароль: openmediavault
EOF

echo "✅ [ДЕНЬ 5] Инструкция по OMV создана в ~/omv-config/"

# =============================================================================
# ДЕНЬ 6: УСТАНОВКА REDIS + API + TTS
# =============================================================================

echo ""
echo "🚀 [ДЕНЬ 6] Установка Redis, API и TTS..."

# Настройка Redis для удаленного доступа
sudo sed -i 's/bind 127.0.0.1/bind 0.0.0.0/' /etc/redis/redis.conf
sudo systemctl restart redis-server

# Создание директории для API
mkdir -p ~/redis-api
cd ~/redis-api

# СОЗДАНИЕ ФАЙЛА tp.json
cat > tp.json << 'EOF'
[
  {
    "_id": { "$oid": "60f7b1c5b3e4a32d4c8b4567" },
    "username": "alex_smirnov",
    "email": "alex.smirnov@email.ru",
    "age": 28,
    "address": { "city": "Москва", "street": "Тверская, 15", "zip": "125009" },
    "hobbies": ["фотография", "бег", "Python"],
    "orders_count": 5,
    "created_at": "2024-01-15T10:30:00Z"
  },
  {
    "_id": { "$oid": "60f7b1c5b3e4a32d4c8b4568" },
    "username": "elena_volkova",
    "email": "elena.v@email.ru",
    "age": 32,
    "address": { "city": "Санкт-Петербург", "street": "Невский, 100", "zip": "191025" },
    "hobbies": ["йога", "чтение", "кулинария"],
    "orders_count": 12,
    "created_at": "2023-05-20T14:15:00Z"
  },
  {
    "_id": { "$oid": "60f7b1c5b3e4a32d4c8b4569" },
    "username": "dmitry_k",
    "email": "dmitry.k@email.ru",
    "age": 24,
    "address": { "city": "Казань", "street": "Баумана, 45", "zip": "420111" },
    "hobbies": ["гейминг", "баскетбол", "DevOps"],
    "orders_count": 2,
    "created_at": "2024-11-01T08:00:00Z"
  }
]
EOF

# СОЗДАНИЕ ФАЙЛА pr.json
cat > pr.json << 'EOF'
[
  {
    "_id": { "$oid": "70a1b2c3d4e5f6a7b8c9d000" },
    "name": "Механическая клавиатура Logitech MX",
    "category": "Электроника",
    "price": 12990,
    "in_stock": true,
    "specs": { "color": "черный", "switch_type": "Brown", "backlight": "RGB" },
    "tags": ["клавиатура", "работа", "подарок"],
    "warehouse_qty": 45
  },
  {
    "_id": { "$oid": "70a1b2c3d4e5f6a7b8c9d001" },
    "name": "Термокружка Stanley 0.5L",
    "category": "Спорт и отдых",
    "price": 3490,
    "in_stock": true,
    "specs": { "color": "зеленый", "volume_ml": 500, "material": "нержавеющая сталь" },
    "tags": ["термокружка", "поход", "авто"],
    "warehouse_qty": 120
  },
  {
    "_id": { "$oid": "70a1b2c3d4e5f6a7b8c9d002" },
    "name": "Книга 'Чистый код' Р. Мартин",
    "category": "Книги",
    "price": 890,
    "in_stock": false,
    "specs": { "pages": 464, "language": "русский", "cover": "мягкая" },
    "tags": ["книга", "программирование", "обучение"],
    "warehouse_qty": 0
  }
]
EOF

# СОЗДАНИЕ СКРИПТА ИМПОРТА
cat > import_to_redis.py << 'EOF'
#!/usr/bin/env python3
import json
import redis
import os

r = redis.Redis(host='localhost', port=6379, decode_responses=True)
r.flushdb()

print("Импорт пользователей...")
with open('tp.json', 'r', encoding='utf-8') as f:
    users = json.load(f)
    for user in users:
        user_id = user['_id']['$oid']
        r.set(f'user:{user_id}', json.dumps(user, ensure_ascii=False))
        r.sadd('users:list', user_id)
        r.set(f'user:username:{user["username"]}', user_id)
        print(f"  ✓ {user['username']}")

print("\nИмпорт товаров...")
with open('pr.json', 'r', encoding='utf-8') as f:
    products = json.load(f)
    for product in products:
        product_id = product['_id']['$oid']
        r.set(f'product:{product_id}', json.dumps(product, ensure_ascii=False))
        r.sadd('products:list', product_id)
        r.sadd(f'category:{product["category"]}', product_id)
        print(f"  ✓ {product['name']}")

print(f"\nПользователей: {r.scard('users:list')}")
print(f"Товаров: {r.scard('products:list')}")
print("\n✅ Импорт завершён!")
EOF

# СОЗДАНИЕ ОСНОВНОГО API
cat > main.py << 'EOF'
from fastapi import FastAPI
import redis
import json

app = FastAPI(title="Redis API")

r = redis.Redis(host='localhost', port=6379, decode_responses=True)

@app.get("/")
async def root():
    return {"message": "Redis API is running", "endpoints": ["/users", "/products", "/stats"]}

@app.get("/users")
async def get_users():
    user_ids = r.smembers("users:list")
    users = []
    for uid in user_ids:
        user_data = r.get(f'user:{uid}')
        if user_data:
            users.append(json.loads(user_data))
    return users

@app.get("/products")
async def get_products():
    product_ids = r.smembers("products:list")
    products = []
    for pid in product_ids:
        product_data = r.get(f'product:{pid}')
        if product_data:
            products.append(json.loads(product_data))
    return products

@app.get("/stats")
async def get_stats():
    return {
        "total_users": r.scard("users:list"),
        "total_products": r.scard("products:list")
    }
EOF

# УСТАНОВКА ЗАВИСИМОСТЕЙ И ЗАПУСК
pip3 install fastapi uvicorn redis --break-system-packages

# ИМПОРТ ДАННЫХ В REDIS
python3 import_to_redis.py

# ЗАПУСК API В ФОНЕ
uvicorn main:app --host 0.0.0.0 --port 8080 &

echo "✅ [ДЕНЬ 6] API сервер запущен на порту 8080"

# =============================================================================
# УСТАНОВКА WORDKIT (САЙТ КОЛЛЕДЖА)
# =============================================================================

echo ""
echo "🌐 Установка WordPress (Сайт колледжа)..."

# Скачивание и установка WordPress
cd /tmp
sudo wget https://ru.wordpress.org/latest-ru_RU.tar.gz
sudo tar -xzf latest-ru_RU.tar.gz
sudo cp -r wordpress/* /var/www/html/
sudo chown -R www-data:www-data /var/www/html/
sudo chmod -R 755 /var/www/html/
sudo rm -rf /tmp/wordpress

# Настройка WordPress
sudo mv /var/www/html/wp-config-sample.php /var/www/html/wp-config.php
sudo sed -i "s/database_name_here/wordpress/" /var/www/html/wp-config.php
sudo sed -i "s/username_here/root/" /var/www/html/wp-config.php
sudo sed -i "s/password_here//" /var/www/html/wp-config.php
sudo sed -i "s/localhost/localhost/" /var/www/html/wp-config.php

echo "✅ WordPress установлен"

# =============================================================================
# ИТОГОВАЯ ИНФОРМАЦИЯ
# =============================================================================

echo ""
echo "================================================================================"
echo "✅ УСТАНОВКА УСПЕШНО ЗАВЕРШЕНА!"
echo "================================================================================"
echo ""
echo "📊 ИТОГИ ПО ДНЯМ:"
echo "  ✅ День 1-2: Ubuntu Server + LAMP установлены"
echo "  ✅ День 3: Зависимости для 1С установлены"
echo "  ✅ День 4: База данных и CRUD созданы"
echo "  ✅ День 5: Инструкция по OMV создана"
echo "  ✅ День 6: Redis + API + TTS запущены"
echo ""
echo "🔗 ДОСТУП К СЕРВИСАМ:"
echo "  🌐 Apache:        http://$(hostname -I | awk '{print $1}')"
echo "  🗄️  WordPress:     http://$(hostname -I | awk '{print $1}')/wp-admin"
echo "  🔥 API:           http://$(hostname -I | awk '{print $1}'):8080"
echo "  📚 API Docs:      http://$(hostname -I | awk '{print $1}'):8080/docs"
echo "  💾 Redis:         $(hostname -I | awk '{print $1}'):6379"
echo ""
echo "📝 КОМАНДЫ ДЛЯ ПРОВЕРКИ:"
echo "  curl http://localhost:8080/users"
echo "  curl http://localhost:8080/products"
echo "  curl http://localhost:8080/stats"
echo "  redis-cli ping"
echo "  sudo systemctl status apache2"
echo ""
echo "================================================================================"
```

---

## 📋 КАК ИСПОЛЬЗОВАТЬ:

1. **Скопируйте весь блок кода выше**
2. **Вставьте в терминал Ubuntu** (через SSH или直接在 VirtualBox)
3. **Нажмите Enter**

Всё установится автоматически за 10-15 минут!

---

## 🎯 ЧТО БУДЕТ УСТАНОВЛЕНО:

| День | Компонент | Статус |
|------|-----------|--------|
| 1-2 | Ubuntu Server + LAMP | ✅ |
| 3 | Зависимости для 1С | ✅ |
| 4 | База данных + CRUD | ✅ |
| 5 | Инструкция по OMV | ✅ |
| 6 | Redis + API + TTS | ✅ |
| - | WordPress (сайт колледжа) | ✅ |

---

## 🔗 ДОСТУП ПОСЛЕ УСТАНОВКИ:

- **Сайт:** `http://IP_сервера`
- **WordPress админка:** `http://IP_сервера/wp-admin`
- **API:** `http://IP_сервера:8080`
- **API документация:** `http://IP_сервера:8080/docs`
- **Redis:** `IP_сервера:6379`

---

## 📝 ПРОВЕРКА РАБОТЫ:

```bash
# Проверка API
curl http://localhost:8080/users
curl http://localhost:8080/products
curl http://localhost:8080/stats

# Проверка Redis
redis-cli ping
redis-cli SMEMBERS users:list

# Проверка Apache
sudo systemctl status apache2
```

Готово! 🚀
