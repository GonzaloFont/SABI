# sabi-tools

Plugin de Claude Cowork con dos formas de trabajar con datos de SABI
(Informa/Bureau van Dijk) para un fondo de Private Equity.

SABI no tiene conector MCP oficial en Cowork, así que este plugin cubre
las dos vías disponibles:

## Skills incluidas

### 1. `sabi-lookup` — Búsqueda en vivo (navegador)
Cuando pides datos de una o varias empresas concretas ("búscame el EBITDA
de Empresa X"), Claude abre Chrome, navega a SABI, busca la empresa y
extrae los datos directamente de la ficha.

**Requisito:** debes tener sesión iniciada en SABI en el navegador donde
corre la extensión de Claude in Chrome. La URL de acceso ya está fijada
en el skill. Claude nunca introduce usuario ni contraseña — si detecta
que no hay sesión, te pedirá que inicies sesión tú manualmente y
esperará confirmación.

Comando: `/sabi-lookup [nombre o NIF de la empresa]`

### 2. `sabi-screening` — Cribado por lote (archivo)
Cuando tienes un export de SABI en Excel/CSV con muchas empresas y quieres
aplicar los criterios de inversión del fondo (facturación, EBITDA, sector,
geografía), sube el archivo y usa este skill para generar un scorecard.

Comando: `/sabi-screen [ruta del archivo]`

## Instalación

1. Añade este repositorio como marketplace en Cowork:
   **Personalizar → Plugins → "+" → Add marketplace** → pega la URL de
   este repo de GitHub
2. Sincroniza y luego instala el plugin **sabi-tools**
3. Para `sabi-lookup`, asegúrate de tener **Claude in Chrome** conectado
   (Ajustes → Conectores) y haber iniciado sesión en SABI en esa pestaña

## Personalización

- Edita `skills/sabi-lookup/SKILL.md` si tu URL de acceso a SABI cambia,
  o para ajustar los campos por defecto a extraer
- Edita `skills/sabi-screening/SKILL.md` para fijar tus criterios de
  inversión por defecto (facturación, EBITDA, sector, geografía)