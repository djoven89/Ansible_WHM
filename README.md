# Ansible y WHM
Automatización de las tareas comunes para un servidor Centos 7 ejecutando el software WHM .

Las operaciones que realiza el playbook de Ansible sobre WHM:

* Instalación del software básico
* Configuración extra de seguridad para el servicio SSH y para las contraseñas del sistema.
* Instalación y configuración del comando 'aws' para la gestión de AWS.
* Instalación y configuración de las métricas de 'CloudWatch' de AWS.


## Cómo usar el repositorio

1. Descarga del repositorio en el equipo que contenga Ansible instalado:

		git clone https://github.com/djoven89/Ansible_WHM.git

2. Modificar la dirección IP del servidor junto con los valores de las variables globales:

		vim Ansible_WHM/hosts
		vim Ansible_WHM/group_vars/all

3. Ejecutar el 'playbook' :

		 ansible-playbook -i Ansible_WHM/hosts Ansible_WHM/configuration.yml -K


## Cómo usarlo con una imagen de Docker para Ansible

1. Iniciar el container que tenga la imagen de Ansible:

		docker run --rm --name ansible -h ansible -d -v /mnt/proyectos/ansible/:/etc/ansible mis_img/ansible:v1

2. Descargar el repositorio en el directorio mapeado:

		git clone https://github.com/djoven89/Ansible_WHM.git /mnt/proyectos/ansible

3. Especificar la IP de servidor o servidores y ajuste de las variables globales:

		vim Ansible_WHM/hosts
		vim Ansible_WHM/group_vars/all

4. Introducirse dentro del container:

		docker exec -ti ansible /bin/bash

5. Comprobar la conexión con SSH (importante aceptar el 'fingerprint') :

		ssh usuario@IP

6. Ejecutar el playbook:

		ansible-playbook -i /etc/ansible/hosts /etc/ansible/configuration.yml -K
