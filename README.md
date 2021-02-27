# The-AgEvent-theory
A theory to re-phrase or re-describe the Relation of an Agent to the Environment in Reinforcement-Learning(RL).

# Brief Note:
The statements below are for educational purposes only, Which defines the relationship between an Agent and Environment in Reinforcement-Learning(RL) in a more clear point-of-view. That is that how both terms are identical or non-identical to one-another based on their behviour, functionality and infrastructure.

## The need of re-description.
[You can skip this]

![alt text](https://github.com/Sikander-SD/The-AgEvent-theory/blob/images/Basic.png?raw=true)

As the image above is simple, A DNN-model takes input(data) and give output(prediction) and to be more accurate in predictions, The model weights has to be updated timely with a loss function. A loss function in normaly speaking is a function which calculates the difference between the Lable of the data and the Prediction by the model (loss = y - pred). This is quite simple when we are working on a model which is based on Supervised Machine Learning, But when it comes to Unsupervised Machine Learning, we do not have any access or approach to Labels. We only have the input Data wihout Labels.Then in that case we can not calculate the loss in the same way as we do|did in Supervised Machine Leaning.

I am working on a project that is entirely based on Unsupervised Machine|Deep Leaning and i had to find out to calclute the loss for my model to update the weights. The usual methods were not leading to anywhere, Then i decide to learn about Reinforement Learing, That what is it and how does it works?

I went to google and searched for RL. I go through Actor-Critic, DDPG, Q-Learning and "some others which i could not understand much". Then i found that these methods (Actor-critic, DDPG, Q-Learning) are actually using a DNN-model to just get a Value which can be used in loss calculation, And then i dig-in to understand more about how they works line-by-line and i plotted the sturcutures in the images below.

## From the basics to the modifications.
Below are the three images presenting the basic theory of Reinforcement learning.

![alt text](https://github.com/Sikander-SD/The-AgEvent-theory/blob/images/reinforcement%20learning%20Agent%20and%20Environment%20sturcture.png?raw=true)

Image 1: 
  It is the basic concept that all reinforcement learning algorithms follows, That is there is an Agent that acts on the Environment when given a state of the environment to the Agent. And the Environment returns the next state of itself back to the Agent with some reward.
 
![layout](https://user-images.githubusercontent.com/78195281/109388658-6e3ed480-792e-11eb-9e72-ec61f8b5242f.png)

![alt text](https://github.com/Sikander-SD/The-AgEvent-theory/blob/images/comparing%20RL%20architectures.png?raw=true)
![alt text](https://github.com/Sikander-SD/The-AgEvent-theory/blob/images/ditricircle.png?raw=true)
![alt text](https://github.com/Sikander-SD/The-AgEvent-theory/blob/images/chessboard.png?raw=true)
