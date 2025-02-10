DOUBLY CIRCULAR 

#include<stdio.h>
#include<stdlib.h>
#include<malloc.h>
struct node
{
int info;
struct node *next;
struct node *prev;
};

struct node *insert_before(struct node *head)
{
    int info;
    printf("Enter the value before which to insert: ");
    scanf("%d", &info);

    struct node *newNode = (struct node *)malloc(sizeof(struct node));
    if (newNode == NULL) {
        printf("Memory issue\n");
        return head;
    }
    
    printf("Enter value for the new node: ");
    scanf("%d", &newNode->info);

    if (head == NULL) {
        printf("List is empty\n");
        free(newNode);
        return head;
    }

    struct node *temp = head;
    do {
        if (temp->info == info) {
            // Insert newNode before temp
            newNode->next = temp;
            newNode->prev = temp->prev;
            temp->prev->next = newNode;
            temp->prev = newNode;

            if (temp == head) {
                head = newNode;  // Update head if we inserted before the head
            }
            return head;
        }
        temp = temp->next;
    } while (temp != head);

    printf("Node with value %d not found\n", info);
    free(newNode);
    return head;
}
struct node *delete_before(struct node *head)
{
    int info;
    printf("Enter the value of the node to delete before: ");
    scanf("%d", &info);

    if (head == NULL) {
        printf("List is empty\n");
        return head;
    }

    struct node *temp = head;
    struct node *nodeToDelete = NULL;

    // Search for the node with the given info
    do {
        if (temp->info == info) {
            // If the node to delete is before head
            if (temp->prev == head) {
                printf("There is no node before the head\n");
                return head;
            } else {
                nodeToDelete = temp->prev;
                // Update links to delete nodeToDelete
                nodeToDelete->prev->next = temp;
                temp->prev = nodeToDelete->prev;

                if (nodeToDelete == head) {
                    head = temp;  // Update head if we delete the head node
                }
                free(nodeToDelete);
                return head;
            }
        }
        temp = temp->next;
    } while (temp != head);

    printf("Node with value %d not found\n", info);
    return head;
}

struct node *insert_k(struct node *head)
{
    int k, value;
    printf("Enter the position to insert: ");
    scanf("%d", &k);
    printf("Enter the value to insert: ");
    scanf("%d", &value);

    struct node *temp = (struct node *)malloc(sizeof(struct node));
    if (temp == NULL) {
        printf("Memory allocation issue\n");
        return head;
    }
    temp->info = value;

    // Special case: insert at the head (1st position)
    if (k == 1) {
        if (head == NULL) {
            temp->next = temp;
            temp->prev = temp;
            head = temp;
        } else {
            struct node *last = head->prev;
            temp->next = head;
            temp->prev = last;
            last->next = temp;
            head->prev = temp;
            head = temp;
        }
        return head;
    }

    // Traverse to the (k-1)-th node
    struct node *current = head;
    int count = 1;
    while (count < k - 1 && current->next != head) {
        current = current->next;
        count++;
    }

    // If k is out of bounds
    if (count != k - 1) {
        printf("Position out of bounds\n");
        free(temp);
        return head;
    }

    // Insert the new node at the k-th position
    temp->next = current->next;
    temp->prev = current;
    current->next->prev = temp;
    current->next = temp;

    return head;
}
struct node *delete_k(struct node *head)
{
    int k;
    printf("Enter the position to delete: ");
    scanf("%d", &k);

    if (head == NULL) {
        printf("List is empty\n");
        return head;
    }

    struct node *temp = head;
    int count = 1;

    // Special case: deleting the head (1st node)
    if (k == 1) {
        if (head->next == head) {
            free(head);
