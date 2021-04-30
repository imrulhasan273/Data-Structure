# Data-Structure

---

# **Linked List**

---

## Singly Linked List

```cpp
#include<stdio.h>
#include<stdlib.h>
struct Node
{
    int data;                //4 bytes
    struct Node* next;       //4 bytes
};
struct Node* head;
void InsertStart(int x)
{
    printf("data: %d\n",x);
    struct Node* temp = (Node*)malloc(sizeof(struct Node));     //Node* temp = new Node();
    temp->data = x;
    if(head==NULL)
        temp->next = NULL;
    else
        temp->next = head;  //address containing in head will set in temp->next
    head = temp;            //address of head contains temp(new value)
}
void InsertEnd(int x)
{
    printf("data: %d\n",x);
    struct Node* temp = (Node*)malloc(sizeof(struct Node));
    temp->data = x;
    if(head==NULL)
    {
        temp->next = NULL;
        head = temp;
        return;
    }
    struct Node* ptr = head;
    while(ptr->next != NULL)
    {
        ptr = ptr->next;
    }
    temp->next = ptr->next;
    ptr->next = temp;
}
void InsertPosition(int n,int data)
{
    printf("pos: %d, data: %d\n", n, data);
    int i;
    struct Node* temp1 = (Node*)malloc(sizeof(struct Node));
    temp1->data = data;
    temp1->next = NULL;
    if(n==1){
        temp1->next = head;
        head = temp1;
        return;
    }
    struct Node* temp2 = head;
    for(i=2;i<n;i++)
    {
        temp2 = temp2->next;
    }
    temp1->next = temp2->next;
    temp2->next = temp1;
}
void DeleteStart()
{
    struct Node* toDelete;
    if(head == NULL)
        return;
    toDelete = head;
    head = head->next;
    printf("Data: %d\n", toDelete->data);
    free(toDelete);
}
void DeletePosition(int n)
{
    printf("pos: %d\n", n);
    struct Node* temp1 = head;
    if(n==1)
    {
        head = temp1->next; //head now points to second node
        free(temp1);
        return;
    }
    int i;
    for(i=2;i<n;i++)
    {
        temp1 = temp1->next;
    }
    //temp1 points to (n-1)th node
    struct Node* temp2 = temp1->next;   //nth node
    temp1->next = temp2->next; //(n+1)th node
    free(temp2);    //C++: delete(temp2)
}
void DeleteValue(int data)
{
    printf("data: %d\n", data);
    struct Node* del = head;
    struct Node* prev;
    if(del->data==data)
    {
        head = del->next;
        free(del);
        return;
    }
    while(del!=NULL)
    {
        prev = del; //Preserve the last del Node info
        del = del->next;
        if(del->next==NULL)
            return;
        else if(del->data==data)
            break;
    }
    //now del ==> Which will be deleted | prev ==> prev Node of Deleted Node.
    prev->next = del->next;
    free(del);
}
void Print()
{
    struct Node* temp = head;
    printf("[LINKED_LIST]: ");
    while(temp != NULL)
    {
        printf(" %d", temp->data);
        temp = temp->next;
    }
    printf("\n");
}
int main()
{
    head = NULL;    //head contains only address. So there is nothing like head->data or head->next here....

    printf("\nINSERTION ON STARING POSITION\n------------------------------\n");
    InsertStart(6);
    Print();
    InsertStart(2);
    Print();
    InsertStart(4);
    Print();
    InsertStart(5);
    Print();

    printf("\nINSERTION ON ENDING POSITION\n------------------------------\n");
    InsertEnd(99);
    Print();
    InsertEnd(44);
    Print();
    InsertEnd(77);
    Print();

    printf("\nINSERTION NODE ON ANY POSITION: GIVEN (POSITION,DATA)\n-----------------------------------------------------\n");
    InsertPosition(1,2);
    Print();
    InsertPosition(4,12);
    Print();
    InsertPosition(5,31);
    Print();
    InsertPosition(3,22);
    Print();
    InsertPosition(5,20);
    Print();
    InsertPosition(4,84);
    Print();
    InsertPosition(8,55);
    Print();
    InsertPosition(9,19);
    Print();


    printf("\nDELETE NODE FROM STARING POSITION\n------------------------\n");
    DeleteStart();
    Print();
    DeleteStart();
    Print();
    DeleteStart();
    Print();

    printf("\nDELETE NODE IN ANY POSITION: GIVEN (POSITION)\n---------------------------------------------\n");
    DeletePosition(1);
    Print();
    DeletePosition(4);
    Print();
    DeletePosition(6);
    Print();


    printf("\nDELETE NODE WHEN FOUND FIRST: GIVEN VALUE\n-----------------------------------------\n");
    DeleteValue(31);
    Print();
    DeleteValue(12);
    Print();
    DeleteValue(19);
    Print();
    DeleteValue(77);
    Print();
    DeleteValue(4);
    Print();
    DeleteValue(65);
    Print();

    return 0;
}
```



