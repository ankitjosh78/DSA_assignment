
## You are given an array of n integers, and your task is to find four values (at distinct positions) whose sum is x.

### Input:
The first input line has two integers *n* and *x*: the array size and the target sum.

The second line has *n* integers a<sub>1</sub>, a<sub>2</sub>, ..., a<sub>n</sub> : the array values.

### Output:
Print four integers: the positions of the values. 

If there are several solutions, you may print any of them. 
If there are no solutions, print IMPOSSIBLE.

### Solution:
#### Idea:
This problem is an extension of the standard 2-Sum Problem.

In that problem, we try to find two indices *i*, *j* such that *a[i]* + *a[j]* = *X*.

We solve that by checking, if for an element *a[i]* in array, there exists another element *X - a[j]* in the array.

If so, we have found the solution. Now, this other element can be easily tracked with help of a hashmap. 

#### Approach:
Now, coming to this problem, we can leverage a hashmap to store sums of pairs of numbers and then check if complementary pairs exist that sum up to *x*.

#### C++ code:
```c++
  #include <bits/stdc++.h>
  #define ll long long int
  using namespace std;
  typedef pair<int, int> pii;
  
  // Define a map to store the sum of pairs and their indices
  map<ll, vector<pii>> mp;
  
  int main() {
      int n;      // Number of elements in the array
      ll x;       // Target sum for the four values
      cin >> n;   // Input the number of elements
      cin >> x;   // Input the target sum
      
      vector<ll> a(n + 1); // Array to store the elements, 1-indexed for convenience
      for (int i = 1; i <= n; i++) {
          cin >> a[i];  // Input the elements
      }
      
      // Iterate over all pairs of elements in the array
      for (int i = 1; i <= n; i++) {
          for (int j = i + 1; j <= n; j++) {
              ll sum = a[i] + a[j]; // Calculate the sum of the current pair
  
              // If the sum is greater than or equal to the target, skip this pair
              if (sum >= x)
                  continue;
  
              // Check if there exists a pair in the map whose sum with the current pair equals x
              if (mp.find(x - sum) != mp.end()) {
                  for (pii P : mp[x - sum]) {
                      // Ensure that all indices are distinct
                      if (P.first != i && P.first != j && P.second != i && P.second != j) {
                          // Print the indices of the four elements
                          cout << P.first << " " << P.second << " " << i << " " << j << endl;
                          return 0; // Exit the program as we found the solution
                      }
                  }
              }
  
              // Store the current pair in the map
              mp[sum].push_back({i, j});
          }
      }
      
      // If no such four elements are found, print "IMPOSSIBLE"
      cout << "IMPOSSIBLE" << endl;
  }
  ```

  #### Java code:
  ```java
  import java.util.*;
  public class FourSum {
      public static void main(String[] args) {
          Scanner scanner = new Scanner(System.in);
  
          int n = scanner.nextInt(); // Number of elements in the array
          long x = scanner.nextLong(); // Target sum for the four values
  
          long[] a = new long[n + 1]; // Array to store the elements, 1-indexed for convenience
          for (int i = 1; i <= n; i++) {
              a[i] = scanner.nextLong(); // Input the elements
          }
  
          Map<Long, List<int[]>> map = new HashMap<>(); // Map to store the sum of pairs and their indices
  
          // Iterate over all pairs of elements in the array
          for (int i = 1; i <= n; i++) {
              for (int j = i + 1; j <= n; j++) {
                  long sum = a[i] + a[j]; // Calculate the sum of the current pair
  
                  // If the sum is greater than or equal to the target, skip this pair
                  if (sum >= x)
                      continue;
  
                  // Check if there exists a pair in the map whose sum with the current pair equals x
                  if (map.containsKey(x - sum)) {
                      for (int[] pair : map.get(x - sum)) {
                          // Ensure that all indices are distinct
                          if (pair[0] != i && pair[0] != j && pair[1] != i && pair[1] != j) {
                              // Print the indices of the four elements
                              System.out.println(pair[0] + " " + pair[1] + " " + i + " " + j);
                              return; // Exit the program as we found the solution
                          }
                      }
                  }
  
                  // Store the current pair in the map
                  map.computeIfAbsent(sum, k -> new ArrayList<>()).add(new int[]{i, j});
              }
          }
  
          // If no such four elements are found, print "IMPOSSIBLE"
          System.out.println("IMPOSSIBLE");
      }
  }
  ```
