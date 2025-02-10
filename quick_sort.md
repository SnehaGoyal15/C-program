#include <stdio.h>
#include <string.h>

// Partition function for integer array
int partitionInt(int arr[], int low, int high) {
    int pivot = arr[high];
    int i = low - 1;

    for (int j = low; j < high; j++) {
        if (arr[j] <= pivot) {
            i++;
            // Swap arr[i] and arr[j] directly
            int temp = arr[i];
            arr[i] = arr[j];
            arr[j] = temp;
        }
    }
    // Swap arr[i + 1] and arr[high] directly
    int temp = arr[i + 1];
    arr[i + 1] = arr[high];
    arr[high] = temp;

    return i + 1;
}

// Quick Sort for integer array
void quickSortInt(int arr[], int low, int high) {
    if (low < high) {
        int pi = partitionInt(arr, low, high);

        quickSortInt(arr, low, pi - 1);
        quickSortInt(arr, pi + 1, high);
    }
}

// Partition function for string array
int partitionString(char arr[][100], int low, int high) {
    char pivot[100];
    strcpy(pivot, arr[high]);
    int i = low - 1;

    for (int j = low; j < high; j++) {
        if (strcmp(arr[j], pivot) <= 0) {
            i++;
            // Swap arr[i] and arr[j] directly
            char temp[100];
            strcpy(temp, arr[i]);
            strcpy(arr[i], arr[j]);
            strcpy(arr[j], temp);
        }
    }
    // Swap arr[i + 1] and arr[high] directly
    char temp[100];
    strcpy(temp, arr[i + 1]);
    strcpy(arr[i + 1], arr[high]);
    strcpy(arr[high], temp);

    return i + 1;
}

// Quick Sort for string array
void quickSortString(char arr[][100], int low, int high) {
    if (low < high) {
        int pi = partitionString(arr, low, high);

        quickSortString(arr, low, pi - 1);
        quickSortString(arr, pi + 1, high);
    }
}

int main() {
    int n;

    // Input the number of integers
    printf("Enter the number of integers: ");
    scanf("%d", &n);
    int intArray[n];
    printf("Enter %d integers:\n", n);
    for (int i = 0; i < n; i++) {
        scanf("%d", &intArray[i]);
    }

    // Input the number of strings
    printf("Enter the number of strings: ");
    scanf("%d", &n);
    char strArray[n][100];
    printf("Enter %d strings:\n", n);
    for (int i = 0; i < n; i++) {
        scanf("%s", strArray[i]);
    }

    // Perform quick sort on the integer array
    quickSortInt(intArray, 0, n - 1);
    printf("Sorted integers:\n");
    for (int i = 0; i < n; i++) {
        printf("%d ", intArray[i]);
    }
    printf("\n");

    // Perform quick sort on the string array
    quickSortString(strArray, 0, n - 1);
    printf("Sorted strings:\n");
    for (int i = 0; i < n; i++) {
        printf("%s\n", strArray[i]);
    }

    return 0;
}
