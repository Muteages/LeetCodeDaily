# Design a Food Rating System

https://leetcode.com/problems/design-a-food-rating-system

Design a food rating system that can do the following:

Modify the rating of a food item listed in the system.
Return the highest-rated food item for a type of cuisine in the system.
Implement the FoodRatings class:

FoodRatings(String[] foods, String[] cuisines, int[] ratings) Initializes the system. The food items are described by foods, cuisines and ratings, all of which have a length of n.
foods[i] is the name of the ith food,
cuisines[i] is the type of cuisine of the ith food, and
ratings[i] is the initial rating of the ith food.
void changeRating(String food, int newRating) Changes the rating of the food item with the name food.
String highestRated(String cuisine) Returns the name of the food item that has the highest rating for the given type of cuisine. If there is a tie, return the item with the lexicographically smaller name.
Note that a string x is lexicographically smaller than string y if x comes before y in dictionary order, that is, either x is a prefix of y, or if i is the first position such that x[i] != y[i], then x[i] comes before y[i] in alphabetic order.


## Approach 1

Use set
``` C++
class FoodRatings {

struct MyCompare
{
    bool operator()(const std::pair<int, std::string>& f1, const std::pair<int, std::string>& f2) const
    {
        if (f1.first == f2.first)
        { // Name ascending order
            return f1.second < f2.second;
        }
        else
        { // Rating descending order
            return f1.first > f2.first;
        }
    }
};

std::unordered_map<std::string, std::string> cuisineOfFood;   // food - cuisine
std::unordered_map<std::string, int> ratingOfFood;            // food - rating
std::unordered_map<std::string, std::set<std::pair<int, std::string>, MyCompare>> ratingOfCuisine; // cuisine - cuisine list with rating and food name

public:
    FoodRatings(vector<string>& foods, vector<string>& cuisines, vector<int>& ratings) {
        for (int i = 0; i < foods.size(); i++)
        { // Update the maps
            const std::string& food = foods[i];
            const std::string& cuisine = cuisines[i];
            int rating = ratings[i];

            cuisineOfFood[food] = cuisine;
            ratingOfFood[food] = rating;
            
            ratingOfCuisine[cuisine].emplace(rating, food);
        }
    }
    
    void changeRating(string food, int newRating) {
        // Update the rating map
        int oldRating = ratingOfFood[food];
        ratingOfFood[food] = newRating;

        // Update the cuisine rating list
        auto& curCuisineList = ratingOfCuisine[cuisineOfFood[food]];
        curCuisineList.erase(std::make_pair(oldRating, food));
        curCuisineList.emplace(newRating, food);
    }
    
    string highestRated(string cuisine) {
        return ratingOfCuisine[cuisine].begin()->second;
    }
};
```

## Approach 2

Use priority_queue
``` C++
class FoodRatings {

struct MyCompare
{
    bool operator()(const std::pair<int, std::string>& f1, const std::pair<int, std::string>& f2) const
    {
        if (f1.first == f2.first)
        { // Name ascending order
            return f1.second > f2.second;
        }
        else
        { // Rating descending order
            return f1.first < f2.first;
        }
    }
};

std::unordered_map<std::string, std::string> cuisineOfFood;   // food - cuisine
std::unordered_map<std::string, int> ratingOfFood;            // food - rating
std::unordered_map<std::string, std::priority_queue<std::pair<int, std::string>, std::vector<std::pair<int, std::string>>, MyCompare>> ratingOfCuisine; 
// cuisine - cuisine list with rating and food name

public:
    FoodRatings(vector<string>& foods, vector<string>& cuisines, vector<int>& ratings) {
        for (int i = 0; i < foods.size(); i++)
        { // Update the maps
            const std::string& food = foods[i];
            const std::string& cuisine = cuisines[i];
            int rating = ratings[i];

            cuisineOfFood[food] = cuisine;
            ratingOfFood[food] = rating;
            
            ratingOfCuisine[cuisine].emplace(rating, food);
        }
    }
    
    void changeRating(string food, int newRating) {
        // Update the cuisine rating list
        ratingOfCuisine[cuisineOfFood[food]].emplace(newRating, food);
        // Update the rating map
        ratingOfFood[food] = newRating;
    }
    
    string highestRated(string cuisine) {
        auto [rating, food] = ratingOfCuisine[cuisine].top();

        while (rating != ratingOfFood[food])
        {
            ratingOfCuisine[cuisine].pop();
            std::tie(rating, food) = ratingOfCuisine[cuisine].top();
        }
        return food;
    }
};
```