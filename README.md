# Odoo-18
Paso a paso

Utilice WSL2 para poder trabajar en un entorno Linux real sin necesidad de modificar mi instalación de windows.

WSl2 + DOCKER
No es necesario cambiar completamente de sistema operativo.
Me acerco al entorno Linux
Es más facil levantar Odoo

DOCKER
Simplifica el manejo de dependencias, hace el entorno reproducible y evita problema de instalación local.

UBUNTU
Es una de las distribuciones Linux más utilizadas en desarrollo y tiene muy buena compatibilidad con Docker y Odoo.

1. Primero verifique si tenia habilitado WSL2.
- wsl --status

2. Despues verifique si tenia instalado Ubuntu
- wsl -l -v
instalación
- wsl --install Ubuntu
Luego cree mi usuario Linux y entre a la terminal Ubuntu.

3. Actulice Ubuntu
sudo apt update && sudo apt upgrade -y
update → actualiza la lista de paquetes
upgrade → instala actualizaciones

Aqui ya tenia listo el entorno Linux

4. Luego instale Docker desktop
Active la integración con Ubuntu
Luego verifique en la terminal de Ubuntu y estaba funcionando correctamente
- docker --version
- docker compose version

5. Creé el proyecto Odoo.
Dentro de ubunto ejecuté:
- mkdir ~/odoo18
- cd ~/odoo18

6. Creé el archivo que levantara Odoo y PostgreSQL
Levante automaticamente Odoo usando Docker y PostgreSQL
Definí los contenedoress que se van a ejecutar

Dentro de la carpeta Odoo18:
nano docker-compose.yml

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

7. Levantar Odoo
Ejecuté el archivo que había creado
- Descarga imagenes
- Crea la red interna
- Crea los volumenes
- Inicia los contenedores
sudo docker compose up

Levantar nuevamente
sudo docker compose up

Levantar en segundo plano
sudo docker compose up -d

Detener contenedores
sudo docker compose down


  


