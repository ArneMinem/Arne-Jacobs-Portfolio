# PSO-ANN for Concrete Compressive Strength Prediction
`October 2025 to December 2025`

See our full report [here](BIC_Coursework_Report_ESMAN_JACOBS.pdf).

## About the module

This project was carried out as part of the Bio-Inspired Computation module at Heriot-Watt University.

## The team

This was a pair project with Antoine Esman, both of us studying at Heriot-Watt University.

We received a grade of 85% for the project, which was the highest mark in the class.

## The problem

Predicting the compressive strength of concrete from its mix design is a nonlinear regression problem, well suited to an Artificial Neural Network. Rather than training the network with a standard gradient-based method, we set ourselves the challenge of optimising its weights using Particle Swarm Optimisation (PSO), a bio-inspired, derivative-free approach, and studying how PSO's many hyperparameters (inertia, cognitive and social coefficients, informant strategies, swarm size, velocity limits) actually affect training performance.

## What we built

We implemented both the ANN and the PSO algorithm from scratch. The neural network is a modular `Sequential` class built from stackable `Linear` and `Activation` layers, which let us freely experiment with different topologies. The PSO algorithm treats each particle's position as a vector of the network's weights and biases, evaluating fitness by feeding that vector straight back through the network.

To search for good PSO configurations without doing it all by hand, we added a Genetic Algorithm that evolves PSO hyperparameters, evaluating each candidate configuration by running it multiple times to avoid lucky results. Since GA runs took days to complete, we built a small Streamlit web interface to launch and monitor training remotely, backed by a database to store results. We also visualised how the swarm converges over time by projecting particle positions down to two dimensions with PCA, animating the process across epochs.

## Our results

Working from a literature-informed baseline, we found that a two-hidden-layer topology of `[8, 4]` neurons gave the best trade-off between training time and accuracy, consistent with the common recommendation to size hidden layers between the input and output dimensions. Larger swarm sizes reliably improved accuracy, but only when paired with enough epochs to let the swarm converge, up to a point of diminishing returns. Acceleration coefficients proved harder to pin down: while our GA's inertia value matched what we found through manual testing, its cognitive, social, and global-best weights did not fully hold up under closer, repeated experimentation, which itself became an interesting finding about the reliability of GA-tuned hyperparameters. The number of informants turned out to behave almost chaotically, which we believe explains why our GA consistently favoured very low social weights.

## My contribution

Antoine and I worked side by side on the core of this project, sitting down together to hand-code both the ANN and the PSO algorithm so that we each fully understood the whole codebase rather than splitting it into disconnected parts. This shared foundation made the rest of the project move much faster, since we could both debug, extend, and reason about any part of the system.

From there, we jointly designed and ran the full experimental campaign: testing network topologies, swarm sizes and epoch counts, acceleration coefficients, jump size, and informant strategies, and interpreting the (sometimes contradictory) results together. We also built the Genetic Algorithm layer and the Streamlit web interface, using ChatGPT as a tool to accelerate implementation on components that weren't the core focus of the coursework, while keeping the research questions, methodology, and analysis our own.

## Conclusion

Building an ANN and a PSO optimiser entirely from scratch was demanding but genuinely clarified how derivative-free optimisation behaves differently from backpropagation, particularly around multiple local minima and the absence of vanishing gradients. Just as valuable was learning to be sceptical of our own automated tuning: several of our GA's "optimal" hyperparameters didn't reproduce well under closer scrutiny, which taught us a lot about the reliability (and limits) of evolutionary hyperparameter search.

Development of:

* Knowledge: Particle Swarm Optimisation, Genetic Algorithms, neural network design and hyperparameter tuning
* Skills: Python, object-oriented design, Streamlit, data visualisation, dimensionality reduction (PCA/UMAP/t-SNE)
* Competencies: problem-solving, experimental design, critical analysis, pair programming, time management