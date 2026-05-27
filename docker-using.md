# 1. start and create MySQL container
```
docker compose up -d

up: create and start container
-d: running in the background
```

# 2. check whether container is running
```docker compose ps```

# 3. login MySQL
```
docker exec -it mysql-learning mysql -u student -p

docker exec: execute a command in running container

-i: keep enter channel opening
-t: open terminal(>mysql:)
-u: user
-p: hint to enter 
```