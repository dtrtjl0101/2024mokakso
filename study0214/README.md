# 2024mokakso
## 개념이용한 백준풀이
### 10828번 (스택)
![](./image/10828.png)
```c
#include<stdio.h>
#include<string.h>
#include<stdlib.h>
int main() {
	int SIZE;
	scanf("%d", &SIZE);
	int* a = (int*)malloc(SIZE * sizeof(int));
	int p = -1;
	for (int i = 0; i < SIZE; i++) {
		char word[50];
		int k;
		scanf("%s", word);
		if (strcmp(word, "push") == 0) {
			if (p < SIZE - 1) {
				scanf("%d", &k);
				a[++p] = k;
			}
		}
		else if (strcmp(word, "top") == 0) {
			if (p == -1)
				printf("-1\n");
			else
				printf("%d\n", a[p]);
		}
		else if (strcmp(word, "size") == 0) {
			printf("%d\n", p + 1);
		}
		else if (strcmp(word, "empty") == 0) {
			if (p == -1)
				printf("1\n");
			else printf("0\n");
		}
		else if (strcmp(word, "pop") == 0) {
			if (p == -1)
				printf("-1\n");
			else {
				printf("%d\n", a[p]);
				p--;
			}
		}
	}
	free(a);
	return 0;
}
```
---
### 10845번 (큐)
![](./image/10845.png)
```c
#define _CRT_SECURE_NO_WARNINGS
#include<stdio.h>
#include<string.h>
#include<stdlib.h>
int main() {
	int num;
	scanf("%d", &num);
	int* a = (int*)malloc(num * sizeof(int));
	int p = -1;
	int q = 0;
	for (int i = 0; i < num; i++) {
		char word[50];
		int k;
		scanf("%s", word);
		if (strcmp(word, "push") == 0) {
			if (p < num - 1) {
				scanf("%d", &k);
				a[++p] = k;
			}
		}
		else if (strcmp(word, "pop") == 0) {
			if ((p == -1)||(q==-1)||q>p)
				printf("-1\n");
			else {
				printf("%d\n", a[q]);
				q++;
			}
		}
		else if (strcmp(word, "size") == 0) {
			printf("%d\n", p - q + 1);
		}
		else if (strcmp(word, "empty") == 0) {
			if ((p == -1)||(q==-1)|| q > p)
				printf("1\n");
			else printf("0\n");
		}
		else if (strcmp(word, "front") == 0) {
			if ((p == -1) || (q == -1)|| q > p)
				printf("-1\n");
			else
				printf("%d\n", a[q]);
		}
		else if (strcmp(word, "back") == 0) {
			if ((p == -1) || (q == -1)|| q > p)
				printf("-1\n");
			else
				printf("%d\n", a[p]);
		}
	}
	free(a);
	return 0;
}
```
---
### 11650번 (정렬)
![](./image/11650.png)
```c
#include <stdio.h>
#include <stdlib.h>
typedef struct{
	int x;
	int y;
} array;
int compare(const void *p1, const void *p2){
	array A = *(array *)p1;
	array B = *(array *)p2;
	if (A.x > B.x) return 1;
	else if (A.x < B.x) return -1;
	else {
		if (A.y > B.y) return 1;
		else if (A.y < B.y) return -1;
	}
}
array a[100000];
int main(void){
	int n;
	scanf("%d", &n);
	for (int i = 0; i < n; i++){
		scanf("%d %d", &a[i].x, &a[i].y);
	}
	qsort(a, n, sizeof(array), compare);
	for (int i = 0; i < n; i++){
		printf("%d %d\n", a[i].x, a[i].y);
	}
	return 0;
}
```