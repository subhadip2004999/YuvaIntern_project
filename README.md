# YuvaIntern_project

A small Java console application: a Library Books Management System implemented in `src/main/java/mypackage`.

## Project summary

This repository contains a small Java program that provides a command-line library book management system. It currently includes three Java source files under `src/main/java/mypackage`:

- `mainApp.java` — program entry point (class `mypackage.mainApp`). Presents a text UI with options to add, list, update, and delete books.
- `Management.java` — contains book management logic and an in-memory `ArrayList<Book>` used as the library database. Offers methods `addBook()`, `listBook()`, `updateBook()`, `deleteBook()`.
- `Book.java` — simple data class for a book with fields: `title`, `author`, `isbn`, `publicationyear` and corresponding getters.

## Requirements

- Java 11 or newer (JDK)

## Build & run (no build tool)

This project doesn't use Maven/Gradle. Compile and run using `javac`/`java`:

```bash
# from the repository root
find src -name "*.java" > sources.txt
javac -d out @sources.txt

# run the main class
java -cp out mypackage.mainApp
```

Notes:
- The main entry point is `mypackage.mainApp`.
- The program is interactive and reads input from the console.

## Project structure

src/main/java/mypackage/
- `Book.java` — model class representing a book.
- `Management.java` — contains the management operations and in-memory data store.
- `mainApp.java` — console UI and program entry point.

## Example run (sample session)

Below is an example of what a user session looks like after compiling and running `mypackage.mainApp`.

```text
$ java -cp out mypackage.mainApp

||---------------------------------||
|| LIBRARY BOOKS MANAGEMENT SYSTEM ||
||---------------------------------||
1. Add books to library
2. Display all the books
3. Update books of it's ID
4. Delete books from library
5. Exit

Enter your choice: 1
Enter Title of the Book: The Alchemist
Enter Author of the Book: Paulo Coelho
Enter ISBN of the Book: 123456789
Enter Publication Year of the Book: 1988

The book (The Alchemist) is successfully added to the List !!

Enter your choice: 2
The current list of Books: 

1. ID of the Book: 0
   Title: The Alchemist
   Author: Paulo Coelho
   ISBN: 123456789
   Publication Year: 1988

Enter your choice: 3
Enter the ID of the book to be updated: 0

 UPDATE THE BOOK CONTENTS 

Enter New Title of the Book: The Alchemist (Updated)
Enter New Author of the Book: Paulo Coelho
Enter New ISBN of the Book: 123456789
Enter New Publication Year of the Book: 1988

Book is Successfully updated for the ID: 0 !!

Enter your choice: 4
Enter the ID of the book to be deleted: 0

Book is Successfully removed form the list !!

Enter your choice: 5

PROGRAM EXITED SUCCESSFULLY
```

This example demonstrates adding, listing, updating, deleting a book, and exiting the application.

## Quick usage

- Start the program: `java -cp out mypackage.mainApp` after compilation.
- Use menu choices 1–5 to add, list, update, delete books, or exit.

## Known issues & suggestions (observed in source)

- `Management.updateBook()` and `Management.deleteBook()` use a conditional `if (index <0 && booklist.isEmpty())` which will not correctly detect invalid indices; it should likely be `if (booklist.isEmpty() || index < 0 || index >= booklist.size())` to avoid IndexOutOfBoundsException or check for empty list separately.
- Input parsing mixes `nextInt()` and `nextLine()`; current code calls `sc.nextLine()` after `nextInt()` which mitigates the newline issue but be cautious when refactoring.
- `ISBN` is stored in an `int`. Consider using `long` or `String` if you expect larger or non-numeric ISBN formats.
- `Management.booklist` is `public static` — consider making it private and exposing controlled access.
- The `Scanner` instances are not closed. It's OK for short CLI programs, but closing System.in Scanner can have side effects; document or centralize scanner use.

## Contribution

Contributions are welcome. Suggested workflow:
1. Fork the repository
2. Create a branch for your change
3. Open a pull request

## License

No LICENSE file found. If you want this project licensed, add a LICENSE file (e.g., MIT) or tell me which license to add and I can create it.

---

This README was generated/updated automatically by a repository assistant after inspecting `src/main/java/mypackage`. If you want a more detailed README (examples, test instructions, or a branch/PR instead of direct commits), tell me and I will update accordingly.
