# Development environment

## Estructura de directorios

* Crea los siguientes directorios

```bash
  $ mkdir local_deploy/ backend/ frontend/
  $ ls -1
  backend/
  local_deploy
  frontend/
```

* Obtenemos una copia del código backend

```bash
  $ cd backend
  $ git init
  $ git remote add origin https://github.com/test-tech-for-companies/sis_CRUD_with_django.git
  $ git pull origin main
  $ git branch -M main
```

* Obtenemos una copia del código frontend

```bash
  $ cd backend
  $ git init
  $ git remote add origin https://github.com/test-tech-for-companies/sis_auth_angular.git
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
  |    ├── Dockerfile_django
  |    ├── Dockerfile_mysql
  |    ├── LICENSE
  |    ├── README.md
  |    ├── createdb.sh
  |    └── docker-compose.yml
  └── frontend
      ├── README.md
      ├── angular.json
      ├── images
      │   ├── Captura1.JPG
      │   ├── Captura2.JPG
      │   ├── Captura3.JPG
      │   ├── Captura4.JPG
      │   ├── Captura5.JPG
      │   ├── Captura6.JPG
      │   ├── Captura7.JPG
      │   └── Captura8.JPG
      ├── karma.conf.js
      ├── node_modules
      ├── package-lock.json
      ├── package.json
      ├── src
      │   ├── app
      │   │   ├── app-routing.module.ts
      │   │   ├── app.component.css
      │   │   ├── app.component.html
      │   │   ├── app.component.spec.ts
      │   │   ├── app.component.ts
      │   │   ├── app.module.ts
      │   │   ├── auth.guard.spec.ts
      │   │   ├── auth.guard.ts
      │   │   ├── components
      │   │   │   ├── home-user
      │   │   │   │   ├── home-user.component.css
      │   │   │   │   ├── home-user.component.html
      │   │   │   │   ├── home-user.component.spec.ts
      │   │   │   │   └── home-user.component.ts
      │   │   │   ├── principal
      │   │   │   │   ├── principal.component.css
      │   │   │   │   ├── principal.component.html
      │   │   │   │   ├── principal.component.spec.ts
      │   │   │   │   └── principal.component.ts
      │   │   │   ├── signin
      │   │   │   │   ├── signin.component.css
      │   │   │   │   ├── signin.component.html
      │   │   │   │   ├── signin.component.spec.ts
      │   │   │   │   └── signin.component.ts
      │   │   │   └── signup
      │   │   │       ├── signup.component.css
      │   │   │       ├── signup.component.html
      │   │   │       ├── signup.component.spec.ts
      │   │   │       └── signup.component.ts
      │   │   └── services
      │   │       ├── auth.service.spec.ts
      │   │       ├── auth.service.ts
      │   │       ├── data.service.spec.ts
      │   │       ├── data.service.ts
      │   │       ├── token-interceptor.service.spec.ts
      │   │       └── token-interceptor.service.ts
      │   ├── assets
      │   ├── environments
      │   │   ├── environment.prod.ts
      │   │   └── environment.ts
      │   ├── favicon.ico
      │   ├── index.html
      │   ├── main.ts
      │   ├── polyfills.ts
      │   ├── styles.css
      │   └── test.ts
      ├── tsconfig.app.json
      ├── tsconfig.json
      └── tsconfig.spec.json

```

## Run

* Hacemos un build 

```bash
$ docker-compose build
```

* Iniciamos la applicación

```bash
$ docker-compose up -d backend
```

* Generamos las migraciones (nuestro primer contacto con la base de datos)

```bash
$ docker-compose exec backend python3 manage.py makemigrations
$ docker-compose exec backend python3 manage.py migrate
```

* Reiniciamos un nuevo contenedor que tomará los cambios nuevos

```bash
$ docker-compose down
$ docker-compose up -d backend
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

## Run frontend

* Es posible que nuestro contenedor de angular se demore un poco
```
$ docker-compose up -d angularfrontend
Creating angular ... done
[ hi ~/web_application/local_deploy ]

$ docker-compose logs angularfrontend
Attaching to angular
angular            | yarn run v1.22.15
angular            | $ ng serve --port 4000 --host 0.0.0.0
angular            | Warning: This is a simple server for use in testing or debugging Angular applications
. . .
angular            | ✔ Compiled successfully.
```

* El servidor de angular si debe retornarnos como código de respuesta OK.

```bash
  curl --write-out "%{http_code}\n" --silent --output /dev/null http://127.0.0.1:400
  200
```


* Revisa que todos servicios docker corriendo

```bash
$ docker-compose ps -a
    Name                  Command               State                          Ports
-----------------------------------------------------------------------------------------------------------
angular        docker-entrypoint.sh yarn  ...   Up      0.0.0.0:4000->4000/tcp,:::4000->4000/tcp
backend_auth   python manage.py runserver ...   Up      0.0.0.0:8000->8000/tcp,:::8000->8000/tcp
mysql          docker-entrypoint.sh mysqld      Up      0.0.0.0:3306->3306/tcp,:::3306->3306/tcp, 33060/tcp
```