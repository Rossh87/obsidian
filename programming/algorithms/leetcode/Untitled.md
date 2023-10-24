# Greatest Common Divisor of Strings

URL: https://leetcode.com/problems/greatest-common-divisor-of-strings/description/

Categories:
1. Recursion

Insights:
1. If strings are the same length they MUST be identical for there to be a solution
2. If they aren't the same length, we can recursively bite off the shorter of the two strings, check that it's identical to the prefix of the longer string, then recurse with the 'tail', i.e. the un-compared part of the longer string 

Notes: If there is a match, the first characters of the longer string must correspond to each character of the shorter string. If that's the case, 

Solution:
```go
func gcdOfStrings(str1 string, str2 string) string {
    if str1 == str2 {
        return str1
    }

    if len(str2) > len(str1) {
        str1, str2 = str2, str1
    }

    if str1[:len(str2)] != str2 {
        return ""
    }

    return gcdOfStrings(str1[len(str2):], str2)
}
```