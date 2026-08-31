# Módulo 3: Redes, Servicios y Rutas TLS (Edge, Passthrough, Re-encrypt)

## 1. Conceptos Clave
- **Service (ClusterIP):** IP virtual interna estable para balancear tráfico L4 entre Pods.
- **Route Edge:** Cifra HTTPS cliente-router. El Ingress Router descifra y envía HTTP plano al Pod.
- **Route Passthrough:** El router reenvía el tráfico SSL/TLS intacto directamente al Pod.
- **Route Re-encrypt:** Cifra cliente-router, el router descifra y vuelve a cifrar con otro certificado hacia el Pod.

> Nota: Consulta el archivo DIAGRAMA.md en esta carpeta para ver la terminación TLS Edge.

## 2. Comandos de Examen Esenciales
- oc create route edge secure-route --service=secure-app --cert=tls.crt --key=tls.key`n- oc create route passthrough pass-route --service=secure-app`n- oc get route secure-route -o yaml`n
## 3. Pregunta Tipo Examen EX180
**Escenario:** Cifrar conexión externa HTTPS pero enviar HTTP plano al Pod interno para no sobrecargar de procesamiento criptográfico al contenedor.

**Solución Correcta:**
oc create route edge secure-route --service=secure-app --cert=tls.crt --key=tls.key`n
**Análisis de Opciones:**
- **A) Route Passthrough:** INCORRECTA. Obliga al Pod a procesar TLS.
- **B) Route Edge:** CORRECTA. Descarga la tarea criptográfica en el Ingress Router.
- **C) oc expose --enable-tls:** INCORRECTA. El flag --enable-tls no existe en oc expose.
- **D) Route Re-encrypt:** INCORRECTA. Mantendría tráfico cifrado en la red interna.
