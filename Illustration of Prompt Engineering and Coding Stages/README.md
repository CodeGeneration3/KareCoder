# Illustration of Prompt Engineering and Coding Stages
The objective of code generation is to aid individuals in resolving programming issues. We postulate that the thought process of LLMs parallels that of human programmers, which can be bifurcated into two stages when tackling programming problems: initially, comprehending the problem and learning or recalling knowledge that may be applied to its resolution, followed by formulating a preliminary plan;    secondly, executing code writing based on this plan.
Consequently, we partition the workflow of KareCoder into two stages, Prompt Engineering and Coding, adhering to a sequential approach to the task:

• In the Prompt Engineering Stage, we designate ChatGPT as a prompt engineer, accountable for comprehending the problem and learning as well as reviewing the algorithms and data structures knowledge pertinent to resolving the issue, subsequently generating a problem-solving prompt.

• In the Coding Stage, we assign ChatGPT the role of a coder, tasked with perusing the problem and implementing this solution in a programming language, guided by the prompt provided by the prompt engineer.

# You can see the full details in Figures 6 and 7 of our article here
## Example 1
### Problem (Q)：
You are given a grid with $n$ rows and $m$ columns. We denote the square on the $i$-th ($1\le i\le n$) row and $j$-th ($1\le j\le m$) column by $(i, j)$ and the number there by $a_{ij}$. All numbers are equal to $1$ or to $-1$.

You start from the square $(1, 1)$ and can move one square down or one square to the right at a time. In the end, you want to end up at the square $(n, m)$.

Is it possible to move in such a way so that the sum of the values written in all the visited cells (including $a_{11}$ and $a_{nm}$) is $0$?


-----Input-----

Each test contains multiple test cases. The first line contains the number of test cases $t$ ($1 \leq t \leq 10^4$). Description of the test cases follows.

The first line of each test case contains two integers $n$ and $m$ ($1 \le n, m \le 1000$)  — the size of the grid.

Each of the following $n$ lines contains $m$ integers. The $j$-th integer on the $i$-th line is $a_{ij}$ ($a_{ij} = 1$ or $-1$)  — the element in the cell $(i, j)$.

It is guaranteed that the sum of $n\cdot m$ over all test cases does not exceed $10^6$.


-----Output-----

For each test case, print "YES" if there exists a path from the top left to the bottom right that adds up to $0$, and "NO" otherwise. You can output each letter in any case.


-----Examples-----

Input
5
1 1
1
1 2
1 -1
1 4
1 -1 1 -1
3 4
1 -1 -1 -1
-1 1 1 -1
1 1 1 -1
3 4
1 -1 1 1
-1 1 -1 1
1 -1 1 1
Output
NO
YES
YES
YES
NO

-----Note-----

One possible path for the fourth test case is given in the picture in the statement.
### Knowledge Description (K'):
"DP":"DP, or dynamic programming, is a technique used to solve complex problems by breaking them down into smaller, simpler sub-problems. It involves solving each sub-problem only once and storing the solutions in a table for future use. DP is used in optimization problems where the goal is to find the optimal solution among many possible solutions. It is often more efficient than brute force or other methods, but requires careful analysis and design of the sub-problems. DP is commonly used in fields such as computer science, engineering, and finance."

"Data Structures":"Data structures are arrangements of data in a computer's memory that enable efficient access, storage, and manipulation of information. They provide a means for organizing and managing data, and are essential for efficient algorithm design. Examples of data structures include arrays, linked lists, stacks, queues, trees, and graphs. Each data structure has its own advantages and disadvantages, and selecting the appropriate structure depends on the nature of the data and the operations to be performed on it."

"Brute Force":"Brute force is a straightforward approach to problem-solving that exhaustively searches all possible solutions. It involves systematically testing each possible solution until the correct one is found. This approach is often used when the problem size is small, or when other methods are not feasible. Brute force can be computationally expensive and impractical for large-scale problems, but it is guaranteed to find the optimal solution, if one exists. It is commonly used in algorithm design for testing and benchmarking."
### Knowledge-aware Prompt (P):
1.Read t, the number of test cases.

2.Loop t times to read each test cases.

3.Read n and m, the dimensions of the matrix.

4.Read the elements of the n x m matrix and store them in a 2D list a.

5.Check if (n + m - 1) is odd. If it is, print "NO" and continue to the next test case.

6.Create a list dp of length m + 1, initialized with all zeros.

7.Loop n times, allet dp[0] to 1 if i is 0, otherwise keep it 0.

8.Loop m times, compute the value of dp[j + 1] based on dp[j], dp[j + 1] and the element at a[i][j]. The bit shift operation is used here to handle the state transition.

9.Check the (n+m-1)//2 bit of dp[-1]. If it is 1, print "YES"; otherwise, print "NO".

10.End all loop.
### Solution Code (C):
```python  
for case in range(int(input())):
    n, m = map(int, input().split())
    a = [list(map(int, input().split())) for _ in range(n)]
    if (n + m - 1) % 2:
        print("NO")
        continue
    dp = [0] * (m + 1)
    for i in range(n):
        dp[0] = int(not i)
        for j in range(m):
            dp[j + 1] = (dp[j] | dp[j + 1]) << (a[i][j] == -1)
    if dp[-1] & (1 << ((n + m - 1) // 2)):
        print("YES")
    else:
        print("NO")
```

## Example 2
### Problem (Q)：
There is a string $s$ of length $3$, consisting of uppercase and lowercase English letters. Check if it is equal to "YES" (without quotes), where each letter can be in any case. For example, "yES", "Yes", "yes" are all allowable.

-----Input-----

The first line of the input contains an integer $t$ ($1 \leq t \leq 10^3$) — the number of testcases.

The description of each test consists of one line containing one string $s$ consisting of three characters. Each character of $s$ is either an uppercase or lowercase English letter.

-----Output-----

For each test case, output "YES" (without quotes) if $s$ satisfies the condition, and "NO" (without quotes) otherwise.

You can output "YES" and "NO" in any case (for example, strings "yES", "yes" and "Yes" will be recognized as a positive response).

-----Examples-----

Input
10
YES
yES
yes
Yes
YeS
Noo
orZ
yEz
Yas
XES
Output
YES
YES
YES
YES
YES
NO
NO
NO
NO
NO

-----Note-----

The first five test cases contain the strings "YES", "yES", "yes", "Yes", "YeS". All of these are equal to "YES", where each character is either uppercase or lowercase.
### Knowledge Description (K'):
"Brute Force":"Brute force is a straightforward approach to problem-solving that exhaustively searches all possible solutions. It involves systematically testing each possible solution until the correct one is found. This approach is often used when the problem size is small, or when other methods are not feasible. Brute force can be computationally expensive and impractical for large-scale problems, but it is guaranteed to find the optimal solution, if one exists. It is commonly used in algorithm design for testing and benchmarking."

"Strings":"Strings are sequences of characters used to represent text or other data in a computer program. String algorithms are used to manipulate and process strings, such as searching for substrings, replacing characters, and comparing two strings. String algorithms can be simple or complex, and may require specialized techniques such as pattern matching or regular expressions. They are used in a variety of applications, including text processing, natural language processing, and data analysis. Proper selection and implementation of string algorithms can significantly impact the performance and functionality of a software system."

"Implementation":"Implementation is the process of translating a design or specification into a working program. It involves writing code, compiling and testing the program, and integrating it with other systems. Implementation also includes documenting the code and providing user support. Good implementation requires attention to detail, adherence to coding standards, and the ability to adapt to changing requirements. Effective implementation leads to a reliable and maintainable software system."
## Knowledge-aware Prompt (P):
1.Read t, the number of test cases.

2.Loop t times to read each test case string s.

3.Convert the string s to lowercase using the built-in function lower().

4.Check if the string s is equal to "yes".

5.If it is, print "YES". Otherwise, print "NO".

6.End the loop."
### Solution Code (C):
```python  
t = int(input())
for i in range(t):
    s = input()
    s = s.lower()
    print('YES' if s == 'yes' else 'NO')
```
