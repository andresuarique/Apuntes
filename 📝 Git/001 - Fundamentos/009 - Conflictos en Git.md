## **Conflictos en Git**

Un conflicto ocurre cuando:

1. Dos usuarios editan el mismo archivo en la misma línea de código.
2. Git no puede fusionar automáticamente las [[008 - Ramas Git|ramas]] debido a las diferencias encontradas.

### **Cómo evitar conflictos:**

- Dividir bien el trabajo para evitar que más de una persona edite el mismo archivo o sección de código.

## **Resolución de conflictos manualmente:**

1. **Al intentar un _merge_, [[002 - ¿Qué es Git?|Git]] muestra un mensaje de conflicto.**

2. **Buscar los marcadores de conflicto en el archivo afectado:**

- **Marcador inicial:**

```
<<<<<<<< HEAD
```

Contiene los cambios de la rama actual (HEAD).
- **Divisor:**

```
========
```

Separa los cambios de las ramas en conflicto.
- **Marcador final:**

```
>>>>>>>>
```

Contiene los cambios de la otra rama.
3. **Editar manualmente:**

- Decidir qué parte del código mantener o combinar las secciones necesarias.
- Eliminar los marcadores (`<<<<<<`, `=======`, `>>>>>>`).
4. **Finalizar el conflicto:**

- Una vez resuelto, añadir los cambios al _stage_:

```
git add archivo
```

- Confirmar los cambios:

```
git commit -m "Resolviendo conflictos"
```


## **Ejemplo de flujo con conflicto:**

1. Cambiar a la rama donde se realizará la fusión (_merge_):

```
git checkout branchDestino
```

2. Traer los datos de la rama que se quiere fusionar:

```
git pull origin branchOrigen
```

3. Realizar la fusión:

```
git merge branchOrigen
```

4. Resolver manualmente los conflictos si Git no los puede resolver automáticamente.

## **Notas importantes:**

- Git intenta resolver automáticamente las diferencias cuando es posible.
- Los conflictos manuales son comunes al trabajar en equipo, pero con una buena división de tareas se pueden minimizar.