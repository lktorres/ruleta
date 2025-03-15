import random
# Inicio del jugador
jugador = {
    "saldo": 100,
    "apuestas": [],
    "ganancias": 0,
    "victorias": 0,
    "derrotas": 0
}

# Configuración de la ruleta
numeros_rojos = {1,3,5,7,9,12,14,16,18,19,21,23,25,27,30,32,34,36}
secciones = {
    "1-12": set(range(1, 13)),
    "13-24": set(range(13, 25)),
    "25-36": set(range(25, 37))
}

def girar_ruleta():
    return random.randint(1, 36)

def realizar_apuesta():
    print("\nOpciones de apuesta:")
    print("1. Número específico (paga 20x)")
    print("2. Sección (1-12, 13-24, 25-36) (paga 5x)")
    print("3. Color (rojo o negro) (paga 2x)")
    
    tipo = input("Seleccione una opción (1-3): ")

    if tipo not in {"1", "2", "3"}:
        print("Opción inválida.")
        return

    monto = int(input(f"Saldo disponible: {jugador['saldo']}\nIngrese el monto a apostar: "))
    
    if monto > jugador["saldo"] or monto <= 0:
        print("Apuesta inválida.")
        return

    apuesta = {"tipo": tipo, "monto": monto}
    
    if tipo == "1":
        apuesta["valor"] = int(input("Ingrese el número (1-36): "))
        if apuesta["valor"] not in range(1, 37):
            print("Número inválido.")
            return
    elif tipo == "2":
        apuesta["valor"] = input("Ingrese la sección (1-12, 13-24, 25-36): ")
        if apuesta["valor"] not in secciones:
            print("Sección inválida.")
            return
    elif tipo == "3":
        apuesta["valor"] = input("Ingrese el color (rojo/negro): ").lower()
        if apuesta["valor"] not in {"rojo", "negro"}:
            print("Color inválido.")
            return

    jugador["apuestas"].append(apuesta)
    jugador["saldo"] -= monto

    print(f"Apuesta realizada: {apuesta}")

def calcular_resultado():
    if not jugador["apuestas"]:
        print("\nNo hay apuestas realizadas.")
        return
    
    resultado = girar_ruleta()
    color = "rojo" if resultado in numeros_rojos else "negro"

    print(f"\nLa ruleta giró... ¡Salió el número {resultado} ({color})!\n")
    
    for apuesta in jugador["apuestas"]:
        monto = apuesta["monto"]
        if apuesta["tipo"] == "1": # Apuesta a número
            if apuesta["valor"] == resultado:
                premio = monto * 20
                print(f"¡Ganaste {premio} coins apostando al número {resultado}!")
                jugador["saldo"] += premio
                jugador["ganancias"] += premio
                jugador["victorias"] += 1
            else:
                jugador["derrotas"] += 1
        elif apuesta["tipo"] == "2": # Apuesta a sección
            if resultado in secciones[apuesta["valor"]]:
                premio = monto * 5
                print(f"¡Ganaste {premio} coins apostando a la sección {apuesta['valor']}!")
                jugador["saldo"] += premio
                jugador["ganancias"] += premio
                jugador["victorias"] += 1
            else:
                jugador["derrotas"] += 1
        elif apuesta["tipo"] == "3": # Apuesta a color
            if apuesta["valor"] == color:
                premio = monto * 2
                print(f"¡Ganaste {premio} coins apostando al color {color}!")
                jugador["saldo"] += premio
                jugador["ganancias"] += premio
                jugador["victorias"] += 1
            else:
                jugador["derrotas"] += 1

    jugador["apuestas"] = [] # Reset apuestas después de la ronda

def mostrar_estadisticas():
    print("\n=== Estadísticas ===")
    print(f"Saldo actual: {jugador['saldo']} coins")
    print(f"Total ganado: {jugador['ganancias']} coins")
    print(f"Victorias: {jugador['victorias']}, Derrotas: {jugador['derrotas']}")
    
    total_partidas = jugador["victorias"] + jugador["derrotas"]
    if total_partidas > 0:
        exito = jugador["victorias"] / total_partidas * 100
        print(f"Porcentaje de éxito: {exito:.2f}%")
    else:
        print("Aún no hay estadísticas suficientes.")

def menu():
    while jugador["saldo"] > 0:
        print("\n--- Ruleta Online ---")
        print("1. Realizar apuesta")
        print("2. Girar ruleta")
        print("3. Ver estadísticas")
        print("4. Salir")
        
        opcion = input("Seleccione una opción: ")

        if opcion == "1":
            realizar_apuesta()
        elif opcion == "2":
            calcular_resultado()
        elif opcion == "3":
            mostrar_estadisticas()
        elif opcion == "4":
            print("Saliendo del juego. ¡Gracias por jugar! diversion y emocion en un solo lugar")
            break
        else:
            print("Opción inválida.")

    if jugador["saldo"] <= 0:
        print("\nTe has quedado sin saldo. ¡Juego terminado.!")

# Ejecutar el juego
menu()
