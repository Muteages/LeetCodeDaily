# Meeting Rooms III

https://leetcode.com/problems/meeting-rooms-iii

You are given an integer n. There are n rooms numbered from 0 to n - 1.

You are given a 2D integer array meetings where meetings[i] = [starti, endi] means that a meeting will be held during the half-closed time interval [starti, endi). All the values of starti are unique.

Meetings are allocated to rooms in the following manner:

Each meeting will take place in the unused room with the lowest number.
If there are no available rooms, the meeting will be delayed until a room becomes free. The delayed meeting should have the same duration as the original meeting.
When a room becomes unused, meetings that have an earlier original start time should be given the room.
Return the number of the room that held the most meetings. If there are multiple rooms, return the room with the lowest number.


## Approach

``` C++
    int mostBooked(int n, vector<vector<int>>& meetings) {
        std::sort(meetings.begin(), meetings.end());
        std::vector<int> rooms(n, 0); // Record the numbers of meetings that held in rooms.
        std::priority_queue<int, std::vector<int>, std::greater<int>> availableRooms;
        for (int i = 0; i < n; i++)
        {
            availableRooms.emplace(i);
        }

        std::priority_queue<std::pair<long long, int>, std::vector<std::pair<long long, int>>, std::greater<>> occupiedRooms; // endingTime - room number
        for (int i = 0; i < meetings.size(); i++)
        {
            long long originalStart = meetings[i][0];
            long long originalEnd = meetings[i][1];
    
            while (!occupiedRooms.empty() && occupiedRooms.top().first <= originalStart)
            { // Release available rooms
                availableRooms.emplace(occupiedRooms.top().second);
                occupiedRooms.pop();
            }

            if (!availableRooms.empty())
            { // It's able to hold current meeting on time
                int room = availableRooms.top();
                availableRooms.pop();
                occupiedRooms.emplace(meetings[i][1], room);
                rooms[room]++;
            }
            else
            { // The meeting need to be delayed, find the room that the meeting will end the soonest 
                auto [time, room] = occupiedRooms.top();
                occupiedRooms.pop();
                long long duration = originalEnd - originalStart;
                occupiedRooms.emplace(time + duration, room);
                rooms[room]++;
            }
        }
        auto it = std::max_element(rooms.begin(), rooms.end());
        return it - rooms.begin();
    }
```
