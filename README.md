# Laravel-Sail-App
##### 1.2. Установка через  Docker
- Прежде чем создавать приложение Laravel, необходимо установить [Docker Desktop](https://www.docker.com/products/docker-desktop) и необходимо установить и включить Windows Subsystem for [Linux 2 (WSL2)](https://docs.microsoft.com/en-us/windows/wsl/install-win10). После установки и включения WSL2 необходимо убедиться, что Docker Desktop настроен для использования [бэкенда WSL2](https://docs.docker.com/docker-for-windows/wsl/).
После всех приготовленний разворачиваем проект командой
``` bash
# запуск WSL (можно через кнопку Пуск). Выход: logout
wsl
# переход в папку проекта
cd /mnt/c/Users/twkos/MADK/Temp/
# создание нового приложения 
curl -s https://laravel.build/Laravel-Sail-App | bash
# переходим в папку с проектом 
cd Laravel-Sail-App
# запуск Laravel Sail и настройка  Docker
./vendor/bin/sail up -d     # запустить (-d в фоне)
./vendor/bin/sail down      # остановить
./vendor/bin/sail shell     # заходим внутрь контейнера
./vendor/bin/sail share     # публичная ссылка
# миграции базы данных (можно вначале поправить .ENV)
./vendor/bin/sail artisan migrate
```
##### 1.2 Разворачивание проекта после скачивания с GitHub
``` conf
# Скачайте проект с GitHub
git clone https://github.com/ikv1980/Laravel-Sail-App.git
# Установите зависимости
composer install
# Создайте файл .env (или скопируйте нужный)
cp .env.example .env
# запуск WSL (можно через кнопку Пуск). Выход: logout
wsl
# запуск Laravel Sail и настройка Docker
./vendor/bin/sail up -d     # запустить (-d в фоне)
# Выполните команду для генерации ключа приложения
# Этот ключ автоматически добавляется в файл .env проекта в переменную APP_KEY.
sail artisan key:generate
# Если проект использует базу данных, выполните миграции (fresh - перезапись БД)
sail artisan migrate
sail artisan migrate:fresh
sail artisan migrate:rollback    # откат последних изменений
sail artisan migrate:reset       # откат всех миграций
# Для разработки вы можете использовать встроенный сервер
sail artisan serve
--host=127.0.0.1    # адрес хоста, на котором будет запущен сервер (localhost)
--port=8080         # порт, который будет использоваться сервером (8000)
--no-reload         # отключает автоматическую перезагрузку сервера при изменении файлов
--quiet             # подавляет вывод сообщений об ошибках и логов в консоль
# Можно запускать и composer run dev, но тут следует учесть, эта команда запускает задачи, определенные в секции scripts файла composer.json
# По умолчанию сервер будет доступен по адресу http://localhost:8000
```

##### 1.3 Рекомендации для разработки
Во время разработки рекомендуется регулярно очищать кеш:
```bash
sail artisan cache:clear
sail artisan config:clear
sail artisan route:clear
sail artisan view:clear
```
Так же можно отключить на время разработки кеш в браузере (Chrome, FireFox):
- Жмем `F12` или `Ctrl + Shift + I` (Windows/Linux);
- В открывшихся инструментах разработчика идем вкладку "Network"(Сеть); 
- На панели инструментов вкладки "Network"  найдите флажок (checkbox) с надписью "Disable cache (while DevTools is open)"  (Отключить кэш (при открытом DevTools)).





















__Примечание:__ _в первый раз развертывание проекта будет достаточное продолжительное время._
Более подробно подробно смотри документацию [SAIL](https://laravel.com/docs/11.x/sail)
Например, чтобы не вводить длинную команду `./vendor/bin/sail` можно настроить alias. Запускаем WSL, вводим команду `nano ~/.bashrc
` и прописываем внутри файла команду `alias sail='sh $([ -f sail ] && echo sail || echo vendor/bin/sail)'`
