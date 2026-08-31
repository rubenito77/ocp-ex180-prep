# Módulo 2: Configuración de Aplicaciones (ConfigMaps y Secrets)

## 1. Conceptos Clave de Arquitectura
- **ConfigMap:** Almacena datos de configuración no confidenciales en texto plano (archivos .properties, variables de entorno).
- **Secret:** Almacena datos sensibles (contraseñas, llaves TLS, tokens) codificados en Base64.
- **Inyección:** Se pueden inyectar como variables de entorno (oc set env) o montados como archivos en el sistema de archivos (oc set volume).

## 2. Diagrama de Integración Módulo 2
``n[ ConfigMap / Secret ] ---> [ Deployment ] ---> [ Pod ] ---> (Env Vars / Volume Mount)
``n
## 3. Comandos de Examen Esenciales
- oc create secret generic db-credentials --from-literal=DB_USER=appuser --from-literal=DB_PASS=SuperSecure123
- oc create configmap app-config --from-file=app.properties
- oc set env deployment/nginx-cert --from=secret/db-credentials
- oc set volume deployment/nginx-cert --add --name=config-volume --type=configmap --configmap-name=app-config --mount-path=/etc/config

## 4. Pregunta Tipo Examen EX180
**Escenario:** Inyectar credenciales de BD y un archivo app.properties sin exponer datos sensibles en texto plano en los manifiestos YAML.

**Solución Correcta:**
Crear un Secret para credenciales, un ConfigMap para el archivo app.properties, inyectar el Secret con oc set env y montar el ConfigMap con oc set volume.

**Análisis de Opciones:**
- A) Hardcode en YAML + PVC: INCORRECTA. Expone datos sensibles.
- B) ConfigMap para claves y Secret para propiedades: INCORRECTA. Invierte la seguridad.
- C) Secret para credenciales + ConfigMap montado: CORRECTA. Cumple estándares.
- D) Recompilar imagen con COPY: INCORRECTA. Viola inmutabilidad.
