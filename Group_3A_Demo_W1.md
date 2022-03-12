#include <iostream>

void Showmenu(){
    printf("1. Nhap mang\n");
    printf("2. Xuat mang\n");
    printf("3. Linear Search\n");
    printf("4. Binary Search\n");
    printf("5. InterchangeSort\n");
    printf("6. BubbleSort\n");
    printf("7. SelectionSort\n");
    printf("8. InserttionSort\n");
    printf("9. QuịckSort\n");
    printf("10. Thoat\n");

}

void input_array(float arr[], int length){
    for (int i = 0; i < length; i++) {
        scanf("%f", &arr[i]);
    }
}

void show_array(float arr[], int length){
    for (int i = 0; i < length; i++) {
        printf("%f ", arr[i]);
    }
    printf("\n");
}

void hoan_vi(float arr[], int i_a, int i_b){
    float temp = 0;
    temp = arr[i_a];
    arr[i_a] = arr[i_b];
    arr[i_b] = temp;
}

void Linearsearch(float arr[], int n, float keyW){
    bool NotFind = true;
    for (int i = 0; i < n; ++i) {
        if(arr[i] == keyW){
            printf("Phann tu %f ở vi tri  %d \n", arr[i], i);
            NotFind = false;
        }
    }
    if (NotFind){
        printf("Khong tim thay !!\n");
    }
}

// kieudulieu tenham (tham so){   }
// void ten(cac tham so);

int Binarysearch(float arr[], int n, float keyW){
    int l, r, mid;
    l = 0; r = n-1;
    do{
        mid = (l+r)/2;
        if (arr[mid] == keyW) return mid;
        else{
            if (arr[mid] > keyW){
                r = mid - 1;
            } else{
                l = mid + 1;
            }
        }
    } while (l <= r);
    return -1;
}

void InterchangeSort(float arr[], int n){
    for (int i = 0; i < n-1; ++i) {
        for (int j = i+1; j < n; ++j) {
            if (arr[j] < arr[i]){
                hoan_vi(arr, i, j);
            }
        }
    }
}

void bubbleSort(float arr[], int n)
{
    int i, j;
    bool haveSwap = false;
    for (i = 0; i < n-1; i++){
        haveSwap = false;
        // j : 0 -
        for (j = 0; j < n-i-1; j++){
            if (arr[j] > arr[j+1]){
                hoan_vi(arr, j, j+1);
                haveSwap = true; // Kiểm tra lần lặp này có swap không
            }
        }
        if(haveSwap == false){
            break;
        }
    }
}

void selectionSort(float arr[], int n)
{
    int i, j, min_idx;
    // Di chuyển ranh giới của mảng đã sắp xếp và chưa sắp xếp
    for (i = 0; i < n-1; i++)
    {
        // Tìm phần tử nhỏ nhất trong mảng chưa sắp xếp
        min_idx = i;
        for (j = i+1; j < n; j++){
            if (arr[j] < arr[min_idx]) hoan_vi(arr, min_idx, j);
        }
    }
}

void InserttionSort(float arr[], int n){
    int pos;
    float x; // luu gia tri a[i] tránh bị ghi đè khi dời chỗ các phần tử
    for (int i = 0; i < n; ++i) {
        x = arr[i];
        pos = i-1;
        while((pos >= 0)&&(arr[pos] > x)){
            arr[pos+1] = arr[pos];
            pos--;
        }
        arr[pos+1] = x;
    }
}

void Quicksort(float arr[], int l, int r){
    int i, j;
    float x;
    int mid = (l+r)/2;
    x = arr[mid];
    i = l, j = r;
    do {
        while(arr[i] < x) i++;
        while (arr[j] > x) j--;
        if(i <= j){
            hoan_vi(arr, i, j);
            i++; j--;
        }
    } while (i < j);
    if(l < j) Quicksort(arr, l, j);
    if(i < r) Quicksort(arr, i, r);
}


int main() {
    int chose = 0;
    float arr[100];
    int n = 0;
    do{
        Showmenu();
        printf("Chon chuc nang: ");
        scanf("%d", &chose);
        printf("\n");
        switch (chose) {
            case 1:{
                printf("Nhap so phan tu cua manng: ");
                scanf("%d", &n);
                printf("\n");
                printf("Nhap cac phan tu cua mang: \n");
                input_array(arr, n);
                break;}
            case 2:{
                if(n == 0) {
                    printf("!Vui long nhap mang!\n");
                    break;
                }
                printf("Cac phan tu trong mang: ");
                show_array(arr, n);
                break;}
            case 3:{
                if(n == 0) {
                    printf("!Vui long nhap mang!\n");
                    break;
                }
                float keyW = 0.0;
                printf("Nhap tu khoa can tim: ");
                scanf("%f", &keyW);
                printf("\n");
                Linearsearch(arr, n, keyW);
                break;}
            case 4:{
                if(n == 0) {
                    printf("!Vui long nhap mang!\n");
                    break;
                }
                float keyW = 0.0;
                printf("Nhap tu khoa can tim: ");
                scanf("%f",&keyW);
                printf("\n");
                int pos = Binarysearch(arr, n, keyW);
                if (pos > 0){
                    printf("Phan tu %f o vi tri %d \n", keyW, pos);
                }
                break;}
            case 5:{
                InterchangeSort(arr, n);
                printf("Da sap xep xong \n");
                break;}
            case 6:{
                bubbleSort(arr, n);
                printf("Da sap xep xong \n");
                break;}
            case 7:{
                selectionSort(arr, n);
                printf("Da sap xep xong \n");
                break;}
            case 8:{
                InserttionSort(arr, n);
                printf("Da sap xep xong \n");
                break;}
            case 9:{
                Quicksort(arr, 0, n-1);
                printf("Da sap xep xong \n");
                break;}
            default:
                printf("Xin chao tam biet\n");
        }
    } while (chose != 10);
    return 0;
}
