# Guia 03 — Condicionales

Hasta ahora tus programas ejecutan todas las instrucciones de arriba hacia abajo, siempre de la misma manera. Pero los programas utiles toman **decisiones**: muestran un mensaje diferente segun la edad del usuario, hacen una cosa si la respuesta es correcta y otra si no lo es, permiten el acceso solo si se cumple cierta condicion.

Para eso existen los **condicionales**.

---

## La instruccion `if`

Un condicional basico tiene esta forma:

```python
if condicion:
    instruccion
```

Se lee: "**Si** la condicion es verdadera, ejecuta la instruccion."

Ejemplo:

```python
edad = 15

if edad >= 12:
    print("Puedes participar en Technovation Girls")
```

Si `edad` es mayor o igual a 12, se muestra el mensaje. Si no, no pasa nada.

### La indentacion importa

Nota que la linea dentro del `if` tiene un sangrado (4 espacios o un tabulador). Eso se llama **indentacion** y es obligatorio en Python. Le dice a Python que esa instruccion pertenece al bloque del `if`.

```python
# Correcto
if edad >= 12:
    print("Bienvenida")

# Error: falta la indentacion
if edad >= 12:
print("Bienvenida")  # IndentationError
```

---

## `if` y `else`

Muchas veces quieres que pase algo si la condicion es verdadera, **y otra cosa** si es falsa:

```python
if condicion:
    # esto pasa si la condicion es True
else:
    # esto pasa si la condicion es False
```

Ejemplo:

```python
puntaje = 45

if puntaje >= 60:
    print("Aprobaste")
else:
    print("No aprobaste, pero puedes intentarlo de nuevo")
```

Solo uno de los dos bloques se ejecuta, nunca los dos.

---

## `if`, `elif` y `else`

Cuando hay mas de dos posibilidades, usas `elif` (abreviacion de "else if", que significa "si no, si..."):

```python
if condicion_1:
    # pasa si condicion_1 es True
elif condicion_2:
    # pasa si condicion_1 es False y condicion_2 es True
elif condicion_3:
    # pasa si las anteriores son False y condicion_3 es True
else:
    # pasa si ninguna condicion anterior fue True
```

Ejemplo con niveles de puntaje:

```python
puntaje = int(input("Cual es tu puntaje? "))

if puntaje >= 90:
    print("Excelente")
elif puntaje >= 75:
    print("Muy bien")
elif puntaje >= 60:
    print("Aprobaste")
else:
    print("Necesitas practicar mas")
```

Python revisa las condiciones en orden. En cuanto encuentra una que es `True`, ejecuta ese bloque y **se salta el resto**.

---

## Operadores de comparacion

Las condiciones se construyen con operadores de comparacion. Todos devuelven `True` o `False`:

| Operador | Significado | Ejemplo | Resultado |
|---|---|---|---|
| `==` | Igual a | `5 == 5` | `True` |
| `!=` | Diferente de | `5 != 3` | `True` |
| `>` | Mayor que | `7 > 10` | `False` |
| `<` | Menor que | `3 < 8` | `True` |
| `>=` | Mayor o igual que | `6 >= 6` | `True` |
| `<=` | Menor o igual que | `4 <= 2` | `False` |

**Cuidado con `=` vs `==`:**

- `=` asigna un valor a una variable: `edad = 15`
- `==` compara dos valores: `edad == 15` pregunta "es edad igual a 15?"

Confundir estos dos es uno de los errores mas comunes al empezar.

---

## Operadores logicos

Puedes combinar varias condiciones usando operadores logicos:

### `and` — las dos condiciones deben ser verdaderas

```python
edad = 14
tiene_permiso = True

if edad >= 12 and tiene_permiso:
    print("Puedes entrar")
```

### `or` — al menos una condicion debe ser verdadera

```python
dia = "sabado"

if dia == "sabado" or dia == "domingo":
    print("Es fin de semana")
```

### `not` — invierte el valor de la condicion

```python
esta_lloviendo = False

if not esta_lloviendo:
    print("Buen dia para salir")
```

### Tabla de verdad

| `a` | `b` | `a and b` | `a or b` | `not a` |
|---|---|---|---|---|
| True | True | True | True | False |
| True | False | False | True | False |
| False | True | False | True | True |
| False | False | False | False | True |

---

## Condicionales anidados

Puedes poner un `if` dentro de otro `if`. Esto se llama **anidamiento**:

```python
tiene_cuenta = True
saldo = 150

if tiene_cuenta:
    if saldo >= 100:
        print("Puedes realizar la compra")
    else:
        print("Saldo insuficiente")
else:
    print("Primero debes crear una cuenta")
```

Cada nivel de anidamiento agrega 4 espacios mas de indentacion. No abuses del anidamiento: si tienes mas de dos o tres niveles, probablemente hay una forma mas clara de escribir lo mismo.

---

## Comparar texto

Las comparaciones tambien funcionan con strings:

```python
respuesta = input("Deseas continuar? (si/no) ")

if respuesta == "si":
    print("Continuando...")
elif respuesta == "no":
    print("Hasta luego")
else:
    print("No entendi tu respuesta")
```

**Tip:** Las comparaciones de texto distinguen mayusculas y minusculas. `"si"` y `"Si"` no son iguales para Python. Para evitar problemas, puedes convertir la respuesta a minusculas antes de comparar:

```python
respuesta = input("Deseas continuar? (si/no) ").lower()

if respuesta == "si":
    print("Continuando...")
```

El metodo `.lower()` convierte cualquier texto a minusculas.

---

## Verificar si un valor esta en una lista

Con la palabra clave `in` puedes verificar si un valor pertenece a un conjunto de opciones:

```python
color = input("Cual es tu color favorito? ")

if color in ["rojo", "azul", "verde"]:
    print("Es un color primario")
else:
    print("No es un color primario")
```

Esto es mas claro que escribir `color == "rojo" or color == "azul" or color == "verde"`.

---

## Ejemplo completo: clasificador de edad

```python
nombre = input("Como te llamas? ")
edad = int(input("Cuantos anos tienes? "))

if edad < 6:
    categoria = "Infancia temprana"
elif edad < 12:
    categoria = "Ninez"
elif edad < 18:
    categoria = "Adolescencia"
else:
    categoria = "Adultez"

print(f"Hola, {nombre}. Segun tu edad ({edad} anos), estas en la etapa de: {categoria}.")
```

Ejemplo de ejecucion:
```
Como te llamas? Daniela
Cuantos anos tienes? 14
Hola, Daniela. Segun tu edad (14 anos), estas en la etapa de: Adolescencia.
```

---

## Ejercicio de esta guia

Escribe un programa que funcione como un **quiz de una pregunta**:

1. Le muestre al usuario una pregunta de cultura general (tu eliges cual)
2. Espere su respuesta con `input()`
3. Compare la respuesta con la respuesta correcta
4. Si es correcta, felicite al usuario
5. Si no, le diga cual era la respuesta correcta

**Reto extra:** Haz que la comparacion no distinga entre mayusculas y minusculas (usa `.lower()`).

**Reto avanzado:** Permite hasta dos intentos antes de revelar la respuesta.

---

## Resumen

| Concepto | Que aprendiste |
|---|---|
| `if` | Ejecuta un bloque si la condicion es verdadera |
| `else` | Ejecuta un bloque si la condicion es falsa |
| `elif` | Agrega mas condiciones entre `if` y `else` |
| Indentacion | Espaciado obligatorio que define los bloques de codigo |
| `==`, `!=`, `>`, etc. | Operadores que comparan valores y devuelven `True` o `False` |
| `and`, `or`, `not` | Operadores logicos para combinar condiciones |
| `.lower()` | Convierte texto a minusculas para comparaciones seguras |
| `in` | Verifica si un valor esta dentro de un conjunto de opciones |

---

## Que sigue

En la siguiente guia aprenderas sobre **ciclos**: como repetir instrucciones automaticamente sin tener que escribirlas una y otra vez.

[Anterior: 02 — Variables y tipos de datos](02_variables_y_tipos_de_datos.md) | [Siguiente: 04 — Ciclos](04_ciclos.md)
