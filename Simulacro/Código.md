```python
# GESTIÓN DE INVENTARIO CON FUNCIONES Y COLECCIONES

# 1. Añadir productos

def añadir_producto(inventario, nombre, precio, cantidad):
    nombre = input("Nombre del producto: ") .lower()
    while True:
        try:
            precio = float(input("Precio: "))
            if precio > 0:
                break
            else:
                print("Oops, el precio debe ser un número positivo.")
        except ValueError:
            print("Por favor, ingresa un número válido para el precio.")

    while True:
        try:
            cantidad = int(input("Cantidad disponible: "))
            if cantidad >= 0:
                break
            else:
                print("Oops, introduce un número entero positivo o cero.")
        except ValueError:
            print("Por favor, ingresa un número entero.")

    inventario[nombre] = {'Precio': precio, 'Cantidad': cantidad}
    print(f"Tu producto {nombre} ha sido agregado correctamente.")

inventario = {}

while True:
    print ("¿Deseas agregar un nuevo producto? ( si / no ): ")
    answer = input().lower()

    if answer == 'si':
        print ("Agrega el nuevo producto")
        añadir_producto(inventario)
    elif answer == 'no':
        print ("Proceso finalizado correctamente")
        break
    else:
        print ("Oops, debes introducir 'si' o 'no', intentemos nuevamente")


# 2. Consultar productos

def buscar_productos(inventario, nombre):
    if nombre in inventario:
        precio, cantidad = inventario[nombre]
        print (f"Producto: {nombre}")
        print (f"Precio: {precio}")
        print (f"Cantidad: {cantidad}")
    else: (f"El producto '{nombre} no está en nuestro inventario")


# 3. Actualizar precios

def actualizar_precio (inventario, nombre, precio_actualizado):
    if nombre not in inventario:
        print ("Este producto no está en nuestro inventario, intenta nuevamente")
        return
    
    if not isinstance (precio_actualizado(int, float)) or precio_actualizado <=0:
        print ("Ingresa un precio válido por favor")
        return
    
    cantidad = inventario[nombre]['Cantidad']
    inventario[nombre]['Precio'] = precio_actualizado
    print (f"El precio de {nombre} ha sido actualiza a $ {precio_actualizado}.")


# 4. Eliminar productos

def eliminar_producto(inventario, nombre, eliminar_prod):
    if nombre in inventario:
        del inventario[nombre]
        print (f"El producto {nombre} ha sido eliminado del inventario correctamente.")
    else: print (f"El producto {nombre} no se encuentra en nuestro inventario.")


# Calcular el valor total de los productos del inventario

def valor_total (inventario):
    total = sum(lambda item:item[1][0] * item [1][1], inventario.items(()))
    print (f"El valor total de tu inventario es $ {total:,.2f}")


# Crear menú 

def menu():
    inventario = {}

    print("Hola coder, bienvenido a tu Gestión de inventario. ¿Qué deseas hacer?")

    while True:
        print ('-'*20)
        print ("1. Añadir producto")
        print ("2. Consultar productos")
        print ("3. Actualizar precio")
        print ("4. Eliminar producto")
        print ("5. Calcular el valor total de tu inventario")
        print ("6. Salir")

        opc = int(input("Selecciona una opción (1-6): "))

        if opc == "1":
            nombre = input("Nombre del producto: ")
            try:
                precio = float(input("Precio: "))
                cantidad = int(input("Cantidad: "))
            except ValueError:
                print("Precio y Cantidad deben ser números válidos. ")
                continue
            añadir_producto(inventario, nombre, precio, cantidad)


        elif opc == "2":
            if not inventario:
                print ("No hay productos en el invetario")
            print ("Productos disponibles")
            for nombre in inventario:
                print (f"✅ {nombre}")

            nombre = input ("Nombre del producto que quieres consultar: ")
            buscar_productos(inventario, nombre) 
            continue
        

        elif opc == "3":
            
``
