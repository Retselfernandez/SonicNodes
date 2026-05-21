# ⚙️ API Reference - SonicNodes v4.5

## 📚 Índice
- [Objetos de Datos](#objetos-de-datos)
- [Funciones Principales](#funciones-principales)
- [Eventos](#eventos)
- [APIs Externas](#apis-externas)
- [Configuración](#configuración)

---

## 📦 Objetos de Datos

### GENRES
Diccionario de todos los géneros musicales con metadata.

```javascript
GENRES = {
  [genreId]: {
    label: string,              // Nombre del género
    color: string,              // Color hex (#rrggbb)
    bio: string,                // Descripción histórica
    tags: string[],             // Tags descriptivos
    itunesQuery: string,        // Query para iTunes API
    spotifySearch: string       // Query para Spotify
  }
}
```

**Ejemplo**:
```javascript
GENRES.rock = {
  label: "Rock",
  color: "#ef4444",
  bio: "Género musical originado en 1950s...",
  tags: ["guitarra", "1950s", "electricidad"],
  itunesQuery: "the beatles rock",
  spotifySearch: "rock classic"
}
```

**Cantidad**: 21+ géneros definidos

---

### macroGenres
Array de géneros principales con sus subgéneros.

```javascript
macroGenres = [
  {
    id: string,              // ID del macro-género
    children: string[]       // IDs de subgéneros
  }
]
```

**Ejemplo**:
```javascript
macroGenres = [
  {
    id: "rock",
    children: ["rock_clasico", "rock_alt", "punk", "metal", "grunge", "indie_rock"]
  },
  {
    id: "electronica",
    children: ["house", "techno", "drum_bass", "ambient", "synthwave", "dubstep"]
  }
  // ... 21 total
]
```

**Total**: 21 macro-géneros, ~90 subgéneros

---

### bridges
Conexiones transversales entre géneros relacionados.

```javascript
bridges = [
  {
    s: string,    // ID género fuente
    t: string,    // ID género destino
    l: string     // Etiqueta de conexión
  }
]
```

**Ejemplo**:
```javascript
bridges = [
  { s: "jazz_fusion", t: "rock_alt", l: "Jazz-Rock Fusion" },
  { s: "funk", t: "trap", l: "Funk en el Hip Hop" },
  { s: "reggae", t: "lofi", l: "Reggae Vibes" }
]
```

**Total**: 8+ bridges

---

### GENRE_ARTISTS
Artistas representativos por género.

```javascript
GENRE_ARTISTS = {
  [genreId]: [
    {
      id: string,      // ID único del artista
      name: string,    // Nombre del artista
      q: string        // Query para iTunes/Spotify
    }
  ]
}
```

**Ejemplo**:
```javascript
GENRE_ARTISTS.rock = [
  { id: "the_beatles", name: "The Beatles", q: "the beatles" },
  { id: "led_zeppelin", name: "Led Zeppelin", q: "led zeppelin" },
  { id: "pink_floyd", name: "Pink Floyd", q: "pink floyd" }
]
```

**Total**: 30+ géneros con artistas mapeados

---

## 🔧 Funciones Principales

### buildGraphData(depth)
Construye estructura de nodos y enlaces para el grafo.

```javascript
function buildGraphData(depth: 'macro' | 'sub' | 'artist'): {
  nodes: Node[],
  links: Link[]
}
```

**Parámetros**:
- `depth`: Profundidad del grafo
  - `'macro'`: 21 macro-géneros
  - `'sub'`: 90+ subgéneros
  - `'artist'`: 100+ artistas

**Retorna**: Objeto con arrays de nodos y enlaces

**Ejemplo**:
```javascript
const { nodes, links } = buildGraphData('sub');
console.log(nodes.length);  // ~90
console.log(links.length);  // ~120+
```

---

### initGraph(depth)
Inicializa el grafo con profundidad especificada.

```javascript
function initGraph(depth: 'macro' | 'sub' | 'artist'): void
```

**Efecto**:
- Limpia nodos expandidos
- Construye datos con `buildGraphData()`
- Renderiza con `renderGraph()`
- Actualiza contador de nodos

**Ejemplo**:
```javascript
initGraph('sub');  // Cambia a vista de subgéneros
```

---

### renderGraph(nodes, links)
Renderiza el grafo en canvas.

```javascript
function renderGraph(
  nodes: Node[],
  links: Link[]
): void
```

**Configura**:
- Colores de nodos
- Colores de enlaces según tipo
- Eventos de click/hover
- Zoom y navegación
- Animaciones

**Parámetros internos**:
```javascript
.nodeRelSize(15)              // Tamaño relativo
.nodeColor(n => n.color)      // Color del nodo
.linkColor(l => colorByType(l.type))
.onNodeClick(onNodeClick)
.onNodeHover(onNodeHover)
```

---

### setDepth(newDepth, button)
Cambia la profundidad del grafo y actualiza UI.

```javascript
function setDepth(
  newDepth: 'macro' | 'sub' | 'artist',
  button: HTMLElement
): void
```

**Efectos**:
- Actualiza `currentDepth`
- Llama a `initGraph()`
- Marca botón como activo
- Actualiza contador

**Ejemplo**:
```javascript
// Usuario hace click en botón "Sub"
setDepth('sub', subButton);
```

---

### updateInspector(node)
Actualiza el panel inspector lateral con info del nodo.

```javascript
function updateInspector(node: Node): void
```

**Actualiza**:
- Nombre del género
- Tipo de nodo
- Descripción (bio)
- Tags
- Links a iTunes/Spotify
- Avatar color

**Ejemplo**:
```javascript
const rockNode = graphNodes.find(n => n.id === 'rock');
updateInspector(rockNode);
// Panel muestra: "Rock | Macro-Género | Bio... | Tags: [...]"
```

---

### toggleTheme()
Alterna entre tema oscuro y claro.

```javascript
function toggleTheme(): void
```

**Efectos**:
- Cambia atributo `data-theme` en body
- Recarga colores de enlaces
- Actualiza ícono del botón
- Guarda preferencia

**Ejemplo**:
```javascript
toggleTheme();  // Alterna a tema opuesto
```

---

## 🎯 Eventos

### onNodeClick
Se dispara cuando usuario hace click en un nodo.

```javascript
currentGraph.onNodeClick(node => {
  // Centrar en nodo
  currentGraph.centerAt(node.x, node.y, 700);
  
  // Zoom
  currentGraph.zoom(3.5, 700);
  
  // Actualizar inspector
  updateInspector(node);
  
  // Auto-expand si es macro-género
  if (node.type === 'core' && currentDepth === 'macro') {
    setTimeout(() => setDepth('sub', subBtn), 200);
  }
});
```

---

### onNodeHover
Se dispara cuando mouse entra/sale de un nodo.

```javascript
currentGraph.onNodeHover(node => {
  const tt = document.getElementById('node-tooltip');
  
  if (node) {
    tt.style.display = 'block';
    const type = node.type === 'core' ? 'Macro-Género' : 'Subgénero';
    tt.innerHTML = `<strong>${node.label}</strong><br>${type}`;
  } else {
    tt.style.display = 'none';
  }
});
```

---

### onLinkHover
Se dispara cuando mouse entra/sale en un enlace.

```javascript
currentGraph.onLinkHover(link => {
  // Resaltar enlace
  if (link) {
    // Mostrar tipo de conexión
  }
});
```

---

## 🌐 APIs Externas

### iTunes Search API

**Endpoint**:
```
GET https://itunes.apple.com/search?term={query}&entity=musicTrack&limit=1
```

**Query Building**:
```javascript
const itunesQuery = GENRES[genreId].itunesQuery;
// Ejemplo: "the beatles rock"
```

**Response**:
```javascript
{
  results: [{
    trackName: "Song Name",
    artworkUrl100: "https://...",
    previewUrl: "https://...", // 30 segundos
    artistName: "Artist",
    trackViewUrl: "https://music.apple.com/..."
  }]
}
```

**Uso en SonicNodes**:
```javascript
fetch(`https://itunes.apple.com/search?term=${itunesQuery}&entity=musicTrack&limit=1`)
  .then(r => r.json())
  .then(data => {
    if (data.results.length) {
      const track = data.results[0];
      audioPlayer.src = track.previewUrl;
      artwork.src = track.artworkUrl100;
    }
  });
```

---

### Spotify Web API (Opcional)

**Requerimientos**:
- Client ID
- Client Secret (backend)
- OAuth token

**Endpoint**:
```
GET https://api.spotify.com/v1/search?q={query}&type=artist&limit=5
```

**Response**:
```javascript
{
  artists: {
    items: [{
      id: "spotify_id",
      name: "Artist Name",
      images: [{url: "..."}],
      external_urls: {spotify: "https://..."}
    }]
  }
}
```

**Estado en SonicNodes**: Parcialmente integrado (búsqueda básica)

---

## ⚙️ Configuración

### Parámetros de Simulación

```javascript
// Fuerzas del grafo (D3.js)
const FORCE_STRENGTH = -400;      // Repulsión entre nodos
const LINK_DISTANCE = 80;         // Distancia ideal de enlace
const COLLISION_RADIUS = 25;      // Radio de colisión

// Simulación
const ALPHA_DECAY = 0.1;          // Decay de la simulación
const VELOCITY_DECAY = 0.6;       // Fricción
```

### Tamaños de Nodos

```javascript
const NODE_SIZE_MACRO = 30;       // Macro-géneros
const NODE_SIZE_SUB = 15;         // Subgéneros
const NODE_SIZE_ARTIST = 10;      // Artistas
```

### Colores (Light/Dark Mode)

```javascript
// Dark Mode
const RING_LINK_DARK = 'rgba(255,255,255,0.04)';
const INTERNAL_LINK_DARK = 'rgba(255,255,255,0.1)';
const BRIDGE_LINK_DARK = 'rgba(255,255,255,0.15)';

// Light Mode
const RING_LINK_LIGHT = 'rgba(0,0,0,0.22)';      // ↑ Mejorado de 0.04
const INTERNAL_LINK_LIGHT = 'rgba(0,0,0,0.28)';  // ↑ Mejorado de 0.1
const BRIDGE_LINK_LIGHT = 'rgba(0,0,0,0.3)';
```

### Animaciones

```javascript
const CENTER_ANIMATION = 700;     // ms para centrar nodo
const ZOOM_ANIMATION = 700;       // ms para hacer zoom
const AUTO_EXPAND_DELAY = 200;    // ms antes de auto-expand
const EXPAND_ANIMATION = 600;     // ms para re-centrar después expand
```

### CSS Variables (en estilos)

```css
:root {
  --bg: #0a0a0a;
  --text: #ffffff;
  --muted: #888888;
  --accent: #06b6d4;
  --border: rgba(255,255,255,0.1);
  --glass-bg: rgba(10,10,10,0.8);
  --glass-border: rgba(255,255,255,0.2);
}

[data-theme="light"] {
  --bg: #ffffff;
  --text: #000000;
  --muted: #666666;
  --border: rgba(0,0,0,0.1);
  --glass-bg: rgba(255,255,255,0.9);
  --glass-border: rgba(0,0,0,0.1);
}
```

---

## 📖 Ejemplos de Uso

### Agregar un género

```javascript
// 1. Agregar a GENRES
GENRES.mi_genero = {
  label: "Mi Género",
  color: "#hexcolor",
  bio: "Descripción...",
  tags: ["tag1", "tag2"],
  itunesQuery: "query",
  spotifySearch: "query"
};

// 2. Agregar a macroGenres como hijo
macroGenres.find(m => m.id === 'electronica')
  .children.push('mi_genero');

// 3. (Opcional) Agregar artistas
GENRE_ARTISTS.mi_genero = [
  { id: "artist1", name: "Artist 1", q: "artist 1" }
];

// 4. Recargar
initGraph(currentDepth);
```

### Programar auto-expand

```javascript
// Al cargar página, expandir automáticamente a Sub
document.addEventListener('DOMContentLoaded', () => {
  initGraph('macro');
  // Auto-expand después de 3 segundos
  setTimeout(() => {
    initGraph('sub');
  }, 3000);
});
```

### Búsqueda personalizada

```javascript
function searchGenres(query) {
  const results = graphNodes.filter(n =>
    n.label.toLowerCase().includes(query.toLowerCase()) ||
    n.tags.some(t => t.includes(query.toLowerCase()))
  );
  return results;
}

const rockGenres = searchGenres('rock');
// [{id: 'rock', label: 'Rock'}, {id: 'rock_alt', label: 'Rock Alternativo'}...]
```

---

## 🔗 Recursos

- [ForceGraph Documentation](https://github.com/vasturiano/force-graph)
- [D3.js API Reference](https://github.com/d3/d3/blob/main/API.md)
- [iTunes Search API](https://developer.apple.com/library/archive/documentation/AudioVideo/Conceptual/iTuneSearchAPI/index.html)
- [Spotify Web API](https://developer.spotify.com/documentation/web-api)

---

**Última actualización**: Mayo 2026  
**Versión**: 4.5  
**Autor**: Lester Fernandez
