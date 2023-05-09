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


  





