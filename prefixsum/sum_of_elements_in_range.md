## Given an array nums, answer multiple queries about the sum of elements within a specific range [i, j].

Example:

Input: nums = [1, 2, 3, 4, 5, 6], i = 1, j = 3

Output: 9

## Approaches
    1. [Naive Approach](#naive-approach)
    2. [Prefix Sum Approach](#prefix-sum-approach)

### Naive Approach:

### Intution
The simplest approach is to calculate the sume of the elements between the given two indices.
this involves iterating through the elements between the given indices.

#### Code
```javascript
function sumofelements(arr, s, e) {
    let sum = 0;

    for(let i=s, i<=e; i++) {
        sum += arr[i];
    }
    return sum;
}

console.log(sumofelements(nums, i, j));

#### Complexity Analysis
- **Time Complexity**: O(n) per query, where n is the number of elements between `i` and `j`. 
- **Space Complexity**: O(1), as we do not use any additional a sum variable.

### Prefix Sum Approach

#### Intuition
To optimize the sum computation for each query, we can leverage precomputation using a prefix sum array. The idea is to preprocess the array to calculate and store cumulative sums such that the sum of any subarray can be obtained in constant time. The prefix sum array at index `i` contains the sum of the array elements from the start up to that index.

#### Code
```javascript

function preCompute(pf, arr){
    pf[0] = arr[0];
    for(let i=1; i<arr.length; i++){
        pf[i] = arr[i] + pf[i-1]
    }
}

function sumofEle(pf, s, e){
    if(s===0) {
        return pf[e];
    } else{
        return pf[e] - pf[s-1]
    }
}

function sumofelementsPrefix(arr, s, e) {
    let sum = 0;
    let pf = []

    preCompute(pf, arr);
    return sumofEle(pf, s, e);
}

#### Complexity Analysis
- **Time Complexity**: 
  - Preprocessing: O(n), where n is the length of the input array for constructing the prefix sum array.
  - Query: O(1), each `sumRange` query is resolved in constant time as it involves only two array accesses and a subtraction.
- **Space Complexity**: O(n), to store the prefix sum array of size n+1.

