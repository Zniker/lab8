# lab8

#Данная лабораторная работа посвещена изучению систем автоматизации развёртывания и управления приложениями на примере Docker
1) Устанавливаем Docker c помощью
```
sudo apt update
sudo apt install apt-transport-https
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
sudo apt update
sudo apt install docker-ce
sudo systemctl status docker
sudo usermod -aG docker $USER
>>>logout/login<<<
```

2) Dockerfile:
```
FROM ubuntu:18.04
RUN apt update
RUN apt install -yy gcc g++ cmake
COPY . print/
WORKDIR print
RUN cmake -H. -B_build -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=_install
RUN cmake --build _build
RUN cmake --build _build --target install
ENV LOG_PATH /home/logs/log.txt
ENV LOG_PATH /home/logs/log.txt
VOLUME /home/logs
WORKDIR _install/bin
ENTRYPOINT ./demo
```
Docker — это платформа, которая предназначена для разработки, развёртывания и запуска приложений в контейнерах.
Контейнер Docker — это образ Docker, вызванный к жизни. Это — самодостаточная операционная система, в которой имеется только самое необходимое и код приложения.
Образы Docker являются результатом процесса их сборки, а контейнеры Docker — это выполняющиеся образы.
В файлах Dockerfile содержатся инструкции по созданию образа. С них, набранных заглавными буквами, начинаются строки этого файла. После инструкций идут их аргументы. Инструкции, при сборке образа, обрабатываются сверху вниз.
Слои в итоговом образе создают только инструкции FROM, RUN, COPY, и ADD. Другие инструкции что-то настраивают, описывают метаданные, или сообщают Docker о том, что во время выполнения контейнера нужно что-то сделать, например — открыть какой-то порт или выполнить какую-то команду.
 
3)image ghost 
```
docker pull ghost 
docker run -d --name some-ghost ghost
docker run -d --name some-ghost -e url=http://localhost:3001 -p 3001:2368 ghost
![image](https://user-images.githubusercontent.com/46539072/170060715-91099367-2645-42fd-972b-59d2cb1c6499.png)


```
## Основные команды для управления контейнерами

```
run
stop
rm
logs
```
Основные инструкции Dockerfile:
FROM — задаёт базовый (родительский) образ.
LABEL — описывает метаданные. Например — сведения о том, кто создал и поддерживает образ.
ENV — устанавливает постоянные переменные среды.
RUN — выполняет команду и создаёт слой образа. Используется для установки в контейнер пакетов.
COPY — копирует в контейнер файлы и папки.
ADD — копирует файлы и папки в контейнер, может распаковывать локальные .tar-файлы.
CMD — описывает команду с аргументами, которую нужно выполнить когда контейнер будет запущен. Аргументы могут быть переопределены при запуске контейнера. В файле может присутствовать лишь одна инструкция CMD.
WORKDIR — задаёт рабочую директорию для следующей инструкции.
ARG — задаёт переменные для передачи Docker во время сборки образа.
ENTRYPOINT — предоставляет команду с аргументами для вызова во время выполнения контейнера. Аргументы не переопределяются.
EXPOSE — указывает на необходимость открыть порт.
VOLUME — создаёт точку монтирования для работы с постоянным хранилищем.
