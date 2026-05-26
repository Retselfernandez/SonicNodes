# 📑 Índice del Proyecto SonicNodes

## 📂 Estructura del Repositorio

```
SonicNodes/
├── 📄 README.md               ← EMPEZAR AQUÍ
├── 📄 INDEX.md                ← Este archivo
├── 📄 VERSIONS.md             ← Historial de versiones
├── 📄 CONTRIBUTING.md         ← Cómo contribuir
├── 📄 API_REFERENCE.md        ← Referencia técnica
├── .gitignore
├── Logo.html                  ← Logo (auxiliar)
├── grafos_isomorfos.html      ← v1.0 (Prototipo)
├── sonic_nodes_v2.html        ← v2.0 (MVP)
└── Sonic_nodes_V13_4.html     ← v13.4 (ACTUAL - ABRIR ESTA)
```

---

## 🚀 Inicio Rápido

### 1️⃣ Ver la Aplicación
```bash
# Opción A: Abrir directamente
open Sonic_nodes_V13_4.html

# Opción B: Con servidor local
python -m http.server 8000
# Luego abre: http://localhost:8000/Sonic_nodes_V13_4.html
```

### 2️⃣ Leer la Documentación
| Archivo | Propósito |
|---------|-----------|
| **README.md** | Qué es, cómo se usa, características |
| **VERSIONS.md** | Evolución del proyecto v1.0 → v13.4 |
| **API_REFERENCE.md** | Funciones, objetos, configuración |
| **CONTRIBUTING.md** | Cómo reportar bugs, sugerir géneros |

### 3️⃣ Explorar el Código
- **HTML Structure**: Ver `<body>` en `Sonic_nodes_V4.html`
- **Géneros**: Buscar `const GENRES = {` (~línea 530)
- **Grafo**: Función `renderGraph()` (~línea 750)
- **Eventos**: Función `onNodeClick()` (~línea 790)

---

## 📚 Documentación Completa

### Para Usuarios
- **Principiantes**: Lee [README.md](README.md) sección "¿Qué es SonicNodes?"
- **Exploración**: Abre [Sonic_nodes_V4.html](Sonic_nodes_V4.html)
- **Búsqueda de Géneros**: Usa el buscador en la aplicación
- **Audio Preview**: Haz click en [iTunes] para escuchar

### Para Desarrolladores
- **Entender la Arquitectura**: Lee [API_REFERENCE.md](API_REFERENCE.md)
- **Agregar Géneros**: Sigue pasos en [CONTRIBUTING.md](CONTRIBUTING.md)
- **Ver Evolución**: Consulta [VERSIONS.md](VERSIONS.md)
- **Editar Código**: Abre `Sonic_nodes_V4.html` en editor

### Para Contribuidores
- **Reportar Bugs**: [CONTRIBUTING.md](CONTRIBUTING.md#-reportar-bugs)
- **Sugerir Géneros**: [CONTRIBUTING.md](CONTRIBUTING.md#-sugerir-nuevos-géneros)
- **Pull Requests**: [CONTRIBUTING.md](CONTRIBUTING.md#-contribuir-código)

---

## 🎯 Qué Encontrarás

### En esta Carpeta

#### Aplicación Principal
- **Sonic_nodes_V13_4.html** ⭐ (v13.4 - ACTUAL)
  - 21 macro-géneros
  - 90+ subgéneros
  - Auto-expand funcional
  - Light/Dark mode optimizado
  - APIs iTunes + Spotify
  - Artistas Similares (V13_4)

#### Versiones Anteriores (Referencia)
- **grafos_isomorfos.html** (v1.0)
  - Prototipo inicial
  - 5 géneros
  - Demostración de concepto

- **sonic_nodes_v2.html** (v2.0)
  - MVP expandido
  - Búsqueda integrada
  - Tema claro/oscuro

#### Documentación
- **README.md**: Guía completa del proyecto
- **VERSIONS.md**: Historial y comparativa de versiones
- **CONTRIBUTING.md**: Guía para colaboradores
- **API_REFERENCE.md**: Referencia técnica completa
- **INDEX.md**: Este archivo (navegación)

#### Auxiliares
- **Logo.html**: Logo del proyecto
- **.gitignore**: Archivos ignorados por Git

---

## 🔍 Navegación por Secciones

### Entender el Proyecto
```
README.md
├─ ¿Qué es SonicNodes?
├─ ¿Para qué se usa?
├─ Características Principales
└─ Arquitectura Técnica
```

### Usar la Aplicación
```
Sonic_nodes_V13_4.html → Abre en navegador
├─ Vista Macro: 21 géneros principales
├─ Vista Sub: 90+ subgéneros
├─ Vista Artista: Artistas relacionados
└─ Tema: Dark/Light mode
```

### Desarrollar Mejoras
```
API_REFERENCE.md
├─ Objetos de Datos (GENRES, macroGenres)
├─ Funciones Principales (buildGraphData, renderGraph)
├─ Eventos (onNodeClick, onNodeHover)
└─ Configuración (Parámetros de simulación)
```

### Contribuir
```
CONTRIBUTING.md
├─ Reportar Bugs
├─ Sugerir Géneros
├─ Contribuir Código
└─ Guía de Estilo
```

---

## 🎵 Géneros Disponibles

### Macro-Géneros (21)
```
1. Rock              9. Jazz Avant          17. Blues Roots
2. Electrónica       10. Electrónica Exp    18. Country Folk
3. Hip Hop           11. Indie Alt          19. World Fusion
4. Reggaeton         12. Rock Alt Gen       20. Flamenco Span
5. Afrobeats Gen     13. Metal Gen          21. Reggae Gen
6. Latina            14. Ambient Gen
7. Jazz              15. Drum Bass Gen
8. Funk Soul Gen     16. Bossa Latino
```

### Subgéneros (Ejemplos)
```
Rock → Rock Clásico, Rock Alt, Punk, Metal, Grunge, Indie Rock
Electrónica → House, Techno, Drum & Bass, Ambient, Synthwave, Dubstep
Hip Hop → Rap East Coast, Trap, Lo-Fi
Jazz → Jazz, Bebop, Jazz Fusion, Soul, Funk
... y 70+ más
```

---

## 🛠️ Tareas Comunes

### Quiero...

#### ▶️ Usar la aplicación
→ Abre [Sonic_nodes_V13_4.html](Sonic_nodes_V13_4.html)

#### 📖 Entender qué es SonicNodes
→ Lee [README.md](README.md)

#### ➕ Agregar un nuevo género
→ Sigue [CONTRIBUTING.md - Agregando Géneros](CONTRIBUTING.md#agregando-géneros)

#### 🐛 Reportar un bug
→ Ve a [CONTRIBUTING.md - Reportar Bugs](CONTRIBUTING.md#-reportar-bugs)

#### 💻 Ver el código
→ Abre `Sonic_nodes_V13_4.html` en editor
→ Busca función específica en [API_REFERENCE.md](API_REFERENCE.md)

#### 📊 Ver evolución del proyecto
→ Lee [VERSIONS.md](VERSIONS.md)

#### 🔧 Configurar parámetros
→ Consulta [API_REFERENCE.md - Configuración](API_REFERENCE.md#configuración)

#### 🚀 Contribuir código
→ Lee [CONTRIBUTING.md - Contribuir Código](CONTRIBUTING.md#-contribuir-código)

---

## 📞 Contacto

- **Autor**: Lester Fernandez
- **Email**: fernandez.lester@gmail.com
- **GitHub**: [@Retselfernandez](https://github.com/Retselfernandez)
- **Repositorio**: [SonicNodes](https://github.com/Retselfernandez/SonicNodes)

---

## 📄 Licencia

MIT License - Libre para uso, modificación y distribución

---

## 🎓 Tecnologías Usadas

- **HTML5** - Estructura
- **CSS3** - Estilos (variables CSS, glassmorphism)
- **JavaScript ES6+** - Lógica
- **ForceGraph** - Renderización de grafo
- **D3.js** - Simulación física
- **iTunes API** - Audio previews
- **Spotify API** - Búsqueda (opcional)

---

## 📋 Checklist para Desarrolladores

Antes de empezar a trabajar:

- [ ] Clonaste el repositorio
- [ ] Abriste `Sonic_nodes_V13_4.html` en navegador
- [ ] Leíste el README.md
- [ ] Entiendes la estructura en API_REFERENCE.md
- [ ] Instalaste Git (si vas a contribuir)

---

## 🔄 Flujo de Contribución

```
1. Reporta/Sugiere (Issues)
        ↓
2. Crea Fork + Branch
        ↓
3. Haz Cambios
        ↓
4. Commit con mensaje claro
        ↓
5. Push a tu branch
        ↓
6. Pull Request
        ↓
7. Review
        ↓
8. Merge a main
```

---

## 🎉 Lo Que Hace Especial a SonicNodes

✨ **Visualización Interactiva** - Explora géneros en tiempo real
🎨 **Diseño Moderno** - Glassmorphism, dark/light mode
🎵 **Audio Integrado** - Escucha previsualizaciones de iTunes
🔗 **Relaciones Complejas** - Ve cómo los géneros se conectan
🚀 **Rendimiento** - Maneja 90+ nodos sin lag
💡 **Educativo** - Aprende la evolución de la música

---

## 🏆 Mejoras en v13.4

✅ 4x más géneros (5 → 21 macro)
✅ 3.5x más nodos (25 → 90+)
✅ Auto-expand implementado
✅ Líneas visibles en light mode
✅ Documentación completa
✅ Artistas Similares vía iTunes API (V13_4)

---

**¡Bienvenido a SonicNodes!** 🎵  
*Navega el universo musical como nunca antes lo habías hecho.*

---

**Última actualización**: Mayo 2026  
**Versión**: 13.4  
**Estado**: ✅ Producción
