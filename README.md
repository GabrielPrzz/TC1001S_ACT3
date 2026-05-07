# Pac-Man Game 👾

## Descripción

Implementación clásica del juego arcade **Pac-Man** en Python utilizando la librería `turtle` y `freegames`. Controla a Pac-Man para comer todos los puntos del laberinto mientras evitas a los fantasmas enemigos.

## Requisitos

- **Python** 3.7+
- **turtle** (incluido en la instalación estándar de Python)
- **freegames** (librería personalizada)

## Instalación

### 1. Clonar o descargar el repositorio
```bash
git clone https://github.com/tu-usuario/pacman-game.git
cd pacman-game
```

### 2. Instalar dependencias
```bash
pip install freegames
```

## Uso

Ejecuta el juego con:
```bash
python pacman.py
```

### Controles del Juego

| Tecla | Acción |
|-------|--------|
| `↑` | Mover arriba |
| `↓` | Mover abajo |
| `←` | Mover izquierda |
| `→` | Mover derecha |

## Características

✅ **Laberinto dinámico** - Tablero diseñado con sistema de tiles  
✅ **Sistema de puntuación** - Acumula puntos al comer  
✅ **4 Fantasmas con busqueda mejorada** - Fantasmas con algoritmo
 sencillo de busqueda para experiencia mas retadora  
✅ **Colisión** - Detección de colisiones con fantasmas  
✅ **Gráficos retro** - Estilo arcade clásico con Turtle Graphics  

## Estructura del Código

```
pacman.py
├── Variables Globales
│   ├── state          # Estado del juego (puntuación)
│   ├── pacman         # Posición de Pac-Man
│   ├── ghosts         # Array de fantasmas [posición, dirección]
│   └── tiles          # Mapa del laberinto (20x20)
├── Funciones Gráficas
│   ├── square()       # Dibuja un cuadrado
│   ├── world()        # Renderiza el laberinto
│   └── offset()       # Calcula índice en el grid
├── Lógica del Juego
│   ├── valid()        # Valida posiciones
│   ├── move()         # Loop principal de movimiento
│   └── change()       # Cambia dirección de Pac-Man
└── Configuración
    └── setup(), listen(), done()
```

## Caracteristicas mejoradas/implementadas


### 1. Fantasmas mas inteligentes! ✅
Los fantasmas ahora pueden encontrar mejores caminos en x y y, siendo mas retador
```python
    for point, course in ghosts:
        dx = pacman.x - point.x
        dy = pacman.y - point.y

        if abs(dx) > abs(dy):
            preferred = vector(5*GHOST_SPEED_FACTOR if dx > 0 else -5*GHOST_SPEED_FACTOR, 0)
        else:
            preferred = vector(0, 5*GHOST_SPEED_FACTOR if dy > 0 else -5*GHOST_SPEED_FACTOR)

        if valid(point + preferred):
            course.x = preferred.x
            course.y = preferred.y
        elif valid(point + course):
            pass
        else:
            options = [
                vector(5*GHOST_SPEED_FACTOR, 0),
                vector(-5*GHOST_SPEED_FACTOR, 0),
                vector(0, 5*GHOST_SPEED_FACTOR),
                vector(0, -5*GHOST_SPEED_FACTOR),
            ]
            plan = choice(options)
            course.x = plan.x
            course.y = plan.y

        point.move(course)
```

### 2. Tablero mas grande y complicado... ✅
Agregamos un tablero con una estructura mas dificil y expandida, modificable en cualquier momento...
```python
tiles = [
    0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,
    0, 1, 0, 1, 0, 1, 0, 1, 0, 1, 0, 1, 0, 1, 0, 1, 1, 1, 0, 0,
    0, 1, 0, 0, 1, 0, 0, 1, 0, 1, 0, 0, 1, 0, 0, 1, 0, 1, 0, 0,
    0, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 0, 0,
    0, 1, 0, 0, 1, 0, 1, 0, 0, 0, 1, 0, 1, 0, 0, 1, 0, 0, 0, 0,
    0, 1, 1, 1, 1, 0, 1, 1, 0, 1, 1, 0, 1, 1, 1, 1, 1, 1, 0, 0,
    0, 1, 0, 0, 1, 0, 0, 1, 0, 1, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0,
    0, 1, 0, 0, 1, 0, 1, 1, 1, 1, 1, 0, 1, 0, 0, 1, 0, 0, 0, 0,
    0, 1, 1, 1, 1, 1, 1, 0, 0, 0, 1, 1, 1, 1, 1, 1, 0, 0, 0, 0,
    0, 0, 0, 0, 1, 0, 1, 1, 1, 1, 1, 0, 1, 0, 0, 1, 0, 0, 0, 0,
    0, 0, 0, 0, 1, 0, 1, 0, 0, 0, 1, 0, 1, 0, 0, 1, 0, 0, 0, 0,
    0, 1, 1, 1, 1, 1, 1, 1, 0, 1, 1, 1, 1, 1, 1, 1, 0, 0, 0, 0,
    0, 1, 0, 0, 1, 0, 0, 1, 0, 1, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0,
    0, 1, 1, 0, 1, 1, 1, 1, 1, 1, 1, 1, 1, 0, 1, 1, 0, 0, 0, 0,
    0, 0, 1, 0, 1, 0, 1, 0, 0, 0, 1, 0, 1, 0, 1, 0, 0, 0, 0, 0,
    0, 1, 1, 1, 1, 0, 1, 1, 0, 1, 1, 0, 1, 1, 1, 1, 0, 0, 0, 0,
    0, 1, 0, 0, 0, 0, 0, 1, 0, 1, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0,
    0, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 0, 0, 0, 0,
    0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,
    0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,
]
```

### 3. Velocidad modificable para los fantasmas ✅
Se agrego el **GHOST_SPEED_FACTOR** pudiendo hacer a los fantasmas mas rapidos o mas lentos de forma muy sencilla
```python
  ...
  GHOST_SPEED_FACTOR = 0.6
  ...
      for point, course in ghosts:
        dx = pacman.x - point.x
        dy = pacman.y - point.y

        if abs(dx) > abs(dy):
            preferred = vector(5*GHOST_SPEED_FACTOR if dx > 0 else -5*GHOST_SPEED_FACTOR, 0)
        else:
            preferred = vector(0, 5*GHOST_SPEED_FACTOR if dy > 0 else -5*GHOST_SPEED_FACTOR)

        if valid(point + preferred):
            course.x = preferred.x
            course.y = preferred.y
        elif valid(point + course):
            pass
        else:
            options = [
                vector(5*GHOST_SPEED_FACTOR, 0),
                vector(-5*GHOST_SPEED_FACTOR, 0),
                vector(0, 5*GHOST_SPEED_FACTOR),
                vector(0, -5*GHOST_SPEED_FACTOR),
            ]
            plan = choice(options)
            course.x = plan.x
            course.y = plan.y

        point.move(course)
  ...
```
 
## Posibles Mejoras

- 🎯 Implementar algoritmo A* para IA de fantasmas
- 💾 Sistema de niveles
- 🎵 Efectos de sonido y música
- 👻 Fantasmas con comportamientos diferenciados
- 📊 Tabla de puntuaciones
- 🎨 Temas personalizables

## Licencia

Este proyecto utiliza la librería `freegames` de [Giles Thomas](https://github.com/giles/freegames).

## Autor

Creado como práctica de programación con Turtle Graphics.

---

**¿Listo para jugar?** 🕹️ Ejecuta `python pacman.py` y ¡que disfrutes!
