## covid
# kaggle competition of covid
# Simulation of Virux propagation
The file _markov-generator_ simulates the propagation of a virus within a population with a Markov Chain Model. 
# The assumptions are: 
- each person is a randon variable following 4 possibles states: 
  - *healthy* : initial state of the person
  - *dead* : the person dies from the disease
  - *ill* : the persion is ill
  - *recovered* : the person was recovered from the disease
 - The random variables follows a Markov Chain with a 4 states transition matrix. Depending on the simulation, the transition probabilities can describe severals type of propagation and policies : Examples
  - the *dead* states is an absorbed states. Once a person reaches this state, she can not move to another one
  - *recovered* : If it is an absorbed state, there is no possibility of become ill again.
  - *healthy* : A healthy person can move to the following states : recovered or ill with different propabilities.  
  - *ill* : Only healthy person can reach this state. A person can move to recovered or dead states. 
- each person is independent. This means that the 'contagion' model is excluded.
- The model assumed that all the person have the same caracteristics. But it is easy the include different groups of population such as (old, young, child etc..). For a given group, each person will have the same parameters. The simulation will aggregate each group at the end of the simulation. 

# The next step is to include dependence between persons (individuals)
The effect of the dependence will be to change the transition probabilities within a simulation run. The main effect of the dependence will be reflected in the transition probability from *healthy* to *ill*. 
Each person will have some new _relationship_ properties that bind individuals together. In the simulation, before drawing the random variable, the transition probabilities in the markov chain of each individual will be ajusted as a fonction of their _relationships_ with other individuals. 
The new type of assumptions are : 
- *contagion* will be possible by artificially increasing the transition probability of *healthy* to *ill* for individuals close to an *ill* person.
- *contagion time* will be simulated by fixing the number of simulation steps (or days) where the increase of the transition probability is active.
The need of a thrustable *contagion* model : These transition probability is modeled via a sigmoid function (sigd(n)), to ensure that the probability is always smaller than 1, where n is a proxy for the total number of contacts with ill individuals on its relationships. Then 
 n= sum(a_i) where a_i is a function of the _distance_ to his/her ill relationship : Ex
 - a_i = 1 for *family* relationships
 - a_i = 0.5 for *school* relationships
 - a_i = 0.1 for *friends* relationships
 - a_i = 0.01 for *city* relationships
 
 
