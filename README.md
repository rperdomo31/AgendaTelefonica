# AgendaTelefonica
Trabajo final 1 para PYT- 01/Programación Python - PYT-01 VIERNES 5-7 PM MARZO - ABRIL 2022 - Prof. Francis Fulgencio

# Code
class Contact:
    def __init__(self, contact_id, name, phone):
        self.contact_id = contact_id
        self.name = name
        self.phone = phone

    def __str__(self):
        return f"ID: {self.contact_id}, Name: {self.name}, Phone: {self.phone}"

class PhoneBook:
    def __init__(self):
        self.contacts = [
            Contact(i, f"Contact {i}", f"555-00{i}") for i in range(1, 11)
        ]

    def add_contact(self):
        while True:
            contact_id = int(input("Enter ID: "))
            name = input("Enter name: ")
            phone = input("Enter phone: ")
            self.contacts.append(Contact(contact_id, name, phone))
            more = input("Do you want to add another contact? (y/n): ")
            if more.lower() != 'y':
                break

    def search_contact(self):
        search_type = input("Search by (id/name): ")
        if search_type.lower() == "id":
            contact_id = int(input("Enter ID: "))
            results = [c for c in self.contacts if c.contact_id == contact_id]
        else:
            name = input("Enter name: ")
            results = [c for c in self.contacts if name.lower() in c.name.lower()]
        
        for contact in results:
            print(contact)
        if not results:
            print("No contacts found.")

    def update_contact(self):
        contact_id = int(input("Enter ID of contact to update: "))
        for contact in self.contacts:
            if contact.contact_id == contact_id:
                contact.name = input("Enter new name: ") or contact.name
                contact.phone = input("Enter new phone: ") or contact.phone
                print("Contact updated.")
                return
        print("Contact not found.")

    def delete_contact(self):
        contact_id = int(input("Enter ID of contact to delete: "))
        self.contacts = [c for c in self.contacts if c.contact_id != contact_id]
        print("Contact deleted.")

    def list_contacts(self):
        for contact in self.contacts:
            print(contact)

    def menu(self):
        while True:
            print("\nPhone Book Menu")
            print("1. Add Contact")
            print("2. Search Contact")
            print("3. Update Contact")
            print("4. Delete Contact")
            print("5. List Contacts")
            print("6. Exit")
            choice = input("Choose an option: ")
            
            if choice == "1":
                self.add_contact()
            elif choice == "2":
                self.search_contact()
            elif choice == "3":
                self.update_contact()
            elif choice == "4":
                self.delete_contact()
            elif choice == "5":
                self.list_contacts()
            elif choice == "6":
                print("Exiting phone book.")
                break
            else:
                print("Invalid choice, try again.")

if __name__ == "__main__":
    phone_book = PhoneBook()
    phone_book.menu()
