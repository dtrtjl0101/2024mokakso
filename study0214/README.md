# 2024mokakso
## 개념이용한 백준풀이
### 10828번 (스택)
![](study0214/10828.PNG)
```c
#include<stdio.h>
#include<string.h>
#include<stdlib.h>
int main() {
    int SIZE;
    // 배열의 크기 입력 받음
    scanf("%d", &SIZE);
    // 동적으로 메모리 할당하여 정수 배열 생성
    int* a = (int*)malloc(SIZE * sizeof(int));
    int p = -1; // 스택의 top을 나타내는 변수
    // 사용자로부터 입력된 명령어를 처리
    for (int i = 0; i < SIZE; i++) {
        char word[50]; // 명령어를 저장할 문자열 배열
        int k;
        // 명령어 입력 받기
        scanf("%s", word);
        // 명령어에 따라 동작 결정
        if (strcmp(word, "push") == 0) {
            // push 명령어 처리
            if (p < SIZE - 1) {
                scanf("%d", &k);
                a[++p] = k; // 스택에 정수 k를 push
            }
        }
        else if (strcmp(word, "top") == 0) {
            // top 명령어 처리
            if (p == -1)
                printf("-1\n"); // 스택이 비어있는 경우
            else
                printf("%d\n", a[p]); // 스택의 top 요소 출력
        }
        else if (strcmp(word, "size") == 0) {
            // size 명령어 처리
            printf("%d\n", p + 1); // 스택의 크기 출력
        }
        else if (strcmp(word, "empty") == 0) {
            // empty 명령어 처리
            if (p == -1)
                printf("1\n"); // 스택이 비어있으면 1 출력
            else
                printf("0\n"); // 그렇지 않으면 0 출력
        }
        else if (strcmp(word, "pop") == 0) {
            // pop 명령어 처리
            if (p == -1)
                printf("-1\n"); // 스택이 비어있는 경우
            else {
                printf("%d\n", a[p]); // 스택의 top 요소 출력
                p--; // top을 한 칸 앞으로 이동
            }
        }
    }
    // 동적으로 할당된 메모리 해제
    free(a);
    return 0;
}
```
#### 코드설명
* push: 스택에 정수를 추가한다.
* pop: 스택의 top에 있는 요소를 제거하고 그 값을 출력한다.
* top: 스택의 top에 있는 요소를 출력한다.
* size: 스택의 크기를 출력한다.
* empty: 스택이 비어있는지 여부를 출력한다.
* 동적 메모리 할당을 사용하여 사용자가 입력한 크기에 따라 스택을 생성한다. 
* 사용자로부터 입력을 받아 명령어를 처리하고, 처리된 결과를 출력한다.
---
### 10845번 (큐)
![](./study0214/10845.png)
```c
// 표준 입력 함수와 관련된 경고를 무시하기 위한 선언
#define _CRT_SECURE_NO_WARNINGS
#include<stdio.h>
#include<string.h>
#include<stdlib.h>
int main() {
    int num;
    // 정수 하나를 입력 받음
    scanf("%d", &num);
    // 동적으로 메모리 할당하여 정수 배열 생성
    int* a = (int*)malloc(num * sizeof(int));
    int p = -1; // 스택의 top을 나타내는 변수
    int q = 0;  // 스택의 front를 나타내는 변수
    // 입력된 명령 수행
    for (int i = 0; i < num; i++) {
        char word[50]; // 명령어를 저장할 문자열 배열
        // 명령어 입력
        scanf("%s", word);
        // 명령어 처리
        if (strcmp(word, "push") == 0) {
            // push 명령어 처리
            if (p < num - 1) {
                int k;
                scanf("%d", &k);
                a[++p] = k; // 스택에 정수 k를 push
            }
        }
        else if (strcmp(word, "pop") == 0) {
            // pop 명령어 처리
            if ((p == -1) || (q == -1) || q > p)
                printf("-1\n"); // 스택이 비어있는 경우
            else {
                printf("%d\n", a[q]); // 스택의 front 요소를 출력
                q++; // front를 한 칸 옮김
            }
        }
        else if (strcmp(word, "size") == 0) {
            // size 명령어 처리
            printf("%d\n", p - q + 1); // 스택의 크기 출력
        }
        else if (strcmp(word, "empty") == 0) {
            // empty 명령어 처리
            if ((p == -1) || (q == -1) || q > p)
                printf("1\n"); // 스택이 비어있으면 1 출력
            else
                printf("0\n"); // 그렇지 않으면 0 출력
        }
        else if (strcmp(word, "front") == 0) {
            // front 명령어 처리
            if ((p == -1) || (q == -1) || q > p)
                printf("-1\n"); // 스택이 비어있는 경우
            else
                printf("%d\n", a[q]); // 스택의 front 요소 출력
        }
        else if (strcmp(word, "back") == 0) {
            // back 명령어 처리
            if ((p == -1) || (q == -1) || q > p)
                printf("-1\n"); // 스택이 비어있는 경우
            else
                printf("%d\n", a[p]); // 스택의 top 요소 출력
        }
    }
    // 동적으로 할당된 메모리 해제
    free(a);
    return 0;
}
```
#### 코드설명
* push: 스택에 정수를 추가한다. 만약 스택이 가득 찬 경우(스택의 크기를 넘어선 경우) 추가하지 않는다.
* pop: 스택의 맨 위에 있는 요소를 제거하고 출력한다. 만약 스택이 비어있는 경우("-1"을 출력할 수 없는 경우), "-1"을 출력한다.
* size: 스택의 현재 크기를 출력한다.
* empty: 스택이 비어있는지 여부를 출력한다. 비어있으면 "1"을, 그렇지 않으면 "0"을 출력한다.
* front: 스택의 맨 앞에 있는 요소를 출력한다. 만약 스택이 비어있는 경우("-1"을 출력할 수 없는 경우), "-1"을 출력한다.
* back: 스택의 맨 끝에 있는 요소를 출력한다. 만약 스택이 비어있는 경우("-1"을 출력할 수 없는 경우), "-1"을 출력한다.
* 이 코드는 사용자로부터 입력을 받아 각 명령어에 따라 스택을 조작하고, 그 결과를 출력한다. 
* 스택은 배열로 구현되며, 메모리 동적 할당을 통해 스택의 크기를 유동적으로 조절할 수 있다. 
* 코드는 사용자가 입력한 명령어에 따라 적절한 처리를 수행하고, 스택의 상태를 출력한다.
---
### 11650번 (정렬)
![](./study0214/11650.png)
```c
#include <stdio.h>
#include <stdlib.h>
// 배열을 나타내는 구조체 정의
typedef struct {
    int x;
    int y;
} array;
// qsort 함수에서 사용할 비교 함수
int compare(const void *p1, const void *p2) {
    // void 포인터를 array 포인터로 형변환 후 역참조하여 구조체로 변환
    array A = *(array *)p1;
    array B = *(array *)p2;
    
    // x 좌표를 기준으로 정렬
    if (A.x > B.x) return 1;
    else if (A.x < B.x) return -1;
    else {
        // x 좌표가 같을 경우 y 좌표를 기준으로 정렬
        if (A.y > B.y) return 1;
        else if (A.y < B.y) return -1;
    }
    // A와 B가 같을 경우
    return 0;
}
// 메인 함수
int main(void) {
    int n;
    scanf("%d", &n); // 배열 크기 입력 받기
    array a[100000]; // 배열 선언
    // 배열 요소 입력 받기
    for (int i = 0; i < n; i++) {
        scanf("%d %d", &a[i].x, &a[i].y);
    }
    // qsort 함수를 사용하여 배열 정렬
    qsort(a, n, sizeof(array), compare);
    // 정렬된 배열 출력
    for (int i = 0; i < n; i++) {
        printf("%d %d\n", a[i].x, a[i].y);
    }
    return 0;
}
```
#### 코드설명
* 이 프로그램은 사용자로부터 배열의 크기를 입력 받은 후, 배열의 요소들을 입력 받는다. 각 요소는 (x, y) 좌표를 나타내는 두 정수로 구성된다.
* 다음으로, qsort() 함수를 사용하여 입력된 배열을 정렬한다. 이 때, 정렬 기준은 compare() 함수를 통해 지정된다. compare() 함수는 두 개의 요소를 비교하여 정렬 기준을 제공한다. 먼저 x 좌표를 기준으로 비교를 수행하고, x 좌표가 같은 경우 y 좌표를 기준으로 비교를 수행한다.
* 마지막으로, 정렬된 배열을 출력한다. 각 요소는 정렬된 순서대로 출력되며, 각 요소의 (x, y) 좌표가 공백으로 구분되어 출력된다.
