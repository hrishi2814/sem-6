# Greedy Search Algorithm for Selection Sort

## Intuition and Mental Model

**Greedy Approach in Selection Sort:**
Imagine you're organizing a hand of playing cards:
1. Scan all cards to find the smallest one
2. Swap it with the first card
3. Repeat the process for the remaining unsorted portion

**Key Characteristics:**
- Makes the locally optimal choice at each step
- Never reconsider choices once made
- Simple and intuitive approach
- O(n²) time complexity (inefficient for large datasets)

## Implementation in C++ and Java

### C++ Implementation
```cpp
#include <iostream>
#include <vector>
using namespace std;

void selectionSort(vector<int>& arr) {
    int n = arr.size();
    
    for (int i = 0; i < n-1; i++) {
        // Find the minimum element in unsorted array
        int min_idx = i;
        for (int j = i+1; j < n; j++) {
            if (arr[j] < arr[min_idx]) {
                min_idx = j;
            }
        }
        
        // Swap the found minimum element with the first element
        swap(arr[min_idx], arr[i]);
    }
}

int main() {
    vector<int> arr = {64, 25, 12, 22, 11};
    
    cout << "Original array: ";
    for (int num : arr) cout << num << " ";
    cout << endl;
    
    selectionSort(arr);
    
    cout << "Sorted array: ";
    for (int num : arr) cout << num << " ";
    cout << endl;
    
    return 0;
}
```

### Java Implementation
```java
public class SelectionSort {
    public static void selectionSort(int[] arr) {
        int n = arr.length;
        
        for (int i = 0; i < n-1; i++) {
            // Find the minimum element in unsorted array
            int min_idx = i;
            for (int j = i+1; j < n; j++) {
                if (arr[j] < arr[min_idx]) {
                    min_idx = j;
                }
            }
            
            // Swap the found minimum element with the first element
            int temp = arr[min_idx];
            arr[min_idx] = arr[i];
            arr[i] = temp;
        }
    }
    
    public static void main(String[] args) {
        int[] arr = {64, 25, 12, 22, 11};
        
        System.out.print("Original array: ");
        for (int num : arr) System.out.print(num + " ");
        System.out.println();
        
        selectionSort(arr);
        
        System.out.print("Sorted array: ");
        for (int num : arr) System.out.print(num + " ");
        System.out.println();
    }
}
```

## Step-by-Step Execution Example

Let's trace the algorithm with input: [64, 25, 12, 22, 11]

**Pass 1:**
- Find min in entire array: 11 at index 4
- Swap with first element (index 0)
- Array becomes: [11, 25, 12, 22, 64]

**Pass 2:**
- Find min in [25, 12, 22, 64]: 12 at index 2
- Swap with second element (index 1)
- Array becomes: [11, 12, 25, 22, 64]

**Pass 3:**
- Find min in [25, 22, 64]: 22 at index 3
- Swap with third element (index 2)
- Array becomes: [11, 12, 22, 25, 64]

**Pass 4:**
- Find min in [25, 64]: 25 at index 3
- Swap with itself (no change)
- Final sorted array: [11, 12, 22, 25, 64]

## Why This is a Greedy Algorithm

1. **Greedy Choice Property**: At each step, we make the locally optimal choice by selecting the smallest remaining element.
2. **Optimal Substructure**: After placing an element in its correct position, we're left with a smaller subproblem of the same nature.
3. **Irrevocability**: Once we place an element, we never reconsider that decision.

## Time Complexity Analysis

- **Best Case**: O(n²) - Already sorted array still requires comparisons
- **Average Case**: O(n²)
- **Worst Case**: O(n²)

**Space Complexity**: O(1) - In-place sorting algorithm

## When to Use Selection Sort

- When memory is constrained (in-place sorting)
- When simplicity is more important than efficiency
- For small datasets where O(n²) is acceptable
- When you need minimal swaps (only O(n) swaps total)