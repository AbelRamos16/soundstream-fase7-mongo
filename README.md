# 🎵 SoundStream - Fase 7 | Proyecto Integrador

Plataforma de streaming de música desarrollada sobre **MongoDB (NoSQL)** como parte del Proyecto Integrador de **Base de Datos II**.

Esta versión implementa una arquitectura basada en documentos utilizando **MongoDB Atlas**, un backend desarrollado con **Django**, y un frontend en **HTML, CSS y JavaScript**. Además, integra la API pública de **Deezer** para obtener imágenes de artistas, portadas de álbumes y previews de audio de 30 segundos.

> **Materia:** ITIZ-2201 - Base de Datos II  
> **Fase:** 7 - Implementación Web sobre MongoDB

---

# 🚀 Tecnologías utilizadas

- **Backend**
  - Python 3.12
  - Django 5.2
  - django-mongodb-backend
  - PyMongo

- **Base de datos**
  - MongoDB Atlas
  - Modelo NoSQL basado en documentos

- **Frontend**
  - HTML5
  - CSS3
  - JavaScript Vanilla

- **API externa**
  - Deezer API (sin API Key)

---

# 📁 Modelo NoSQL

La aplicación utiliza un modelo documental optimizado para MongoDB.

## Colecciones principales

- `usuarios`
- `artistas`
- `albumes`
- `canciones`
- `playlists`
- `pagos`
- `reproducciones`

### Características del modelo

- **Artistas**
  - Embeben la información de la discográfica.

- **Canciones**
  - Embeben el arreglo de géneros.
  - Referencian al artista y al álbum.

- **Usuarios**
  - Embeben:
    - cancionesGuardadas
    - albumesGuardados
    - artistasSeguidos

- **Playlists**
  - Embeben el arreglo de canciones.

- Los identificadores (`_id`) son enteros incrementales calculados automáticamente.

---

# 📋 Requisitos previos

Antes de ejecutar el proyecto es necesario tener instalado:

- Python 3.12
- MongoDB Atlas (o una instancia accesible)
- Git
- Conexión a Internet (Atlas + Deezer)

---

# ⚙ Instalación

## 1. Clonar el repositorio

```powershell
git clone https://github.com/AbelRamos16/soundstream-fase7-mongo.git
cd soundstream-fase7-mongo
```

---

## 2. Crear entorno virtual

```powershell
py -3.12 -m venv .venv

.\.venv\Scripts\Activate.ps1
```

---

## 3. Instalar dependencias

```powershell
pip install -r soundstream/requirements.txt
```

---

# 🔐 Configuración de MongoDB Atlas

Por seguridad, la cadena de conexión **no se almacena dentro del proyecto**.

Copiar el archivo de ejemplo:

```powershell
cd soundstream

copy db_config.example.json db_config.json
```

Editar el archivo:

```json
{
  "URI": "mongodb+srv://USUARIO:PASSWORD@cluster.mongodb.net/?retryWrites=true&w=majority",
  "NAME": "SoundStreamDB_NoSQL"
}
```

También puede especificarse mediante la variable de entorno:

```
SOUNDSTREAM_DB_CONFIG
```

---

# 🗄 Migraciones de Django

```powershell
python manage.py migrate
```

Esto crea únicamente las colecciones internas utilizadas por Django.

Las colecciones de SoundStream ya deben existir dentro de MongoDB Atlas.

---

# 🎼 (Opcional) Actualizar contenido desde Deezer

```powershell
python manage.py fotos_artistas

python manage.py portadas_albumes

python manage.py previews_canciones
```

---

# ▶ Ejecutar el proyecto

```powershell
python manage.py runserver
```

Abrir:

```
http://127.0.0.1:8000/
```

---

# 👤 Usuario Administrador

Puede ingresar al sistema utilizando el siguiente usuario de prueba:

**Administrador**

**Email**

```
abelramos302@gmail.com
```

**Contraseña**

```
12345
```

---

# 🎧 Funcionalidades

| Página | Descripción |
|---------|-------------|
| `/` | Página principal con Top Canciones y Top Artistas |
| `/catalogo/` | Catálogo musical con buscador |
| `/artistas/` | Consulta de artistas |
| `/albumes/` | Consulta de álbumes |
| `/usuarios/playlists/publicas/` | Playlists públicas |
| `/usuarios/playlists/mias/` | CRUD de playlists personales |
| `/usuarios/playlists/<id>/` | Gestión de canciones de una playlist |
| `/suscripciones/` | Planes de suscripción |
| `/suscripciones/contratar/` | Pago simulado |
| `/operacion/historial/` | Historial de reproducciones y pagos |
| `/operacion/regalias/` | Reporte de regalías |
| `/catalogo/gestion/` | Panel administrativo |
| `/reportes/` | Dashboard de reportes administrativos |

---

# 💳 Tarjeta de prueba

Número

```
4242 4242 4242 4242
```

Fecha

```
12/30
```

CVV

```
123
```

---

# 🛠 Comandos útiles

```powershell
python manage.py check

python manage.py migrate

python manage.py runserver

python manage.py fotos_artistas

python manage.py portadas_albumes

python manage.py previews_canciones
```

Todos los comandos aceptan:

```
--solo-vacias
```

para procesar únicamente registros incompletos.

---

# 🏗 Arquitectura

```
Cliente
      │
      ▼
Frontend
HTML + CSS + JS
      │
      ▼
Django
      │
      ▼
MongoDB Atlas
```

La aplicación implementa una arquitectura basada en:

- Modelo Cliente-Servidor
- Base de datos NoSQL
- Documentos embebidos
- Aggregation Pipelines
- Separación por aplicaciones Django

---

# 🔒 Seguridad

- La conexión a MongoDB se almacena en un archivo externo (`db_config.json`).
- No existen credenciales dentro del código fuente.
- Los reportes utilizan **Aggregation Pipelines** de MongoDB.
- Los pagos son completamente simulados.
- No se almacenan datos de tarjetas bancarias.

---

# 📌 Observaciones

- Las imágenes y previews provienen directamente desde Deezer.
- Si no existe conexión a Internet, se mostrarán imágenes de respaldo.
- Las URLs de audio se obtienen dinámicamente para evitar expiración.
- El sistema utiliza un modelo documental optimizado para MongoDB.
- Las contraseñas de los usuarios se mantienen en texto plano únicamente porque corresponden a los datos académicos entregados para el proyecto.

---

# 👨‍💻 Autor

**Abel Ramos, Sthefano Zambrano y Julian Pacheco**

Proyecto Integrador - Base de Datos II

Universidad de Las Américas (UDLA)

GitHub

https://github.com/AbelRamos16

---

# 📄 Licencia

Proyecto desarrollado con fines exclusivamente académicos para la asignatura **Base de Datos II**.
