# AgendaTelefonica
Trabajo final 1 para PYT- 01/Programación Python - PYT-01 VIERNES 5-7 PM MARZO - ABRIL 2022 - Prof. Francis Fulgencio

# Code
class Contacto:
    def __init__(self, id, nombre, telefono):
        self.id = id
        self.nombre = nombre
        self.telefono = telefono
    
    def __str__(self):
        return f"ID: {self.id}, Nombre: {self.nombre}, Teléfono: {self.telefono}"

class AgendaTelefonica:
    def __init__(self):
        self.contactos = [
            Contacto(i, f"Contacto{i}", f"123-456-78{i}") for i in range(1, 11)
        ]
    
    def agregar_contacto(self):
        while True:
            id = input("Ingrese ID del contacto: ")
            nombre = input("Ingrese Nombre: ")
            telefono = input("Ingrese Teléfono: ")
            self.contactos.append(Contacto(id, nombre, telefono))
            
            otro = input("¿Desea agregar otro contacto? (s/n): ").lower()
            if otro != 's':
                break
    
    def buscar_contacto(self):
        criterio = input("Buscar por (1) ID o (2) Nombre: ")
        if criterio == "1":
            id_buscar = input("Ingrese ID: ")
            resultados = [c for c in self.contactos if c.id == id_buscar]
        elif criterio == "2":
            nombre_buscar = input("Ingrese Nombre: ")
            resultados = [c for c in self.contactos if nombre_buscar.lower() in c.nombre.lower()]
        else:
            print("Opción inválida.")
            return
        
        if resultados:
            for c in resultados:
                print(c)
        else:
            print("Contacto no encontrado.")
    
    def actualizar_contacto(self):
        id_buscar = input("Ingrese ID del contacto a actualizar: ")
        for c in self.contactos:
            if c.id == id_buscar:
                c.nombre = input("Ingrese nuevo Nombre: ")
                c.telefono = input("Ingrese nuevo Teléfono: ")
                print("Contacto actualizado correctamente.")
                return
        print("Contacto no encontrado.")
    
    def borrar_contacto(self):
        id_buscar = input("Ingrese ID del contacto a borrar: ")
        for c in self.contactos:
            if c.id == id_buscar:
                self.contactos.remove(c)
                print("Contacto eliminado correctamente.")
                return
        print("Contacto no encontrado.")
    
    def listar_contactos(self):
        if self.contactos:
            for c in self.contactos:
                print(c)
        else:
            print("No hay contactos guardados.")
    
    def menu(self):
        while True:
            print("\n--- Agenda Telefónica ---")
            print("1. Agregar Contacto")
            print("2. Buscar Contacto")
            print("3. Actualizar Contacto")
            print("4. Borrar Contacto")
            print("5. Listar Contactos")
            print("6. Salir")
            
            opcion = input("Seleccione una opción: ")
            
            if opcion == "1":
                self.agregar_contacto()
            elif opcion == "2":
                self.buscar_contacto()
            elif opcion == "3":
                self.actualizar_contacto()
            elif opcion == "4":
                self.borrar_contacto()
            elif opcion == "5":
                self.listar_contactos()
            elif opcion == "6":
                print("Saliendo...")
                break
            else:
                print("Opción inválida. Intente de nuevo.")

if __name__ == "__main__":
    agenda = AgendaTelefonica()
    agenda.menu()
