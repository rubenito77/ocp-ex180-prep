# Diagrama de Arquitectura - Módulo 2: Inyección de Configuración y Seguridad

## Flujo de Integración de Componentes

``n  +---------------------------------------------------------------------------------+
  | OPENSHIFT PROJECT: ex180-mod2                                                   |
  |                                                                                 |
  |   [ Archivo app.properties ] ---> [ ConfigMap: app-config ]                    |
  |                                            |                                    |
  |                                            | (oc set volume --type=configmap)   |
  |                                            v                                    |
  |   [ Secret: db-credentials ] ---> [ Deployment: nginx-cert ]                    |
  |    (DB_USER, DB_PASS en Base64)            |                                    |
  |                                            | (oc set env --from=secret/...)     |
  |                                            v                                    |
  |                                [ Pod: nginx-cert-yyy ]                          |
  |                                +--------------------------------------------+   |
  |                                | Contenedor de Aplicación                   |   |
  |                                | - Env Vars: DB_USER=appuser                |   |
  |                                | - Mount Path: /etc/config/app.properties   |   |
  |                                +--------------------------------------------+   |
  +---------------------------------------------------------------------------------+
