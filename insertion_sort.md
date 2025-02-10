#include <stdio.h>
#include <string.h>

void insertionSortInt(int arr[], int n) {
    for (int i = 1; i < n; i++) {
        int key = arr[i];
        int j = i - 1;
        while (j >= 0 && arr[j] > key) {
            arr[j + 1] = arr[j];
            j--;
        }
        arr[j + 1] = key;
    }
}

void insertionSortString(char arr[][100], int n) {
    for (int i = 1; i < n; i++) {
        char key[100];
        strcpy(key, arr[i]);
        int j = i - 1;
        while (j >= 0 && strcmp(arr[j], key) > 0) {
            strcpy(arr[j + 1], arr[j]);
            j--;
        }
        strcpy(arr[j + 1], key);
    }
}

int main() {
    int n;
    printf("Enter the number of integers: ");
    scanf("%d", &n);
    int intArray[n];
    printf("Enter %d integers:\n", n);
    for (int i = 0; i < n; i++) {
        scanf("%d", &intArray[i]);
    }

    printf("Enter the number of strings: ");
    scanf("%d", &n);
    char strArray[n][100];
    printf("Enter %d strings:\n", n);
    for (int i = 0; i < n; i++) {
        scanf("%s", strArray[i]);
    }

    insertionSortInt(intArray, n);
    printf("Sorted integers:\n");
    for (int i = 0; i < n; i++) {
        printf("%d ", intArray[i]);
    }
    printf("\n");

    insertionSortString(strArray, n);
    printf("Sorted strings:\n");
    for (int i = 0; i < n; i++) {
        printf("%s\n", strArray[i]);
    }

    return 0;
}
