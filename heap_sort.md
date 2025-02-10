#include <stdio.h>

// MaxHeapify function to maintain the heap property
void maxHeapify(int arr[], int n, int i) {
    int largest = i;
    int left = 2 * i + 1;
    int right = 2 * i + 2;

    // If left child is larger than root
    if (left < n && arr[left] > arr[largest]) {
        largest = left;
    }

    // If right child is larger than largest so far
    if (right < n && arr[right] > arr[largest]) {
        largest = right;
    }

    // If largest is not root, swap and continue heapifying
    if (largest != i) {
        // Swap arr[i] and arr[largest]
        int temp = arr[i];
        arr[i] = arr[largest];
        arr[largest] = temp;

        // Recursively heapify the affected subtree
        maxHeapify(arr, n, largest);
    }
}

// BuildMaxHeap function to convert the array into a max-heap
void buildMaxHeap(int arr[], int n) {
    // Start from the last non-leaf node and call maxHeapify
    for (int i = n / 2 - 1; i >= 0; i--) {
        maxHeapify(arr, n, i);
    }
}

// HeapSort function to sort the array using heap sort algorithm
void heapSort(int arr[], int n) {
    // Build a max heap
    buildMaxHeap(arr, n);

    // One by one extract elements from the heap
    for (int i = n - 1; i > 0; i--) {
        // Swap root (maximum element) with the last element
        int temp = arr[0];
        arr[0] = arr[i];
        arr[i] = temp;

        // Call maxHeapify on the reduced heap
        maxHeapify(arr, i, 0);
    }
}

int main() {
    int n;

    // Input the number of integers
    printf("Enter the number of integers: ");
    scanf("%d", &n);

    // Input the integer array
    int arr[n];
    printf("Enter %d integers:\n", n);
    for (int i = 0; i < n; i++) {
        scanf("%d", &arr[i]);
    }

    // Perform heap sort
    heapSort(arr, n);

    // Print the sorted array
    printf("Sorted integers:\n");
    for (int i = 0; i < n; i++) {
        printf("%d ", arr[i]);
    }
    printf("\n");

    return 0;
}
