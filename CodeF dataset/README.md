## CodeF
We construct an entirely new dataset, CodeF. Taking September 2021 (the cutoff date for ChatGPT’s training data) as the node, we divided this dataset into two parts: CodeF pre2021-9 which comprises problems that ChatGPT might have encountered during its training, CodeF post2021-9 which consists of problems that ChatGPT would not have previously seen.

CodeF incorporates 1523 problems posted from January 2020 to April 2023 on the CodeForces programming website. The creation of CodeF primarily involves two phases: data acquisition and processing. 

During the data acquisition phase, we evaluated several programming contest platforms, including Codeforces, HackerRank and Geeksforgeeks. Factors such as legal restrictions, interface complexities of the platforms and our specific requirement for algorithms and data structures tag for the problems, as well as the release time information, led us to select CodeForces (a programming competition website) as our data source. In order to ensure dataset quality, we designed an HTML parser specifically tailored for the CodeForces site. We crawled the site for problem description, solution, input and output examples and a set of associated labels, which include difficulty, date and tag (indicating algorithms and data structures suitable for solving the problem), etc. We consolidated all the problems into a standardized format. Figure 1 below
presents a sample of the collected problems.



<div align="center">
  <img src="https://github.com/CodeGeneration3/KareCoder/blob/main/CodeF%20dataset/Example%20of%20a%20programming%20problem.png?raw=true" width="659" height="445" alt="Example of a programming problem">
  <br>
  <p> Figure 1: Example of a programming problem (including problem description, Input/Output format and example, solution code, labels and other information).</p>
</div>



During the data acquisition process, we endeavoured to ensure the consistency of our data with that of the CodeForces website. However, since the code was sourced from user submissions, often embedded with comments and potential error codes, we implemented the following measures during the data processing phase: 

• To render CodeF more orderly, we employed Abstract Syntax Tree (AST) parsing to remove comment nodes from code that was heavily annotated. 

• Even though we extracted code that was tested and verifiedas correct by the website, we conducted unit tests on all code to prevent errors during parsing. This step assuredthe accuracy of the test samples and code. 

• Based on the date tag, we partitioned CodeF into two subsets: CodeF Pre2021-9 and CodeF Post2021-9.

According to the cutoff date of ChatGPT’s training data - September 2021, we partitioned the dataset into CodeF pre2021-9 (comprising 805 problems) and CodeF post2021-9 (consisting of 718 problems). The difficulty level of all problems is denoted in the format “*xxx” (ranging from *800-*31003).

In order to explore the rules of different difficulty problems, we classified the datasets according to the level of difficulty and extracted one hundred problems each from the Simple, Medium and Hard difficulty categories from both datasets.

| Dataset    |  Difficulty | Difficulty Range  |  Problem Number |
|------------|----------|-------|------|
|CodeF Post2021-9  | Simple | *800        | 000-099  |
| CodeF Post2021-9 | Medium | *1300-*1600 | 400-499  |
| CodeF Post2021-9 | Hard   | *1900-*2500 | 600-699  |
| CodeF Pre2021-9  | Simple | *800        | 000-099  |
| CodeF Pre2021-9  | Medium | *1300-*1600 | 400-499  |
| CodeF Pre2021-9  | Hard   | *1900-*2200 | 640-739  |
