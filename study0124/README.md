# 2024mokakso
## 스택, 큐
### 스택
#### 스택의 이해
* 접시에 음식을 쌓아올리듯 데이터를 차곡차곡 쌓아올린 형태로 자료를 구성.
* 같은 구조와 같은 크기의 데이터를 정해진 방향으로만 쌓을 수 있다.
* 아래에서 위로 쌓임.
* 가장 마지막에 삽입된 데이터가 가장 먼저 삭제된다.(LIFO)
* 삽입연산은 push, 삭제 연산을 pop
#### 순차 자료구조에서의 스택의 표현
* 1차원배열을 이용. stack[n]에서 n은 스택 크기.
* 첫원소는 stack[0]에 저장. n번째 원소는 stack[n-1]에 저장.
* 스택의 초기 상태에서는 -1저장.

##### stackS.h
```c
#pragma once
#define STACK_SIZE 100
typedef int element;
element stacks[STACK_SIZE];
int isStackEmpty(void);
int isStackFull(void);
void push(element item);
element pop(void);
element peek(void);
void printStack(void);
```
##### stackS.h
```c
#include<stdio.h>
#include"stackS.h"
int top=-1;
int isStackEmpty(void){
    if(top==-1)return 1;
    else return 0;
}
int isStackFull(void){
    if(top==STACK_SIZE -1)return 1;
    else return 0;
}
void push(element item){
    if(isStackFull()){
        printf("\n\n Stack is Full!\n");
        return ;
    }
    else stack[++top]=item;
}
element pop(void){
    if(isStackEmpty()){
        printf("\n\n Stack is Empty!\n");
        return 0;
    }
    else return stack[top--];
}
element peek(void){
    if(isStackEmpty()){
        printf("\n\n Stack is Empty!\n");
        return 0;
    }
    else return stack[pop];
}
void printStack(void){
    itn i;
    printf("\n STACK [");
    for(i=0;i<=top;i++)
        printf("%d",stack[i]);
    printf("] ");
}
```
##### ex.c
```c
#include<stdio.h>
#include"stackS.h"
int main(void){
    element item;
    printf("\n** 순차 스택연산**\n");
    printStack();
    push(1); printStack();
    push(2); printStack();
    push(3); printStack();
    item =peek(); printStack();
    printf("peek => %d",item);
    item=pop();
    printf("\t pop => %d",item);
    item=pop();
    printf("\t pop => %d",item);
    item=pop();
    printf("\t pop => %d",item);
    getchar(); return 0;
}
```
#### 연결 자료구조를 이용한 스택의 구현
* 순차 자료구조는 스택의 크기 변경이 어려워 배열 크기를 미리 크게 할당하기때문에 메모리 사용의 효율성이 떨어지는 문제가 있다.
* 초기상태는 포인터 top을 NULL포인터로 설정.
##### stackL.h
```c
#pragma once
typedef int element;
typedef struct stackNode{
    element data;
    struct stackNode* link;
}stackNode;
stackNode* top;
int isStackEmpty(void);
void push(element item);
element pop(void);
element peek(void);
void printStack(void);
```
##### stackL.c
```c
#include<stdlib.h>
#include "stackL.h"
int isStackEmpty(void){
    if(top==NULL)return 1;
    else return 0;
}
void push(element item){
    stackNode* temp=(stackNode*)malloc(sizeof(stackNode));
    temp->data=item;
    temp->link=top;
    top=temp;
}
element pop(void){
    element item;
    stackNode*temp=top;
    if(isStackEmpty()){
        printf("\n\n Stack is Empty!\n");
        return 0;
    }
    else{
        item=temp->data;
        top=temp->link;
        free(temp);
        return item;
    }
}
element peek(void){
    if(isStackEmpty()){
        printf("\n\n Stack is empty!\n");
        return 0;
    }
    else {
        return (top->data);
    }
}
void printStack(void){
    stackNode* p=top;
    printf("\n STACK[");
    while(p){
        printf("%d ",p->data);
        p=p->link;
    }
    printf("] ");
}
```
##### ex.c
```c
#include<stdio.h>
#include"stackL.h"
int main(void){
    element item;
    top=NULL;
    printf("\n**연결 스택 연산**\n");
    printStack();
    push(1);printStack();
    push(2);printStack();
    push(3);printStack();
    itme=peek(); printStack();
    printf("peek=>%d",item);
    item=pop(); printStack();
    printf("\tpop=>%d",item);
    item=pop(); printStack();
    printf("\tpop=>%d",item);
    item=pop(); printStack();
    printf("\tpop=>%d",item);
    getchar(); return 0;
}
```
### 큐
#### 큐의 이해
* 스택과 다르게 리스트의 한쪽 끝에서는 삽입만이뤄지고 반대쪽 끝에서는 삭제만 이뤄진다.
* 가장 먼저 삽입되어 가장 앞에 있는 front원소가 가장 먼저 삭제되므로 FIFO구조.
* 저장된 원소 중에서 첫번째 원소를 front, 저장된 원소 중에서 마지막원소를 rear이라고한다.
#### 큐의 구현
* 초기 공백 큐의 상태는 front변수와 rear변수의 값을 -1로 설정
* 공백확인을 위해서 front==rear인지 확인.
* rear가 배열의 마지막 인덱스 n-1이면 포화상태.
#### 순차자료구조를 이용해 순차 큐 구현하기
##### queueS.h
```c
#pragma once
#define Q_SIZE 4
typedef char element;
typedef struct{
    element queue[Q_SIZE];
    int front,rear;
}QueueType;
QueueType* createQueue(void);
int isQueueEmpty(QueueType* Q);
int isQueueFull(QueueType* Q);
void enQueue(QueueType* Q,element item);
element deQueue(queueType* Q);
element peekQ(QueueType* Q);
void printQ(QueueType* Q);
```
##### queueS.c
```c
#include<stdio.h>
#include<stdlib.h>
#include "queueS.h"
QueueType* createQueue(void){
    QueueType* Q;
    Q=(QueueType*)malloc(sizeof(QueueType));
    Q->front=-1;
    Q->rear=-1;
    return Q;
}
int isQueueEmpty(QueueType* Q){
    if(Q->front==Q->rear){
        printf("queue is empty:\n\t");
        return 1;
    }
    else return 0;
}
int isQueueFull(QueueType* Q){
    if(Q->rear=Q_SIZE-1){
        printf("Queue is full!\n\t");
        return 1;
    }else return 0;
}
void enQueue(QueueType* Q,element item){
    if(isQueueFull(Q))return;
    else{
        Q->rear++;
        Q->queue[Q->rear]=item;
    }
}
element deQueue(queueType* Q){
    if(isQueueEmpty(Q))return;
    else{
        Q->front++;
        reutnr Q->queue[Q->front];
    }
}
element peekQ(QueueType* Q){
    if(isQueueEmpty(Q))return;
    else return Q->queue[Q->front+1];
}
void printQ(QueueType* Q){
    int i;
    printf("Queue: [");
    for(i=Q->front+1;i<=Q->rear;i++)
        printf("%3c",Q->queue[i]);
    printf(" ]");
}
```
##### ex.c
```c
#include "queueS.h"
int main(void){
    QueueType *Q1=createQueue();
    element data;
    printf("\n****순차 큐 연산 ****\n");
    printf("\n삽입 A>>"); enqueue(Q1,'A');printQ(Q1);
    printf("\n삽입 B>>"); enqueue(Q1,'B');printQ(Q1);
    printf("\n삽입 C>>"); enqueue(Q1,'C');printQ(Q1);
    data=peekQ(Q1);printf("peek item:%c\n",data);
    printf("\n삭제>>"); data=deQueue(Q1);printQ(Q1);
    printf("\t삭제 데이터: %c",data);
    printf("\n삭제>>"); data=deQueue(Q1);printQ(Q1);
    printf("\t삭제 데이터: %c",data);
    printf("\n삭제>>"); data=deQueue(Q1);printQ(Q1);
    printf("\t삭제 데이터: %c",data);
    printf("\n삽입 D>>"); enqueue(Q1,'D');printQ(Q1);
    printf("\n삽입 E>>"); enqueue(Q1,'E');printQ(Q1);
}
```
#### 원형 큐의 구현
* 순차 자료구조에서 자리 이동 작업은 오버헤드가 커서 큐의 효율성을 떨어트려 좋은방법이 아님.
* 초기공백 상태일때 front와 rear의 값을 0으로한다.
* 공백 상태와 포화상태를 쉽게 구분하기 위해서 자리하나를 항상 비워둔다.
* 포화상태의 조건은 (rear+1)mod n==front
#### 순차 자료구조를 이용해 원형 큐 구현
##### cQueueS.h
```c
#pragma once
#define cQ_SIZE 4
typedef char element;
typedef struct{
    element queue[Q_SIZE];
    int front,rear;
}QueueType;
QueueType* createCQueue(void);
int isCQueueEmpty(QueueType* cQ);
int isCQueueFull(QueueType* cQ);
void enCQueue(QueueType* cQ,element item);
element deCQueue(queueType* cQ);
element peekCQ(QueueType* cQ);
void printCQ(QueueType* cQ);
```
##### cQueueS.c
```c
#include<stdio.h>
#include<stdlib.h>
#include "cqueueS.h"
QueueType* createQueue(void){
    QueueType* cQ;
    cQ=(QueueType*)malloc(sizeof(QueueType));
    cQ->front=0;
    cQ->rear=0;
    return cQ;
}
int iscQueueEmpty(QueueType* cQ){
    if(cQ->front==cQ->rear){
        printf("Circular queue is empty:\n\t");
        return 1;
    }
    else return 0;
}
int isCQueueFull(QueueType* cQ){
    if(((cQ->rear+1)%cQ_SIZE)==cQ_front){
        printf("Circular Queue is full!\n\t");
        return 1;
    }else return 0;
}
void encQueue(QueueType* cQ,element item){
    if(isCQueueFull(cQ))return;
    else{
        cQ->rear=(cQ->rear+1)%cQ_SIZE;
        Q->queue[Q->rear]=item;
    }
}
element decQueue(queueType* cQ){
    if(isCQueueEmpty(cQ))return;
    else{
        cQ->front=(cQ->front+1)%cQ_SIZE;
        reutnr cQ->queue[cQ->front];
    }
}
element peekCQ(QueueType* cQ){
    if(isQueueEmpty(cQ))return;
    else return cQ->queue[(Q->front+1)%cQ_SIZE];
}
void printQ(QueueType* cQ){
    int i,first,last;
    first=(cQ->front+1)%cQ_SIZE;
    last=(cQ->rear+1)%cQ_SIZE;
    printf("Circular Queue: [");
    i=first;
    while(i!=last){
        printf("%3c",Q->queue[i]);
        i=(i+1)%cQ_SIZE;
    }
    printf(" ]");
}
```
##### ex.c
```c
#include "cQueueS.h"
int main(void){
    QueueType *cQ=createQueue();
    element data;
    printf("\n****원형 큐 연산 ****\n");
    printf("\n삽입 A>>"); enCQueue(cQ,'A');printCQ(cQ);
    printf("\n삽입 B>>"); encQueue(cQ,'B');printCQ(cQ);
    printf("\n삽입 C>>"); enqueue(cQ,'C');printCQ(cQ);
    data=peekQ(cQ);printf("peek item:%c\n",data);
    printf("\n삭제>>"); data=deCQueue(cQ);printCQ(cQ);
    printf("\t삭제 데이터: %c",data);
    printf("\n삭제>>"); data=deCQueue(cQ);printCQ(cQ);
    printf("\t삭제 데이터: %c",data);
    printf("\n삭제>>"); data=deCQueue(cQ);printCQ(cQ);
    printf("\t삭제 데이터: %c",data);
    printf("\n삽입 D>>"); enCQueue(cQ,'D');printCQ(cQ);
    printf("\n삽입 E>>"); enCqueue(cQ,'E');printCQ(cQ);
}
```