## RLlib Atari Results

Benchmarks of [RLlib](https://rllib.io) algorithms against published results. These benchmarks are a work in progress. For other results to compare against, see [yarlp](https://github.com/btaba/yarlp) and [more plots](https://github.com/openai/baselines-results/blob/master/acktr_ppo_acer_a2c_atari.ipynb) from OpenAI.

#### Ape-X Distributed Prioritized Experience Replay

`rllib train -f atari-apex/apex.yaml`

We compare the performance of the RLlib Ape-X implementation to Async DQN and A3C after 10M time-steps (**40M frames**). Here we use only eight workers per environment in order to run all experiments concurrently on a single machine. Further speedups may be obtained by using more workers:

|env|RLlib Ape-X 8-workers|Mnih et al Async DQN 16-workers|
|---|---|---|
|BeamRider|6134|~6000|
|Breakout|123|~50|
|QBert|15302|~1200|
|SpaceInvaders|686|~600|

Comparing after 1 hour of training:

|env|RLlib Ape-X 8-workers|Mnih et al Async DQN 16-workers|
|---|---|---|
|BeamRider|4873|~1000|
|Breakout|77|~10|
|QBert|4083|~500|
|SpaceInvaders|646|~300|

Ape-X plots:
![apex](/atari-apex/apex.png)

#### IMPALA and A2C

`rllib train -f atari-impala/atari-impala.yaml`

`rllib train -f atari-a2c/atari-a2c.yaml`

RLlib IMPALA and A2C on 10M time-steps (**40M frames**). Results compared to learning curves from [Mnih et al, 2016](https://arxiv.org/pdf/1602.01783.pdf) extracted at 10M time-steps from Figure 3.

|env|RLlib IMPALA 32-workers|RLlib A2C 5-workers|Mnih et al A3C 40M 16-workers|
|---|---|---|---|
|BeamRider|2071|1401|~3000|
|Breakout|385|374|~150|
|QBert|4068|3620|~1000|
|SpaceInvaders|719|692|~600|

IMPALA and A2C vs A3C after 1 hour of training:

|env|RLlib IMPALA 32-workers|RLlib A2C 5-workers|Mnih et al A3C 1h 16-workers|
|---|---|---|---|
|BeamRider|3181|874|~1000|
|Breakout|538|268|~10|
|QBert|10850|1212|~500|
|SpaceInvaders|843|518|~300|

IMPALA plots:
![tensorboard](/atari-impala/atari-impala.png)

A2C plots:
![tensorboard](/atari-a2c/atari-a2c.png)

#### DQN / Rainbow

`rllib train -f atari-dqn/basic-dqn.yaml`
`rllib train -f atari-dqn/duel-ddqn.yaml`
`rllib train -f atari-dqn/dist-dqn.yaml`

RLlib DQN after 10M time-steps (**40M frames**). Note that RLlib evaluation scores include the 1% random actions of epsilon-greedy exploration. You can expect slightly higher rewards when rolling out the policies without any exploration at all.

| env  |  RLlib Basic DQN | RLlib Dueling DDQN | RLlib Distributional DQN  |  Hessel et al. DQN |  Hessel et al. Rainbow |
|---|---|---|---|---|---|
|BeamRider|2869|1910|4447|~2000|~13000|
|Breakout|287|312|410|~150|~300|
|QBert|3921|7968|15780|~4000|~20000|
|SpaceInvaders|650|1001|1025|~500|~2000|

Basic DQN plots:
![tensorboard](/atari-dqn/basic-dqn.png)

Dueling DDQN plots:
![tensorboard](/atari-dqn/dueling-ddqn.png)

Distributional DQN plots:
![tensorboard](/atari-dqn/dist-dqn.png)

#### Proximal Policy Optimization

`rllib train -f atari-ppo/atari-ppo.yaml`

RLlib PPO with 10 workers after 10M and 25M time-steps (**40M/100M frames**). Note that RLlib does not use clip parameter annealing.

|env|RLlib PPO @10M|RLlib PPO @25M|Baselines PPO @10M|
|---|---|---|---|
|BeamRider|2807|4480|~1800|
|Breakout|104|201|~250|
|QBert|11085|14247|~14000|
|SpaceInvaders|671|944|~800|

PPO plots:
![tensorboard](/atari-ppo/atari-ppo.png)
