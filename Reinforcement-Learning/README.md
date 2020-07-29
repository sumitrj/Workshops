# Reinforcement Learning

This provides a brief introduction to reinforcement learning, Markov Decision Process and Q-Learning with example of path planning.

To know more on swarm robotics based applications, visit [ConnectedQ-Multi-agent-Reinforcement-Learning-Algorithm](https://github.com/sumitrj/ConnectedQ-Multi-agent-Reinforcement-Learning-Algorithm)

Happy Learning!

## What is Reinforcement Learning and how is it different from supervised learning?

Reinforcement learning (RL) is an area of machine learning concerned with how software agents ought to take actions in an environment in order to maximize the notion of cumulative reward.

In simple words, we learn to play football by following instructions of coaches and fellow players while we learnt to walk simply by learning to move forward without falling. Former is an example of supervised learning where we learn by seeing the correct responses while the latter is reinforcement learning where we learn by facing penalties(falling) and rewards (moving forward).

## General Applications

Reinforcment Learning is a classic subset of optimization prblems. These span over the vast domains of  game theory, control theory, operations research, information theory, simulation-based optimization, multi-agent systems, swarm intelligence, statistics and genetic algorithms.

## Basic terminology:

It can be often very difficult to understand the terminology associated with new concept. Let's begin by by being empathetic.

You are an agent in an environment.

You perform certain a action which takes you to another state from the present state.

These actions result in either a penalty or a reward.

You decide your next actions based on the penalty or reward that you received.

It is called as a **Markov Decision Process** and can be generalized as:

1. An agent starts from a start state, makes a number of transitions from its current state to a next state based on its choice of action and also the environment the agent is interacting in. 

2. At every step of transition, the agent from a state takes an action, observes a reward from the environment, and then transits to another state. 

3. If at any point of time the agent ends up in one of the terminating states that means there are no further transition possible. This is the condition of completion of an <u> episode. </u>

For maximal reward while transiting states, it is vital to have a notion of the reward which could be obtained in the furture transitions after completion of the current transition, hence providing a metric of the quality of the current transition.

<b> This is achieved by the Value matrix. </b>

By definition, 
<b> V[x] = Quality of transitions from State x. </b>

So by now, you are familiar with intuition of state, action, reward, penalty and value matrix.

Let's start with the most important parameter of these all, 

### Q matrix

Imagine for each state, yoou knew how good the quality of transition to another state was. You'd compare the qualities of all the states and then pich the best one possible.

An agent refers to the Q matrix for deciding it's next action. 
By following the Q-matrix, the agent traverses through a se
This means that this matrix must update as an agent traverses in an environment observing certain penalties and rewards for it's  actions.
The method of updating the Q matrix is called **Q-Learning**.

Let's assume a classic problem to understand how it works. 
An agent travelling in a 2D environment, trying to find the best way to traverse through the points. Obviously, it is a problem tat can be solved by using Kruskal's algorithm and isn't exactly a problem which needs reinforcement learning, but let's start with it owing to your familiarity with it.

Input:

Field Parameters

	Coordinates of Target Points:
	P1 [0] ['x'] 
	P1 [0] ['y']
	P1 [1] ['x'] 
	P1 [1] ['y']
	P1 [2] ['x'] 
	P1 [2] ['y']
	...
	P1 [N-1] ['x'] 
	P1 [N-1] ['y'] 
	
	P1 = [ P1.0, P1.2, P2.2, .... P2.N ]

L = Length of the total Area 
B = Breadth of the total Area

Algorithm Hyperparameters

G = Gamma = Learning Rate
E = Number of Episodes

**State Space:**

This is the set of all states possible. In this case, a state is depicted by location of the agent in the field ata a given time which means the X-Y coordinate. The set of all possible coordinates gives the state space. Hemce, the size of state space becomes L*B.
State : Action : Reward

Let the bot change locations from Li to Lj. This implies that the system has performed an action such that the state of the system changed from Li to Lj.

For each action, the agent receives a penalty as given by the penalty function.

### Penalty Function:

Penalty function can be made as per the problem under consideration and objective functions associated with it. For this case, we define it as follows:

Penalty = mean of distances travelled by each bot where divided by the diagonal length.

    Penalty(L1,L2):
      S = ( (X1 - X2)**2 + (Y1 - Y2) **2 ))**0.5   
      return S/Di # Di = Diagonal Length


As described earlier, 

Q[State,Action] = Quality of the given transition

In our case, Action is basically transition to a different state ( a different L ). Hence the Q matrix has the dimension same as length of State Space L*B.

### Training

Declarations to be done before begining training

AllPoints = {} # Set of Target Points (Set P1 as mentioned in problem 	description section)
Q = Zero Matrix of order L*B
scores = []
policies = []
Functions:

Specially defined functions:

NextState(Visited): 
	
	p = State index selected at random
	next_state = StateSpace[p]
	
	if( isSubset( set(next_state), Visited) ):
		NextState(Visited) 
	else:
		return next_state
Generic functions:

	1. Union(A,B): 
	returns the union of sets A and B

	2. isSubSet(A,B) :
	returns 1 if r is subset of B, returns 0 otherwise

	3. isSuperSet(A,B):
	returns 1 if A is superset of B, returns 0 otherwise
	An episode of training can be described as follows:


**G** or Gamma is a very important parameter. 

While measuring quality of a state and agent should not only know about quality of transition from present state to next state but also from the next state to other states.

While Learning, G is the metric of weightage given to the future transitions.

TrainEpisode():	
	
	p = State index selected at random
	initial_state = StateSpace[p]
	current_state = initial_state 
	Visited = {} # Set of Visited Points
	Visited = Union( Visited, set( current_state ) )
	policy = [] # Sequence of States forming the policy for the considered episode
	EpisodePenalty = 0
		
	while( isSuperSet ( AllPoints, Visited ) ):
	
		next_state = NextState( Visited )
		policy.append(next_state)
		Visited = Union( Visited , set(next_state) )
		EpisodePenalty = EpisodePenalty + Penalty(current_state, next_state)
		Q[current_state][next_state] = Penalty(current_state, next_state) + G*min(Q[next_state])
		current_state = next_state 
		
	scores.append(EpisodePenalty)
	policies.append(policy)


Implementation

Input:

Field Parameters

Coordinates of Target Points:
	P1 [0] ['x'] 
	P1 [0] ['y']
	P1 [1] ['x'] 
	P1 [1] ['y']
	P1 [2] ['x'] 
	P1 [2] ['y']
	...
	P1 [N-1] ['x'] 
	P1 [N-1] ['y'] 
	P1 = [ P1.0, P1.2, P2.2, .... P2.N ]

Location of Bots:
	Starting location of bot L
	L = Length of the total Area 
	B = Breadth of the total Area
	Algorithm Hyperparameters

	G = Gamma = Learning Rate
	E = Number of Episodes

Training:

	for e in range(E):
		TrainEpisode()
Testing

	Initial_State = < As given in the input >
	current_state = Initial_State 
	Visited = {} # Set of Visited Points 
	Visited = Union( Visited, set( current_state ) ) 
	policy = [] # Sequence of States forming the policy for the considered episode
	EpisodePenalty = 0 
	
	while( isSuperSet ( AllPoints, Visited ) ): 
		next_state = NextStatebyQ(current_state) 
		policy.append(next_state) 
		Visited = Union( Visited , set(next_state) ) 
		EpisodePenalty = EpisodePenalty + Penalty(current_state, next_state)
	scores.append(EpisodePenalty) 
	policies.append(policy)

	NextStateByQ(Initial_State,Visited):
		Next_State = Initial_State + 1
		for i in Visited:
			if(Q[Initial_State][Next_State]>Q[Initial_State][i]):
				Next_State = i
		return Next_State


