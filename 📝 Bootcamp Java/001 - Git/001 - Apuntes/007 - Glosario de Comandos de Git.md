# Glosario de Comandos de Git

## **Ayuda**

- **General**:

```
git help
```

- **Comando específico**:

```
git help add
git help commit
git help <comando>
```

## **Configuración del usuario**

- Establecer nombre y correo:

```
git config --global user.name "nombre de usuario"
git config --global user.email "email@email.com"
```

- Eliminar configuraciones:

```
git config --global --unset user.name
git config --global --unset user.email
```

- Ver la configuración actual:

```
git config --list
```

## **Repositorio**

- Crear un repositorio local:

```
git init
```

- Verificar el estado:

```
git status
```

## **Stage y Commit**

- Añadir archivos al _stage_:

```
git add archivo.txt# Archivo específico
git add .  # Todos los archivos
```

- Confirmar los cambios (_commit_):

```
git commit -m "mensaje"
```

- Ver el historial:

```
git log # Todo el historial
git log -- archivo.txt  # Historial de un archivo
git log --author=usuario# Cambios de un autor
```

## **Deshacer operaciones**

- Cambios locales no añadidos al stage:

```
git checkout -- archivo
```

- Cambios en el _stage_:

```
git reset HEAD archivo
```

## **Repositorio remoto**

- Ver los [[003 - Conceptos básicos sobre repositorios en Git|repositorios]] remotos:

```
git remote  
git remote -v  
```

- Enlazar un repositorio local a un remoto:

```
git remote add origin "url_del_repositorio"
```

- Ver detalles del remoto:

```
git remote show origin
```

- Renombrar o desvincular un remoto:

```
git remote rename origin nuevo_nombre  
git remote rm nombre_remoto  
```

- Subir cambios al remoto:

```
git push origin main
```

- Actualizar el repositorio local:

```
git pull  
git fetch  
```

- Clonar un repositorio remoto:

```
git clone "url_del_repositorio"
```

## **Branches**

- Crear y cambiar de _branch_:

```
git branch nuevaBranch_nombre  # Crear branch  
git checkout nuevaBranch_nombre# Cambiar a branch  
git checkout -b nuevaBranch_nombre # Crear y cambiar a branch  
```

- Volver a la rama principal:

```
git checkout master
```

- Fusionar (_merge_):

```
git merge nuevaBranch_nombre
```

- Listar _branches_:

```
git branch # Listar todas  
git branch -v  # Ver últimos commits  
git branch --merged# Ver fusionadas  
git branch --no-merged # Ver no fusionadas  
```

- Eliminar una _branch_:

```
git branch -d nombre_branch  
```

- Subir una _branch_ al remoto:

```
git push origin nombreBranch
```

- Resolver conflictos en un _merge_:

```
git merge --abort  
git reset --merge  
```

- Volver a un commit anterior:

```
git reset HEAD~n   # n es el número de commits atrás  
```

## **Reescribiendo el historial**

- Cambiar mensaje de un _commit_:

```
git commit --amend -m "Nuevo mensaje"
```

