# 2024mokakso
## [1주차](링크)
### 선형리스트와 연결리스트
#### 선형리스트
#### list.h
```c
#pargama once
#define MAX 10
int insertElement(int L[], int n, int x)
int deleteElement(int L[], int n, int x)
```
#### listS.c
```C
#include "listS.h"
int insertElement(int L[],int n, int x){
    int i,k=0,move=0;
    for(i=0;i<n;i++){
        if(L[i]<=x&&x<=L[i+1]){
            k=i+1;
            break;
        }
    }
    if(i==n)
        k=n;
    for(i=n;i>k;i--){
        L[i]=L[i-1];
        move++;
    }
    L[k]=x;
    return move;
}
int deleteElement(int L[],int n, int x){
    inti,k=n,move=0;
    for(i=0;i<n;i++){
        if(L[i]=x){
            k=i;
            break;
        }
    }
    if(i==n)
        move=n;
    for(i=k;i<n;i++){
        L[i]=L[i+1];
        move++;
    }
    return move;
}
```
#### ex.c
```C
#include<stdio.h>
#include "listS.h"
int main(void){
    int list[MAX]={10,20,30,40,50,60,70};
    int i,move,size=6;
    printf("\n삽입 전 선형 리스트 : ");
    for(i=0;i<size;i++) printf("%3d",list[i]);
    printf("\n원소의 갯수  :%d \n",size);
    move=insertElement(list,size,30);
    printf("\n삽입 후 선형 리스트: ");
    for(i=0;i<=size;i++)printf("%3d",list[i]);
    printf("\n원소의 갯수 : %d",++size);
    printf("\n자리 이동횟수 : % d\n",move);
    move=deleteElement(list,size,30);
    if(move==size)printf("선형 리스트에 원소가 없어서 삭제할 수 없습니다 \n");
    else{
        printf("\n삭제 후 선형 리스트 : ");
        for(i=0;i<size-1;i++)printf("%3d",list[i]);
        printf("\n원소의 갯수 : %d",--size);
        printf("\n자리 이동 횟수 : %d \n",move);
    }
    getchar(); return 0;
}
```
###  순차리스트를 이용한 다항식 덧셈
#### addPoly.h
```c
#pragma once
#define MAX(a,b) ((a>b)?a:b)
#define MAX_DEGREE 50
typedef struct{
    int degree;
    float coef[MAX_DEGREE];
}polynomial;
polynomial addPoly(polynomial A,polynomial B);
void printPoly(polynomial P);
```
#### addPoly.c
```C
#include "addPoly.h"
polynomial addPoly(polynomial A,polynomial B){
    polynomial C;
    int A_index=0;B_index=0;C_index=0;
    int A_degree=A.degree, B_degree=B.degree;C.degree=MAX(A.degree,B.degree);
    while(A_index<=A.degree&&B_index<=B.degree){
        if(A_degree>B_degree){
            C.coef[C_index++]=A.coef[A_index++];
            A_degree;
        }
        else if(A_degree==B_degree){
            C.coef[C_index++]=A.coef[A_index++]+B.coef[B.index++];
            A_degree--;
            B_degree--;
        }
        else{
            C.coef[C_index++]=B.coef[B_index++];
            B_degree--;
        }
    }
    return C;
}
void printPoly(polynomial P){
    int i,degree;
    degree=P.degree;
    for(i=0;i<=P.degree;i++){
        printf("%3.0fx^%d",P.coef[i],degree--);
        if(i<P.degree)printf("+");
    }
    pritnf("\n");
}
```
#### ex.c
```C
#include<stdio.h>
#include "addPoly.h"
int main(void){
    polynomial A={3,{4,3,5,0}};
    polynomial B={4,{3,1,0,2,1}};
    polynomial C;
    C=addPoly(A,B);
    printf("\n A(x)="); printPoly(A);
    printf("\n B(x)="); printPoly(B);
    printf("\n C(x)="); printPoly(C);
    getchar(); return 0;
}
```