# Diagrama de Arquitectura - Módulo 3: Rutas TLS Edge

## Flujo de Integración de Componentes

``n  [ Cliente Web / Navegador ]
             |
             | (Tráfico HTTPS / Puerto 443)
             v
  +---------------------------------------------------------------------------------+
  | OPENSHIFT INGRESS ROUTER (HAProxy)                                              |
  |                                                                                 |
  |   Route EDGE (Contiene tls.crt y tls.key)                                        |
  |   -> Realiza la terminación SSL/TLS y descifra el tráfico aquí.                 |
  +---------------------------------------------------------------------------------+
             |
             | (Tráfico HTTP Plano / Puerto 8080 en Red SDN Interna)
             v
  +---------------------------------------------------------------------------------+
  | OPENSHIFT PROJECT: ex180-mod3                                                   |
  |                                                                                 |
  |   [ Service: secure-app ] (ClusterIP)                                           |
  |             |                                                                   |
  |             v                                                                   |
  |   [ Pod: secure-app ] (Procesa tráfico HTTP ligero sin carga criptográfica)      |
  +---------------------------------------------------------------------------------+
