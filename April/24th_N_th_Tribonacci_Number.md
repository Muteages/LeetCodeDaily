# Nth Tribonacci Number

The Tribonacci sequence Tn is defined as follows: 

T0 = 0, T1 = 1, T2 = 1, and Tn+3 = Tn + Tn+1 + Tn+2 for n >= 0.

Given n, return the value of Tn.

## Approach 1

``` C++
    int tribonacci(int n) {
        if (n == 0)
        {
            return 0;
        }
        else if (n == 1 || n == 2)
        {
            return 1;
        }
        int a = 0, b = 1, c = 1;
        while (n >= 3)
        {
            int temp = c;
            c += a + b;
            a = b;
            b = temp;
            n--;
        }
        return c;
    }
```

## Approach 2

Variant of Approach 1 but use tuple
``` C++
    int tribonacci(int n) {
        if (n == 0)
        {
            return 0;
        }
        else if (n == 1 || n == 2)
        {
            return 1;
        }
        std::tuple<int, int, int> tri = {0, 1, 1};
        while (n >= 3)
        {
            auto [a, b, c] = tri;
            tri = {b, c, a + b + c};
            n--;
        }
        return std::get<2>(tri);
    }
```

## Approach 3

``` C++
    int tribonacci(int n) {
        std::vector<int> tri(38);
        tri[0] = 0, tri[1] = 1, tri[2] = 1;
        for (int i = 3; i <= n; i++)
        {
            tri[i] = tri[i - 3] + tri[i - 2] + tri[i - 1];
        }
        return tri[n];
    }
```