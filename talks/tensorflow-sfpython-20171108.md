# Tensorflow Talk @ SF Python

Speaker: Adam Fletcher - adam@gyroscope.cc


# Using Python To Create SNES STreetFighter II AIs

Environment (SNES9x) - BizHawk - Environment (Gym) - Agent (Keras-RL)

Python Libraries: Gym from OpenAI, Keras-RL for training the agent


## Gym

Gives you an environment for machine learning - what you are operating on.

Functions: step, reset


### Observation Space 

For Street Fighter is the timer, health, position of character.

The observation space they chose is based on what a human could see.

You get to choose how big your observation space would be.


#### Stepping

??


### Action space - if it gets too big it becomes too hard to do good learning

I think they just decided you can only press one button and one direction at the same time.

A human typically does not press right and left at the same time, so it is not part of our action space.


### Rewards Function

Hardest part of all of this. Tons of naive approaches - did you win?

Damage received vs damage done.

Settled on delta in my health vs opponents health, then maximize that gap.


## Agent (Keras-RL)

Great abstraction for reinforcement learning. Prebuilt agents.

Random agent - chooses something from the action space and tries it, does not care about observation.

How do you know if your stuff is working? Compare it against the random one.

Also has logging and testing for you which is nice.

### Forward

Pass it an observation and say what should I do?

### Backwards

It says 'here are the results' - learn from it!


## Controller

Code wrote to pass all that data back and forth. 

Python3 Socket server with threads - it just worked with the threaded mixin!

Passed json back and forth over a tcp socket.

Imagine a state machine that simulated the emulator in your AI code.

Also with multiple controllers, agents could play each other.

Python socketserver io 450fps on a cloud server. Lua ip 60fps, lua sqlite io 120fps


## Does it work?

After 300 games, it worked!

They ran a final tournament every game.

M. Bison is OP and the AI always wins.  So he got banned.

Sagat won the 2nd tournament.


## Python in AI/ML

Python made things super fast!!

- Gym
- Tensorflow 
- SciPy
- Keras


## One example, when both had very low health, they would back away from each other!!

So they could not see an advantage from fighting when they could not get a big delta in opponent's health versus theirs.  


## The AI is way better than a human

- millisecond reaction time
- way more training can be done, period

