# Minimise XOR

https://leetcode.com/problems/minimize-xor

Given two positive integers num1 and num2, find the positive integer x such that:

x has the same number of set bits as num2, and
The value x XOR num1 is minimal.
Note that XOR is the bitwise XOR operation.

Return the integer x. The test cases are generated such that x is uniquely determined.

The number of set bits of an integer is the number of 1's in its binary representation.

## Approach 

``` C++
    int minimizeXor(int num1, int num2) {
        int oneCnt = popcount((size_t)num2);
        std::bitset<31> ans = 0, num = num1;
        for (int dig = 30; dig >= 0 && oneCnt > 0; dig--)
        {
            if (num[dig] == 1)
            {
                ans[dig] = 1;
                oneCnt--;
            }
        }

        for (int dig = 0; dig < 31 && oneCnt > 0; dig++)
        {
            if (ans[dig] == 0)
            {
                ans.flip(dig);
                oneCnt--;
            }
        }
        return ans.to_ulong();
    }
```

``` JavaScript
var minimizeXor = function(num1, num2) {
    let oneCnt = num2.toString(2).split('1').length - 1;
    let ans = 0;
    for (let dig = 30; dig >= 0 && oneCnt > 0; dig--) {
        if (num1 & (1 << dig)) {
            ans |= (1 << dig);
            oneCnt--;
        }
    }

    for (let dig = 0; dig < 31 && oneCnt; dig++) {
        if (!(ans & (1 << dig))) {
            ans |= (1 << dig);
            oneCnt--;
        }
    }
    return ans;
};
```

``` Python
    def minimizeXor(self, num1: int, num2: int) -> int:
        cnt_num2 = num2.bit_count()
        cnt_num1 = num1.bit_count()

        if cnt_num2 < cnt_num1:
            ans = 0
            for dig in range(31, -1, -1):
                if cnt_num2 and (num1 & 1 << dig):
                    ans |= 1 << dig
                    cnt_num2 -= 1
            
            return ans
        else:
            diff = cnt_num2 - cnt_num1
            for dig in range(31):
                if diff and not(num1 & 1 << dig):
                    num1 |= 1 << dig
                    diff -= 1
            
            return num1
        
        return -1
```