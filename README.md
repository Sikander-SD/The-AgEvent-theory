# The-AgEvent-theory
A theory to re-phrase or re-describe the Relation of an Agent to the Environment in Reinforcement-Learning(RL).
This thoery states that "One's Actions are the States to the other".

# Brief Note:
The statements below are for educational purposes only, Which defines the relationship between an Agent and Environment in Reinforcement-Learning(RL) in a more clear point-of-view. That is that how both terms are identical or non-identical to one-another based on their behaviour, functionality and infrastructure.

## The need of re-description.

![DNN model](https://user-images.githubusercontent.com/78195281/109762634-f1a24380-7c16-11eb-8f72-b82f822f6299.png)


As the image above is simple, A DNN-model takes input(data) and give output(prediction) and to be more accurate in predictions, The model weights has to be updated timely with a loss function. A loss function in normaly speaking is a function which calculates the difference between the Lable of the data and the Prediction by the model (loss = y - pred). This is quite simple when we are working on a model which is based on Supervised Machine Learning, But when it comes to Unsupervised Machine Learning, we do not have any access or approach to Labels. We only have the input Data wihout Labels.Then in that case we can not calculate the loss in the same way as we do|did in Supervised Machine Leaning.

I am working on a project that is entirely based on Unsupervised Machine|Deep Leaning and i had to find out to calclute the loss for my model to update the weights. The usual methods were not leading to anywhere, Then i decide to learn about Reinforement Learing, That what is it and how does it works?

I went to google and searched for RL. I go through Actor-Critic, DDPG, Q-Learning and "some others which i could not understand much". Then i found that these methods (Actor-critic, DDPG, Q-Learning) are actually using a DNN-model to just get a Value which can be used in loss calculation, And then i dig-in to understand more about how they works line-by-line and i plotted the sturcutures in the images below.

## The basic architecture
Below are the three images presenting the same basic theory of Reinforcement-learning in three different ways  for the sake of understanding.

![reinforcement learning Agent and Environment sturcture](https://user-images.githubusercontent.com/78195281/109762702-0bdc2180-7c17-11eb-897b-92ef53382b2c.png)


### Image 1: 
  It is the basic concept that all reinforcement learning algorithms follows, That is there is an Agent that acts on the Environment when given a state of the environment to the Agent. And the Environment returns the next state of itself back to the Agent with some reward. This reward is used to calculate the loss.

### Image 2:
  This is the extended and modified version of the basic concept of Reinforcement Learning algorithm. Or We can say that i made some modification to the basic concept of Reinforcement Learning algorithm based on my needs to calculate loss. That is there is an Agent that acts on the Environment to estimate the future reward in return from the Environment and then the Environment takes that action as a state of the Agent and further acts back to the Agent with an action to estimate its own future reward and then that action of the Environment again becomes a state of the Environment to the Agent. The loss here now is the difference of both estimated future rewards of Agent and Environment.

### Image 3:
  This image is just to show the continues cycle among Agnet and Environment.
  Precisely speaking, The image presents the transitions of
  
  Env_State -> Agent -> Ag_State -> Environment -> Env_State
                 V                      V
           estimated reward      estimated reward

  More detailes are below.

## Comparing the modified architecture with original ones.
The below image shows the difference between Acto-Critic, DDPG and DDPG-Lite(modified version) and why i had to modify to DDPG-Lite.

![comparing RL architectures](https://user-images.githubusercontent.com/78195281/109762737-1b5b6a80-7c17-11eb-8d93-8e4f0269ecd3.png)


### Actor-Critic:
  This architecture is using an Actor which acts on the Environment to estimate the future rewards from the Environment and the Critic is a small model that estimates the future reward for the Actor. The Environmnet then returns its state back to the Actor with actual rewards. The calculation is done as [loss = actual - estimated].
More details can be found on https://keras.io/examples/rl/actor_critic_cartpole.

### DDPG (Deep Deterministic Policy Gradient):
  This architecture is a better version of Actor-Critic concept with not just one but TWO Critic models and also TWO Actor models, that comes out 4 models in total. These 4 models are devided into two parts which is Actor,Critic and Target_Actor,Target_Critic. The process goes like this:
Actor acts on Environment to estimate the future rewards form the Environment and Critic computes the estimated rewards for the Actor and then Environment gives out the rewards and its next state and then that next state is feeded to the Target_Actor which gives out the action to estimate the future rewards, But the twist here is that this Taget_Actor does not act on Environment unlike the Actor model does, Rather the action of the Taget_Actor is used only to estimate the future rewards by input the action to the Taget_Critic model.
So basically, Actor acts on Environment and Environment acts on Target_Actor which further does not act on anything. Both the Critc and Target_Critic models works for Actor and Target_Actor respectively to estimate their future rewards as shown in the image.
More details can be found on https://keras.io/examples/rl/ddpg_pendulum.

### DDPG-Lite (The modified version of DDPG):
  This architecture almost works the same way as the DDPG but this version is using only three model Actor, Critic and Target_Critic and i just removed the Taget_Actor to better fullfil my needs.




![ditricircle](https://user-images.githubusercontent.com/78195281/109762810-3af29300-7c17-11eb-88c9-63e848aa5520.png)
![The AgEvent theory](https://user-images.githubusercontent.com/78195281/109762824-3ded8380-7c17-11eb-855e-deac49faaa65.png)
![The AgEvent theory](https://user-images.githubusercontent.com/78195281/109762883-4e9df980-7c17-11eb-98ed-3040fa41e6ee.png)

