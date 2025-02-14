# Product of the Last K Numbers

https://leetcode.com/problems/product-of-the-last-k-numbers


Design an algorithm that accepts a stream of integers and retrieves the product of the last k integers of the stream.

Implement the ProductOfNumbers class:

ProductOfNumbers() Initializes the object with an empty stream.
void add(int num) Appends the integer num to the stream.
int getProduct(int k) Returns the product of the last k numbers in the current list. You can assume that always the current list has at least k numbers.
The test cases are generated so that, at any time, the product of any contiguous sequence of numbers will fit into a single 32-bit integer without overflowing.


## Approach 

``` C++
class ProductOfNumbers {
public:
    ProductOfNumbers() : n(0) {
        products.emplace_back(1);
    }
    
    void add(int num) {
        if (num == 0)
        { // Reset products since all possible products including current numebr will be 0 and we don't need to keep it
            products = {1};
            n = 0;
        }
        else
        {
            products.emplace_back(products[n++] * num);
        }
    }
    
    int getProduct(int k) {
        if (n < k) return 0; // Indicates there aren't enough non-zero continuous number
        return products[n] / products[n - k];
    }

private:
    std::vector<int> products;
    int n;
};
```

``` Python
class ProductOfNumbers:

    def __init__(self):
        self.products = [1]
        self.n = 0

    def add(self, num: int) -> None:
        if num == 0:
            self.products = [1]
            self.n = 0
        else:
            self.products.append(self.products[-1] * num)
            self.n += 1

    def getProduct(self, k: int) -> int:
        if self.n < k:
            return 0
        return self.products[-1] // self.products[- 1 - k]
```

``` JavaScript
var ProductOfNumbers = function() {
    this.products = [1];
    this.n = 0;
};

/** 
 * @param {number} num
 * @return {void}
 */
ProductOfNumbers.prototype.add = function(num) {
    if (num === 0) {
        this.products = [1];
        this.n = 0;
    } else {
        this.products.push(this.products[this.n] * num);
        this.n++;
    }
};

/** 
 * @param {number} k
 * @return {number}
 */
ProductOfNumbers.prototype.getProduct = function(k) {
    if (this.n < k) return 0;
    return this.products[this.n] / this.products[this.n - k];
};
```

## Approach 2

Just want to try to avoid rebuilding products over and over again
``` C++
class ProductOfNumbers {
public:
    ProductOfNumbers() : n(0) {
       //stream.clear();
        products.emplace_back(1);
        zeros.emplace_back(0);
    }
    
    void add(int num) {
        //stream.emplace_back(num);
        products.emplace_back(num == 0 ? 1 : products.back() * num);
        zeros.emplace_back(zeros.back() + (num == 0));
        n++;
    }
    
    int getProduct(int k) {
        
        if (zeros[n] - zeros[n - k] > 0) return 0;
        return products[n] / products[n - k];
    }

private:
    std::vector<int> products;
    std::vector<int> zeros;
    int n;
};
```