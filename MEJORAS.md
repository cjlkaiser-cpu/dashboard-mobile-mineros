# Plan de Mejoras - Dashboard Mobile minerOS

## Filosofía
- **Un solo archivo HTML** (KISS)
- **LocalStorage** como persistencia
- **Mobile-first** (375px iPhone SE)
- **Sin dependencias externas** (vanilla JS)

---

## ✅ FASE 1: Seguridad + Quick Wins - COMPLETADA

### 1.1 Sanitización XSS ✅
- Función `escapeHTML()` aplicada a todo contenido de usuario
- Seguro contra inyección de código

### 1.2 Sistema de Backup ✅
- Botón "Exportar" → descarga `mineros-backup-FECHA.json`
- Botón "Importar" → carga y merge con datos actuales
- Ubicación: Vista Stack

### 1.3 Filtrado de Proyectos ✅
- Pills: `Todos` | `Production` | `Prototype` | `Archived`

---

## ✅ FASE 2: Actividad Real - COMPLETADA

### 2.1 Check-in de Sesiones ✅
- Botón "Iniciar/Detener Sesión" en Home
- Timer visible en tiempo real
- Guarda duración en `activityLog[fecha]`
- Persiste si cierras navegador

### 2.2 Racha y Stats Reales ✅
- Racha calculada desde días consecutivos con actividad
- Minutos semanales reales
- Gráfica de últimos 14 días con datos reales

---

## ✅ FASE 3: UX Móvil - COMPLETADA

### 3.1 Swipe para Borrar ✅
- Swipe izquierda revela botón rojo
- Estilo Gmail/iOS
- Touch events nativos

### 3.2 Modal Zen Mode ✅
- `visualViewport` API detecta teclado virtual
- Oculta selectores cuando teclado abierto
- Scroll automático al textarea

### 3.3 Haptic Feedback ✅
- `navigator.vibrate()` en acciones clave
- Navegación, guardar, borrar, swipe

---

## ✅ FASE 4: Contenido Enriquecido - COMPLETADA

### 4.1 Markdown Básico ✅
- `**bold**` → negrita
- `*italic*` → cursiva
- `` `code` `` → código (verde monospace)
- `- item` → listas
- Aplicado DESPUÉS de sanitizar (seguro)

### 4.2 Selector de Proyecto ✅
- Dropdown en modal de captura
- Opción "Auto-detectar" por defecto
- Lista todos los proyectos

### 4.3 Prioridad en Capturas ✅
- 🟢 Baja (default)
- 🟡 Media
- 🔴 Alta
- Badge visible solo si Media/Alta

---

## ✅ FASE 5: PWA Instalable - COMPLETADA

### 5.1 manifest.json ✅
- Nombre, colores, display standalone
- Iconos en todos los tamaños

### 5.2 Service Worker ✅
- Cache-first con stale-while-revalidate
- Funciona offline después de primera visita
- Detecta actualizaciones

### 5.3 Iconos y Meta Tags ✅
- SVG base + generador de PNGs
- apple-touch-icon para iOS
- Meta tags completos

**Cómo instalar:**
```bash
cd /Users/carlos/Desktop/dashboard-mobile-mineros
python3 -m http.server 8080
# Abrir en móvil: http://TU_IP:8080
# Safari: Compartir → Añadir a pantalla de inicio
# Chrome: Menú → Instalar app
```

---

## ✅ FASE 6: Conexión DirectOS API - COMPLETADA (6.1)

### 6.1 Fetch Proyectos desde API ✅
- Conecta con DirectOS si está corriendo (localhost:8000)
- Fallback a datos locales si offline
- Indicador de estado en vista Stack
- Botón "Sincronizar" manual

### 6.2 Sincronizar Capturas (PENDIENTE)
**Requiere:** Añadir endpoint en DirectOS
```python
# backend/main.py
@app.post("/api/captures")
async def save_capture(capture: CaptureModel):
    # Guardar en SQLite/archivo
    pass

@app.get("/api/captures")
async def get_captures():
    # Retornar capturas guardadas
    pass
```

### 6.3 Actividad Git Real (PENDIENTE)
**Requiere:** Endpoint en DirectOS que ejecute git log
```python
@app.get("/api/projects/{id}/activity")
async def get_git_activity(id: str, days: int = 14):
    # subprocess.run(['git', 'log', ...])
    # Parsear y retornar commits por día
    pass
```

---

## Resumen Final

| Fase | Estado | Contenido |
|------|--------|-----------|
| **1** | ✅ | Seguridad XSS + Backup + Filtros |
| **2** | ✅ | Timer sesiones + Actividad real |
| **3** | ✅ | Swipe + Zen mode + Haptic |
| **4** | ✅ | Markdown + Proyecto + Prioridad |
| **5** | ✅ | PWA instalable + Offline |
| **6** | 🟡 | API DirectOS (6.1 ✅, 6.2-6.3 pendientes) |

---

## Archivos del Proyecto

```
dashboard-mobile-mineros/
├── index.html          # App completa (HTML+CSS+JS)
├── manifest.json       # Configuración PWA
├── sw.js              # Service Worker
├── MEJORAS.md         # Este archivo
└── icons/
    ├── icon.svg       # Icono vectorial base
    ├── generate-icons.html  # Herramienta para generar PNGs
    └── icon-*.png     # Iconos generados
```

---

## 📋 PRÓXIMAS MEJORAS (v1.1)

### 7.1 Heatmap de Actividad (Estilo GitHub) 🔥
**Problema:** El gráfico de barras actual ocupa mucho espacio vertical.
**Propuesta:**
- Cambiar barras por fila de "cuadraditos" (heatmap horizontal)
- Últimos 14 días en una línea compacta
- Verde oscuro = mucha actividad, verde claro = poca
- Más compacto y "hacker"
**Esfuerzo estimado:** 30 min

### 7.2 Smart Pasting 🧠
**Problema:** Los enlaces se ven como texto plano sin contexto.
**Propuesta:**
- Detectar URLs al guardar captura
- Si es GitHub: mostrar icono 🐙 + repo/issue
- Si es YouTube: mostrar icono ▶️ + extraer título
- Otros enlaces: icono 🔗 + dominio
- Regex para detectar: `https?://[^\s]+`
**Esfuerzo estimado:** 45 min

### 7.3 (Bonus) Búsqueda rápida 🔍
**Propuesta:** Barra de búsqueda en Home para filtrar proyectos y capturas
**Esfuerzo estimado:** 30 min

---

*"Piano piano se arriva lontano"* - ¡Todas las fases principales completadas! 🎉
