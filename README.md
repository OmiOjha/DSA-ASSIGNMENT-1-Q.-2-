#include <stdio.h>
#include <string.h>

// Define a structure to store book details
struct Book {
    char title[50];
    char author[50];
    float price;
};

// Function to input details of books

void inputBookDetails(struct Book* b, int count) 
{
    
    for (int i = 0; i < count; i++) {
        
        printf("Enter details for Book %d:\n", i + 1);

        printf("Title: ");
        getchar();  // To consume newline character from previous input
        fgets(b[i].title, sizeof(b[i].title), stdin);
        b[i].title[strcspn(b[i].title, "\n")] = 0;  // Remove trailing newline

        printf("Author: ");
        fgets(b[i].author, sizeof(b[i].author), stdin);
        b[i].author[strcspn(b[i].author, "\n")] = 0;  // Remove trailing newline

        printf("Price: ");
        scanf("%f", &b[i].price);
        printf("\n");
    }
}

// Function to find the most expensive and cheapest book
void findMostExpensiveAndCheapest(struct Book* b, int count, struct Book** mostExpensive, struct Book** cheapest) {
    *mostExpensive = &b[0];
    *cheapest = &b[0];

    for (int i = 1; i < count; i++) {
        if (b[i].price > (*mostExpensive)->price) {
            *mostExpensive = &b[i];
        }
        if (b[i].price < (*cheapest)->price) {
            *cheapest = &b[i];
        }
    }
}

// Function to display book details
void displayBookDetails(struct Book* b) {
    printf("Title: %s\n", b->title);
    printf("Author: %s\n", b->author);
    printf("Price: %.2f\n", b->price);
}

int main() {
    int n = 3;
    struct Book books[n];
    struct Book* mostExpensive;
    struct Book* cheapest;

    // Input details for three books
    inputBookDetails(books, n);

    // Find the most expensive and cheapest books
    findMostExpensiveAndCheapest(books, n, &mostExpensive, &cheapest);

    // Display the most expensive book
    printf("Most Expensive Book:\n");
    displayBookDetails(mostExpensive);
    printf("\n");

    // Display the cheapest book
    printf("Cheapest Book:\n");
    displayBookDetails(cheapest);

    return 0;
}
