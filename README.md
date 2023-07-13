#productora de creativos.cl, necesita desarrollar una aplicación que permita controlar la venta de entradas...

import datetime

entradas_disponibles = 100
ganancias_totales = 0
asistentes = []
ubicaciones_disponibles = ['Platinum']*20 + ['Gold']*30 + ['Silver']*50
ubicaciones_vendidas = []

def comprar_entradas():
    global entradas_disponibles, ganancias_totales, asistentes, ubicaciones_disponibles, ubicaciones_vendidas
    cantidad = int(input("Ingrese la cantidad de entradas que desea comprar (1-3): "))
    
    run = input("Ingrese el RUN de la persona que ocupará la ubicación: ")

    if run in asistentes:
        print("Operación realizada correctamente.")
        
    else:
        print("El RUN ingresado no está registrado en la lista de asistentes.")
    
    print("Ubicaciones disponibles:")
    for i, ubicacion in enumerate (ubicaciones_disponibles):
        if ubicacion == 'Platinum':
            precio = 120000
        elif ubicacion == 'Gold':
            precio = 80000
        else:
            precio = 50000
        
        print(f"{i+1}. {ubicacion} - Precio: {precio}")
    
    ubicaciones_seleccionadas = []
    for _ in range (cantidad):
        ubicacion_seleccionada = int(input("Seleccione una ubicación: "))
        
        if ubicacion_seleccionada < 1 or ubicacion_seleccionada > len(ubicaciones_disponibles):
            print("Ubicación inválida, Por favor selecione una ubicacion que sea valida.")
            return
        
        elif ubicaciones_disponibles [ubicacion_seleccionada-1] != 'Platinum':
            print("la ubicacion selecionada no se encuentra disponible.")
            return
        
        ubicaciones_seleccionadas.append(ubicacion_seleccionada)
    
    run = input("Ingrese el RUN de la persona que ocupará la ubicación: ")
    
    if run in asistentes:
        for ubicacion_seleccionada in ubicaciones_seleccionadas:
            ubicaciones_disponibles [ubicacion_seleccionada-1] = 'X'
            ubicaciones_vendidas.append (ubicacion_seleccionada)
        
        if ubicacion_seleccionada <= 20:
            ganancias_totales += cantidad * 120000
        elif ubicacion_seleccionada <= 50:
            ganancias_totales += cantidad * 80000
        else:
            ganancias_totales += cantidad * 50000
        
        print("Operación realizada correctamente.")
    else:
        print("El RUN ingresado no está en la lista de asistentes.")

def mostrar_ubicaciones():
    print("Estado actual de la venta de entradas:")
    for i, ubicacion in enumerate(ubicaciones_disponibles):
        if i+1 in ubicaciones_vendidas:
            estado = 'Vendida'
        else:
            estado = 'Disponible'
        
        print(f"{i+1}. {ubicacion} - Estado: {estado}")

def ver_listado_asistentes():
    print("Listado de asistentes por RUN:")
    for asistente in sorted(asistentes):
        run = asistente
        asientos = asistentes.count(asistente)
        print(f"RUN: {run}, Asientos: {asientos}")

def mostrar_ganancias_totales():
    print(f"Ganancias totales: ${ganancias_totales}")

def salir():
    print(f"Hasta luego {datetime.datetime.now().strftime('%Y-%m-%d')}")
while True:
    print("----- MENÚ -----")
    print("1. Comprar entradas")
    print("2. Mostrar ubicaciones disponibles")
    print("3. Ver listado de asistentes")
    print("4. Mostrar ganancias totales")
    print("5. Salir")
    
    opcion = input ("Ingrese una opción: ")

    if opcion == '1':
        comprar_entradas()
    elif opcion == '2':
        mostrar_ubicaciones()
    elif opcion == '3':
        ver_listado_asistentes()
    elif opcion == '4':
        mostrar_ganancias_totales()
    elif opcion == '5':
        salir()
        break
    else:
        print("Opción inválida. Por favor ingrese una opción válida.")



































