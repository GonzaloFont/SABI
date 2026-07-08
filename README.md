# pe-fund-tools

Marketplace personal/interno de plugins para Claude Cowork, empezando con
el plugin de cribado de compañías SABI para Private Equity.

## Estructura

```
pe-fund-tools/
├── .claude-plugin/
│   └── marketplace.json        ← catálogo del marketplace
└── plugins/
    └── sabi-screening/
        ├── .claude-plugin/plugin.json
        ├── skills/sabi-screening/SKILL.md
        ├── commands/sabi-screen.md
        └── README.md
```

## Cómo lo usa Claude Cowork

1. En Cowork, abre **Personalizar → Plugins**
2. Click en **"+"** → **"Add marketplace"** → pega la URL de este
   repositorio de GitHub (ej. `https://github.com/tu-usuario/pe-fund-tools`)
   o el formato corto `tu-usuario/pe-fund-tools`
3. Click en **"Sincronizar"**
4. Verás el plugin **sabi-screening** disponible para instalar
5. Instálalo y ya puedes usar `/sabi-screen` o dejar que se active
   automáticamente al subir un export de SABI

## Añadir más plugins al marketplace

1. Crea una nueva carpeta en `plugins/tu-nuevo-plugin/`
2. Añade su `.claude-plugin/plugin.json`, `skills/`, `commands/`, etc.
3. Añade una entrada nueva al array `plugins` en
   `.claude-plugin/marketplace.json`
4. Haz commit y push — Cowork podrá sincronizar los cambios con el botón
   "Actualizar" en el marketplace
