jump                                                                                                                                                                                                           #include <stdio.h>

void jumpSearch() {
    int n, key, comparisons = 0, step = 2, prev = 0;
    scanf("%d", &n);
    int arr[n];
    for (int i = 0; i < n; i++) scanf("%d", &arr[i]);
    scanf("%d", &key);
    while (prev < n && arr[prev] < key) {
        comparisons++;
        if (prev + step >= n || arr[prev + step] >= key) break;
        prev += step;
        step *= 2;
    }
    for (int i = prev; i < n && i <= prev + step; i++) {
        comparisons++;
        if (arr[i] == key) {
            printf("Present %d\n", comparisons);
            return;
        }
    }
    printf("Not Present %d\n", comparisons);
}

int main() {
    int T;
    scanf("%d", &T);
    while (T--) jumpSearch();
    return 0;
}
