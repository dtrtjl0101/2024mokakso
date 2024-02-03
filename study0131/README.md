# 2024mokakso
## 정렬
### 정렬의 이해
* 정렬이란 순서없이 배열된 자료를 오름차순이나 내림차순으로 재배열한 것.
* 자료를 정렬하는데 사용하는 기준이 되는 특정값을 `key`라고한다.
---
### 선택정렬
* 전체 원소 중에서 기준 위치에 맞는 원소를 선택해 자리를 교환하는 방식을 사용.
* 시간복잡도는 어떤 경우에서나 비교 횟수가 같으므로 `O(n^2)`
#### selectSort.c
```c
#include<stdio.h>
void SelectionSort(int a[],int size){
    int i,j,t,min,temp;
    for(i=0;i<size-1;i++){
        min=i;
        for(j=i+1;j<size;j++){
            if(a[j]<a[min])min=j;
        }
        temp=a[i];
        a[i]=a[min];
        a[min]=temp;
        printf("\n%d단계 : ",i+1);
        for(t=0;t<size;t++)printf("%3d",a[t]);
    }
}
```
#### ex.c
```c
#include<stdio.h>
void SelectionSort(int a[],int size);
int main(void){
    int i, list[8]={69,10,30,2,16,8,31,22}; //정렬할 원소
    int size=sizeof(list)/sizeof(list[0]);
    printf("\n정렬할 원소 : ");
    for(i=0;i<size;i++)printf("%3d",list[i]);   //정렬 전의 원소 출력
    printf("\n<<<<<선택정렬수행>>>>>>>>\n");
    SelectionSort(list,size);   //선택 정렬 함수 호출
    getchar(); return 0;
}
```
---
### 버블정렬
* 인접한 원소를 두개 비교하여 자리를 교환하는 방식을 반복하면서 정렬.
* 시간복잡도는 `O(n^2)`이다.
#### bubbleSort.c
```c
#include<stdio.h>
void bubbleSort(int a[],int size){
    int i,j,t,temp;
    for(i=size-1;i>0;i--){
        printf("\n%d단계 : ",size-i);
        for(j=0;j<i;j++){
            if(a[j]>a[j+1])
                temp=a[i];
                a[i]=a[j+1];
                a[j+1]=temp;
        }
        printf("\n\t");
        for(t=0;t<size;t++)printf("%3d",a[t]);
    }
}
```
#### ex.c
```c
#include<stdio.h>
void bubbleSort(int a[],int size);
int main(void){
    int i, list[8]={69,10,30,2,16,8,31,22}; //정렬할 원소
    int size=sizeof(list)/sizeof(list[0]);
    printf("\n정렬할 원소 : ");
    for(i=0;i<size;i++)printf("%3d",list[i]);   //정렬 전의 원소 출력
    printf("\n<<<<<버블정렬수행>>>>>>>>\n");
    bubbleSort(list,size);   //선택 정렬 함수 호출
    getchar(); return 0;
}
```
---
### 퀵 정렬
* 정렬할 전체 원소에 대해 정렬을 수행하지 않고 기준값을 중심으로 왼쪽 부분집합과 오른쪽 부분집합으로 분할.
* 왼쪽 부분집합에는 기준값보다 작은 원소이동.
* 오른쪽 부분집합에는 기준값봗 큰 원소들을 이동.
* 분할과 정복을 반봅 수행하여 완성.
* 시간 복잡도는 `O(nlogn)`
#### quickSort1.c
```c
#include<stdio.h>
int i=0;    //퀵 정렬 단계 출력용 변수
int partition(int a[],int begin,int end,int size){  // 주어진 부분집합 안에서 피봇의 위치를 확정하여 분할 위치를 정하는 연산
    int pivot,L,R,t,temp;
    L=begin; R=end;
    pivot=(begin+end)/2;    //중간에 위치한 원소를 피봇 원소로 선택
    printf("\n[%d단계 : pivot = %d]\n",++i,a[pivot]);   
        while(L<R){
            while((a[L]<a[pivot])&&(L<R))L++;
            while((a[R]>=a[pivot])&&(L<R))R--;
            if(L<R){    //L과R원소의 자리교환
                temp=a[i];
                a[i]=a[j+1];
                a[j+1]=temp;
                //L이 피봇인 경우, 변경된 피봇의 위치를 다시저장.
                if(L==pivot)pivot=R;
            }   //if(L<R)
        }   //while(L<R)
            //(L=R)이 된경우, 더이상 진행할 수 없으므로 R원소와 피봇 원소의 자리를 교환하여 마무리
        temp=a[pivot];
        a[pivot]=a[R];
        a[R]=temp;
        for(t=0;t<size;t++)printf("%4d",a[t]);  //현재의 정렬 상태 출력
        printf("\n");
        return R;   //정렬되어 확정된 피봇의 위치 방향
}
void quickSort(int a[],int begin,int end,int size){
    int p;
    if(begin<end){
        p=partition(a,begin,end,size);  //피봇의 위치에 의해 분할 위치 결정
        quickSort(a,begin,p-1,size);    //피봇의 왼쪽 부분집합에 대해 퀵정렬을 재귀호출
        quickSort(a,p+1,end,size);      //피봇의 오른쪽 부분집합에 대해 퀵 정렬을 재귀호출
    }
}
```
#### ex.c
```c
#include<stdio.h>
void quickSort(int a[],int begin,int end,int size)
int main(void){
    int i, list[8]={69,10,30,2,16,8,31,22}; //정렬할 원소
    int size=sizeof(list)/sizeof(list[0]);
    printf("\n정렬할 원소 : ");
    for(i=0;i<size;i++)printf("%3d",list[i]);   //정렬 전의 원소 출력
    printf("\n<<<<<퀵정렬수행>>>>>>>>\n");
    quickSort(list,0,size-1,size);   //퀵 정렬 함수 호출
    getchar(); return 0;
}
```
---
### 삽입정렬
* 정렬되어 있는 부분집합에 정렬할 새로운 원소의 위치를 찾아 삽입하는 방식
* 순차 정렬된 경우 시간복잡도는 O(n)이지만 역순 정렬된 경우O(n^2)
#### insetionSort.c
```c
#include<stdio.h>
void insertionSort(int a[],int size){
    int i,j,t,temp;
    for(i=1;i<size;i++){
        temp=a[i];
        j=i;
        while((j>0)&&a[j-1]>temp){
            a[j]=a[j-1];
        }
        a[j]=temp;
        printf("\n%d단계 : ",i);
        for(t=0;t<size;t++)printf("%3d",a[t]);
    }
}
```
#### ex.c
```c
#include<stdio.h>
void insertionSort(int a[],int size);
int main(void){
    int i, list[8]={69,10,30,2,16,8,31,22}; //정렬할 원소
    int size=sizeof(list)/sizeof(list[0]);
    printf("\n정렬할 원소 : ");
    for(i=0;i<size;i++)printf("%3d",list[i]);   //정렬 전의 원소 출력
    printf("\n<<<<<삽입정렬수행>>>>>>>>\n");
    insertionSort(list,size);   //삽입 정렬 함수 호출
    getchar(); return 0;
}
```
---