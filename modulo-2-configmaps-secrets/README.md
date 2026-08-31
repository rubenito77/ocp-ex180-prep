# Módulo 2: Configuración de Aplicaciones (ConfigMaps y Secrets)

## 1. Conceptos Clave
- **ConfigMap:** Datos de configuración no confidenciales en texto plano.
- **Secret:** Datos sensibles (contraseñas, llaves TLS, tokens) codificados en **Base64**.
- **Mecanismos de Inyección:** Variables de entorno (oc set env) o Volúmenes montados (oc set volume).

> Nota: Consulta el archivo DIAGRAMA.md en esta carpeta para ver la interacción entre objetos.

## 2. Comandos de Examen Esenciales
- oc create secret generic db-credentials --from-literal=DB_USER=appuser --from-literal=DB_PASS=SuperSecure123`n- oc create configmap app-config --from-file=app.properties`n- oc set env deployment/nginx-cert --from=secret/db-credentials`n- oc set volume deployment/nginx-cert --add --name=config-volume --type=configmap --configmap-name=app-config --mount-path=/etc/config`n
## 3. Pregunta Tipo Examen EX180
**Escenario:** Inyectar credenciales de BD y un archivo pp.properties sin exponer datos sensibles en texto plano en los manifiestos YAML.

**Solución Correcta:**
Crear un Secret para credenciales, un ConfigMap para el archivo pp.properties, inyectar el Secret con oc set env y montar el ConfigMap con oc set volume.

**Análisis de Opciones:**
- **A) Hardcode en YAML + PVC:** INCORRECTA. Expone datos sensibles y malgasta almacenamiento.
- **B) ConfigMap para claves y Secret para propiedades:** INCORRECTA. Invierte los conceptos de seguridad.
- **C) Secret para credenciales + ConfigMap montado:** CORRECTA. Cumple estándares de seguridad.
- **D) Recompilar imagen con COPY:** INCORRECTA. Viola el principio de inmutabilidad del contenedor.
