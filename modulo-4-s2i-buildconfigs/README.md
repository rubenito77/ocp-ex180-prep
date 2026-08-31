# Módulo 4: Source-to-Image (S2I) y BuildConfigs

## Conceptos
- **S2I (Source-to-Image):** Construcción de imágenes combinando Código Git + Builder Image.
- **BuildConfig (BC):** Definición declarativa de la receta de construcción.

## Comando de Examen
`oc new-app openshift/nodejs:20-ubi8~https://github.com/sclorg/nodejs-ex.git --name=nodejs-s2i`
