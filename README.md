# Categorizing(Sorting & Searching)
Project: Categorizing

Code:
```cpp
#include <iostream>
using namespace std;

const int MAX_SIZE = 100;

void inputArray(int arr[], int &n) {
    cout << "Enter number of elements (max " << MAX_SIZE << "): ";
    cin >> n;

    if (n > MAX_SIZE || n <= 0) {
        cout << "Invalid size." << endl;
        return;
    }

    cout << "Enter " << n << " elements: " << endl;
    for (int i = 0; i < n; i++)
        cin >> arr[i];
}

void displayArray(int arr[], int n) {
    cout << "Array: ";
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";
    cout << endl;
}

void selectionSort(int arr[], int n) {
    for (int i = 0; i < n - 1; i++) {
        int minIndex = i;
        for (int j = i + 1; j < n; j++)
            if (arr[j] < arr[minIndex])
                minIndex = j;

        // Swap
        int temp = arr[i];
        arr[i] = arr[minIndex];
        arr[minIndex] = temp;
    }
}

void merge(int arr[], int l, int m, int r) {
    int n1 = m - l + 1;
    int n2 = r - m;

    int left[100], right[100];

    for (int i = 0; i < n1; i++)
        left[i] = arr[l + i];
    for (int j = 0; j < n2; j++)
        right[j] = arr[m + 1 + j];

    int i = 0, j = 0, k = l;

    while (i < n1 && j < n2)
        arr[k++] = (left[i] <= right[j]) ? left[i++] : right[j++];

    while (i < n1)
        arr[k++] = left[i++];
    while (j < n2)
        arr[k++] = right[j++];
}

void mergeSort(int arr[], int l, int r) {
    if (l < r) {
        int m = (l + r) / 2;
        mergeSort(arr, l, m);
        mergeSort(arr, m + 1, r);
        merge(arr, l, m, r);
    }
}

int linearSearch(int arr[], int n, int key) {
    for (int i = 0; i < n; i++)
        if (arr[i] == key)
            return i;
    return -1;
}

int binarySearch(int arr[], int n, int key) {
    int left = 0, right = n - 1;

    while (left <= right) {
        int mid = (left + right) / 2;
        if (arr[mid] == key)
            return mid;
        else if (key < arr[mid])
            right = mid - 1;
        else
            left = mid + 1;
    }
    return -1;
}

int main() {
    int arr[MAX_SIZE], n = 0, choice, key;

    do {
        cout << "Sorting and Searching Algorithms " << endl;
        cout << "1. Input Array" << endl;
        cout << "2. Display Array" << endl;
        cout << "3. Selection Sort" << endl;
        cout << "4. Merge Sort" << endl;
        cout << "5. Linear Search" << endl;
        cout << "6. Binary Search" << endl;
        cout << "0. Exit" << endl;
        cout << "Enter your choice: " << endl;
        cin >> choice;

        switch (choice) {
        case 1:
            inputArray(arr, n);
            break;
        case 2:
            displayArray(arr, n);
            break;
        case 3:
            selectionSort(arr, n);
            cout << "Array sorted using Selection Sort." << endl;
            displayArray(arr, n);
            break;
        case 4:
            mergeSort(arr, 0, n - 1);
            cout << "Array sorted using Merge Sort." << endl;
            displayArray(arr, n);
            break;
        case 5:
            cout << "Enter element to search: " << endl;
            cin >> key;
            {
                int index = linearSearch(arr, n, key);
                displayArray(arr, n);
                if (index != -1)
                    cout << "Element found at index " << index << ". " << endl;
                else
                    cout << "Element not found." << endl;
            }
            break;
        case 6:
            cout << "Enter element to search: " << endl;
            cin >> key;
            {
                displayArray(arr, n);
                int index = binarySearch(arr, n, key);
                if (index != -1)
                    cout << "Element found at index " << index << ". " << endl;
                else
                    cout << "Element not found." << endl;
            }
            break;
        case 0:
            cout << "Exiting program." << endl;
            break;
        default:
            cout << "Invalid choice." << endl;
        }

    } while (choice != 0);

    return 0;
}
```
Output:
![categorizing]()
![categorizing]()
![categorizing]()
Out
