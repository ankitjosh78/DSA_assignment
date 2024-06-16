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

  #### C++ code:

  ```c++
    #include <bits/stdc++.h>
    #define ll long long int
    using namespace std;
    
    int main() {
        ll n, x; // n is the number of elements, x is the target sum
        cin >> n >> x; // Input the number of elements and the target sum
        vector<ll> arr(n); // Array to store the elements
        for (int i = 0; i < n; i++) {
            cin >> arr[i]; // Input each element into the array
        }
    
        ll sum = 0LL; // Variable to store the current prefix sum
        map<ll, ll> mp; // Map to store the frequency of prefix sums
        ll ans = 0; // Variable to store the number of subarrays with sum equal to x
    
        // Iterate through each element in the array
        for (int i = 0; i < n; i++) {
            sum += arr[i]; // Update the prefix sum with the current element
    
            // Check if the current prefix sum equals x
            if (sum == x) {
                ans++; // Increment the count of subarrays with sum equal to x
            }
    
            // Check if there exists a prefix sum such that (current prefix sum - desired sum) exists in the map
            if (mp.find(sum - x) != mp.end()) {
                ans += mp[sum - x]; // Add the count of such subarrays to the answer
            }
    
            mp[sum]++; // Increment the frequency of the current prefix sum in the map
        }
    
        cout << ans << endl; // Output the total number of subarrays with sum equal to x
    }

  ```

  #### Java code:
```java
  import java.util.HashMap;
  import java.util.Map;
  import java.util.Scanner;
  
  public class SubarraySum {
      public static void main(String[] args) {
          Scanner sc = new Scanner(System.in);
  
          // Input the number of elements and the target sum
          int n = sc.nextInt();
          long x = sc.nextLong();
  
          long[] arr = new long[n]; // Array to store the elements
          for (int i = 0; i < n; i++) {
              arr[i] = sc.nextLong(); // Input each element into the array
          }
  
          long sum = 0L; // Variable to store the current prefix sum
          Map<Long, Long> mp = new HashMap<>(); // Map to store the frequency of prefix sums
          long ans = 0L; // Variable to store the number of subarrays with sum equal to x
  
          // Iterate through each element in the array
          for (int i = 0; i < n; i++) {
              sum += arr[i]; // Update the prefix sum with the current element
  
              // Check if the current prefix sum equals x
              if (sum == x) {
                  ans++; // Increment the count of subarrays with sum equal to x
              }
  
              // Check if there exists a prefix sum such that (current prefix sum - desired sum) exists in the map
              if (mp.containsKey(sum - x)) {
                  ans += mp.get(sum - x); // Add the count of such subarrays to the answer
              }
  
              // Increment the frequency of the current prefix sum in the map
              mp.put(sum, mp.getOrDefault(sum, 0L) + 1);
          }
  
          System.out.println(ans); // Output the total number of subarrays with sum equal to x
      }
  }
  ```
