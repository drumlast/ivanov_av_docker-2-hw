# Домашнее задание к занятию "Docker part2" - Иванов Анатолий Васильевич


### Инструкция по выполнению домашнего задания

   1. Сделайте `fork` данного репозитория к себе в Github и переименуйте его по названию или номеру занятия, например, https://github.com/имя-вашего-репозитория/git-hw или  https://github.com/имя-вашего-репозитория/7-1-ansible-hw).
   2. Выполните клонирование данного репозитория к себе на ПК с помощью команды `git clone`.
   3. Выполните домашнее задание и заполните у себя локально этот файл README.md:
      - впишите вверху название занятия и вашу фамилию и имя
      - в каждом задании добавьте решение в требуемом виде (текст/код/скриншоты/ссылка)
      - для корректного добавления скриншотов воспользуйтесь [инструкцией "Как вставить скриншот в шаблон с решением](https://github.com/netology-code/sys-pattern-homework/blob/main/screen-instruction.md)
      - при оформлении используйте возможности языка разметки md (коротко об этом можно посмотреть в [инструкции  по MarkDown](https://github.com/netology-code/sys-pattern-homework/blob/main/md-instruction.md))
   4. После завершения работы над домашним заданием сделайте коммит (`git commit -m "comment"`) и отправьте его на Github (`git push origin`);
   5. Для проверки домашнего задания преподавателем в личном кабинете прикрепите и отправьте ссылку на решение в виде md-файла в вашем Github.
   6. Любые вопросы по выполнению заданий спрашивайте в чате учебной группы и/или в разделе “Вопросы по заданию” в личном кабинете.
   
Желаем успехов в выполнении домашнего задания!
   
### Дополнительные материалы, которые могут быть полезны для выполнения задания

1. [Руководство по оформлению Markdown файлов](https://gist.github.com/Jekins/2bf2d0638163f1294637#Code)

---

### Задание 1

С помощью docker compose можно развернуть сервис, или несколько сервисов из нескольких контейнеров описав все в одном файле compose.yaml и подняв все одной командой docker compose up -d 

---

### Задание 2

services:

volumes:

networks:
   ivanov-av-my-netology-hw:
     driver: bridge
     ipam:
       config:
        - subnet: 10.5.0.0/16
        - gateway: 10.5.0.1

---

### Задание 3


services:
  prometheus:
    image: prom/prometheus:v2.47.2
    container_name: ivanov-av-my-netology-prometheus
    command: --web.enable-lifecycle --config.file=/etc/prometheus/prometheus.yml
    ports:
      - "9090:9090"
    volumes:
      - ./prometheus:/etc/prometheus
      - prometheus-data:/prometheus
    networks:
      - ivanov-av-my-netology-hw
    restart: always

volumes:
   prometheus-data:

networks:
  ivanov-av-my-netology-hw:
     driver: bridge
     ipam:
       config:
        - subnet: 10.5.0.0/16
        - gateway: 10.5.0.1



### Задание 4

services:
  prometheus:
    image: prom/prometheus:v2.47.2
    container_name: ivanov-av-my-netology-prometheus
    command: --web.enable-lifecycle --config.file=/etc/prometheus/prometheus.yml
    ports:
      - "9090:9090"
    volumes:
      - ./prometheus:/etc/prometheus
      - prometheus-data:/prometheus
    networks:
      - ivanov-av-my-netology-hw
    restart: always

  pushgateway:
    image: prom/pushgateway:v1.6.2
    container_name: ivanov-av-my-netology-pushgateway
    ports:
      - 9091:9091
    networks:
      - vanov-av-my-netology-hw
    depends_on:
      - prometheus
    restart: always

volumes:
   prometheus-data:

networks:
  ivanov-av-my-netology-hw:
     driver: bridge
     ipam:
       config:
        - subnet: 10.5.0.0/16
        - gateway: 10.5.0.1