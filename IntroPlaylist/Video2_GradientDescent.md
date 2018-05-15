# Chapter 2 - *Gradient Descent, how neural networks learn*

*This video continues with the previous handwritten digits example.*

## Intro to Gradient Descent
- We initialize the weights and bias randomly. This gets you a terrible output. 
- You add up the squares of the differences between the predicted value and the actual value to calculate the **cost** of the difference. The cost is small when classifies correctly, but large when it doesn't know what it's doing.
- Consider average cost over 10s of thousands of examples. And you figure out how good/bad the network is.
- The cost function is a layer of complexity on top of the function.
    - Takes in the 13,002 weights and biases and outputs one number (the cost) based on parameters, the training examples.

Instead of thinking of a function with 13,002 inputs, let's first think of a function with one parameter, like a quadratic function.
- We know from calculus that the minimum can be found for simpler functions, but that's hard for super complicated functions.
- A better way is to pick a random starting point, find the "slope" of the function. Go left if slope is positive (go more negative) and vice versa, eventually you get to a local minimum.
- There's no guarantee that local minimum is the global minimum. Local minimums are doable, but global minimums are crazy hard and computationally expensive (why? idk).
- This possible error carries over to the neural network.
- Protip: Keep step size proportional to slope. As slope gets smaller, you step smaller as well since you're getting closer to 0 and you don't want to overshoot.

Consider a function with 2 parameters, C(x, y)
- Think of the input as x-y plane and cost function as height of graph.
- Now think, which direction should I step as to decrease the output of the function most quickly? In otherwords, what is the downhill direction? Think of a ball rolling down that hill.
- Multivariable calculus concepts say that the **gradient** of a function gives you the direction of steepest descent. We want the negative of this. 
- The previous concept we used still applies here, but instead of slope we use gradient. This is called **gradient descent**.
- Eventually, the network starts to look like less than a random choice and more like a decision.
- The algorithm for computing this gradient efficiently is called **backpropagation**.
- Independent of implementation details, the main concept is that **learning is just minimizing a cost function**. 
- A consequence of this is that the cost function must be nice and smooth. This is why artificial neurons have continuous activations instead of binary activations like biological neurons. Also, this helps us figure out which changes to which nodes matter more when minimizing the cost function.

Review
- Network is inputs and outputs to your original problem
- Cost function is on top of this, which takes all the weights and biases and spits out one number of cost.
- Gradient tells us which nudges to weights and biases give us the fastest change to minimize the cost function.

Playing with this is what optimizes your network.

## Analysis of Network
- Remember how we thought that maybe the first hidden layer picks up on edges, and the second hidden layer picks up on loops and straight lines? Turns out, that's not at all what's happening
- In this 13,002-dimensional space, the findings at each layer look almost random, with some consistent output towards the center of the image heatmaps.
- When you feed the network some nonsense data, it'll confidently give you one answer (5!), when in reality, the answer is none of them.
- Basically, it knows how to read numbers, but it doesn't know how to make one from scratch.

## Where to Learn More
From the video description...

> To learn more, I highly recommend the book by Michael Nielsen
http://neuralnetworksanddeeplearning....
The book walks through the code behind the example in these videos, which you can find here: 
https://github.com/mnielsen/neural-ne...

> MNIST database:
http://yann.lecun.com/exdb/mnist/

> Also check out Chris Olah's blog: 
http://colah.github.io/
His post on Neural networks and topology is particular beautiful, but honestly all of the stuff there is great.

> And if you like that, you'll *love* the publications at distill:
https://distill.pub/

> For more videos, Welch Labs also has some great series on machine learning: 
https://youtu.be/i8D90DkCLhI
https://youtu.be/bxe2T-V8XRs

> "But I've already voraciously consumed Nielsen's, Olah's and Welch's works", I hear you say.  Well well, look at you then.  That being the case, I might recommend that you continue on with the book "Deep Learning" by Goodfellow, Bengio, and Courville.

> Thanks to Lisha Li (@lishali88) for her contributions at the end, and for letting me pick her brain so much about the material.  Here are the articles she referenced at the end:
https://arxiv.org/abs/1611.03530
https://arxiv.org/abs/1706.05394
https://arxiv.org/abs/1412.0233

## Amplify Venture Capitalists
Hoping to start AI companies. Reach out to them at 3blue1brown@amplifypartners.com
