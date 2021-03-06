# Dining philosophers problem.

Solution created by using Web Workers and some fancy CSS3 for displaying the state.

## Philosophers

The philosophers are observable state machines (eat-state and think-state). They also have a property indicating their hunger.

### Eat state

While in the eating state philosophers become fed, reducing hunger by 5 each tick. If hunger reaches zero, they drop their forks and begin to think.

### Think state

While in the thinking state philosophers become hungry, increasing hunger by 1 each tick. Each tick they will try to pick up both forks. If they succeed, they begin to eat. Otherwise they drop any forks they possess and continue to think. This prevents resource-hogging, allowing up to two philosophers to eat at the same time.

Another solution would be to let the philosophers keep any fork they manage to pick up. This would prevent other philosophers from snatching "their" forks, and might reduce the time they spend hungry/thinking. But it would also result in (usually) only one philosopher eating at a time as well as blocking other philosophers who might need the forks more.

## Forks

The forks are a shared resource represented as a simple array. At initialization, each philosophers is assigned two forks, one for the left hand and one for the right. The philosophers request ownership of forks and if successful keeps both forks until they are released. This is all handled by the main thread, which could be considered a resource delegator.
