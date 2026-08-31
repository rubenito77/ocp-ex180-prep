# Módulo 3: Redes, Servicios y Rutas TLS (Edge, Passthrough, Re-encrypt)

## 1. Conceptos Clave de Arquitectura
- **Service (ClusterIP):** Asigna una IP virtual interna estable para balancear tráfico L4 entre Pods.
- **Route Edge:** Cifra HTTPS entre el cliente y el Ingress Router (HAProxy). El router descifra y envía HTTP plano al Pod.
- **Route Passthrough:** El router reenvía el tráfico SSL/TLS intacto al Pod. El Pod descifra la conexión.
- **Route Re-encrypt:** Cifra cliente-router, el router descifra y vuelve a cifrar con otro certificado hacia el Pod.

## 2. Diagrama de Integración Módulo 3 (Terminación Edge)
``n[ Cliente Web / HTTPS ] ---> [ OpenShift Ingress Router (HAProxy - Edge TLS) ] ---> [ Service (ClusterIP:8080) ] ---> [ Pod: secure-app ]
``n
## 3. Comandos de Examen Esenciales
- oc create route edge secure-route --service=secure-app --cert=tls.crt --key=tls.key
- oc create route passthrough pass-route --service=secure-app
- oc get route secure-route -o yaml

## 4. Pregunta Tipo Examen EX180
**Escenario:** Cifrar conexión externa HTTPS pero enviar HTTP plano al Pod interno para no sobrecargar de procesamiento criptográfico al contenedor.

**Solución Correcta:**
oc create route edge secure-route --service=secure-app --cert=tls.crt --key=tls.key

**Análisis de Opciones:**
- A) Route Passthrough: INCORRECTA. Obliga al Pod a procesar TLS.
- B) Route Edge: CORRECTA. Descarga la tarea criptográfica en el Ingress Router.
- C) oc expose --enable-tls: INCORRECTA. El flag --enable-tls no existe.
- D) Route Re-encrypt: INCORRECTA. Mantendría tráfico cifrado en la red interna.
