# Design By Contract
- This is a Discipline of system construction
- It helps to:
  - Get the software right
  - Debug and test the software

- The Contract is the goal you have in mind when you design the software

### We ask: 
  - What does it expect? A precondition
  - What does it promise? A post-condition
  - What does it maintain? An invariant

- A precondition can be used to test the arguments of a method call
- Post-condition could be used to make sure that after an operation has been done the the result still matches what is expected
- An invariant can be used to test whether or not something matches a set of given conditions at all **interesting** times in the program

- Example given: moving a cursor forward
  - Before the move_forth call the cursor is at any position other than the very last
  - After the cursor's position must be at the pre position + 1
  - These are things that are obvious to you because they are the fundamental properties of your method or data structure, but expressing them explicitly ensures:
    - That the method is never doing something that it wasn't expected to do (could tell you where something went wrong faster)
    - That you understand every single step in your method

### Applications

###### Documentation
- These add a layer of documentation to every piece of code
- Other developers can see exactly what is expected at every step in your code

###### Testing
- A bug by definition is a discrepancy between what is expected of a program and what the actual behavior is
- A violation in contract always signals this bug at the exact point that it occurs
- With typical debugging you just know something before the error went wrong

###### Run Time Effect
- These are usually all taken out in production, but it is easy to use some preconditions/postconditions in suspected areas
- If you are running into an issue it is easy to turn these back on, go to lunch, and come back and read the assertion violations that have occurred

###### Benefits
- You know what goes wrong immediately and from the running code itself
- There is no test environment or other extraneous factors to worry about changing in production
- Library's can trust documentation to be up to date and accurate
- Contracts can be inherited
- Catches things that aren't typically tested for or are difficult to test for— ie reuse errors 