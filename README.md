# Odoo-18

## Paso a paso

Utilice WSL2 para poder trabajar en un entorno Linux real sin necesidad de modificar mi instalación de Windows.

### WSL2 + Docker

* No es necesario cambiar completamente de sistema operativo.
* Me acerco al entorno Linux.
* Es más fácil levantar Odoo.

### Docker

Simplifica el manejo de dependencias, hace el entorno reproducible y evita problema de instalación local.

### Ubuntu

Es una de las distribuciones Linux más utilizadas en desarrollo y tiene muy buena compatibilidad con Docker y Odoo.

---

## 1. Verificación de WSL2

Primero verifique si tenía habilitado WSL2.

```bash
wsl --status
```

---

## 2. Verificación e instalación de Ubuntu

Después verifique si tenía instalado Ubuntu.

```bash
wsl -l -v
```

Instalación:

```bash
wsl --install Ubuntu
```

Luego creé mi usuario Linux y entré a la terminal Ubuntu.

---

## 3. Actualización de Ubuntu

```bash
sudo apt update && sudo apt upgrade -y
```

* `update` → actualiza la lista de paquetes.
* `upgrade` → instala actualizaciones.

Aquí ya tenía listo el entorno Linux.

---

## 4. Instalación de Docker Desktop

Luego instalé Docker Desktop.

Activé la integración con Ubuntu.

Luego verifiqué en la terminal de Ubuntu y estaba funcionando correctamente:

```bash
docker --version
docker compose version
```

---

## 5. Creación del proyecto Odoo

Dentro de Ubuntu ejecuté:

```bash
mkdir ~/odoo18
cd ~/odoo18
```

---

## 6. Creación del archivo que levantará Odoo y PostgreSQL

Levanté automáticamente Odoo usando Docker y PostgreSQL.

Definí los contenedores que se van a ejecutar.

Dentro de la carpeta `odoo18`:

```bash
nano docker-compose.yml
```

```yaml
services:
  web:
    image: odoo:18
    depends_on:
      - db
    ports:
      - "8069:8069"
    environment:
      - HOST=db
      - USER=odoo
      - PASSWORD=odoo
    volumes:
      - odoo-web-data:/var/lib/odoo

  db:
    image: postgres:15
    environment:
      - POSTGRES_DB=postgres
      - POSTGRES_USER=odoo
      - POSTGRES_PASSWORD=odoo
    volumes:
      - odoo-db-data:/var/lib/postgresql/data

volumes:
  odoo-web-data:
  odoo-db-data:
```

---

## 7. Levantar Odoo

Ejecuté el archivo que había creado.

Este proceso:

* Descarga imágenes.
* Crea la red interna.
* Crea los volúmenes.
* Inicia los contenedores.

```bash
cd ~/odoo18
```

### Levantar nuevamente

```bash
sudo docker compose up
```

### Levantar en segundo plano

```bash
sudo docker compose up -d
```
### Mostrar

```bash
sudo docker ps
```

### Detener contenedores

```bash
sudo docker compose down
```

---

## Acceso a Odoo

Puerto:

```text
http://localhost:8069
```



  


