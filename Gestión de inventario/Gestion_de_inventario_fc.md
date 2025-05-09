# Gestión de inventario con funciones y colecciones 🚀
¡Hola! Crearemos un programa en Python que permita al equipo de una tienda añadir, consultar, actualizar y eliminar productos del inventario de manera eficiente, así como calcular el valor total del inventario.

## ✅ 1. Añadir productos

〰️ Cada producto debe estar definido por su nombre, precio y cantidad disponible.

〰️ Esta información será almacenada de modo que el inventario pueda crecer dinámicamente.

```python
GESTIÓN DE INVENTARIO CON FUNCIONES Y COLECCIONES

#  Creamos nuestro diccionario (vacío) para almacenar nuestros productos
inventario = {}

# 1. Añadir productos

def añadir_producto(inventario):

    nombre = input("Nombre del producto: ").lower()

    while True: # Creamos un bucle para asegurar un precio válido
        precio_str = input("Precio: ")
        try:
            precio = float(precio_str.replace(".", "")) # Permite puntos como separador y las elimina para float
            if precio > 0:
                break # Salimos del bucle si el precio es válido
            else:
                print("\nOops, el precio debe ser un número válido. 🫢")
        except ValueError:
            print("\nPor favor, ingresa un número válido para el precio.")


    while True: # Creamos un bucle para asegurar una cantidad válida
        try:
            cantidad = int(input("Cantidad disponible: "))
            if cantidad >= 0:
                break
            else:
                print("\nOops, ingresa un número válido. 🫢")
        except ValueError:
            print("\nPor favor, ingresa un número válido.")


    inventario[nombre] = (precio_str, precio, cantidad) # Agregamos el producto al diccionario
    print(f"\nTu producto '{nombre}' ha sido agregado correctamente. 🥳")


```

## ✅ 2. Consultar productos

〰️ Se debe poder buscar un producto por su nombre y obtener detalles como su precio y cantidad disponible.

〰️ Si el producto no está en el inventario, se debe notificar adecuadamente.

```python
# 2. Consultar productos

def buscar_productos(inventario, nombre):
    if nombre in inventario: # Verificamos si el producto existe en el inventario
        producto = inventario[nombre] # Busca en el diccionario de inventario el nombre, y los valores asociado a él, los guarda en la variable

        precio_str, precio, cantidad = producto # Desempaquetamos la tupla directamente

        print(f"➡️  Producto: {nombre.capitalize()}") # Usamos el nombre original consultado
        print(f"➡️  Precio: {precio_str}")
        print(f"➡️  Cantidad: {cantidad}")
    else:
        print(f"\nOops, el producto '{nombre}' no está en tu inventario. 🫢")
```

## ✅ 3. Actualizar precios

〰️ El programa debe permitir al usuario seleccionar un producto e introducir un nuevo precio, asegurando que este se actualice correctamente en el inventario.

```python
# 3. Actualizar precios

def actualizar_precio(inventario, nombre):

    if nombre not in inventario: # Verificamos si el producto existe
        print("Este producto no está en tu inventario 🫢... Intenta nuevamente")
        return

    precio_anterior_str, precio_anterior, cantidad_anterior = inventario[nombre] # Desempaquetamos la tupla

    print(f"⏪ Precio anterior de '{nombre}': {precio_anterior_str}")

    while True: # Creamos un bucle para asegurar un nuevo precio válido
        nuevo_precio_str = input("⏩ Ingresa el nuevo precio: ")
        try:
            nuevo_precio = float(nuevo_precio_str.replace(".", ""))
            if nuevo_precio > 0:
                break # Salimos del bucle si el nuevo precio es válido
            else:
                print("\nOops 🫢... Debes ingresar un precio válido.")
        except ValueError:
            print("\nPor favor, ingresa un número válido para el precio.")

    inventario[nombre] = (nuevo_precio_str, nuevo_precio, cantidad_anterior) # Actualizamos la tupla completa
    print(f"\n✳️  El precio de '{nombre}' ha sido actualizado a $ {nuevo_precio_str}.")
```

# ✅ 4. Eliminar productos

〰️ El programa debe permitir al usuario eliminar productos del inventario de manera segura

```python
# 4. Eliminar productos

def eliminar_producto(inventario, nombre):

    if nombre in inventario: # Verificamos si el producto existe
        del inventario[nombre] # Eliminamos el producto del diccionario
        print(f"\nEl producto '{nombre}' ha sido eliminado de tu inventario correctamente. ✅")
    else:
        print(f"El producto '{nombre}' no se encuentra en tu inventario. ❌")
```

# ✅ 5. Calcular el valor total del inventario

〰️ El programa debe calcular el valor total de los productos en inventario y mostrarlo al usuario.

〰️ Para ello, utilizarás una función anónima (lambda) que facilite este cálculo.

```python
5. Calcular el valor total de los productos del inventario

def valor_total(inventario):
    calcular_valor = lambda producto: producto[1] * producto[2] # Tomamos la información de un producto (la tupla) y devolvemos el precio (índice 1) multiplicado por la cantidad (índice 2).
    total = sum(calcular_valor(producto) for producto in inventario.values()) # Para cada tupla de producto, calcula su valor individual y luego suma todos los valores.
    print(f"\n✳️   El valor total de tu inventario es $ {total:,.2f}")
```

# ✅ Creamos nuestro menú

```python
def menu():
    print("\n¡Hola coder, bienvenido a tu Gestión de inventario! 🚀. ¿Qué deseas hacer?")

    while True: # Bucle principal del menú
        print('-' * 20)
        print("1. Añadir producto")
        print("2. Consultar productos")
        print("3. Actualizar precio")
        print("4. Eliminar producto")
        print("5. Calcular el valor total de tu inventario")
        print("6. Salir")

        opc_str = input("\n✳️  Selecciona una opción (1-6): ")

        if not opc_str.isdigit(): # Verificamos si la entrada es un número (.isdigit() se utiliza para verificar si todos los caracteres dentro de una cadena son dígitos (0-9))
            print("\n Oops 🫢 ...Por favor, ingresa un número válido para la opción.")
            continue # Volvemos al inicio del bucle

        opc = int(opc_str) # Convertimos la entrada a entero


        if opc == 1: # Op 1. Añadir producto
            print("Agrega el nuevo producto\n")
            añadir_producto(inventario)


        elif opc == 2: # Op 2. Consultar producto
            if not inventario: # Verificamos si el inventario está vacío
                print("No hay productos en tu inventario. ✳️")
                continue # Volvemos al inicio del bucle

            print("\nProductos disponibles:\n")
            for nombre in inventario:
                print(f"\n✅ {nombre.capitalize()}") # Mostramos los nombres con la primera letra en mayúscula
            nombre_consultar = input("\nNombre del producto que quieres consultar 🔎 ").lower().strip()
            buscar_productos(inventario, nombre_consultar)


        elif opc == 3: # Op 3. Actualizar precio
            if not inventario: # Verificamos si el inventario está vacío
                print("No hay productos en tu inventario para actualizar. ✳️")
                continue # Volvemos al inicio del bucle
            print("\nProductos disponibles:\n")

            for nombre in inventario:
                print(f"✅ {nombre.capitalize()}") # Mostramos los nombres con la primera letra en mayúscula
            nombre_actualizar = input("\nNombre del producto a actualizar 📌: \n").lower()
            actualizar_precio(inventario, nombre_actualizar)


        elif opc == 4: # Op 4. Eliminar producto
            if not inventario: # Verificamos si el inventario está vacío
                print("\nNo hay productos en el inventario para eliminar. 🗑️")
                continue # Volvemos al inicio del bucle
            print("\n📍 Productos disponibles:\n")

            for nombre in inventario:
                print(f"✅ {nombre.capitalize()}") # Mostramos los nombres con la primera letra en mayúscula
            nombre_eliminar = input("\n🗑️   Nombre del producto a eliminar: ").lower()
            eliminar_producto(inventario, nombre_eliminar)


        elif opc == 5: # Op 5. Calcular el valor total
            valor_total(inventario)


        elif opc == 6: # Opción para salir
            print("¡Hasta pronto coder! 🚀")
            break # Salimos del bucle principal
        else: # Opción inválida
            print("Oops, debes introducir un número entre 1 y 6 🫢. Intenta nuevamente.")

# Ejecutar el menú principal
menu()
```
