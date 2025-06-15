#MLmodels #ML
## What is HMM?
- Is a finite set of states
- each associated with a probability distribution
- transition among states are governed by set of probabilities called transition sates

A hidden Markov model works with probabilities to predict future events or states.
## Components of MM
- States : warm or cold , high or low ,  R ,G and B. Hidden within the model
- Observation : State has particular outcome or observation based of PD.  On a Hot day Tim has 80 % chance of being happy and 20 % sad.
- Transition : Likely hood of a state transition  . A cold day has 30% chance of being followed by a hot day and 70% of another cold day.

```
States:     Sunny ----> Rainy
              ^          |
              |          v
Observes:  [No Umbrella] [Umbrella]

```
- The system transitions between hidden states
- It emits an observation at each step
- We only see the observation , not the states
## To create HMM we need
- States 
- Observation Distribution
- Transition Distribution
