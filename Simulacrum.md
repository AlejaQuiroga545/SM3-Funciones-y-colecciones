```python
# Comunnity library

# Create our library
class Book:
    def __init__(self, tittle, author, copies, genre):
        if not isinstance(tittle, str) or not tittle:
            raise ValueError("You must join a valid text")
        if not isinstance(author, str) or not author:
            raise ValueError("You must join a valid name")
        if not isinstance(copies, int) or copies < 0:
            raise ValueError("You must join a valid number")
        if genre not in ["Fiction", "Non-Fiction", "Science", "Biography", "Children"]:
            raise ValueError(
                f"The genre {genre} is not valid.\nThe genres allowed are: Fiction, Non-Fiction, Science, Biography and Children."
            )

        self.tittle = tittle
        self.author = author
        self.copies = copies
        self.initial_copies = copies  # Store initial copies
        self.genre = genre

    def __str__(self):
        return (
            f"Tittle: {self.tittle} \nAuthor: {self.author} \nCopies: {self.copies} \nGenre: {self.genre}"
        )


class Library:
    def __init__(self):
        self.books = {}
        self.genre_allowed = ["Fiction", "NonFiction", "Science", "Biography", "Children"]

    def add_book(self, tittle, author, copies, genre):
        try:
            new_book = Book(tittle, author, copies, genre)
            if tittle in self.books:
                print(
                    f"This book already exist with the tittle {tittle}. The number of copies will be updated"
                )
                self.books[tittle].copies += copies
            else:
                self.books[tittle] = new_book
            print(f"The book '{tittle}, has been added succesfully")
        except ValueError as e:
            print(f"Error adding the book: {e}")

    def search_book(self, tittle):
        if tittle in self.books:
            print(self.books[tittle])
        else:
            print("Book not found")

    def loan_book(self, tittle):
        if tittle in self.books:
            if self.books[tittle].copies > 0:
                self.books[tittle].copies -= 1  # Corrected: Decrement copies
                print(
                    f"Loan of {tittle} has been successfully. Available copies {self.books[tittle].copies}"
                )
            else:
                print(f"There are not available copies of {tittle}")
        else:
            print("Book not found")

    def return_book(self, tittle):
        if tittle in self.books:
            self.books[tittle].copies += 1
            print(
                f"The return was succesfully. Available copies: {self.books[tittle].copies}"
            )
        else:
            print("Book not found")

    def delete_book(self, tittle):
        if tittle in self.books:
            if self.books[tittle].copies == self.books[tittle].initial_copies:  # Use initial_copies
                del self.books[tittle]
                print(f"Book {tittle} has been deleted successfully.")
            else:
                print(
                    f"We couldn't delete the book because it has loan copies"
                )  # Corrected the message
        else:
            print("Book not found")

    def list_by_genre(self, genre):
        if genre not in self.genre_allowed:
            print(
                f"Genre {genre} isn't valid. The allowed genres are: {', '.join(self.genre_allowed)}."
            )  # Corrected f-string
            return

        found_book = [book for book in self.books.values() if book.genre == genre]
        if found_book:
            print(f"Book of genre {genre}: ")
            for book in found_book:
                print(
                    f"- {book.tittle} | Author {book.author}. Copies {book.copies}"
                )  # Corrected f-string
        else:
            print(f"We couldn't find books of the genre {genre}.")

    def inventary(self):
        total_books = len(self.books)
        total_available_copies = sum(
            book.copies for book in self.books.values()
        )  # Changed to .copies
        print("\n--- Resumen del Inventario ---")
        print(f"Total de libros en la biblioteca: {total_books}")
        print(f"Total de copias disponibles: {total_available_copies}")
        print("-----------------------------\n")


def menu():
    print("Hi coder, welcome to our community library.")
    print("-" * 20)
    print("1. Add a book")
    print("2. Search a book")
    print("3. Loan a book")
    print("4. Return a book")
    print("5. Delete a book")
    print("6. List of books by genre")
    print("7. Inventory")
    print("8. Exit")
    print("-" * 20) #added separator


def get_book_info(lib): # Added lib as parameter
    tittle = input("Tittle: ")
    author = input("Author: ")
    while True:
        try:
            copies = int(input("Available copies: "))
            if copies >= 0:
                break
            else:
                print("It must be a positive number.")
        except ValueError:
            print("Please, join a valid number.")
    while True:
        genre = input(
            f"Genre ({', '.join(lib.genre_allowed)}): " #added parenthesis
        ).capitalize()
        if genre in lib.genre_allowed:
            break
        else:
            print("Género no válido. Por favor, elija de la lista.")
    return tittle, author, copies, genre



if __name__ == "__main__":
    lib = Library() #changed variable name

    while True:
        menu()
        opc_str = input("Choose an option (1-8): ")

        if not opc_str.isdigit():  # Verificamos si la entrada es un número
            print("\n Oops 🫢 ...Please, choose a valid option.")
            continue

        opc = int(opc_str)

        if opc == 1:
            tittle, author, copies, genre = get_book_info(lib) # Passed lib instance
            lib.add_book(tittle, author, copies, genre)

        elif opc == 2:
            tittle_search = input("Join the tittle of the book that you want to search: ")
            lib.search_book(tittle_search)

        elif opc == 3:
            tittle_loan = input("Join the tittle of the book that you want to loan: ")
            lib.loan_book(tittle_loan)

        elif opc == 4:
            tittle_return = input("Join the tittle of the book that you want to return: ")
            lib.return_book(tittle_return) # Corrected method call

        elif opc == 5:
            tittle_delete = input("Join the tittle of the book that you want to delete: ")
            lib.delete_book(tittle_delete) # Corrected method call

        elif opc == 6:
            list_genre = input(
                f"Write the genre you want to choose. \nOptions: {', '.join(lib.genre_allowed)}): "
            ).capitalize()
            lib.list_by_genre(list_genre)

        elif opc == 7:
            lib.inventary()

        elif opc == 8:
            print("Thanks for use our system of Community library, see you soon!")
            break

        else:
            print("Unvalid option, please try again.")

```
