```python
# Simulacro de prueba

# Info que deseamos introducir en nuestro diccionario

def añadir_libros(Libros):
    Titulo = input("Título del libro: ")
    Autor = input("Nombre del autor: ")
    Copias = int(input ("Cantidad de copias disponibles: "))
    Genero = input ("Género literario: ")
    
    Libros [Titulo] = {'Autor': Autor, 'Copias': Copias, 'Género':Genero}
    print(f"El libro '{Titulo}' ha sido agregado exitosamente")

biblioteca = {
    
}

while True:
    print ("\nDeseas agregar un nuevo libro? ( si / no ): ")
    respuesta= input().lower()
    
    if respuesta == 'si':
        print ("\nIngresa la información del libro")
        añadir_libros (biblioteca)
        
    elif respuesta == 'no':
        print ("Tus libros han sido agregados a nuestra biblioteca")
        break
    else:
        print ("Oops, debes introducir 'si' o 'no', por favor intenta nuevamente")
        
print ("\n--- Contenido de la Biblioteca ---")
if biblioteca:  # Verificar si la biblioteca no está vacía
    for titulo, detalles in biblioteca.items():
        print(f"Título: {titulo}")
        print(f"  Autor: {detalles['Autor']}")
        print(f"  Copias disponibles: {detalles['Copias']}")
        print(f"  Género: {detalles['Género']}")
        print("-" * 40) # Imprimir una línea separadora

# Buscar libros por título

def buscar_libros(Libros, buscar_titulo):
    resultado = []
    buscar_titulo = buscar_titulo.lower()
    
    for titulo, detalles in Libros.items:
        if buscar_titulo in titulo:
            resultado.append((titulo, detalles))
    return resultado
``
