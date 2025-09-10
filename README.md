# 📖 Las Crónicas de IT

Bienvenidos al repo oficial de nuestro curso.  
Acá no solo vamos a practicar Git, sino que también vamos a escribir las **Crónicas de IT**:  
una mezcla épica de infraestructura, datos, anécdotas familiares y errores que nadie quiere admitir pero todos cometemos.  

---

## 🌌 Archivos centrales

### 1. INDICE.md
La línea temporal de nuestra saga.  
Cada alumno agrega info sobre una historia, evento gracioso o info tecnica que pueda ser interesante para el curso relacionada con el curso.  

Ejemplos:
1 - Aparece el bug inmortal en la base de datos.
2 - Primer programador que se casa con un script de Bash.
3 - Terraform conquista el mundo y nombra a un S3 bucket como presidente.

> ⚠️ **Nota importante**  
> Este archivo existe, en gran parte, para obligarlos a **toquetear todos el mismo archivo** y que se generen conflictos de Git.  
> Sí, lo hicimos a propósito 😈.  
> La idea es que aprendan a resolverlos y agarren práctica. 💥

---

### 2. INDICE.md
El índice de capítulos de las Crónicas.  
Acá entra TODO: desde cheatsheets útiles hasta relatos absurdos.  

Ejemplos de capítulos:
- **Cheatsheet Git** (para sobrevivir a los `push --force`)  
- **Anécdota de mi primo** (borró toda la historia con un rebase)  
- **Relato de mi tío** (su empresa todavía usa Excel como base de datos… y funciona)  
- **Poemas sobre Logs** (spoiler: nunca hay final feliz)  
- **Filosofía de Servidores** (“si un server cae y no hay nadie mirando, ¿crashea igual?”)  

Cada capítulo debe tener su propio archivo profundizando en `CAPITULOS/`.

---

## ✍️ Qué podés subir
No todo tiene que ser serio. Podés aportar:  
- Una guía rápida o cheatsheet.  
- Una anécdota graciosa de Infra o Data.  
- Una reflexión poética sobre deploys, backups o ETLs.  
- O un invento surrealista como *El Gremlin del FTP*.  

Lo importante es que quede en **Markdown** y aparezca en la cronología o el índice.  

---

## 📂 Estructura del repo

├─ INDICE.md # Índice de capítulos serios/absurdos
├─ CAPITULOS/ # Capítulos individuales en Markdown
│ ├─ cheatsheet-git.md
│ ├─ anecdota-primo.md
│ └─ relato-tio.md
└─ README.md # Este archivo

---

## 📜 Reglas mínimas
- Todo en **Markdown** (porque el TXT es del 2005).  
- Cada aporte debe aparecer en **al menos un archivo central** (`CRONOLOGIA.md` o `INDICE.md`).  
- Si el contenido es útil, buenísimo. Si no lo es… igual suma, porque al menos nos reímos.  
- Lo importante es **romperse un poquito con Git** y aprender.  
- ⚠️ **Todos los cambios deben subirse mediante Pull Requests (PRs).**  
  - Nada de commits directos a `main`.  
  - Creá tu rama (`feat/mi-historia`, `story/mi-anecdota`, etc.), hacé el cambio y abrí un PR.  
  - Solo se mergearán PRs que cumplan **todas estas reglas**.  
  - Tus compañeros (o el profe) revisarán el PR antes del merge.

---

⚡ **Objetivo de la semana (y quizas del repo)**  
Compartí un pensamiento asociado a lo visto en clase.    
Lo importante no es la seriedad del aporte, sino que **uses Git y no rompas todo (o sí, para aprender)**.

