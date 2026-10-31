# 📦🚚 Simulador CLI de Pilas y Colas: Almacén y Despacho de Camiones

Un simulador interactivo para la **línea de comandos** que muestra, de forma práctica, cómo funcionan dos estructuras de datos fundamentales:

- **Pila (Stack, LIFO)**: las cajas del almacén. La última caja apilada es la primera en salir.
- **Cola (Queue, FIFO)**: los camiones en la fila de espera. El primer camión en llegar es el primero en ser despachado.

El programa simula un almacén donde se apilan cajas con un camión de destino, los camiones llegan a una fila, las cajas se cargan en el camión que les corresponde y, finalmente, los camiones salen con su cargamento.

---

## 📑 Tabla de contenidos

- [Características](#-características)
- [Requisitos](#-requisitos)
- [Instalación y ejecución](#-instalación-y-ejecución)
- [Cómo funciona la simulación](#-cómo-funciona-la-simulación)
- [Guía de uso paso a paso](#-guía-de-uso-paso-a-paso)
- [Ejemplo de sesión](#-ejemplo-de-sesión)
- [Estructura del código](#-estructura-del-código)
- [Reglas y limitaciones a tener en cuenta](#-reglas-y-limitaciones-a-tener-en-cuenta)
- [Ideas para mejorar el proyecto](#-ideas-para-mejorar-el-proyecto)
- [Contribuir](#-contribuir)
- [Licencia](#-licencia)

---

## ✨ Características

- Implementación propia de las clases `Stack` (pila) y `Queue` (cola), sin librerías externas.
- Menú interactivo con 6 opciones.
- Apilado de cajas con **nombre libre** y **camión de destino**.
- Registro de camiones en una fila de espera.
- Despacho de cajas **solo desde la cima** de la pila, respetando la regla LIFO.
- Validación de que el camión de destino de la caja ya haya llegado antes de cargarla.
- Despacho de camiones **desde el frente** de la fila, respetando la regla FIFO, mostrando el cargamento con el que sale.
- Vista del estado actual del almacén y de la fila de camiones.
- Validación de entradas (opciones numéricas, respuestas Si/No, nombres vacíos, duplicados).

---

## 🧰 Requisitos

- **Python 3.10 o superior** (el programa usa la instrucción `match`/`case`, que no existe en versiones anteriores).
- No requiere instalar dependencias.

Para verificar tu versión de Python:

```bash
python --version
```

---

## 🚀 Instalación y ejecución

1. **Clona el repositorio:**

   ```bash
   git clone https://github.com/<tu-usuario>/<nombre-del-repositorio>.git
   cd <nombre-del-repositorio>
   ```

2. **Ejecuta el programa:**

   ```bash
   python Simulador_CLI_de_Pilas_y_Colas_02.py
   ```

   En algunos sistemas (Linux/macOS) puede ser necesario usar `python3`:

   ```bash
   python3 Simulador_CLI_de_Pilas_y_Colas_02.py
   ```

> 💡 **Consejo:** si tu archivo tiene espacios o puntos en el nombre (por ejemplo `Simulador CLI de Pilas y Colas.02.py`), enciérralo entre comillas al ejecutarlo o renómbralo para evitar problemas.

---

## 🧠 Cómo funciona la simulación

```
   ALMACÉN (PILA / LIFO)                FILA DE CAMIONES (COLA / FIFO)

        ┌────────────┐  ← Cima                Frente                    Fin
        │   Caja 3   │  (sale primero)          ↓                        ↓
        ├────────────┤                     ┌──────────┬──────────┬──────────┐
        │   Caja 2   │                     │ Camion-A │ Camion-B │ Camion-C │
        ├────────────┤                     └──────────┴──────────┴──────────┘
        │   Caja 1   │  ← Base                  ↑ sale primero
        └────────────┘
```

1. Las **cajas** se apilan en el almacén; cada una lleva el nombre del camión al que debe ir.
2. Los **camiones** llegan y se forman en una fila.
3. Se intenta **despachar la caja de la cima** hacia su camión. Solo se puede hacer si ese camión **ya está en la fila**.
4. Se **despacha el camión** que está al frente de la fila, y se muestra qué cajas llevaba.

---

## 📖 Guía de uso paso a paso

Al iniciar, se muestra el menú principal:

```
==================================================
SISTEMA DE DESPACHO Y ALMACÉN
==================================================
1. Almacen de cajas (Apilar cajas)
2. Llegada de camion al almacen (Llega el camion a la fila)
3. Guardar cajas a transportar (Retirar caja de la cima)
4. Enviar camion (Despachar primer camion)
5. Ver estado del almacen y los camiones
6. Salir del programa
--------------------------------------------------
Seleccione una opción (1-6):
```

### Opción 1: Almacén de cajas (apilar)

Agrega cajas a la pila. Para cada caja el programa pide:

| Dato | Descripción | Ejemplo |
|------|-------------|---------|
| Nombre de la caja | Cualquier texto no vacío. No puede repetirse con otra caja que siga en el almacén. | `Televisor`, `Caja-10`, `Ropa` |
| Camión de destino | Puedes escribir el nombre completo o solo la letra/identificador. El programa agrega el prefijo `Camion-` si no lo tienes. | `A` → `Camion-A` |

Después te pregunta si deseas almacenar otra caja (`Si` / `No`).

### Opción 2: Llegada de camión (encolar)

Registra camiones en la fila de espera. Escribe **solo el identificador** del camión; el programa agrega el prefijo `Camion-` automáticamente.

| Escribes | Se registra como |
|----------|------------------|
| `J` | `Camion-J` |
| `Norte` | `Camion-Norte` |

> ⚠️ En esta opción **no** escribas el prefijo `Camion-`, o quedará duplicado (`Camion-Camion-J`).

No se permite registrar dos veces el mismo camión mientras siga en la fila.

### Opción 3: Guardar cajas a transportar (desapilar)

Toma la **caja de la cima** y revisa su camión de destino:

- ✅ **Si el camión está en la fila:** la caja sale de la pila y se carga en ese camión.
- ❌ **Si el camión aún no ha llegado:** se muestra un aviso y la caja permanece en la cima. Debes registrar el camión (opción 2) antes de poder cargarla.

Puedes repetir el proceso respondiendo `Si` cuantas veces quieras; responde `No` para volver al menú.

> Como es una pila, **no puedes saltarte cajas**: si la caja de la cima espera a un camión que no ha llegado, las cajas que están debajo quedan bloqueadas hasta que ese camión llegue.

### Opción 4: Enviar camión (desencolar)

Despacha el camión que está **al frente de la fila** y muestra la lista de cajas con las que salió. Si no hay camiones en cola, se informa que no hay nada que despachar.

### Opción 5: Ver estado

Muestra:

- Las cajas apiladas, ordenadas de **Cima → Base**, con su camión de destino.
- La fila de camiones, ordenada de **Frente → Fin**.

### Opción 6: Salir

Cierra el programa.

---

## 🎬 Ejemplo de sesión

Un escenario que muestra el comportamiento LIFO/FIFO y el bloqueo por camión ausente:

**1. Apilar dos cajas (opción 1):**

```
Ingresa el nombre de la caja: Televisor
Ingresa el nombre del camión al que pertenece (ej. Camion-A o solo A): A
La caja "Televisor" con destino al Camion-A ha sido apilada con éxito.
Quieres almacenar otra caja? (Responde Si o No): Si
Ingresa el nombre de la caja: Ropa
Ingresa el nombre del camión al que pertenece (ej. Camion-A o solo A): B
La caja "Ropa" con destino al Camion-B ha sido apilada con éxito.
Quieres almacenar otra caja? (Responde Si o No): No
Cajas almacenadas con éxito.
```

**2. Llega solo el Camion-A (opción 2):**

```
Ingresa el nombre del camión: A
El camión Camion-A está en la fila.
Quieres enlistar otro camión? (Responde Si o No): No
Camiones enlistados con éxito.
```

**3. Intentar cargar la caja de la cima (opción 3):** la cima es `Ropa` (destino `Camion-B`), que aún no llegó.

```
Quieres despachar la caja de la cima a su camión? (Responde Si o No): Si
AVISO: El camión "Camion-B" (destino de la caja "Ropa") AÚN NO HA LLEGADO a la fila.
Debe registrar o hacer llegar este camión a la cola antes de poder despacharle su caja.
```

**4. Ver estado (opción 5):**

```
--- ESTADO DEL SISTEMA ---
Cajas apiladas (Cima -> Base):
  - Caja: 'Ropa' (Destino: Camion-B)
  - Caja: 'Televisor' (Destino: Camion-A)
Fila de camiones (Frente -> Fin): ['Camion-A']
```

**5. Llega el Camion-B (opción 2), y se vuelve a la opción 3:**

```
¡Éxito! La caja "Ropa" fue enviada a su camión: Camion-B
¡Éxito! La caja "Televisor" fue enviada a su camión: Camion-A
```

**6. Despachar camiones (opción 4):** sale primero `Camion-A` (llegó primero), luego `Camion-B`.

```
Se ha enviado el camión Camion-A y su cargamento era: ['Televisor']
Se ha enviado el camión Camion-B y su cargamento era: ['Ropa']
```

---

## 🗂️ Estructura del código

```
.
├── Simulador_CLI_de_Pilas_y_Colas_02.py   # Programa completo
└── README.md
```

### Clases

| Clase | Métodos | Descripción |
|-------|---------|-------------|
| `Stack` | `is_empty()`, `push(item)`, `pop()`, `peek()` | Pila basada en lista de Python. `pop()` y `peek()` devuelven `None` si está vacía. |
| `Queue` | `is_empty()`, `enqueue(item)`, `dequeue()`, `size()` | Cola basada en lista de Python. `dequeue()` devuelve `None` si está vacía. |

### Función principal: `transporte_cajas()`

Contiene el estado del programa y las funciones internas de cada opción del menú:

| Función interna | Opción | Qué hace |
|-----------------|--------|----------|
| `almacenar_cajas_pila()` | 1 | Apila cajas con su destino. |
| `camion_cola()` | 2 | Encola camiones. |
| `retiro_cajas_pila()` | 3 | Desapila la caja de la cima y la carga en su camión si ya llegó. |
| `despacho_camion()` | 4 | Desencola el primer camión y muestra su cargamento. |
| `estado_cajas_camiones()` | 5 | Imprime el estado de la pila y la cola. |

### Estado interno

- `cajas`: objeto `Stack` con las cajas (diccionarios `{'nombre', 'camion'}`).
- `camiones`: objeto `Queue` con los camiones en fila.
- `lista_cajas` y `lista_camiones`: listas espejo usadas para validar duplicados y mostrar el estado.
- `despacho_cajas`: lista de listas; en la posición `i` guarda las cajas cargadas en el camión `i` de la fila.

---

## ⚠️ Reglas y limitaciones a tener en cuenta

- Las respuestas de confirmación solo aceptan **`Si`** o **`No`** (sin tilde; no distingue mayúsculas/minúsculas). `Sí` con tilde se considerará un error.
- Los nombres de caja distinguen mayúsculas de minúsculas (`Ropa` ≠ `ropa`).
- El nombre de una caja solo debe ser único **mientras esté en el almacén**; una vez cargada, el nombre puede reutilizarse.
- Un camión puede recibir cajas **estando en cualquier posición de la fila**, no solo al frente. Si se despacha antes de cargar sus cajas, esas cajas seguirán en la pila esperando que el camión vuelva a registrarse.
- Una caja cuyo camión de destino ya salió quedará bloqueada en la cima (y bloqueará las de abajo) hasta que ese camión se registre de nuevo.
- Los datos viven **solo en memoria**: al cerrar el programa se pierde todo el estado.
- La opción 5 muestra la pila y la fila, pero no el cargamento actual de cada camión (este solo se ve al despacharlo).
---


