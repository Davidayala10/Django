# Django PostgreSQL Docker - Sistema de Autenticación Completo

Una aplicación web Django moderna con sistema de autenticación completo, PostgreSQL como base de datos y Docker para fácil despliegue. Este proyecto incluye registro de usuarios, login/logout, gestión de usuarios y una interfaz responsive con Bootstrap.

## 🚀 Características

- ⚡ **Django 4.x** - Framework web moderno y robusto
- 🐘 **PostgreSQL** - Base de datos relacional potente
- 🐳 **Docker & Docker Compose** - Containerización completa
- 🔐 **Sistema de Autenticación** - Registro, login, logout
- 👥 **Gestión de Usuarios** - Lista y administración de usuarios
- 🎨 **Bootstrap 5** - Interfaz responsive y moderna
- 📱 **Responsive Design** - Compatible con dispositivos móviles
- ✅ **Validación de Formularios** - Validación robusta del lado servidor
- 🔒 **Protección de Rutas** - Control de acceso a páginas sensibles

## 📋 Requisitos Previos

- [Docker](https://www.docker.com/get-started) (versión 20.x o superior)
- [Docker Compose](https://docs.docker.com/compose/install/) (versión 2.x o superior)

## 🛠️ Instalación y Configuración

### 1. Clonar el Repositorio

```bash
git clone https://github.com/Davidayala10/django-postgres-docker.git
cd django-postgres-docker
```

### 2. Construir los Contenedores

```bash
docker-compose build
```

### 3. Ejecutar la Aplicación

```bash
docker-compose up
```

### 4. Aplicar Migraciones

En una nueva terminal, ejecuta:

```bash
docker-compose run web python manage.py migrate
```

### 5. Crear Superusuario (Opcional)

```bash
docker-compose run web python manage.py createsuperuser
```

### 6. Acceder a la Aplicación

Abre tu navegador y ve a: **http://localhost:8080**

## 🏗️ Estructura del Proyecto

```
django-postgres-docker/
├── app/                          # Aplicación Django principal
│   ├── templates/               # Templates HTML
│   │   ├── index.html          # Página principal
│   │   ├── registration/       # Templates de autenticación
│   │   │   ├── login.html     # Formulario de login
│   │   │   └── registro.html  # Formulario de registro
│   │   └── usuarios/          # Templates de usuarios
│   │       └── lista.html     # Lista de usuarios
│   ├── __init__.py
│   ├── admin.py               # Configuración del admin
│   ├── apps.py                # Configuración de la app
│   ├── forms.py               # Formularios personalizados
│   ├── models.py              # Modelos de base de datos
│   ├── settings.py            # Configuración de Django
│   ├── urls.py                # URLs de la aplicación
│   ├── views.py               # Vistas de la aplicación
│   └── wsgi.py                # Configuración WSGI
├── docker-compose.yml         # Configuración de servicios
├── Dockerfile                 # Imagen Docker para Django
├── manage.py                  # Script de gestión de Django
├── requirements.txt           # Dependencias de Python
├── LICENSE                    # Licencia MIT
└── README.md                  # Este archivo
```

## 🌐 Rutas Disponibles

| Ruta | Descripción | Acceso |
|------|-------------|---------|
| `/` | Página principal | Público |
| `/registro/` | Registro de nuevos usuarios | Público |
| `/login/` | Inicio de sesión | Público |
| `/logout/` | Cerrar sesión | Autenticado |
| `/usuarios/` | Lista de usuarios registrados | Autenticado |
| `/admin/` | Panel de administración | Superusuario |

## 💻 Comandos Útiles

### Gestión de Contenedores

```bash
# Ejecutar en segundo plano
docker-compose up -d

# Ver logs
docker-compose logs

# Ver logs de un servicio específico
docker-compose logs web

# Detener contenedores
docker-compose down

# Detener y eliminar volúmenes
docker-compose down -v
```

### Comandos de Django

```bash
# Crear migraciones
docker-compose run web python manage.py makemigrations

# Aplicar migraciones
docker-compose run web python manage.py migrate

# Crear superusuario
docker-compose run web python manage.py createsuperuser

# Ejecutar tests
docker-compose run web python manage.py test

# Acceder al shell de Django
docker-compose run web python manage.py shell
```

### Comandos de Base de Datos

```bash
# Acceder a PostgreSQL
docker-compose exec db psql -U postgres -d postgres

# Backup de la base de datos
docker-compose exec db pg_dump -U postgres postgres > backup.sql

# Restaurar backup
docker-compose exec -T db psql -U postgres postgres < backup.sql
```

## 🎨 Características de la Interfaz

### Página Principal
- **Diseño moderno** con gradientes y efectos hover
- **Navegación inteligente** que cambia según el estado de autenticación
- **Secciones informativas** sobre las tecnologías utilizadas
- **Responsive design** para móviles y tablets

### Sistema de Autenticación
- **Formularios validados** con mensajes de error claros
- **Registro automático** con inicio de sesión después del registro
- **Mensajes de feedback** para acciones exitosas o erróneas
- **Redirecciones inteligentes** después de login/logout

### Gestión de Usuarios
- **Lista completa** de usuarios registrados
- **Información detallada** (ID, nombre, email, fecha de registro, estado)
- **Interfaz tipo tabla** con diseño limpio y ordenado
- **Acceso protegido** solo para usuarios autenticados

## ⚙️ Variables de Entorno

Las siguientes variables se pueden configurar en `docker-compose.yml`:

```yaml
environment:
  - DJANGO_SECRET_KEY=tu-clave-secreta-aqui
  - POSTGRES_DB=nombre_base_datos
  - POSTGRES_USER=usuario_postgres
  - POSTGRES_PASSWORD=contraseña_postgres
  - DEBUG=True  # Solo para desarrollo
```

## 🔧 Personalización

### Cambiar el Puerto

Para cambiar el puerto de la aplicación, modifica en `docker-compose.yml`:

```yaml
ports:
  - "3000:8080"  # Cambiar 8080 por el puerto deseado
```

### Agregar Nuevas Dependencias

1. Añade la dependencia a `requirements.txt`
2. Reconstruye la imagen: `docker-compose build`

### Personalizar Estilos

Los templates utilizan Bootstrap 5 CDN. Para personalizar:

1. Crea archivos CSS estáticos en `app/static/css/`
2. Configura `STATIC_URL` y `STATICFILES_DIRS` en `settings.py`
3. Carga los archivos estáticos en tus templates

## 🔒 Seguridad

### Para Producción

1. **Cambiar SECRET_KEY**: Genera una clave secreta única
2. **Deshabilitar DEBUG**: Establece `DEBUG = False`
3. **Configurar ALLOWED_HOSTS**: Añade tu dominio
4. **Usar HTTPS**: Configura SSL/TLS
5. **Variables de entorno**: Usa archivos `.env` para credenciales

```python
# settings.py para producción
DEBUG = False
ALLOWED_HOSTS = ['tu-dominio.com', 'www.tu-dominio.com']
```

## 📊 Monitoring y Logs

### Ver logs en tiempo real

```bash
# Todos los servicios
docker-compose logs -f

# Solo Django
docker-compose logs -f web

# Solo PostgreSQL  
docker-compose logs -f db
```

### Acceder a los contenedores

```bash
# Contenedor web (Django)
docker-compose exec web bash

# Contenedor de base de datos
docker-compose exec db bash
```

## 🧪 Testing

Ejecutar los tests incluidos:

```bash
docker-compose run web python manage.py test
```

Para añadir nuevos tests, edita `app/tests.py` o crea nuevos archivos de test.

## 🚀 Despliegue

### Desarrollo Local
Este setup está optimizado para desarrollo local con hot-reload y debugging habilitado.

### Producción
Para producción, considera:

1. **Servidor web dedicado** (Nginx + Gunicorn)
2. **Base de datos externa** (PostgreSQL gestionado)
3. **Variables de entorno seguras**
4. **Archivos estáticos en CDN**
5. **Monitoring y logging**

## 🤝 Contribuir

1. Fork el proyecto
2. Crea una rama para tu feature (`git checkout -b feature/AmazingFeature`)
3. Commit tus cambios (`git commit -m 'Add some AmazingFeature'`)
4. Push a la rama (`git push origin feature/AmazingFeature`)
5. Abre un Pull Request

## 📝 Changelog

### v2.0.0 (Actual)
- ✅ Sistema completo de autenticación
- ✅ Interfaz Bootstrap 5 responsive
- ✅ Gestión de usuarios
- ✅ Templates modernos
- ✅ Validación de formularios
- ✅ Protección de rutas

### v1.0.0 (Inicial)
- ✅ Configuración básica Django + PostgreSQL + Docker
- ✅ Página de inicio simple

## 🐛 Solución de Problemas

### Error: "Could not connect to database"
```bash
# Verificar que el servicio de BD esté ejecutándose
docker-compose ps

# Reiniciar los servicios
docker-compose down && docker-compose up
```

### Error: "Port already in use"
```bash
# Cambiar el puerto en docker-compose.yml o detener el proceso que usa el puerto
lsof -ti:8080 | xargs kill -9
```

### Error: "Template not found"
```bash
# Verificar la estructura de templates y settings.py
docker-compose run web python manage.py check
```

## 📞 Soporte

Si tienes problemas o preguntas:

1. Revisa la sección de **Solución de Problemas**
2. Busca en los **Issues** del repositorio
3. Crea un **nuevo Issue** con detalles del problema

## 📄 Licencia

Este proyecto está licenciado bajo la Licencia MIT. Ver el archivo [LICENSE](LICENSE) para más detalles.

## 🙏 Agradecimientos

- [Django](https://www.djangoproject.com/) - El framework web para perfeccionistas con deadlines
- [PostgreSQL](https://www.postgresql.org/) - La base de datos más avanzada del mundo
- [Docker](https://www.docker.com/) - Containerización que funciona
- [Bootstrap](https://getbootstrap.com/) - Framework CSS para desarrollo responsive

---

⭐ **¡Si te gusta este proyecto, dale una estrella!** ⭐
