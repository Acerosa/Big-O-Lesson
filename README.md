# 📚 Understanding Big-O Notation – A Beginner-Friendly Guide

**Welcome to this GitHub repository dedicated to demystifying Big-O Notation**. This lesson is tailored for learners who want to grasp **algorithmic thinking**, performance, and scalability.

---

## 🔍 What is Big-O?

**Big-O Notation** describes **how the number of operations grows** as the size of input increases. It's not about *how fast* a program runs, but about *how well it scales*.

---

## 📦 Simple Analogy: Checking Boxes

Imagine you're in a factory inspecting boxes on a conveyor belt:

- 10 boxes → you check 10 → 10 steps  
- 100 boxes → you check 100 → 100 steps  
- 1,000 boxes → you check 1,000 → 1,000 steps  

➡️ **The work increases linearly** with input size. That's `O(n)`.

---

## 🧠 Key Terms

- **n** = size of input  
- **O(n)** = as input grows, the work grows linearly  
- **Big-O** focuses on how performance grows — not exact speed.

---

## 🧪 Real example of O(n)

```csharp
public void PrintNames(string[] names)
{
    foreach (string name in names)
    {
        Console.WriteLine(name);
    }
}
```

➡️ 5 names = 5 prints  
➡️ 500 names = 500 prints  
**Linear time complexity**: `O(n)`

---

## 🛠 Visual Metaphors

| Time Complexity | Analogy |
|-----------------|---------|
| `O(1)` | One spoonful no matter the pot size |
| `O(n)` | One spoonful per person |
| `O(log n)` | Cut the problem in half each time (binary search) |
| `O(n²)` | Couples each member must be feed a spoon |

---

## 📊 Big-O Classifications with  Examples

### `O(1)` – Constant Time  
```csharp
public int GetFirst(int[] arr) => arr[0];
```

---
    
### `O(log n)` – Logarithmic Time  
```csharp
public int BinarySearch(int[] arr, int target)
{
    // Step 1: Initialise pointers to the start (left) and end (right) of the array
    int left = 0, right = arr.Length - 1;

    // Step 2: Repeat while the search space is valid
    while (left <= right)
    {
        // Step 3: Find the middle index
        int mid = (left + right) / 2;

        // 🧪 DEBUG TIP: Print current values to observe how the search space shrinks
        // Console.WriteLine($"left: {left}, mid: {mid}, right: {right}, arr[mid]: {arr[mid]}");

        // Step 4: If the middle value is the target, return its index
        if (arr[mid] == target) return mid;

        // Step 5: If the middle value is less than the target, search the right half
        if (arr[mid] < target) left = mid + 1;

        // Step 6: Otherwise, search the left half
        else right = mid - 1;
    }

    // Step 7: If not found, return -1
    return -1;

    // 📊 Time Complexity: O(log n) – because we halve the search space at each step

    
}
```

---

### `O(n)` – Linear Time  
```csharp
public int SumAll(int[] arr)
{
    // Step 1: Initialise a variable to hold the running total
    int sum = 0;

    // Step 2: Loop through each element in the array
    foreach (int num in arr)
    {
        // Step 3: Add the current number to the running total
        sum += num;
    }

    // Step 4: Return the total sum
    return sum;

    // 📊 Time Complexity: O(n) – the function loops through each element once
}

/*
    🧪 RECOMMENDED TEST CASES:
    
    1. Normal case (target in array):
       BinarySearch(new int[] {1, 3, 5, 7, 9}, 5) → returns 2

    2. Target at start or end:
       BinarySearch(new int[] {10, 20, 30, 40, 50}, 10) → returns 0
       BinarySearch(new int[] {10, 20, 30, 40, 50}, 50) → returns 4

    3. Target not in array:
       BinarySearch(new int[] {2, 4, 6, 8}, 5) → returns -1

    4. Empty array:
       BinarySearch(new int[] {}, 1) → returns -1

    5. Single-element array:
       BinarySearch(new int[] {42}, 42) → returns 0
       BinarySearch(new int[] {42}, 99) → returns -1

    🧪 HANDS-ON EXPERIMENTS:

    ✅ Change the array to unsorted → See what breaks!
       BinarySearch(new int[] {9, 2, 7, 4}, 7); // Incorrect results

    ✅ Print every step to trace how it narrows down.

    ✅ Replace `(left + right) / 2` with `left + (right - left) / 2` to avoid overflow.

    ✅ Try binary search on string arrays or floats to understand flexibility:
       BinarySearch(new string[] {"apple", "banana", "cherry"}, "banana");

    ✅ Visually track search space:
       - Highlight left/mid/right with emojis or arrows in the console.
    */
```

---

### `O(n log n)` – Linearithmic Time  
```csharp
// Recursive Merge Sort – Time Complexity: O(n log n)
public void MergeSort(int[] arr)
{
    // Base case: if the array has 1 or 0 elements, it's already sorted
    if (arr.Length <= 1) return;

    // Step 1: Split the array into two halves
    int mid = arr.Length / 2;

    // Left half: from index 0 up to (but not including) mid
    int[] left = arr[..mid];

    // Right half: from index mid to the end
    int[] right = arr[mid..];

    // Step 2: Recursively sort both halves
    MergeSort(left);
    MergeSort(right);

    // Step 3: Merge the two sorted halves back into the original array
    Merge(arr, left, right);

    
}

/*
    🧪 DEBUG TIP:
    Console.WriteLine($"Merging: Left = [{string.Join(", ", left)}], Right = [{string.Join(", ", right)}]");
    Console.WriteLine($"Result = [{string.Join(", ", arr)}]");
    */

    /*
    📌 TESTING RECOMMENDATIONS:
    
    ✅ Basic usage:
       int[] nums = { 5, 2, 8, 1, 3 };
       MergeSort(nums);
       Console.WriteLine(string.Join(", ", nums));  // → 1, 2, 3, 5, 8

    ✅ Try edge cases:
       - Empty array → int[] a = {};
       - One element → int[] a = {42};
       - Already sorted → int[] a = {1, 2, 3};
       - Reversed → int[] a = {9, 7, 5, 3, 1};
       - Duplicates → int[] a = {5, 1, 5, 3, 1};

    ✅ Try printing recursion depth:
       Use a counter or indentation level to visualise recursion.

    ✅ Trace merging visually:
       Highlight what elements are being compared and copied.
    */

// Helper method: merges two sorted arrays (left and right) into the result array
private void Merge(int[] result, int[] left, int[] right)
{
    int i = 0, j = 0, k = 0;

    // Step 1: While both halves have unprocessed elements
    while (i < left.Length && j < right.Length)
    {
        // Copy the smaller element into the result array
        if (left[i] <= right[j])
            result[k++] = left[i++];
        else
            result[k++] = right[j++];
    }

    // Step 2: Copy any remaining elements from left
    while (i < left.Length)
        result[k++] = left[i++];

    // Step 3: Copy any remaining elements from right
    while (j < right.Length)
        result[k++] = right[j++];

   
}

 /*
    🧪 DEBUG TIP:
    Console.WriteLine($"Merged to: [{string.Join(", ", result)}]");
    */
```

---

### `O(n²)` – Quadratic Time  
```csharp
// This function prints all possible ordered pairs from the array, including duplicates and self-pairs.
// Time complexity: O(n²) due to the nested loops.
public void PrintAllPairs(int[] arr)
{
    // Outer loop: iterate over every element in the array
    for (int i = 0; i < arr.Length; i++)
    {
        // Inner loop: for each arr[i], iterate through the full array again
        for (int j = 0; j < arr.Length; j++)
        {
            // Print the pair (arr[i], arr[j]) – this includes self-pairing like (2,2)
            Console.WriteLine($"({arr[i]}, {arr[j]})");
        }
    }

    
}

/*
    🧪 TESTING SUGGESTIONS:

    ✅ Try with a small array:
       int[] arr = {1, 2, 3};
       PrintAllPairs(arr);
       // Output:
       // (1,1), (1,2), (1,3)
       // (2,1), (2,2), (2,3)
       // (3,1), (3,2), (3,3)

    ✅ Visualise pair matrix:
       Use tabbed output to draw a 2D grid of pairs if helpful.

    ✅ Compare to unique pairs (i < j):
       You could modify the inner loop to only print unique combinations:
       for (int j = i + 1; j < arr.Length; j++) —> removes duplicate and mirrored pairs.

    ✅ Try with duplicates in the array:
       int[] arr = {1, 1, 2};
       → Observe how repeated values affect output.

    ✅ Try with an empty or single-element array:
       int[] arr = {}; or int[] arr = {42};

    ✅ Count number of pairs:
       Add a counter to understand growth pattern:
       int count = 0; then count++; after each print
       → Shows how n² pairs grow rapidly as array size increases.
    */

```

---

### `O(2ⁿ)` – Exponential Time  
```csharp
// This function recursively calculates the nth Fibonacci number.
// Time complexity: O(2ⁿ) — very inefficient for large n due to repeated recalculations of the same values.
public int Fibonacci(int n)
{
    // Base case: for n = 0 or n = 1, return n directly
    // F(0) = 0, F(1) = 1
    if (n <= 1) return n;

    // Recursive case:
    // F(n) = F(n - 1) + F(n - 2)
    // This causes an exponential explosion of calls for large n
    // Many subproblems are solved multiple times (e.g., F(3) appears in both F(5) and F(4))
    return Fibonacci(n - 1) + Fibonacci(n - 2);
}

   /*
    🧪 TESTING & LEARNING TIPS:

    ✅ Try small inputs:
       Console.WriteLine(Fibonacci(0)); // 0
       Console.WriteLine(Fibonacci(1)); // 1
       Console.WriteLine(Fibonacci(5)); // 5
       Console.WriteLine(Fibonacci(10)); // 55

    ⚠️ Try larger input like:
       Console.WriteLine(Fibonacci(30));
       → Notice how much slower it gets! (Exponential time)

    🔍 Visualise the call stack:
       Try tracing F(5):
       F(5)
        ├── F(4)
        │   ├── F(3)
        │   │   ├── F(2)
        │   │   │   ├── F(1)
        │   │   │   └── F(0)
        │   │   └── F(1)
        │   └── F(2)
        │       ├── F(1)
        │       └── F(0)
        └── F(3)
            ├── F(2)
            │   ├── F(1)
            │   └── F(0)
            └── F(1)

    🚀 Improve it:
       Use **memoization** or **dynamic programming** to store results and avoid recomputation.

       // Memoized version example:
       Dictionary<int, int> cache = new();
       public int FibonacciMemo(int n)
       {
           if (n <= 1) return n;
           if (cache.ContainsKey(n)) return cache[n];
           return cache[n] = FibonacciMemo(n - 1) + FibonacciMemo(n - 2);
       }

    📈 Key takeaway:
       Brute-force recursive Fibonacci is a classic *"what not to do"* when performance matters.
    */
```

---

### `O(n!)` – Factorial Time  
```csharp
// This function generates all permutations of a list of integers using recursion and backtracking.
// Time complexity: O(n!) — factorial time because it explores every possible arrangement of the list.
public void Permute(List<int> nums, int start)
{
    // 🧪 EXPERIMENT 1:
    // Try printing 'start' and 'nums' at each step to see how the recursion progresses
    // Console.WriteLine($"start: {start} → {string.Join(", ", nums)}");

    // 🧩 Base Case:
    // When 'start' reaches the end, a full permutation is ready.
    if (start == nums.Count)
    {
        Console.WriteLine(string.Join(", ", nums)); // Print the final permutation
        return;
    }

    // 🔁 Loop from the current index to the end to generate permutations
    for (int i = start; i < nums.Count; i++)
    {
        // 🧪 EXPERIMENT 2:
        // Add a print statement to see which elements are being swapped
        // Console.WriteLine($"Swapping index {start} and {i}: {nums[start]} ↔ {nums[i]}");

        // 🔄 Swap to fix an element at the 'start' position
        (nums[start], nums[i]) = (nums[i], nums[start]);

        // 🧪 EXPERIMENT 3:
        // Insert a pause here to step through permutations slowly
        // Console.ReadLine(); // Hit enter to continue

        // 🔁 Recurse to permute the remaining sublist
        Permute(nums, start + 1);

        // 🔙 Backtrack to reset the list
        (nums[start], nums[i]) = (nums[i], nums[start]);

        // 🧪 EXPERIMENT 4:
        // After backtracking, print to confirm the list is restored
        // Console.WriteLine($"Backtracked: {string.Join(", ", nums)}");
    }
}

    /*
    🧪 EXPERIMENT 5: Try this with different inputs!
    -------------------------------------------------
    → Permute(new List<int> { 1, 2, 3 }, 0);
    → Permute(new List<int> { 1, 1, 2 }, 0); // See how duplicates affect output
    → Permute(new List<int> { }, 0);        // What happens with empty list?
    → Permute(new List<int> { 42 }, 0);     // What if there's only one element?

    🧪 EXPERIMENT 6: Modify the base case
    -------------------------------------------------
    - Try returning early only when `start == nums.Count - 1`
    - See how that changes the output (hint: incomplete permutations)

    🧪 EXPERIMENT 7: Sort and skip duplicates (Challenge!)
    -------------------------------------------------
    - Sort the list before the loop
    - Inside the loop, skip i when nums[i] == nums[start] and i != start
    - Helps avoid duplicate permutations (requires a bit more logic)

    🧪 EXPERIMENT 8: Return a list of permutations instead of printing
    -------------------------------------------------
    - Modify the function to return `List<List<int>>`
    - Instead of printing, add a copy of the list to the result
    - Useful for using the permutations in later logic

    🧠 EXTRA CHALLENGE:
    -------------------------------------------------
    - Implement a non-recursive version using a stack or queue!
    - Try to count permutations instead of printing
    - Visualise the recursion as a tree (great for whiteboarding)
    */

```

---

## ⚠️ Why Do We Ignore `O(1)` Inside `O(n)`?

Big-O focuses on dominant growth as `n → ∞`. So constants like `O(1)` are **ignored** unless they define the entire function.

```csharp
// This function sums all elements in an array and returns the result multiplied by 2.
// Time Complexity: O(n) — linear, since it loops through the array once.
public int SumElementsAndMultiplyByTwo(int[] arr)
{
    // ✅ Step 1: Initialise a variable to store the running total — O(1)
    int total = 0;

    // ✅ Step 2: Loop through each element in the array — O(n)
    foreach (int num in arr)
        total += num; // Each addition is constant time → overall this loop is O(n)

    // ✅ Step 3: Multiply the total by 2 — O(1)
    return total * 2;

    // 🧠 Final Time Complexity:
    // O(1) for initialisation + O(n) for the loop + O(1) for the final operation
    // Simplified → O(n)
}

// Total: O(1 + n + 1) = O(n)

/*
🧪 EXPERIMENT 1:
- Try printing the `total` inside the loop to see it accumulate step-by-step:
    Console.WriteLine($"Running total: {total}");

🧪 EXPERIMENT 2:
- Change the final operation to multiply by a different number or apply other math:
    return total * 3;
    return total + 100;
    return total / arr.Length; // Average

🧪 EXPERIMENT 3:
- What happens with edge cases?
    int[] empty = new int[] { };           // → Should return 0
    int[] oneElement = new int[] { 10 };   // → Should return 20
    int[] negatives = new int[] { -1, -2 };// → Should return -6

🧪 EXPERIMENT 4:
- Return early if the array is empty (to avoid unnecessary loop):
    if (arr.Length == 0) return 0;

🧪 EXPERIMENT 5:
- Replace the `foreach` with a `for` loop and compare readability and performance.

🧪 EXPERIMENT 6:
- Use LINQ instead:
    return arr.Sum() * 2;
  Compare readability and performance (especially for large arrays).
*/

```

---

## 🧮 Understanding Logarithmic Time – O(log n)

Logarithmic complexity means **halving the input** until 1.

```text
n = 16 → log₂(n) = 4 steps:
16 → 8 → 4 → 2 → 1
```

In :

```csharp
while (n > 1)
{
    n = n / 2;
    steps++;
}
```

---

## 🎯 Summary Table

| Big-O     | Meaning                        | Growth Pattern                      |
|-----------|-------------------------------|--------------------------------------|
| O(1)      | Constant                       | Always takes same steps              |
| O(log n)  | Logarithmic                    | Cut in half each time                |
| O(n)      | Linear                         | One operation per element            |
| O(n log n)| Linearithmic                   | Split + sort + merge                 |
| O(n²)     | Quadratic                      | Every element with every other       |
| O(2ⁿ)     | Exponential                    | Doubles for each element             |
| O(n!)     | Factorial                      | All combinations/permutations        |

---

# 🚀 Big-O Time Complexity in : Brute-force vs Optimised

This showcases how we can refactor simple brute-force algorithms into more efficient solutions using proper Big-O reasoning. Each pair highlights a common task solved first with a brute-force mindset, and then using optimised logic and data structures like `HashSet`, `Dictionary`, and `StringBuilder`.

---

## 🔧 Algorithm Pairs

Each example includes:

- A **Brute-force** solution with unnecessary or inefficient logic
- An **Optimised** solution that achieves the same result with better time complexity

---

### 1️⃣ Find the Largest Number in an Array

```csharp
// Brute-force approach to finding the maximum value in an array
// ❗ Time Complexity: O(n²) – because for each element, we compare it with all others
public int FindMaxBrute(int[] arr)
{
    // Step 1: Start by setting 'max' to the smallest possible integer value
    // This will hold the maximum value if no element satisfies the condition in the loop
    int max = int.MinValue;

    // Step 2: Outer loop – for each element in the array
    for (int i = 0; i < arr.Length; i++)
    {
        // Assume the current element is the maximum until proven otherwise
        bool isMax = true;

        // Step 3: Inner loop – compare this element with every other element
        for (int j = 0; j < arr.Length; j++)
        {
            // If we find another element that is greater, then this one is not the max
            if (arr[j] > arr[i])
            {
                isMax = false;
                break; // No need to check further, move to the next outer element
            }
        }

        // Step 4: If this element was greater than or equal to all others, return it as max
        if (isMax) return arr[i];
    }

    // Fallback: return 'max' (though in practice, line above should return the max first)
    return max;
}

// Optimised O(n)
public int FindMax(int[] arr)
{
    // STEP 1: Assume the first element is the largest (set max to arr[0])
    // STEP 2: Loop through each number in the array
    // STEP 3: If the current number is greater than max, update max
    // STEP 4: After the loop, return the max
}
```

---

### 2️⃣ Count Even Numbers

```csharp
// Brute-force method to count even numbers in an array
// ❗ Time Complexity: O(n²) – due to the unnecessary inner loop for each number
public int CountEvensBrute(int[] arr)
{
    // Step 1: Initialise a counter to keep track of even numbers
    int count = 0;

    // Step 2: Iterate through each number in the array (O(n))
    foreach (int num in arr)
    {
        // Step 3: Assume the number is not even
        bool isEven = false;

        // Step 4: Inner loop (O(num)) – loops from 1 to num (unnecessarily)
        // Although this loop doesn't do anything with 'i', it runs num times
        for (int i = 1; i <= num; i++)
        {
            // This check is repeated multiple times even though the result is the same
            if (num % 2 == 0) isEven = true;
        }

        // Step 5: If the number is even, increment the count
        if (isEven) count++;
    }

    // Step 6: Return the total count of even numbers
    return count;
}

// Optimised O(n)
public int CountEvens(int[] arr)
{
    // STEP 1: Create a counter variable (set to 0)
    // STEP 2: Loop through each number in the array
    // STEP 3: If the number is divisible by 2 (num % 2 == 0), increment the counter
    // STEP 4: Return the counter
}
```

---

### 3️⃣ Check for Duplicates

```csharp
// Brute-force method to check if an array contains duplicate values
// ❗ Time Complexity: O(n²) – compares every unique pair of elements
public bool HasDuplicatesBrute(int[] arr)
{
    // Step 1: Iterate through each element in the array using index i
    for (int i = 0; i < arr.Length; i++)
    {
        // Step 2: For each i, compare it with every element after it (index j)
        for (int j = i + 1; j < arr.Length; j++)
        {
            // Step 3: If a duplicate is found, return true immediately
            if (arr[i] == arr[j]) return true;
        }
    }

    // Step 4: If no duplicates were found, return false
    return false;
}

// Optimised O(n) using HashSet
public bool HasDuplicates(int[] arr)
{
    // STEP 1: Create an empty HashSet to track seen numbers
    // STEP 2: Loop through each number in the array
    // STEP 3: If the number is already in the HashSet, return true
    // STEP 4: Otherwise, add the number to the HashSet
    // STEP 5: After the loop, return false (no duplicates found)
}
```

---

### 4️⃣ Sum of First N Numbers

```csharp
// Brute-force method to calculate the sum of all numbers from 1 to n
// 🕒 Time Complexity: O(n) – performs one addition per number
public int SumUpToNBrute(int n)
{
    // Step 1: Initialise a sum variable to hold the result – this is constant time (O(1))
    int sum = 0;

    // Step 2: Loop from 1 to n, adding each number to the sum – this loop runs n times
    for (int i = 1; i <= n; i++)
    {
        sum += i;  // Each iteration does one addition → O(n) total
    }

    // Step 3: Return the final computed sum – also constant time (O(1))
    return sum;
}

// Optimised O(1) using formula
public int SumUpToN(int n)
{
    // STEP 1: Use the arithmetic formula n * (n + 1) / 2
    // STEP 2: Return the result
}

```

---

### 5️⃣ Find Index of Target

```csharp
// Brute-force linear search to find the index of a target element in an array
// 🕒 Time Complexity: O(n) – potentially checks every element once
public int IndexOfTargetBrute(int[] arr, int target)
{
    // Step 1: Loop through each index of the array
    for (int i = 0; i < arr.Length; i++)
    {
        int temp = arr[i];  // Optional: storing the current value in a temp variable (not necessary)

        // Step 2: Check if the current element matches the target
        if (temp == target) return i;  // If match found, return the index immediately
    }

    // Step 3: If the loop completes with no match, return -1 to indicate not found
    return -1;
}

// Optimised O(n)
public int IndexOfTarget(int[] arr, int target)
{
    // STEP 1: Loop through the array with an index variable
    // STEP 2: Check if the current element is equal to the target
    // STEP 3: If so, return the current index
    // STEP 4: If the loop finishes, return -1 (not found)
}
```

---

### 6️⃣ Count Word Frequency

```csharp
// Brute-force word frequency counter
// 🕒 Time Complexity: O(n²) – for each word, compares it with all others
public Dictionary<string, int> WordCountBrute(string[] words)
{
    // Step 1: Create a dictionary to hold the final word counts
    Dictionary<string, int> result = new Dictionary<string, int>();

    // Step 2: Loop through each word in the array
    foreach (string word in words)
    {
        int count = 0; // Counter for how many times this word appears

        // Step 3: For each word, loop again through the array to count its total occurrences
        foreach (string compare in words)
        {
            if (word == compare) count++; // If the word matches, increment the count
        }

        // Step 4: Add the word and its count to the result dictionary
        result[word] = count;
    }

    // Step 5: Return the full dictionary with word frequencies
    return result;
}

// Optimised O(n)
public Dictionary<string, int> WordCount(string[] words)
{
    // STEP 1: Create a dictionary to hold word counts
    // STEP 2: Loop through each word in the array
    // STEP 3: If the word is already in the dictionary, increment its count
    // STEP 4: Otherwise, add the word with count 1
    // STEP 5: Return the dictionary
}
```

---

### 7️⃣ Filter Positive Numbers

```csharp

// Brute-force positive number filter
// 🕒 Time Complexity: O(n) – technically two passes over the array
public List<int> FilterPositivesBrute(int[] arr)
{
    // Step 1: Create a new list to hold all elements (positive and negative)
    List<int> positives = new List<int>();

    // Step 2: Add every number from the input array to the list
    foreach (int num in arr)
        positives.Add(num); // Adds all numbers, even negatives

    // Step 3: Remove all negative numbers from the list
    positives.RemoveAll(x => x < 0); // This makes a second pass over the list

    // Step 4: Return the filtered list containing only non-negative values
    return positives;
}

// Optimised O(n)
public List<int> FilterPositives(int[] arr)
{
    // STEP 1: Create a new list to store results
    // STEP 2: Loop through each number in the array
    // STEP 3: If the number is 0 or positive, add it to the list
    // STEP 4: Return the filtered list
}
```

---

### 8️⃣ Reverse a String

```csharp
// Brute-force string reversal using string concatenation
// 🕒 Time Complexity: O(n²) – due to string immutability in .NET
public string ReverseStringBrute(string input)
{
    // Step 1: Create an empty string to build the reversed result
    string reversed = "";

    // Step 2: Loop through the original string from the end to the beginning
    for (int i = input.Length - 1; i >= 0; i--)
    {
        // Step 3: Add each character to the reversed string (inefficiently)
        reversed += input[i]; // ⚠️ O(n) operation each time due to immutability
    }

    // Step 4: Return the reversed string
    return reversed;
}

// Optimised using StringBuilder
public string ReverseString(string input)
{
    // STEP 1: Create a StringBuilder to build the result
    // STEP 2: Loop from the end of the string to the beginning
    // STEP 3: Append each character to the StringBuilder
    // STEP 4: Convert StringBuilder to string and return it
}
```

---

### 9️⃣ Find Pair with Target Sum

```csharp

// Brute-force approach to check if any two elements in the array sum up to a target value
// 🕒 Time Complexity: O(n²) – checks every unique pair
public bool HasPairBrute(int[] arr, int target)
{
    // Step 1: Loop through each element in the array
    for (int i = 0; i < arr.Length; i++)
    {
        // Step 2: For each element, check every element that comes after it
        for (int j = i + 1; j < arr.Length; j++)
        {
            // Step 3: If a pair adds up to the target, return true
            if (arr[i] + arr[j] == target)
                return true;
        }
    }

    // Step 4: If no pair was found, return false
    return false;
}

// Optimised O(n) with HashSet
public bool HasPair(int[] arr, int target)
{
    // STEP 1: Create an empty HashSet to store seen numbers
    // STEP 2: Loop through each number in the array
    // STEP 3: Calculate complement = target - current number
    // STEP 4: If complement is in HashSet, return true
    // STEP 5: Otherwise, add the current number to the HashSet
    // STEP 6: Return false after loop (no pair found)
}
```

---

### 🔟 Check if Array is Sorted

```csharp

// Brute-force approach to check if an array is sorted in ascending order
// 🕒 Time Complexity: O(n²) – compares every pair of elements
public bool IsSortedBrute(int[] arr)
{
    // Step 1: Loop through each element in the array
    for (int i = 0; i < arr.Length; i++)
    {
        // Step 2: Compare the current element with every element that comes after it
        for (int j = i + 1; j < arr.Length; j++)
        {
            // Step 3: If any element ahead is smaller, the array is not sorted
            if (arr[i] > arr[j])
                return false;
        }
    }

    // Step 4: If no such pair is found, the array is sorted
    return true;
}

// Optimised O(n)
public bool IsSorted(int[] arr)
{
    // STEP 1: Loop from the start to the second-to-last element
    // STEP 2: Compare current element with the next one
    // STEP 3: If current is greater than next, return false
    // STEP 4: After the loop, return true (array is sorted)
}
```


## ✍️ Created by Ricardo Rosa

If you're interested in **learning or teaching algorithms**, or want to book **1:1 or classroom tutoring**, visit:

🌐 [CoderRosa Website](https://coderrosa.webflow.io/)
