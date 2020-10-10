# SnakeGeneticAlgorithm

An AI agent for classic game Snake using a genetic algorithm

# How to use

First, you'll want to install the packages 'deap' and 'pygame'. You may adjust the game parameters and some genetic algorithm parameters located near the top of the script. Then, run the script using:

```python
python snake.py
```

# Motivation / Further Work

There are winning strategies for snake that can be easily implemented, and several non-explicit ways of winning the game. Genetic algorithms are a poor choice if you're just looking to win, but it's an interesting application nonetheless. Another imporovement to the algorithm can be made by using a blend between a genetic algorithm and a neural network, but no neural net is used here.

# Genetic Algorithm

## Fitness

The fitness function uses the length of the snake - that is, the number of food pieces collected during the run. Additionally, it's preferred to grow the snake as quickly as possible, so a small penalty for number of moves made is subtracted from the fitness. Because food collection is sparse, we add a bonus using the Manhattan distance from the head of the snake to the food, which is a heuristic representing the minimum number of moves to get to the next food piece.

## Genome

Each allele in the genome represents a single action or move in each of the four directions. In the standard Snake game, the snake cannot move back into itself, so the random generation of alleles does not allow for a move that conflicts with the previous move.

To allow faster convergence toward better individuals, by default, moves that crash into a wall are ignored, and simply removed after the fitness is calculated by playing the game. Then, all moves taken after the invalid action are shifted to the left to avoid overfilling the genome.

## Mutation

Every individual is mutated, as it's the only way an individual can improve. The problem with alleles is that they are dependent on eachother. For example, turning left at a specific time will not always bring you to the same spot - it depends on where the previous actions/alleles have taken you. For that reason, we found it best to only mutate alleles around the time of death.

The idea is that the fate of the snake is decided shortly before it dies by trapping itself. If we change the actions taken before death, we can help the snake escape. As the snake grows larger, more moves may be required to untrap itself, so higher-fitness individual will have more alleles mutated before the action just before death. However, this won't allow the snake to optimize how quickly it can get to its current length.

## Crossover

No crossover is implemented for our algorithm. The reason is that there isn't a good way to combine two individuals since all alleles are completely dependent on one another.
