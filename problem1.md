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
    #include <bits/stdc++.h>
    #define ll long long int
    using namespace std;

    int main() {
      ll n, x;
      cin >> n >> x;
      vector<ll> arr(n);
      for (int i = 0; i < n; i++) {
        cin >> arr[i];
      }

      ll sum = 0LL;
      map<ll, ll> mp;
      ll ans = 0;
      for (int i = 0; i < n; i++) {
        sum += arr[i];
        if (sum == x) {
          ans++;
        }
        if (mp.find(sum - x) != mp.end()) {
          ans += mp[sum - x];
        }
        mp[sum]++;
      }
      cout << ans << endl;
  ```

  Java code:
```java
  import java.util.*;
  
  public class Main {
      public static void main(String[] args) {
          Scanner scanner = new Scanner(System.in);
  
          long n = scanner.nextLong();
          long x = scanner.nextLong();
          long[] arr = new long[(int)n];
          for (int i = 0; i < n; i++) {
              arr[i] = scanner.nextLong();
          }
  
          long sum = 0;
          Map<Long, Long> mp = new HashMap<>();
          long ans = 0;
          for (int i = 0; i < n; i++) {
              sum += arr[i];
              if (sum == x) {
                  ans++;
              }
              if (mp.containsKey(sum - x)) {
                  ans += mp.get(sum - x);
              }
              mp.put(sum, mp.getOrDefault(sum, 0L) + 1);
          }
  
          System.out.println(ans);
      }
  }
```
