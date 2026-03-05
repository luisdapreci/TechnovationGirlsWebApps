# Guia 04 — Ciclos

Imagina que quieres mostrar los numeros del 1 al 100, o saludar a cada participante de una lista, o seguir pidiendo una contrasena hasta que sea correcta. Hacerlo con `print` o `if` uno por uno seria muy lento y repetitivo.

Para eso existen los **ciclos**: estructuras que repiten un bloque de instrucciones automaticamente.

Python tiene dos tipos de ciclos: `for` y `while`.

---

## El ciclo `for`

Usa `for` cuando sabes de antemano **cuantas veces** quieres repetir algo, o cuando quieres recorrer una coleccion de elementos uno por uno.

```python
for variable in coleccion:
    instrucciones
```

### Recorrer un rango de numeros con `range()`

La funcion `range()` genera una secuencia de numeros:

```python
for numero in range(5):
    print(numero)
```

Resultado:
```
0
1
2
3
4
```

`range(5)` genera los numeros del `0` al `4` (5 numeros en total). En Python, los rangos **empiezan en 0** por defecto y el numero final **no se incluye**.

Para empezar desde 1:

```python
for numero in range(1, 6):
    print(numero)
```

Resultado:
```
1
2
3
4
5
```

`range(inicio, fin)` genera numeros desde `inicio` hasta `fin - 1`.

Para contar de dos en dos (o cualquier otro paso):

```python
for numero in range(0, 11, 2):
    print(numero)
```

Resultado:
```
0
2
4
6
8
10
```

`range(inicio, fin, paso)` avanza de `paso` en `paso`.

### Recorrer una lista de elementos

```python
participantes = ["Ana", "Lucia", "Valeria", "Sofia"]

for nombre in participantes:
    print(f"Bienvenida, {nombre}!")
```

Resultado:
```
Bienvenida, Ana!
Bienvenida, Lucia!
Bienvenida, Valeria!
Bienvenida, Sofia!
```

El ciclo toma cada elemento de la lista uno por uno y lo guarda en la variable `nombre` durante esa repeticion.

### Recorrer un string caracter por caracter

Los strings tambien son recorribles:

```python
palabra = "Python"

for letra in palabra:
    print(letra)
```

Resultado:
```
P
y
t
h
o
n
```

---

## El ciclo `while`

Usa `while` cuando no sabes exactamente cuantas repeticiones necesitas, sino que quieres repetir **mientras una condicion sea verdadera**.

```python
while condicion:
    instrucciones
```

Ejemplo: contar hasta 5

```python
contador = 1

while contador <= 5:
    print(contador)
    contador = contador + 1
```

Resultado:
```
1
2
3
4
5
```

En cada repeticion, el programa revisa si `contador <= 5`. Si es `True`, ejecuta el bloque. Si es `False`, sale del ciclo.

**Muy importante:** asegurate de que la condicion eventualmente se vuelva `False`. Si no, el ciclo corre para siempre y el programa se congela. Eso se llama **ciclo infinito**.

```python
# CICLO INFINITO - no ejecutes esto
while True:
    print("Esto nunca para")
```

Si accidentalmente creas uno, puedes detener el programa con `Ctrl + C`.

### Pedir datos hasta que sean validos

Un uso muy comun de `while` es repetir una pregunta hasta obtener una respuesta aceptable:

```python
respuesta = ""

while respuesta != "si" and respuesta != "no":
    respuesta = input("Deseas continuar? (si/no) ").lower()

print(f"Elegiste: {respuesta}")
```

El programa seguira preguntando hasta que el usuario escriba exactamente `"si"` o `"no"`.

---

## Acumular valores dentro de un ciclo

Un patron muy util es usar una variable que **acumula** un resultado a lo largo del ciclo:

### Sumar una serie de numeros

```python
total = 0

for numero in range(1, 6):
    total = total + numero

print(f"La suma de 1 a 5 es: {total}")
```

Resultado:
```
La suma de 1 a 5 es: 15
```

### Contar cuantos elementos cumplen una condicion

```python
puntajes = [85, 42, 91, 60, 73, 38, 88]
aprobados = 0

for puntaje in puntajes:
    if puntaje >= 60:
        aprobados = aprobados + 1

print(f"Aprobaron {aprobados} de {len(puntajes)} estudiantes")
```

Resultado:
```
Aprobaron 5 de 7 estudiantes
```

---

## `break` y `continue`

Estas dos palabras clave te dan mas control sobre el flujo del ciclo.

### `break` — salir del ciclo antes de que termine

```python
for numero in range(1, 11):
    if numero == 6:
        break
    print(numero)
```

Resultado:
```
1
2
3
4
5
```

En cuanto `numero` llega a 6, `break` interrumpe el ciclo completamente.

### `continue` — saltar al siguiente paso sin ejecutar el resto del bloque

```python
for numero in range(1, 11):
    if numero % 2 == 0:
        continue
    print(numero)
```

Resultado:
```
1
3
5
7
9
```

Cuando el numero es par (`numero % 2 == 0`), `continue` salta el `print` y pasa al siguiente numero.

---

## `for` vs `while`: cuando usar cada uno

| Situacion | Ciclo recomendado |
|---|---|
| Sabes cuantas repeticiones necesitas | `for` |
| Recorres una lista o secuencia | `for` |
| Repites hasta que se cumpla una condicion | `while` |
| Pides datos hasta que sean validos | `while` |
| No sabes cuantas veces se repetira | `while` |

---

## Ejemplo completo: juego de adivinanza

```python
import random

numero_secreto = random.randint(1, 10)
intentos = 0
adivinado = False

print("Adivina el numero entre 1 y 10.")

while not adivinado:
    intento = int(input("Tu numero: "))
    intentos = intentos + 1

    if intento < numero_secreto:
        print("Demasiado bajo, intenta de nuevo.")
    elif intento > numero_secreto:
        print("Demasiado alto, intenta de nuevo.")
    else:
        adivinado = True

print(f"Correcto! Lo adivinaste en {intentos} intento(s).")
```

Este programa usa `while` porque no sabe cuantos intentos necesitara el usuario. Tambien usa `import random` para generar un numero al azar: aprenderemos mas sobre modulos en la guia 08.

---

## Ejercicio de esta guia

Escribe un programa que calcule la **tabla de multiplicar** de un numero elegido por el usuario.

Ejemplo de ejecucion:
```
De que numero quieres la tabla? 7

Tabla del 7:
7 x 1 = 7
7 x 2 = 14
7 x 3 = 21
7 x 4 = 28
7 x 5 = 35
7 x 6 = 42
7 x 7 = 49
7 x 8 = 56
7 x 9 = 63
7 x 10 = 70
```

**Reto extra:** Despues de mostrar la tabla, preguntale al usuario si quiere ver otra tabla. Si responde `"si"`, pide otro numero y repite. Si responde `"no"`, muestra un mensaje de despedida y termina.

**Reto avanzado:** Valida que el numero ingresado este entre 1 y 10. Si no lo esta, vuelve a pedirlo antes de mostrar la tabla.

---

## Resumen

| Concepto | Que aprendiste |
|---|---|
| `for` | Repite un bloque un numero definido de veces o recorre una coleccion |
| `while` | Repite un bloque mientras una condicion sea verdadera |
| `range(inicio, fin, paso)` | Genera una secuencia de numeros para usar con `for` |
| Variable acumuladora | Variable que se actualiza en cada repeticion para acumular un resultado |
| `break` | Sale del ciclo inmediatamente |
| `continue` | Salta al siguiente paso del ciclo |
| Ciclo infinito | Error comun: una condicion `while` que nunca se vuelve `False` |

---

## Que sigue

En la siguiente guia aprenderas sobre **funciones**: como organizar tu codigo en bloques reutilizables para no repetirte y hacer programas mas claros.

[Anterior: 03 — Condicionales](03_condicionales.md) | [Siguiente: 05 — Funciones](05_funciones.md)
