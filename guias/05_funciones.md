# Guia 05 — Funciones

A medida que tus programas crecen, empezaras a notar que repites los mismos bloques de codigo en varios lugares. Copiar y pegar codigo es una mala practica: si necesitas corregir algo, tienes que cambiarlo en todos los lugares donde lo copiaste.

La solucion son las **funciones**: bloques de codigo con nombre que puedes definir una vez y usar cuantas veces quieras.

Ya has usado funciones que Python trae incluidas: `print()`, `input()`, `int()`, `len()`, `range()`. Ahora aprenderas a crear las tuyas.

---

## Definir una funcion

```python
def nombre_de_la_funcion():
    instrucciones
```

La palabra clave `def` le dice a Python que vas a definir una funcion. Despues va el nombre, parentesis, dos puntos, y el bloque de codigo indentado.

Ejemplo:

```python
def saludar():
    print("Hola!")
    print("Bienvenida a Technovation Girls.")
```

Esto **define** la funcion, pero no la ejecuta todavia. Para ejecutarla, la **llamas** escribiendo su nombre con parentesis:

```python
saludar()
```

Resultado:
```
Hola!
Bienvenida a Technovation Girls.
```

Puedes llamarla cuantas veces quieras:

```python
saludar()
saludar()
saludar()
```

---

## Funciones con parametros

Los **parametros** son variables que le pasas a una funcion para que trabaje con ellas. Van dentro de los parentesis al definir la funcion:

```python
def saludar(nombre):
    print(f"Hola, {nombre}!")
```

Ahora puedes llamarla con diferentes nombres:

```python
saludar("Ana")
saludar("Lucia")
saludar("Valeria")
```

Resultado:
```
Hola, Ana!
Hola, Lucia!
Hola, Valeria!
```

El valor que le pasas al llamar la funcion se llama **argumento**. En el ejemplo, `"Ana"` es el argumento y `nombre` es el parametro.

### Multiples parametros

Una funcion puede tener mas de un parametro, separados por comas:

```python
def presentar(nombre, edad, ciudad):
    print(f"Me llamo {nombre}, tengo {edad} anos y soy de {ciudad}.")

presentar("Sofia", 15, "Guadalajara")
presentar("Daniela", 13, "Bogota")
```

Resultado:
```
Me llamo Sofia, tengo 15 anos y soy de Guadalajara.
Me llamo Daniela, tengo 13 anos y soy de Bogota.
```

---

## Funciones que devuelven un valor

Hasta ahora las funciones solo ejecutan instrucciones. Pero muchas veces necesitas que una funcion **calcule algo y te devuelva el resultado** para usarlo despues.

Para eso usas `return`:

```python
def sumar(a, b):
    resultado = a + b
    return resultado
```

Ahora puedes guardar o usar lo que devuelve la funcion:

```python
total = sumar(8, 5)
print(total)  # muestra: 13

print(sumar(100, 200))  # muestra: 300
```

Cuando Python llega a `return`, devuelve el valor y **sale de la funcion inmediatamente**. Cualquier codigo despues del `return` no se ejecuta.

### Diferencia entre `print` y `return`

Esta es una confusion comun al principio:

```python
# Esta funcion MUESTRA el resultado pero no lo devuelve
def sumar_con_print(a, b):
    print(a + b)

# Esta funcion DEVUELVE el resultado para usarlo
def sumar_con_return(a, b):
    return a + b
```

```python
resultado = sumar_con_print(3, 4)   # muestra 7 en pantalla
print(resultado)                     # muestra: None (no devolvio nada)

resultado = sumar_con_return(3, 4)  # no muestra nada
print(resultado)                     # muestra: 7
```

Usa `return` cuando necesitas el resultado para hacer algo mas con el. Usa `print` solo para mostrar informacion al usuario.

---

## Parametros con valor por defecto

Puedes darle a un parametro un valor predeterminado que se usa si no se le pasa ninguno:

```python
def saludar(nombre, mensaje="Bienvenida"):
    print(f"{mensaje}, {nombre}!")

saludar("Ana")              # usa el valor por defecto
saludar("Lucia", "Hola")   # usa el valor que le pasamos
```

Resultado:
```
Bienvenida, Ana!
Hola, Lucia!
```

Los parametros con valor por defecto siempre van al **final** de la lista de parametros.

---

## Variables locales y globales

Las variables que creas **dentro** de una funcion son **locales**: solo existen mientras la funcion se ejecuta y no son accesibles desde afuera.

```python
def calcular():
    resultado = 42  # variable local
    print(resultado)

calcular()
print(resultado)  # NameError: resultado no existe aqui
```

Las variables que creas **fuera** de las funciones son **globales** y se pueden leer desde cualquier parte del programa:

```python
nombre = "Sofia"  # variable global

def saludar():
    print(f"Hola, {nombre}")  # puede leer la variable global

saludar()
```

Como buena practica, **evita modificar variables globales desde dentro de las funciones**. Es mejor pasar los datos que necesitas como parametros y devolver los resultados con `return`. Esto hace el codigo mas facil de entender y de corregir.

---

## Organizar el codigo con funciones

Las funciones no son solo para reutilizar codigo: tambien sirven para **organizar** el programa en partes con responsabilidades claras.

Compara estos dos programas que hacen lo mismo:

**Sin funciones:**
```python
nombre = input("Como te llamas? ")
edad = int(input("Cuantos anos tienes? "))

if edad >= 18:
    categoria = "adulta"
else:
    categoria = "menor de edad"

print(f"Hola, {nombre}. Eres {categoria}.")
print(f"En 10 anos tendras {edad + 10} anos.")
```

**Con funciones:**
```python
def obtener_datos():
    nombre = input("Como te llamas? ")
    edad = int(input("Cuantos anos tienes? "))
    return nombre, edad

def clasificar_edad(edad):
    if edad >= 18:
        return "adulta"
    else:
        return "menor de edad"

def mostrar_resultado(nombre, edad, categoria):
    print(f"Hola, {nombre}. Eres {categoria}.")
    print(f"En 10 anos tendras {edad + 10} anos.")

# Programa principal
nombre, edad = obtener_datos()
categoria = clasificar_edad(edad)
mostrar_resultado(nombre, edad, categoria)
```

La segunda version es mas larga, pero cada funcion tiene una tarea clara. Cuando algo falle o quieras cambiarlo, sabras exactamente donde buscar.

---

## Devolver multiples valores

Python permite que una funcion devuelva mas de un valor separandolos con comas:

```python
def minimo_y_maximo(numeros):
    return min(numeros), max(numeros)

menor, mayor = minimo_y_maximo([4, 1, 9, 2, 7])
print(f"Minimo: {menor}, Maximo: {mayor}")
```

Resultado:
```
Minimo: 1, Maximo: 9
```

---

## Ejemplo completo: calculadora de promedio

```python
def pedir_calificaciones():
    calificaciones = []
    print("Ingresa tus calificaciones (escribe 'fin' para terminar):")

    while True:
        entrada = input("Calificacion: ")
        if entrada.lower() == "fin":
            break
        calificaciones.append(float(entrada))

    return calificaciones

def calcular_promedio(calificaciones):
    if len(calificaciones) == 0:
        return 0
    return sum(calificaciones) / len(calificaciones)

def evaluar_promedio(promedio):
    if promedio >= 90:
        return "Excelente"
    elif promedio >= 75:
        return "Muy bien"
    elif promedio >= 60:
        return "Aprobado"
    else:
        return "Reprobado"

# Programa principal
calificaciones = pedir_calificaciones()
promedio = calcular_promedio(calificaciones)
evaluacion = evaluar_promedio(promedio)

print(f"\nCalificaciones: {calificaciones}")
print(f"Promedio: {promedio:.1f}")
print(f"Resultado: {evaluacion}")
```

Nota el uso de `:.1f` en el f-string: muestra el numero con exactamente un decimal.

---

## Ejercicio de esta guia

Crea un programa con las siguientes funciones:

1. `saludar(nombre)` — muestra un saludo personalizado
2. `es_par(numero)` — devuelve `True` si el numero es par, `False` si es impar
3. `celsius_a_fahrenheit(celsius)` — convierte temperatura usando la formula `(celsius * 9/5) + 32`
4. `contar_vocales(texto)` — devuelve cuantas vocales tiene un texto

Despues de definir las funciones, escribe un programa principal que las use todas.

**Reto extra:** Agrega una funcion `menu()` que muestre las opciones disponibles y le permita al usuario elegir que funcion ejecutar.

---

## Resumen

| Concepto | Que aprendiste |
|---|---|
| `def` | Palabra clave para definir una funcion |
| Parametro | Variable que recibe un valor al llamar la funcion |
| Argumento | El valor que le pasas a una funcion al llamarla |
| `return` | Devuelve un resultado desde la funcion |
| Valor por defecto | Parametro con un valor predefinido si no se pasa ninguno |
| Variable local | Variable que solo existe dentro de la funcion |
| Variable global | Variable que existe en todo el programa |

---

## Que sigue

En la siguiente guia aprenderas sobre **listas y diccionarios**: las estructuras de datos fundamentales de Python para guardar y organizar colecciones de informacion.

[Anterior: 04 — Ciclos](04_ciclos.md) | [Siguiente: 06 — Listas y diccionarios](06_listas_y_diccionarios.md)
