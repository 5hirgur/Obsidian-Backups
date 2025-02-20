#RRTM 
Presentation by Lance Shi on 05-11-2024

What neural architecture search methods are good for SNNs
What SNNs are good for Image recognition tasks. 

# SNNs

Imitation of real neurons on a deeper level comparing to traditional NNs. 
Each Spiking Neuron transmits a spike to its post connections when its internal state reaches a threshold. Then the internal state is reset
The ability for each neuron to spike independently means that the network can be very expressive for time series data. 

# NAS Neural Architecture Search 

Manual search for neural network architecture can be time consuming and unrealistic for large models. 

NAS:
- Define a search space
- Select a search strategy 
- evlitionalry algorithms, gradient based methods, reinforcement based methods 
- Preformation Estimation 

## Why use NAS for SNNs

SNNs are difficult to train and construct.  Incorporate temporal feedback in the search space. 

