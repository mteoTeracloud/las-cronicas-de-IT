
---

# 🐧 Linux Cheatsheet

Guía rápida de comandos básicos y útiles de Linux, con ejemplos prácticos.

---

## 📂 Navegación de archivos y directorios

* **`pwd`** → muestra el directorio actual.

  ```bash
  pwd
  /home/usuario/proyectos
  ```

* **`ls`** → lista los archivos y directorios.

  * `ls -l` → lista con detalles (permisos, propietario, tamaño).
  * `ls -a` → incluye archivos ocultos.

* **`cd <directorio>`** → cambia de directorio.

  * `cd ..` → sube un nivel.
  * `cd ~` → va al home del usuario.

---

## 📄 Archivos y directorios

* **`touch archivo.txt`** → crea un archivo vacío.
* **`mkdir carpeta`** → crea un directorio.
* **`rm archivo.txt`** → elimina un archivo.
* **`rm -r carpeta/`** → elimina un directorio con todo su contenido.
* **`cp origen destino`** → copia un archivo.

  ```bash
  cp notas.txt copia_notas.txt
  ```
* **`mv origen destino`** → mueve o renombra un archivo.

  ```bash
  mv notas.txt /home/usuario/documentos/
  mv notas.txt notas_viejas.txt
  ```

---

## 🔑 Permisos de archivos

Cada archivo/directorio tiene permisos: **owner | group | others**.
Se ven con `ls -l`:

```bash
-rwxr-xr--  1 usuario grupo  512 sep  9 20:10 script.sh
```

* `r` → read (leer)
* `w` → write (escribir)
* `x` → execute (ejecutar)

Comandos para modificarlos:

* **`chmod 755 archivo`** → cambia permisos (ejecución + lectura).
* **`chown usuario:grupo archivo`** → cambia propietario.
* **`chgrp grupo archivo`** → cambia grupo.

---

## 📖 Visualización de archivos

* **`cat archivo.txt`** → muestra el contenido.

  * Si empieza con `-`: usar `cat ./-archivo`.
  * Con espacios: `cat "mi archivo.txt"` o `cat mi\ archivo.txt`.

* **`less archivo.txt`** → abre archivo con paginación.

* **`head archivo.txt`** → muestra primeras 10 líneas.

* **`tail archivo.txt`** → muestra últimas 10 líneas.

  * `tail -f log.txt` → sigue en tiempo real (útil para logs).

---

## 🔍 Búsqueda y filtrado

* **`find ruta -type f -name "*.txt"`** → busca archivos `.txt` en ruta.
* **`grep "texto" archivo.txt`** → busca líneas que contengan texto.

  * `grep -i` → ignora mayúsculas/minúsculas.
  * `grep -r "error" /var/log` → busca recursivamente en carpetas.
  * `grep -a` → trata archivos binarios como texto.
* **`sort archivo.txt`** → ordena líneas alfabéticamente.
* **`uniq -u archivo.txt`** → muestra solo líneas únicas.
* **`wc -l archivo.txt`** → cuenta las líneas del archivo.

---

## 🔗 Redirecciones y pipes

* **`>`** → redirige salida a un archivo (sobrescribe).

  ```bash
  echo "Hola mundo" > saludo.txt
  ```
* **`>>`** → agrega salida al final de un archivo.
* **`|`** → pipe: conecta la salida de un comando con la entrada de otro.

  ```bash
  cat archivo.txt | grep "error" | sort | uniq
  ```

---

## 🛠️ Otros útiles

* **`echo "texto"`** → imprime texto.
* **`history`** → muestra historial de comandos.
* **`man comando`** → abre el manual de un comando.

  ```bash
  man ls
  ```
* **`tldr comando`** → versión resumida de `man` con ejemplos prácticos.

---

