# API de Lista de Tareas (ToDo) - README

Este proyecto es una API RESTful para administrar una lista de tareas (ToDo). Permite a los usuarios realizar operaciones CRUD (Crear, Leer, Actualizar, Eliminar) en sus tareas, así como autenticarse y autorizarse mediante tokens de autenticación.

## Tecnologías Utilizadas

- Django: Framework web de Python utilizado para construir la API.
- Django REST Framework (DRF): Biblioteca de Django para crear APIs web.
- Django REST Framework Token Authentication: Método de autenticación basado en tokens para la API.
- SQLite: Motor de base de datos utilizado para almacenar los datos de la aplicación.

## Estructura del Proyecto

El proyecto está estructurado de la siguiente manera:

- `backend/`: Directorio principal del proyecto Django.
  - `api/`: Aplicación Django que contiene las vistas, modelos, serializers y URLs de la API.
    - `models.py`: Definición de los modelos de datos para las tareas (ToDo).
    - `serializers.py`: Serializadores para convertir los modelos en formatos JSON.
    - `views.py`: Definición de las vistas de la API para realizar operaciones CRUD.
    - `urls.py`: Configuración de las URLs de la API.
  - `backend/`: Configuración del proyecto Django.
    - `settings.py`: Configuración del proyecto, incluyendo la configuración de la autenticación.
  - `manage.py`: Script de gestión de Django para realizar diversas tareas.
  
## Configuración

1. Clona este repositorio en tu máquina local.
2. Instala las dependencias del proyecto utilizando `pip install -r requirements.txt`.
3. Ejecuta las migraciones de la base de datos utilizando `python manage.py migrate`.
4. Crea un superusuario para acceder al panel de administración de Django usando `python manage.py createsuperuser`.
5. Inicia el servidor de desarrollo con `python manage.py runserver`.

## Uso

1. Accede al panel de administración de Django en `http://127.0.0.1:8000/admin/` para crear usuarios y tareas.
2. Utiliza las rutas de la API para realizar operaciones CRUD en las tareas:
   - `/api/todos/`: Lista todas las tareas o crea una nueva tarea.
   - `/api/todos/<id>/`: Obtiene, actualiza o elimina una tarea específica.
   - `/api/todos/<id>/complete/`: Marca una tarea como completada.
   - `/api/signup/`: Registra un nuevo usuario.
   - `/api/login/`: Inicia sesión con un usuario registrado y obtiene un token de autenticación.

## Ejemplo de Uso

```bash
# Registra un nuevo usuario
curl -X POST http://127.0.0.1:8000/api/signup/ -d "username=user1&password=user1"

# Inicia sesión y obtiene un token de autenticación
curl -X POST http://127.0.0.1:8000/api/login/ -d "username=user1&password=user1"

# Lista todas las tareas (requiere autenticación)
curl http://127.0.0.1:8000/api/todos/ -H "Authorization: Token <YOUR TOKEN>"

# Crea una nueva tarea (requiere autenticación)
curl -X POST http://127.0.0.1:8000/api/todos/ -H "Authorization: Token <YOUR TOKEN>" -d "title=Nueva Tarea&memo=Descripción de la nueva tarea"

# Actualiza una tarea existente (requiere autenticación)
curl -X PUT http://127.0.0.1:8000/api/todos/<id>/ -H "Authorization: Token <YOUR TOKEN>" -d "title=Tarea Actualizada"

# Marca una tarea como completada (requiere autenticación)
curl -X PUT http://127.0.0.1:8000/api/todos/<id>/complete/ -H "Authorization: Token <YOUR TOKEN>"
