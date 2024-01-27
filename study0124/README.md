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