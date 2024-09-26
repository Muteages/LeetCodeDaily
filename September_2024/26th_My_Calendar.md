# My Calendar

https://leetcode.com/problems/my-calendar-i/

You are implementing a program to use as your calendar. We can add a new event if adding the event will not cause a double booking.

A double booking happens when two events have some non-empty intersection (i.e., some moment is common to both events.).

The event can be represented as a pair of integers start and end that represents a booking on the half-open interval [start, end), the range of real numbers x such that start <= x < end.

Implement the MyCalendar class:

MyCalendar() Initializes the calendar object.
boolean book(int start, int end) Returns true if the event can be added to the calendar successfully without causing a double booking. Otherwise, return false and do not add the event to the calendar.


## Approach 1

``` C++
class MyCalendar {
public:
    MyCalendar() {
        intervals.clear();
    }
    
    bool book(int start, int end) {
        auto it = intervals.lower_bound({start, -1});

        if ((it != intervals.end() && it->first < end) ||
            (it != intervals.begin() && std::prev(it)->second > start))
        { // Overlap with other intervals
            return 0;
        }

        intervals.emplace(start, end);
        return 1;
    }
private:
    std::set<std::pair<int, int>> intervals;
};
```

## Approach 2

Brute force

``` C++
class MyCalendar {
public:
    MyCalendar() {
        intervals.clear();
    }
    
    bool book(int start, int end) {
        for (auto [is, ie] : intervals)
        {
            if ((start < ie && end > is) || 
                (start < is && end < ie && end > is))
            {
                return false;
            }
        }
        intervals.emplace_back(start, end);
        return true;
    }
    std::vector<std::pair<int, int>> intervals;
};
```

## Approach 3

``` C++
struct Node{
    int s, t;
    Node *left, * right;
    Node(int s, int t): s(s), t(t), left(NULL), right(NULL){}
};
class MyCalendar {
    Node* root;
public:
    MyCalendar(): root(NULL) {}
    
    bool dfs(int s, int t, Node* &curr)
    {
        if (!curr) 
        {
            curr=new Node(s, t);
            return 1;
        }
        if (t<=curr->s) return dfs(s, t, curr->left);
        else if (s>=curr->t) return dfs(s, t, curr->right);
        else return 0;
    }
    
    bool book(int start, int end) {
        return dfs(start, end, root);
    }
};
```