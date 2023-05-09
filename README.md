# Работа с Docker и использование баз данных
## Установка Docker была произведена на операционной системе Linux AntiX от Debian
### Docker - это программное обеспечение для автоматизации развёртывания и управления приложениями в средах с поддержкой контейнеризации, контейнеризатор приложений. Позволяет «упаковать» приложение со всем его окружением и зависимостями в контейнер, который может быть развёрнут на любой Linux-системе с поддержкой контрольных групп в ядре, а также предоставляет набор команд для управления этими контейнерами.
### ВНИМАНИЕ! Прошу подробно ознакомиться с этой статьей: https://docs.docker.com/engine/install/debian/ Также там есть множество полезных материалов, которые очень помогают.
### Сразу оговорюсь. Вести рассказы о том, как устанавливать Linux, MAC или какую-либо другую операционную систему не буду! Вся информация есть в интернете, YouTube в помощь.

## Установка Docker
Самая сложная часть работы - это установка Docker (такое уж мое суровое субъективное мнение)
Итак читатель, я буду звать тебя Джонни, для начала необходимо открыть терминал в линукс.
После этого сильно сложного действия нам необходимо обновить пакеты. Используй следующую команду:

sudo apt update

Результат работы команды представлен на скриншоте:

![Screenshot_1](https://user-images.githubusercontent.com/95550202/236998657-6769c030-cd01-439e-9d6d-81485fa7560e.png)

Удали старые версии командой:

sudo apt-get remove docker docker-engine docker.io containerd runc

Результат выполнения команды:

![Screenshot_2](https://user-images.githubusercontent.com/95550202/236999520-998f74a9-ceae-4fe4-b876-39e7da9d2ebc.png)


Для чего это нужно? Отвечу лаконично - чтобы не возникло проблем! Если Джонни не устраивает такой ответ, он может почитать статьи и докопаться до интернета)

Теперь нужно разрешить использование репозитория по протоколу HTTPS. Используем:

sudo apt-get install ca-certificates curl gnupg

Результат выполнения команды:

![Screenshot_3](https://user-images.githubusercontent.com/95550202/237000177-5390f96f-098b-43a0-a527-0dad0a80ffb1.png)

Добавь официальный GPG-ключ Docker:

sudo install -m 0755 -d /etc/apt/keyrings

curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

sudo chmod a+r /etc/apt/keyrings/docker.gpg

Результат ввода команд:

![Screenshot_4](https://user-images.githubusercontent.com/95550202/237000751-1d35a129-a832-43a3-bc76-64dd9a624610.png)

Теперь настрой репозиторий командой:

echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/debian \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
  
Результат:

![Screenshot_5](https://user-images.githubusercontent.com/95550202/237001179-52385971-50c8-4cba-bc24-385cb20857a9.png)

И вот ты дошел до установки самого движка!

Снова обнови свои пакеты уже известной командой:

sudo apt-get update

Результат выполнения команды:

![Screenshot_6](https://user-images.githubusercontent.com/95550202/237001501-67cd9592-7e74-4642-82b9-21854d48563a.png)

Установи Docker Engine, containerd и Docker Compose командой:

sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

Результат выполнения команды:

![Screenshot_7](https://user-images.githubusercontent.com/95550202/237001795-91b907d9-58f9-41c1-b72f-7e8fab5f7506.png)

Убедись, что установка Docker Engine прошла успешно, запустив hello-world изображение:

sudo docker run hello-world

Результат выполнения команды:

![Screenshot_8](https://user-images.githubusercontent.com/95550202/237002005-06b307f8-d751-4343-a053-d3b525afa6d0.png)

Дальше ты должен выпустить этого демона (ну точнее запустить) командой:

sudo dockerd

Результат выполнения команды:

![Screenshot_9](https://user-images.githubusercontent.com/95550202/237002789-6850964d-d75f-411e-80de-f0fa19a28406.png)

Можно глянуть какие статусы способен принимать Docker командой:

sudo service docker status

Результат выполнения команды:

![Screenshot_10](https://user-images.githubusercontent.com/95550202/237003180-7c89288c-7806-4392-a36b-1b8bb49a8991.png)

Запусти Docker следующей командой:

docker start

Результат выполнения команды:

![Screenshot_11](https://user-images.githubusercontent.com/95550202/237003366-42981505-42b5-40a0-9652-e053c6293e11.png)

## Работа с MySQL
### MySQL - это свободная реляционная система управления базами данных.

Теперь необходимо скачать image mySQL сервера командой, представленной на скриншоте:

![Screenshot_24](https://user-images.githubusercontent.com/95550202/237004065-527c4396-b760-45a4-879b-1627ec4240aa.png)

Запускаем сервер:

![Screenshot_12](https://user-images.githubusercontent.com/95550202/237004398-d78c42d1-551f-4ee8-8632-013301dc9f63.png)

Где задаем имя: skilbox-mysql и пароль: pass

Просматриваем запущенный контейнер командой:

docker ps

Результат выполнения:

![Screenshot_13](https://user-images.githubusercontent.com/95550202/237004744-5a9bb531-051f-4a99-8795-1eed225350f1.png)

Используем следующую команду для подключения БД внутри контейнера:

![Screenshot_16](https://user-images.githubusercontent.com/95550202/237004973-b85c8c29-f6e8-485f-af47-c654610ac83e.png)

Где интерактивно указываем пользователя, пароль и путь файла.

Сохраняем файлы с созданными БД и их заполнением (выложены здесь как файлы schema.sql и data.sql):

![Screenshot_15](https://user-images.githubusercontent.com/95550202/237005388-490fe818-ac7d-4aed-9fec-056ee4a47c4e.png)

После выполнения предыдущей команды произошло подключение БД и теперь можно просмотреть базы данных командой:

show databases;

Просмотр баз данных:

![Screenshot_17](https://user-images.githubusercontent.com/95550202/237005811-5b61acbc-daf2-451a-81c1-bb3214f6484e.png)

Отмечу, что все команды, которые отправляются на сервер должны заканиваться точкой с запятой.
Затем сервер возвращает ответ, который показан на рисунке.

Перейдем к рандомной базе данных:

![Screenshot_18](https://user-images.githubusercontent.com/95550202/237006514-ff32d7c6-e5e8-49f9-8e59-1d14a2a3e8b5.png)

Просмотрим ее таблицы с помощью команды представленной на рисунке:

![Screenshot_19](https://user-images.githubusercontent.com/95550202/237006596-8191e089-b2b7-452c-b73e-41aff643261d.png)

Просмотр системных таблиц, которые описывают хранение созданных данных:

![Screenshot_20](https://user-images.githubusercontent.com/95550202/237006902-58d0dd08-1e89-4b72-a4aa-05dbd5cc33e2.png)

Выйти из СУБД можно с помощью следующей команды или нажав клавиши Ctrl + D:

![Screenshot_21](https://user-images.githubusercontent.com/95550202/237007093-92529a86-1a0c-4295-8b15-1aa7a9c5f841.png)

Укажем пути импортированных файлов:

![Screenshot_22](https://user-images.githubusercontent.com/95550202/237007321-b1896718-b0f1-43b2-9795-3a3acdcd110c.png)

Теперь снова запускаем сервер:

![Screenshot_23](https://user-images.githubusercontent.com/95550202/237007461-2fb07a56-a3b2-425f-ac32-6737734578b8.png)

## Задание 1
В этом задании и далее используется БД `skillboxdb`, созданная на уроках модуля.

Опишите структуру таблицы discussion_group:

1. Какие в таблице есть колонки и каких типов?
2. Какие колонки могут принимать значение null?
3. Какие ограничения на размер значений есть для различных колонок?
Укажите запросы, которые использовали для выполнения этого задания.

1) Таблица discussion_group состоит из 6 атрибутов (столбцов): Field, Type, Null, Key, Default, Extra и 7 кортежей (строк): group_id, creation_time, name, description, group_tags, admin_user_id, approve_required.

![Screenshot_29](https://user-images.githubusercontent.com/95550202/237016900-ecdbef31-135f-47f9-b163-4095dce65036.png)

![Screenshot_31](https://user-images.githubusercontent.com/95550202/237043751-13bbad96-7793-4884-bc1d-2e8ed2050d70.png)

INT UNSIGNED - хранит любое число в диапазоне от 0 до 4294967295.

TIMESTAMP — тип данных для хранения даты и времени. Данные хранятся в виде количества секунд, прошедших с начала «эпохи Юникса». Диапазон значений: 1970-01-01 00:00:00 — 2038-12-31 00:00:00. Занимает 4 байта.

VARCHAR в MySQL хранит строку переменной длины (от 0 до 216-1 символов), которая также задается на этапе создания таблицы.

TEXT предназначен также для хранения больших данных, но текстового содержания.

JSON - объектная нотация JavaScript.

TINYINT - представляет целые числа от -128 до 127, занимает 1 байт.

2) Значение NULL может принимать только одна колонка description:

![Screenshot_30](https://user-images.githubusercontent.com/95550202/237043483-5f5829b0-0d5a-4ee3-943a-b67818a95bdd.png)

3) Ограничение на размер значений зависит от типа значений. Описание ограничений приведено выше.

4) Запросы, которые были использованы при выполнении задания:

Просмотр существующих баз данных:

![Screenshot_32](https://user-images.githubusercontent.com/95550202/237047428-3d3224eb-cc21-44d8-8fde-cc8f38920eb5.png)

Использование искомой бд:

![Screenshot_33](https://user-images.githubusercontent.com/95550202/237047464-394713b3-a3b9-4a0b-a02f-079ccbb475f8.png)

Просмотр существующих в бд таблиц:

![Screenshot_34](https://user-images.githubusercontent.com/95550202/237047495-32ccfc80-e87b-4d96-8a3e-1cc1341b4220.png)

Просмотр существующей таблицы:

![Screenshot_35](https://user-images.githubusercontent.com/95550202/237047523-d7828f6c-4058-4123-a22a-396c1319b87e.png)

## Задание 2
Из таблицы пользователей выберите логин пользователя и тип регистрации, переименуйте колонки следующим образом: `user_login`, `sign_on_with`. Ответ предоставьте в виде выполняемого запроса к СУБД MySQL.

Выполним следующий запрос, который производит выборку по колонкам user_id и registration_type, изменяя их название на указанные из таблицы user:

SELECT user_id AS user_login, registration_type AS sign_on_with FROM user;

Результат выполнения запроса представлен на рисунке:

![Screenshot_36](https://user-images.githubusercontent.com/95550202/237051705-db72f923-9dbf-4089-b9d7-9864278ad97d.png)

## Задание 3
Выберите все дискуссионные группы, в которых требуется подтверждение (аппрув). Ответ предоставьте в виде выполняемого запроса к СУБД MySQL.










  





