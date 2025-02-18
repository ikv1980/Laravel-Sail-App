# Laravel-Sail-App
##### 1.2. Установка через  Docker
- Прежде чем создавать приложение Laravel, необходимо установить [Docker Desktop](https://www.docker.com/products/docker-desktop) и необходимо установить и включить Windows Subsystem for [Linux 2 (WSL2)](https://docs.microsoft.com/en-us/windows/wsl/install-win10). После установки и включения WSL2 необходимо убедиться, что Docker Desktop настроен для использования [бэкенда WSL2](https://docs.docker.com/docker-for-windows/wsl/).
После всех приготовленний разворачиваем проект командой
``` bash
# запуск WSL (можно через кнопку Пуск)
wsl
# переход в папку проекта
cd /mnt/c/Users/twkos/MADK/Temp/
# создание нового приложения 
curl -s https://laravel.build/doc-app | bash
# запуск Laravel Sail из корневой папки приложения
cd doc-app
./vendor/bin/sail up -d     # запустить (-d в фоне)
./vendor/bin/sail down      # остановить
./vendor/bin/sail shell     # заходим внутрь контейнера
./vendor/bin/sail share     # публичная ссылка
# миграции базы данных (можно вначале поправить .ENV)
./vendor/bin/sail artisan migrate
```
__Примечание:__ _в первый раз развертывание проекта будет достаточное продолжительное время._
Более подробно подробно смотри документацию [SAIL](https://laravel.com/docs/11.x/sail)
Например, чтобы не вводить длинную команду `./vendor/bin/sail` можно настроить alias. Запускаем WSL, вводим команду `nano ~/.bashrc
` и прописываем внутри файла команду `alias sail='sh $([ -f sail ] && echo sail || echo vendor/bin/sail)'`
