#include <stdio.h>
#include <stdlib.h>

// Structure to represent a node in the adjacency list
typedef struct Node {
    int vertex;
    int weight;
    struct Node *next;
} Node;

// Structure to represent a graph
typedef struct Graph {
    int vertices;
    Node **adjList; // Array of pointers to adjacency lists
} Graph;

// Function to create a new node
Node *createNode(int vertex, int weight) {
    Node *newNode = (Node *)malloc(sizeof(Node));
    newNode->vertex = vertex;
    newNode->weight = weight;
    newNode->next = NULL;
    return newNode;
}

// Function to create a graph
Graph *createGraph(int vertices) {
    Graph *graph = (Graph *)malloc(sizeof(Graph));
    graph->vertices = vertices;

    // Allocate memory for adjacency list array
    graph->adjList = (Node **)malloc(vertices * sizeof(Node *));
    for (int i = 0; i < vertices; i++) {
        graph->adjList[i] = NULL; // Initialize all lists as empty
    }
    return graph;
}

// Function to add an edge to the graph
void addEdge(Graph *graph, int src, int dest, int weight) {
    // Add edge from src to dest
    Node *newNode = createNode(dest, weight);
    newNode->next = graph->adjList[src];
    graph->adjList[src] = newNode;

   
}

// Function to print the adjacency list of the graph
void printGraph(Graph *graph) {
    for (int i = 0; i < graph->vertices; i++) {
        Node *temp = graph->adjList[i];
        printf("Vertex %d:", i);
        while (temp) {
            printf(" -> (%d, weight=%d)", temp->vertex, temp->weight);
            temp = temp->next;
        }
        printf("\n");
    }
}

// DFS function
void dfs(Graph *graph, int startVertex, int visited[]) {
    printf("%d ", startVertex); // Print the current vertex
    visited[startVertex] = 1;   // Mark as visited

    Node *temp = graph->adjList[startVertex];
    while (temp) {
        if (!visited[temp->vertex]) {
            dfs(graph, temp->vertex, visited);
        }
        temp = temp->next;
    }
}

// BFS function
void bfs(Graph *graph, int startVertex) {
    int *visited = (int *)malloc(graph->vertices * sizeof(int));
    for (int i = 0; i < graph->vertices; i++) {
        visited[i] = 0; // Initialize all vertices as unvisited
    }

    int *queue = (int *)malloc(graph->vertices * sizeof(int));
    int front = 0, rear = 0;

    visited[startVertex] = 1; // Mark start vertex as visited
    queue[rear++] = startVertex;

    printf("BFS Traversal: ");
    while (front < rear) {
        int currentVertex = queue[front++]; // Dequeue
        printf("%d ", currentVertex);

        Node *temp = graph->adjList[currentVertex];
        while (temp) {
            if (!visited[temp->vertex]) {
                visited[temp->vertex] = 1; // Mark as visited
                queue[rear++] = temp->vertex; // Enqueue
            }
            temp = temp->next;
        }
    }
    printf("\n");

  
}

// Main function
int main() {
    int vertices, edges, src, dest, weight, startVertex;

    printf("Enter the number of vertices and edges: ");
    scanf("%d %d", &vertices, &edges);

    // Create the graph
    Graph *graph = createGraph(vertices);

    printf("Enter the edges in the format (source destination weight):\n");
    for (int i = 0; i < edges; i++) {
        scanf("%d %d %d", &src, &dest, &weight);
        addEdge(graph, src, dest, weight);
    }

    // Print the adjacency list representation of the graph
    printf("Adjacency List Representation of the Weighted Graph:\n");
    printGraph(graph);

    printf("Enter the starting vertex for DFS: ");
    scanf("%d", &startVertex);
    int visited = (int *)malloc(vertices( sizeof(int))); // Initialize visited array
    printf("DFS Traversal: ");
    dfs(graph, startVertex, visited);
    printf("\n");

    printf("Enter the starting vertex for BFS: ");
    scanf("%d", &startVertex);
    bfs(graph, startVertex);

    

    return 0;
}
