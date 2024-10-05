---
Created: 2024-06-07T20:07
Updated: 2024-06-07T20:16
---
ssh root@162.55.175.66

Current setup:

```Plain
root@petstore:~# docker ps
CONTAINER ID   IMAGE                                   COMMAND                  CREATED         STATUS      PORTS
             NAMES
680b20cd40eb   springcommunity/spring-petclinic-rest   "java -cp /app/resou…"   18 months ago   Up 8 days   0.0.0.0:9966->9966/tcp, :::9966->9966/tcp   fervent_shirley

root@petstore:~# docker images
REPOSITORY                              TAG       IMAGE ID       CREATED        SIZE
hello-world                             latest    feb5d9fea6a5   2 years ago    13.3kB
springcommunity/spring-petclinic-rest   latest    607211961f21   54 years ago   185MB
```