
# Kubernetes (K8s)

Kubernetes (K8s) es una plataforma de código abierto para automatizar la implementación, el escalado y la gestión de aplicaciones en contenedores.

## Conceptos Clave

- **Cluster**: Un conjunto de máquinas que ejecutan aplicaciones en contenedores. Un cluster de K8s está formado por:
    - **Control Plane**: El cerebro del clúster. Toma las decisiones y responde a las solicitudes del usuario.
    - **Worker Nodes**: Los nodos de trabajo donde se ejecutan tus aplicaciones.
- **Pod**: La unidad de despliegue más pequeña. Un Pod es uno o más contenedores que comparten recursos como la red y el almacenamiento. Son efímeros.
- **Deployment**: Un objeto que gestiona réplicas de Pods. Asegura que el número deseado de Pods se esté ejecutando y los reemplaza si fallan.
- **Service**: Un objeto que expone una aplicación dentro del clúster con una dirección IP y un nombre de DNS estables, permitiendo que otros Pods la encuentren.
- **Ingress**: Gestiona el acceso externo al clúster para tráfico HTTP/S.

---

## Comandos Esenciales de `kubectl`

`kubectl` es la herramienta de línea de comandos para interactuar con tu clúster de K8s.

| Comando                                     | Función                                                               |
|---------------------------------------------|-----------------------------------------------------------------------|
| `kubectl get pods`                          | Lista los Pods que se están ejecutando.                               |
| `kubectl apply -f archivo.yaml`             | Crea o actualiza recursos a partir de un archivo.                     |
| `kubectl delete -f archivo.yaml`            | Elimina recursos del clúster.                                         |
| `kubectl describe pod <nombre>`             | Muestra un resumen detallado de un Pod específico, útil para depurar. |
| `kubectl logs <nombre-del-pod>`             | Muestra la salida (logs) de un contenedor.                            |
| `kubectl exec -it <nombre-del-pod> -- bash` | Abre una terminal interactiva dentro de un Pod.                       |

