# Development environment

## Estructura de directorios

* Crea los siguientes directorios

```bash
  $ mkdir local_deploy/ backend/
  $ ls -1
  backend
  local_deploy
```

* Obtenemos una copia del código

```bash
  $ cd backend
  $ git init
  $ git remote add origin https://github.com/test-tech-for-companies/sis_CRUD_with_django.git
  $ git pull origin main
  $ git branch -M main
```


* El contenido de cada directorio debe quedar de la siguiente manera
```bash
  $ tree .
  .
  ├── backend
  │   ├── LICENSE
  │   ├── README.md
  │   ├── applications
  │   │   ├── __init__.py
  │   │   ├── authen
  │   │   │   ├── __init__.py
  │   │   │   ├── admin.py
  │   │   │   ├── apps.py
  │   │   │   ├── migrations
  │   │   │   │   ├── __init__.py
  │   │   │   ├── serializers
  │   │   │   │   ├── __init__.py
  │   │   │   │   └── authTokenSerializer.py
  │   │   │   ├── urls.py
  │   │   │   └── views
  │   │   │       ├── __init__.py
  │   │   │       ├── loginView.py
  │   │   │       └── signupView.py
  │   │   └── users
  │   │       ├── __init__.py
  │   │       ├── admin.py
  │   │       ├── apps.py
  │   │       ├── migrations
  │   │       │   ├── 0001_initial.py
  │   │       │   ├── __init__.py
  │   │       ├── models
  │   │       │   ├── __init__.py
  │   │       │   └── user.py
  │   │       ├── serializers
  │   │       │   ├── __init__.py
  │   │       │   └── userSerializer.py
  │   │       ├── urls.py
  │   │       └── views
  │   │           ├── __init__.py
  │   │           ├── userCreateView.py
  │   │           ├── userDetailView.py
  │   │           └── verifyTokenView.py
  │   ├── manage.py
  │   ├── requirements.txt
  │   └── user_auth
  │       ├── __init__.py
  │       ├── asgi.py
  │       ├── config
  │       │   ├── __init__.py
  │       │   ├── base.py
  │       │   ├── local.py
  │       │   └── prod.py
  │       ├── urls.py
  │       └── wsgi.py
  └── local_deploy
      ├── Dockerfile_django
      ├── Dockerfile_mysql
      ├── LICENSE
      ├── README.md
      ├── createdb.sh
      └── docker-compose.yml
```

## Run

* Hacemos un build 

```bash
$ docker-compose build
```

* Iniciamos la applicación

```bash
$ docker-compose up -d
```

* Generamos las migraciones (nuestro primer contacto con la base de datos)

```bash
$ docker-compose exec backend python3 manage.py makemigrations
$ docker-compose exec backend python3 manage.py migrate
```

* Reiniciamos un nuevo contenedor que tomará los cambios nuevos

```bash
$ docker-compose down
$ docker-compose up -d
```

* Vamos a ver si funciona

```bash
  curl --write-out "%{http_code}\n" --silent --output /dev/null http://127.0.0.1:8000
```

* Como estamos en etapa de desarrollo te debería retornar codigo de estado 404, es la página de debugging que tiene activa la aplicación.1


## Checking database

* Tambien tendremos la opción de ejecutar queries sql para verificar que todo anda bien

  Podrian seguir el siguiente formato

  * -ujack: es nuestro usuario que administra la base de datos
  * -pjack: es la contraseña

  ```bash
    $ docker-compose exec auth_db mysql -ujack -pjack -e "USE auth_ms;SELECT * FROM authtoken_token \G;"
  ```
  
  Output:
  ```
  mysql: [Warning] Using a password on the command line interface can be insecure.
  *************************** 1. row *************************** <br>
      key: 169cbf18e79c24a94b203b358eea5c519d362427<br>
  created: 2022-04-21 17:29:47.777709<br>
  user_id: 1<br>
  ```