# Blog Project - Modelos, ORM y Panel de Administración en Django

Aplicación web desarrollada con **Django** que conecta el modelo `Post` con una base de datos relacional **SQLite (`db.sqlite3`)** mediante el ORM de Django y gestiona las publicaciones desde el panel administrativo `/admin`.

## Características implementadas
1. **Modelo `Post` (`posts/models.py`)**:
   - Campos: `titulo`, `contenido`, `autor`, `fecha_creacion` (`auto_now_add=True`) y `estado` (`borrador` / `publicado`).
   - Método `__str__` que retorna el título de la publicación.
2. **Migraciones y Base de Datos (`posts/migrations/0001_initial.py` y `db.sqlite3`)**:
   - Archivo de migración inicial generado para el modelo `Post`.
   - Base de datos `db.sqlite3` sincronizada con 4 publicaciones de prueba (3 en estado `publicado` y 1 en estado `borrador`).
3. **Panel de Administración (`posts/admin.py`)**:
   - Modelo `Post` registrado junto con la clase `PostAdmin(admin.ModelAdmin)` mostrando las columnas `titulo`, `autor`, `estado` y `fecha_creacion` en la lista (`list_display`).
4. **Consulta ORM y Renderizado Dinámico (`posts/views.py` y `posts/templates/posts/lista_posts.html`)**:
   - La vista `lista_posts` consulta `Post.objects.filter(estado="publicado").order_by("-fecha_creacion")`.
   - El template `lista_posts.html` recorre los objetos con `{% for post in posts %}` mostrando título, autor, fecha y contenido en la página de inicio.

## Cómo entrar al Panel de Administración (`/admin`)

1. Inicia el servidor de desarrollo desde la raíz del proyecto:
   ```bash
   python manage.py runserver
   ```
2. Abre tu navegador web e ingresa a:
   - **Página de inicio (lista dinámica de posts):** `http://127.0.0.1:8000/`
   - **Panel de administración:** `http://127.0.0.1:8000/admin/`
3. Inicia sesión en `/admin/` con las credenciales del superusuario incluido en `db.sqlite3`:
   - **Usuario:** `admin`
   - **Contraseña:** `admin1234`
   *(Opcionalmente, puedes crear un nuevo superusuario ejecutando `python manage.py createsuperuser` en la terminal).*
4. Dentro de la sección **Posts**, podrás crear nuevas publicaciones, editar las existentes y filtrar por `autor` y `estado` (`publicado` o `borrador`).
