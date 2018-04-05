# Descripción
Conjunto de scripts para el despliegue de un cluster kubernetes con los siguientes [requerimientos](REQUERIMIENTOS.md)

# Prerequisitos:

- Libvirt
- Vagrant con libvirt
- Ansible 2.4 >
- 3GB de RAM para las vms

# Instalacion:

Para poder utilizar libvirt como provider en Vagrant necesitamos el plugin *vagrant-libvirt*
  
Para instalarlo primero instalar las dependencias necesarias según tu distro siguiendo estas [indicaciones](https://github.com/vagrant-libvirt/vagrant-libvirt#installation) 

Posteriormente instalar el plugin en Vagrant: `vagrant plugin install vagrant-libvirt` 

Por último indicar que Vagrant utilice libvirt: 
`export VAGRANT_DEFAULT_PROVIDER=libvirt`

y ahora desplegamos las vms con `vagrant up`

El provisioner es el playbook de Ansible *site.yml*

(Como en mi entorno no se ejecutaba correctamente el playbook desde Vagrant tuve que quitar esa referencia)
Por ello es que el último paso es ejecutar el playbook:


    ansible-playbook site.yml

# Variables
En `servers.yaml` se definen las variables para las vms de Vagrant.
El resto de las variables está definido en el fichero `group_vars/all.yml`


# Roles del playbook
## pre-setup
Configura las vms con los requerimientos necesarios.

## install-kubernetes
Instala un cluster kubernetes en 3 nodos (1 master + 2 nodos).

## ingress-nginx
Crea y configura Ingress con Ngninx para hacer load balancing desde el nodo master. 

## build-app
Este rol contruye los artefactos de la aplicacion que necesitaremos luego para crear la imagen docker.

## deploy-app
Instala la imagen y crea un contenedor con la aplicacion en el cluster kubernetes.

# Test
Para poder acceder es necesario editar /etc/hosts y agregar el siguiente registro:

```
10.10.0.10  spring-boot-sample-hateoas.cluster.local
```


La aplicacion puede accederse en el puerto tcp 443: https://spring-boot-sample-hateoas.cluster.local

Podemos probar por ej: 
```
curl -v https://spring-boot-sample-hateoas.cluster.local/customers/1 -k
```
