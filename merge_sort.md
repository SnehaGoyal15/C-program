#include <stdio.h>
#include <string.h>

void mergeInt(int arr[], int left, int mid, int right) {
    int n1 = mid - left + 1;
    int n2 = right - mid;
    int L[n1], R[n2];

    for (int i = 0; i < n1; i++) {
        L[i] = arr[left + i];
    }
    for (int i = 0; i < n2; i++) {
        R[i] = arr[mid + 1 + i];
    }

    int i = 0, j = 0, k = left;
    while (i < n1 && j < n2) {
        if (L[i] <= R[j]) {
            arr[k++] = L[i++];
        } else {
            arr[k++] = R[j++];
        }
    }

    while (i < n1) {
        arr[k++] = L[i++];
    }
    while (j < n2) {
        arr[k++] = R[j++];
    }
}

void mergeSortInt(int arr[], int left, int right) {
    if (left < right) {
        int mid = left + (right - left) / 2;
        mergeSortInt(arr, left, mid);
        mergeSortInt(arr, mid + 1, right);
        mergeInt(arr, left, mid, right);
    }
}

void mergeString(char arr[][100], int left, int mid, int right) {
    int n1 = mid - left + 1;
    int n2 = right - mid;
    char L[n1][100], R[n2][100];

    for (int i = 0; i < n1; i++) {
        strcpy(L[i], arr[left + i]);
    }
    for (int i = 0; i < n2; i++) {
        strcpy(R[i], arr[mid + 1 + i]);
    }

    int i = 0, j = 0, k = left;
    while (i < n1 && j < n2) {
        if (strcmp(L[i], R[j]) <= 0) {
            strcpy(arr[k++], L[i++]);
        } else {
            strcpy(arr[k++], R[j++]);
        }
    }

    while (i < n1) {
        strcpy(arr[k++], L[i++]);
    }
    while (j < n2) {
        strcpy(arr[k++], R[j++]);
    }
}

void mergeSortString(char arr[][100], int left, int right) {
    if (left < right) {
        int mid = left + (right - left) / 2;
        mergeSortString(arr, left, mid);
        mergeSortString(arr, mid + 1, right);
        mergeString(arr, left, mid, right);
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

    mergeSortInt(intArray, 0, n - 1);
    printf("Sorted integers:\n");
    for (int i = 0; i < n; i++) {
        printf("%d ", intArray[i]);
    }
    printf("\n");

    mergeSortString(strArray, 0, n - 1);
    printf("Sorted strings:\n");
    for (int i = 0; i < n; i++) {
        printf("%s\n", strArray[i]);
    }

    return 0;
}
