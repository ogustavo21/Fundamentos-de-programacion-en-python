---
marp: true
theme: default
paginate: true
title: Fundamentos de Programación con Python y Flask
---


![bg](https://unav.edu.mx/wp-content/uploads/2025/07/isc-malla-2-scaled-1-2048x1295.webp)

---

# 🐍 Fundamentos de Programación con Python  
#### Semana Internacional: Clase espejo  
**Duración:** 110 minutos  
**Docente:** Ing. Gustavo Ordóñez Nuñez
**Contacto:** ogustavo@unav.edu.mx  
![bg left:40% 80%](https://upload.wikimedia.org/wikipedia/commons/c/c3/Python-logo-notext.svg)

---

## 🎯 Objetivos de Aprendizaje

- Comprender los fundamentos de Python (listas, tuplas, condicionales, ciclos, funciones).  
- Implementar una aplicación web sencilla con Flask.  
- Desarrollar pensamiento lógico y estructurado.  
- Aplicar los conocimientos en un mini-proyecto interactivo.

---

## 🧩 ¿Qué es Python?

- Lenguaje de programación interpretado y de alto nivel.  
- Sintaxis clara, ideal para principiantes.  
- Se usa en **ciencia de datos, IA, desarrollo web, automatización** y más.  

```python
print("Hola mundo desde Python!")
```
---

🧠 **Ejemplo:**  
Un programa que calcula la suma de dos números:
```python
a = int(input("Ingresa un número: "))
b = int(input("Ingresa otro número: "))
print("La suma es:", a + b)
```

---

## 📦 Listas

Las listas almacenan varios elementos en una sola variable.

```python
frutas = ["manzana", "pera", "uva"]
print(frutas[1])  # 👉 pera
```

### 🔧 Operaciones comunes

```python
frutas.append("naranja")  # Agregar
frutas.remove("pera")     # Eliminar
frutas[0] = "sandía"      # Modificar
```

📘 **Ejemplo práctico:**  
```python
numeros = [10, 20, 30]
suma = sum(numeros)
print("Suma total:", suma)
```

---

## 🔗 Tuplas

Similares a las listas, pero **inmutables** (no se pueden modificar).

```python
persona = ("Ana", 25, "Ingeniera")
print(persona[0])  # Ana
```

🧠 Se usan cuando los datos no deben cambiar.

📘 **Ejemplo práctico:**
```python
coordenadas = (10, 20)
x, y = coordenadas
print(f"Posición X:{x}, Y:{y}")
```

---

## 🧮 Listas de Tuplas

Permiten combinar listas (mutables) con tuplas (inmutables).

```python
tareas = [
    ("Leer un libro", False),
    ("Hacer ejercicio", True),
    ("Estudiar Python", False)
]
```

🔍 Ejemplo de recorrido:

```python
for tarea, hecha in tareas:
    if hecha:
        print(f"✅ {tarea} completada")
    else:
        print(f"❌ {tarea} pendiente")
```
---

📘 **Otro ejemplo:**
```python
alumnos = [("Ana", 9.5), ("Luis", 7.8), ("Sofía", 8.9)]
for nombre, calificacion in alumnos:
    print(f"{nombre} obtuvo {calificacion}")
```

---

## 🔀 Condicionales

Permiten ejecutar código dependiendo de una condición.

```python
edad = 18
if edad >= 18:
    print("Eres mayor de edad")
else:
    print("Eres menor de edad")
```

🎯 **Ejemplo práctico:**
```python
numero = int(input("Ingresa un número: "))
if numero % 2 == 0:
    print("Es par")
else:
    print("Es impar")
```
---

📘 **Ejemplo adicional:**
```python
nota = float(input("Ingresa tu calificación: "))
if nota >= 9:
    print("Excelente")
elif nota >= 7:
    print("Aprobado")
else:
    print("Reprobado")
```

---

## 🔁 Ciclos

Repetición controlada de instrucciones.

### 🔸 For

```python
for i in range(5):
    print("Número:", i)
```

### 🔸 While

```python
x = 0
while x < 3:
    print("x vale", x)
    x += 1
```
---

📘 **Ejemplo práctico:**  
```python
for fruta in ["manzana", "pera", "uva"]:
    print(f"Me gusta la {fruta}")
```

---

## ⚙️ Funciones

Bloques de código reutilizables.

```python
def saludar(nombre):
    print(f"Hola, {nombre}!")
```

📘 **Ejemplo práctico:**

```python
def promedio(a, b, c):
    return (a + b + c) / 3

print(promedio(8, 9, 10))
```
---

📘 **Otro ejemplo:**
```python
def convertir_a_fahrenheit(celsius):
    return celsius * 9/5 + 32

print(convertir_a_fahrenheit(25))
```

---


## 🌐 Introducción a Flask

Framework ligero para crear aplicaciones web con Python.

```bash
py -3 -m venv .venv
.venv\Scripts\activate
pip install flask
```

🧱 **Estructura básica:**
```python
from flask import Flask
app = Flask(__name__)

@app.route("/")
def home():
    return "Hola desde Flask!"

if __name__ == "__main__":
    app.run(debug=True)
```
---

```html
<!DOCTYPE html>
<html>
<head>
  <title>Lista de Tareas</title>
  <style>
    body { font-family: Arial; margin: 30px; }
    .hecha { text-decoration: line-through; color: gray; }
  </style>
</head>
<body>
  <h1>📝 Mi Pagina web</h1>
  <p>Hola mundo {{ nombres }}</p>


</body>
</html>

```
---

## 🖥️ Mini Proyecto: Lista de Tareas

📂 **Estructura de archivos:**
```
proyecto/
├── app.py
└── templates/
    └── index.html
```

---
📜 **Código de ejemplo (app.py):**
```python
from flask import Flask, render_template, request, redirect

app = Flask(__name__)

# Lista de tuplas: (nombre_tarea, completada)
tareas = [
    ("Estudiar Python", False),
    ("Leer un libro", True),
    ("Hacer ejercicio", False)
]

# --- Funciones básicas ---
def agregar_tarea(nombre):
    if nombre:  # Condicional
        tareas.append((nombre, False))

def marcar_completada(indice):
    if 0 <= indice < len(tareas):
        tarea, _ = tareas[indice]
        tareas[indice] = (tarea, True)

@app.route("/")
def index():
    return render_template("index.html", tareas=tareas)

@app.route("/agregar", methods=["POST"])
def agregar():
    nombre = request.form["nombre"]
    agregar_tarea(nombre)
    return redirect("/")

@app.route("/completar/<int:indice>")
def completar(indice):
    marcar_completada(indice)
    return redirect("/")

if __name__ == "__main__":
    app.run(debug=True)
```

---

## 🎨 Interfaz HTML (index.html)
```html
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <title>Gestor de Tareas</title>
    <style>
        body { font-family: Arial; background-color: #f8f9fa; padding: 20px; }
        h1 { color: #007BFF; }
        form { margin-bottom: 20px; }
        .tarea { padding: 10px; border-bottom: 1px solid #ccc; }
        .hecha { text-decoration: line-through; color: gray; }
        button { margin-left: 10px; }
    </style>
</head>
<body>
    <h1>Gestor de Tareas</h1>
    <form method="POST" action="/agregar">
        <input type="text" name="nombre" placeholder="Nueva tarea" required>
        <button type="submit">Agregar</button>
    </form>

    {% for tarea, hecha in tareas %}
        <div class="tarea">
            {% if hecha %}
                <span class="hecha">{{ tarea }}</span>
            {% else %}
                <span>{{ tarea }}</span>
                <a href="/completar/{{ loop.index0 }}">✔️ Completar</a>
            {% endif %}
        </div>
    {% endfor %}
</body>
</html>
```
---
## 🧩 Ejecución
```bash
(.venv) set FLASK_APP=app.py

(.venv) flask run

 * Running on http://127.0.0.1:5000

```
---

## 🧩 Quiz Final (Kahoot)

1️⃣ ¿Qué tipo de datos son inmutables?  
2️⃣ ¿Qué instrucción se usa para ciclos repetitivos?  
3️⃣ ¿Qué comando inicia Flask?  
4️⃣ ¿Cómo se define una función en Python?  
5️⃣ ¿Qué estructura contiene pares de datos relacionados?  

---

## 📚 Referencias

- [Documentación oficial de Python](https://docs.python.org/3/)  
- [Documentación de Flask](https://flask.palletsprojects.com/)  
- [Marp para presentaciones Markdown](https://marp.app/)

---

## 👨‍🏫 Fin de la Clase

¡Excelente trabajo! 🎉  
Recuerda practicar y modificar el proyecto para afianzar tus conocimientos.
