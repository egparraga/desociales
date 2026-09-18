# Cómo subir cambios de la web a producción

Guía rápida para cuando edites contenido en local y quieras que aparezca en https://desociales.es

## 0. Dónde está todo

- Carpeta del proyecto: `~/Datos/Nextcloud/desociales/desociales`
- El sitio se genera con Hugo y se publica solo mediante GitHub Pages: **cada vez que subes (push) cambios a la rama `main`, GitHub construye y publica la web automáticamente** (tarda 1-3 minutos). No hay que subir nada a mano por FTP ni nada parecido.

## 1. Moverte a la carpeta del proyecto

```
cd ~/Datos/Nextcloud/desociales/desociales
```

## 2. (Opcional pero recomendado) Previsualizar antes de subir

Para ver cómo queda antes de publicarlo:

```
hugo server -D
```

Abre `http://localhost:1313` en el navegador. Ctrl+C para parar el servidor cuando termines de revisar.

## 3. Ver qué has cambiado

```
git status
```

Te lista:
- **Archivos sin seguimiento** (nuevos, en rojo/sin marcar): contenido nuevo que aún no conoce git.
- **Cambios sin preparar**: archivos ya existentes que has modificado.

## 4. Añadir los cambios

Para añadir archivos o carpetas concretas (más seguro, evita subir cosas por error):

```
git add "content/nombre-carpeta"
git add "static/PDF/nombre-carpeta"
```

Si has revisado `git status` y quieres añadir *todo* lo que aparece:

```
git add -A
```

Vuelve a hacer `git status` para confirmar que lo que está en verde es justo lo que querías subir.

## 5. Crear el commit (guardar el cambio con un mensaje)

```
git commit -m "Descripción breve de lo que has añadido o cambiado"
```

Ejemplos de buenos mensajes:
- `Añadir contenido de 4º ESO Economía (tema 1)`
- `Corregir enlace roto en tema 2 de Geografía`
- `Actualizar imagen destacada de la guía de mapas`

## 6. Subir a GitHub (esto dispara la publicación)

```
git push origin main
```

Si todo va bien verás algo como `main -> main` al final. **A partir de aquí, GitHub construye y publica la web solo** — no hace falta hacer nada más.

> Nota sobre este repo en concreto: puede que veas un aviso de que "el repositorio se ha movido" a otra cuenta (`egparraga/desociales`). Es normal, GitHub redirige el push automáticamente y no falla. Si algún día ese aviso pasara a ser un error real, dímelo y lo revisamos.

## 7. Comprobar que se ha publicado

Espera 1-3 minutos y recarga https://desociales.es (o la página concreta que hayas tocado). Si quieres ver el progreso del despliegue en tiempo real: https://github.com/tecnoyonqui/desociales/actions

## Resumen ultra-rápido (cuando ya lo domines)

```
cd ~/Datos/Nextcloud/desociales/desociales
git add -A
git commit -m "mensaje descriptivo"
git push origin main
```

## Si algo sale mal

- **`git push` pide usuario/contraseña o falla por autenticación**: avísame, hay que revisar las credenciales guardadas.
- **La web no se actualiza tras varios minutos**: revisa la pestaña "Actions" del repo (enlace arriba) para ver si el build falló, y si falla, copia el error y lo revisamos juntas.
- **Te arrepientes de un `git add` antes de hacer commit**: `git restore --staged <archivo>` lo quita de la zona de "preparado" sin borrar el archivo.
