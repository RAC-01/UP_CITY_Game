# UP CITY — Simulador Interactivo del Campus UP

**Autores:**  
Luis Mario Padilla Reyes · Andrea Constanza Jiménez Carmona · Rania Hannin Aceves Chávez  
**Docente:** Ing. Isaac Arriaga  
**Materia:** Diseño Lógico · Universidad Panamericana Campus Bonaterra  
**Fecha:** 30 de octubre de 2025  

---

## Descripción general

**UP CITY** es un simulador educativo en 2D del campus universitario, desarrollado en **Python** con **Pygame** y **Tiled**.  
Permite jugar como **Alumno**, **Maestro** o **Colaborador**, cada uno con tareas, necesidades y rutinas diarias que afectan su **salud**, **economía** y **rendimiento académico**.

El juego busca reflejar la vida universitaria real de manera interactiva, mostrando la importancia de cada rol dentro del campus.  
El jugador debe cumplir actividades, mantener sus necesidades básicas y equilibrar tiempo, salud y dinero durante el día.

---

## Funcionalidades principales

- Sistema de **roles** (Alumno, Maestro, Colaborador).  
- **Mapa TMX** interactivo con colisiones reales.  
- **NPCs** con movimiento pseudoaleatorio e interacción por teclado (tecla **E**).  
- **Economía diaria**: las acciones completadas generan dinero, las que se omiten lo restan.  
- **Sistema de GPA (promedio académico)** y penalizaciones por descuido.  
- **HUD dinámico** con indicadores de dinero, día, GPA y tiempo.  
- **Diálogos personalizados** almacenados en `dialogues.json`.  
- **Arquitectura modular y orientada a objetos** que separa lógica, interfaz, motor y configuración.  

---

## Arquitectura del código

| Archivo / Carpeta | Función |
|--------------------|---------|
| **`main.py`** | Núcleo del juego y administración de escenas (menú, selección, ajustes, gameplay). |
| **`settings.py`** | Configuración global: colores, rutas, economía, GPA, sonido, y duración del día. |
| **`core/engine.py`** | Motor base, clase `Scene`, cámara 2D y utilidades de dibujo. |
| **`core/tilemap_tmx.py`** | Carga de mapas creados en Tiled (`.tmx`) y gestión de colisiones y marcadores. |
| **`core/tilemap.py`** | Proxy que expone `TileMap` y permite cambiar la implementación sin modificar el resto. |
| **`game/entities.py`** | Define `Entity`, `Player`, `NPC`, `Enemy`, `Item`. Cada uno con movimiento, colisión y comportamiento. |
| **`game/dialogue.py`** | Sistema de diálogos con NPCs, incluyendo texto, nombre del hablante y control de páginas. |
| **`game/ui.py`** | Elementos de interfaz: botones, sliders y el HUD del jugador. |
| **`assets/`** | Carpeta con imágenes, música, efectos de sonido y fuentes. |
| **`data/`** | Contiene los mapas `.tmx` y los diálogos (`dialogues.json`). |

El proyecto está completamente **modularizado**: cada componente es independiente y puede modificarse sin afectar al resto.  
Esto facilita la ampliación del juego (añadir más NPCs, nuevos mapas o misiones) sin alterar el funcionamiento central.

---

## Lógica y algoritmos utilizados

- **Bucle principal (Game Loop):** ejecuta lectura de eventos, actualización y renderizado por cuadro (`update()` / `draw()`).  
- **Movimiento pseudoaleatorio:** los NPCs eligen direcciones aleatorias cada cierto tiempo y cambian al chocar con paredes.  
- **Colisiones:** detección basada en rectángulos (`pygame.Rect.colliderect()`), impidiendo atravesar muros o edificios.  
- **Planificación de tareas:** listas y diccionarios manejan rutinas diarias con duración, recompensa y penalización.  
- **Economía diaria:** reglas en `MONEY_RULES` determinan cuánto se gana o se pierde según el comportamiento.  
- **Orientación a objetos:** herencia (`Entity`, `Player`, `NPC`) y composición (cada `Scene` contiene mapa, cámara, UI, etc.).  
- **Cámara centrada:** `Camera2D` sigue al jugador sin mostrar zonas fuera del mapa.  

---

## Instalación y ejecución

### Requisitos
- Python 3.12 o superior  
- Pygame  
- PyTMX  

### Instalación
```bash
pip install pygame pytmx
