
> **The example problem:** _A rectangular garden is 15m long and 8m wide. The owner wants to increase the area by 20% by extending only the length. Find the new length and the new perimeter._

|Topic|Method|Prompt Before Method|Prompt After Following Method|
|---|---|---|---|
|Garden area/perimeter|**General Prompting**|"Solve this: garden length 15m width 8m, increase area by 20% by extending length only. Find new length and perimeter."|"Solve the following math problem step by step. Clearly label each step, show all formulas used, and end with a line that says 'Final Answer: —'. Problem: A rectangular garden is 15m long and 8m wide. The owner wants to increase the area by 20% by extending only the length. Find the new length and the new perimeter."|
|Garden area/perimeter|**Zero/One-Shot Prompting**|"A rectangular garden is 15m long and 8m wide. Increase area by 20% by extending length only. Find new length and perimeter."|"Example: A rectangle is 10m long and 5m wide. To increase its area by 10% by extending the length only: New area = 50 × 1.10 = 55. New length = 55/5 = 11m. New perimeter = 2(11+5) = 32m. Now solve this the same way: A rectangular garden is 15m long and 8m wide. Increase area by 20% by extending the length only. Find the new length and the new perimeter."|
|Garden area/perimeter|**Few-Shot Prompting**|"Solve: garden 15×8, +20% area by extending length only."|"Example 1: Rectangle 10×5, +10% area by extending length → new length 11m, perimeter 32m. Example 2: Rectangle 20×4, +25% area by extending length → new area 100, new length 25m, perimeter 58m. Example 3: Rectangle 6×3, +50% area by extending length → new area 27, new length 9m, perimeter 24m. Now solve: Rectangle 15×8, increase area by 20% by extending length only. Find new length and perimeter."|
|Garden area/perimeter|**System Prompting**|"Solve: garden 15×8, +20% area, extend length only."|_System:_ "You are a precise math tutor. Always define variables first, write the formula, substitute values, and show units at every step. Never skip a calculation."  <br>_User:_ "A rectangular garden is 15m long and 8m wide. Increase the area by 20% by extending the length only. Find the new length and new perimeter."|
|Garden area/perimeter|**Role Prompting**|"Solve: garden 15×8, +20% area, extend length only."|"You are an experienced landscaping contractor explaining a fencing quote to a homeowner in simple, non-technical language. A garden is 15m by 8m and the client wants a 20% bigger area by extending the length only. Explain how you'd calculate the new length and how much new fencing (perimeter) they'll need."|
|Garden area/perimeter|**Contextual Prompting**|"Solve: garden 15×8, +20% area, extend length only."|"I'm a landscaper quoting a fencing job. My client's garden is currently 15m long and 8m wide, and they want to expand the area by 20% by extending the length only (the width stays fixed since there's a wall on that side). Fencing costs $12/meter. Calculate the new dimensions, the new perimeter, and the total fencing cost so I can send an accurate quote."|
|Garden area/perimeter|**Chain-of-Thought Prompting**|"Solve: garden 15×8, +20% area, extend length only."|"Solve this step by step, thinking through each calculation before moving to the next: A rectangular garden is 15m long and 8m wide. The owner wants to increase the area by 20% by extending only the length. Let's think step by step: 1) Find the current area, 2) find the target area after a 20% increase, 3) solve for the new length using the fixed width, 4) compute the new perimeter."|
|Garden area/perimeter|**Self-Consistency Prompting**|"Solve: garden 15×8, +20% area, extend length only."|"Solve this problem using three independent methods: (1) direct area/percentage algebra, (2) proportional reasoning on the length only, (3) plugging numbers into the perimeter formula after finding area. Show all three solutions separately, then compare the final answers and report the value that all three methods agree on as the final answer."|
|Garden area/perimeter|**Tree-of-Thought Prompting**|"Solve: garden 15×8, +20% area, extend length only."|"Explore this problem using multiple reasoning branches before answering. Branch A: solve algebraically by setting up an equation for the new area. Branch B: solve using percentage scaling of the length directly. Branch C: solve by first finding the area increase in m² then dividing by width. For each branch, evaluate whether the logic is sound, discard any branch that gives an inconsistent answer, and converge on the most reliable final answer with justification for why that branch was chosen."|
|Garden area/perimeter|**ReAct Prompting**|"Solve: garden 15×8, +20% area, extend length only."|"You have access to a calculator tool. Use the format: Thought → Action → Observation → ... → Final Answer. Problem: A rectangular garden is 15m long and 8m wide. Increase the area by 20% by extending the length only. Find the new length and new perimeter. Begin: Thought: I need to find the current area first. Action: calculate(15*8). Observation: [result]. Continue this cycle until you reach the Final Answer."|



1. General Prompting — Asking the question plainly with minimal structure or guidance. The model relies entirely on its own judgment for format and approach.

2. One-Shot Prompting — Giving exactly one worked example before the actual question. This shows the model the expected format and reasoning style.

3. Few-Shot Prompting — Giving multiple (usually 2-5) worked examples before the question. More examples help the model infer patterns, edge cases, and consistent formatting.

4. System Prompting — Setting persistent instructions or rules (often via a separate "system" role) that govern how the model should behave throughout. It shapes tone, constraints, and behavior rather than the specific task content.

5. Role Prompting — Assigning the model a specific persona or profession (e.g., "you are a cashier"). This shifts vocabulary, tone, and the angle from which the answer is framed.

6. Contextual Prompting — Embedding the question inside a real-world scenario or purpose (e.g., "I'm splitting a bill"). Extra context helps the model tailor the answer to practical relevance, not just correctness.

7. Chain-of-Thought Prompting — Instructing the model to reason step by step before answering. This improves accuracy on multi-step problems by making intermediate logic explicit.

8. Self-Consistency Prompting — Asking the model to solve the same problem multiple independent ways and compare results. Agreement across methods increases confidence in the final answer.

9. Tree-of-Thought Prompting — Having the model explore several reasoning branches in parallel, evaluate each, and prune the weak ones. It converges on the most defensible path instead of committing to the first line of reasoning.

10. ReAct Prompting — Interleaving reasoning ("Thought") with concrete actions ("Action") and their results ("Observation"), often using external tools. This lets the model verify intermediate steps rather than reasoning blindly.





Problem : Find the sum of all even numbers between 1 and 50.


1. Zero Shot:
Find the sum of all even numbers between 1 and 50.
Calculate the sum of even integers from 1 to 50.




2. Few Shot:
Example:
Find the sum of even numbers between 1 and 10.
Answer:
Even numbers: 2, 4, 6, 8, 10
Sum = 30


Now solve:
Find the sum of even numbers between 1 and 50.


—


Example:
Odd numbers between 1 and 9 → 1,3,5,7,9 → Sum = 25


Now:
Find the sum of even numbers between 1 and 50.








3. System Prompting

System:
You are a mathematics tutor who explains every step clearly. Give the response in JSON format.

User:
Find the sum of all even numbers between 1 and 50.

System:
You are an exam evaluator. Give a concise answer with formula.

User:
Find the sum of even numbers from 1 to 50.


PS: what is 15% of 80 ?
System: You are a precise math tutor. Always convert the percentage to a decimal first, then multiply and show units.
User: What is 15% of 80 ?


4. Contextual Prompting
        You are helping a school student who just learned arithmetic progressions.


Find the sum of even numbers between 1 and 50.




This problem is part of a coding interview.
Explain the mathematical logic and also provide a Python solution.


Find the sum of even numbers from 1 to 50.






5. Role Prompting

        Act as a mathematics teacher.
Explain step-by-step how to find the sum of even numbers between 1 and 50.




        You are a competitive programming coach.
Solve the problem efficiently and explain the logic.







6. Chain of Thought

Solve the following problem step by step:
Find the sum of all even numbers between 1 and 50.
Explain your reasoning clearly.




Think step by step and show all intermediate calculations.


Find the sum of even numbers from 1 to 50.




"Find the sum of all even numbers between 1 and 50.
To solve this, please think step-by-step:
1. Identify the sequence: Define the first and last numbers in the set and the common difference.
2. Count the terms: Calculate how many numbers are actually in this sequence.
3. Select a method: Choose an appropriate mathematical formula (like the arithmetic series formula).
4. Calculate: Show the intermediate arithmetic steps.
5. Verify: Briefly double-check the logic for any missed numbers."






Self Consistency:


Solve this problem using three different methods of reasoning. After you have all three results, determine which answer is the most consistent and provide that as the final conclusion


Tree of Thoughts:
=================

Role: You are a senior tech architect.

You are solving a complex problem.


1. Generate 3 possible approaches.
2. Evaluate the strengths and weakness of each path.
3. Expand the most optimal approach.
4. If it is not suitable, backtrack and try another path.
5. Present the best final solutions.


{
        "type": "function",
        "function": {
            "name": "get_weather",
            "description": "Get current weather for a city",
            "parameters": {
                "type": "object",
                "properties": {
                    "city": {
                        "type": "string",
                        "description": "Name of the city"
                    }
                },
                "required": ["city"]
            }
        }
    }
