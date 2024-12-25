ข้อ 1
Consider a sequence of n Bernoulli trials with success probabilty p per trial. 
A string of consecutive successes is known as a success run. 
Write a function that returns the counts for runs of length k for each k observed in a dictionary.
----------------------------------------------------------------------------------------------------
from collections import Counter
import numpy as np

def count_runs(lists):
    return Counter(map(len, filter(None, ''.join(map(str, lists)).split('0'))))

# Example usage
lists = [0, 1, 0, 1, 1, 0, 0, 0, 0, 1]
print(count_runs(lists))

# For a random large binary sequence

random_lists = np.random.randint(0, 2, 1000000)
count_runs(random_lists)

ข้อ 2
Continuing from Part 1, what is the probability of observing at least one run of length 5 or more when n=100 and p=0.5?. 
Estimate this from 100,000 simulated experiments. Is this more, less or equally likely than finding runs of length 7 or more when p=0.7 ?
--------------------------------------------------------------------------------------------------------
from collections import Counter
import numpy as np

def count_runs(sequence):
    return Counter(map(len, filter(None, ''.join(map(str, sequence)).split('0'))))

def run_prob(expts, n, k, p):
    return sum(any(r >= k for r in count_runs(np.random.choice([0, 1], n, p=[1-p, p]))) for _ in range(expts)) / expts

# Example usage
print(run_prob(100000, 100, 5, 0.5))  # Expected ~0.80704
print(run_prob(100000, 100, 7, 0.7))  # Expected ~0.94881
