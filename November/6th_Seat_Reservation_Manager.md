# Seat Reservation Manager

https://leetcode.com/problems/seat-reservation-manager

Design a system that manages the reservation state of n seats that are numbered from 1 to n.

Implement the SeatManager class:

SeatManager(int n) Initializes a SeatManager object that will manage n seats numbered from 1 to n. All seats are initially available.
int reserve() Fetches the smallest-numbered unreserved seat, reserves it, and returns its number.
void unreserve(int seatNumber) Unreserves the seat with the given seatNumber.

## Approach 1

``` C++
public:
    SeatManager(int n) {
        for (int i = 1; i <= n; i++)
        {
            seats.emplace(i);
        }
    }
    
    int reserve() {
        int seat = seats.top();
        seats.pop();
        return seat;
    }
    
    void unreserve(int seatNumber) {
        seats.emplace(seatNumber);
    }
private:
    std::priority_queue<int, std::vector<int>, std::greater<>> seats;
```

## Approach 2

Optimal Solution

``` C++
public:
    SeatManager(int n) 
        : unreservedSmallest(1)
    {}
    
    int reserve() {
        if (!seats.empty())
        { // Indicates there must be at least one smaller seat which is unreserved
            int seat = seats.top();
            seats.pop();
            return seat;
        }

        return unreservedSmallest++;
    }
    
    void unreserve(int seatNumber) {
        unreservedSeats.emplace(seatNumber);
    }
private:
    int unreservedSmallest;
    std::priority_queue<int, std::vector<int>, std::greater<>> unreservedSeats;
```