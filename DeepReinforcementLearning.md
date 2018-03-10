# Deep Reinforcement Learning

I started my journey of Deep Reinforcement Learning from [Andrej Karpathy's blog post](http://karpathy.github.io/2016/05/31/rl/).
This note document is writen while I'm reading his post. It should include any additional information I'm getting from other resources 
in the future.

## ToDo

1. Research Machine Learning math tricks. [Shakir's blog](http://blog.shakirm.com/2015/11/machine-learning-trick-of-the-day-5-log-derivative-trick/) has some resources to study but I found the content arranged rather difficult to see.
1. Check out terms: LQR solvers, SLAM system.
1. Study [Andrej's Python code](https://gist.github.com/karpathy/a4166c7fe253700972fcbc77e4ea32c5).
1. Study Cross-entropy method, a simple stochastic hill-climbing "guess and check" approach. And try
[Trust Region Policy Optimization](https://arxiv.org/abs/1502.05477), which almost always works better 
and more consistently than vanilla PG in practice.

## Resources

* [Richard Sutton's book](http://incompleteideas.net/book/bookdraft2017nov5.pdf)
* [David Silver's course](http://www0.cs.ucl.ac.uk/staff/d.silver/web/Teaching.html)
* [REINFORCEjs](https://cs.stanford.edu/people/karpathy/reinforcejs/)
* [Gym.openai RL benchmarking toolkit](https://gym.openai.com/)
* [A Beginner’s Guide to Recurrent Networks and LSTMs](https://deeplearning4j.org/lstm.html)
* [Building Machines That Learn and Think Like People](https://arxiv.org/abs/1604.00289)
* [Gradient Estimation Using Stochastic Computation Graphs](https://arxiv.org/abs/1506.05254)
* [Neural Turing Machines](https://arxiv.org/abs/1410.5401)

## Notes

1. ConvNets
1. Deep Q Learning
1. AlphaGo uses policy gradients with Monte Carlo Tree Search (MCTS)
1. Long Short-Term Memory Units (LSTMs)
1. Policy Gradients (PG), our favorite default choice for attacking RL problems at the moment
1. Note that it is standard to use a stochastic policy, meaning that we only produce a probability of moving UP. Every iteration we will sample from this distribution (i.e. toss a biased coin) to get the actual move. The reason for this will become more clear once we talk about training.
1. [rectified linear unit (ReLU)](https://en.wikipedia.org/wiki/Rectifier_(neural_networks))
1. credit assignment problem: how can we tell what made that happen? Was it something we did just now? Or maybe 76 frames ago? Or maybe it had something to do with frame 10 and then frame 90? And how do we figure out which of the million knobs to change and how, in order to do better in the future?
1. log probability
1. So reinforcement learning is exactly like supervised learning, but on a continuously changing dataset (the episodes), scaled by the advantage, and we only want to do one (or very few) updates based on each sampled dataset.
1. Math behind deriving policy gradients. [notations of likelihood function](https://en.wikipedia.org/wiki/Likelihood_function)
1. Policy Gradients have to actually experience a positive reward, and experience it very often in order to eventually and slowly shift the policy parameters towards repeating moves that give high rewards. With our abstract model, humans can figure out what is likely to give rewards without ever actually experiencing the rewarding or unrewarding transition. I don’t have to actually experience crashing my car into a wall a few hundred times before I slowly start avoiding to do so.
1. The current consensus is that PG works well only in settings where there are a few discrete choices so that one is not hopelessly sampling through huge search spaces.

