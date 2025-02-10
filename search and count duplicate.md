#include <stdio.h>

int countOccurrences(int arr[], int n, int key) {
    int low = 0, high = n - 1, mid, first = -1, last = -1;
    
    while (low <= high) {
        mid = (low + high) / 2;
        if (arr[mid] == key) {
            first = mid;
            high = mid - 1; // Search in left half
        } else if (arr[mid] < key)
            low = mid + 1;
        else
            high = mid - 1;
    }
    
    if (first == -1) return 0; // Key not found

    low = 0, high = n - 1;
    while (low <= high) {
        mid = (low + high) / 2;
        if (arr[mid] == key) {
            last = mid;
            low = mid + 1; // Search in right half
        } else if (arr[mid] < key)
            low = mid + 1;
        else
            high = mid - 1;
    }
    
    return last - first + 1;
}

int main() {
    int n, key, i;
    printf("Enter number of elements: ");
    scanf("%d", &n);
    int arr[n];
    printf("Enter %d sorted elements: ", n);
    for (i = 0; i < n; i++)
        scanf("%d", &arr[i]);
    printf("Enter key to search: ");
    scanf("%d", &key);
    
    int count = countOccurrences(arr, n, key);
    if (count)
        printf("Element found %d times\n", count);
    else
        printf("Element not found\n");
    
    return 0;
}
