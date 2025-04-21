# **Ramas y Conflictos en Git**

## **¿Qué son las ramas?**

- Una rama es un espacio dentro del [[002 - Conceptos básicos sobre repositorios en Git|repositorio]] donde se almacenan archivos y cambios.
- Por defecto, la rama principal de [[002 - ¿Qué es Git?|Git]] se llama `master` o `main`.
- Se utilizan para que un desarrollador o equipo trabaje en un proyecto sin interferir con el conjunto de archivos originales.

### **Ventajas de trabajar con ramas:**

1. Permite trabajar de manera organizada y flexible.
2. Evita errores o pérdida de información en la rama principal.
3. Solo se incorporan los cambios a la rama principal cuando se verifica que funcionan correctamente.

## **Comandos para trabajar con ramas:**

|**Comando**|**Descripción**|
|---|---|
|`git branch`|Mostrar la lista de ramas existentes y la rama actual.|
|`git branch nombre`|Crear una nueva rama.|
|`git checkout -b branchNueva branchExistente`|Crear una rama nueva a partir de otra.|
|`git checkout nombre`|Cambiar de rama.|
|`git branch -d nombre`|Eliminar una rama.|
|`git branch -c nombreBranch nombreCopia`|Crear una copia de una rama.|
|`git diff branch1 branch2`|Ver las diferencias entre dos ramas.|
|`git merge branchOrigen branchDestino`|Unificar ramas. (Debe ejecutarse desde la rama que recibirá los cambios).|
