[+ Volver al índice](../INDICE.md)

---

# TDD (Test-Driven Development) — Explicación conceptual

**¿Qué es?**  
TDD es una técnica de desarrollo en la que **primero se diseña la prueba** y **después se escribe el código** que la hace pasar.  
Su premisa central: *“si no puedo describir claramente el comportamiento que espero, no debería implementar la solución todavía”*.  
El flujo se resume en **Rojo → Verde → Refactor**.

---

## Fundamento filosófico

- **Claridad antes que implementación**: al escribir la prueba primero, el equipo debe acordar *qué* debe ocurrir (comportamiento observable) antes de pensar en *cómo* implementarlo.  
- **Diseño guiado por ejemplos**: cada test es un **ejemplo ejecutable** de lo que el sistema debe hacer; por eso se habla de *specification by example*.  
- **Feedback continuo y seguro**: la suite de pruebas confirma rápidamente si un cambio rompe un comportamiento existente.  
- **Mantenibilidad como objetivo**: TDD no es solo “testear”, es **diseñar** con foco en cohesión, bajo acoplamiento y responsabilidad única.

---

## Las dos prácticas que componen TDD

1) **Test-First Development**  
   - Primero se escriben **pruebas unitarias** (y, cuando aplica, pruebas de integración de bajo costo) que definen la **característica**.  
   - Luego se implementa **solo el código necesario** para que esas pruebas pasen.  
   - Este enfoque **obliga a modularizar** y a dar **una sola responsabilidad** a clases/métodos, porque lo no esencial se vuelve difícil de justificar con tests.

2) **Refactoring**  
   - Con todos los tests en verde, se **reestructura el código** sin cambiar su comportamiento.  
   - Se mejoran nombres, se elimina duplicación, se simplifica la complejidad y se separan responsabilidades.  
   - El objetivo es **legibilidad, diseño limpio y mantenibilidad** a largo plazo.

---

## Ciclo TDD (Rojo → Verde → Refactor)

1. **Rojo**: escribir una prueba **nueva** que falla (define el comportamiento esperado).  
2. **Verde**: implementar **lo mínimo necesario** para que esa prueba pase.  
3. **Refactor**: mejorar el diseño con la seguridad que dan las pruebas en verde.  
> Se repite en pasos pequeños; cada iteración mueve el sistema un poquito hacia el objetivo.

---

## Beneficios (por qué TDD)

- **Diseño más claro**: los tests fuerzan a explicar el “qué” en términos concretos.  
- **Menos regresiones**: la suite actúa como red de contención ante cambios.  
- **Mejor arquitectura**: favorece componentes pequeños, con menos acoplamiento.  
- **Documentación viva**: los tests describen el comportamiento real del sistema.  
- **Feedback temprano**: errores conceptuales aparecen antes, cuando son baratos.

---

## Qué incluye (y qué no)

**Incluye**  
- Pruebas que verifican **comportamientos** relevantes de negocio.  
- Casos borde y reglas importantes.  
- Dependencias externas aisladas mediante **dobles de prueba** (stubs/mocks/fakes).

**No es**  
- “Escribir muchos tests después de implementar”.  
- “Buscar 100% de cobertura por sí misma”.  
- “Testear detalles internos inestables” o acoplarse a la UI/tiempos.

---

## Cuándo conviene usar TDD

- Funcionalidades con **reglas de negocio** claras o críticas.  
- Código que se **evolucionará** con frecuencia (refactors futuros).  
- Módulos que deben ser **confiables** (riesgo alto de regresión).  

**Puede no ser ideal** (o requiere adaptación) en:  
- Investigación/POCs muy exploratorios donde el objetivo aún no está claro.  
- Interfaces de usuario muy volátiles (conviene testear por capas, no la UI cruda).  
- Integraciones muy lentas/costosas (se usan dobles y pruebas de contrato).

---

## Malentendidos frecuentes

- **“TDD es escribir tests después”** → No: es **test-first**.  
- **“TDD frena la velocidad”** → Al principio puede parecer más lento, pero reduce retrabajo y regresiones, acelerando el flujo total.  
- **“Más cobertura = buen diseño”** → La cobertura ayuda, pero **lo importante es cubrir comportamientos** significativos.  
- **“Hay que mockear todo”** → Se mockea lo externo/caro; el dominio se prueba de forma **real**.

---

## Resumen en una frase

> **TDD es diseñar el software guiados por pruebas que expresan el comportamiento esperado, avanzando en ciclos pequeños que aseguran calidad y permiten refactorizar con confianza.**

---

[+ Volver al índice](../INDICE.md)