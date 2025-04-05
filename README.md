# COURSE-PROJECT-OOPS
#include <stdio.h>
#include <string.h>
#define MAX_BOOKS 100
#define MAX_MEMBERS 50

struct Book {
    int id;
    char title[50];
    char author[50];
    int isBorrowed;  
};

struct Member {
    int id;
    char name[50];
};

struct Book library[MAX_BOOKS];
int bookCount = 0;

void addBook() {
    printf("Enter Book ID: ");
    scanf("%d", &library[bookCount].id);
    getchar(); 
    printf("Enter Book Title: ");
    fgets(library[bookCount].title, 50, stdin);
    printf("Enter Author: ");
    fgets(library[bookCount].author, 50, stdin);
    library[bookCount].isBorrowed = 0;
    bookCount++;
    printf("Book added successfully!\n");
}

void displayBooks() {
    printf("\nList of Books:\n");
    for (int i = 0; i < bookCount; i++) {
        printf("ID: %d, Title: %s, Author: %s, Status: %s\n",
               library[i].id,
               library[i].title,
               library[i].author,
               library[i].isBorrowed ? "Borrowed" : "Available");
    }
}

void borrowBook() {
    int id;
    printf("Enter Book ID to Borrow: ");
    scanf("%d", &id);
    for (int i = 0; i < bookCount; i++) {
        if (library[i].id == id) {
            if (!library[i].isBorrowed) {
                library[i].isBorrowed = 1;
                printf("Book '%s' borrowed successfully!\n", library[i].title);
            } else {
                printf("Sorry, this book is already borrowed.\n");
            }
            return;
        }
    }
    printf("Book not found.\n");
}

void returnBook() {
    int id;
    printf("Enter Book ID to Return: ");
    scanf("%d", &id);
    for (int i = 0; i < bookCount; i++) {
        if (library[i].id == id) {
            if (library[i].isBorrowed) {
                library[i].isBorrowed = 0;
                printf("Book '%s' returned successfully!\n", library[i].title);
            } else {
                printf("This book was not borrowed.\n");
            }
            return;
        }
    }
    printf("Book not found.\n");
}

int main() {
    int choice;
    while (1) {
        printf("\n--- Library Management System ---\n");
        printf("1. Add Book\n");
        printf("2. Display Books\n");
        printf("3. Borrow Book\n");
        printf("4. Return Book\n");
        printf("5. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1:
                addBook();
                break;
            case 2:
                displayBooks();
                break;
            case 3:
                borrowBook();
                break;
            case 4:
                returnBook();
                break;
            case 5:
                printf("Exiting the system. Goodbye!\n");
                return 0;
            default:
                printf("Invalid choice. Please try again.\n");
        }
    }
    return 0;
}
