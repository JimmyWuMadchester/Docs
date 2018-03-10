# Deep Reinforcement Learning

I started my journey of Deep Reinforcement Learning from [Andrej Karpathy's blog post](http://karpathy.github.io/2016/05/31/rl/).
This note document is writen while I'm reading his post. It should include any additional information I'm getting from other resources 
in the future.

## Resources
* [Richard Sutton's book](http://incompleteideas.net/book/bookdraft2017nov5.pdf)
* [David Silver's course](http://www0.cs.ucl.ac.uk/staff/d.silver/web/Teaching.html)
* [REINFORCEjs](https://cs.stanford.edu/people/karpathy/reinforcejs/)
* [Gym.openai RL benchmarking toolkit](https://gym.openai.com/)
* [A Beginner’s Guide to Recurrent Networks and LSTMs](https://deeplearning4j.org/lstm.html)

## Notes

1. ConvNets
1. Deep Q Learning
1. AlphaGo uses policy gradients with Monte Carlo Tree Search (MCTS)
1. Long Short-Term Memory Units (LSTMs)
1. Policy Gradients (PG), our favorite default choice for attacking RL problems at the moment
1. Note that it is standard to use a stochastic policy, meaning that we only produce a probability of moving UP. Every iteration we will sample from this distribution (i.e. toss a biased coin) to get the actual move. The reason for this will become more clear once we talk about training.
