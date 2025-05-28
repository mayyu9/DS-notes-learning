# [Leetcode Problem 2485. Find the Pivot Integer](https://leetcode.com/problems/find-the-pivot-integer/description/)

## Approaches
1. [Naive Approach](#naive-approach)
2. [Prefix Sum Approach](#prefix-sum-approach)

### Naive Approach

#### Intuition
Pivot index is nothing but the index where the sum of elements from left = sum of elements from right

first calculate the prefix array of left which is inclusive of the ith element.
now loop over starting from the last element 'n' till >=1


#### Code
```javascript
function pivot(n) {
   // calculate prefixsum for left
    for(let i=1; i<=n; i++) {
        left[i] = i + left[i-1];
        // left.push(i + left[i - 1])
        // left.push(temp)
    }

    // console.log("left: ", left);
    let right = 0;
    for(let i=n; i >= 1; i--) {
        right += i;
        
        // console.log("right: ", right, i, left[i]);
        if(left[i] == right){
            return i;
        }
    }
    return -1
}
// Example usage:
// const numArray = new NumArray([-2, 0, 3, -5, 2, -1]);
console.log(pivot(8))
```

#### Complexity Analysis
- **Time Complexity**: O(n), iterating over the range of elements.
- **Space Complexity**: O(n), we have left array

### Prefix Sum Approach

#### Intuition
To optimize the sum computation for each query, we can leverage precomputation using a prefix sum array. The idea is to preprocess the array to calculate and store cumulative sums such that the sum of any subarray can be obtained in constant time. The prefix sum array at index `i` contains the sum of the array elements from the start up to that index.

#### Code
```javascript
function pivot(n) {
   let total = 0;
    
    for(let i=1; i<=n; i++){
        total += i;
    }
    
    let left =0; let right = 0; let i=1;
    
    while(i<=n) {
        right = total - left - i; //  from total subtract left and current value like sliding window
        
        if(left == right) {
            return i;
        }
        left = left + i;
        i++;
    }
    
    return -1
}
// Example usage:
// const numArray = new NumArray([-2, 0, 3, -5, 2, -1]);
console.log(pivot(8))


#### Complexity Analysis
- **Time Complexity**: O(n), iterating over the range of elements.
- **Space Complexity**: O(1)

The prefix sum approach drastically improves the query efficiency by sacrificing some additional space, making it highly effective for handling multiple range sum queries on a static array of numbers.
