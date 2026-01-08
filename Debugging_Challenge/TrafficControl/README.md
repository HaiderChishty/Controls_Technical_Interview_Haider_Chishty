# Traffic Light Problem (1 hour)

There's a busy traffic intersection outside your building. The roads at the intersection are horizantal street and vertical street. 
You are an engineer with the department of transportation and you're trying to come up with a new traffic light pattern that 
prevents cars from crashing in the intersection but also minimizes traffic jams. You ask a junior engineer to come up with a new 
traffic pattern and simulate the traffic flow at the intersection for two minutes or until 40 cars pass through. They work on it 
but then come to you saying they're stuck and they can't get the simulation to work. The traffic lights are exhibiting erratic 
behavior, crashes aren't reported properly, and their output results of cumulative time waiting look off. They ask you to review 
their code and help them make it work.

Your goal:
- Find all the errors in the code to get the simulation working properly
- Give feedback on how to make the code better next time

You will additionally be assessed on:
- The quality of your code

A few things to note about where the junior engineer is 98% certain there are NOT errors:
- There should be no issues with the 'advanceLane' function or the functions that start with 'draw'

A few other things to note about the simulation:
- Cars waiting to go into the intersection can only move into the intersection if the light is green.
- Cars already in the intersection can move out of the intersection even when the light is red or yellow.
- A crash should occur if a car on horizantal street and a car on vertical street are in the intersection at the same time.
- Cars IN the intersection are denoted with an 'X'. Cars on either side of the intersection are denoted with a '+'. 
  This will make more sense once you try running the program.
- Only one car from each lane can be IN the intersection at once. For example, if two cars are waiting in the eastbound 
  lane to cross the intersection, they cannot both move into the intersection at the same time. The first car in the 
  lane will move into the intersection. Then, the second car will move into the intersection as the first car leaves. 

To build the project, type the following in your bash terminal:
gcc traffic_light_problem.c -o traffic_light_problem

To run the project, type the following in your bash terminal:
./traffic_light_problem.exe

Candidate Action Items:
- Find the errors in the code to make the simulation work as the junior engineer intended
- Make any other improvements to the code as you see fit
- Answer the following questions:
  - What would you tell the junior engineer about ways that they could improve their code in the future? (1-3 sentences)
    - Most of the "errors" were more honest mistakes that happen when dealing with a lot of code/not revisiting (e.g. collision detection using horizontal lanes twice, if statements being accidentally nested, no breaks in switch). I find that these types of errors are unavoidable, but the solution to mitigating them is to not place yourself in this type of position via the structure of your code - as I'll expand on below, a coding structure that uses two nearly identical functions (i.e. horizontal vs vertical lights) invites twice as much areas for error. Beyond the error fixes, I modified timing constraints from G -> Y to avoid erratic behavior (min 5 secs before switch).
  - How else would you change this code to make it better so you can build on it in the future?(1-10 sentences).
    - As mentioned above, I would not include two functions for Vertical vs. Horizontal lights. The state machine needs to switch/be in charge of both lights at the same time to 1: avoid more errors and 2: be more stucturally sound - the lights work together/are dependent on eachother, so this should be implimented in this code as well. I.e., perhaps the same logic step switches one light from R->G at the same point the other switches Y->R (or at some fixed time after - the critical point here is that the same "state"/subsection of the code should cover both these changes as they're inherently related). Similarly, the lights absolutely can't both be G, so the variables should be linked in a way that this can't happen (i.e., within the same state always ensure they're not both green). Other major room for improvement relates to the G->Y logic as a whole: I just enforced a min switch time, but implimenting logic that allows for switching if no one is in the lane would be a simple way to reduce wait times.

Don't forget; we are interested in both your solution and your thought process.

Good Luck!