# Módulo 1: Fundamentos de OpenShift CLI (oc), Proyectos y Despliegues

## 1. Conceptos Clave de Arquitectura
- **Namespace vs. Project:** En Kubernetes se usan namespaces. En OpenShift se usan **Projects**, que son namespaces extendidos con políticas de seguridad (RBAC), cuotas de recursos y aisladores de red SDN/OVN.
- **Generación Imperativa (--dry-run=client):** La regla de oro en el EX180 es **nunca escribir YAMLs desde cero**. Generamos manifiestos básicos con la CLI y los modificamos.

## 2. Diagrama de Integración Módulo 1
``n[ Cliente / CLI oc ] -> (oc new-project ex180-mod1) -> [ Project: ex180-mod1 ]
[ Deployment ] ---> [ Pods ] <--- [ Service (ClusterIP) ] <--- [ Route (Ingress Router) ]
``n
## 3. Comandos de Examen Esenciales
- oc login -u developer -p developer https://api.crc.testing:6443
- oc new-project ex180-mod1
- oc new-app --docker-image=docker.io/nginxinc/nginx-unprivileged:latest --name=nginx-cert
- oc expose svc/nginx-cert

## 4. Pregunta Tipo Examen EX180
**Escenario:** Intentas descargar una imagen de un registro privado y el Pod queda en ImagePullBackOff con error unauthorized: authentication required.

**Solución Correcta:**
Crear un Secret tipo docker-registry y vincularlo a la Cuenta de Servicio default del proyecto:
oc secrets link sa/default <secret-name> --for=pull

**Análisis de Opciones:**
- A) SSH al nodo y podman login: INCORRECTA. No es escalable ni declarativo.
- B) Secret docker-registry + link sa/default: CORRECTA. Forma nativa y segura.
- C) Modificar daemon.json: INCORRECTA. Eso es para registros sin TLS (HTTP).
- D) Flag --grant-permissions: INCORRECTA. El flag no existe en oc new-app.
