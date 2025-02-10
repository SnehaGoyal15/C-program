#include <stdio.h>

void binarySearch() {
    int n, key, comparisons = 0;
    printf("Enter size of array: ");
    scanf("%d", &n);
    int arr[n];
    printf("Enter sorted elements: ");
    for (int i = 0; i < n; i++) scanf("%d", &arr[i]);
    printf("Enter key to search: ");
    scanf("%d", &key);

    int low = 0, high = n - 1, mid;
    while (low <= high) {
        mid = (low + high) / 2;
        comparisons++;
        if (arr[mid] == key) {
            printf("Present (comparisons: %d)\n", comparisons);
            return;
        } else if (arr[mid] < key)
            low = mid + 1;
        else
            high = mid - 1;
    }
    printf("Not Present (comparisons: %d)\n", comparisons);
}

int main() {
    int T;
    printf("Enter number of test cases: ");
    scanf("%d", &T);
    while (T--) binarySearch();
    return 0;
}
