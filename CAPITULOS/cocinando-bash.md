[+ Volver al índice](../INDICE.md)

---

# Comandos Bash: Una Receta de Cheesecake 🍰

*Porque aprender bash es como cocinar: al principio quemás todo, pero después sale rico*

## 📋 Comandos que vas a aprender hoy:

- `pwd` - ¿Dónde estoy parado?
- `ls` - ¿Qué hay acá?
- `cd` - Moverse por directorios
- `mkdir` - Crear directorios
- `touch` - Crear archivos vacíos
- `nano/vim` - Editar archivos
- `cat` - Ver contenido completo
- `head/tail` - Ver principio/final
- `cp` - Copiar archivos
- `mv` - Mover/renombrar
- `rm` - Eliminar (¡CUIDADO!)
- `grep` - Buscar texto
- `find` - Buscar archivos
- `history` - Ver comandos anteriores

---

## Tu Cocina es la Terminal

Imaginate que la terminal es tu cocina. Tenés que moverte por ella, encontrar ingredientes, y hacer tu cheesecake paso a paso.

### `pwd` - "¿Dónde estoy parado?"

```bash
pwd
# /home/chef/cocina
```

Es como preguntarte: "¿En qué parte de la cocina estoy?" 
- ¿Estoy en la heladera? 
- ¿En la alacena? 
- ¿En la mesada?

**Siempre sabé dónde estás parado antes de hacer algo.**

### `ls` - "¿Qué hay acá?"

```bash
ls
# moldes/  ingredientes/  utensilios/  recetas.txt

ls -la
# -rw-r--r-- 1 chef chef 1024 Oct 10 14:30 recetas.txt
# drwxr-xr-x 2 chef chef  256 Oct 10 13:45 ingredientes/
```

Como abrir la alacena y ver qué tenés:
- `ls` = "¿Qué hay en esta estantería?"
- `ls -la` = "Mostrame TODO, hasta las cosas vencidas que están escondidas atrás"

### `cd` - "Moverse por la cocina"

```bash
# Ir a buscar ingredientes
cd ingredientes/
pwd
# /home/chef/cocina/ingredientes

# Volver a la cocina principal  
cd ..
pwd
# /home/chef/cocina

# Ir directo a los moldes
cd moldes/
```

Como caminar por la cocina:
- `cd ingredientes/` = ir hasta la heladera
- `cd ..` = volver donde estabas antes
- `cd` (solo) = volver a la cocina principal

### `mkdir` - "Organizar el espacio"

```bash
# Crear un lugar para el cheesecake de hoy
mkdir cheesecake_domingo

# Crear varios espacios de una
mkdir postres/tartas postres/tortas postres/helados
```

Como sacar bowls y organizarte antes de cocinar. Si no tenés dónde poner las cosas, se te va a desordenar todo.

### `touch` - "Anotar la receta"

```bash
# Crear la receta nueva
touch receta_cheesecake.txt

# Crear varios archivos de una
touch ingredientes.txt pasos.txt tiempos.txt
```

Es como agarrar una hoja en blanco y escribir "RECETA DE CHEESECAKE" arriba. Todavía no tiene nada, pero ya existe.

### `nano` / `vim` - "Escribir la receta"

```bash
# Editar la receta
nano receta_cheesecake.txt
```

Como sentarte a escribir los ingredientes y pasos en tu cuaderno de recetas. Acá es donde pones toda la información.

### `cat` - "Leer la receta"

```bash
# Ver qué dice la receta
cat receta_cheesecake.txt

# Ingredientes:
# - 200g galletitas
# - 100g manteca
# - 500g queso crema
# - 3 huevos
```

Es como agarrar tu cuaderno y leer en voz alta toda la receta de una vez.

### `head` / `tail` - "Ver pedacitos de la receta"

```bash
# Ver solo los primeros ingredientes
head -5 receta_cheesecake.txt

# Ver solo los últimos pasos
tail -3 receta_cheesecake.txt
```

- `head` = "Mostrame solo los primeros ingredientes, no me leas toda la receta"
- `tail` = "Saltate todo y decime solo cómo termina"

### `cp` - "Hacer una copia de la receta"

```bash
# Hacer una copia por las dudas
cp receta_cheesecake.txt receta_cheesecake_backup.txt

# Copiar a otra carpeta
cp receta_cheesecake.txt postres/
```

Como cuando encontrás una receta increíble y la fotocopiás antes de que se manche o se rompa. Siempre tené backup de las cosas importantes.

### `mv` - "Cambiar nombre o mover cosas"

```bash
# Cambiar el nombre
mv receta_cheesecake.txt mi_super_cheesecake.txt

# Mover a otra carpeta
mv mi_super_cheesecake.txt recetas/postres/
```

Es como:
- Cambiar "Receta 1" por "El Cheesecake de la Abuela"
- O mover tu receta del cajón de la cocina al libro de recetas

### `rm` - "Tirar a la basura" ⚠️

```bash
# Borrar un archivo (¡CUIDADO!)
rm receta_mala.txt

# Borrar una carpeta completa
rm -rf experimentos_fallidos/
```

**¡PELIGRO!** Es como tirar algo a la basura. Una vez que lo hacés, no hay vuelta atrás. El `rm -rf` es como tirar toda una bolsa de basura - borra TODO lo que hay adentro.

### `grep` - "Buscar en la receta"

```bash
# Buscar dónde dice "huevos"
grep "huevos" receta_cheesecake.txt
# - 3 huevos

# Buscar en todas las recetas
grep "chocolate" *.txt
```

Como usar Ctrl+F en la vida real. "¿En qué parte de esta receta mencioné los huevos?"

### `find` - "¿Dónde dejé esa receta?"

```bash
# Buscar todas las recetas de cheesecake
find . -name "*cheesecake*"

# Buscar todos los archivos de texto
find . -name "*.txt"
```

Como cuando no te acordás dónde pusiste esa receta increíble que probaste la semana pasada. "Buscar todo lo que tenga 'cheesecake' en el nombre."

### `history` - "¿Qué hice antes?"

```bash
history
# 1  cd cocina/
# 2  ls
# 3  mkdir cheesecake_domingo
# 4  nano receta_cheesecake.txt
```

Como el historial de tu navegador, pero de la cocina. "¿Qué fue lo último que hice? ¿Ya agregué la vainilla?"

## La Receta Completa: Hacer un Cheesecake

```bash
# 1. Organizarse
pwd                          # ¿Dónde estoy?
mkdir cheesecake_hoy         # Preparar el espacio
cd cheesecake_hoy           # Ir al espacio de trabajo

# 2. Preparar la receta
touch receta.txt            # Crear la hoja
nano receta.txt             # Escribir ingredientes y pasos

# 3. Verificar que esté todo
cat receta.txt              # Leer toda la receta
ls                          # Ver qué archivos tengo

# 4. Hacer backup
cp receta.txt ../recetas/   # Guardar una copia

# 5. Si algo sale mal...
rm intento_fallido.txt      # Borrar el desastre
cd ..                       # Volver y empezar de nuevo
```

## Los Errores Más Comunes (y sus Equivalentes en Cocina)

### "No such file or directory"
```bash
cat receta_que_no_existe.txt
# cat: receta_que_no_existe.txt: No such file or directory
```
**Traducción:** "Esa receta no existe" - como buscar sal en el azucarero.

### "Permission denied"
```bash
rm /recetas_de_la_abuela/secretas.txt
# rm: cannot remove '/recetas_de_la_abuela/secretas.txt': Permission denied
```
**Traducción:** "No podés tocar eso" - como intentar usar la sartén especial de tu mamá.

### Escribir mal el comando
```bash
sl
# bash: sl: command not found
```
**Traducción:** Escribiste `sl` en lugar de `ls`. Es como confundir sal con azúcar - pasa, pero el resultado no es el esperado.

## Consejos de Supervivencia

1. **Siempre `pwd` antes de hacer algo destructivo** - sabé dónde estás parado
2. **`ls` es tu mejor amigo** - mirá antes de actuar
3. **Hacé `cp` de cosas importantes** - backup, backup, backup
4. **`rm` no tiene deshacer** - pensá dos veces antes de borrar
5. **Usá `history`** - para recordar qué hiciste que funcionó

## Moraleja

Bash es como cocinar:
- Al principio te perdés en la cocina (`pwd`, `ls`)
- Después aprendés a organizarte (`mkdir`, `cd`)
- Empezás a crear cosas (`touch`, `nano`)
- Y con práctica, hacés cosas increíbles

La diferencia es que en bash, si la cagás, no se quema la cocina... solo tu paciencia 😅

---

*¡Que disfrutes cocinando con bash! Y recordá: la práctica hace al maestro... chef... programador... ¡lo que sea! 🍰👨‍💻*

**PD:** Si tu cheesecake sale mal, siempre podés `rm -rf cheesecake_desastre/` y empezar de nuevo. En la vida real no es tan fácil... 😉

---

[+ Volver al índice](../INDICE.md)