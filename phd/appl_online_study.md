# Elements for the DESPOT solver 

## Essential

### DSPOMDP class 

#### Deterministic simulative model and related functions

Step function returns a bool value of whether the terminal state has been reached.  Parameters:

* state (class State can be override): Current state of the world
* random_num: Random number in a scenario
* action: Action to be take, ACT_TYPE is a int value
* reward: Reward recieved after taking action from state
* obs: OBS_TYPE is a uint64_t value

```c++
	virtual bool Step(State& state, double random_num, ACT_TYPE action,
		double& reward, OBS_TYPE& obs) const = 0;
```

#### Action

NumActions() returns the number of actions

```c++
	virtual int NumActions() const = 0;
```

#### Functions related to beliefs and starting states

ObsProb function, it returns the observation probability of an observation obs in the condition of current state and the action taken. P(obs|state, action)

```c++
	virtual double ObsProb(OBS_TYPE obs, const State& state,
		ACT_TYPE action) const = 0;
```

Initial Beilief function, it returns the initial belief

```c++
	virtual Belief* InitialBelief(const State* start,
		std::string type = "DEFAULT") const = 0;
```

#### Bound-related functions

GetMaxReward function, it returns the maximum reward.

```c++
	virtual double GetMaxReward() const = 0;
```

GetBestAction function  (Not understand), it returns (a, v), where a is an action with largest minimum reward when it is executed, and v is its minimum reward, that is, a = \max_{a'} \min_{s}R(a', s), and v = \min_{s} R(a, s).

```c++
	virtual ValuedAction GetBestAction() const = 0;
```

ValueAction is a struct defined in the default_policy.h. The DefaultPolicy class can be customized by inheriting.



#### Display

```c++
	virtual void PrintState(const State& state, std::ostream& out = std::cout) const = 0;

```

```c++
	virtual void PrintObs(const State& state, OBS_TYPE obs, std::ostream& out = std::cout) const = 0;
```

```c++
	virtual void PrintAction(ACT_TYPE action, std::ostream& out = std::cout) const = 0;
```

```c++
	virtual void PrintBelief(const Belief& belief, std::ostream& out = std::cout) const = 0;
```

#### Memory management

Allocate function. it allocates a state

```c++
	virtual State* Allocate(int state_id = -1, double weight = 0) const = 0;
```

state_id is one property defined in the State class.

Copy function (Not sure what it is used for)

```c++
	virtual State* Copy(const State* state) const = 0;
```

```c++
	virtual void Free(State* state) const = 0;
```

```c++
	virtual int NumActiveParticles() const = 0;
```

