# Fraction Addition and Subtraction

https://leetcode.com/problems/fraction-addition-and-subtraction

Given a string expression representing an expression of fraction addition and subtraction, return the calculation result in string format.

The final result should be an irreducible fraction. If your final result is an integer, change it to the format of a fraction that has a denominator 1. So in this case, 2 should be converted to 2/1.

## Approach 

``` C++
    std::vector<std::pair<int, int>> extractFractions(const std::string& expression)
    {
        std::vector<std::pair<int, int>> fractions{};
        int sign{1}, prev{}, curr{}, n = expression.size();
        // Check the first possible sign
        if (expression[0] == '-')
        {
            sign = -1;
        }
        else if (std::isdigit(expression[0]))
        {
            curr = expression[0] - '0';
        }

        for (int i = 1; i < n; i++)
        {
            char c = expression[i];
            while (std::isdigit(c))
            {
                curr = 10 * curr + (c - '0');
                if (i == n - 1) break;
                c = expression[++i];
            }

            if (c == '/')
            {
                prev = curr * sign;
                curr = 0;
            }
            else if (c == '+')
            {
                fractions.emplace_back(prev, curr);
                sign = 1;
                curr = 0;
            }
            else if (c == '-')
            {
                fractions.emplace_back(prev, curr);
                sign = -1;
                curr = 0;
            }
        }
        fractions.emplace_back(prev, curr);
        return fractions;
    }

    std::pair<int, int> add(std::pair<int, int>& sum, const std::pair<int, int>& f)
    {
        auto [aNume, aDeno] = sum;
        auto [bNume, bDeno] = f;
        long long nume = aNume * bDeno + aDeno * bNume, 
                  deno = aDeno * bDeno;
        long long g = std::gcd(nume, deno);
        return {nume / g, deno / g};
    }


    string fractionAddition(string expression) {
        auto fractions = extractFractions(expression);
        std::pair<int, int> sum = {0, 1};
        for (auto& f : fractions)
        {
            sum = add(sum, f);
        }
        std::string ans = std::to_string(sum.first) + "/" + std::to_string(sum.second);
        return ans;
    }
```