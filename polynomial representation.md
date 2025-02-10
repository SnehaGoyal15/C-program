POLYNOMIAL REPRESENTATION 
#include <stdio.h>
#include <stdlib.h>

struct polyn {
    int co;         // Coefficient
    int pow;       // Power
    struct polyn* next; // Pointer to the next term
};

typedef struct polyn* pn;

// Function to add two polynomials
void add_polynomials(pn a, pn b, pn* c) {
    *c = NULL; // Start with an empty polynomial
    pn last = NULL; // To keep track of the last node in the result

    while (a != NULL && b != NULL) {
        pn new_node = (pn)malloc(sizeof(struct polyn));
        
        if (a->pow > b->pow) {
            new_node->pow = a->pow;
            new_node->co = a->co;
            a = a->next;
        } else if (a->pow < b->pow) {
            new_node->pow = b->pow;
            new_node->co = b->co;
            b = b->next;
        } else {
            // Equal powers
            new_node->pow = a->pow;
            new_node->co = a->co + b->co;
            a = a->next;
            b = b->next;
        }
        
        new_node->next = NULL;
        
        if (*c == NULL) {
            *c = new_node;
        } else {
            last->next = new_node;
        }
        last = new_node;
    }

    while (a != NULL) {
        pn new_node = (pn)malloc(sizeof(struct polyn));
        new_node->pow = a->pow;
        new_node->co = a->co;
        new_node->next = NULL;

        if (*c == NULL) {
            *c = new_node;
        } else {
            last->next = new_node;
        }
        last = new_node;
        a = a->next;
    }

    while (b != NULL) {
        pn new_node = (pn)malloc(sizeof(struct polyn));
        new_node->pow = b->pow;
        new_node->co = b->co;
        new_node->next = NULL;

        if (*c == NULL) {
            *c = new_node;
        } else {
            last->next = new_node;
        }
        last = new_node;
        b = b->next;
    }
}

// Function to print the polynomial
void print_polynomial(pn poly) {
    while (poly != NULL) {
        printf("%dx^%d ", poly->co, poly->pow);
        if (poly->next != NULL) {
            printf("+ ");
        }
        poly = poly->next;
    }
    printf("\n");
}

// Function to create a polynomial from user input
pn create_polynomial() {
    pn head = NULL;
    pn last = NULL;
    int num_terms, co, pow;

    printf("Enter the number of terms in the polynomial: ");
    scanf("%d", &num_terms);

    for (int i = 0; i < num_terms; i++) {
        printf("Enter coefficient and power (co pow): ");
        scanf("%d %d", &co, &pow);
        
        pn new_node = (pn)malloc(sizeof(struct polyn));
        new_node->co = co;
        new_node->pow = pow;
        new_node->next = NULL;

        if (head == NULL) {
            head = new_node;
        } else {
            last->next = new_node;
        }
        last = new_node;
    }
    return head;
}

// Example usage
int main() {
    // Create first polynomial from user input
    printf("Polynomial 1:\n");
    pn poly1 = create_polynomial();

    // Create second polynomial from user input
    printf("Polynomial 2:\n");
    pn poly2 = create_polynomial();

    // Result polynomial
    pn result = NULL;

    // Add polynomials
    add_polynomials(poly1, poly2, &result);

    // Print result
    printf("Result: ");
    print_polynomial(result);

    // Free memory (not shown)

    return 0;
}
