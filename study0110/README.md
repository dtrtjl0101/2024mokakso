# 2024mokakso
## 순차 자료구조와 선형리스트
### 순차 자료구조
#### 순차 자료구조 개념
* 메모리의 저장 시작 위치부터 빈자리 없이 자료를 순서대로 연속하여 저장한다.
* 논리적인순서와 물리적순서가 동일
* 배열을 이용한 구현
* 삽입, 삭제 연산을 해도 빈자리 없이 자료가 순서대로 연속하여 저장된다.
* 원소들을 순서대로 나열한 리스트를 `선형리스트`라고한다.
#### 선형리스트란?
* 메모리에 저장하는 구현 방식에 따라 선형 순차 리스트와 선형연결리스트로 나뉜다.
### 선형리스트에서 원소 삽입
* 원소를 삽입할 자리를 만들려면 삽입할 위치 다음에 있는 원소를 모두 한자리씩 뒤로 옮겨야한다.
* 필요한 이동횟수는 n-k+1(마지막 원소의 인덱스- 삽입할 자리의 인덱스+1)이다.
### 선형리스트에서 원소 삭제
* 원소를 삭제한 위치 뒤에 있는 원소를 모두 한 자리씩 앞으로 옮겨야한다.
* 필요한 이동횟수는 n-k(마지막 원소의 인덱스-삭제한 원소의 인덱스)
### 선형 리스트 프로그램
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
    int i,k=0,move=0;    //move는 자리 이동 횟수 카운터
    for(i=0;i<n;i++){    //원소의 크기를 비교하여 삽입 위치 k찾기
        if(L[i]<=x&&x<=L[i+1]){
            k=i+1;
            break;
        }
    }
    if(i==n)    //삽입 원소가 가장 큰 원소인 경우
        k=n;
    for(i=n;i>k;i--){    //마지막 원소부터 k+1원소까지 뒤로 자리이동
        L[i]=L[i-1];
        move++;
    }
    L[k]=x;    //자리 이동하여 만든 자리 k에 삽입 원소 저장
    return move;
}
int deleteElement(int L[],int n, int x){
    inti,k=n,move=0;    //move는 자리이동횟수 카운터
    for(i=0;i<n;i++){    //원소의 크기를 비교하여 삭제 위치 K찾기
        if(L[i]=x){
            k=i;
            break;
        }
    }
    if(i==n)
        move=n;
    for(i=k;i<n;i++){    //k+1부터 마지막 원소까지 앞으로 자리이동
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
    int i,move,size=6;    //size는 리스트에있는 원소의 개수
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
* 지수가 n인 다항식은 최다항개수가 n+1개이므로 n+1개인 배열을 사용해서 순차 자료구조로 표현가능.
* 하지만 차수와 항의 개수 차이가 심한 희소 다항식은 메모리가 낭비된다.
* 희소 다항식은 항의 개수에 따라 배열크기를 결정하는것이 효율적
    * <지수, 계수>쌍을 2차원 배열로 저장.
#### addPoly.h
```c
#pragma once
#define MAX(a,b) ((a>b)?a:b)
#define MAX_DEGREE 50
typedef struct{    //구조체 정의
    int degree;    //다항식의 차수를 저장할 변수
    float coef[MAX_DEGREE];    // 다항식의 가가 항의 계수를 저장할 1차원 배열
}polynomial;
polynomial addPoly(polynomial A,polynomial B);
void printPoly(polynomial P);
```
#### addPoly.c
```C
#include "addPoly.h"
polynomial addPoly(polynomial A,polynomial B){
    polynomial C;    //다항식덧셈의결과 다항식을 저장할 구조체 변수 선언
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
    return C;    // 다항식 덧셈의 결과 다항식 C를 반환
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
    polynomial A={3,{4,3,5,0}};    //다항식 A의초기화
    polynomial B={4,{3,1,0,2,1}};    //다항식 B의 초기화
    polynomial C;
    C=addPoly(A,B);    //다항식 A,B에 대한 덧셈을 수행하기 위해 addPoly함수호출
    printf("\n A(x)="); printPoly(A);    //다항식 A출력
    printf("\n B(x)="); printPoly(B);    //다항식 B출력
    printf("\n C(x)="); printPoly(C);    //다항식 C출력
    getchar(); return 0;
}
```
