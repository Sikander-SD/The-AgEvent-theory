# Brief Note:
The statements below defines the relationship between an Agent and Environment in Reinforcement-Learning(RL) in a more clear point-of-view. That is- That how both terms are identical or non-identical to one-another based on their behaviour, functionality and infrastructure.

# The-AgEvent-theory
A theory to re-phrase or re-describe the Relation of an Agent to the Environment in Reinforcement-Learning(RL).
This thoery states that "One's Actions are the States to the other".

![The AgEvent theory](https://user-images.githubusercontent.com/78195281/109762824-3ded8380-7c17-11eb-855e-deac49faaa65.png)


The image above tells everything you need to know about the concept. So, I am not going to explain to too much.

The idea comes from the Chess-board game where player-1 is playing as Agent and player-2 is playing as Environment. Both players are aiming to understand each-other's game by performing the actions against each-other's states of the game. They observe the state which is a cause of the opposite player's last move (action) and then they make their move (an action) of that observed state to predict the next move (estimate the future reward which can be good or bad for the palyer) of the opposite player.
Basiclly, one expects somthing from the other when it performs an action.

The player-1 performs its move based on the state of the game to predict that this move may lead the player-1 to the win.
On the other side, The player-2 sees the move of the player-1 which now is a new state of the game and then the player-2 does the same as player-2; Performes its move based on the state of game to predict that this move may lead the player-2 to the win.

if we image that the player-1 is Agent and player-2 is Environment then you can see that the only difference is the name and the mind(structure), Otherwise they both are doing the same thing to each-ther over and over. Hence "One's Actions are the States to the Other."


## The need of re-description

![DNN model](https://user-images.githubusercontent.com/78195281/109762634-f1a24380-7c16-11eb-8f72-b82f822f6299.png)


As the image above is simple, A DNN-model takes input(data) and gives output(prediction) and, To be more accurate in predictions, The model weights has to be updated timely with a loss function. A loss function in normaly speaking is a function which calculates the difference between the Lable of the data and the Prediction by the model (loss = y - pred). This is quite simple when we are working on a model which is based on Supervised Machine Learning, But when it comes to Unsupervised Machine Learning, we do not have any access or approach to Labels. We only have the input Data wihout Labels. Then in that case we can not calculate the loss in the same way as we do | did in Supervised Machine Leaning.

I am working on a project that is entirely based on Unsupervised Machine | Deep Leaning and i had to find out to calclute the loss for my model to update the weights. The usual methods were not leading me to anywhere close to what i actually want. Then i decide to learn about Reinforement Learing like "What is it?" and "How does it works?" specially "How RL calculates the loss?".

I went to google and searched for the Reinforcement-Learning. I go through Actor-Critic, DDPG, Q-Learning (and some other architectures which i could not understand much). Then i found that these methods (Actor-critic, DDPG, Q-Learning) are actually using a DNN-model to just get a Value which can be used as label in loss calculation, And then i dig-in to understand more about how they work line-by-line and i plotted the sturcutures in the images below.

## The basic architecture
Below are the three images presenting the same basic theory of Reinforcement-learning in three different ways for the sake of understanding.

![reinforcement learning Agent and Environment sturcture](https://user-images.githubusercontent.com/78195281/109762702-0bdc2180-7c17-11eb-897b-92ef53382b2c.png)


### Image 1: 
  It is the basic concept which all the reinforcement learning algorithms follows, That is- There is an Agent which acts on the Environment when given a state of the environment to the Agent and the Environment returns the new state of itself back to the Agent with some reward. This reward is used to calculate the loss.

### Image 2:
  This is the extended and modified version of the basic concept of Reinforcement Learning algorithm. Or We can say that i made some modification to the basic concept of Reinforcement Learning algorithm based on my needs for loss calculation. That is- There is an Agent which acts on the Environment to estimate the future reward in return from the Environment and then the Environment takes that action as a state of the Agent and further acts back to the Agent with an action to estimate its own future reward and then that action of the Environment again becomes a state of the Environment to the Agent. The loss here is now the difference of both estimated future rewards of Agent and Environment.

### Image 3:
  This image is just to show the continues cycle among Agnet and Environment.
  Precisely speaking, The image presents the transitions:
  
    Env_State -> Agent -> Action -> Agent_State -> Environment -> Action -> Env_State -> Agent .....
                   V                                    V                                  V
             estimated reward                     estimated reward                  estimated reward

  More detailes are below.

## Comparing the modified architecture with original ones.
The below image shows the difference between Acto-Critic, DDPG and DDPG-Lite(modified version) and why i had to modify DDPG to DDPG-Lite.

![comparing RL architectures](https://user-images.githubusercontent.com/78195281/109762737-1b5b6a80-7c17-11eb-8d93-8e4f0269ecd3.png)


### Actor-Critic:
  This architecture is using an Actor which acts on the Environment to estimate the future rewards from the Environment and the Critic is a small model that estimates the future reward for the Actor. The Environmnet then returns its state back to the Actor with actual rewards. The calculation is done as [loss = actual - estimated].
  
 I described in a different way than the description given in the link below.
More details can be found on https://keras.io/examples/rl/actor_critic_cartpole.

### DDPG (Deep Deterministic Policy Gradient):
  This architecture is a better version of Actor-Critic concept with not just one but TWO Critic models and also TWO Actor models, that comes out 4 models in total. These 4 models are devided into two parts which is Actor, Critic and Target_Actor, Target_Critic. The process goes like this:
Actor acts on Environment to estimate the future rewards form the Environment and Critic computes the estimated rewards for the Actor and then Environment gives out the rewards and its next state and then that next state is feeded to the Target_Actor which gives out the action to estimate the future rewards, But the twist here is that this Taget_Actor does not act on Environment unlike the Actor model does, Rather the action of the Taget_Actor is used only to estimate the future rewards by input the target_action to the Taget_Critic model.

So basically, Actor acts on Environment and Environment acts on Target_Actor which further does not act on anything. Both the Critc and Target_Critic models works for Actor and Target_Actor respectively to estimate their future rewards as shown in the image.
More details can be found on https://keras.io/examples/rl/ddpg_pendulum.

### DDPG-Lite (The modified version of DDPG):
  This architecture almost works the same way as the DDPG but this version is using only three models- Actor, Critic and Target_Critic. I just removed the Taget_Actor because we do not need the Target_Actor model. The purpose of Target_Actor model is to mimic the Actor model, But My theory "The AgEvent theory" told me that we do not need the Targe_Actor model because we have the Environment just to do the same work.
 
 ## The BiTri-Circle Diagram
  Before we start describing this diagram, I want to tell you that the name "BiTri-Circle" comes from "Bi" means Two and "Tri" means Triangles and the "Circle", That turns out to be "Two Triangles inside a Circle, One of which is upside-down".
  
  The BiTi-Circle diagram is to give you a different point-of-view of the same concept or thoery.
  
  ![ditricircle](https://user-images.githubusercontent.com/78195281/109762810-3af29300-7c17-11eb-88c9-63e848aa5520.png)
  
  
  The diagram is representing the relatioship between state-acton-new_state, Which is clearly seen by the Upside-down big triangle, Whose edges are connecting the terms to each-other. The Flow of the process goes form the state to action to new state to state. The colors are refering the terms agent | actor, environment, critic, state difference, estimated future rewards, state, action and new state.
  
  To the left side of the diagram:
    The state goes through the Agent all the way to the Action and the critic is estimating the future rewards.
  To the right side of the diagram:
    The Action goes through the Environment all the way to the new State and the target-critic is estimating the future rewards.
  To the top side of the diagram:
    The new State of the Environment becomes the State of the Environment and follow the whole process again from the state to the acton and then to  the new-state.
    
   We can go from top-left to down to top-right or the reverse. "Is it possible to go reverse?", YES! That is why the theory states "One's Actions are the States to the other."

# Full image of The-AgEvent-theory ( "One's Actions are the  States to the other." )
![The AgEvent theory](https://user-images.githubusercontent.com/78195281/109762883-4e9df980-7c17-11eb-98ed-3040fa41e6ee.png)

