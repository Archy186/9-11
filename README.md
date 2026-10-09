# Домашнее задание к занятию 5. «Практическое применение Docker»
# Задача 0  
Задача 0
Убедитесь что у вас НЕ(!) установлен docker-compose, для этого получите следующую ошибку от команды docker-compose --version
Command 'docker-compose' not found, but can be installed with:

sudo snap install docker          # version 24.0.5, or
sudo apt  install docker-compose  # version 1.25.0-1

See 'snap info docker' for additional versions.
В случае наличия установленного в системе docker-compose - удалите его.
2. Убедитесь что у вас УСТАНОВЛЕН docker compose(без тире) версии не менее v2.24.X, для это выполните команду docker compose version
# Ответ 
[Репозиторий](https://github.com/netology-code/shvirtd-example-python)

<img width="931" height="271" alt="Задание 0" src="https://github.com/user-attachments/assets/5a7974d9-174b-44bd-a284-24a814ae5ca5" />
# Задача 1
Создайте файл Dockerfile.python на основе существующего Dockerfile:
Используйте базовый образ python:3.12-slim
Обязательно используйте конструкцию COPY . . в Dockerfile
Создайте .dockerignore файл для исключения ненужных файлов
Используйте CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "5000"] для запуска
Протестируйте корректность сборки 2.1 Используйте multistage сборку вместо single stage.
# Ответ
<img width="933" height="688" alt="задание 1" src="https://github.com/user-attachments/assets/dba5aba5-92f8-4901-8689-eaab3efd6c9f" />

# Задача 3
Изучите файл "proxy.yaml"
Создайте в репозитории с проектом файл compose.yaml. С помощью директивы "include" подключите к нему файл "proxy.yaml".
Опишите в файле compose.yaml следующие сервисы:
web. Образ приложения должен ИЛИ собираться при запуске compose из файла Dockerfile.python ИЛИ скачиваться из yandex cloud container registry(из задание №2 со *). Контейнер должен работать в bridge-сети с названием backend и иметь фиксированный ipv4-адрес 172.20.0.5. Сервис должен всегда перезапускаться в случае ошибок. Передайте необходимые ENV-переменные для подключения к Mysql базе данных по сетевому имени сервиса web

db. image=mysql:8. Контейнер должен работать в bridge-сети с названием backend и иметь фиксированный ipv4-адрес 172.20.0.10. Явно перезапуск сервиса в случае ошибок. Передайте необходимые ENV-переменные для создания: пароля root пользователя, создания базы данных, пользователя и пароля для web-приложения.Обязательно используйте уже существующий .env file для назначения секретных ENV-переменных!

Запустите проект локально с помощью docker compose , добейтесь его стабильной работы: команда curl -L http://127.0.0.1:8090 должна возвращать в качестве ответа время и локальный IP-адрес. Если сервисы не стартуют воспользуйтесь командами: docker ps -a  и docker logs <container_name> . Если вместо IP-адреса вы получаете информационную ошибку --убедитесь, что вы шлете запрос на порт 8090, а не 5000.

Подключитесь к БД mysql с помощью команды docker exec -ti <имя_контейнера> mysql -uroot -p<пароль root-пользователя>(обратите внимание что между ключем -u и логином root нет пробела. это важно!!! тоже самое с паролем) . Введите последовательно команды (не забываем в конце символ ; ): show databases; use <имя вашей базы данных(по-умолчанию virtd, как это указано в .env)>; show tables; SELECT * from requests LIMIT 10;. Примечание: таблица в БД создается после первого поступившего запроса к приложению.

Остановите проект. В качестве ответа приложите скриншот sql-запроса.
# Ответ
<img width="935" height="960" alt="Задание 3" src="https://github.com/user-attachments/assets/a2e06cc4-0e6a-4cc0-bc18-5b31f8e2fa62" />
<img width="940" height="435" alt="Задание 3-1" src="https://github.com/user-attachments/assets/e0ffd518-76bc-445f-921a-a57a439c8f7a" />
<img width="705" height="870" alt="Задание 3-2" src="https://github.com/user-attachments/assets/7b4c1c2b-7851-419c-a1c3-ce216c70b39b" />

# Задача 4
Запустите в Yandex Cloud ВМ (вам хватит 2 Гб Ram).
Подключитесь к Вм по ssh и установите docker.
Напишите bash-скрипт, который скачает ваш fork-репозиторий в каталог /opt и запустит проект целиком.
Зайдите на сайт проверки http подключений, например(или аналогичный): https://check-host.net/check-http и запустите проверку вашего сервиса http://<внешний_IP-адрес_вашей_ВМ>:8090. Таким образом трафик будет направлен в ingress-proxy. Трафик должен пройти через цепочки: Пользователь → Internet → Nginx → HAProxy → FastAPI(запись в БД) → HAProxy → Nginx → Internet → Пользователь
(Необязательная часть) Дополнительно настройте remote ssh context к вашему серверу. Отобразите список контекстов и результат удаленного выполнения docker ps -a
Повторите SQL-запрос на сервере и приложите скриншот и ссылку на fork.

# Ответ

<img width="932" height="1010" alt="Задание 4" src="https://github.com/user-attachments/assets/92668511-3e2a-481b-8e53-dd982ef10ef6" />

# Задача 6
Скачайте docker образ hashicorp/terraform:latest и скопируйте бинарный файл /bin/terraform на свою локальную машину, используя dive и docker save. Предоставьте скриншоты действий .
# Ответ
<img width="940" height="336" alt="Задание 6-1" src="https://github.com/user-attachments/assets/04fcea5f-1a6c-427e-8088-2c39a68cd512" />
<img width="933" height="962" alt="задание 6-2" src="https://github.com/user-attachments/assets/81b9261c-cd5d-4648-934d-db92e1b5d44a" />
<img width="926" height="357" alt="задание 6-3" src="https://github.com/user-attachments/assets/790b9e89-327f-44e0-a601-63c933b4e051" />


