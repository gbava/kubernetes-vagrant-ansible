# Tareas a realizar:

### Creación  de 3 máquinas virtuales CentOS 7:
- centos-master (ip: 10.10.0.10)
- centos-node1 (ip: 10.10.0.11)
- centos-node2 (ip: 10.10.0.12)

### Configuración de Kubernetes
Se configura kubernetes con los tres nodos:

- centos-master (master node)
- centos-node1 (node)
- centos-node2 (node)

### Despliegue de la aplicación  
Despliegue de esta [aplicación](https://github.com/spring-projects/spring-boot/tree/master/spring-boot-samples/spring-boot-sample-hateoas)  en dos de los nodos en el puerto 9000 sin modificar el código de la app.

### Instalación  de un load balancer. 
- Instalación de un load balancer en el nodo restante para balancear entre los dos nodos.
- El entrypoint será el puerto 443.