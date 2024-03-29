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
typedef struct ListNode{    //단순 연결 리스트의 노드 구조를 구조체로 정의
    char data[4];
    struct ListNode* link;
}listNode;
typedef struct{ //리스트의 시작을 나타내는 head노드를 구조체로 정의
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
linkedList_h* createLinkedList_h(void){ //공백연결리스트를 생성하는 연산
    linkedList_h* L;
    L=(linkedList_h*)malloc(sizeof(linkedList_h));
    L->head=NULL;   //공백리스트이므로 NULL로설정
    return L;
}
void freeLinkedList_h(linkedList_h* L){ //연결리스트의 전체메모리를 해제하는 연산
    listNode* p;
    while(L->head!=NULL){
        p=L->head;
        L->head=L->head->link;
        free(p);
        p=NULL;
    }
}
void printList(linkedList_h* L){    //연결리스트를 순서대로 출력하는 연산
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
void insertFirstNode(linkedList_h *L,char *x){  //첫번째 노드로 삽입하는 연산
    listNode* newNode;
    newNode=(listNode*)malloc(sizeof(listNode));    //삽입할 새노드 할당
    strcpy(newNode->data,x);    //새노드의 데이터 필드에 x저장
    newNode->link=L->head;
    L->head=newNode;
}
void insertMiddleNode(linkedList_h *L,listNode *pre,char *x){//새 노드를 pre뒤에 삽입하는 연산
    listNode* newNode;
    newNode=(listNode*)malloc(sizeof(listNode));
    strcpy(newNode->data,x);
    if(L->head==NULL){  //공백 리스트인 경우
        newNode->linke=NULL;    //새 노드를 첫번째이자 마지막 노드로 연결
        L->head=newNode;
    }else if(pre==NULL){    //삽입 위치를 저장하는 포인터pre가 NULL인경우
        newNode->link=L->head;  //새노드를 첫번째 노드로 삽입
        L->head=newNode;
    }else{
        newNode->link=pre->link;    //포인터 pre의노드 뒤에 새 노드연결
        pre->link=newNode;
    }
}
void insertLastNode(linkedList_h *L,char *x){   //마지막 노드로 삽입하는 연산
    listNode* newNode;
    listNode* temp;
    newNode=(listNode*)malloc(sizeof(listNode));
    strcpy(newNode->data,x);
    newNode->link=NULL;
     if(L->head==NULL){ //현재리스트가 공백인경우
        L->head=newNode;    //새노드를 리스트의 시작 노드로 연결
        return ;
     }
     //현재리스트가 공백이 아닌경우
     temp=L->head;  
     while(temp->link!=NULL)temp=temp->link;    //현재리스트의 마지막 노드를 찾음
     temp->link=newNode;    //새노드를 마지막 노드의 다음노드로 연결
}
void deleteNode(linkedList_h* L,listNode*p){    //리스트에서 노드p를 삭제하는 연산
    listNode* pre;
    if(L->head==NULL)return;
    if(L->head->link==NULL){
        free(L->head);
        L->head=NULL;   
        return;
    }else if(p==NULL)return;    //삭제할 노드가 없다면 삭제연산중단
    else{   //삭제할 노드p의 선행자 노드를 포인터 pre를 이용해 찾음
        pre=L->head;
        while(pre->link;){
            pre=pre->link;
        }
    pre->link=p->link;  //삭제할 노드p의 선행자 노드와 다음 노드를 연결
    free(p);    //삭제노드의 메모리해제
    }
}
listNode* searchNode(linkedList_h* L,char*x){   //리스트에서 x노드를 탐색하는 연산
    listNode *temp;
    temp=L->head;
    while(temp!=NULL){
        if(strcmp(temp->data,x)==0)return temp;
        else temp=temp->link;
    }
    return  temp;
}
void reverse(linkedList_h * L){ //리스트의 노드 순서를 역순으로 바꾸는 연산
    listNode* p;
    listNode* q;
    listNode* r;
    p=L->head;  //포인터p를 첫번째 노드에 설정
    q=NULL;
    r=NULL;
    while(p!=NULL){ //리스트의 첫번째 노드부터 링크를 따라 다음 노드로 이동하면서 노드간의 연결을 바꿈
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
linkedList_h* createLinkedList_h(void){ //공백원형연결리스트를 생성하는 연산
    linkedList_h* CL;
    CL=(linkedList_h*)malloc(sizeof(linkedList_h));
    CL->head=NULL;
    return CL;
}
void printList(linkedList_h* CL){   //연결리스트를 순서대로 출력하는 연산
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
    newNode=(listNode*)malloc(sizeof(listNode));    //삽입할 새노드할당
    strcpy(newNode->data,x);
    if(CL->head==NULL){ //원형 연결 리스트가 공백인 경우
        CL->head=newNode;   //새 노드를 리스트의 시작 노드로 연결
        newNode->link=newNode;
    }else{  //원형연결 리스트가 공백이 아닌경우
        temp=CL->head;
        while(temp->link!=CL->head)
            temp=temp->link;
        newNode->link=temp->link;
        temp->link=newNode; //마지막 노드를 첫번째 노드인 new와 원형연결
        CL->head=newNode;
    }
}
void insertMiddleNode(linkedList_h *CL,listNode *pre,char *x){  //pre뒤에 노드를 삽입하는 연산
    listNode* newNode;
    newNode=(listNode*)malloc(sizeof(listNode));
    strcpy(newNode->data,x);
    if(CL->head==NULL){
        CL->head=newNode;
        newNode->linke=NULL;
    }else{
        newNode->link=pre->link;
        pre->link=newNode;
    }
}
void deleteNode(linkedList_h* CL,listNode*old){ //원형연결리스트 pre뒤에 있는 노드 old를 삭제하는 연산   
    listNode* pre;  //삭제할 노드의 선행자 노드를 나타내는 포인터
    if(CL->head==NULL)return;   //공백리스트인 경우 삭제연산중단
    if(CL->head->link==CL->head){   //리스트노드가 한개만 있는경우
        free(CL->head); //첫번째 노드의 메모리를해제하고
        CL->head=NULL;  //리스트 시작 포인터를 NULL로설정
        return;
    }else if(old==NULL)return;  //삭제할 노드가 없는 경우 삭제연산중단
    else{
        pre=CL->head;   //포인터 pre를 리스트의 시작 노드에 연결
        while(pre->link!=old){
            pre=pre->link;  //선행자 노드를 포인터 pre를 이용해 찾음
        }
    pre->link=old->link;
    if(old==CL->head)
        CL->head=old->link;
    free(old);  //삭제노드의 메모리를 해제
    }
}
listNode* searchNode(linkedList_h* CL,char*x){  //원형연결 리스트에서 x노드 탐색하는 연산
    listNode *temp;
    temp=CL->head;
    while(temp==NULL)return NULL;
    do{
        if(strcmp(temp->data,x)==0)return temp;
        else temp=temp->link;
    }while(temp!=CL->head);
    return  NULL;
}
```
##### ex.c
```c
#include<stdio.h>
#include "CircularLinkedList.h"
int main(void){
    linkedList_h* CL;
    listNode*p;
    CL=createLinkedList_h(); //공백 원형 연결리스트 생성
    printf("\n원형리스트에 [월]노드 집어넣기\n");
    insertLastNode(CL,"월");
    printList(CL);
    printf("\n원형리스트 [월]뒤에 [수]노드 집어넣기\n");
    p=searchNode(CL,"월");insertMiddleNode(CL,p,"수");
    printList(CL);
    printf("\n원형리스트 [수]뒤에 [금]노드 집어넣기\n");
    p=searchNode(CL,"수");insertMiddleNode(CL,p,"금");
    printList(CL);
    printf("\n원형리스트 [수]삭제하기\n");
    p=searchNode(CL,"수");deleteNode(CL,p);
    printList(CL);
    return 0;
}
```