# holbertonschool-softy-pinko-docker

A Docker project that builds an infrastructure made of a reverse proxy, a load balancer, two API servers and one front-end static server, all orchestrated with Docker Compose.

## Architecture

Client -> Nginx proxy (port 80) -> front-end (Nginx, port 9000) and back-end (Flask, port 5252, round robin).

## Requirements

- Docker Desktop
- Docker Compose

## Tasks

| Task | Description | Run |
|------|-------------|-----|
| task0 | First Docker image based on the latest Ubuntu that prints "Hello, World!" | `docker build -f ./Dockerfile -t softy-pinko:task0 .` then `docker run -it --rm softy-pinko:task0` |
| task1 | Back-end: Flask API on port 5252 with the `/api/hello` endpoint | `docker run -p 5252:5252 -it --rm softy-pinko:task1` |
| task2 | Front-end: Nginx serving the Softy Pinko static site on port 9000 | `docker run -p 9000:9000 -it --rm softy-pinko-front-end:task2` |
| task3 | Front-end calls the back-end (CORS enabled with flask-cors) | Run both containers in two terminals |
| task4 | Docker Compose runs the front-end and back-end together | `docker-compose up` |
| task5 | Nginx proxy on port 80 routing `/` to the front-end and `/api` to the back-end | `docker-compose up`, then open http://localhost |
| task6 | Horizontal scaling: two API servers with round-robin load balancing | `docker-compose up --scale back-end=2` |

## Notes

- In task5 and task6 the front-end and back-end are not exposed on the host. Everything goes through the proxy on port 80.
- In task6 reload http://localhost several times and watch the logs alternate between `back-end-1` and `back-end-2`.

## Author

Sarah Alkhubaizy
