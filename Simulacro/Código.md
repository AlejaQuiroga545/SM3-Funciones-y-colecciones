# GESTIÓN DE INVENTARIO CON FUNCIONES Y COLECCIONES

# 1. Añadir productos
def añadir_producto(inventario):

    nombre = input("Nombre del producto: ").lower()
    while True:
        try:
            precio = float(input("Precio: "))
            if precio > 0:
                break  # Sale del bucle si el precio es positivo
            else:
                print("Oops, el precio debe ser un número positivo, intenta nuevamente.")
        except ValueError:
            print("Por favor, ingresa un número válido para el precio.")

    while True:
        try:
            cantidad = int(input("Cantidad disponible: "))  # Pide la cantidad y la convierte a entero
            if cantidad >= 0:
                break  # Sale del bucle si la cantidad es positiva o cero
            else:
                print("Oops, introduce un número entero positivo o cero.")
        except ValueError:
            print("Por favor, ingresa un número entero.")

    inventario[nombre] = {'Precio': precio, 'Cantidad': cantidad}  # Agrega el producto al inventario como un diccionario
    print(f"\n✅ Tu producto {nombre} ha sido agregado correctamente.")


# 2. Consultar productos
def buscar_productos(inventario):
    
    if not inventario:
        print("\nOops, el inventario está vacío.")
        return

    print("\n🛒 Productos en el inventario:")
    for nombre in inventario:
        print(f"- {nombre}")

    nombre_buscar = input("\nIngresa el nombre del producto que desea consultar 🔎  ").lower()
    
    if nombre_buscar in inventario:
        precio = inventario[nombre_buscar]['Precio']
        cantidad = inventario[nombre_buscar]['Cantidad']
        
        print(f"\nProducto: {nombre_buscar}")
        if type(precio) == int:
            print (precio)
        else: (precio)
        print(f"Precio: ${precio: .3f}")
        print(f"Cantidad: {cantidad}")
    else:
        print(f"Oops, el producto '{nombre_buscar}' no está en nuestro inventario. 🤔")


# 3. Actualizar precios
def actualizar_precio(inventario, nombre, precio_actualizado):
    
    if not inventario:
        print("\nEl inventario está vacío. No hay productos para actualizar. 🫣")
        return

    print("🛒 Productos en el inventario:")
    for nombre in inventario:
        print(f"- {nombre}")

    nombre_actualizar = input("📍 Ingresa el nombre del producto del cual quieres actualizar el precio: ").lower()
    if nombre_actualizar not in inventario:
        print(f"Ops, el producto '{nombre_actualizar}' no está en tu inventario 🫣 intenta nuevamente.")
        return

    while True:
        try:
            precio_actualizado = float(input(f"Nuevo precio para {nombre_actualizar}: "))
            if precio_actualizado > 0:
                break
            else:
                print("El precio debe ser un número positivo.")
        except ValueError:
            print("Por favor, ingresa un número válido para el precio.")

    inventario[nombre_actualizar]['Precio'] = precio_actualizado
    print(f"✅ El precio de {nombre_actualizar} ha sido actualizado a ${precio_actualizado}.")


# 4. Eliminar productos
def eliminar_producto(inventario, nombre):

    if nombre in inventario:
        del inventario[nombre]  # Elimina el producto del diccionario
        print(f"✅ El producto {nombre} ha sido eliminado del inventario correctamente.")
    else:
        print(f"Oops, el producto '{nombre}' no se encuentra en nuestro inventario. 🫣")


# Calcular el valor total de los productos del inventario
def valor_total(inventario):
    """
    Calcula el valor total del inventario sumando el valor de cada producto
    (precio * cantidad).
    """
    total = sum(item['Precio'] * item['Cantidad'] for item in inventario.values())
    print(f"✅ El valor total de tu inventario es ${total}")  # Muestra el valor total con formato de moneda



# Crear menú
def menu():
    """
    Función principal que muestra el menú de opciones al usuario
    y permite interactuar con las diferentes funcionalidades del inventario.
    """
    inventario = {}  # Inicializa el diccionario que almacenará el inventario

    print("\nHola coder, bienvenido a tu Gestión de inventario 🛒. ¿Qué deseas hacer?")

    while True:
        print('-' * 20)
        print("1. Añadir producto")
        print("2. Consultar productos")
        print("3. Actualizar precio")
        print("4. Eliminar producto")
        print("5. Calcular el valor total de tu inventario")
        print("6. Salir")

        try:
            opc = int(input("Selecciona una opción (1-6): "))  # Pide la opción al usuario y la convierte a entero

            if opc == 1:
                añadir_producto(inventario)  # Llama a la función para añadir un producto

            elif opc == 2:
                buscar_productos(inventario)  # Llama a la función para buscar un producto

            elif opc == 3:
                actualizar_precio(inventario)  # Llama a la función para actualizar el precio

            elif opc == 4:
                nombre = input("Nombre del producto a eliminar: ").lower()
                eliminar_producto(inventario, nombre)  # Llama a la función para eliminar un producto

            elif opc == 5:
                valor_total(inventario)  # Llama a la función para calcular el valor total

            elif opc == 6:
                print("Saliendo del programa...")
                break  # Sale del bucle del menú

            else:
                print("Oops, ingresa una opción válida por favor.")
        except ValueError:
            print("Por favor, ingresa un número del 1 al 6.")

menu()  # Llama a la función menú para iniciar el programa
