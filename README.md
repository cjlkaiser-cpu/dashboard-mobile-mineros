# minerOS Dashboard Mobile v1.0

Dashboard móvil PWA para consulta rápida de proyectos y capturas de ideas.

## Características

- **Mobile-first**: Diseñado para iPhone SE (375px) y superior
- **PWA instalable**: Funciona offline, añadir a pantalla de inicio
- **Un solo archivo**: KISS - HTML+CSS+JS en `index.html`
- **LocalStorage**: Persistencia sin backend

### Funcionalidades

| Feature | Descripción |
|---------|-------------|
| **Proyectos** | Vista de todos los proyectos con filtros por estado |
| **Capturas** | Ideas, dudas, bugs, TODOs con markdown y prioridades |
| **Timer** | Check-in de sesiones de trabajo con racha |
| **Swipe** | Deslizar para borrar (estilo Gmail) |
| **Backup** | Export/Import JSON de datos |
| **API** | Conexión opcional con DirectOS |

## Uso

### Opción 1: Abrir directamente
```bash
open index.html
```

### Opción 2: Servidor local (para PWA)
```bash
cd /Users/carlos/Desktop/dashboard-mobile-mineros
python3 -m http.server 8080
# Abrir en móvil: http://TU_IP:8080
```

### Instalar como PWA
- **iPhone Safari**: Compartir (⬆️) → "Añadir a pantalla de inicio"
- **Android Chrome**: Menú (⋮) → "Instalar app"

## Generar Iconos PWA

1. Abrir `icons/generate-icons.html` en navegador
2. Click "Download All Icons"
3. Guardar en carpeta `icons/`

## Conexión con DirectOS

Si DirectOS está corriendo en `localhost:8000`, el dashboard sincronizará proyectos automáticamente.

```bash
# Iniciar DirectOS
cd ~/Desktop/DirectOS && ./start.sh

# El dashboard detectará la API y mostrará "🟢 Online" en Stack
```

## Stack

- HTML5 + CSS3 + JavaScript ES6+
- LocalStorage para persistencia
- Service Worker para offline
- Web Manifest para PWA

## Estructura

```
dashboard-mobile-mineros/
├── index.html          # App completa
├── manifest.json       # Config PWA
├── sw.js              # Service Worker
├── README.md          # Este archivo
├── MEJORAS.md         # Historial de desarrollo
└── icons/
    ├── icon.svg       # Icono base
    └── generate-icons.html
```

## Desarrollo

Ver `MEJORAS.md` para el historial completo de las 6 fases de desarrollo.

---

*minerOS Dashboard v1.0 - Noviembre 2024*
