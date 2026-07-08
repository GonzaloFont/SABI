---
description: Criba compañías a partir de un export de SABI aplicando los criterios de inversión del fondo
argument-hint: [ruta-al-export-sabi]
---

Usa el skill `sabi-screening` para procesar el archivo de SABI indicado
en $ARGUMENTS (o pide al usuario que lo suba/indique la ruta si no se
proporciona ninguno).

Antes de ejecutar el cribado:
1. Confirma con el usuario los criterios de inversión si no los ha dado
   ya en esta conversación (facturación, EBITDA/margen, sector, geografía,
   exclusiones).
2. Muestra un plan breve de qué vas a hacer antes de generar el archivo
   final.

Después, sigue el proceso completo descrito en el skill `sabi-screening`
y entrega el Excel con el scorecard.