### Run Rabbitmq with Docker

docker-compose.yml
```yml
version: "3.2"
services:
  rabbitmq:
    image: rabbitmq:3-management-alpine
    container_name: 'rabbitmq'
    ports:
        - 5672:5672
        - 15672:15672
    volumes:
        - ~/.docker-conf/rabbitmq/data/:/var/lib/rabbitmq/
        - ~/.docker-conf/rabbitmq/log/:/var/log/rabbitmq
    networks:
        - rabbitmq_go_net

networks:
  rabbitmq_go_net:
    driver: bridge
```

```docker-compose up -d```

Check connection:
```
http://localhost:15672/#/connections
Default credential: guest/guest
```

Reference: https://github.com/prakash-babajyoti/springbootrabbitmq
