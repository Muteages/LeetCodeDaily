# Evaluate Reverse Polish Notation

https://leetcode.com/problems/evaluate-reverse-polish-notation

You are given an array of strings tokens that represents an arithmetic expression in a Reverse Polish Notation.

Evaluate the expression. Return an integer that represents the value of the expression.

## Approach 

``` C++
    std::stack<int> nums;
    void calculate(const std::string& op)
    { // It is guaranteed that we can have two numbers before we encounter an operator
        int a = nums.top();
        nums.pop();

        int b = nums.top();
        nums.pop();

        int temp{};
        if (op == "+")
        {
            temp = a + b;
        }
        else if (op == "-")
        {
            temp = b - a;
        }
        else if (op == "*")
        {
            temp = a * b;
        }
        else 
        {
            temp = b / a;
        }
        nums.push(temp);
    };
    int evalRPN(vector<string>& tokens) {
        for (auto& token : tokens)
        {
            if (token.size() > 1 || isdigit(token[0]))
            { // Get a number
                nums.push(std::stoi(token));
            }
            else
            { // Get an operator
                calculate(token); 
            }
        }
        return nums.top();
    }
```