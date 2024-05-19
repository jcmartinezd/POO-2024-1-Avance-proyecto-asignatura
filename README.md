class Animal:
    def __init__(self, nombre, edad, puntos):
        self.nombre = nombre
        self.edad = edad
        self.puntos = puntos

    def __str__(self):
        return f"Nombre: {self.nombre}, Edad: {self.edad}, Puntos: {self.puntos}"

class Perro(Animal):
    def __init__(self, nombre, raza, edad, puntos):
        super().__init__(nombre, edad, puntos)
        self.raza = raza

    def __str__(self):
        return super().__str__() + f", Raza: {self.raza}"

class ExposicionCanina:
    def __init__(self):
        self.perros = []

    def limpiar_pantalla(self):
        os.system('cls' if os.name == 'nt' else 'clear')

    def agregar_perro(self, perro):
        self.perros.append(perro)

    def listar_perros(self, criterio):
        if criterio not in ["raza", "puntos", "edad"]:
            raise ValueError("Criterio de ordenamiento no válido.")
        
        perros_ordenados = sorted(self.perros, key=lambda x: getattr(x, criterio))
        
        for perro in perros_ordenados:
            print(perro)
        input("Presione Enter para continuar...")
        self.limpiar_pantalla()

    def mostrar_info_perro(self, nombre):
        for perro in self.perros:
            if perro.nombre == nombre:
                print(perro)
                break
        else:
            print("Perro no encontrado.")
        input("Presione Enter para continuar...")
        self.limpiar_pantalla()

    def buscar_perro_por_nombre(self, nombre):
        for perro in self.perros:
            if perro.nombre == nombre:
                print(perro)
                break
        else:
            print("Perro no encontrado.")
        input("Presione Enter para continuar...")
        self.limpiar_pantalla()

    def perro_ganador(self):
        if not self.perros:
            print("No hay perros registrados.")
        else:
            ganador = max(self.perros, key=lambda x: x.puntos)
            print("El perro ganador es:")
            print(ganador)
        input("Presione Enter para continuar...")
        self.limpiar_pantalla()

    def perro_menor_puntuacion(self):
        if not self.perros:
            print("No hay perros registrados.")
        else:
            menor_puntuacion = min(self.perros, key=lambda x: x.puntos)
            print("El perro con menor puntuación es:")
            print(menor_puntuacion)
        input("Presione Enter para continuar...")
        self.limpiar_pantalla()

    def perro_mas_viejo(self):
        if not self.perros:
            print("No hay perros registrados.")
        else:
            mas_viejo = max(self.perros, key=lambda x: x.edad)
            print("El perro más viejo es:")
            print(mas_viejo)
        input("Presione Enter para continuar...")
        self.limpiar_pantalla()

def menu():
    print("\n--- MENÚ ---")
    print("1. Mostrar lista de perros ordenada")
    print("2. Mostrar información de un perro")
    print("3. Registrar nuevo perro")
    print("4. Buscar perro por nombre")
    print("5. Perro ganador de la exposición")
    print("6. Perro con menor puntuación")
    print("7. Perro más viejo")
    print("8. Salir")
    opcion = input("Seleccione una opción: ")
    return opcion

if __name__ == "__main__":
    exposicion = ExposicionCanina()

    while True:
        try:
            opcion = menu()

            if opcion == "1":
                criterio = input("Ingrese el criterio de ordenamiento (raza/puntos/edad): ")
                exposicion.listar_perros(criterio)
            elif opcion == "2":
                nombre = input("Ingrese el nombre del perro: ")
                exposicion.mostrar_info_perro(nombre)
            elif opcion == "3":
                nombre = input("Nombre del perro: ")
                raza = input("Raza del perro: ")
                edad = int(input("Edad del perro: "))
                puntos = int(input("Puntos del perro: "))
                perro_nuevo = Perro(nombre, raza, edad, puntos)
                exposicion.agregar_perro(perro_nuevo)
                print("Perro registrado exitosamente.")
            elif opcion == "4":
                nombre = input("Ingrese el nombre del perro: ")
                exposicion.buscar_perro_por_nombre(nombre)
            elif opcion == "5":
                exposicion.perro_ganador()
            elif opcion == "6":
                exposicion.perro_menor_puntuacion()
            elif opcion == "7":
                exposicion.perro_mas_viejo()
            elif opcion == "8":
                print("¡Hasta luego!")
                break
            else:
                print("Opción no válida. Intente de nuevo.")
        except ValueError as e:
            print("Error:", e)
