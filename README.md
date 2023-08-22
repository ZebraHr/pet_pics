
# Kittygram
Социальная сеть для любителей котиков. Здесь можно добавлять фото и достижения любимых пушистых хвостиков.
Проект предназанчен для запуска на удаленном сервере.


## Технологии:
Python 3.9
Django 3.2.3
djangorestframework 3.12.4
Nginx
gunicorn
Docker

## Описание работы:
В проекте Kittygram_final для удаленного сервера можно добавлять фото и достижения любимых пушистых хвостиков, а так же просматривать котиков других пользователей.

## Установка проекта
- Сделайте fork репозитория, затем клонируйте его:
```
git clone https://github.com/ZebraHr/kittygram_final
```
- Для адаптации проекта на своем удаленном сервере добавьте секреты в GitHub Actions:
```
DOCKER_USERNAME                # имя пользователя в DockerHub
DOCKER_PASSWORD                # пароль пользователя в DockerHub
HOST                           # ip_address сервера
USER                           # имя пользователя
SSH_KEY                        # приватный ssh-ключ (cat ~/.ssh/id_rsa)
SSH_PASSPHRASE                 # кодовая фраза (пароль) для ssh-ключа

TELEGRAM_TO                    # id телеграм-аккаунта (можно узнать у @userinfobot, команда /start)
TELEGRAM_TOKEN                 # токен бота (получить токен можно у @BotFather, /token, имя бота)
```
- На удаленном сервере создайте папку kittygram/
- На удаленном сервере в папке проекта cоздайте файл .env:
```
POSTGRES_DB=<Желаемое_имя_базы_данных>
POSTGRES_USER=<Желаемое_имя_пользователя_базы_данных>
POSTGRES_PASSWORD=<Желаемый_пароль_пользователя_базы_данных>
DB_HOST=db
DB_PORT=5432

SECRET_KEY = 'ваш_secret_key'
ALLOWED_HOSTS = ip_удаленного сервера, 127.0.0.1, localhost
DEBUG = False
```
- Установка Nginx. Находясь на удалённом сервере, из любой директории выполните команду, затем запустите Nginx:
```
sudo apt install nginx -y 
sudo systemctl start nginx
```
- Перейдите в файл конфигурации nginx и измените его настройки на следующие:
```
nano /etc/nginx/sites-enabled/default
```
```
server {
    server_name server_name <публичный-IP-адрес> <доменное-имя>;

    location / {
        proxy_pass http://127.0.0.1:9000;
    }

}
```
- Перезарузите Nginx:
```
sudo nginx -t
sudo systemctl reload nginx
```
- Откройте порты для фаервола и активируйте его:
```
sudo ufw allow 'Nginx Full'
sudo ufw allow OpenSSH
sudo ufw enable
```
- (Опционально) Получите SSL-сертификат для вашего доменного имени с помощью Certbot:
```
sudo apt install snapd
sudo snap install core; sudo snap refresh core
sudo snap install --classic certbot
sudo ln -s /snap/bin/certbot /usr/bin/certbot 
sudo certbot --nginx
```
- Пуш в ветку main запускает тестирование и деплой Kittygram на ваш удаленный сервер, а после успешного деплоя вам приходит оповещение в телеграм.

### Автор
Анна Победоносцева

Студент Яндекс Практикума ["Python-разаботчик плюс"](https://practicum.yandex.ru/python-developer-plus/?from=catalog)

GitHub:
(https://github.com/ZebraHr)
