# Problems

## Arrays

### Second Largest Element in an Array

Given an array of positive integers arr[] of size n, the task is to find second largest distinct element in the array.

Note: If the second largest element does not exist, return -1.

Examples:

Input: arr[] = [12, 35, 1, 10, 34, 1]
Output: 34
Explanation: The largest element of the array is 35 and the second largest element is 34.

Input: arr[] = [10, 5, 10]
Output: 5
Explanation: The largest element of the array is 10 and the second largest element is 5.

Input: arr[] = [10, 10, 10]
Output: -1
Explanation: The largest element of the array is 10 there is no second largest element.

``` java

import java.util.*;
import java.util.stream.*;

public class SecondLargest {
    public static int findSecondLargest(int[] arr) {
        return Arrays.stream(arr)
            .boxed()                           // Convert to Stream<Integer>
            .distinct()                        // Remove duplicates
            .sorted(Comparator.reverseOrder()) // Sort descending
            .skip(1)                           // Skip the largest
            .findFirst()                       // Get the second largest
            .orElse(-1);                       // Return -1 if not present
    }

    public static void main(String[] args) {
        int[] arr1 = {10, 5, 10, 3, 1};
        int[] arr2 = {8};  // Only one element

        System.out.println(findSecondLargest(arr1)); // Output: 5
        System.out.println(findSecondLargest(arr2)); // Output: -1
    }
}

```

### Third Largest Element in an Array

Given an array of n integers, the task is to find the third largest element. All the elements in the array are distinct integers. 

Examples : 

Input: arr[] = {1, 14, 2, 16, 10, 20}
Output: 14
Explanation: Largest element is 20, second largest element is 16 and third largest element is 14

Input: arr[] = {19, -10, 20, 14, 2, 16, 10}
Output: 16
Explanation: Largest element is 20, second largest element is 19 and third largest element is 16 

``` java

import java.util.*;

class Main {
    public static void main(String[] args) {
        int[] arr = { 19, -10, 20, 14, 2, 16, 10 };
        System.out.println(getSolution(arr));
    }
    
    private static int getSolution(int[] nums) {
        return Arrays.stream(nums)
                        .boxed()
                        .distinct()
                        .sorted(Comparator.reverseOrder())
                        .skip(2)
                        .limit(1)
                        .findFirst()
                        .orElse(-1);
    }
}

```

### Maximum product of a triplet in an array

Given an integer array, find a maximum product of a triplet in the array.

Examples: 

Input:  arr[ ] = [10, 3, 5, 6, 20]
Output: 1200
Explanation: Multiplication of 10, 6 and 20

Input:  arr[ ] =  [-10, -3, -5, -6, -20]
Output: -90

Input: arr[ ] =  [1, -4, 3, -6, 7, 0]
Output: 168

3 ways different ways to find 3 max values and 2 min values and then return (m1 * m2* m3) or (mi1 * mi2* m1) whichever is greater.

``` java

// Java program to find a maximum product of a
// triplet in array of integers using sorting

import java.util.*;

class GfG {
    /* Function to find a maximum product of a triplet
       in array of integers of size n */
    static int maxProduct(int[] arr) {
        int n = arr.length;
        
        // Sort the array in ascending order
        Arrays.sort(arr);

        // Return the maximum of product of last three
        // elements and product of first two elements
        // and last element
        return Math.max(arr[0] * arr[1] * arr[n - 1],
                        arr[n - 1] * arr[n - 2] * arr[n - 3]);
    }

    public static void main(String[] args) {
        int[] arr = {-10, -3, 5, 6, -20}; 
        int max = maxProduct(arr);
        System.out.println(max);
    }
}

```

``` java

// A O(n) Java program to find maximum product
// pair in an array.
import java.util.*;

class GfG {
    
    /* Function to find a maximum product of a triplet
       in array of integers of size n */
    static int maxProduct(int[] arr) {
        int n = arr.length;

        // Initialize Maximum, 
        // second maximum and third maximum element
        int maxA = Integer.MIN_VALUE, 
        maxB = Integer.MIN_VALUE, maxC = Integer.MIN_VALUE;

        // Initialize Minimum and second minimum element
        int minA = Integer.MAX_VALUE, minB = Integer.MAX_VALUE;

        for (int i = 0; i < n; i++) {
            
            // Update Maximum, second maximum
            // and third maximum element
            if (arr[i] > maxA) {
                maxC = maxB;
                maxB = maxA;
                maxA = arr[i];
            } else if (arr[i] > maxB) {
                maxC = maxB;
                maxB = arr[i];
            } else if (arr[i] > maxC) {
                maxC = arr[i];
            }

            // Update Minimum and second minimum element
            if (arr[i] < minA) {
                minB = minA;
                minA = arr[i];
            } else if (arr[i] < minB) {
                minB = arr[i];
            }
        }

        return Math.max(minA * minB * maxA, maxA * maxB * maxC);
    }

    public static void main(String[] args) {
        int[] arr = {-10, -3, 5, 6, -20};
        System.out.println(maxProduct(arr));
    }
}

```

``` java

import java.util.*;
import java.util.stream.*;

public class MaxTripletProduct {
    public static int maximumProduct(int[] arr) {
        List<Integer> list = Arrays.stream(arr).boxed().collect(Collectors.toList());

        // Get top 3 max elements
        List<Integer> top3 = list.stream()
            .sorted(Comparator.reverseOrder())
            .limit(3)
            .collect(Collectors.toList());

        // Get bottom 2 min elements
        List<Integer> bottom2 = list.stream()
            .sorted()
            .limit(2)
            .collect(Collectors.toList());

        // Calculate the two possible max products
        int product1 = top3.get(0) * top3.get(1) * top3.get(2); // three largest
        int product2 = bottom2.get(0) * bottom2.get(1) * top3.get(0); // two smallest & largest

        return Math.max(product1, product2);
    }

    public static void main(String[] args) {
        int[] arr1 = {10, 3, 5, 6, 20};
        int[] arr2 = {-10, -3, -5, -6, -20};
        int[] arr3 = {1, -4, 3, -6, 7, 0};

        System.out.println(maximumProduct(arr1)); // Output: 1200
        System.out.println(maximumProduct(arr2)); // Output: -90
        System.out.println(maximumProduct(arr3)); // Output: 168
    }
}


```