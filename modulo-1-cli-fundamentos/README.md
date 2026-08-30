# Módulo 1: Fundamentos de OpenShift CLI (oc), Proyectos y Despliegues

## Comandos Esenciales para EX180

### 1. Gestión de Sesión y Contexto
- oc login -u developer -p developer https://api.crc.testing:6443
- oc new-project ex180-mod1
- oc project

### 2. Despliegue de Aplicaciones
- oc new-app --docker-image=docker.io/nginxinc/nginx-unprivileged:latest --name=nginx-cert

### 3. Exposición Externa
- oc expose svc/nginx-cert

### 4. Técnica Dry-Run
- oc create deployment web-app --image=quay.io/bitnami/nginx:latest --dry-run=client -o yaml > deployment.yaml
