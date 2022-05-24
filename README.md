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
```
![image](https://user-images.githubusercontent.com/46539072/170060715-91099367-2645-42fd-972b-59d2cb1c6499.png)
# сигнатура
```
docker run [OPTIONS] IMAGE[:TAG|@DIGEST] [COMMAND] [ARG...]
# основные настройки (флаги)
-d - запуск контейнера в качестве отдельного процесса
-p - публикация открытого порта в интерфейсе хоста (HOST:CONTAINER)
# например
-p 3000:3000
--name - название контейнера
--rm - очистка системы при остановке/удалении контейнера
--restart - политика перезапуска - no (default) | on-failure[:max-retries] | always | unless-stopped
-e - установка переменной среды окружения
```
docker ps 
```
# основные флаги
-a - показать все контейнеры (как запущенные, так и остановленные)
-f - фильтрация вывода на основе условия (`id`, `name`, `status` и т.д.)
-n - показать n последних созданных контейнеров
-l - показать последний созданный контейнер
```
## Основные команды для управления контейнерами

```
run
stop
rm
logs
```
