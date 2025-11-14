Proyecto Final Asignatura Programacion Orientada a Objetos
-------------------------------------------------------------------------------------------------------------------
### Bienvenido!
El equipo de trabajo Unidentified Programmable Object (UPO) te de la bienvenida a este repo en el cual se evidenciara y dara a conocer el desarrollo de un problema como proyecto final semestral de la materia Porgramacion Orientada a Objetos (POO).

### Integrantes: 
-Hector Alfredo Gomez Andrade
-
-

### Proyecto 
Un sistemque traduce instrucciones en lenguaje natural a G-code y muestras graficamente el recorrido de la herramienta.

### Contexto 
El **CNC (control numerico computarizado)** es un sistema que controla el movimiento de maquinas (como fresadoras o contadoras laser) medinate instrucciones precisas llamadas **G-code** cada comando g indica a ala maquina como moverse o que accion ejecutar (cortar, posicionar, hacer arcos, etc.).

### Problea a solucionar
Cuando se trabaja con maquinas CNC, crear el **G-code manualmente** es lento y muy facil de equivocarse, un solo error puede dañar la pieza o generar cortes erroneos, por eso este proyecto busca simplificar el proceso, perminitiendo escribir instrucciones en lenguaje antural (por ejemplo, dibujar una linea de 5 a 10 ) y ver como se traduce y se ejecuta graficamente. 

### Solución propuesta

Se desarrolló un **simulador de CNC 2D** que:
- Traduce instrucciones naturales a **G-code**.  
- Muestra la **trayectoria de la herramienta** en una gráfica.  
- Valida el tamaño del área de trabajo (maximo 200x300 mm).  

Esto permite verificar el resultado antes de ejecutar el código real en una máquina física.

### Interfaz y visualización

Para construir la interfaz se utilizó **Flet**, una librería que permite crear GUIs con Python fácilmente.  
Los gráficos se generan con **Matplotlib**, y se renderizan como imágenes para mostrarlas dentro de la interfaz.  

### Ejemplo de funciones gráficas
```python
# Línea recta (interpolación lineal)
ax.plot([x_inicial, x_final], [y_inicial, y_final], 'b-')

# Arco circular (interpolación circular)
self._dibujar_arco(ax, x, y, I, J, sentido="horario")
```

### Diagrama de clases 
```python
classDiagram
direction TB
    class CNCMachine {
        +load_instructions()
        +translate()
        +simulate()
    }
    class Translator {
        +translate_text()
    }
    class Grapher {
        +draw_path()
        +draw_arc()
    }
    class WorkArea {
        +validate_size()
    }
    class CutterTool {
        +position_X
        +position_Y
    }

    CNCMachine --> Translator
    CNCMachine --> Grapher
    CNCMachine --> WorkArea
    CNCMachine --> CutterTool
```
```python
flowchart TD
    A[Inicio] --> B[Leer instrucciones]
    B --> C{¿Tipo de instrucción?}
    C -->|Ubicar| D[Generar G00]
    C -->|Línea| E[Generar G01]
    C -->|Arco| F[Generar G02 / G03]
    D --> G[Guardar en archivo G-code]
    E --> G
    F --> G
    G --> H{¿Hay más líneas?}
    H -->|Sí| B
    H -->|No| I[Fin]
```



