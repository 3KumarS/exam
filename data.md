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

--------
4. Implementation of Singly Linked List
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node* next;
};

Node* head = NULL;

void insert(int x) {
    Node* temp = new Node();
    temp->data = x;
    temp->next = head;
    head = temp;
}

void display() {
    Node* temp = head;
    while(temp != NULL) {
        cout << temp->data << " -> ";
        temp = temp->next;
    }
    cout << "NULL";
}

int main() {
    insert(10);
    insert(20);
    insert(30);
    display();
    return 0;
}

o/p
>>
30 -> 20 -> 10 -> NULL

=== Code Execution Successful ===

----------------
5. Stack Implementation using Array
>>
#include <iostream>
using namespace std;

#define SIZE 5
int stack[SIZE];
int top = -1;

void push(int x) {
    if(top == SIZE - 1)
        cout << "Stack Overflow\n";
    else {
        top++;
        stack[top] = x;
    }
}

void pop() {
    if(top == -1)
        cout << "Stack Underflow\n";
    else {
        cout << "Popped: " << stack[top] << endl;
        top--;
    }
}

int main() {
    push(10);
    push(20);
    push(30);
    pop();
    pop();
    return 0;
}

o/p
>>
Popped: 30
Popped: 20


=== Code Execution Successful ===

-------------------------------
6(a). Postfix Evaluation using Stack
#include <iostream>
#include <stack>
using namespace std;

int main() {
    stack<int> s;
    string exp = "23*54*+";

    for(char ch : exp) {
        if(isdigit(ch))
            s.push(ch - '0');
        else {
            int b = s.top(); s.pop();
            int a = s.top(); s.pop();

            switch(ch) {
                case '+': s.push(a + b); break;
                case '-': s.push(a - b); break;
                case '*': s.push(a * b); break;
                case '/': s.push(a / b); break;
            }
        }
    }
    cout << "Result: " << s.top();
    return 0;
}

o/p
>>
Result: 26

=== Code Execution Successful ===

-----------------------
7. Linear Queue using Array
>>
#include <iostream>
using namespace std;

#define SIZE 5
int queue[SIZE];
int front = -1, rear = -1;

void enqueue(int x) {
    if(rear == SIZE - 1)
        cout << "Queue Overflow\n";
    else {
        if(front == -1) front = 0;
        queue[++rear] = x;
    }
}

void dequeue() {
    if(front == -1 || front > rear)
        cout << "Queue Underflow\n";
    else
        cout << "Deleted: " << queue[front++] << endl;
}

int main() {
    enqueue(10);
    enqueue(20);
    enqueue(30);
    dequeue();
    dequeue();
    return 0;
}

o/p
>>
Deleted: 10
Deleted: 20


=== Code Execution Successful ===

---------------------
8. Binary Search Tree + Traversals
>>
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node* left;
    Node* right;
};

Node* insert(Node* root, int x) {
    if(root == NULL) {
        root = new Node();
        root->data = x;
        root->left = root->right = NULL;
    }
    else if(x < root->data)
        root->left = insert(root->left, x);
    else
        root->right = insert(root->right, x);

    return root;
}

// Inorder Traversal
void inorder(Node* root) {
    if(root != NULL) {
        inorder(root->left);
        cout << root->data << " ";
        inorder(root->right);
    }
}

int main() {
    Node* root = NULL;
    root = insert(root, 50);
    insert(root, 30);
    insert(root, 70);
    insert(root, 20);
    insert(root, 40);

    cout << "Inorder Traversal: ";
    inorder(root);
    return 0;
}

o/p
>>

Inorder Traversal: 20 30 40 50 70 

=== Code Execution Successful ===

----------------------------
9(a). DFS – Depth First Search
>>
#include <iostream>
using namespace std;

int graph[5][5] = {
    {0,1,1,0,0},
    {1,0,0,1,0},
    {1,0,0,1,1},
    {0,1,1,0,1},
    {0,0,1,1,0}
};

bool visited[5];

void DFS(int v) {
    cout << v << " ";
    visited[v] = true;

    for(int i=0; i<5; i++) {
        if(graph[v][i] && !visited[i])
            DFS(i);
    }
}

int main() {
    DFS(0);
    return 0;
}

o/p
>>
0 1 3 2 4 

=== Code Execution Successful ===


-----------

9(b). BFS – Breadth First Search
>>
#include <iostream>
#include <queue>
using namespace std;

int graph[5][5] = {
    {0,1,1,0,0},
    {1,0,0,1,0},
    {1,0,0,1,1},
    {0,1,1,0,1},
    {0,0,1,1,0}
};

int main() {
    bool visited[5] = {false};
    queue<int> q;

    q.push(0);
    visited[0] = true;

    while(!q.empty()) {
        int v = q.front(); q.pop();
        cout << v << " ";

        for(int i=0;i<5;i++) {
            if(graph[v][i] && !visited[i]) {
                visited[i] = true;
                q.push(i);
            }
        }
    }
    return 0;
}

o/p
>>
0 1 2 3 4 

=== Code Execution Successful ===


-----------------------------------


10. Minimum Spanning Tree – Kruskal’s Algorithm
>>
#include <iostream>
using namespace std;

struct Edge {
    int u, v, w;
};

int parent[10];

int find(int i) {
    while(parent[i] != i)
        i = parent[i];
    return i;
}

void unite(int x, int y) {
    parent[x] = y;
}

int main() {
    Edge edges[5] = {
        {0,1,10},
        {0,2,6},
        {0,3,5},
        {1,3,15},
        {2,3,4}
    };

    for(int i=0;i<4;i++)
        parent[i] = i;

    cout << "Edges in MST:\n";
    for(int i=0;i<5;i++) {
        int x = find(edges[i].u);
        int y = find(edges[i].v);

        if(x != y) {
            cout << edges[i].u << " - " << edges[i].v << " : " << edges[i].w << endl;
            unite(x, y);
        }
    }
    return 0;
}

o/p
>>
Edges in MST:
0 - 1 : 10
0 - 2 : 6
0 - 3 : 5


=== Code Execution Successful ===