# Chapter 1 - *But what **is** a Neural Network?*

*This video covers the structure of a plain, basic (**"multilayer perceptron"**) Neural Net with the classic example of handwritten digits*

**Neural Networks** are inspired by the brain.
- A neuron is a node that holds a number. The network has a node/neuron for each pixel on the 28x28 image. We have 784 pixels.
- The number in the image represents grayscale/alpha value of the pixel. Each value is called its **activation**. Each neuron is "lit up" when its activation is a high number.
- All 784 neurons per pixel makes the input layer.
- The output layer is 10 neurons long (values 0 through 9).
- There are hidden layers in between the input and output layer. 
- The video arbitrarily chooses 16 neurons for 2 hidden layers.
- Activations in one layer determine activations of the next layer.
- This is loosely analogous to neurons in the brain to fire.

## Training
The network has been trained. Give it an image which causes a pattern of activations in each layer and gives a pattern of activation in the output layer. The "brightest" output neuron is the network's "choice" for what the answer is.

## Why the Layers?
Assume 4 layers with 2 hidden layers.
- When a human recognizes digits, we piece together distinctive components. For example, a 9 has a loop and a line. An 8 has two loops. A 4 breaks down into 3 specific lines, etc.
- In a perfect world, we would hope that each neuron in the 3rd layer (right before the output) would have one of these distinctive number-identification features (ex: A loop towards the top). Then, going to the last layer just means learning which components correspond to which number.
- Recognizing a loop also breaks down into sub-problems.
    - You can learn which small edges make up the loop (circle into tangent lines).
    - This might be what the second layer represents, and then it lights up all the neurons associated with the component edges of, say, a loop. Then the neurons with the most light-up pass on to the last layer, which chooses the brightest neuron.
- Processing speech uses a similar separation process to pick out sounds to make syllables and then, finally, words.

## What are these connections actually doing?
- Goal is to have one mechanism that could combine pixels into edges, loops, and other patterns.
- Let's say the hope for one specific neuron in the 2nd layer is to pick up on whether the image has an edge in the top region. What parameters should the network have? What dials and knobs should we be able to tweak so it's expressive enough to capture the right pattern?
- We will assign a numerical **weight** to each connection between each layer. Then we multiply the activation of each neuron with the weight of its specific connection, and compute the weighted sum. 
- But this isn't enough to find out if there's an edge or not; we're basically just adding up the grayscale value of each pixel in that region. What we should do is assign negative weights to areas outside the region so that we bias towards a sharp fall-off from high grayscale to low grayscale, thus creating an edge.
- Then, the sum is largest when the middle pixels are bright but surrounding pixels are dark.
- We want to **normalize** this output--that is, keep it between a simple range, usually between 0 and 1. This is commonly done with functions such as the sigmoid function: 
![sigmoid function](https://latex.codecogs.com/png.latex?\fn_cm&space;\sigma&space;(x)&space;=&space;\frac{1}{1&plus;{e}^{-x}})
- Therefore, the activation of the neuron in the next layer is how positive it is.

## Controlling activation
- What if you want to activate meaningfully, such as when the weighted sum > 10 instead of > 0? Then, we can introduce a **bias** for inactivity. We can simply add a `-10` to the end of the weighted sum to ensure that.
- This was all work for **only one neuron**! Each neuron has its own set of weights and biases for every connection to ensure optimal output.
- Each layer therefore has (28x28x16x16 + 16x10) weights and (16+16+10) biases, meaning 13,002 different parameters in this network.
- **Learning** is therefore finding the optimal combinations of these knobs with a bunch of training data.

All of this information is useful to "debug" your network. It's good to have a "relationship" with your network.

## Mathematics
- The sigmoid function is a little cumbersome to write--it's sigma times the sum of weights*activations plus whatever bias.
- Usually we organize the activations into a vector (1D matrix) and then organize all the weights as a matrix, where each row corresponds to the connections between one layer and a particular neuron in the next layer.
- Then, taking the weighted sum is just one term in the matrix-vector product.
- We then keep the biases as another vector and adding the entire vector to the previous matrix-vector product.
- Lastly, we scalar multiply the result with sigma, and we end up with the following equation:
![sigmoid](https://latex.codecogs.com/gif.latex?%5Cfn_cm%20a%5E%7B%281%29%7D%3D%5Csigma%28Wa%5E%7B%280%29%7D%20&plus;%20b%29)
where `a` represents a neuron, `W` represents the weights matrix, and `b` represents the bias vector.

Writing equations in this linear algebra format helps make code easier too. Consider the following Neural Network class and the `feedforward` function:

```python
class Network(object):
    def __init__(self, *args, **kwargs):
        '''Initialization stuff'''
    
    def feedforward(self, a):
        '''Return the output of the network for an input vector a.'''
        for b, w in zip(self.biases, self.weights):
            a = sigmoid(np.dot(w, a) + b)
        
        return a
```

It's more accurate to think of each neuron as a function that takes the output of the previous layer, converts it to a different layer, and then *feeds it forward* (**feedforward neural network**). In fact, the entire neural network is just a function.
