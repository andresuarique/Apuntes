
## Trabajar con repositorios remotos  
1. **Enlazar un repositorio local con un repositorio remoto**:  
```

git remote add origin "url"

```
- Esto configura la URL del [[002 - Conceptos básicos sobre repositorios en Git|repositorio]] remoto con el que queremos sincronizar.  

2. **Enviar los cambios al repositorio remoto**:  
```

git push origin main

```
- Este comando sube los cambios confirmados en el [[008 - Ramas Git|branch]] local `main` al repositorio remoto.  