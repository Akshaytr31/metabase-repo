# metabase-repo
metabase deployment in docker compose

    • root@ubuntu:~# cd metabase-compose/

    • root@ubuntu:~/metabase-compose# ls
      Dockerfile-mysql  Dockerfile-postgres  LICENSE  README.md  docker-compose.yml  public
    • root@ubuntu:~/metabase-compose# la -a
      .  ..  .env.example  .git  .github  .gitignore  Dockerfile-mysql  Dockerfile-postgres  LICENSE  README.md docker-compose.yml  public


    • root@ubuntu:~/metabase-compose# cp .env.example .env

    • root@ubuntu:~/metabase-compose# vi .env
    
    • root@ubuntu:~/metabase-compose# vi docker-compose.yml
    • root@ubuntu:~/metabase-compose# cat docker-compose.yml 
      
      version: '3.3'
      
      services:
        db:
          build:
            context: .
            dockerfile: 'Dockerfile-${DB_TYPE}'
            args:
              db_name: ${DB_NAME}
              db_user: ${DB_USER}
              db_password: ${DB_PASSWORD}
              db_port: ${DB_PORT}
          restart: always
          volumes:
            - type: volume
              source: ${DB_OUTSIDE_VOLUME}
              target: ${DB_INSIDE_VOLUME}
      
        adminer:
          image: adminer
          restart: always
          ports:
            - '${ADMINER_PORT}:8080'
          depends_on:
            - 'db'
      
        metabase:
          image: metabase/metabase
          restart: always
          environment:
            MB_DB_FILE: '${MB_DB_FILE}'
            MB_DB_TYPE: '${DB_TYPE}'
            MB_DB_DBNAME: '${DB_NAME}'
            MB_DB_PORT: '${DB_PORT}'
            MB_DB_USER: '${DB_USER}'
            MB_DB_HOST: 'db'
            MB_DB_PASS: '${DB_PASSWORD}'
            JAVA_TIMEZONE: '${MB_JAVA_TIMEZONE}'
          ports:
            # <Port exposed>:<Port running inside container>
            - '${MB_PORT}:3000'
          volumes:
            # Volumes where Metabase data will be persisted
            - 'mb-data:/metabase-data'
          depends_on:
            - 'db'
      
      volumes:
        db-data:
        mb-data:


    • root@ubuntu:~/metabase-compose# docker-compose build
    • root@ubuntu:~/metabase-compose# docker-compose up
    • go to a new tab 
         http://0.0.0.0:3000/setup/
    
