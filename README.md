
import tkinter as tk
from tkinter import messagebox

# =========================
# FUNCIONES DE LA CALCULADORA
# =========================

def sumar(a, b):
    return a + b


def restar(a, b):
    return a - b


def multiplicar(a, b):
    return a * b


def dividir(a, b):
    if b == 0:
        raise ValueError("No se puede dividir entre cero.")
    return a / b


# =========================
# FUNCION PARA CALCULAR
# =========================

def calcular(operacion):
    try:
        num1 = float(entrada1.get())
        num2 = float(entrada2.get())

        if operacion == "+":
            resultado = sumar(num1, num2)

        elif operacion == "-":
            resultado = restar(num1, num2)

        elif operacion == "*":
            resultado = multiplicar(num1, num2)

        elif operacion == "/":
            resultado = dividir(num1, num2)

        etiqueta_resultado.config(
            text=f"Resultado: {resultado:g}"
        )

    except ValueError as error:
        etiqueta_resultado.config(text="Resultado: ")

        if str(error) == "No se puede dividir entre cero.":
            messagebox.showerror("Error", str(error))
        else:
            messagebox.showerror(
                "Error",
                "Debes ingresar números válidos."
            )


# =========================
# FUNCION PARA LIMPIAR
# =========================

def limpiar():
    entrada1.delete(0, tk.END)
    entrada2.delete(0, tk.END)
    etiqueta_resultado.config(text="Resultado: ")


# =========================
# CREAR VENTANA
# =========================

ventana = tk.Tk()
ventana.title("Mi Calculadora")
ventana.geometry("380x460")
ventana.resizable(False, False)
ventana.configure(bg="#202B3C")

# Titulo
titulo = tk.Label(
    ventana,
    text="MINI CALCULADORA",
    font=("Arial", 20, "bold"),
    bg="#202B3C",
    fg="white"
)
titulo.pack(pady=25)

# Primer numero
tk.Label(
    ventana,
    text="Primer número:",
    font=("Arial", 12),
    bg="#202B3C",
    fg="white"
).pack()

entrada1 = tk.Entry(
    ventana,
    font=("Arial", 16),
    justify="center"
)
entrada1.pack(pady=8)

# Segundo numero
tk.Label(
    ventana,
    text="Segundo número:",
    font=("Arial", 12),
    bg="#202B3C",
    fg="white"
).pack()

entrada2 = tk.Entry(
    ventana,
    font=("Arial", 16),
    justify="center"
)
entrada2.pack(pady=8)

# Botones de operaciones
tk.Label(
    ventana,
    text="Selecciona una operación:",
    font=("Arial", 12),
    bg="#202B3C",
    fg="white"
).pack(pady=12)

marco_botones = tk.Frame(ventana, bg="#202B3C")
marco_botones.pack()

operaciones = [
    ("+", 0, 0),
    ("-", 0, 1),
    ("*", 1, 0),
    ("/", 1, 1)
]

for simbolo, fila, columna in operaciones:
    boton = tk.Button(
        marco_botones,
        text=simbolo,
        font=("Arial", 18, "bold"),
        width=7,
        bg="#3498DB",
        fg="white",
        command=lambda op=simbolo: calcular(op)
    )
    boton.grid(row=fila, column=columna, padx=8, pady=8)

# Mostrar resultado
etiqueta_resultado = tk.Label(
    ventana,
    text="Resultado: ",
    font=("Arial", 16, "bold"),
    bg="#202B3C",
    fg="#2ECC71"
)
etiqueta_resultado.pack(pady=20)

# Boton limpiar
boton_limpiar = tk.Button(
    ventana,
    text="LIMPIAR",
    font=("Arial", 12, "bold"),
    width=15,
    bg="#E67E22",
    fg="white",
    command=limpiar
)
boton_limpiar.pack(pady=5)

# Boton salir
boton_salir = tk.Button(
    ventana,
    text="SALIR",
    font=("Arial", 12, "bold"),
    width=15,
    bg="#E74C3C",
    fg="white",
    command=ventana.destroy
)
boton_salir.pack(pady=5)

# Mantener ventana abierta
