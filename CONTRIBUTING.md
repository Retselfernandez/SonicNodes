# 🤝 Contribuyendo a SonicNodes

¡Gracias por tu interés en contribuir a SonicNodes! Este documento explica cómo puedes ayudar a mejorar el proyecto.

## 📋 Tipos de Contribuciones

### 🐛 Reportar Bugs
Si encuentras un error, por favor:

1. **Verifica que el bug no esté reportado ya**
   - Busca en [Issues](https://github.com/Retselfernandez/SonicNodes/issues)

2. **Crea un nuevo Issue** con:
   - Título descriptivo: `[BUG] Las líneas desaparecen en Firefox`
   - Descripción del problema
   - Pasos para reproducir
   - Navegador y SO
   - Screenshot si aplica

### 🎵 Sugerir Nuevos Géneros
Si quieres agregar géneros musicales:

1. **Abre un Issue** con título: `[GENRE] Sugerencia: Synthpop`
2. **Incluye**:
   - Nombre del género
   - Descripción histórica
   - Color sugerido (hex)
   - Tags relevantes
   - Artistas representativos
   - A qué macro-género pertenece

### 💡 Sugerir Mejoras
Mejoras, nuevas features, optimizaciones:

1. **Abre un Issue** con título: `[FEATURE] Exportar grafo como SVG`
2. **Describe**:
   - Qué problema resuelve
   - Cómo debería funcionar
   - Por qué es importante

### 🔧 Contribuir Código
Para cambios de código:

1. **Fork** el repositorio
2. **Crea una rama**: `git checkout -b feature/mi-mejora`
3. **Haz cambios** y **commit**: `git commit -m "[FEATURE] Descripción clara"`
4. **Push**: `git push origin feature/mi-mejora`
5. **Pull Request** con descripción detallada

---

## 📝 Guía de Estilo

### Nombres de Géneros
```javascript
// ✓ CORRECTO
rock_clasico: {
  label: "Rock Clásico",
  ...
}

// ✗ INCORRECTO
rockclasico: {  // Falta underscore
  label: "rock clásico",  // Debe empezar mayúscula
  ...
}
```

### Estructura de Género Nuevo
```javascript
GENRES: {
  mi_genero: {
    label: "Mi Género",           // Nombre legible
    color: "#hexcolor",            // Color único
    bio: "Descripción...",         // 1-2 párrafos
    tags: ["tag1", "tag2"],        // 2-5 tags
    itunesQuery: "artist genre",   // Para iTunes
    spotifySearch: "genre artist"  // Para Spotify
  }
}
```

### Commits
```
[FEATURE] Agregar género Synthpop
[BUG] Corregir crash en Firefox
[DOCS] Actualizar README
[REFACTOR] Simplificar buildGraphData()
[PERF] Optimizar rendering de 100+ nodos
```

---

## 🛠️ Configuración del Entorno

### Requisitos Mínimos
- Navegador moderno
- Editor de texto
- Git
- Opcionalmente: Live Server extension de VS Code

### Setup Local
```bash
# Clonar
git clone https://github.com/Retselfernandez/SonicNodes.git
cd SonicNodes

# Abrir en navegador
open Sonic_nodes_V4.html

# O usar servidor local
python -m http.server 8000
# Luego: http://localhost:8000/Sonic_nodes_V4.html
```

### Editar Localmente
1. Abre `Sonic_nodes_V4.html` en tu editor
2. Haz cambios
3. Recarga el navegador (Cmd+R en Mac)
4. Verifica en Dark y Light mode

---

## ✅ Checklist para Pull Request

Antes de enviar tu PR, asegúrate que:

- [ ] El código funciona en Chrome, Firefox y Safari
- [ ] No hay errores en la consola
- [ ] Las líneas son visibles en modo light y dark
- [ ] Los nuevos géneros tienen metadata completa
- [ ] El README se actualizó (si aplica)
- [ ] El commit message es descriptivo
- [ ] No agregaste archivos innecesarios (.DS_Store, etc.)

---

## 🎨 Agregando Géneros

### Paso a Paso

**1. Agrega a GENRES object (~línea 534)**
```javascript
synthpop: {
  label: "Synthpop",
  color: "#ec4899",
  bio: "Pop sintetizado de los 80s, mezcla de sintetizadores con pop pegadizo...",
  tags: ["sintetizador", "1980s", "pop"],
  itunesQuery: "depeche mode synthpop",
  spotifySearch: "synthpop 80s"
}
```

**2. Agrega a macroGenres (~línea 670)**
```javascript
// Si es subgénero de electrónica:
{ id: "electronica", children: ["synthpop", "house", ...] }
```

**3. Agrega artistas en GENRE_ARTISTS (~línea 730)**
```javascript
synthpop: [
  { id: "depeche_mode", name: "Depeche Mode", q: "depeche mode" },
  { id: "pet_shop_boys", name: "Pet Shop Boys", q: "pet shop boys" },
]
```

**4. Prueba**
```
- Carga página
- Expande a Sub-view
- Busca "Synthpop"
- Haz click en el nodo
- Verifica que aparezca info completa
```

**5. Commit**
```bash
git add Sonic_nodes_V4.html
git commit -m "[GENRE] Agregar Synthpop con 2 artistas"
git push origin feature/synthpop
```

---

## 🐛 Debugging

### Ver errores en consola
1. Abre DevTools (F12 o Cmd+Option+I)
2. Ve a "Console"
3. Busca mensajes de error

### Errores comunes

**"node not found: XXX"**
- Problema: Referencia a género que no existe
- Solución: Verifica que el ID esté en GENRES object

**Líneas invisibles en light mode**
- Problema: Opacidad muy baja
- Solución: Aumenta opacity en linkColor (~línea 752)

**Nodos se solapan**
- Problema: Fuerza de repulsión insuficiente
- Solución: Aumenta FORCE_STRENGTH en código

---

## 📞 Contacto

- **Issues**: [GitHub Issues](https://github.com/Retselfernandez/SonicNodes/issues)
- **Email**: fernandez.lester@gmail.com
- **Twitter**: [@Retselfernandez](https://twitter.com/Retselfernandez)

---

## 📄 Licencia

Al contribuir a SonicNodes, aceptas que tu código sea licenciado bajo MIT.

---

**¡Gracias por hacer que SonicNodes sea mejor! 🎵**
