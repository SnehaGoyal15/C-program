#include <stdio.h>
#include <stdlib.h>

struct Node {
    int data;
    struct Node *left, *right;
};

void insert(struct Node **root, int value) {
    if (*root == NULL) {
        *root = (struct Node *)malloc(sizeof(struct Node));
        (*root)->data = value;
        (*root)->left = NULL;
        (*root)->right = NULL;
    } else if (value < (*root)->data) {
        insert(&(*root)->left, value);
    } else {
        insert(&(*root)->right, value);
    }
}

int countLeafNodes(struct Node *root) {
    if (root == NULL) return 0;
    if (root->left == NULL && root->right == NULL) return 1;
    return countLeafNodes(root->left) + countLeafNodes(root->right);
}

int countSingleChildNodes(struct Node *root) {
    if (root == NULL) return 0;
    int count = 0;
    if ((root->left == NULL && root->right != NULL) || (root->left != NULL && root->right == NULL)) {
        count = 1;
    }
    return count + countSingleChildNodes(root->left) + countSingleChildNodes(root->right);
}

int countTwoChildNodes(struct Node *root) {
    if (root == NULL) return 0;
    int count = (root->left != NULL && root->right != NULL) ? 1 : 0;
    return count + countTwoChildNodes(root->left) + countTwoChildNodes(root->right);
}

struct Node *findSecondLargest(struct Node *root) {
    struct Node *parent = NULL;
    struct Node *current = root;
    while (current && current->right) {
        parent = current;
        current = current->right;
    }
    if (current && current->left) return findMin(current->left);
    return parent;
}

struct Node *findSecondSmallest(struct Node *root) {
    struct Node *parent = NULL;
    struct Node *current = root;
    while (current && current->left) {
        parent = current;
        current = current->left;
    }
    if (current && current->right) return findMin(current->right);
    return parent;
}

void printNodesWithCommonParent(struct Node *root) {
    if (root == NULL) return;
    if (root->left && root->right) {
        printf("Parent: %d, Children: %d and %d\n", root->data, root->left->data, root->right->data);
    }
    printNodesWithCommonParent(root->left);
    printNodesWithCommonParent(root->right);
}

struct Node *findMin(struct Node *root) {
    while (root && root->left) root = root->left;
    return root;
}

void inorder(struct Node *root) {
    if (root != NULL) {
        inorder(root->left);
        printf("%d ", root->data);
        inorder(root->right);
    }
}

int main() {
    struct Node *root = NULL;
    int choice, value;

    while (1) {
        printf("\n1. Insert\n2. In-order Traversal\n3. Count Leaf Nodes\n4. Count Nodes with One Child\n5. Count Nodes with Two Children\n6. Find Second Largest Node\n7. Find Second Smallest Node\n8. Print Nodes with Common Parent\n9. Exit\nEnter choice: ");
        scanf("%d", &choice);
        if (choice == 9) break;
        switch (choice) {
            case 1:
                printf("Enter value to insert: ");
                scanf("%d", &value);
                insert(&root, value);
                break;
            case 2:
                printf("In-order Traversal: ");
                inorder(root);
                printf("\n");
                break;
            case 3:
                printf("Number of Leaf Nodes: %d\n", countLeafNodes(root));
                break;
            case 4:
                printf("Number of Nodes with One Child: %d\n", countSingleChildNodes(root));
                break;
            case 5:
                printf("Number of Nodes with Two Children: %d\n", countTwoChildNodes(root));
                break;
            case 6:
                {
                    struct Node *secondLargest = findSecondLargest(root);
                    if (secondLargest) {
                        printf("Second Largest Node: %d\n", secondLargest->data);
                    } else {
                        printf("Tree does not have enough elements.\n");
                    }
                }
                break;
            case 7:
                {
                    struct Node *secondSmallest = findSecondSmallest(root);
                    if (secondSmallest) {
                        printf("Second Smallest Node: %d\n", secondSmallest->data);
                    } else {
                        printf("Tree does not have enough elements.\n");
                    }
                }
                break;
            case 8:
                printf("Nodes with Common Parent:\n");
                printNodesWithCommonParent(root);
                break;
            default:
                printf("Invalid choice.\n");
        }
    }

    return 0;
}
