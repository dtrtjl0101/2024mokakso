# 2024mokakso
## 검색
### 검색의 이해
* 무언가를 찾는것.
* 저장한 자료는 그 자료를 구별하여 인식할 수 있는 키를 가짐 -> 탐색키
### 순차 검색
* 일렬로 나열된 자료를 처음부터 마지막까지 순서대로 검색하는 방법
* 검색해야 하는 자료의 양에 따라 효율다름
---
#### 정렬되어 있지 않은 자료를 순차 검색
* 첫 원소부터 마지막 원소까지 순서대로 키값이 일치하는 원소가 있는지 비교하여 찾기.
* 마지막 원소까지 비교해도 키값이 일치하는 원소가 없으면 검색실패
* 시간복잡도는 O(n)

#### sequentialSearch.c
```c
#include<stdio.h>
typedef int element;
void sequentialSearch1(element a[],int n,element key){
    int i=0;
    printf("\n%3d를 검색해라! ->>",key);
    while(i<n && a[i] !=key)i++;
    if(i<n) printf("%3d번째에 검색 성공! \n",i+1);
    else printf("%3d번째에 검색 실패! \n",i+1); 
}
```
#### ex.c
```c
#include<stdio.h>
typedef int element;
void sequentialSearch1(element a[],int n, int key);
int main(void){
    int i;
    element a[]={8,30,1,9,11,19,2};
    int size=sizeof(a)/sizeof(a[0]); //배열 원소의 개수
    printf("\n\t<<검색 대상자료 >>\n");
    for(i=0;i<size;i++)printf("%5d",a[i]);puts("");
    sequentialSearch1(a,size,9);    //배열 a의 n개 원소 중에서 탐색키가 9인 원소 검색
    sequentialSearch1(a,size,6);    //배열 a의 n개 원소 중에서 탐색키가 6인 원소 검색
    getchar(); return 0;
}
```
---
### 정렬된 자료를 순차 검색
* 첫 번째 원소부터 비교하다가 비교하는 우너소의 키값이 찾는 키값보다 크면 찾는 원소가 없는 것이므로 더 이상 검색을 수행하지 않아도 검색 실패 알 수 있다.
* 시간복잡도는 O(n)이다
#### sequentialSearch.c
```c
#include<stdio.h>
typedef int element;
void sequentialSearch1(element a[],int n,element key){
    int i=0;
    printf("\n%3d를 검색해라! ->>",key);
    while(i<n && a[i] !=key)i++;
    if(i<n) printf("%3d번째에 검색 성공! \n",i+1);
    else printf("%3d번째에 검색 실패! \n",i+1); 
}
void sequentialSearch2(element a[],int n,element key){
    int i=0;
    printf("\n%3d를 검색해라! ->>",key);
    while(i<n && a[i] < key)i++;
    if(a[i]==key) printf("%3d번째에 검색 성공! \n",i+1);
    else printf("%3d번째에 검색 실패! \n",i+1); 
}
```
#### ex.c
```c
#include<stdio.h>
typedef int element;
void sequentialSearch2(element a[],int n, int key);
int main(void){
    int i;
    element a[]={1,2,8,9,11,19,29};
    int size=sizeof(a)/sizeof(a[0]); //배열 원소의 개수
    printf("\n\t<<검색 대상자료 >>\n");
    for(i=0;i<size;i++)printf("%5d",a[i]);puts("");
    sequentialSearch2(a,size,9);    //배열 a의 n개 원소 중에서 탐색키가 9인 원소 검색
    sequentialSearch2(a,size,6);    //배열 a의 n개 원소 중에서 탐색키가 6인 원소 검색
    getchar(); return 0;
}
```
---
### 이진검색
* 자료 가운데 있는 항목을 키값과 비교하여 키값이 더 크면 오른쪽 부분을 검색하고, 키값이 더 작으면 왼쪽 부분을 검색하는 방법.
* 시간 복잡도는 O(logn)
#### binarySearch.c
```c
#include<stdio.h>
typedef int element;
int cnt=0;  //이진 검색의 연산 횟수
void binarySearch(element a[],int begin, int end,element key){
    int middle;
    cnt++;  //이진 검색 연산 횟수 1증가
    if(begin==end){ //검색 범위가 한개인 경우
        if(key==a[begin])printf("%3d번째에 검색 성공!\n",cnt);
        else printf("%3d번째에 검색 실패! \n",cnt); 
        return;
    }
    middle=(begin+end)/2;   //검색 범위가 이진 분할되는 기준 위치 설정
    if(key==a[begin])printf("%3d번째에 검색 성공!\n",cnt);
    else if(key<a[middle]&&(middle-1>=begin))
        binarySearch(a,begin,middle-1,key);
    else if(key>a[middle]&&(middle+1<>=begin))
        binarySearch(a,middle+1,end,key);
    else printf("%3d번째에 검색 실패! \n",cnt); 
}
```
#### ex.c
```c
#include<stdio.h>
typedef int element;
int main(void){
    element a[]={1,2,8,9,11,19,29},key;
    int i,size=sizeof(a)/sizeof(a[0]); //배열 원소의 개수
    char more;
    extern int cnt;
    printf("\n\t<<검색 대상자료 >>\n");
    for(i=0;i<size;i++)printf("%5d",a[i]);puts("");
    do{
        cnt=0;
        printf("\n\n검색할 키를 입력하세요 : ");scanf("%d",&key);
        printf("\n%3d를 검색하라! ->>",key);
        binarySearch(a,0,size-1,key);
        printf("\n\n검색을 계속하려면 y를 누르세요>>");scanf("  %C",&more);
    }while(more =='y');
    getchar(); return 0;
}
```
---
### 해싱
* 산술적인 연산으로 키가 있는 위치를 계산하여 바로 찾아가는 계산 검색 방식.
* 키값을 원소 위치로 변환하는 함수 : 해시함수
* 해시 함수로 계산된 주소 위치에 항목을 저장한 표 : 해시테이블
#### 해싱 관련 용어
* 동거자 - 서로 다른 키값을 가지지만 해시 함수에 의해 같은 버킷에 저장된 키값.
* 충돌 - 키 값이 서로 다름에도 불구하고 해시 함수에 의해 주어진 버킷 주소가 같은 경우
* 키값밀도 - 실제사용중인 키값의 개수 / 사용 가능한 키값의 개수
* 적재밀도 - 실제 사용중인 키값의 개수 / 해시테이블에 저장 가능한 전체 키값의 개수
          = 실제 사용중인 키값의 개수 / (버킷개수 x 슬롯 개수)
### 해시 함수
* 해시 함수는 계산이 쉬워야한다.
    * 비교 검색 방법을 사용하여 키값의 비교 연산을 수행하는 시간보다 해시 함수를 사용하여 계산하는 시간이 빨라야 해싱검색을 사용하는 의미가 있다.
* 해시 함수는 충돌이 적어야 한다.
    * 충돌이 많이 발생한다는 것은 같은 버킷을 할당받는 키값이 많다는 뜻. 비어있는 버키싱 많다 하더라도 어떤 버킷은 오버플로우가 발생할 수 있는 상태가 되므로 좋은 해시함수가 불가.
* 해시 테이블에 고르게 분포할 수 있도록 주소를 만들어야 한다.