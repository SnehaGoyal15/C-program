Queue using linked list 
#include <stdio.h>
#include <stdlib.h>

struct Node {
    int data;
    struct Node* next;
};

struct Node* display(struct Node* f) {
    struct Node* r = f;
    if (r == NULL) {
        printf("The list is empty.\n");
        return f;
    }

    while (r != NULL) {
        printf("%d \t", r->data);
        r = r->next;
    }
    printf("\n");
    return f;
}

struct Node* delstart(struct Node* f) {
    if (f == NULL) {
        printf("The list is empty, nothing to delete.\n");
        return f; // Return unchanged list
    } 
    else if (f->next == NULL) { // Only one node
        printf("Data deleted is: %d\n", f->data);
        free(f);
        return NULL; // The list is now empty
    } 
    else {
        struct Node* r = f;
        f = f->next; // Move the head to the next node
        printf("Data deleted is: %d\n", r->data);
        free(r);
        return f; 
    }
}

struct Node* insertend(struct Node* f) {
    struct Node* t = (struct Node*)malloc(sizeof(struct Node)); 
    
    if (t == NULL) {
        printf("Memory allocation failed.\n");
        return f; // Return unchanged list
    }

    printf("Enter the data to be inserted in the new node: ");
    scanf("%d", &(t->data));
    t->next = NULL;

    if (f == NULL) { // If the list is empty
        return t; // New node is now the head
    } else {
        struct Node* r = f;
        while (r->next != NULL) {
            r = r->next;
        }
        r->next = t; // Link the new node
    }
    return f; 
}

int main() {
    int c;
    struct Node* f = NULL;

    do {
        printf("\nEnter 1 to insert, 2 to display, 3 to delete from start, 4 to exit: ");
        scanf("%d", &c);
        switch(c) {
            case 1:
                f = insertend(f);
                break;
            case 2:
                display(f);
                break;
            case 3:
                f = delstart(f);
                break;
            case 4:
                printf("Exiting...\n");
                break;
            default:
                printf("Invalid option. Try again.\n");
        }
    } while (c != 4);

    // Free the remaining nodes before exit
    while (f != NULL) {
        f = delstart(f);
    }

    return 0;
}
