# Containers
Урок 5. Docker Compose и Docker Swarm
Скрыть
Задание 1:
1) создать сервис, состоящий из 2 различных контейнеров: 1 - веб, 2 - БД
2) далее необходимо создать 3 сервиса в каждом окружении (dev, prod, lab)
3) по итогу на каждой ноде должно быть по 2 работающих контейнера
4) выводы зафиксировать

![containerization](https://github.com/Amant-987/Containers/blob/main/Screenshots_task1/Screenshot_1.png)
![containerization](https://github.com/Amant-987/Containers/blob/main/Screenshots_task1/Screenshot_2.png)
![containerization](https://github.com/Amant-987/Containers/blob/main/Screenshots_task1/Screenshot_3.png)
![containerization](https://github.com/Amant-987/Containers/blob/main/Screenshots_task1/Screenshot_4.png)
![containerization](https://github.com/Amant-987/Containers/blob/main/Screenshots_task1/Screenshot_5.png)
![containerization](https://github.com/Amant-987/Containers/blob/main/Screenshots_task1/Screenshot_6.png)
![containerization](https://github.com/Amant-987/Containers/blob/main/Screenshots_task1/Screenshot_7.png)
![containerization](https://github.com/Amant-987/Containers/blob/main/Screenshots_task1/Screenshot_8.png)
![containerization](https://github.com/Amant-987/Containers/blob/main/Screenshots_task1/Screenshot_9.png)
![containerization](https://github.com/Amant-987/Containers/blob/main/Screenshots_task1/Screenshot_10.png)
![containerization](https://github.com/Amant-987/Containers/blob/main/Screenshots_task1/Screenshot_11.png)
![containerization](https://github.com/Amant-987/Containers/blob/main/Screenshots_task1/Screenshot_12.png)
![containerization](https://github.com/Amant-987/Containers/blob/main/Screenshots_task1/Screenshot_13.png)
![containerization](https://github.com/Amant-987/Containers/blob/main/Screenshots_task1/Screenshot_14.png)
![containerization](https://github.com/Amant-987/Containers/blob/main/Screenshots_task1/Screenshot_15.png)
![containerization](https://github.com/Amant-987/Containers/blob/main/Screenshots_task1/Screenshot_16.png)
![containerization](https://github.com/Amant-987/Containers/blob/main/Screenshots_task1/Screenshot_17.png)
![containerization](https://github.com/Amant-987/Containers/blob/main/Screenshots_task1/Screenshot_18.png)



Задание 2*:
1) нужно создать 2 ДК-файла, в которых будут описываться сервисы
2) повторить задание 1 для двух окружений: lab, dev
3) обязательно проверить и зафиксировать результаты, чтобы можно было выслать преподавателю для проверки

Process:
-- Аналогично предыдущему заданию создадим два файла:  lab_dk.yml и dev_dk.yml с одинаковым содержимым:
version: '3.9'
services:
  web:
    image: adminer:4.8.1
    restart: always
    ports:
      - 6080:8080
  db:
    image: mariadb:10.10.2
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: 123456
-- За web составляющую будет отвечать adminer версии 4.8.1, а за базу данных mariadb версии 10.10.2
-- Для запуска сервисов в окружении "lab" выполним команду:
root@server-for-task:/home/n/Docker# docker-compose -f lab_dk.yml up -d
[+] Running 17/17
 ✔ web 7 layers [⣿⣿⣿⣿⣿⣿⣿]      0B/0B      Pulled                          32.9s 
   ✔ 918547b94326 Pull complete                                           23.0s 
   ✔ 6bf072a3c195 Pull complete                                           28.5s 
   ✔ 3683a3b1017a Pull complete                                           28.8s 
   ✔ 51a450f50bf3 Pull complete                                           29.0s 
   ✔ c9988d325d7e Pull complete                                           29.1s 
   ✔ d88de51838f2 Pull complete                                           29.4s 
   ✔ ccbdbbaee470 Pull complete                                           29.5s 
 ✔ db 8 layers [⣿⣿⣿⣿⣿⣿⣿⣿]      0B/0B      Pulled                          35.7s 
   ✔ 10ac4908093d Pull complete                                           22.0s 
   ✔ 44449101e748 Pull complete                                           22.2s 
   ✔ a721db3e3f3d Pull complete                                           24.2s 
   ✔ 1850a930b84a Pull complete                                           24.7s 
   ✔ 397a938c7da3 Pull complete                                           25.3s 
   ✔ 826be17e856d Pull complete                                           32.1s 
   ✔ 644de6c90876 Pull complete                                           32.1s 
   ✔ cd00814cfb1a Pull complete                                           32.2s 
[+] Running 3/3
 ✔ Network docker_default  Created                                         0.2s 
 ✔ Container docker-web-1  Started                                         2.4s 
 ✔ Container docker-db-1   Started                                         2.4s 
 
 -- Для запуска сервисов в окружении "dev" выполним команду:
root@server-for-task:/home/n/Docker# docker-compose -f dev_dk.yml up -d
[+] Running 2/0
 ✔ Container docker-db-1   Running                                         0.0s 
 ✔ Container docker-web-1  Running                                         0.0s 

-- Далее можно очистить все, что мы сделали, за ненадобностью
docker stop $(docker ps -qa) && docker rm $(docker ps -qa) && docker rmi -f $(docker images -qa) && docker volume rm $(docker volume ls -q) && docker network rm $(docker network ls -q)



__________________________________________________________________________________________________________
Задание со звездочкой - повышенной сложности, это нужно учесть при выполнении (но сделать его необходимо).

Формат сдачи ДЗ: предоставить доказательства выполнения задания посредством ссылки на google-документ с правами на комментирование/редактирование.
Результатом работы будет: текст объяснения, логи выполнения, история команд и скриншоты (важно придерживаться такой последовательности).
В названии работы должны быть указаны ФИ, номер группы и номер урока.

Критерии оценивания ПА “Контейнеризация”:
1) Выслан подробный отчет по выполнению 5-го ДЗ (см.: результаты работы)
2) Выполнено / частично выполнено / сделана попытка выполнения задания 2* в 5-м ДЗ.
3) Добавлена история выполнения команд в 5-м ДЗ. Идеально, если выслан весь процесс попыток выполнения, учитывая ошибочные.
3
