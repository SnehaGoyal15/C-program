STACK BY LINKED LIST
// SINGLY LINKED LIST :->
#include <stdio.h>
#include <stdlib.h>
#include<malloc.h>
struct Node {
    int data;
    struct Node* next;
};
struct Node* display(struct Node* top) 
{
    struct Node* t = (struct Node*)malloc(sizeof(struct Node)); 
    
    if (t == NULL) { 
        printf("Memory allocation failed.\n");
        
    }
    else
    {
        struct Node* p;
        p=top;
     while(p!=NULL)
     {
        printf("%d \t",p->data);
        p=p->next;
    }}
    return top;
}

struct Node* insertBegin(struct Node* top) 
{
    struct Node* t = (struct Node*)malloc(sizeof(struct Node)); 
    
    if (t == NULL) { 
        printf("Memory allocation failed.\n");
        
    }
    else
    {
     printf("enter the data to be inserted in the new node \n");
     scanf("%d",&(t->data));
        t->next=top;
        top=t;
    }
    return top;
}
struct Node* delend(struct Node* top) 
{
    if (top == NULL) 
    { 
        printf("Memory allocation failed.\n");
        
    }
    else if(!top->next)
    {
        struct Node* p;
        p=top;
        top=NULL;
        free(p);
    }
    else
    {
        struct Node* p1=top;
        top=top->next;
     printf("data deleted is:- %d  \n",(p1->data));
        free(p1);
    }
    return top; 
}

int main()
{
    int c;
    struct Node* top=NULL;
do
    {
        printf(" \n enter 1 for push \n 2.for display \n 3 for pop \n");
        scanf("%d",&c);
        switch(c)
        {
            case 1:
            head=insertBegin(head);
            break;
            case 2:
            display(head);
            break;
            case 3:
            delend(head);
                default:
            printf("invalid \n");
        }
    }while(1);
    return 0;
}
