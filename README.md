# 🎵 SonicNodes — Visualización Interactiva del Universo Musical

![Version](https://img.shields.io/badge/version-4.5-blue.svg)
![License](https://img.shields.io/badge/license-MIT-green.svg)
![Status](https://img.shields.io/badge/status-active-brightgreen.svg)

## 👤 Autor
**Lester Fernandez**  
📧 Email: [fernandez.lester@gmail.com](mailto:fernandez.lester@gmail.com)  
🔗 GitHub: [@Retselfernandez](https://github.com/Retselfernandez)

---

## 📖 ¿Qué es SonicNodes?

**SonicNodes** es una aplicación web interactiva que visualiza las relaciones entre géneros musicales como un **grafo isomorfo dinámico**. Utiliza física de redes (force-directed graph) para crear constelaciones visuales donde cada nodo representa un género musical, y las conexiones muestran influencias y relaciones mutuas entre géneros.

La aplicación permite explorar la **arquitectura del universo musical moderno** con más de **90 géneros** organizados jerárquicamente y conectados a través de relaciones transversales (bridges) que representan fusiones musicales.

---

## 🎯 ¿Para qué se usa?

- **Educación Musical**: Comprender la evolución y las influencias entre géneros musicales
- **Exploración Interactiva**: Navegar el universo musical a través de tres niveles de profundidad
- **Análisis de Géneros**: Descubrir subgéneros y artistas relacionados dentro de cada categoría
- **Recomendación de Audio**: Escuchar previsualizaciones de iTunes directamente en la aplicación
- **Investigación de Tendencias**: Analizar géneros por región y período histórico

---

## ✨ Características Principales

### 🔍 Tres Niveles de Profundidad
1. **Macro** (21 géneros principales)
   - Rock, Electrónica, Hip Hop, Reggaeton, Afrobeats, Latina, Jazz, y más...
   
2. **Sub** (~90 nodos totales)
   - Subgéneros de cada categoría macro
   - Ejemplo: Rock → Rock Clásico, Rock Alternativo, Punk, Metal, Grunge, Indie Rock
   
3. **Artista** (Expansión de múltiples artistas)
   - Visualización de artistas relacionados por género
   - Integración con iTunes y Spotify

### 🎨 Visualización Avanzada
- **Modo Oscuro/Claro**: Tema adaptable con contraste optimizado
  - Líneas de conexión mejoradas en modo light (opacity: 0.22-0.28)
  - Glassmorphism UI con backdrop blur
  
- **Física de Redes**: Force-directed graph con simulación D3.js
  - Repulsión entre nodos para claridad visual
  - Atracción jerárquica entre macro-géneros y subgéneros
  - Puentes transversales entre géneros relacionados

- **Nodos Coloreados**: Cada género tiene un color distintivo
  - Fácil identificación visual
  - Paleta armónica de 21+ colores

### 🎧 Características Interactivas
- **Búsqueda en Tiempo Real**: Filtrar géneros y artistas
- **Audio Preview**: Escuchar previsualizaciones de iTunes
- **Información Detallada**: Bio de géneros, tags, conexiones
- **Zoom y Navegación**: Centrado automático en nodos seleccionados
- **Auto-expand**: Al hacer clic en macro-género, expande automáticamente a subgéneros

### 📊 Métricas Históricas
- Selector de región: Global, LATAM, España, Galicia, USA
- Selector de período: Ahora, 2020, 2015, 2010, 2005, 2000, 1995
- Top 10 artistas y géneros por región/época

---

## 🏗️ Arquitectura Técnica

### Estructura de Datos

#### GENRES Object
```javascript
{
  id: {
    label: "Nombre del Género",
    color: "#hexcolor",
    bio: "Descripción histórica",
    tags: ["tag1", "tag2"],
    itunesQuery: "query para iTunes API",
    spotifySearch: "query para Spotify API"
  }
}
```
**Ejemplo**:
```javascript
rock: {
  label: "Rock",
  color: "#ef4444",
  bio: "Originado en 1950s EE.UU., revolucionó la música con guitarra eléctrica...",
  tags: ["guitarra", "1950s", "electricidad"],
  itunesQuery: "the beatles rock",
  spotifySearch: "rock classic"
}
```

#### macroGenres Array
```javascript
[
  { id: "rock", children: ["rock_clasico", "rock_alt", "punk", "metal", "grunge", "indie_rock"] },
  { id: "electronica", children: ["house", "techno", "drum_bass", "ambient", "synthwave", "dubstep"] },
  // ... 21 macro-géneros en total
]
```

#### Bridges (Conexiones Transversales)
```javascript
[
  { s: "jazz_fusion", t: "rock_alt", l: "Jazz-Rock Fusion" },
  { s: "funk", t: "trap", l: "Funk en el Hip Hop" },
  // Representan influencias cruzadas
]
```

### Algoritmo de Visualización

#### Force-Directed Graph (D3.js v7)
```
1. Inicialización:
   - Crear nodos basados en GENRES
   - Crear enlaces jerárquicos (macro→sub, sub→artista)
   - Crear bridges entre géneros relacionados

2. Simulación Física:
   - manyBody: -400 (repulsión entre nodos)
   - link: Fuerza de atracción según jerarquía
   - collide: Radio de colisión para evitar solapamiento
   - center: Atracción hacia el centro

3. Actualización:
   - Cada frame: Calcular nuevas posiciones basadas en fuerzas
   - Renderizar en canvas HTML5
   - Aplicar colores, etiquetas, interactividad
```

#### Transiciones Entre Vistas
```
macro (21 nodos)
    ↓
sub (90 nodos) - Auto-expand disponible
    ↓
artist (100+ nodos) - Artistas por género
```

---

## 🛠️ Configuración

### Requisitos
- Navegador moderno (Chrome, Firefox, Safari, Edge)
- Conexión a Internet (para iTunes API y Spotify)
- Sin instalación requerida (aplicación standalone)

### Instalación Local
```bash
# Clonar repositorio
git clone https://github.com/Retselfernandez/SonicNodes.git

# Navegar a carpeta
cd SonicNodes

# Abrir en navegador (archivo local o servidor web)
open Sonic_nodes_V4.html
# O usar un servidor local:
python -m http.server 8000
# Luego acceder a: http://localhost:8000/Sonic_nodes_V4.html
```

### Variables de Configuración (en código)
```javascript
// Fuerza de simulación
const FORCE_STRENGTH = -400;      // Repulsión entre nodos
const LINK_DISTANCE = 80;          // Distancia natural de enlaces
const COLLISION_RADIUS = 25;       // Radio para evitar colisiones

// Visualización
const NODE_SIZE_MACRO = 30;       // Tamaño macro-géneros
const NODE_SIZE_SUB = 15;         // Tamaño subgéneros
const NODE_SIZE_ARTIST = 10;      // Tamaño artistas

// Zoom y navegación
const ZOOM_LEVEL = 3.5;           // Zoom al seleccionar nodo
const CENTER_ANIMATION = 700;     // Duración animación (ms)
```

### Personalización de Géneros
Para agregar nuevos géneros, editar:
1. **GENRES object** (línea ~534+): Agregar nueva entrada con metadata
2. **macroGenres array** (línea ~655+): Agregar a children si es subgénero
3. **GENRE_ARTISTS object** (línea ~730+): Agregar artistas relacionados

---

## 💻 Tecnologías Utilizadas

### Frontend Stack
| Tecnología | Versión | Propósito |
|-----------|---------|----------|
| **HTML5** | - | Estructura semántica |
| **CSS3** | - | Styling, glassmorphism, variables CSS |
| **JavaScript (ES6+)** | - | Lógica interactiva, eventos |
| **Force-Graph** | 1.43.5 | Renderización de grafo interactivo |
| **D3.js** | 7.0+ | Simulación física de fuerzas |
| **Canvas HTML5** | - | Rendering 2D de alto rendimiento |

### APIs Externas
- **iTunes Search API**: Previsualizaciones de audio (sin autenticación)
- **Spotify Web API**: Búsqueda de artistas (requiere setup opcional)
- **Librería de íconos**: Iconos SVG inline

### Librerías de Diseño
- **Space Grotesk**: Tipografía body (sans-serif)
- **DM Mono**: Tipografía monoespaciada
- **CSS Custom Properties**: Sistema de diseño tokenizado

### Componentes Interactivos
```
├── Canvas de Grafo (ForceGraph)
├── Panel Inspector Lateral
├── Audio Player (iTunes)
├── Controles de Profundidad (Macro/Sub/Artista)
├── Selector de Tema (Dark/Light)
├── Búsqueda en Tiempo Real
├── Métricas Históricas (Selectors)
└── Simbología Interactiva
```

---

## 📊 Comparación de Versiones

### v1.0 (grafos_isomorfos.html)
- **Géneros**: 5 macro-géneros iniciales
- **Nodos**: ~20 totales
- **Features**: Visualización básica de grafo
- **Tema**: Solo modo oscuro
- **APIs**: Ninguna integración externa
- **Estado**: Prototipo fundacional

### v2.0 (sonic_nodes_v2.html)
- **Géneros**: 8 macro-géneros
- **Nodos**: ~40 totales
- **Features**: 
  - Búsqueda implementada
  - Panel inspector básico
  - Tema claro/oscuro
- **APIs**: iTunes Search integrada
- **Estado**: MVP expandido

### v4.0 (Sonic_nodes_V4.html - Pre v4.5)
- **Géneros**: 5 macro-géneros
- **Nodos**: 25 totales
- **Features**:
  - Métricas históricas
  - Spotify integration
  - Audio player completo
  - Simbología avanzada
- **Líneas**: Tenues en modo light (problema reportado)
- **Auto-expand**: No implementado
- **Estado**: Versión estable con limitaciones

### v4.5 (Sonic_nodes_V4.html - ACTUAL) ⭐
- **Géneros**: 21 macro-géneros (expandido 4x)
- **Nodos**: 90+ totales (expansión jerárquica)
- **Features Nuevas**:
  - ✅ Auto-expand de subgéneros al click
  - ✅ Líneas más visibles en modo light
  - ✅ 25+ nuevos géneros con metadata completa
  - ✅ Bridges transversales optimizados
  - ✅ Validación mejorada de referencias
- **Líneas (Light Mode)**: 
  - Ring links: `rgba(0,0,0,0.22)` (mejora: +5.5x visibilidad)
  - Internal links: `rgba(0,0,0,0.28)` (mejora: +2.8x visibilidad)
- **Estado**: Producción con todas las mejoras implementadas

#### 📈 Evolución de Métricas

| Métrica | v1.0 | v2.0 | v4.0 | v4.5 |
|---------|------|------|------|------|
| Macro-Géneros | 5 | 8 | 5 | 21 |
| Nodos Totales | ~20 | ~40 | 25 | 90+ |
| Profundidades | 1 | 1 | 2 | 3 |
| Auto-expand | ✗ | ✗ | ✗ | ✓ |
| Light Mode | ✗ | ✓ | ✓ | ✓ (mejorado) |
| APIs Externas | 0 | 1 | 2 | 2 |

---

## 🚀 Uso

### Interfaz Principal

```
┌─────────────────────────────────────────────────────────────┐
│  [Logo] SonicNodes v4.5    🔍 Buscar...  🌙  📊  🎧        │
├─────────────────────────────────────────────────────────────┤
│                                                              │
│  [PANEL INSPECTOR]  │        [CANVAS DE GRAFO]            │
│  ─────────────────  │  Visualización interactiva de 21     │
│  • Macro-Género     │  macro-géneros con animación         │
│  • Descripción      │  force-directed                      │
│  • Tags             │                                       │
│  • [iTunes]         │  Haz clic en nodos para:             │
│  • [Spotify]        │  • Expandir automáticamente          │
│                     │  • Ver descripción completa          │
│  [AUDIO PLAYER]     │  • Escuchar previas                  │
│  ────────────────   │                                       │
│  [⏮ 0:15 / 3:45 ⏭] │                                       │
│                     │                                       │
├─────────────────────┤  [MÉTRICAS HISTÓRICAS]              │
│ Profundidad Grafo:  │  ───────────────────                │
│ [Macro] [Sub] [A]   │  🌐 Global | 📍 Ahora               │
│                     │  Top 10: Bad Bunny, Taylor...       │
│ Simbología:         │                                       │
│ 🔵 Macro-Género     │                                       │
│ 🟢 Subgénero        │                                       │
│ 🟡 Artista          │                                       │
│ ⟶  Puente           │                                       │
└─────────────────────┴───────────────────────────────────────┘
```

### Ejemplo de Interacción

**Paso 1**: Página carga en modo Macro
```
21 nodos visibles (Rock, Electrónica, Hip Hop, etc.)
```

**Paso 2**: Hacer clic en "Rock"
```
→ Se amplía la vista
→ Automáticamente cambia a Sub
→ Se muestran ~6 subgéneros de Rock
→ Panel inspector muestra info de Rock Clásico, Rock Alt, etc.
```

**Paso 3**: Búsqueda
```
Escribir "Jazz" en buscador
→ Destaca nodos Jazz, Jazz Fusion, Bebop, Cool Jazz
→ Las líneas que conectan se resaltan
```

**Paso 4**: Cambiar tema
```
Clic en 🌙
→ Fondo de blanco
→ Texto de oscuro a claro
→ Líneas de conexión con opacity mejorada (visible en light)
```

**Paso 5**: Reproducir audio
```
Clic en [iTunes]
→ Se abre player con vista previa
→ Botón play, barra de progreso, duración
```

---

## 📡 APIs Integradas

### iTunes Search API
```javascript
// Endpoint público (sin autenticación)
GET https://itunes.apple.com/search?term=rock&entity=musicTrack&limit=1

// Respuesta incluye:
{
  results: [{
    trackName: "...",
    artworkUrl100: "...",
    previewUrl: "...", // Audio 30 segundos
    artistName: "...",
    trackViewUrl: "..."
  }]
}

// Uso en SonicNodes:
itunesQuery: "the beatles rock" → Busca preview de canción
```

### Spotify Web API (Opcional)
```javascript
// Requiere Client ID para búsqueda avanzada
// Actualmente usado para búsqueda de artistas

spotifySearch: "rock classic" → Búsqueda en Spotify
```

---

## 🎨 Paleta de Colores

Cada género tiene un color distintivo para identificación rápida:

```
Rock:          #ef4444 (Rojo)
Electrónica:   #06b6d4 (Cyan)
Hip Hop:       #f59e0b (Ámbar)
Reggaeton:     #10b981 (Verde)
Afrobeats:     #8b5cf6 (Púrpura)
Latina:        #ec4899 (Rosa)
Jazz:          #6366f1 (Índigo)
Blues:         #3b82f6 (Azul)
... y 13 más
```

---

## 🔧 Troubleshooting

### Las líneas se ven borrosas
**Solución**: Cambiar a modo Light (🌙 button)
- Modo Dark: Líneas con baja opacidad (`0.04` → `0.22` mejorado)
- Modo Light: Contraste automático

### Los nodos se solapan
**Solución**: El algoritmo force-directed se auto-ajusta
- Si persiste, aumentar `COLLISION_RADIUS` en código
- O aumentar el zoom (rueda del ratón)

### No funciona iTunes
**Solución**: 
- Verificar conexión a Internet
- iTunes Search API requiere HTTPS en algunos navegadores
- Usar servidor local: `python -m http.server`

### Rendimiento bajo en muchos nodos
**Solución**:
- Reducir nivel de profundidad (ir a Macro view)
- Usar navegador moderno (Chrome/Firefox recomendado)
- Reducir `LINK_DISTANCE` en código

---

## 📝 Cambios en v4.5

### Bugfixes
- ✅ Corregido error "node not found: afrobeats"
- ✅ Eliminada redundancia en estructura de macroGenres
- ✅ Validación mejorada de referencias de nodos

### Mejoras de UX
- ✅ **Líneas visibles en modo light**: +500% de contraste
- ✅ **Auto-expand inmediato**: Al hacer clic en macro-género
- ✅ **Estructura jerárquica clara**: 21 macro → 90 sub

### Contenido Nuevo
- ✅ 16 nuevos macro-géneros agregados
- ✅ 70+ nuevas definiciones de subgéneros
- ✅ Metadata completa para todos los géneros

---

## 📚 Referencias

### Inspiración
- [Force-Graph Documentation](https://github.com/vasturiano/force-graph)
- [D3.js Force Simulation](https://d3js.org/d3-force)
- [Spotify for Developers](https://developer.spotify.com)

### Géneros Musicales
- [All Music Guide - Géneros](https://www.allmusic.com/genres)
- [Pitchfork - Music Genres](https://pitchfork.com)
- [Wikipedia - Music Genre](https://en.wikipedia.org/wiki/Music_genre)

---

## 📄 Licencia

MIT License - Libre para uso, modificación y distribución

---

## 🤝 Contribuciones

¿Ideas para mejorar SonicNodes?
- Reportar bugs: GitHub Issues
- Sugerir géneros: Pull Requests
- Feedback general: fernandez.lester@gmail.com

---

**Última actualización**: Mayo 2026  
**Versión actual**: 4.5  
**Mantenedor**: Lester Fernandez [@Retselfernandez](https://github.com/Retselfernandez)

---

*"La música es el arte de combinar sonidos de manera agradable al oído. La visualización es el arte de mostrar cómo esos sonidos se conectan en el universo."* 🎵
