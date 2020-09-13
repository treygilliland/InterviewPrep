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
