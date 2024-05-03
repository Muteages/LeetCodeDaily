# Compare Version Numbers

https://leetcode.com/problems/compare-version-numbers

Given two version numbers, version1 and version2, compare them.

Version numbers consist of one or more revisions joined by a dot '.'. Each revision consists of digits and may contain leading zeros. Every revision contains at least one character. Revisions are 0-indexed from left to right, with the leftmost revision being revision 0, the next revision being revision 1, and so on. For example 2.5.33 and 0.1 are valid version numbers.

To compare version numbers, compare their revisions in left-to-right order. Revisions are compared using their integer value ignoring any leading zeros. This means that revisions 1 and 001 are considered equal. If a version number does not specify a revision at an index, then treat the revision as 0. For example, version 1.0 is less than version 1.1 because their revision 0s are the same, but their revision 1s are 0 and 1 respectively, and 0 < 1.

## Approach 

``` C++
    int compareVersion(string version1, string version2) {
        int l1 = version1.length(), l2 = version2.length();
        int i1 = 0, i2 = 0;
        while (i1 < l1 || i2 < l2)
        {
            int r1 = 0, r2 = 0;
            // Calcuate current revision number
            while (i1 < l1 && version1[i1] != '.')
            {
                r1 = 10 * r1 + (version1[i1] - '0');
                i1++;
            }
            while (i2 < l2 && version2[i2] != '.')
            {
                r2 = 10 * r2 + (version2[i2] - '0');
                i2++;
            }

            if (r1 > r2)
            {
                return 1;
            }
            else if (r1 < r2)
            {
                return -1;
            }
            i1++;
            i2++;
        }
        return 0;
    }
```