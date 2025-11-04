# Generación de un conflicto en git y fichero .gitignore

## PRIMERA PARTE: GESTIÓN DE RAMAS Y CONFLICTOS

### 1. Creación del repositorio y la rama principal

Se comienza creando una nueva carpeta de proyecto y dentro de ella se inicializa un repositorio Git:

```bash
git init
````

Si la rama principal no se llama main, se renombra:

```bash
git branch -M main
```

A continuación, se crea un archivo index.html con la estructura básica de una página web:

```html
<!DOCTYPE html>
<html lang="es">
  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Mi Página</title>
  </head>
  <body>
  </body>
</html>
```

Se añaden y confirman los cambios iniciales:

```bash
git add index.html
git commit -m "Estructura HTML básica en main"
```

![alt text](<img/1.png>)

---

### 2. Creación de la rama rama-1 y avance con un commit

Creamos y cambiamos a la nueva rama:

```bash
git switch -c rama-1
```

En esta rama se modifica el contenido del `<body>` añadiendo un párrafo con el *nombre de pila*:

```html
<body>
  <p>Marco</p>
</body>
```

Después, se confirman los cambios:

```bash
git add index.html
git commit -m "Añadido el nombre en rama-1"
```

![alt text](<img/2.png>)

---

### 3. Volver a main y crear rama-2

Desde la rama principal:

```bash
git switch main
git switch -c rama-2
```

En esta nueva rama se añade un párrafo con el *apellido* en el mismo archivo index.html:

```html
<body>
  <p>Apellido</p>
</body>
```

Confirmamos el cambio:

```bash
git add index.html
git commit -m "Añadido apellido en rama-2"
```

![alt text](<img/3.png>)

---

### 4. Ver el estado del repositorio de forma gráfica y resumida

```bash
git log --oneline --graph --all
```

![alt text](<img/4.png>)

---

### 5. Fusión de ramas y generación del conflicto

Intentamos fusionar rama-2 en rama-1:

```bash
git switch rama-1
git merge rama-2
```

El conflicto se produce porque ambas ramas modifican la misma parte del `<body>` del archivo index.html.

![alt text](<img/5.png>)

En este punto el archivo se verá así:

```html
<body>
<<<<<<< HEAD
  <p>Marco</p>
=======
  <p>Apellido</p>
>>>>>>> rama-2
</body>
```

---

### 6. Resolución del conflicto

Para resolverlo, se edita el archivo eliminando las marcas `<<<<<<<`, `=======`, y `>>>>>>>`, dejando una versión final coherente:

```html
<body>
  <p>Marco</p>
  <p>Apellido</p>
</body>
```

Guardamos los cambios y confirmamos la resolución:

```bash
git add index.html
git commit -m "Conflicto resuelto entre rama-1 y rama-2"
```

![alt text](<img/6.png>)

---

### 7. Ver el estado del repositorio nuevamente

```bash
git log --oneline --graph --all
```

![alt text](<img/7.png>)

---

### 8. Fusión en la rama principal (Fast-Forward)

Volvemos a main y realizamos una fusión que, al tener relación de ancestro, será tipo *fast-forward*:

```bash
git switch main
git merge rama-1
```

![alt text](<img/8.png>)

---

### 9. Visualizar ramas fusionadas con main

```bash
git branch --merged
```

![alt text](<img/9.png>)

---

### 10. Avanzar un commit más en main

Realizamos un cambio adicional en main, por ejemplo, agregando un comentario en el HTML:

```html
<!-- Proyecto completado -->
```

```bash
git add index.html
git commit -m "Actualización final en main"
```

![alt text](<img/10.png>)

---

### 11. Eliminar ramas fusionadas

Finalmente, eliminamos las ramas ya fusionadas:

```bash
git branch -d rama-1
git branch -d rama-2
```

Y comprobamos que solo queda la rama principal:

```bash
git branch
```

![alt text](<img/11.png>)

---

## SEGUNDA PARTE: ARCHIVO .gitignore

En el repositorio de la unidad se crea un archivo .gitignore que excluya:

* Archivos con extensión .doc
* El directorio llamado prueba

Se puede generar de forma automática o escribirlo manualmente:

```bash
echo "*.doc" > .gitignore
echo "prueba/" >> .gitignore
```

El contenido final debe quedar así:

```bash
*.doc
prueba/
```

![alt text](<img/12.png>)