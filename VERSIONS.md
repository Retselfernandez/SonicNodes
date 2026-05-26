# 📜 Historial de Versiones de SonicNodes

## Releases

### v13.4 (Mayo 2026) - ACTUAL ⭐
**Título**: "Real-Time Trends, Live Bilingual Translation & Similar Artists"

**Cambios Principales**:
- ✅ **Sección "Lo Más Nuevo" (Actual)**: Se inyectó una sección dinámica e interactiva en el panel lateral derecho que consume el Feed RSS en tiempo real de iTunes/Apple Music para listar las 10 canciones más populares.
- ✅ **Filtro de Tendencias por País**: Selector interactivo de países (España, Estados Unidos, Reino Unido, Argentina, México, Colombia, y ahora **Chile**) con actualizaciones asíncronas en tiempo real (hot reload) e indicador visual de carga (spinner).
- ✅ **Sincronización Total de Reproducción (Play Sync)**: Los clips de audio preview de la lista "Actual" se integran directamente con el reproductor principal (esquina inferior izquierda) y con los temas clave de la discografía del modal de la "Máquina del Tiempo". Al hacer clics sucesivos se conmuta el estado play/pause de forma bidireccional y sincrónica.
- ✅ **Traducción Bilingüe Instantánea (ES / EN)**: Botón `#btn-lang-toggle` con ícono de globo terráqueo en la barra superior. Traduce instantáneamente y sin recarga de página:
  - Textos estáticos de la barra lateral, simbología, buscador, descripciones y selectores.
  - Títulos y discografías de la Máquina del Tiempo.
  - Los **60+ géneros musicales y biografías completas** renderizados en el grafo D3 ForceGraph (inyectando propiedades `labelEn` y `bioEn` dinámicamente y regenerando el grafo).
  - Mapeo y formateo lingüístico adaptativo en las sugerencias del buscador predictivo.
- ✅ **Badge de Versión Actualizado**: Distintivo visual actualizado a `v13.4` en la barra superior de la aplicación.
- ✅ **Optimización de UX en "Lo Más Nuevo"**: Se duplicó el espacio y se aumentó la legibilidad de las tarjetas de canciones en el panel derecho alineándolo simétricamente a 300px (igualando al panel izquierdo). Se incrementaron las dimensiones de las carátulas a **`48px`**, el espaciado interior a **`12px 14px`** y la altura máxima a **`420px`** (con espaciados y tamaños de fuentes optimizados).
- ✅ **Ajuste de Lectura y Envoltura Multilínea**: Se inyectó soporte de envoltura multilínea con truncamiento en la segunda línea (`-webkit-line-clamp: 2` y `white-space: normal`) para títulos de canciones largos, y se aplicó **`flex-shrink: 0`** para asegurar que el navegador jamás aplaste verticalmente las tarjetas de canciones, complementado por tooltips informativos con el título completo al posicionar el cursor sobre cada elemento.
- ✅ **Integración de Subgénero K-Pop**: Inyección de la categoría global **K-Pop** bajo el macro-género **World & Fusion** en la base de datos y en el D3 ForceGraph. Se definieron sus descripciones bilingües y se curaron los 5 artistas pilares más influyentes del género (**BTS, BLACKPINK, NewJeans, TWICE, PSY**) con sus respectivas pistas y previews de iTunes. Además, se tejió un puente transversal (*transversal bridge*) directo entre **K-Pop** y **Trap** en el grafo interactivo para representar visualmente la fuerte influencia rítmica mutua.
- ✅ **Artistas Similares (V13_4)**: Nueva sección en "Lo Más Nuevo" que muestra artistas similares al artista trending seleccionado. Se activa automáticamente al reproducir un artista del feed trending, consultando la iTunes API para obtener artistas similares. Incluye tarjetas con portada, nombre y botón de reproducción integrado. Traducción bilingüe "Artistas Similares" / "Similar Artists".

**Archivos**:
- `Sonic_nodes_V13_3.html` (versión principal y completa de producción v13.4)
- `Sonic_nodes_V13.html` (versión principal y completa de producción v13.4)
- `Sonic_nodes_V13_4.html` (versión V13_4 con Artistas Similares)

---

### v13.3 (Mayo 2026) - Anterior
**Título**: "The Universal Search & Deep-Link Era"

**Cambios Principales**:
- ✅ **Buscador Predictivo Flotante (Glassmorphism)**: Se sustituyó el buscador lineal instantáneo (que solo operaba en nodos presentes en el grafo activo) por un motor de búsqueda recursivo universal que escanea la base de datos de macro-géneros, subgéneros, artistas curados y artistas del OLAP en tiempo real.
- ✅ **Sugerencias Predictivas Segmentadas**: Al escribir se despliega un panel flotante con Glassmorphism que divide los resultados en "Macro-género", "Género" (Subgénero) y "Artista", indicando la procedencia/género de este último.
- ✅ **Enlace Profundo Multi-nivel Completo**: Al seleccionar una sugerencia:
  - *Macro-género*: Se enfoca el nodo de inmediato (siempre presente).
  - *Subgénero*: Se cambia la profundidad del grafo a "Subgénero" y se hace zoom/centrado sobre el nodo en el grafo.
  - *Artista*: Se inyecta al artista en la base de datos dinámica en caliente (ej: "The Doors" se registra en el subgénero "psychedelic"), se cambia la profundidad a "Artista", y se enfoca con un zoom de 4x.
- ✅ **Navegación e Interactividad Mejoradas**: Se incorporó soporte de teclado (tecla `Enter` ejecuta la primera sugerencia), ocultado al hacer clic fuera y re-enfoque automático.

**Archivos**:
- `Sonic_nodes_V13_3.html` (versión principal y completa de producción v13.3)
- `Sonic_nodes_V13.html` (versión principal y completa de producción)

---

### v13.2 (Mayo 2026) - Anterior

**Cambios Principales**:
- ✅ **Enlace Profundo e Inteligente con el Grafo ("Ver en el Grafo")**: Se solucionó el problema por el cual el botón en la pantalla de discografía no lograba enfocar a artistas que no estaban cargados por defecto en el grafo. Se inyectó un resolvedor de géneros interactivo con mapeo heurístico multikeyword y registro dinámico en base de datos.
- ✅ **Mapeo Heurístico e Inyección Dinámica**: Si el artista seleccionado de la Máquina del Tiempo no se encuentra en el grafo, el resolvedor determina su género aproximado (p. ej., Grime, Reggaeton, Trap, Indie, Pop, Metal, etc.) y lo inyecta dinámicamente como un nodo satélite en el grafo real en tiempo real.
- ✅ **Transición y Enfoque Directo en Artista**: El sistema cambia de forma automática el nivel de profundidad a "Artista" (habilitando la renderización de todos los nodos satélites) y ejecuta una animación de centrado tridimensional, zoom y selección con actualización inmediata de la barra lateral.

**Archivos**:
- `Sonic_nodes_V13.html` (versión principal y completa de producción)

---

### v13.1 (Mayo 2026) - Anterior
**Título**: "The Discography & Autoplay Era"

**Cambios Principales**:
- ✅ **Reproducción Automática de Éxitos**: Al hacer clic en cualquier tarjeta de artista de la Máquina del Tiempo, la aplicación busca y reproduce inmediatamente una previsualización de iTunes en segundo plano, enlazada al reproductor de la barra inferior.
- ✅ **Pantalla de Discografía en Tiempo Real**: Al pulsar un artista, el modal de la Máquina del Tiempo realiza una transición hacia una espectacular pantalla de detalle del artista, cargando dinámicamente hasta 25 éxitos y álbumes en tiempo real desde la API de iTunes.
- ✅ **Ecualizador Animado Glassmorphic**: Diseño esmerilado que incluye una mini tarjeta del reproductor activo con carátula del álbum y un ecualizador interactivo animado por CSS.
- ✅ **Interacción Cruzada Dinámica ("Ver en el Grafo")**: El botón en la pantalla de detalle de discografía cierra el modal y redirige la cámara de ForceGraph hacia el artista seleccionado con un efecto de zoom y centrado suave.
- ✅ **Navegación Fluida (Volver)**: El botón "Volver a la Máquina del Tiempo" restablece de forma suave el panel del buscador geográfico multidimensional sin interrumpir la reproducción del tema musical actual.

**Archivos**:
- `Sonic_nodes_V13.html` (versión principal y completa de producción)

---

### v13.0 (Mayo 2026) - Anterior
**Título**: "The Time Machine Era"

**Cambios Principales**:
- ✅ **La Máquina del Tiempo Inmersiva**: Reestructuración total del panel lateral derecho. Extraída la funcionalidad de métricas históricas de la barra lateral para convertirla en un espectacular modal superpuesto a pantalla completa (ocupando el 90% de la ventana) con un sofisticado diseño Glassmorphism y fondo difuminado (backdrop blur).
- ✅ **Selector Geográfico en Cascada (OLAP)**: Sistema dinámico multidimensional donde elegir un Continente (Europa, América) desbloquea y filtra inmediatamente los Países correspondientes (Reino Unido, España / EE.UU., Argentina), ofreciendo a su vez las décadas de los 2020s, 1980s y 1940s.
- ✅ **Interacción Cruzada con ForceGraph**: Conexión interactiva bidireccional. Al hacer clic en cualquier tarjeta del top de éxitos del modal, este se cierra de forma fluida, coloca el nombre del artista en el cuadro de búsqueda principal (`#global-search`) y ejecuta automáticamente una búsqueda que centra, enfoca y amplía el nodo en el grafo interactivo.
- ✅ **Base de Datos Multidimensional Robusta**: Inyección de un objeto de datos estructurado (`timeMachineData`) con exactamente 20 artistas detallados por país/década (más de 240 registros de primer nivel como Taylor Swift, Queen, Soda Stereo, Rosalía, etc.) alineados con los nombres del ForceGraph.
- ✅ **Tarjetas de Éxitos con Tendencias**: Cada registro presenta su posición histórica (1-20), avatar con inicial del artista, género asociado, y una flecha indicativa de tendencia en colores dinámicos (subida en verde, bajada en rojo y estable en amarillo).
- ✅ **Estado Vacío Informativo (Fallback)**: Diseño premium para décadas sin datos (como las décadas de 1990 o 1970) mostrando un hermoso aviso centrado indicando que no hay métricas cargadas para ese periodo específico.
- ✅ **Limpieza y Optimización del Panel Derecho**: El panel derecho ahora luce extremadamente limpio y profesional, mostrando únicamente la "Profundidad del Grafo" y la "Simbología", permitiendo al usuario enfocarse en la navegación estructural.

**Archivos**:
- `Sonic_nodes_V13.html` (versión principal y completa de producción)

**Estadísticas**:
- Registros OLAP: 240+ artistas indexados.
- Líneas de código: ~2900 (incluyendo base de datos estructurada, estilos CSS y lógica interactiva).

---

### v4.5 (Mayo 2026) - Anterior
**Título**: "The 21 Genres Expansion"

**Cambios Principales**:
- ✅ **Expansión de géneros**: 5 → 21 macro-géneros
- ✅ **Mejora de visualización en light mode**: +500% contraste en líneas
- ✅ **Auto-expand automático**: Al click en macro-género expande subgéneros
- ✅ **70+ nuevos subgéneros**: Rock, Electrónica, Hip Hop, Jazz, Latina, etc.

**Bugfixes**:
- Corregido error "node not found: afrobeats"
- Eliminada redundancia en estructura macroGenres
- Validación mejorada de referencias de nodos

**Características Nuevas**:
- Bridges transversales optimizados
- Metadata completa para todos los géneros
- Sistema de colores expandido (21+ colores)

**Archivos**:
- `Sonic_nodes_V4.html` (versión final)

**Estadísticas**:
- Nodos: 21 (macro) → 90+ (sub)
- Géneros: 21 macro + 70 sub
- Líneas de código: ~2400
- Puentes transversales: 8

---

### v4.0 (Anterior) 
**Título**: "The Metrics & Streaming Era"

**Características**:
- 5 macro-géneros principales
- Panel de métricas históricas con selectors de región/época
- Integración completa con Spotify API
- Audio player avanzado con visualización
- Tema claro/oscuro (pero con líneas tenues en light)
- Simbología interactiva

**Limitaciones**:
- ✗ Pocas variantes de géneros
- ✗ Líneas poco visibles en modo light
- ✗ Sin auto-expand de subgéneros
- ✗ Sin bridges entre géneros

**Archivos**:
- Versión anterior de `Sonic_nodes_V4.html`

---

### v2.0 (Anterior) 🔍
**Título**: "The Search & Theme Era"

**Características**:
- 8 macro-géneros
- Búsqueda en tiempo real
- Primer tema claro/oscuro
- Integración iTunes Search API
- Panel inspector básico
- ~40 nodos totales

**Avances respecto a v1**:
- Búsqueda implementada
- APIs externas integradas
- Temas mejorados

**Archivo**:
- `sonic_nodes_v2.html`

**Estadísticas**:
- Tiempo de desarrollo: ~2 semanas
- Géneros: 8 macro
- Nodos: ~40

---

### v1.0 (Primera versión) 🚀
**Título**: "SonicNodes — The Beginning"

**Características**:
- Prototipo fundacional de grafo isomorfo
- 5 macro-géneros iniciales
- Visualización basic con ForceGraph
- Modo oscuro apenas
- ~20 nodos totales
- Sin APIs externas

**Propósito**:
- Demostración de concepto
- Exploración de visualización de redes
- Prueba de Force-directed graph

**Archivo**:
- `grafos_isomorfos.html`

**Tecnologías**:
- HTML5 + CSS3 + JavaScript
- ForceGraph v1.43.5
- D3.js

**Estadísticas**:
- Líneas de código: ~800
- Desarrollo: Prototipo inicial
- Nodos: 21 (macro), 0 (sub)
- Tiempo: Proof of Concept

---

## 📊 Comparativa de Evolución

| Aspecto | v1.0 | v2.0 | v4.0 | v4.5 | v13.0 | v13.1 | v13.2 | v13.3 | v13.4 |
|---------|------|------|------|------|-------|-------|-------|-------|-------|
| **Macro-Géneros** | 5 | 8 | 5 | 21 | 21 | 21 | 21 | 21 | 21 |
| **Total Nodos** | ~20 | ~40 | 25 | 90+ | 90+ | 90+ | 90+ (dinámicos) | 90+ (dinámicos) | 90+ (dinámicos) |
| **Profundidades** | 1 | 1 | 2 | 3 | 3 | 3 | 3 | 3 | 3 |
| **Búsqueda** | ✗ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | Universal Predictiva ⭐ | Universal Predictiva ⭐ |
| **iTunes API** | ✗ | ✓ | ✓ | ✓ | ✓ | ✓ (Búsqueda + Discografía) | ✓ (Autoplay + Discografía) | ✓ (Autoplay + Discografía) | ✓ (Autoplay + Discografía + Similar Artists) |
| **Spotify API** | ✗ | ✗ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| **Temas** | ✗ | Básico | Avanzado | Avanzado + | Premium Glassmorphism | Premium Glassmorphism | Premium Glassmorphism | Premium Glassmorphism | Premium Glassmorphism |
| **Métricas** | ✗ | ✗ | ✓ | ✓ | Máquina del Tiempo Fullscreen | M. Tiempo + Discografía en vivo | Deep-Link + Discografía en vivo | Deep-Link + Discografía en vivo | Deep-Link + Discografía en vivo |
| **Auto-expand** | ✗ | ✗ | ✗ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| **Bridges** | ✗ | ✗ | Limitados | Completos | Completos | Completos | Completos | Completos | Completos |
| **Light Mode** | ✗ | ✓ (tenue) | ✓ (tenue) | ✓ (mejorado) | ✓ (espectacular con blur) | ✓ (espectacular con blur) | ✓ (espectacular con blur) | ✓ (espectacular con blur) | ✓ (espectacular con blur) |
| **Líneas Código** | ~800 | ~1200 | ~2000 | ~2400 | ~2900 | ~3400 | ~3500 | ~3700 | ~3800 |

---

## 🎯 Roadmap Futuro

### v5.0 (Planeado)
- [ ] Integración con Last.fm API
- [ ] Historial de reproducción usuario
- [ ] Colaboración en tiempo real
- [ ] Exportar grafo como imagen/SVG
- [ ] Recomendaciones IA basadas en grafo
- [ ] Modo oscuro mejorado (OLED-friendly)

### v6.0 (Futuro)
- [ ] Mobile-responsive design
- [ ] Aplicación nativa (Electron)
- [ ] Análisis de tendencias por año
- [ ] Comunidad de usuarios
- [ ] Compartir grafos personalizados

---

## 🔄 Proceso de Desarrollo

### Metodología
```
Concepto → Prototipo → MVP → Expansión → Optimización
   v1         v2       v4.0      v4.5       v5.0+
```

### Ciclo de mejoras en v4.5
```
1. Identificación de problemas
   ├─ Problema 1: Solo 5 géneros (limitado)
   ├─ Problema 2: Líneas invisibles en light mode
   └─ Problema 3: Sin auto-expand de subgéneros

2. Análisis de solución
   ├─ Expandir géneros a 21+
   ├─ Mejorar opacity de líneas
   └─ Implementar auto-expand

3. Implementación
   ├─ Agregar 70+ nuevos subgéneros
   ├─ Modificar linkColor para light mode
   └─ Agregar lógica en onNodeClick

4. Testing
   ├─ Verificar 90+ nodos se renderizan
   ├─ Confirmar líneas visibles en light
   └─ Probar auto-expand funciona

5. Deployment
   ├─ Commit a Git
   ├─ Push a GitHub
   └─ Documentación en README
```

---

## 📈 Métricas de Crecimiento

### Complejidad del Proyecto
```
v1.0: ████ (Simple)
v2.0: ████████ (Básico)
v4.0: ████████████ (Intermedio)
v4.5: ██████████████████ (Avanzado)
v5.0: ████████████████████ (Muy Avanzado - Planeado)
```

### Cobertura de Géneros
```
v1.0:  5 géneros
v2.0:  8 géneros
v4.0:  5 géneros
v4.5: 21 géneros ← 420% crecimiento desde v1
```

### Interactividad
```
v1.0: Ver nodos
v2.0: Ver + Buscar
v4.0: Ver + Buscar + Métricas
v4.5: Ver + Buscar + Métricas + Auto-expand + Bridges
```

---

## 🎓 Lecciones Aprendidas

### v1.0 → v2.0
- ✓ ForceGraph es flexible para múltiples géneros
- ✗ Búsqueda requiere índice optimizado
- → Agregamos búsqueda en v2

### v2.0 → v4.0
- ✓ APIs externas enriquecen la experiencia
- ✗ Cambios de tema requieren rerender completo
- → Mejoramos sistema de temas en v4

### v4.0 → v4.5
- ✓ Escalabilidad: 90+ nodos se renderizan sin lag
- ✗ Opacity insuficiente en light mode (0.04 → 0.22)
- ✓ Auto-expand mejora UX significativamente
- → Todas las mejoras implementadas en v4.5

---

## 📝 Notas Históricas

### Inspiración Original
El proyecto nació de la pregunta: *"¿Cómo visualizar las relaciones complejas entre géneros musicales?"*

La respuesta fue usar:
- **Grafos**: Para representar relaciones
- **Física**: Para auto-layout natural (Force-directed)
- **Interactividad**: Para exploración intuitiva

### Decisiones Arquitectónicas

1. **HTML5 Standalone vs Framework**
   - Elegimos: Standalone HTML5
   - Razón: Carga instantánea, sin dependencies complejas

2. **ForceGraph vs D3.js Puro**
   - Elegimos: ForceGraph (wrapper de D3.js)
   - Razón: API simple, gran comunidad, bien mantenido

3. **Canvas vs SVG**
   - Elegimos: Canvas (via ForceGraph)
   - Razón: Mejor rendimiento con 90+ nodos

4. **Temas vs Single Color**
   - Elegimos: Temas dinámicos con CSS variables
   - Razón: Accesibilidad, preferencias usuario

---

## 🏆 Hitos Importantes

- **Mayo 2026**: v4.5 lanzado con todas las mejoras solicitadas
- **Anterior**: v4.0 con métricas históricas
- **Anterior**: v2.0 con búsqueda integrada
- **Inicio**: v1.0 como concepto de prueba

---

**Mantenedor**: Lester Fernandez  
**Email**: fernandez.lester@gmail.com  
**GitHub**: [@Retselfernandez](https://github.com/Retselfernandez)  
**Última actualización**: Mayo 2026
