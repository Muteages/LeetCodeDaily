# Number of Senior Citizens

ou are given a 0-indexed array of strings details. Each element of details provides information about a given passenger compressed into a string of length 15. The system is such that:

The first ten characters consist of the phone number of passengers.
The next character denotes the gender of the person.
The following two characters are used to indicate the age of the person.
The last two characters determine the seat allotted to that person.
Return the number of passengers who are strictly more than 60 years old.

## Approach 

``` JavaScript
var countSeniors = function(details) {
    return details.reduce((cnt, detail) => {
        return cnt + (Number(detail.slice(11,13)) > 60);
        }, 0);
};
```

``` JavaScript
var countSeniors = function(details) {
    return details.filter(detail => detail.slice(11, 13) > 60).length;
};
```

``` C++
    int countSeniors(vector<string>& details) {
        return std::count_if(details.begin(), details.end(), [](std::string& s) {
            return std::stoi(s.substr(11, 2)) > 60;
        });
    }
```