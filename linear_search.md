#include <stdio.h>

void searchElement() {
    int n, key, comparisons = 0, found = 0;
    scanf("%d", &n);
    int arr[n];
    for (int i = 0; i < n; i++) scanf("%d", &arr[i]);
    scanf("%d", &key);
    for (int i = 0; i < n; i++) {
        comparisons++;
        if (arr[i] == key) {
            found = 1;
            break;
        }
    }
    if (found) printf("Present %d\n", comparisons);
    else printf("Not Present %d\n", comparisons);
}

int main() {
    int T;
    scanf("%d", &T);
    while (T--) searchElement();
    return 0;
}
