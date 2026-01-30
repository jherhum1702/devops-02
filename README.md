# Tarea DevOps  
**Autor:** José Antonio Hernández Humanes  

---

## 2. Conociendo la aplicación

### 2.0.1 Reinicio del servicio Docker y de red

Antes de comenzar, se reinician los servicios necesarios:

```bash
sudo systemctl restart docker.service
sudo systemctl restart networking.service
```

---

## 2.1 Prueba local

### 2.1.1 Creación y activación del entorno virtual

Se crea y activa un entorno virtual para aislar las dependencias del proyecto:

```bash
python3 -m venv .venv
source .venv/bin/activate
```

---

### 2.1.3 Instalación de dependencias

Instalación de los paquetes necesarios definidos en el fichero `requirements.txt`:

```bash
pip install -r requirements.txt
```

---

### 2.1.4 Comprobación de funcionamiento de la aplicación

Ejecución directa de la aplicación:

```bash
python3 src/app.py
```

También se ha probado el arranque mediante **Gunicorn**:

```bash
gunicorn --chdir src app:app --bind 0.0.0.0:5000
```

📸 Foto:  
[Ver captura en Imgur](https://imgur.com/kl9bC4g)

---

## 2.2 Creación de la imagen Docker

- Se ha creado un fichero `.dockerignore` para excluir el entorno virtual `.venv`.
- Se ha modificado el fichero `index.html` para incluir el nombre del autor.

### Construcción de la imagen Docker

```bash
docker build -t hernande/galeria:latest .
```

### Arranque del contenedor

```bash
docker run -d -p 80:5000 --name testgaleria hernande/galeria:latest
```

📸 Foto:  
[Ver captura en Imgur](https://imgur.com/kl9bC4g)

### Parada y eliminación del contenedor

```bash
docker stop testgaleria && docker rm testgaleria
```

---

## 2.3 Prueba de la imagen en local con Docker Compose

Se ha modificado el fichero `docker-compose.yml` para que utilice la imagen subida a Docker Hub:

```yaml
image: hernande/galeria:latest
```

### Arranque del servicio

```bash
docker compose up -d
```

📸 Foto:  
[Ver captura en Imgur](https://imgur.com/tb35faM)

### Parada del servicio

```bash
docker compose down
```

---

## 2.4 Subida de la imagen a Docker Hub

Finalmente, se sube la imagen al repositorio de Docker Hub:

```bash
docker push hernande/galeria:latest
```

---

