# Automata Machine

Given a randomly generated set of rules, an 8-bit initial state, and an 8-bit goal state, write a GA that finds the set of rules that will transform the initial state to the goal state after some amount of passes.

###Instructions
An individual is a set of randomly generated rules based off of a 5-bit truth table. 

Example:

Input | Rule
--- | ---
00000 | 1
00001 | 0
00010 | 3
...   | ...
11110 | 2
11111 | 2

The rules work as follows:


> 0 - replace middle value with a 0

> 1 - replace middle value with a 1

> 2 - delete the middle value

> 3 - replicate the middle value

You will use a 5-bit sliding window to implement the rules on the initial state. It may dramatically shorten run time if you parallelize the sliding window.

###Example: 5-bit Initial State and 3-bit Sliding Window###
Input | Rule
--- | ---
000 | 0
001 | 1
010 | 2
011 | 3
100 | 3
101 | 2
110 | 1
111 | 0

Initial State: 01000

Goal State: 11111

Current State = copy(Initial State)

Current State: 01000

**First Pass**

Next State = copy(Current State)

Next State: 01000

Step | Current State | Sliding Window | Rule | Change to Next State this Pass
--- | --- | --- | --- | ---
0 | 01000 |  |  |  01000 (note this is a copy of Current State)
1 | ***010***00 | 010 | 2 |  0***_***000
2 | 0***100***0 | 100 | 3 | 00***0***00
3 | 01***000*** | 000 | 0 | 000***0***0
4 | ***0***10***00*** | 000 | 0 | 0000***0***
5 | ***01***00***0*** | 001 | 1 | ***1***0000

**During each pass ONLY change Next State - DO NOT CHANGE THE INITIAL/CURRENT STATE**

Update Current State once all passes are completed.

Next State: 10000

Current State = copy(Next State)

Current State: 10000

**End of First Pass**



It may take multiple passes to get to the goal state. Some rules will you get close to the goal state, but never fully reach it.

Population is a JSON file with the desired number(population_size) of individuals. The first and second elements refer to the intial state and goal state respectively.

Running the intialize_population function, generates the JSON file - automata-population.json.
