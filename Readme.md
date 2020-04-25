# MySQL Sample Database Container Images

I have included TWO sample databases:

1. employees (HR Database) refer to [docker-compose](./employees/docker-compose.yaml) 
2. sakila (Sakila Movies Database) refer to [docker-compose](/sakila/docker-compose.yaml)

Feel free to modify my `Dockerfile` or `docker-compose` file to make your custom mysql database with sample database.

### For Lazy people (skip building images)

You can download and use pre-built images from [docker hub](https://hub.docker.com/repository/docker/mahendrshinde/mysql-sample).

The sample `docker-compose` to create instance of sample database:

1. sakila-db

```yaml
version: "3.5"

networks: 
    net1:
        ipam: 
            driver: default
            config: 
            - subnet: 182.18.0.0/24

services: 
    sakila-db:
        image: mahendrshinde/mysql-sample:sakila
        environment:
        ## Feel free to change following values
        - MYSQL_DATABASE: sakila
        - MYSQL_USER: mahendra
        - MYSQL_PASSWORD: pass@1234        
        - MYSQL_ROOT_PASSWORD: roPass@1234
        networks: 
            net1:
                ipv4_address: 182.18.0.5

```

> You can connect your mysql instance now on 182.18.0.5:3306/sakila

2. employees-db 

```yaml
version: "3.5"

networks: 
    net1:
        ipam: 
            driver: default
            config: 
            - subnet: 182.19.0.0/24

services: 
    hr-db:
        image: mahendrshinde/mysql-sample:employees
        environment:
        ## Feel free to change following values
        - MYSQL_DATABASE: hr
        - MYSQL_USER: mahendra
        - MYSQL_PASSWORD: pass@1234        
        - MYSQL_ROOT_PASSWORD: roPass@1234

        networks: 
            net1:
                ipv4_address: 182.19.0.5

```

> You can connect your mysql instance now on 182.19.0.5:3306/hr
