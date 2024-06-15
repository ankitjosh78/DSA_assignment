## Given an array of n integers. Find the total number of subarrays that have sum X.
  ### Input:
  The first line contains two integers *n* and *X*.
  
  The next line has n intgers a<sub>1</sub>, a<sub>2</sub>, ... a<sub>n</sub>.

  ### Output:
  Print one integer: the required number of subarrays.

### Solution: 
  This problem can be solved using Hashing. 
  But what is Hashing?
  1. Hashing is a fundamental algorithmic technique that efficiently stores and retrieves data in a way that allows for quick access. 
  2. It involves mapping data to a specific index in a hash table using a hash function that enables fast retrieval of information based on its key. 
  3. This method is commonly used in databases, caching systems, and various programming applications to optimize search and retrieval operations.

  Now, coming to this question. We want to find the total number of subarrays that have sum equal to some given value.
  
  For solving it, we are going to use a technique called Prefix Sum and Hashing.

  #### Prefix Sum Concept:

  The prefix sum of an array at index (*i*) is the sum of all elements till the index (*i*) starting from the beginning.

  If we have prefix sum array, we can calculate the sum for any subarray. 

  *sum(a[l]...a[r]) = prefixSum[r] - prefixSum[l-1]*

  


  #### Using Hash Map:

  We maintain a hash map to store the frequency of prefix sums.

  As we iterate through the array, we compute the prefix sum and check if *prefixSum - X* exists in the hash map. f it does, it means there is a subarray ending at the current index that sums to X.

  We will use a hash map to store the frequency of prefix sums encountered.

  C++ code:

  ```c++
    #include <iostream>
    #include <unordered_map>
    #include <vector>
    
    int countSubarraysWithSumX(const std::vector<int>& arr, int X) {
        std::unordered_map<int, int> prefixSumFreq;
        int prefixSum = 0;
        int count = 0;
    
        // Initial condition for subarrays that start from the beginning
        prefixSumFreq[0] = 1;
    
        for (int num : arr) {
            prefixSum += num;
    
            // Check if there exists a prefix sum that would form the required sum
            if (prefixSumFreq.find(prefixSum - X) != prefixSumFreq.end()) {
                count += prefixSumFreq[prefixSum - X];
            }
    
            // Update the frequency of the current prefix sum
            prefixSumFreq[prefixSum]++;
        }
    
        return count;
    }
    
    int main() {
        int n, X;
        std::cin >> n >> X;
    
        std::vector<int> arr(n);
        for (int i = 0; i < n; ++i) {
            std::cin >> arr[i];
        }
    
        int result = countSubarraysWithSumX(arr, X);
        std::cout << "Total number of subarrays with sum " << X << " is: " << result << std::endl;
    
        return 0;
    }
  ```

  Java code:
```java
import java.util.HashMap;
import java.util.Scanner;

public class SubarraySum {
    
    public static int countSubarraysWithSumX(int[] arr, int X) {
        HashMap<Integer, Integer> prefixSumFreq = new HashMap<>();
        int prefixSum = 0;
        int count = 0;

        // Initial condition for subarrays that start from the beginning
        prefixSumFreq.put(0, 1);

        for (int num : arr) {
            prefixSum += num;

            // Check if there exists a prefix sum that would form the required sum
            if (prefixSumFreq.containsKey(prefixSum - X)) {
                count += prefixSumFreq.get(prefixSum - X);
            }

            // Update the frequency of the current prefix sum
            prefixSumFreq.put(prefixSum, prefixSumFreq.getOrDefault(prefixSum, 0) + 1);
        }

        return count;
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        int n = scanner.nextInt();
        int X = scanner.nextInt();
        int[] arr = new int[n];

        for (int i = 0; i < n; i++) {
            arr[i] = scanner.nextInt();
        }

        int result = countSubarraysWithSumX(arr, X);
        System.out.println("Total number of subarrays with sum " + X + " is: " + result);
        
        scanner.close();
    }
}
```
