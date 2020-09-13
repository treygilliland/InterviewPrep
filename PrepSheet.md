# Preperation sheet
This sheet is an in-order document of which topics I covered for preperation so I know what to review when finished.

<details>
    <summary>Binary & Bit Manipulation</summary>

### Bitwise Operators
1. & - AND  
2. | - OR  
3. ^ - XOR  
4. ~ - One's Complement  
5. << - Left Bit Shift  
* roughly equal to multiplying by 2

6. \>\> - Arithmetic Right Bit Shift  
* roughly equal to dividing by 2 
* arithmetic == fills in most signifigant bit (MSB) w/ sign of leading bit

7. \>\>\> - Logical Right Bit Shift
* logical == fills in most signifigant bit w/ 0

Note: +, -, * can also be used for binary arithmetic  
Note: - can be used as a "Two's Complement Operator"

### Common Tasks & Tricks
* & operator is commonly used to mask bits, downsize bits, and to turn bits off.
* | operator is used to turn bits on.

**Get Value @ index i:**
```
num & (1 << i) != 0
```

**Set Value @ index i**
```
num |= (1 << i)
```

**Clear Value @ index i**
```
num &= ~(1 << i)
```

**Clear Bits from MSB to index i (inclusive)**
```
num &= (1 << i)-1
```

**Clear Bits from index i to 0 (inclusive)**
```
num &= (-1 << (i+1))
```

**Clear LSB**
```
num &= (num-1)
```

### Top 75 Problems
<details>
<summary>[Sum of Two Integers](https://leetcode.com/problems/sum-of-two-integers/)</summary>

* ^ operator can be used for addition when bits do not need to be carried.
* Using the & operator on both numbers will return the bits that need to be carried

```
def getSum(self, a: int, b: int) -> int:  
    mask = 0xffffffff  
    
    if not (b&mask):  
        return a  
        
    return mask & self.getSum(a^b, (a&b)<<1)
```
</details>

<details>
<summary>[Number of 1 Bits](https://leetcode.com/problems/number-of-1-bits/)</summary>

```
while(n):
    n = n & (n-1) # this removes LSB  
    count++  
```
</details>

<details>
<summary>[Counting Bits](https://leetcode.com/problems/counting-bits/)</summary>

DP solution (Best):
```
def countBits(self, num: int) -> List[int]:
        dp = [0]
        for i in range(1, num + 1):
            # if odd, it is the last number + LSB
            if i % 2 == 1:
                dp.append(dp[i - 1] + 1)
            # if even, it is the same as the number half its size
            else:
                dp.append(dp[i // 2])
        return dp
```

Brute force solution:
* Use solution of "Number of 1 Bits" above to count each number individually
</details>

<details>
<summary>[Missing Number](https://leetcode.com/problems/missing-number/)</summary>

Two solutions:  
* Get sum of summation with (n*(n+1)/2) and without missing number and subtract to find it
* Starting with the num = len(li), iterate through li and ^ the number at index i and index i and you will be left with the missing number

</details>

<details>
<summary>[Reverse Bits](https://leetcode.com/problems/reverse-bits/)</summary>

```
# Pythonic way, easy to understand.
def reverseBits(self, n):
    bit_str = '{0:032b}'.format(n)
    reverse_str = bit_str[::-1]
    return int(reverse_str, 2)

# General way, easy to understand.
def reverseBits_1(self, n):
    reversed = 0
    for i in range(32):
        reversed = reversed << 1
        reversed |= (n >> i) & 0x1
    return reversed
```

</details>
</details>

<details>
<summary>Linked Lists</summary>
There really isn't much to talk about when it comes to Linked Lists. 
See [Interview Notes](https://raw.githubusercontent.com/treygilliland/InterviewPrep/master/InterviewNotes.md) for more detail.

* O(n) access and search  
* O(1) insertion and deletion at tails
* In LeetCode Questions, linked lists will be implemented using Node classes  
* LinkedList can be just a pointer to head node or a LinkedList class wrapper to ensure no messy pointer update issues  
* Python lists can be used as linked lists  
* For more efficiency, python has collections.deque for implementation of doubly linked lists.  

### Common Questions
<details>
    <summary>CTCI explanations</summary>
Remove duplicates:  
  * Use a HashMap as a temporary buffer  
  * If no buffer is allowed, then use MergeSort and then remove duplicates from a sorted LL  
  
K'th to the last:  
  * Go to the end, to find the length. (length - k) => number of elements to go through. Then, iterate again and return  
  * Use a runner which is k places ahead. When the runner reaches the end, your main pointer will be k'th to the last  
  
Deleting a node:  
  * Go until you find it, and skip: O(n)  
  
Partition around a value:  
  * Use a runner to get to the value that you need to partition around. Then add one from the head, and one from the runner, alternatively  
  
Intersection/Loop Detection:  
  * If you can use C/C++, just use pointers  
  * If not, you can still check the reference by == for objects
</details>
<details>
    <summary>Top 75 Problems</summary>
    
Reverse a Linked List - https://leetcode.com/problems/reverse-linked-list/

Detect Cycle in a Linked List - https://leetcode.com/problems/linked-list-cycle/  
* see more on cycle detection [here](https://en.wikipedia.org/wiki/Cycle_detection#Tortoise_and_hare)

Merge Two Sorted Lists - https://leetcode.com/problems/merge-two-sorted-lists/  

Merge K Sorted Lists - https://leetcode.com/problems/merge-k-sorted-lists/  
* can be done similar to two sorted lists or using merge sort or using priority queue to determine next node

Remove Nth Node From End Of List - https://leetcode.com/problems/remove-nth-node-from-end-of-list/  
* done using two pointers n-distance apart, remove on slow pointer

Reorder List - https://leetcode.com/problems/reorder-list/  
* use fast/slow pointer to split the lists
* reverse the second half
* merge the two lists
</details>
