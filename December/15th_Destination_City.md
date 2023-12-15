# Destination City

https://leetcode.com/problems/destination-city

You are given the array paths, where paths[i] = [cityAi, cityBi] means there exists a direct path going from cityAi to cityBi. Return the destination city, that is, the city without any path outgoing to another city.

## Approach 1 

unordered_map
``` C++
    string destCity(vector<vector<string>>& paths) {
        std::unordered_map<std::string, std::string> ump;
        for (const auto& path : paths)
        {            
            ump[path[0]] = path[1];
            if (ump.find(path[1]) == ump.end())
            {
                ump[path[1]] = "";
            }
            
        }

        for (const auto& [go, to] : ump)
        {
            if (to == "")
            { // Find the desination city 
                return go;
            }
        }
        return "";
    }
```

## Approach 2

unordered_set
``` C++
    string destCity(vector<vector<string>>& paths) {
        std::unordered_set<std::string> us;

        for (const auto& path : paths)
        {
            us.insert(path[0]);
        } 

        for (const auto& path : paths)
        {
            if (us.find(path[1]) == us.end())
            {
                return path[1];
            }
        }
        return "";
    }
```