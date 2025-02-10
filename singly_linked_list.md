// SINGLY LINKED LIST :->
#include <stdio.h>
#include <stdlib.h>
#include<malloc.h>
struct Node {
    int data;
    struct Node* next;
};
struct Node* insalter(struct Node* head)
{
    if (head == NULL) { 
        printf("The list is empty.\n");
        return head;
    }
    
    struct Node* p1 = head;
    struct Node* temp = NULL; 

    while (p1 != NULL) 
    {
        temp = (struct Node*)malloc(sizeof(struct Node));
        if (temp == NULL) {
            printf("Memory allocation failed.\n");
        }
        else
        {
        printf("Enter the data to insert at alternate position: ");
        scanf("%d", &(temp->data));
        temp->next = p1->next;
        p1->next = temp;
        p1 = temp->next;
        }
    }
    return head;
}


struct Node* delalter(struct Node* head)
{	
    if (head == NULL) { 
        printf("Memory allocation failed.\n");
        
    }
    else
    {
        struct Node* p1 = head;
        struct Node* p2 = NULL;
        while(p1!=NULL && p1->next!=NULL)
        {
            p2=p1->next;
            p1->next=p2->next;
            free(p2);
            p1=p1->next;
        }
    }
    return head;
}
struct Node* duplicate(struct Node* head)
{
    if (head == NULL) { 
        printf("Memory allocation failed.\n");}
    else
    {
        struct Node* p1 = head;
        struct Node* p2 = NULL;
        struct Node* p3 = NULL;
        while(p1!=NULL && p1->next!=NULL)
        {
            p2=p1;
            while(p2->next!=NULL)
            {
                if(p1->data==p2->next->data)
                {
                    p3=p2->next;
                    p2->next=p2->next->next;
                    free(p3);
                }
                else
                    p2=p2->next;
            }
            p1=p1->next;
        }
    }
    return head;
}
struct Node* rev(struct Node* head)
{
    if (head == NULL) { 
        printf("Memory allocation failed.\n");}
    else
    {
        struct Node* p1 = head;
        struct Node* p2 = NULL;
        struct Node* p3 = NULL;
        while(p1!=NULL)
        {
            p3=p1->next;
            p1->next=p2;
            p2=p1;
            p1=p3;
        }
        head=p2;
        printf("reversed linked list is \n");
        while(head!=NULL)
        {
            printf("%d ",head->data);
            head=head->next;
        }
    }
        return head;
}
struct Node* delpos(struct Node* head)
{	
    int v;
    if (head == NULL) { 
        printf("Memory allocation failed.\n");
        
    }
    else
    {
        struct Node* p1 = head;int c=0;
        while(p1!=NULL)
        {
            c++;
            p1=p1->next;
        }
        printf("enter the position \n");
         scanf("%d",&v);
         if(v>c+1)
         {
             printf("not possible \n");
         }
         else if(v==1)
         {
             p1=head;
             head=head->next;
             free(p1);
         }
         else
         {
             c=1;
             p1=head;
             while(c<v-1)
             {
                 p1=p1->next;
                 c++;
             }
             
             struct Node* p2=p1->next;
             p1->next=p2->next;
             printf("element to be deleted is %d",p2->data);
             free(p2);
         }
    }
    return head;
             
 }
 struct Node* insertpos(struct Node* head)
{	
    struct Node* t = (struct Node*)malloc(sizeof(struct Node)); 
    int v;
    if (t == NULL) { 
        printf("Memory allocation failed.\n");
        
    }
    else
    {
        struct Node* p1 = head;int c;
        while(p1!=NULL)
        {
            c++;
            p1=p1->next;
        }
        printf("enter the position \n");
         scanf("%d",&v);
         printf("enter the data to be inserted in the new node");
         scanf("%d",&(t->data));
         if(v>c+1)
         {
             printf("not possible \n");
         }
         else if(v==1)
         {
             t->next=head;
             head=t;
         }
         else
         {
             c=1;
             p1=head;
             while(c<v-1)
             {
                 p1=p1->next;
                 c++;
             }
             t->next=p1->next;
             p1->next=t;
         }
    }
    return head;
             
 }
struct Node* secolast(struct Node* head) {
    
     if (head == NULL) 
        printf("NO ");
    else
    {
        
    struct Node* p2 = NULL;
    struct Node* p1 = head;
    while(p1->next!=NULL) 
    {	p2=p1;
        p1=p1->next;
    }  
    printf("%d is the deleted element \n",p1->data);
    p2->next=p1->next;
    free(p1);
    }
    
    return head;
}
struct Node* delafter(struct Node* head) {
    
     if (head == NULL || head->next == NULL) 
        printf("NO ");
    else
    {
        int v;
        printf("enter value \n");
        scanf("%d",&v);
    struct Node* p2 = NULL;
    struct Node* p1 = head;
    while(p1!=NULL && p1->data!=v) 
    {	
        p1=p1->next;
    }  
    if(p1!=NULL && p1->next!=NULL)
    {
        p2=p1->next;
    printf("%d is the deleted element \n",p2->data);
    p1->next=p2->next;
    free(p2);
    }
    }
    return head;
}
struct Node* delbefore(struct Node* head) {
     if (head == NULL) 
        printf("NO ");
    else
    {
        int v;
        printf("enter value \n");
        scanf("%d",&v);
    struct Node* p2 = NULL;
    struct Node* p1 = head;
    while(p1->next->data!=v) 
    {	p2=p1;
        p1=p1->next;
    }   
    printf("%d is the deleted element \n",p1->data);
    p2->next=p1->next;
    free(p1);
    }
    return head;
}

struct Node* delend(struct Node* head) 
{
    if (head == NULL) 
    { 
        printf("Memory allocation failed.\n");
        
    }
    else if(!head->next)
    {
        struct Node* p;
        p=head;
        head=NULL;
        free(p);
    }
    else
    {
        struct Node* p1=head;
        struct Node* p2=NULL;
        while(p1->next!=NULL)
        {
            p2=p1;
            p1=p1->next;
        }
     printf("data deleted is:- %d  \n",(p1->data));
        p2->next=NULL;
        free(p1);
    }
    return head; 
}
struct Node* insertafter(struct Node* head) {
    struct Node* t = (struct Node*)malloc(sizeof(struct Node)); 
    int v;
    if (t == NULL) { 
        printf("Memory allocation failed.\n");
        
    }
    else
    {
    struct Node* p1 = head;
    
     printf("enter the data for entering a node before it");
     scanf("%d",&v);
     printf("enter the data to be inserted in the new node");
     scanf("%d",&(t->data));
    while (p1 != NULL && p1->data != v) 
    {
        p1 = p1->next;
    }
    if (p1 == NULL) {
        printf("Node with value %d not found.\n", v);
    }
    t->next = p1->next;
    p1->next = t;
}
    return head; // Return the head of the list
}
struct Node* insertend(struct Node* head) 
{
    struct Node* t = (struct Node*)malloc(sizeof(struct Node)); 
    
    if (t == NULL) { 
        printf("Memory allocation failed.\n");
        
    }
    else
    {
        struct Node* p=head;
        while(p->next!=NULL)
        {
            p=p->next;
        }
     printf("enter the data to be inserted in the new node \n");
     scanf("%d",&(t->data));
        t->next=NULL;
        p->next=t;
    }
    return head; 
}
struct Node* insertBefore(struct Node* head) {// Allocate memory for the new node
    struct Node* t = (struct Node*)malloc(sizeof(struct Node)); 
    int v;
    if (t == NULL) { 
        printf("Memory allocation failed.\n");
        
    }
    else
    {
    struct Node* p1 = head;
    struct Node* p2 = NULL;
     printf("enter the data for entering a node before it");
     scanf("%d",&v);
     printf("enter the data to be inserted in the new node");
     scanf("%d",&(t->data));
    while (p1 != NULL && p1->data != v) 
    {
        p2 = p1;    
        p1 = p1->next;
    }
    if (p1 == NULL) {
        printf("Node with value %d not found.\n", v);
    }
    t->next = p1;
    p2->next = t;
}
    return head;
}
struct Node* insertBegin(struct Node* head) 
{
    struct Node* t = (struct Node*)malloc(sizeof(struct Node)); 
    
    if (t == NULL) { 
        printf("Memory allocation failed.\n");
        
    }
    else
    {
     printf("enter the data to be inserted in the new node \n");
     scanf("%d",&(t->data));
        t->next=head;
        head=t;
    }
    return head;
}
struct Node* display(struct Node* head) 
{
    struct Node* t = (struct Node*)malloc(sizeof(struct Node)); 
    
    if (t == NULL) { 
        printf("Memory allocation failed.\n");
        
    }
    else
    {
        struct Node* p;
        p=head;
     while(p!=NULL)
     {
        printf("%d \t",p->data);
        p=p->next;
    }}
    return head;
}
int main()
{
    int c;
    struct Node* head=NULL;
    do
    {
        printf(" \n enter 1 for insert begin \n 2 for node before \n 3 for insert after \n 4 for insert at end \n 5 for display \n 6 for delete end \n 7 for delete before a node info given \n 8 for delete after a node info given \n 9 for secondlast delete \n 10 for insert at kth position \n 11 for delete at position \n 12 for reverse \n 13 for delete duplicate \n 14 for delete alternate node \n 15 for insert at Alternate node");
        scanf("%d",&c);
        switch(c)
        {
            case 1:
            head=insertBegin(head);
            break;
            case 2:
            head=insertBefore(head);
            case 3:
            head=insertafter(head);
            break;
            case 4:
            head=insertend(head);
            break;
            case 5:
            display(head);
            break;
            case 6:
            delend(head);
            break;
            case 7:
            delbefore(head);
            break;
            case 8:
            delafter(head);
            break;
            case 9:
            secolast(head);
            break;
            case 10:
            head=insertpos(head);
            break;
            case 11:
            delpos(head);
            break;
            case 12:
            head=rev(head);
            break;
            case 13:
            head=duplicate(head);
            break;
            case 14:
            delalter(head);
            break;
            case 15:
            head=insalter(head);
            break;
            default:
            printf("invalid \n");
        }
    }while(1);
    return 0;
}
