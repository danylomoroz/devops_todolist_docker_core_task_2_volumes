# ToDo App & MySQL Deployment Instructions

Цей репозиторій містить інструкції щодо розгортання Docker-контейнерів для бази даних MySQL та Django-додатка.

---

## 1. Docker Hub Repository
Ви можете знайти готові образи тут:
* **App Image:** [exodus7707/todoapp:2.0.0](https://hub.docker.com/repository/docker/exodus7707/todoapp/general)
* **MySQL Image:** [exodus7707/mysql-local:1.0.0](https://hub.docker.com/repository/docker/exodus7707/mysql-local/general)

---

## 2. Step 1: Run MySQL Server with Volume
Start the MySQL container first to obtain its IP address. We use a volume for data persistence.

```bash
docker run -d --name mysql-server -v mysql_data:/var/lib/mysql exodus7707/mysql-local:1.0.0
```

## 3. Step 2: Configure and Build the App

### 3.1 Find the MySQL Container IP
Identify the IP address assigned to the mysql-server container. Look at "Containers" and "mysql-server". Copy ipv4


```bash
docker network inspect bridge
```

### 3.2 Запустіть додаток: 

```bash
docker run -d -p 8080:8080 --name app -e DB_HOST=<use_this_ipv4_from_sql> exodus7707/todoapp:2.0.0
```



## 4. Accessing the Application using your Browser

URL: http://localhost:8080