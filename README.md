# ideaABP

# 🎮 Ascenso Pixel - Estilo Celeste

> Un juego de plataformas 2D inspirado en el célebre título *Celeste*, desarrollado por Maddy Makes Games. Este proyecto implementa las mecánicas fundamentales de un platformer moderno con física precisa, dash在空中 y niveles desafiantes.

**Desarrollado por:** Dilan Andres Vélez  
**Versión:** 1.0.0  
**Fecha de creación:** 2026

---

## 📋 Tabla de Contenidos

1. [Descripción del Proyecto](#descripción-del-proyecto)
2. [Características Principales](#características-principales)
3. [Controles del Juego](#controles-del-juego)
4. [Mecánicas de Juego](#mecánicas-de-juego)
5. [Estructura del Código](#estructura-del-código)
6. [Niveles del Juego](#niveles-del-juego)
7. [Ejecución del Proyecto](#ejecución-del-proyecto)
8. [Tecnologías Utilizadas](#tecnologías-utilizadas)
9. [Personalización](#personalización)
10. [Créditos](#créditos)

---

## 📖 Descripción del Proyecto

**Ascenso Pixel** es un juego de plataformas en 2D desarrollado en JavaScript vanilla utilizando el elemento `<canvas>` de HTML5. El proyecto está inspirado en la física y el diseño de niveles del juego *Celeste*, conocido por su gameplay preciso y desafiante.

El juego cuenta con:
- ✅ Física de plataformas con gravedad realista
- ✅ Sistema de dash (embestida) en 8 direcciones
- ✅ Doble salto
- ✅ Plataformas móviles
- ✅ Zonas de viento
- ✅ 4 niveles progresivos
- ✅ Sistema de muertes y reinicio
- ✅ Gráficos estilo pixel art

---

## ✨ Características Principales

### Física de Plataformas
- **Gravedad constante**: Proporciona sensación de peso al personaje
- **Fricción en aire**: Control preciso durante los saltos
- **Velocidad máxima**: Limita la velocidad horizontal para mayor control
- **Colisiones AABB**: Detección de colisiones precisa con tiles del mapa

### Sistema de Dash
- **8 direcciones**: Dash horizontal, vertical o diagonal
- **Efecto de estela visual**:跟随者 efecto visual durante el dash
- **Enfriamiento**: Cooldown entre dashes para equilibrar el gameplay

### Sistema de Niveles
- **4 niveles diseñados**: Desde básico hasta desafío completo
- **Progresión**: Cada nivel introduce nuevas mecánicas
- **Meta (Exit)**: Objetivo de cada nivel

---

## 🎮 Controles del Juego

| Acción | Teclas Primarias | Teclas Alternativas |
|--------|------------------|---------------------|
| **Mover Izquierda** | `←` (Flecha) | `A` |
| **Mover Derecha** | `→` (Flecha) | `D` |
| **Subir** | `↑` (Flecha) | `W` |
| **Bajar** | `↓` (Flecha) | `S` |
| **Saltar** | `Espacio` | `Z` / `K` |
| **Dash** | `X` | `Shift` / `L` |
| **Reiniciar Nivel** | `R` | `R` (mayúscula o minúscula) |

### Consejos de Control
- 🏃 **Movimiento**: Usa las flechas o WASD para moverte
- ⬆️ **Salto**: Presiona espacio/Z para saltar. Puedes presionar nuevamente en el aire para doble salto
- ⚡ **Dash**: Presiona X/Shift durante el movimiento para un impulso rápido en 8 direcciones
- 🔄 **Reiniciar**: Si te quedas atascado, presiona R para reiniciar el nivel

---

## ⚙️ Mecánicas de Juego

### Movimiento del Jugador
El jugador (cubo rojo) se mueve con aceleración y fricción:
- **Aceleración**: 0.8 unidades/frame
- **Fricción**: 0.8 (reduce velocidad al soltar teclas)
- **Velocidad máxima**: 6 unidades/frame
- **Gravedad**: 0.5 unidades/frame²

### Sistema de Salto
- **Fuerza de salto**: -9.5 (hacia arriba)
- **Doble salto**: Disponible al saltar desde el suelo
- **Reducción del segundo salto**: 80% de la fuerza original

### Sistema de Dash
- **Velocidad de dash**: 12 unidades/frame
- **Duración**: 10 frames
- **Enfriamiento**: 25 frames
- **Direcciones**: 8 (cardinales y diagonales)

### Elementos del Nivel

| Símbolo | Elemento | Descripción |
|---------|----------|-------------|
| `#` | Pared | Bloque sólido donde no puedes pasar |
| `^` | Pincho | Peligro que causa muerte al contacto |
| `P` | Inicio | Punto de spawn del jugador |
| `E` | Meta/Salida | Objetivo del nivel |
| `M` | Plataforma móvil | Se mueve horizontalmente |
| `W` | Zona de viento | Empuja al jugador en una dirección |

### Sistema de Muerte
- Contacto con pinchos (fijos o flotantes)
- Caída fuera del mapa (más de 100 pixels debajo del nivel)
- Al morir: el nivel se reinicia y el contador de muertes aumenta

---

## 📁 Estructura del Código

El código está contenido en un solo archivo [`index.html`](index.html:1) y se organiza de la siguiente manera:

### Sección de Estilos (CSS)
- **Líneas 6-50**: Definición de estilos del juego
- Fuente tipográfica: "Press Start 2P" (estilo pixel art)
- Paleta de colores inspirada en Celeste

### Sección de JavaScript

| Sección | Líneas | Descripción |
|---------|--------|-------------|
| **Configuración** | 73-93 | Constantes del motor (gravedad, fricción, velocidades) |
| **Input** | 95-118 | Manejo de eventos de teclado |
| **Clase Particle** | 122-145 | Sistema de partículas visuales |
| **Clase Player** | 147-385 | Lógica del jugador (movimiento, colisiones, dash) |
| **Gestión de Niveles** | 387-442 | Definición de los 4 niveles |
| **Funciones del Juego** | 444-668 | Loop principal, renderizado, gestión de estado |

### Constantes Principales

```javascript
const TILE_SIZE = 40;        // Tamaño de cada tile del mapa
const GRAVITY = 0.5;         // Fuerza de gravedad
const FRICTION = 0.8;        // Fricción del aire
const ACCEL = 0.8;           // Aceleración del jugador
const MAX_SPEED = 6;         // Velocidad máxima horizontal
const JUMP_FORCE = -9.5;     // Fuerza del salto
const DASH_SPEED = 12;       // Velocidad del dash
const DASH_DURATION = 10;    // Duración del dash en frames
const DASH_COOLDOWN = 25;    // Cooldown del dash en frames
```

---

## 🗺️ Niveles del Juego

### Nivel 1: Básico 🟢
- **Dificultad**: Introducción
- **Mecánicas**: Movimiento básico, saltos simples
- **Objetivo**: Aprender los controles fundamentales

### Nivel 2: Plataformas Móviles y Dash 🟡
- **Dificultad**: Intermedia
- **Mecánicas**: Plataformas móviles (M), dash obligatorio
- **Objetivo**: Dominar el dash y la timing con plataformas

### Nivel 3: Viento y Precisión 🟠
- **Dificultad**: Avanzada
- **Mecánicas**: Zonas de viento (W), precisión extrema
- **Objetivo**: Controlar el movimiento con viento

### Nivel 4: El Reto Final 🔴
- **Dificultad**: Experto
- **Mecánicas**: Todo junto (plataformas, viento, pinchos)
- **Objetivo**: Combinar todas las habilidades

---

## 🚀 Ejecución del Proyecto

### Requisitos Previos
- Navegador web moderno (Chrome, Firefox, Edge, Safari)
- Conexión a internet (para cargar la fuente de Google Fonts)

### Pasos para Ejecutar

1. **Clonar o descargar el repositorio**
   ```bash
   git clone <url-del-repositorio>
   cd <nombre-del-proyecto>
   ```

2. **Abrir el archivo**
   - Simplemente haz doble clic en `index.html`
   - O arrastra el archivo a tu navegador

3. **¡Jugar!**
   - Usa los controles especificados para jugar
   - Completa los 4 niveles

### Servidor Local (Opcional)
Si prefieres usar un servidor local:

```bash
# Con Python
python -m http.server 8000

# Con Node.js
npx serve

# Con PHP
php -S localhost:8000
```

Luego visita `http://localhost:8000` en tu navegador.

---

## 🛠️ Personalización

### Agregar Nuevos Niveles

Para agregar un nivel nuevo, añade un nuevo array de strings al arreglo `levels` (línea 391):

```javascript
[ // NIVEL 5: Tu nuevo nivel
    "####################",
    "#................E#",
    "#P.................#",
    "####################"
]
```

### Modificar la Física

Edita las constantes al inicio del script:

```javascript
const GRAVITY = 0.5;      // Mayor = más schwer
const JUMP_FORCE = -9.5;  // Mayor = salto más alto
const DASH_SPEED = 12;    // Mayor = dash más rápido
```

### Cambiar Colores

Modifica el objeto `COLORS` (líneas 85-93):

```javascript
const COLORS = {
    player: '#ff6b6b',   // Tu color preferido
    wall: '#4a4e69',
    spike: '#c1121f',
    goal: '#fca311',
    bg: '#22223b',
    wind: 'rgba(100, 200, 255, 0.2)',
    particle: '#ffffff'
};
```

---

## 📝 Notas de Desarrollo

### Inspiración
Este proyecto está inspirado en *Celeste* de Maddy Makes Games, un título que revolucionó el género de plataformas con su:
- Gameplay preciso y satisfactorio
- Sistema de dash elegante
- Narrativa emocional
- Diseño de niveles maestro

### Mejoras Potenciales
- [ ] Sistema de guardado de progreso
- [ ] Más niveles
- [ ] Personajes adicionales
- [ ] Sonido y música
- [ ] Efectos visuales avanzados
- [ ] Modo editor de niveles

---

## 📄 Licencia

Este proyecto es de uso educativo y personal. No está afiliado ni asociado con Maddy Makes Games ni con el juego original *Celeste*.

---

## 👤 Autor

**Dilan Andres Vélez**  
Desarrollador de Juegos Indie | Entusiasta de la Programación

---

## 🙏 Créditos

- **Inspiración**: [Celeste](https://www.celestegame.com/) por Maddy Makes Games
- **Fuente tipográfica**: [Press Start 2P](https://fonts.google.com/specimen/Press+Start+2P) por Google Fonts
- **Motor**: JavaScript vanilla con HTML5 Canvas

---

<div align="center">

¡Gracias por jugar! 🎮

*Made with ❤️ by Dilan Andres Vélez*

</div>

