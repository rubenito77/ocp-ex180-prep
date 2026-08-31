# Diagrama de Arquitectura - Módulo 1: Despliegue e Ingress Base

## Flujo de Integración de Componentes

``n  +---------------------------------------------------------------------------------+
  | OPENSHIFT PROJECT: ex180-mod1                                                   |
  |                                                                                 |
  |   [ CLI: oc new-app ]                                                           |
  |           |                                                                     |
  |           +---> [ ImageStream: nginx-cert ] ---> Rastrea Tag en Registro Extero |
  |           |                                       (Docker Hub / Quay.io)        |
  |           +---> [ Deployment: nginx-cert ]                                      |
  |                       |                                                         |
  |                       v (gestiona réplicas)                                     |
  |                 [ Pod: nginx-cert-xxx ] (Contenedor ejecutando en puerto 8080)   |
  |                       ^                                                         |
  |                       | (selección mediante Labels)                             |
  |   [ CLI: oc expose ]  |                                                         |
  |           |           |                                                         |
  |           +---> [ Service: nginx-cert ] (Balanceador L4 / ClusterIP:8080)       |
  |                       ^                                                         |
  |                       | (reenvío de tráfico HTTP/L7)                            |
  |   [ CLI: oc expose ]  |                                                         |
  |           |           |                                                         |
  |           +---> [ Route: nginx-cert ] (Dominio FQDN en Ingress Controller)      |
  +---------------------------------------------------------------------------------+
                                  ^
                                  | (Tráfico Web Externo)
                   [ Ingress Router (HAProxy) ]
`"

# Actualizar el README.md limpio del Módulo 1
Set-Content -Path .\modulo-1-cli-fundamentos\README.md -Value 
