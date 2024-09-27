# My Calendar II

https://leetcode.com/problems/my-calendar-ii/

You are implementing a program to use as your calendar. We can add a new event if adding the event will not cause a triple booking.

A triple booking happens when three events have some non-empty intersection (i.e., some moment is common to all the three events.).

The event can be represented as a pair of integers start and end that represents a booking on the half-open interval [start, end), the range of real numbers x such that start <= x < end.

Implement the MyCalendarTwo class:

MyCalendarTwo() Initializes the calendar object.
boolean book(int start, int end) Returns true if the event can be added to the calendar successfully without causing a triple booking. Otherwise, return false and do not add the event to the calendar.

## Approach 

``` C++
class MyCalendarTwo {
public:
    MyCalendarTwo() {

    }
    
    bool book(int start, int end) {
        auto it2 = book2.lower_bound({start, -1});
        // Step 1: Check if the current interval overlaps with interval booked twice
        if ((it2 != book2.end() && it2->first < end) ||
            (it2 != book2.begin() && std::prev(it2)->second > start))
        {
            return 0;
        }
        // Step 2: Check if the current interval overlaps with interval booked once
        for (const auto& [s, e] : book1)
        {
            int maxStart = std::max(start, s), minEnd = std::min(e, end);
            if (maxStart < minEnd)
            { // If it overlaps with the interval within book1, add it to book2
                book2.emplace(maxStart, minEnd);
            }
        }
        book1.emplace_back(start, end);
        return true;
    }

private:
    std::vector<std::pair<int, int>> book1;
    std::set<std::pair<int, int>> book2;
};
```