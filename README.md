# Sistema de Control de Inventario - Ferretería

Trabajo Práctico Integrador de **Programación 1**
Tecnicatura Universitaria en Programación a Distancia - UTN
**Alumna:** Ludmila García

## Descripción

Programa de consola en Python con un menú interactivo para controlar el inventario de una ferretería: cargar herramientas, consultar su stock, registrar ventas e ingresos de mercadería y ver cuáles están agotadas.

Los datos se guardan en una **lista de diccionarios** llamada `inventario`. Se actualizan en el momento, mientras el programa está abierto. Al cerrarlo, los datos se pierden

Cada herramienta es un diccionario con exactamente dos claves:

```python
{'herramienta': 'Martillo', 'cantidad': 10}
```

---

## Enlaces

- 🎥 **Video demostrativo:** [Video presentación TPI](https://youtu.be/N2488aV8hZs)
- 📄 **Informe en PDF:** [Informe_TPI_Programacion1_Garcia_Ludmila.pdf](./Informe_TPI_Programacion1_Garcia_Ludmila.pdf)

---

## Requisitos

- Python 3 (versión utilizada: **3.14.6**).
- No hace falta instalar librerías: el programa usa solamente lo que trae Python.
- Editor utilizado: Visual Studio Code 1.145.0 (opcional, se puede ejecutar desde cualquier terminal).

## Archivos

| Archivo | Contenido |
|---|---|
| `control_inventario.py` | Programa completo (es el único archivo que se ejecuta). |
| `Informe_TPI_Programacion1_Garcia_Ludmila.pdf` | Informe de diseño y fundamentación, con los diagramas de flujo. |
| `README.md` | Este archivo. |

## Cómo ejecutarlo

1. Abrir una terminal en la carpeta donde está `control_inventario.py`.
2. Escribir:

```
python control_inventario.py
```

## Menú del programa

| Opción | Qué hace |
|---|---|
| 1 | **Cargar herramientas.** Pregunta cuántas herramientas distintas se van a cargar y, por cada una, pide nombre y stock inicial. Si un dato es inválido, vuelve a pedir ese dato. Si se ejecuta más de una vez, conserva lo ya cargado. |
| 2 | **Mostrar inventario.** Lista todas las herramientas con su stock. |
| 3 | **Consultar stock.** Busca una herramienta por nombre y muestra sus unidades disponibles. |
| 4 | **Reporte de agotados.** Muestra solo las herramientas con stock igual a 0. |
| 5 | **Alta de nuevo producto.** Agrega una herramienta al final de la lista, con su stock inicial. |
| 6 | **Actualizar stock.** Registra una venta (resta unidades) o un ingreso de mercadería (suma unidades). |
| 7 | **Salir.** Termina el programa. |

El menú se vuelve a mostrar después de cada operación; solo la opción 7 termina el programa.

## Validaciones

- Los nombres se comparan sin importar mayúsculas ni espacios al inicio o al final (`Martillo`, `martillo` y ` Martillo ` son la misma herramienta).
- Nombre vacío o repetido: se rechaza.
- Stock inicial: entero mayor o igual a 0 (el 0 es válido).
- Cantidad de herramientas a cargar y unidades de una venta o ingreso: entero mayor que 0.
- Venta que supera el stock disponible: se rechaza y el stock no cambia.
- Opción del menú que no es un número, o fuera del rango 1 a 7: se muestra el error y se vuelve a pedir.
- Un dato inválido nunca deja datos a medias: una herramienta se agrega recién cuando su nombre y su stock son válidos, y una operación que falla no modifica ningún stock.

## Estructura del código

- `main()`: crea el `inventario`, repite el menú con un `while` y atrapa los errores con `try/except`.
- Una función por opción: `cargar_herramientas`, `mostrar_inventario`, `consultar_stock`, `reporte_agotados`, `alta_producto` y `actualizar_stock`.
- Funciones auxiliares: `mostrar_menu`, `convertir_entero`, `validar_mayor_que_cero`, `validar_stock`, `limpiar_nombre`, `buscar_herramienta` y `validar_nombre_nuevo`.

`inventario` se crea dentro de `main()` y se pasa como parámetro a cada función. No se usan variables globales ni clases.

## Manejo de errores

- `try/except` captura las entradas que no se pueden convertir a número entero.
- `raise ValueError(...)` lanza errores con un mensaje descriptivo cuando se rompe una regla (nombre vacío o repetido, stock negativo, venta mayor al stock, opción fuera de rango).
- En la opción 1 los errores se capturan dentro de la misma función para volver a pedir el dato. En las opciones 3, 5 y 6 salen de la función y los atrapa el `except` de `main()`, que muestra el motivo y vuelve al menú.

## Ejemplo de uso

```
===== CONTROL DE INVENTARIO - FERRETERÍA =====
1. Cargar herramientas con stock inicial
2. Mostrar inventario
3. Consultar stock de una herramienta
4. Reporte de agotados
5. Alta de nuevo producto
6. Actualizar stock (venta / ingreso)
7. Salir
Seleccione una opción: 1
¿Cuántas herramientas distintas va a cargar? 1
Herramienta 1 - nombre: Martillo
Herramienta 1 - stock inicial: 10
Se cargó "Martillo" con 10 unidades.
```
