# ToDo App & MySQL Deployment Instructions

Цей репозиторій містить інструкції щодо розгортання Docker-контейнерів для бази даних MySQL та Django-додатка.

---

## 1. Docker Hub Repository
Ви можете знайти готові образи тут:
* **App Image:** [exodus7707/todoapp:2.0.0](https://hub.docker.com/repository/docker/exodus7707/todoapp/general)
* **MySQL Image:** [exodus7707/mysql-local:1.0.0](https://hub.docker.com/repository/docker/exodus7707/mysql-local/general)

---

## 2. Запуск MySQL з Volume
Спочатку запустіть базу даних. Використання Volume дозволяє зберігати дані навіть після видалення контейнера.

```bash
docker run -d --name mysql-server -v mysql_data:/var/lib/mysql exodus7707/mysql-local:1.0.0
```

## 3. Запуск контейнера з додатком (App)

### 3.1 Дізнайтеся IP-адресу контейнера бази даних. 
У виводі цієї команди вам доведеться очима знайти розділ "Containers" і там побачити ваш mysql-server та його IP.:
замініть <MYSQL_IP> на отриману адресу в todolist/settings.py: 'HOST'

```bash
docker network inspect bridge
```

### 3.2 Запустіть додаток: 

```bash
docker run -d -p 8080:8080 --name app exodus/todoapp:2.0.0
```

## Доступ до додатка через браузер

URL: http://localhost:8080