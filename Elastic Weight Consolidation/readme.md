# Intuition behind elastic weight colsolidation

In the figure below, $\theta^{*}$ are the weights (ie parameters, synaptic strengths) learned by the neural network (NN) to solve old task A, shown as a vector in vector space. ie if this neural network as 100 total weights then this is a 2D representation of $\mathbb{R}^{100}$ space. The blue horizontal arrow shows an example of catastrophic forgetting, whereby $\theta^{*}$ moves out of the region that allows the NN to perform well at task A (grey), and into the center of a region that allows the NN to perform well at task B (cream). The downward green arrow is the update to $\theta^{*}$ regularized by L2 penalty $\alpha (\theta_{i} - \theta_{A , i}^{*})^{2}$ that causes it to move toward the cream region irrespective of the shape of the grey region. The desired update vector is the red arrow that moves the NN weights into a region capable of performing well at both tasks A and B. 

How Elastic Weight Cosolidation Changes Learning New Weights $\theta^{*}$

![alt text](https://raw.githubusercontent.com/clam004/intro_continual_learning/main/files/F1.large.jpg)


EWC encourages movement of weights along the red path by modifying the loss function when re-training a NN that has already been trained to convergence using the loss function for task A, $L_{A}$, which has settled on weights $\theta_{A}$. When re-training the NN on task B using $L_{B}$, we add a term which penalizes changes to weights that are both far from $\theta_{A}$, ie $(\theta_{i} - \theta_{A , i}^{*})^{2}$, and also high in $F_{i}$ which encodes the shape of the grey region.

$$L \left(\right. \theta \left.\right) = L_{B} \left(\right. \theta \left.\right) + \underset{i}{\sum} \frac{\lambda}{2} F_{i} \left(\theta_{i} - \theta_{A , i}^{*}\right)^{2} $$