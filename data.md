1. Implementation of Sorting Techniques

i. Bubble Sort
ii. Insertion Sort

----------------
i. Bubble Sort
>>
#include <iostream>
using namespace std;

int main()
{
    int n;
    int a[50];

    cout << "Enter number of elements: ";
    cin >> n;

    cout << "Enter elements:\n";
    for(int i = 0; i < n; i++)
    {
        cin >> a[i];
    }

    // Bubble Sort
    for(int i = 0; i < n-1; i++)
    {
        for(int j = 0; j < n-1-i; j++)
        {
            if(a[j] > a[j+1])
            {
                int temp = a[j];
                a[j] = a[j+1];
                a[j+1] = temp;
            }
        }
    }

    cout << "Sorted array:\n";
    for(int i = 0; i < n; i++)
    {
        cout << a[i] << " ";
    }

    return 0;
}

-------------------
ii. Insertion Sort
>>
#include <iostream>
using namespace std;

int main() {
    int n;
    cout << "Enter number of elements: ";
    cin >> n;

    if(n > 50) {
        cout << "Maximum allowed size is 50";
        return 0;
    }

    int a[50];
    cout << "Enter elements:\n";
    for(int i = 0; i < n; i++)
        cin >> a[i];

    // Insertion Sort Logic
    for(int i = 1; i < n; i++) {
        int key = a[i];
        int j = i - 1;

        while(j >= 0 && a[j] > key) {
            a[j + 1] = a[j];
            j--;
        }

        a[j + 1] = key;
    }

    cout << "Sorted array:\n";
    for(int i = 0; i < n; i++)
        cout << a[i] << " ";

    return 0;
}

----------------------
2. Implementation of Searching Techniques

i. Linear Search
ii. Binary Search
-----------------
i. Linear Search
>>
#include <iostream>
using namespace std;

int main() {
    int n, key;
    int a[50];

    cout << "Enter number of elements: ";
    cin >> n;

    cout << "Enter elements:\n";
    for(int i = 0; i < n; i++)
        cin >> a[i];

    cout << "Enter element to search: ";
    cin >> key;

    int flag = 0;

    for(int i = 0; i < n; i++) {
        if(a[i] == key) {
            cout << "Element found at position " << i + 1;
            flag = 1;
            break;
        }
    }

    if(flag == 0)
        cout << "Element not found";

    return 0;
}



o/p→

Enter number of elements: 2
Enter elements:
1
2
Enter element to search: 2
Element found at position 2

=== Code Execution Successful ===

---------------------
 Binary Search
 >>
#include <iostream>
using namespace std;

int main() {
    int n, key;
    int a[50];

    cout << "Enter number of elements: ";
    cin >> n;

    cout << "Enter sorted elements:\n";
    for(int i = 0; i < n; i++)
        cin >> a[i];

    cout << "Enter element to search: ";
    cin >> key;

    int low = 0, high = n - 1, mid;
    int flag = 0;

    while(low <= high) {
        mid = (low + high) / 2;

        if(a[mid] == key) {
            cout << "Element found at position " << mid + 1;
            flag = 1;
            break;
        }
        else if(key < a[mid]) {
            high = mid - 1;
        }
        else {
            low = mid + 1;
        }
    }

    if(flag == 0)
        cout << "Element not found";

    return 0;
}

---------------
3. Implement program for Modulo Division as hashing method.

>>
#include <iostream>
using namespace std;

#define SIZE 10     // Size of Hash Table

int table[SIZE];    // Hash Table

// Hash Function (Modulo Division)
int hashFunction(int key)
{
    return key % SIZE;
}

int main()
{
    int key, index;

    // Initialize hash table with -1 (empty)
    for (int i = 0; i < SIZE; i++)
        table[i] = -1;

    cout << "Enter key to insert: ";
    cin >> key;

    index = hashFunction(key);

    // Check for collision
    if (table[index] == -1)
    {
        table[index] = key;
        cout << "Key stored at index: " << index << endl;
    }
    else
    {
        cout << "Collision occurred at index: " << index << endl;
    }

    // Display Hash Table
    cout << "\nHash Table:\n";
    for (int i = 0; i < SIZE; i++)
    {
        cout << i << " -> " << table[i] << endl;
    }

    return 0;
}

o/p

Enter key to insert: 1
Key stored at index: 1

Hash Table:
0 -> -1
1 -> 1
2 -> -1
3 -> -1
4 -> -1
5 -> -1
6 -> -1
7 -> -1
8 -> -1
9 -> -1


=== Code Execution Successful ===
