# Configurando kubernetes
Para realizar los TPs vas a necesitar un cluster de kubernetes y el archivo de config para poder usar `kubectl` y comunicarte con el cluster. Hay varias alternativas a la hora de levantar un cluster:
* User un servicio manejado: la mayoria de los cloud providers ofrecen un servicio de kubernetes manejado. Manejado quiere decir que ellos se encargan de mantener el cluster de masters (etcd, api server y demas) por vos. Ademas de eso, suelen prohibirte (algunos te lo permiten) hacer `ssh` a los nodos workers. Lo bueno de estos servicios es que son muy faciles de configurar y para lo que vamos a estar haciendo no van a tener mucho costo. El mas barato que hemos visto es [Digital Ocean](https://cloud.digitalocean.com), por ~20usd mensuales pueden tener un cluster con mas que suficientes recursos para los TPs, de todas maneras se paga por uso y no necesitan tenerlo siempre levantado, pueden crear/eliminar para cada TP, si hacen eso les va a salir practicamente nada.
* Cluster local: una alternativa gratis es levantar kubernetes en su maquina. Al estar en su maquina van a haber un par de cosas que no van a poder hacer, pero para el primer TP alcanza. Pueden usar [kind](https://kind.sigs.k8s.io/docs/user/quick-start/), el unico requerimiento es tener Docker instalado. Una vez que lo instalan pueden crear un cluster con `kind create cluster --name k8s` y eso ya les va a dar un config file para usar con `kubectl`. Si no quieren usar kind pueden usar [minikube](https://minikube.sigs.k8s.io/docs/), la diferencia principal es que `minikube` levanta una maquina virtual y corre los componentes del cluster ahi dentro.
* Crear un cluster con [kubeadm](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/create-cluster-kubeadm/): si se sienten aventureros/as pueden crear el cluster de kubernetes desde cero por su cuenta usando `kubeadm`. Esto va a requerir crear un par de maquinas virtuales (en un cloud provider o localmente), inicializar el cluster en el nodo master y unir los workers al cluster.

## TP1
En este TP la idea es familiarizarse con `kubectl` y el ciclo de vida básico de la creación de un pod y deployment. Tambíen se pide
crear un pod multi-container para así aprender cómo los containers dentro del mismo interactúan entre sí.

1. Listar todos los namespaces en un cluster
2. Listar todos los PODS en todos los namespaces
3. Listar los pods en un namespace en particular
4. Crear un POD con 3 containers busybox que realizen los iguiente:
	- `ls; sleep 3600`
	- `echo "Hello World"; sleep 3600`
	- `echo "Este es el 3er contenedor"; sleep 3600`
5. Una vez creados los mismos chequear su estado
6. Crear un deployment llamado `webapp` con una imagen de nginx con 2 replicas. Luego:
	* Obtener el deployment creado y mostrar tus labels 
	* Obtener el archivo yaml del deployment creado 
	* Mostrar los pods corriendo del deployment 
	* Escalar el deployment de 2 a 5 replicas y verificar que funciona correctamente 
	* Obtener el estado del scale-up del deployment 
	* Mostrar el replicaset creado por el deployment 
