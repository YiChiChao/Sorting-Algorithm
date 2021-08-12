# $Sorting$ $Note$ 
## 時間複雜度($O(f(n)$)
Def: 當輸入n筆資料時，此function所需要花費的時間。通常指最差情況複雜度(就是在最衰的情況，同一種輸入所需要花最長的時間)

| 執行時間 | 白話文 |例子|
|:------ |:------- |:---------|
| $$O(1)$$   | 不管輸入多少東西，都不影響求出答案的時間範圍。其中$1$可被替換成任意常數。 |printf("%d",book[237])
| $$O(n)$$  | 假設要從$n$個人當中找出拿著筆的人，從第一個人問到第$n$個人，時間複雜度會隨$n$的數目增大而線性增加。 |簡易搜尋|
| $$O(n^2)$$  | 呈上例，在問第一個人時同時叫他也去依序問其他$n-1$個人，這樣執行$n$次。此時時間複雜度會依照$n$增加，以$n^2$圖形增加|**[泡沫排序法](https://hackmd.io/@VSCwqJYJSXeRPkfDpYnbnQ/Sy79MIyju#%E6%B0%A3%E6%B3%A1%E6%8E%92%E5%BA%8F%E6%B3%95Bubble-Sort)**|
| $$O(\log n)$$  |以二分搜尋法為例，在執行當中一次過濾掉資料的一半 ，所以當資料數目增加，時間複雜度會以$\log_2n$圖形增加|二分搜尋法

>寫完發現真的不能不放圖

![time complexity](https://ithelp.ithome.com.tw/upload/images/20181020/20112011LzUSOSLEC0.png)

## $Quick$ $Sort$
Quick Sort 是一種分治法，
>分治法(分而治之)是一種把一個大問題拆成二或多個相同或類似的小問題，直到小問題可以直接求解的方法。

首先Quick Sort當中會需要一個pivot(基準數)，依照這個基準將整個數列分成兩區，一區裡的數均小於pivot，另一區則需均大於pivot。

如下圖，我們選定序列的第一個數作為pivot，i控制序列前端的數並和pivot做比較(必須要小於pivot)，j控制序列後端的數並和pivot做比較(必須要大於pivot)，當i遇到比pivot大的數且j遇到比pivot小的數，則兩數對調。

直到j > i, j 和 pivot 交換位置，則完成一次。

之後以pivot為基準分成兩邊繼續做partition()，直到兩邊都排序好即完成。

![qsort](https://lh3.googleusercontent.com/pw/ACtC-3ffMGXxda36cmTyM8zDCbAvFPaEFdN9YWtdzeVPdhyPebpavRSESWBd6womQ3dDs4B3xumPOwVph7iOq-LqxgWt5063aVKVbtahOPQfV4dU1_-LmzHy2ZSeSfrnBeNYTMyGeixnrEB1N-gInTThj8WJ=w480-h288-no?authuser=0)

```c=
#include<stdio.h>
#include<stdlib.h>
void swap(int* arr, int i, int j);
int partition(int* arr, int i, int j);

void swap(int* arr, int i, int j){
    int tmp = arr[i];
    arr[i] = arr[j];
    arr[j] = tmp;
}
int partition(int* arr, int i, int j){
    /*set the first index of the arr as the pivot*/
    int pivot_index = i;
    int pivot = arr[i];
    
    while(i <= j){
        while(arr[i] <= pivot && i <= j) ++i;
        while(arr[j] >= pivot && i <= j) --j;
        if(i < j) swap(arr, i, j);
    }
    swap(arr, pivot_index, j);
    return j;
}

void quicksort(int* arr, int i, int j){
    int pi;
    if(i >= j) return;
    if(i < j){
        pi = partition(arr, i, j);
    }
    quicksort(arr, i, pi-1);
    quicksort(arr, pi+1, j);
}

int main(){
    int arr[] = {16, 20, 1, 26, 14, 7, 9, 4, 8, 18, 11, 17};
    quicksort(arr, 0, 11);
    printf("arr ={");
    for(int i = 0; i < 12; ++i){
        printf(" %d%c", arr[i], ','*(i != 11)+'}'*(i == 11));
    }
    printf("\n");
}

```
