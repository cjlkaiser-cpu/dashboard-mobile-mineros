# minerOS Dashboard Mobile v1.2

Dashboard móvil PWA para consulta rápida de proyectos, conocimiento técnico y capturas de ideas. Hub de conocimiento conectado con DirectOS.

## Características

- **Mobile-first**: Diseñado para iPhone SE (375px) y superior
- **PWA instalable**: Funciona offline, añadir a pantalla de inicio
- **Un solo archivo**: KISS - HTML+CSS+JS en `index.html`
- **LocalStorage**: Persistencia sin backend
- **Sync DirectOS**: Conecta con tu knowledge base desde cualquier dispositivo

### Funcionalidades v1.2

| Feature | Descripción |
|---------|-------------|
| **Proyectos** | Vista filtrable por estado + bocetos |
| **Capturas** | Ideas, dudas, bugs con markdown y prioridades |
| **Stack** | Tools, Patterns, Flows con modales de detalle |
| **Búsqueda** | Búsqueda global en header |
| **Smart Links** | URLs detectadas con iconos (GitHub, YouTube, etc.) |
| **Bocetos** | Crear y promocionar a proyectos DirectOS |
| **Swipe** | Deslizar para borrar (estilo Gmail) |
| **Backup** | Export/Import JSON de datos |
| **API** | Sync con DirectOS multi-dispositivo |

## Uso

### Opción 1: Abrir directamente
```bash
open index.html
```

### Opción 2: Servidor local (para PWA y móvil)
```bash
cd /Users/carlos/Desktop/dashboard-mobile-mineros
python3 -m http.server 8081

# Abrir en móvil: http://TU_IP:8081
```

### Instalar como PWA
- **iPhone Safari**: Compartir → "Añadir a pantalla de inicio"
- **Android Chrome**: Menú → "Instalar app"

## Conexión con DirectOS

Para sincronizar desde móvil, DirectOS debe escuchar en todas las IPs:

```bash
cd ~/Desktop/DirectOS/backend
source ../venv/bin/activate
uvicorn main:app --host 0.0.0.0 --port 8000
```

El dashboard detecta automáticamente la IP y conecta:
- Desde Mac: `localhost:8081` → conecta a `localhost:8000`
- Desde móvil: `192.168.x.x:8081` → conecta a `192.168.x.x:8000`

## Stack

- HTML5 + CSS3 + JavaScript ES6+
- LocalStorage para persistencia
- Service Worker para offline
- Web Manifest para PWA
- Fetch API para DirectOS

## Estructura

```
dashboard-mobile-mineros/
├── index.html          # App completa (~3500 líneas)
├── manifest.json       # Config PWA
├── sw.js              # Service Worker v1.2
├── README.md          # Este archivo
├── MEJORAS.md         # Historial de desarrollo (8 fases)
└── icons/
    ├── icon.svg       # Icono base
    └── generate-icons.html
```

## Historial de Versiones

| Versión | Contenido |
|---------|-----------|
| v1.0 | Fases 1-6: Core + PWA + API básica |
| v1.1 | Fase 7: Hub de Conocimiento |
| v1.2 | Fase 8: Smart Pasting + Búsqueda + Promoción bocetos |

Ver `MEJORAS.md` para el historial completo.

---

*minerOS Dashboard v1.2 - Noviembre 2025*
