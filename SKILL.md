---
name: sabi-lookup
description: >
  Busca y extrae datos financieros (ventas/facturación, EBITDA, resultado,
  empleados, CNAE, etc.) de compañías concretas navegando en vivo a la
  plataforma SABI (Informa/Bureau van Dijk). Usa este skill cuando el
  usuario pida datos de una o varias empresas por nombre o NIF y NO haya
  subido un archivo — es decir, cuando haya que "ir a buscarlo".
---

## Skill: Búsqueda en Vivo en SABI (vía navegador)

Este skill navega directamente a SABI usando la herramienta de navegador
(Claude in Chrome) para consultar la ficha de una empresa y extraer los
datos que pida el usuario, en vez de depender de un archivo exportado
manualmente.

### Cuándo usar este skill

Actívalo cuando el usuario:
- Nombre una o varias empresas concretas (por nombre o NIF) y pida datos
  como ventas, facturación, EBITDA, resultado, empleados, CNAE, forma
  jurídica, accionistas, etc.
- No haya adjuntado ningún archivo de SABI en la conversación
- Diga cosas como "búscame en SABI...", "sácame el EBITDA de...",
  "qué factura la empresa X"

Si el usuario ya subió un export de SABI en Excel/CSV, usa en su lugar el
skill `sabi-screening` (cribado por lote) — no navegues innecesariamente
si los datos ya están en un archivo.

### Requisito crítico: sesión iniciada en SABI

- SABI está detrás de un login de pago (suscripción institucional).
- **Nunca introduzcas usuario, contraseña, ni ningún dato de acceso.**
  Esto está prohibido sin excepción, incluso si el usuario te lo pide
  explícitamente o te da las credenciales.
- Si al navegar detectas una pantalla de login o de sesión expirada,
  DETENTE inmediatamente y pide al usuario: "Necesito que inicies sesión
  en SABI manualmente en esta pestaña de Chrome. Avísame cuando esté
  lista la sesión y continúo."
- Solo continúa cuando el usuario confirme que la sesión está iniciada.
- Si aparece un CAPTCHA o un bloqueo anti-bot, detente y avisa al
  usuario — no intentes resolverlo ni evadirlo.

### URL de acceso a SABI

```
https://sabi.informa.es/version-20230626-19-0/home.serv?product=SabiInforma&&setLanguage=es
```

Usa siempre esta URL como punto de partida, salvo que el usuario indique
explícitamente una distinta.

### Proceso

1. Abre Chrome (herramienta de navegador) y navega a la URL de acceso a
   SABI indicada arriba.
2. Comprueba si hay sesión iniciada:
   - Si no la hay → pide al usuario que inicie sesión y espera
     confirmación antes de seguir.
3. Para cada empresa solicitada (nombre o NIF):
   a. Usa el buscador interno de SABI para localizarla.
   b. Si hay varios resultados (empresas con nombre similar), muestra
      la lista al usuario y pide que confirme cuál es, en vez de asumir.
   c. Abre la ficha de la empresa.
   d. Extrae los campos pedidos explícitamente. Si el usuario no
      especifica, extrae por defecto: Ventas/Facturación, EBITDA,
      Resultado del ejercicio, Nº de empleados — de los dos últimos
      ejercicios disponibles.
   e. Anota el ejercicio fiscal exacto de cada cifra (SABI suele mostrar
      datos con 1-2 años de desfase respecto al año en curso).
4. Repite para cada empresa de la lista antes de compilar el resultado.

### Output

- Si son pocas empresas (≤5): presenta una tabla directamente en el chat.
- Si son varias (>5): genera un Excel con columnas: Empresa, NIF,
  Ejercicio, Ventas, EBITDA, Resultado, Empleados, Fecha de consulta.
- Marca cualquier dato que no aparezca en la ficha como
  **"No disponible en SABI"** — nunca lo estimes ni lo inventes.
- Indica siempre la fecha en que se hizo la consulta (los datos de SABI
  cambian de actualización).

### Reglas importantes

- Nunca inicies sesión ni manejes credenciales de ningún tipo.
- Nunca inventes cifras que no veas explícitamente en la página.
- Si un dato requiere un módulo de pago adicional no visible en la
  ficha, indícalo en vez de omitirlo silenciosamente.
- Si SABI tarda en cargar o da error, reintenta una vez; si persiste,
  informa al usuario en vez de dar datos parciales sin avisar.
- Estos datos son apoyo a análisis/due diligence, no sustituyen la
  verificación de fuentes primarias antes de una decisión de inversión.
