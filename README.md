# Домашнее задание к занятию "Docker part2" - Иванов Анатолий Васильевич


### Задание 1

С помощью docker compose можно развернуть сервис, или несколько сервисов из нескольких контейнеров описав все в одном файле compose.yaml и подняв все одной командой docker compose up -d 

---

### Задание 2

```yaml
services:

volumes:

networks:
   ivanov-av-my-netology-hw:
     driver: bridge
     ipam:
       config:
        - subnet: 10.5.0.0/16
        - gateway: 10.5.0.1
```

---

### Задание 3

```yaml
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
```

---

### Задание 4

```yaml
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
```

---