[+ Volver al índice](../INDICE.md)
#Tips para Linux::

---

- Si tu os es linux, hay varias mejoras que podes hacer para mejorar tu experiencia de usuario: cambiar la shell, instalar un emulador de terminal distinto al por defecto, istalar plugins, etc.
Estando en ubuntu, la shell por defecto es bash (bourne again shell), y la terminal es gnome terminal; se pueden cambiar por zsh y kitty, respectivamente.

- zsh: Zsh es una extension de sh (bourne shell), la expande las capacidaddes basicas que tenia esta. Tambien cuenta con una comunidad muy activa la cual tiene el 
nombre "oh-my-zsh" la cual mantiene y mejora constantemente zsh. Ohmyzsh permite al usuario instalar plugins como autocompletar, resaltado de syntaxis, integraciones con
docker, etc. Tambien ofrece temas (themes) para mejorar el aspecto visual de la sesion, añadiendo o quitando features.(https://ohmyz.sh/)

- kitty: kitty es un emulador de terminal, open source acelerado por gpu escrito en c y python. Incorpora muchas funcionalidades a la terminal, como por ejemplo la 
capacidad de renderizar imagenes directamente en la terminal, hypervinculos clickeables, renderizado por OpenGL y la capacidad de separar por pestañas en una misma
sesion. (https://sw.kovidgoyal.net/kitty/)


---

# Herramienta GitHub Desktop — Introducción completa (GUI para Git sin terminal)

**¿Qué es?**
GitHub Desktop es una aplicación de escritorio para usar **Git** y **GitHub** con interfaz gráfica.
Sirve para **clonar** repos, **crear ramas**, **committear**, **hacer push/pull**, **abrir Pull Requests**, **actualizar tu rama con `main`** y **resolver conflictos**, todo sin tocar la terminal.

---

## 1) Instalación y requisitos

* **Windows / macOS**: descargá el instalador desde la página oficial de GitHub Desktop.
* **Linux**: existe un port no oficial mantenido por la comunidad (buscá “GitHub Desktop Linux port”).
* Requiere tener **Git** instalado (el instalador lo incluye si no lo tenés) y una cuenta de **GitHub**.

**Primer inicio**

1. Abrí la app y **sign in** con tu cuenta de GitHub.
2. Configurá tu **nombre** y **email** (los que van en los commits).
3. Opcional: elegí tu **editor** por defecto (VS Code, etc.).

---

## 2) Primeros pasos

### Clonar un repositorio

* Menú **File → Clone repository…**
* Elegí de tu cuenta o pegá la **URL** del repo.
* Elegí la carpeta local donde se guardará.

### Crear una rama

* **Current Branch → New Branch…**
* Convención sugerida: `feat/...`, `fix/...`, `docs/...`.

### Hacer cambios y commitear

* Editá archivos en tu editor (la app muestra cambios en **Changes**).
* Escribí un **mensaje de commit** claro y tocá **Commit to `rama`**.

### Subir al remoto (push)

* Botón **Push origin** (arriba).
* Si tu rama no existe en remoto, la crea automáticamente.

### Abrir un Pull Request

* **Create Pull Request** abre el navegador con el PR listo para completar título, descripción y reviewers.

---

## 3) La interfaz (mapa rápido)

* **Current Repository** (arriba a la izquierda): elegís el repo.
* **Current Branch**: cambiar/crear ramas.
* **Fetch / Push / Pull** (arriba): sincronización con el remoto.
* **Changes / History** (columna izquierda): cambios sin commitear e historial.
* **Diff** (panel principal): qué cambió en cada archivo (podés seleccionar líneas/hunks para commits parciales).

---

## 4) Flujo de trabajo recomendado (día a día)

1. **Fetch origin** (traer novedades).
2. **New Branch** desde `main` (actualizado).
3. Cambios → **Commits chicos y descriptivos**.
4. **Push** para subir tu rama.
5. **Create Pull Request** para abrir la PR.
6. Si otro mergeó antes, **Update from main** (o **Rebase**) y resolvé conflictos.
7. **Push** → PR listo para merge.

> Tip: un **tema por PR**. Evitá mezclar cambios distintos.

---

## 5) Actualizar tu rama con `main`

### Opción A — **Merge** (simple y segura)

* Menú **Branch → Update from main**

  > Si no aparece: **Branch → Merge into current branch… → `main`**
* Si hay conflictos, resolvelos (ver sección 7).
* **Commit merge** → **Push**.

### Opción B — **Rebase** (historial más lineal)

* **Branch → Rebase current branch… → `main`**.
* Resolvé conflictos → **Continue rebase** hasta terminar.
* Al final, **Force push** (reescribe historial).

> Si el equipo no definió preferencia, empezá con **Merge**.

---

## 6) Acciones útiles (dónde encontrarlas)

| Acción                                    | Dónde / Cómo                                         |
| ----------------------------------------- | ---------------------------------------------------- |
| Traer lo último                           | **Fetch origin**                                     |
| Cambiar/crear rama                        | **Current Branch** → seleccionar / **New Branch…**   |
| Commit parcial (por líneas/hunks)         | En **Changes**, tildar/desmarcar bloques específicos |
| Descartar cambios                         | Click derecho → **Discard Changes**                  |
| Stash (guardar sin commitear)             | **Branch → Stash changes…** / **Pop Stash**          |
| Revertir un commit                        | **History** → click derecho → **Revert This Commit** |
| Deshacer último commit (mantener cambios) | **History** → **Undo** (sobre el último commit)      |
| Ignorar archivo (agrega a `.gitignore`)   | Click derecho sobre el archivo → **Ignore file**     |
| Abrir PR                                  | **Create Pull Request**                              |

---

## 7) Resolver conflictos (paso a paso, completo)

### 7.1 ¿Qué es un conflicto?

Ocurre cuando **dos cambios tocan la misma parte** de un archivo (o hay choques como *rename/rename* o *delete/modify*). Git no puede decidir por vos y te pide que elijas **qué contenido queda**.

Tipos comunes:

* **Contenido**: ambos modificaron **las mismas líneas**.
* **Add/Add**: dos personas crearon el **mismo archivo** con contenidos distintos.
* **Rename/Rename**: el archivo fue renombrado de formas distintas.
* **Delete/Modify**: una rama lo borró y la otra lo editó.

### 7.2 ¿Dónde lo ves en Desktop?

* Al hacer **Update from main** (merge) o **Rebase**, Desktop muestra un **banner** indicando conflictos y una **lista de archivos** afectados.
* Para cada archivo, tenés: **Open in Editor**, y a veces acciones rápidas **Use current change** / **Use incoming change**.

### 7.3 Resolver con acciones rápidas (casos simples)

* **Use current change** = quedarte con **tu** versión.
* **Use incoming change** = quedarte con la versión que viene de **`main`**.
* Útil cuando una de las dos versiones debe descartarse por completo.

### 7.4 Resolver en tu editor (control total)

Si necesitás **combinar** ambos cambios:

1. Abrí el archivo con **Open in Editor**.
2. Ubicá los **marcadores**:

   ```txt
   <<<<<<< HEAD
   (tu versión)
   =======
   (versión de main)
   >>>>>>> main
   ```
3. **Editá y combiná** lo necesario (podés mantener partes de ambas versiones).
4. **Eliminá** los marcadores `<<<<<<<`, `=======`, `>>>>>>>`.
5. **Guardá** el archivo.

Volvé a Desktop:

* Marcá el archivo como **Mark as resolved**.
* Repetí con **todos** los archivos en conflicto.

---

### 7.5 Finalizar según el flujo

* **Si estabas haciendo Merge**: tocá **Commit merge** y luego **Push**.
* **Si estabas haciendo Rebase**: tocá **Continue rebase** (puede pedirte resolver más commits); al terminar, **Force push**.

---

### 7.6 Ejemplos típicos

**A) `INDICE.md` (listas colaborativas) — conservar ambas entradas**

**Antes (conflicto):**

```md
<<<<<<< HEAD
- 11/09 - *santino-tdd-conceptual* → [📎 Abrir](CAPITULOS/santino-tdd-conceptual.md)
=======
- 11/09 - *agustin-aporte-k8s* → [📎 Abrir](CAPITULOS/agustin-aporte-k8s.md)
>>>>>>> main
```

**Después (resuelto):**

```md
- 11/09 - *agustin-aporte-k8s* → [📎 Abrir](CAPITULOS/agustin-aporte-k8s.md)
- 11/09 - *santino-tdd-conceptual* → [📎 Abrir](CAPITULOS/santino-tdd-conceptual.md)
```

> Elegí el criterio de orden (por fecha, alfabético, etc.) y sé consistente.

**B) Código (misma función tocada por ambos)**

* Leé ambas intenciones y **mezclá con cuidado**.
* **Compilá/corré tests** después de resolver.

**C) Archivos de configuración (JSON/YAML)**

* Revisá **comas finales**, **identación** y **validá** el formato (el editor suele marcar errores).

---

### 7.7 Botones de rescate

* **Abort merge / Abort rebase**: cancela el proceso y vuelve al estado previo.
* **Discard changes** (sobre un archivo): descarta tu edición si te equivocaste y querés empezar de nuevo.

---

### 7.8 Mini-checklist de resolución ✅

* [ ] Leí y entendí la intención de **ambas** versiones.
* [ ] Combiné/ordené y **saqué los marcadores**.
* [ ] **Mark as resolved** en todos los archivos.
* [ ] **Commit merge** / **Continue rebase** según el caso.
* [ ] **Push** (o **Force push** si fue rebase).

---

## 8) Buenas prácticas para evitar conflictos

* **Actualizá tu rama seguido** (*Update from main*).
* **Commits y PRs chicos** (un tema por PR).
* Evitá cambios masivos de **formato** mezclados con lógica (hacelos en PR aparte).
* En archivos compartidos (p. ej., `INDICE.md`), **agregá líneas nuevas**; no edites las existentes salvo que sea necesario.
* Acordá un **criterio de orden** para listas (fecha, alfabético).

---

## 9) Checklist de PR (rápido) ✅

* [ ] Rama creada desde **`main` actualizado**.
* [ ] Commits **atómicos** y mensajes claros.
* [ ] `INDICE.md` actualizado si agregaste un capítulo.
* [ ] Sin archivos temporales ni secretos (logs, `.env`, etc.).
* [ ] CI en verde (si aplica).

---

## 10) TL;DR

1. **Fetch origin** → **New Branch** → cambios → **Commit** → **Push** → **Create PR**.
2. Si alguien mergeó antes: **Update from main** (o **Rebase**) → **resolvé conflictos** → **Push** (o **Force push**).
3. En conflictos de índice/listas: **conservá ambas entradas** y **ordená**.

---

[+ Volver al índice](../INDICE.md)
