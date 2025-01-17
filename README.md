# LEETCODE-Arrays-2683
**Code:**

```java
class Solution {
    public boolean doesValidArrayExist(int[] derived) {
        int n=derived.length;
        int[] original=new int[n];
        original[0]=0;
        for(int i=0;i<n-1;i++) {
            original[i+1]=original[i]^derived[i];
        }
        if((original[n-1]^original[0])==derived[n-1]) {
            return true;
        }
        original[0]=1;
        for(int i=0;i<n-1;i++) {
            original[i+1]=derived[i]^original[i];
        }
        if((original[n-1]^original[0])==derived[n-1]) {
            return true;
        }
        return false;
    }
}
```

**Explanation:**

This code checks if a valid original array can be constructed from a given `derived` array, where `derived[i] = original[i] XOR original[i+1]`.

**Key Idea:**

- The code explores two possibilities for the first element of the `original` array: 0 and 1.
- For each possibility, it reconstructs the `original` array using the given `derived` array and checks if the last element in the reconstructed `original` array satisfies the condition `original[n-1] XOR original[0] = derived[n-1]`.

**Dry Run Example:**

Let's consider:

- `derived = {1, 2, 3}`

**Case 1: `original[0] = 0`**

1. `original[1] = original[0] ^ derived[0] = 0 ^ 1 = 1`
2. `original[2] = original[1] ^ derived[1] = 1 ^ 2 = 3`
3. `original[3] = original[2] ^ derived[2] = 3 ^ 3 = 0`

- Check: `original[n-1] ^ original[0] = 0 ^ 0 = 0`. 
- Since `derived[n-1] = 3`, the condition `original[n-1] ^ original[0] == derived[n-1]` is not satisfied.

**Case 2: `original[0] = 1`**

1. `original[1] = original[0] ^ derived[0] = 1 ^ 1 = 0`
2. `original[2] = original[1] ^ derived[1] = 0 ^ 2 = 2`
3. `original[3] = original[2] ^ derived[2] = 2 ^ 3 = 1`

- Check: `original[n-1] ^ original[0] = 1 ^ 1 = 0`. 
- Since `derived[n-1] = 3`, the condition `original[n-1] ^ original[0] == derived[n-1]` is not satisfied.

**Conclusion:**

In this example, neither of the two cases satisfies the condition. Therefore, it's not possible to construct a valid `original` array from the given `derived` array.
