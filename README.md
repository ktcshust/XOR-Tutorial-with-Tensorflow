The XOR-Problem is a classification problem, where you only have four data points with two features. The training set and the test set are exactly the same in this problem. So the interesting question is only if the model is able to find a decision boundary which classifies all four points correctly
![image](https://user-images.githubusercontent.com/101494254/175780082-2a9f3329-07ee-4596-9399-235bee11826d.png)

Neural Network basics ¶
I think of neural networks as a construction kit for functions. The basic building block - called a "neuron" - is usually visualized like this:
![image](https://user-images.githubusercontent.com/101494254/175780101-13102e91-b75a-45c7-b211-c72287b7dbc2.png)
It gets a variable number of input x0, x1, ..., xn, they get multiplied with weights w0, w1,..., wn, , summed and a function φ is applied to it. The weights is what you want to "fine tune" to make it actually work
In this example, it is only one output and 5 inputs, but it could be any number. The number of inputs and outputs is usually defined by your problem, the intermediate is to allow it to fit more exact to what you need (which comes with some other implications).
Now you have some structure of the function set, you need to find weights which work. This is where backpropagation3 comes into play. The idea is the following: You took functions (φ) which were differentiable and combined them in a way which makes sure the complete function is differentiable. Then you apply an error function (e.g. the euclidean distance of the output to the desired output, Cross-Entropy) which is also differentiable. Meaning you have a completely differentiable function. Now you see the weights as variables and the data as given parameters of a HUGE function. You can differentiate (calculate the gradient) and go from your random weights "a step" in the direction where the error gets lower. This adjusts your weights. Then you repeat this steepest descent step and hopefully end up some time with a good function.
For two weights, this awesome image by Alec Radford visualizes how different algorithms based on gradient descent find a minimum (Source with even more of those):
![image](https://user-images.githubusercontent.com/101494254/175780191-2ea94baa-5bc4-49e0-8e90-cb8a822e9f68.png)
So think of back propagation as a shortsighted hiker trying to find the lowest point on the error surface: He only sees what is directly in front of him. As he makes progress, he adjusts the direction in which he goes

Targets and Error function
First of all, you should think about how your targets look like. For classification problems, one usually takes as many output neurons as one has classes. Then the softmax function is applied.1 The softmax function makes sure that the output of every single neuron is in 
[
0
,
1
]
 and the sum of all outputs is exactly 
1
. This means the output can be interpreted as a probability distribution over all classes.

Now you have to adjust your targets. It is likely that you only have a list of labels, where the 
i
-th element in the list is the label for the 
i
-th element in your feature list 
X
 (or the 
i
-th row in your feature matrix 
X
). But the tools need a target value which fits to the error function. The usual error function for classification problems is cross entropy (CE). When you have a list of 
n
 features 
x
, the target 
t
 and a classifier 
c
l
f
, then you calculate the cross entropy loss for this single sample by:
![image](https://user-images.githubusercontent.com/101494254/175780293-f6682a04-3f36-478f-8397-6f38bf4351c0.png)
