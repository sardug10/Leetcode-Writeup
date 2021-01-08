## Leetcode Problem 1190

[Link](https://leetcode.com/problems/reverse-substrings-between-each-pair-of-parentheses/)

#### Problem Title

**Reverse Substrings Between Each Pair of Parentheses**
You are given a string s that consists of lower case English letters and brackets.

Reverse the strings in each pair of matching parentheses, starting from the innermost one.

Your result should not contain any brackets.

**Example**

> **Input**: s = "(ed(et(oc))el)"
> **Output**: "leetcode"
> **Explanation**: First, we reverse the substring "oc", then "etco", and finally, the whole string.

### Solution

#### Intuition

So, in this problem, as you can see we are given a string with lowercase English letters and parentheses. We have to reverse the string inside matching parentheses, starting from the innermost one. Also, we should not include any brackets in the resulted string.

#### What we have to do?

If you read the problem again and look at the example carefully, you will realize that our main tasks for this problem are very small.

**Our tasks include:-**
**1)** Traversing the given string from the start.
**2)** **If our character is either '(' or 'any alphabet'** , we will **store it** in some suitable data structure.
**3)** The moment **we hit a closing bracket ')'.** We need to **get all the previous characters of the string until we hit the opening bracket.** With this, **we have the string between a pair of brackets.**
Now all left is to **reverse this string and then join it with the characters before the opening bracket.**
**4)** We will **perform tasks 2 and 3 until the end of the string.** In this way, we will reverse every string in a pair of the bracket, and at last, we will get the result.

Now, the **data structure that we will choose** to store the characters that we are iterating through, **should perform the push and pop function with best optimization.** It is **because we'll only be inserting and removing from the end.**

Using **stacks**, in this case, **is the best option but we can also use arrays because inserting and removing from the end has O(1) time complexity.**
<br/>

#### So, let's start by writing the code, and then I will explain it to you.

```python
class Solution:
    def reverseParentheses(self, s: str) -> str:
        stack = []
        for i in s:
            if i == '(' or i.isalpha() == True:
                stack.append(i)
            else:
                temp = ''
                while True:
                    previous = stack.pop()
                    if previous != '(':
                        temp = previous + temp
                    else:
                        temp = temp[::-1]
                        stack.append(temp)
                        break
        return ''.join(stack)
```

1. **The first thing,** that we are doing in this code is to **initialize an empty "stack" array.**
2. Next, we will **start iterating through the string** and will **do the required operations stated above.**

   - In the first condition, we are checking **if our character is either '(' or an alphabet.** If it is so, then we will **insert that at the end.**
   - **If it's not, then obviously it's going to be a closing bracket.**. **In that case,** we will **initialize a new variable "temp" with an empty string.**
     Now, **when we will start popping out the previous characters from the stack, we will concatenate them.**

   We will **do the previous operation until our previous character is not an opening bracket.**

   - If it is the case, we will **take our temp variable, reverse the string that has been stored in it until now.** Finally, we will **push that temp variable at the end of the stack.** So, **in this way, when the next ')' occurs, it will take the whole previous string at once and not single characters thus saving our time.**

**Finally, at the end of the loop, we will join all the character strings in the stack and return it as a single string.**

#### Complexity Analysis

- Time Complexity: **The time complexity would have been O(N)** if we have only while loop inside the for loop. It is **because the outer for loop will run N times. Also, Each index gets pushed and popped at most once from the stack.** But, **since we are also reversing the string inside the while loop, and in the worst case it could take O(N) time complexity.** Therefore, **our time complexity will become O(N^2).**

- Space Complexity: O(W^2). **The size of the stack is bounded** as it represents the characters in the string. Also, **in the temp variable we have to (in worst case) we will be storing the whole string.**
