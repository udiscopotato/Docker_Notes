Docker Compose is a tool for defining and running multi-container Docker applications. It uses a YAML file to configure your application’s services, and then, with a single command, you can create and start all the services from your configuration.
Using Docker Compose, we can configure containers and the communication between them in a declarative way.
Default name for Docker Compose file is "docker-compose.yaml"
Example:
Source:  https://github.com/dockersamples/example-voting-app
docker-compose.yaml
```javascript
services:
  vote:
    image: dockersamples/examplevotingapp_vote
    depends_on:
      redis:
        condition: service_healthy 
    ports:
      - "5000:80"
    networks:
      - front-tier
      - back-tier

  result:
    image: dockersamples/examplevotingapp_result
    depends_on:
      db:
        condition: service_healthy 
    ports:
      - "5001:80"
    networks:
      - front-tier
      - back-tier

  worker:
    image: dockersamples/examplevotingapp_worker
    depends_on:
      redis:
        condition: service_healthy 
      db:
        condition: service_healthy 
    networks:
      - back-tier

  redis:
    image: redis:alpine
    volumes:
      - "./healthchecks:/healthchecks"
    healthcheck:
      test: /healthchecks/redis.sh
      interval: "5s"
    networks:
      - back-tier

  db:
    image: postgres:15-alpine
    environment:
      POSTGRES_USER: "postgres"
      POSTGRES_PASSWORD: "postgres"
    volumes:
      - "db-data:/var/lib/postgresql/data"
      - "./healthchecks:/healthchecks"
    healthcheck:
      test: /healthchecks/postgres.sh
      interval: "5s"
    networks:
      - back-tier

volumes:
  db-data:

networks:
  front-tier:
  back-tier:
```

## Commands
- docker-compose up 
- docker-compose up -d
- docker-compose ps
- docker-compose logs
- docker-compose stop
- docker-compose down
- docker-compose top