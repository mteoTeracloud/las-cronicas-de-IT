[+ Volver al índice](../INDICE.md)

---
# Cheatsheet Git: Stash + Diferencia entre Merge y Rebase

---

## Git Stash

El comando `git stash` permite **guardar temporalmente los cambios no confirmados**  
para poder cambiar de rama o actualizar el repo sin perder nada.

- `git stash` → guarda cambios actuales.
- `git stash list` → muestra las pilas de cambios guardadas.
- `git stash apply` → recupera el stash mas reciente.
- `git stash drop` → borra un stash especifico.
- `git stash pop` → aplica y elimina el ultimo stash en una sola accion.

**Cuando usarlo**:  
Cuando estas en medio de un trabajo, pero necesitas cambiar de rama o actualizar el repo y no queres hacer commit todavia.

---

## Merge vs Rebase

Cuando queres traer cambios de `main` a tu rama, podes hacerlo de dos formas: **merge** o **rebase**.  
Ambos actualizan tu rama, pero lo hacen de distinta manera.

### Merge

- Une dos ramas en un **nuevo commit de merge**.
- Mantiene el historial tal cual (con bifurcaciones).

**Ventajas**
- Historial fiel a la realidad.

**Desventajas**
- Puede ensuciar el historial con muchos commits de merge.

### Rebase

- Reescribe la historia moviendo tus commits para que queden encima de la rama destino.
- El historial queda lineal y mas limpio.

**Ventajas**
- Historial ordenado y facil de leer.

**Desventajas**
- Reescribe commits → no usar en ramas compartidas porque puede romper el trabajo de otros.

---

> **Regla practica:**

> - Trabajo en equipo → usar **merge**.
> - Mantener tu rama limpia antes de abrir un PR → usar **rebase**.
