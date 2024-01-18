# 2024mokakso
## 연결 자료구조와 연결리스트
### 연결 자료구조
#### 연결 자료구조 개념
* 순차 자료구조의 연산시간과 저장 공간에 대한 문제를 개선한 자료 표현방법
* 논리적인 순서와 물리적인 순서가 일치하지 않아도 됨
* 다음 원소의 주소에 의해 순서가 연결되는 구현방식
* 포인터를 이용한 구현
* 연결 자료구조의 원소는 <원소,주소>단위인 노드로 구성
```c
typedef struct Node{
    char data[4];
    struct Node* link;
};
```
#### 단순연결리스트
* 노드의 링크 필드가 하나
#### 단순연결 리스트 삽입,삭제 프로그램
##### LinkedList.h
```c
#pragma once
typedef struct ListNode{
    char data[4];
    struct ListNode* link;
}listNode;
typedef struct{
    listNode* head;
}linkedList_h;
linkedList_h* createLinkedList_h(void);
void freeLinkedList_h(linkedList_h * L);
void printList(linkedList_h * L);
void insertFirstNode(linkedList_h * L, char* x);
void insertMiddleNode(linkedList_h * L, listNode * pre, char* x);
void insertLastNode(linkedList_h * L,char* x);
void deleteNode(linkedList_h* L, listNode* p);
listNode* searchNode(linkedList_h* L, char*x);
void reverse(linkedList_h* L);
```
##### LinkedList.c
```c
#include<stdio.h>
#include<stdlib.h>
#include<string.h>
#include "LinkedList.h"
linkedList_h* createLinkedList_h(void){
    linkedList_h* L;
    L=(linkedList_h*)malloc(sizeof(linkedList_h));
    L->head=NULL;
    return L;
}
void freeLinkedList_h(linkedList_h* L){
    listNode* p;
    while(L->head!=NULL){
        p=L->head;
        L->head=L->head->link;
        free(p);
        p=NULL;
    }
}
void printList(linkedList_h* L){
    listNode* p;
    printf("L=(");
    p=L->head;
    while(p!=NULL){
        printf("%s",p->data);
        p=p->link;
        if(p!=NULL)printf(", ");
    }
    printf(") \n");
}
void insertFirstNode(linkedList_h *L,char *x){
    listNode* newNode;
    newNode=(listNode*)malloc(sizeof(listNode));
    strcpy(newNode->data,x);
    newNode->link=L->head;
    L->head=newNode;
}
void insertMiddleNode(linkedList_h *L,listNode *pre,char *x){
    listNode* newNode;
    newNode=(listNode*)malloc(sizeof(listNode));
    strcpy(newNode->data,x);
    if(L->head==NULL){
        newNode->linke=NULL;
        L->head=newNode;
    }else if(pre==NULL){
        newNode->link=L->head;
        L->head=newNode;
    }else{
        newNode->link=pre->link;
        pre->link=newNode;
    }
}
void insertLastNode(linkedList_h *L,char *x){
    listNode* newNode;
    listNode* temp;
    newNode=(listNode*)malloc(sizeof(listNode));
    strcpy(newNode->data,x);
    newNode->link=NULL;
     if(L->head==NULL){
        L->head=newNode;
        return ;
     }
     temp=L->head;
     while(temp->link!=NULL)temp=temp->link;
     temp->link=newNode;
}
void deleteNode(linkedList_h* L,listNode*p){
    listNode* pre;
    if(L->head==NULL)return;
    if(L->head->link==NULL){
        free(L->head);
        L->head=NULL;
        return;
    }else if(p==NULL)return;
    else{
        pre=L->head;
        while(pre->link;){
            pre=pre->link;
        }
    pre->link=p->link;
    free(p);
    }
}
listNode* searchNode(linkedList_h* L,char*x){
    listNode *temp;
    temp=L->head;
    while(temp!=NULL){
        if(strcmp(temp->data,x)==0)return temp;
        else temp=temp->link;
    }
    return  teml;
}
void reverse(linkedList_h * L){
    listNode* p;
    listNode* q;
    listNode* r;
    p=L->head;
    q=NULL;
    r=NULL;
    while(p!=NULL){
        r=q;
        q=p;
        p=p->link;
        q->link=r;
    }
    L->head=q;
}
```
##### ex.c
```c
#include<stdio.h>
#include "LinkedList.h"
int main(void){
    linkedList_h* L;
    listNode*p;
    L=createLinkedList_h();
    printf("\n리스트에 [월],[수],[일]노드 집어넣기\n");
    insertLastNode(L,"월");insertLastNode(L,"수");insertLastNode(L,"일");
    printList(L);
    printf("\n리스트 [수]노드 찾기\n");
    p=searchNode(L,"수");
    if(p==NULL)printf("찾는 노드가 없습니다\n");
    else("찾았습니다\n");
    printf("\n리스트 [수]뒤에 [금]노드 집어넣기\n");
    insertMiddleNode(L,p,"금");
    printList(L);
    printf("\n리스트에 [일]노드 집어넣기\n");
    p=searchNode(L,"일");
    deleteNode(L,p);
    printList(L);
   printf("\n리스트공간해제해 공백리스트 만들기\n");
    freeLinkedList_h(L);
    printList(L);
    return 0;
}
```
#### 원형연결리스트
* 단순 연결 리스트에서 마지막 노드가 리스트의 첫 번째 노드를 가리키게 하여 리스트 구조를 원형으로 만든 연결 리스트를 원형연결리스트라고한다.
* 원형연결리스트에서는 리스트의 마지막노드에 삽입하는것이 곧 리스트의 첫 번째에 노드를 삽입하는것과 같다.
#### 원형연결리스트의 삽입삭제
##### CircularLinkedList.h
```c
#pragma once
typedef struct ListNode{
    char data[4];
    struct ListNode* link;
}listNode;
typedef struct{
    listNode* head;
}linkedList_h;
linkedList_h* createLinkedList_h(void);
void printList(linkedList_h * L);
void insertFirstNode(linkedList_h * CL, char* x);
void insertMiddleNode(linkedList_h * CL, listNode * pre, char* x);
void deleteNode(linkedList_h* CL, listNode* p);
listNode* searchNode(linkedList_h* CL, char*x);
```
##### CircularLinkedList.c
```c
#include<stdio.h>
#include<string.h>
#include "CircularLinkedList.h"
linkedList_h* createLinkedList_h(void){
    linkedList_h* CL;
    CL=(linkedList_h*)malloc(sizeof(linkedList_h));
    CL->head=NULL;
    return CL;
}
void printList(linkedList_h* CL){
    listNode* p;
    printf("CL=(");
    p=CL->head;
    while(p==NULL){
        printf(") \n");
    }
    do{
        printf("%s",p->data);
        p=p->link;
        if(p!=CL->head)printf(", ");
    }while(p!=CL->head);
    printf(") \n");
}
void insertFirstNode(linkedList_h *CL,char *x){
    listNode* newNode, *temp;
    newNode=(listNode*)malloc(sizeof(listNode));
    strcpy(newNode->data,x);
    if(CL->head==NULL)
    newNode->link=L->head;
    L->head=newNode;
}
void insertMiddleNode(linkedList_h *L,listNode *pre,char *x){
    listNode* newNode;
    newNode=(listNode*)malloc(sizeof(listNode));
    strcpy(newNode->data,x);
    if(L->head==NULL){
        newNode->linke=NULL;
        L->head=newNode;
    }else if(pre==NULL){
        newNode->link=L->head;
        L->head=newNode;
    }else{
        newNode->link=pre->link;
        pre->link=newNode;
    }
}
void insertLastNode(linkedList_h *L,char *x){
    listNode* newNode;
    listNode* temp;
    newNode=(listNode*)malloc(sizeof(listNode));
    strcpy(newNode->data,x);
    newNode->link=NULL;
     if(L->head==NULL){
        L->head=newNode;
        return ;
     }
     temp=L->head;
     while(temp->link!=NULL)temp=temp->link;
     temp->link=newNode;
}
void deleteNode(linkedList_h* L,listNode*p){
    listNode* pre;
    if(L->head==NULL)return;
    if(L->head->link==NULL){
        free(L->head);
        L->head=NULL;
        return;
    }else if(p==NULL)return;
    else{
        pre=L->head;
        while(pre->link;){
            pre=pre->link;
        }
    pre->link=p->link;
    free(p);
    }
}
listNode* searchNode(linkedList_h* L,char*x){
    listNode *temp;
    temp=L->head;
    while(temp!=NULL){
        if(strcmp(temp->data,x)==0)return temp;
        else temp=temp->link;
    }
    return  teml;
}
void reverse(linkedList_h * L){
    listNode* p;
    listNode* q;
    listNode* r;
    p=L->head;
    q=NULL;
    r=NULL;
    while(p!=NULL){
        r=q;
        q=p;
        p=p->link;
        q->link=r;
    }
    L->head=q;
}
```
##### ex.c
```c
#include<stdio.h>
#include "LinkedList.h"
int main(void){
    linkedList_h* L;
    listNode*p;
    L=createLinkedList_h();
    printf("\n리스트에 [월],[수],[일]노드 집어넣기\n");
    insertLastNode(L,"월");insertLastNode(L,"수");insertLastNode(L,"일");
    printList(L);
    printf("\n리스트 [수]노드 찾기\n");
    p=searchNode(L,"수");
    if(p==NULL)printf("찾는 노드가 없습니다\n");
    else("찾았습니다\n");
    printf("\n리스트 [수]뒤에 [금]노드 집어넣기\n");
    insertMiddleNode(L,p,"금");
    printList(L);
    printf("\n리스트에 [일]노드 집어넣기\n");
    p=searchNode(L,"일");
    deleteNode(L,p);
    printList(L);
   printf("\n리스트공간해제해 공백리스트 만들기\n");
    freeLinkedList_h(L);
    printList(L);
    return 0;
}
```