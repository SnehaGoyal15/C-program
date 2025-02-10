#include <stdio.h>
#include <stdlib.h>

struct Edge {
    int src, dest, weight;
};

struct Graph {
    int V, E;
    struct Edge* edges;
};

struct Graph* createGraph(int V, int E) {
    struct Graph* graph = (struct Graph*)malloc(sizeof(struct Graph));
    graph->V = V;
    graph->E = E;
    graph->edges = (struct Edge*)malloc(E * sizeof(struct Edge));
    return graph;
}

int find(int parent[], int i) {
    if (parent[i] != i) {
        parent[i] = find(parent, parent[i]);
    }
    return parent[i];
}

void Union(int parent[], int x, int y) {
    int rootX = find(parent, x);
    int rootY = find(parent, y);

    // Attach one tree under another
    parent[rootX] = rootY;
}

void bubbleSortEdges(struct Edge edges[], int E) {
    for (int i = 0; i < E - 1; i++) {
        for (int j = 0; j < E - i - 1; j++) {
            if (edges[j].weight > edges[j + 1].weight) {
                // Swap edges[j] and edges[j + 1]
                struct Edge temp = edges[j];
                edges[j] = edges[j + 1];
                edges[j + 1] = temp;
            }
        }
    }
}

void KruskalMST(struct Graph* graph) {
    int V = graph->V;
    struct Edge result[V];
    int e = 0;
    int i = 0;

    // Sort edges using bubble sort
    bubbleSortEdges(graph->edges, graph->E);

    int* parent = (int*)malloc(V * sizeof(int));
    for (int v = 0; v < V; v++) {
        parent[v] = v;
    }

    while (e < V - 1 && i < graph->E) {
        struct Edge nextEdge = graph->edges[i++];
        int x = find(parent, nextEdge.src);
        int y = find(parent, nextEdge.dest);

        if (x != y) {
            result[e++] = nextEdge;
            Union(parent, x, y);
        }
    }

    printf("Edges in the Minimum Spanning Tree:\n");
    for (i = 0; i < e; i++) {
        printf("%d -- %d == %d\n", result[i].src, result[i].dest, result[i].weight);
    }

    free(parent);
}

int main() {
    int V, E;
    printf("Enter the number of vertices: ");
    scanf("%d", &V);
    printf("Enter the number of edges: ");
    scanf("%d", &E);

    struct Graph* graph = createGraph(V, E);

    printf("Enter the edges (source, destination, weight):\n");
    for (int i = 0; i < E; i++) {
        scanf("%d %d %d", &graph->edges[i].src, &graph->edges[i].dest, &graph->edges[i].weight);
    }

    KruskalMST(graph);

    free(graph->edges);
    free(graph);

    return 0;
}
