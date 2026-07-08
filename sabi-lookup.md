---
description: Busca en vivo en SABI los datos financieros de una o varias compañías (ventas, EBITDA, empleados, etc.)
argument-hint: [nombre o NIF de la(s) empresa(s)]
---

Usa el skill `sabi-lookup` para buscar en SABI, vía navegador, los datos
de las empresas indicadas en $ARGUMENTS.

Antes de empezar:
1. Si no hay empresas especificadas en $ARGUMENTS, pregunta al usuario
   qué empresas y qué datos concretos necesita (ventas, EBITDA, etc. —
   si no lo dice, usa el set por defecto del skill).
2. Comprueba si hay sesión iniciada en SABI en el navegador. Si no,
   pide al usuario que inicie sesión antes de continuar.

Después, sigue el proceso completo del skill `sabi-lookup` y entrega los
resultados en tabla o Excel según el volumen de empresas.
