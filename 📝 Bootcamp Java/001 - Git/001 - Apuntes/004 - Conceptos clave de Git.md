# Conceptos clave de Git  

## **Stage**  
En [[002 - ¿Qué es Git?|Git]], el *stage* es un estado intermedio donde los archivos se preparan antes de ser confirmados definitivamente (versionados).  
- Es como un "punto de espera" donde los archivos pueden ser seleccionados o desechados antes del commit.  
- Para agregar archivos al stage:  
- `git add archivo.txt`: Agrega un archivo específico.  
- `git add .`: Agrega todos los archivos del proyecto.  

## Comandos importantes  
1. **Verificar el estado del repositorio**:  
```

git status

```
Este comando muestra:  
- Archivos que no están en *stage*.  
- Archivos que ya están en *stage*.  

2. **Confirmar los archivos en stage**:  
```

git commit -m "mensaje"

```
- `commit` guarda de forma definitiva los cambios seleccionados.  
- `-m` permite agregar un mensaje descriptivo.  
- Los *commits* funcionan como *backups* a los que podemos regresar fácilmente.  
