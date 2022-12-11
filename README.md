# Dining-philosopher

the dining philosophers problem is an example problem often used in concurrent algorithm design to illustrate synchronization issues and techniques for resolving them.
(DEADLOCK)

Five silent philosophers sit at a table around a bowl of spaghetti. A fork is placed between each pair of adjacent philosophers. (An alternative problem formulation uses rice and chopsticks instead of spaghetti and forks.)

Each philosopher must alternately think and eat. However, a philosopher can only eat spaghetti when he has both left and right forks. Each fork can be held by only one philosopher and so a philosopher can use the fork only if it's not being used by another philosopher. After he finishes eating, he needs to put down both forks so they become available to others. A philosopher can grab the fork on his right or the one on his left as they become available, but can't start eating before getting both of them.

Eating is not limited by the amount of spaghetti left: assume an infinite supply.

The problem is how to design a discipline of behavior (a concurrent algorithm) such that each philosopher won't starve; i.e., can forever continue to alternate between eating and thinking assuming that any philosopher cannot know when others may want to eat or think.

Src: http://en.wikipedia.org/wiki/Dining_philosophers_problem See more there.



![IllfatedEnviousAardvark-max-1mb](https://user-images.githubusercontent.com/90010134/206897238-e0b6f869-b805-4549-b252-01d555933cc6.gif)


![ezgif com-gif-maker](https://user-images.githubusercontent.com/90010134/206897923-0c2de1aa-f8d6-47c5-8ede-5e75d7961171.gif)

