## Binarized Neural Networks: Training Neural Networks with Weights and Activations Constrained to +1 or 1

**Authors:** Matthieu Courbariaux, Itay Hubara, Daniel Soudry, Ran El-Yaniv, Yoshua Bengio

**Layman's Overview:** The authors talk about a method to train Binarized Neural Networks i.e networks with binary weights and activations. This is so that during the forward pass memory consumption is reduced and power efficiency is increased.

### Crux of the problem

DNNs nowadays are trained on fast and power hungry GPUs. Hence it is a challenge to implement them on low power devices. Memory usage ia another constraint on such devices.

### Aspects of BNN

* Binarization function:
  * Used to transform real valued weights and activations into +1 or -1.
  * Deterministic Binarization function
    * Use a Signum function
  * Stochastic Binarization function
    * +1 some probability p (-1 with (1-p))
    * p is equal to Hard Sigmoid
    * requires hardware to generate random bits
    
* Gradients:
  * real valued gradients with sufficient resolution accumulated into real variable
  * method of training BNN is a variant of Dropout
  
* Gradient Propagation:
  * Derivative of Signum or stochastic function wrt quantities before discretization is zero. Unsuitable for backpropagation.
  * Use **Straight Through Estimator** taking into account the saturation effect.

* Use Signum function to obtain activations for hidden units

* For weights first constrain them to [+1, -1], when using it quantize it using Signum function.

* Shift based Batch Norm and Shift based AdaMax since both the vanilla implementation require many multiplications

* First layer conundrum:
  * First layer is not binarized, hence consider input as a vector of a fixed number of bits along with binary weights both of which are combined according to Algorithm 5 in the paper.

### Conclusion

Advantages:

* Power efficient during forward pass
* reduced memory size and accesses
* multiplications are just converted into XNOR operations
* filter repetitions due to binary nature
* 7x speedup using GPU

Disadvantages:

* Need to save the value of the full precision weights.

### Conclusion

Binary Neural Nets drastically reduce memory size and accesses, and replace most arithmetic operations with bit-wise operations, which might lead to a great increase in power-efficiency.
