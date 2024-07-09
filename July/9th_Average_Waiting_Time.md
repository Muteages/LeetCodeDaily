# Average Waiting Time

https://leetcode.com/problems/average-waiting-time

There is a restaurant with a single chef. You are given an array customers, where customers[i] = [arrivali, timei]:

arrivali is the arrival time of the ith customer. The arrival times are sorted in non-decreasing order.
timei is the time needed to prepare the order of the ith customer.
When a customer arrives, he gives the chef his order, and the chef starts preparing it once he is idle. The customer waits till the chef finishes preparing his order. The chef does not prepare food for more than one customer at a time. The chef prepares food for customers in the order they were given in the input.

Return the average waiting time of all customers. Solutions within 10-5 from the actual answer are considered accepted.


## Approach 

``` C++
    double averageWaitingTime(vector<vector<int>>& customers) {
        double sum = 0;
        const int n = customers.size();
        int available{}, arrive{}, waiting{};
        for (const auto& customer : customers)
        {
            arrive = customer[0];
            waiting = customer[1];
            if (available <= arrive)
            { // Enable to prepare food on time
                available = arrive + waiting;
                sum += waiting;
            }
            else
            { // Occupied, wait till the previous order is done
                available += waiting;
                sum += available - arrive;
            }
        }
        return sum / n;
    }
```

A more concise way
``` C++
    double averageWaitingTime(vector<vector<int>>& customers) {
        double sum = 0;
        int available = 0;
        for (const auto& customer : customers)
        {
            available = std::max(available, customer[0]) + customer[1];
            sum += available - customer[0];
        }
        return sum / customers.size();
    }
```