# Neural Networks Transcript

## How to use this file
This file contains only the transcript content from the videos.  
Answer questions using only this transcript. Do not use outside knowledge.  
If the answer is not covered here, say that it is not covered.

---

## Chapter 1: What is a neural network?

But what is a neural network?| Deep learning chapter 1.\
This is a 3.\
It's sloppily written and rendered at an extremely low resolution of 28x28 pixels,\
but your brain has no trouble recognizing it as a 3.\
And I want you to take a moment to appreciate how\
crazy it is that brains can do this so effortlessly.\
I mean, this, this and this are also recognizable as 3s,\
even though the specific values of each pixel is very different from one\
image to the next.\
The particular light-sensitive cells in your eye that are firing when you\
see this 3 are very different from the ones firing when you see this 3.\
But something in that crazy-smart visual cortex of yours resolves these as representing\
the same idea, while at the same time recognizing other images as their own distinct\
ideas.\
But if I told you, hey, sit down and write for me a program that takes in a grid of\
28x28 pixels like this and outputs a single number between 0 and 10,\
telling you what it thinks the digit is, well the task goes from comically trivial to\
dauntingly difficult.\
Series preview\
Unless you've been living under a rock, I think I hardly need to motivate the relevance\
and importance of machine learning and neural networks to the present and to the future.\
But what I want to do here is show you what a neural network actually is,\
assuming no background, and to help visualize what it's doing,\
not as a buzzword but as a piece of math.\
My hope is that you come away feeling like the structure itself is motivated,\
and to feel like you know what it means when you read,\
or you hear about a neural network quote-unquote learning.\
This video is just going to be devoted to the structure component of that,\
and the following one is going to tackle learning.\
What we're going to do is put together a neural\
network that can learn to recognize handwritten digits.\
This is a somewhat classic example for introducing the topic,\
and I'm happy to stick with the status quo here,\
because at the end of the two videos I want to point you to a couple good\
resources where you can learn more, and where you can download the code that\
does this and play with it on your own computer.\
There are many many variants of neural networks,\
and in recent years there's been sort of a boom in research towards these variants,\
but in these two introductory videos you and I are just going to look at the simplest\
plain vanilla form with no added frills.\
This is kind of a necessary prerequisite for understanding any of the more powerful\
modern variants, and trust me it still has plenty of complexity for us to wrap our minds\
around.\
But even in this simplest form it can learn to recognize handwritten digits,\
which is a pretty cool thing for a computer to be able to do.\
And at the same time you'll see how it does fall\
short of a couple hopes that we might have for it.\
What are neurons?\
As the name suggests neural networks are inspired by the brain, but let's break that down.\
What are the neurons, and in what sense are they linked together?\
Right now when I say neuron all I want you to think about is a thing that holds a number,\
specifically a number between 0 and 1.\
It's really not more than that.\
For example the network starts with a bunch of neurons corresponding to\
each of the 28x28 pixels of the input image, which is 784 neurons in total.\
Each one of these holds a number that represents the grayscale value of the\
corresponding pixel, ranging from 0 for black pixels up to 1 for white pixels.\
This number inside the neuron is called its activation,\
and the image you might have in mind here is that each neuron is lit up when its\
activation is a high number.\
Introducing layers\
So all of these 784 neurons make up the first layer of our network.\
Now jumping over to the last layer, this has 10 neurons,\
each representing one of the digits.\
The activation in these neurons, again some number that's between 0 and 1,\
represents how much the system thinks that a given image corresponds with a given digit.\
There's also a couple layers in between called the hidden layers,\
which for the time being should just be a giant question mark for\
how on earth this process of recognizing digits is going to be handled.\
In this network I chose two hidden layers, each one with 16 neurons,\
and admittedly that's kind of an arbitrary choice.\
To be honest I chose two layers based on how I want to motivate the structure in\
just a moment, and 16, well that was just a nice number to fit on the screen.\
In practice there is a lot of room for experiment with a specific structure here.\
The way the network operates, activations in one\
layer determine the activations of the next layer.\
And of course the heart of the network as an information processing mechanism comes down\
to exactly how those activations from one layer bring about activations in the next\
layer.\
It's meant to be loosely analogous to how in biological networks of neurons,\
some groups of neurons firing cause certain others to fire.\
Now the network I'm showing here has already been trained to recognize digits,\
and let me show you what I mean by that.\
It means if you feed in an image, lighting up all 784 neurons of the input layer\
according to the brightness of each pixel in the image,\
that pattern of activations causes some very specific pattern in the next layer\
which causes some pattern in the one after it,\
which finally gives some pattern in the output layer.\
And the brightest neuron of that output layer is the network's choice,\
so to speak, for what digit this image represents.\
Why layers?\
And before jumping into the math for how one layer influences the next,\
or how training works, let's just talk about why it's even reasonable\
to expect a layered structure like this to behave intelligently.\
What are we expecting here?\
What is the best hope for what those middle layers might be doing?\
Well, when you or I recognize digits, we piece together various components.\
A 9 has a loop up top and a line on the right.\
An 8 also has a loop up top, but it's paired with another loop down low.\
A 4 basically breaks down into three specific lines, and things like that.\
Now in a perfect world, we might hope that each neuron in the second\
to last layer corresponds with one of these subcomponents,\
that anytime you feed in an image with, say, a loop up top,\
like a 9 or an 8, there's some specific neuron whose activation is\
going to be close to 1.\
And I don't mean this specific loop of pixels,\
the hope would be that any generally loopy pattern towards the top sets off this neuron.\
That way, going from the third layer to the last one just requires\
learning which combination of subcomponents corresponds to which digits.\
Of course, that just kicks the problem down the road,\
because how would you recognize these subcomponents,\
or even learn what the right subcomponents should be?\
And I still haven't even talked about how one layer influences the next,\
but run with me on this one for a moment.\
Recognizing a loop can also break down into subproblems.\
One reasonable way to do this would be to first\
recognize the various little edges that make it up.\
Similarly, a long line, like the kind you might see in the digits 1 or 4 or 7,\
is really just a long edge, or maybe you think of it as a certain pattern of several\
smaller edges.\
So maybe our hope is that each neuron in the second layer of\
the network corresponds with the various relevant little edges.\
Maybe when an image like this one comes in, it lights up all of the\
neurons associated with around 8 to 10 specific little edges,\
which in turn lights up the neurons associated with the upper loop\
and a long vertical line, and those light up the neuron associated with a 9.\
Whether or not this is what our final network actually does is another question,\
one that I'll come back to once we see how to train the network,\
but this is a hope that we might have, a sort of goal with the layered structure\
like this.\
Moreover, you can imagine how being able to detect edges and patterns\
like this would be really useful for other image recognition tasks.\
And even beyond image recognition, there are all sorts of intelligent\
things you might want to do that break down into layers of abstraction.\
Parsing speech, for example, involves taking raw audio and picking out distinct sounds,\
which combine to make certain syllables, which combine to form words,\
which combine to make up phrases and more abstract thoughts, etc.\
But getting back to how any of this actually works,\
picture yourself right now designing how exactly the activations in one layer might\
determine the activations in the next.\
The goal is to have some mechanism that could conceivably combine pixels into edges,\
or edges into patterns, or patterns into digits.\
Edge detection example\
And to zoom in on one very specific example, let's say the hope\
is for one particular neuron in the second layer to pick up\
on whether or not the image has an edge in this region here.\
The question at hand is what parameters should the network have?\
What dials and knobs should you be able to tweak so that it's expressive\
enough to potentially capture this pattern, or any other pixel pattern,\
or the pattern that several edges can make a loop, and other such things?\
Well, what we'll do is assign a weight to each one of the\
connections between our neuron and the neurons from the first layer.\
These weights are just numbers.\
Then take all of those activations from the first layer\
and compute their weighted sum according to these weights.\
I find it helpful to think of these weights as being organized into a\
little grid of their own, and I'm going to use green pixels to indicate\
positive weights, and red pixels to indicate negative weights,\
where the brightness of that pixel is some loose depiction of the weight's value.\
Now if we made the weights associated with almost all of the pixels zero\
except for some positive weights in this region that we care about,\
then taking the weighted sum of all the pixel values really just amounts\
to adding up the values of the pixel just in the region that we care about.\
And if you really wanted to pick up on whether there's an edge here,\
what you might do is have some negative weights associated with the surrounding pixels.\
Then the sum is largest when those middle pixels\
are bright but the surrounding pixels are darker.\
When you compute a weighted sum like this, you might come out with any number,\
but for this network what we want is for activations to be some value between 0 and 1.\
So a common thing to do is to pump this weighted sum into some function\
that squishes the real number line into the range between 0 and 1.\
And a common function that does this is called the sigmoid function,\
also known as a logistic curve.\
Basically very negative inputs end up close to 0, positive inputs end up close to 1,\
and it just steadily increases around the input 0.\
So the activation of the neuron here is basically a\
measure of how positive the relevant weighted sum is.\
But maybe it's not that you want the neuron to\
light up when the weighted sum is bigger than 0.\
Maybe you only want it to be active when the sum is bigger than say 10.\
That is, you want some bias for it to be inactive.\
What we'll do then is just add in some other number like negative 10 to this\
weighted sum before plugging it through the sigmoid squishification function.\
That additional number is called the bias.\
So the weights tell you what pixel pattern this neuron in the second\
layer is picking up on, and the bias tells you how high the weighted\
sum needs to be before the neuron starts getting meaningfully active.\
Counting weights and biases\
And that is just one neuron.\
Every other neuron in this layer is going to be connected to\
all 784 pixel neurons from the first layer, and each one of\
those 784 connections has its own weight associated with it.\
Also, each one has some bias, some other number that you add\
on to the weighted sum before squishing it with the sigmoid.\
And that's a lot to think about!\
With this hidden layer of 16 neurons, that's a total of 784 times 16 weights,\
along with 16 biases.\
And all of that is just the connections from the first layer to the second.\
The connections between the other layers also have\
a bunch of weights and biases associated with them.\
All said and done, this network has almost exactly 13,000 total weights and biases.\
13,000 knobs and dials that can be tweaked and turned\
to make this network behave in different ways.\
How learning relates\
So when we talk about learning, what that's referring to is\
getting the computer to find a valid setting for all of these\
many many numbers so that it'll actually solve the problem at hand.\
One thought experiment that is at once fun and kind of horrifying is to imagine sitting\
down and setting all of these weights and biases by hand,\
purposefully tweaking the numbers so that the second layer picks up on edges,\
the third layer picks up on patterns, etc.\
I personally find this satisfying rather than just treating the network as a total black\
box, because when the network doesn't perform the way you anticipate,\
if you've built up a little bit of a relationship with what those weights and biases\
actually mean, you have a starting place for experimenting with how to change the\
structure to improve.\
Or when the network does work but not for the reasons you might expect,\
digging into what the weights and biases are doing is a good way to challenge\
your assumptions and really expose the full space of possible solutions.\
Notation and linear algebra\
By the way, the actual function here is a little cumbersome to write down,\
don't you think?\
So let me show you a more notationally compact way that these connections are represented.\
This is how you'd see it if you choose to read up more about neural networks.\
Organize all of the activations from one layer into a column as a vector.\
Then organize all of the weights as a matrix, where each row of that matrix corresponds\
to the connections between one layer and a particular neuron in the next layer.\
What that means is that taking the weighted sum of the activations in\
the first layer according to these weights corresponds to one of the\
terms in the matrix vector product of everything we have on the left here.\
By the way, so much of machine learning just comes down to having a good\
grasp of linear algebra, so for any of you who want a nice visual\
understanding for matrices and what matrix vector multiplication means,\
take a look at the series I did on linear algebra, especially chapter 3.\
Back to our expression, instead of talking about adding the bias to each one of\
these values independently, we represent it by organizing all those biases into\
a vector, and adding the entire vector to the previous matrix vector product.\
Then as a final step, I'll wrap a sigmoid around the outside here,\
and what that's supposed to represent is that you're going to apply the\
sigmoid function to each specific component of the resulting vector inside.\
So once you write down this weight matrix and these vectors as their own symbols,\
you can communicate the full transition of activations from one layer to the next in an\
extremely tight and neat little expression, and this makes the relevant code both a lot\
simpler and a lot faster, since many libraries optimize the heck out of matrix\
multiplication.\
Recap\
Remember how earlier I said these neurons are simply things that hold numbers?\
Well of course the specific numbers that they hold depends on the image you feed in,\
so it's actually more accurate to think of each neuron as a function,\
one that takes in the outputs of all the neurons in the previous layer and spits out a\
number between 0 and 1.\
Really the entire network is just a function, one that takes in\
784 numbers as an input and spits out 10 numbers as an output.\
It's an absurdly complicated function, one that involves 13,000 parameters\
in the forms of these weights and biases that pick up on certain patterns,\
and which involves iterating many matrix vector products and the sigmoid\
squishification function, but it's just a function nonetheless.\
And in a way it's kind of reassuring that it looks complicated.\
I mean if it were any simpler, what hope would we have\
that it could take on the challenge of recognizing digits?\
And how does it take on that challenge?\
How does this network learn the appropriate weights and biases just by looking at data?\
Well that's what I'll show in the next video, and I'll also dig a little\
more into what this particular network we're seeing is really doing.\
Some final words\
Now is the point I suppose I should say subscribe to stay notified\
about when that video or any new videos come out,\
but realistically most of you don't actually receive notifications from YouTube, do you?\
Maybe more honestly I should say subscribe so that the neural networks\
that underlie YouTube's recommendation algorithm are primed to believe\
that you want to see content from this channel get recommended to you.\
Anyway, stay posted for more.\
Thank you very much to everyone supporting these videos on Patreon.\
I've been a little slow to progress in the probability series this summer,\
but I'm jumping back into it after this project,\
so patrons you can look out for updates there.\
ReLU vs Sigmoid\
To close things off here I have with me Lisha Li who did her PhD work on the\
theoretical side of deep learning and who currently works at a venture capital\
firm called Amplify Partners who kindly provided some of the funding for this video.\
So Lisha one thing I think we should quickly bring up is this sigmoid function.\
As I understand it early networks use this to squish the relevant weighted\
sum into that interval between zero and one, you know kind of motivated\
by this biological analogy of neurons either being inactive or active.\
Exactly. But relatively few modern networks actually use sigmoid anymore.\
Yeah. It's kind of old school right?\
Yeah or rather ReLU seems to be much easier to train.\
And ReLU, ReLU stands for rectified linear unit?\
Yes it's this kind of function where you're just taking a max of zero\
and a where a is given by what you were explaining in the video and\
what this was sort of motivated from I think was a partially by a\
biological analogy with how neurons would either be activated or not.\
And so if it passes a certain threshold it would be the identity function but if it did\
not then it would just not be activated so it'd be zero so it's kind of a simplification.\
Using sigmoids didn't help training or it was very difficult to\
train at some point and people just tried ReLU and it happened\
to work very well for these incredibly deep neural networks.\
All right thank you Lisha.\

### Key ideas
- A neuron holds a number between 0 and 1.
- The input layer corresponds to the 28x28 pixels.
- Hidden layers help transform inputs into useful features.
- The output layer represents the predicted digit.

---

## Chapter 2: Gradient descent

this is the second video: Last video I laid out the structure of a neural network.\
I'll give a quick recap here so that it's fresh in our minds,\
and then I have two main goals for this video.\
The first is to introduce the idea of gradient descent,\
which underlies not only how neural networks learn,\
but how a lot of other machine learning works as well.\
Then after that we'll dig in a little more into how this particular network performs,\
and what those hidden layers of neurons end up looking for.\
As a reminder, our goal here is the classic example of handwritten digit recognition,\
Recap\
the hello world of neural networks.\
These digits are rendered on a 28x28 pixel grid,\
each pixel with some grayscale value between 0 and 1.\
Those are what determine the activations of 784 neurons in the input layer of the network.\
And then the activation for each neuron in the following layers is based on a weighted\
sum of all the activations in the previous layer, plus some special number called a bias.\
Then you compose that sum with some other function,\
like the sigmoid squishification, or a relu, the way I walked through last video.\
In total, given the somewhat arbitrary choice of two hidden layers with 16 neurons each,\
the network has about 13,000 weights and biases that we can adjust,\
and it's these values that determine what exactly the network actually does.\
Then what we mean when we say that this network classifies a given digit is that\
the brightest of those 10 neurons in the final layer corresponds to that digit.\
And remember, the motivation we had in mind here for the layered structure\
was that maybe the second layer could pick up on the edges,\
and the third layer might pick up on patterns like loops and lines,\
and the last one could just piece together those patterns to recognize digits.\
Using training data\
So here, we learn how the network learns.\
What we want is an algorithm where you can show this network a whole bunch of\
training data, which comes in the form of a bunch of different images of handwritten\
digits, along with labels for what they're supposed to be,\
and it'll adjust those 13,000 weights and biases so as to improve its performance\
on the training data.\
Hopefully, this layered structure will mean that what it\
learns generalizes to images beyond that training data.\
The way we test that is that after you train the network,\
you show it more labeled data that it's never seen before,\
and you see how accurately it classifies those new images.\
Fortunately for us, and what makes this such a common example to start with,\
is that the good people behind the MNIST database have put together a collection of tens\
of thousands of handwritten digit images, each one labeled with the numbers they're\
supposed to be.\
And as provocative as it is to describe a machine as learning,\
once you see how it works, it feels a lot less like some crazy sci-fi premise,\
and a lot more like a calculus exercise.\
I mean, basically it comes down to finding the minimum of a certain function.\
Cost functions\
Remember, conceptually, we're thinking of each neuron as being connected to all\
the neurons in the previous layer, and the weights in the weighted sum defining\
its activation are kind of like the strengths of those connections,\
and the bias is some indication of whether that neuron tends to be active or inactive.\
And to start things off, we're just going to initialize\
all of those weights and biases totally randomly.\
Needless to say, this network is going to perform pretty horribly on\
a given training example, since it's just doing something random.\
For example, you feed in this image of a 3, and the output layer just looks like a mess.\
So what you do is define a cost function, a way of telling the computer,\
no, bad computer, that output should have activations which are 0 for most neurons,\
but 1 for this neuron, what you gave me is utter trash.\
To say that a little more mathematically, you add up the squares of the differences\
between each of those trash output activations and the value you want them to have,\
and this is what we'll call the cost of a single training example.\
Notice this sum is small when the network confidently classifies the image correctly,\
but it's large when the network seems like it doesn't know what it's doing.\
So then what you do is consider the average cost over all of\
the tens of thousands of training examples at your disposal.\
This average cost is our measure for how lousy the network is,\
and how bad the computer should feel.\
And that's a complicated thing.\
Remember how the network itself was basically a function,\
one that takes in 784 numbers as inputs, the pixel values,\
and spits out 10 numbers as its output, and in a sense it's parameterized\
by all these weights and biases?\
Well the cost function is a layer of complexity on top of that.\
It takes as its input those 13,000 or so weights and biases,\
and spits out a single number describing how bad those weights and biases are,\
and the way it's defined depends on the network's behavior over all the tens of\
thousands of pieces of training data.\
That's a lot to think about.\
But just telling the computer what a crappy job it's doing isn't very helpful.\
You want to tell it how to change those weights and biases so that it gets better.\
To make it easier, rather than struggling to imagine a function with 13,000 inputs,\
just imagine a simple function that has one number as an input and one number as an\
output.\
How do you find an input that minimizes the value of this function?\
Calculus students will know that you can sometimes figure out that minimum explicitly,\
but that's not always feasible for really complicated functions,\
certainly not in the 13,000 input version of this situation for our crazy complicated\
neural network cost function.\
A more flexible tactic is to start at any input,\
and figure out which direction you should step to make that output lower.\
Specifically, if you can figure out the slope of the function where you are,\
then shift to the left if that slope is positive,\
and shift the input to the right if that slope is negative.\
If you do this repeatedly, at each point checking the new slope and taking the\
appropriate step, you're going to approach some local minimum of the function.\
The image you might have in mind here is a ball rolling down a hill.\
Notice, even for this really simplified single input function,\
there are many possible valleys that you might land in,\
depending on which random input you start at,\
and there's no guarantee that the local minimum you land in is going to\
be the smallest possible value of the cost function.\
That will carry over to our neural network case as well.\
And I also want you to notice how if you make your step sizes proportional to the slope,\
then when the slope is flattening out towards the minimum,\
your steps get smaller and smaller, and that kind of helps you from overshooting.\
Gradient descent\
Bumping up the complexity a bit, imagine instead\
a function with two inputs and one output.\
You might think of the input space as the xy-plane,\
and the cost function as being graphed as a surface above it.\
Now instead of asking about the slope of the function,\
you have to ask which direction you should step in this input\
space so as to decrease the output of the function most quickly.\
In other words, what's the downhill direction?\
Again, it's helpful to think of a ball rolling down that hill.\
Those of you familiar with multivariable calculus will know that the\
gradient of a function gives you the direction of steepest ascent,\
which direction should you step to increase the function most quickly.\
Naturally enough, taking the negative of that gradient gives you\
the direction to step that decreases the function most quickly.\
Even more than that, the length of this gradient vector is\
an indication for just how steep that steepest slope is.\
If you're unfamiliar with multivariable calculus and want to learn more,\
check out some of the work I did for Khan Academy on the topic.\
Honestly though, all that matters for you and me right now is that\
in principle there exists a way to compute this vector,\
this vector that tells you what the downhill direction is and how steep it is.\
You'll be okay if that's all you know and you're not rock solid on the details.\
Cause If you can get that, the algorithm for minimizing the function is to compute this\
gradient direction, then take a small step downhill, and repeat that over and over.\
It's the same basic idea for a function that has 13,000 inputs instead of 2 inputs.\
Imagine organizing all 13,000 weights and biases\
of our network into a giant column vector.\
The negative gradient of the cost function is just a vector,\
it's some direction inside this insanely huge input space that tells you which\
nudges to all of those numbers is going to cause the most rapid decrease to\
the cost function.\
And of course, with our specially designed cost function,\
changing the weights and biases to decrease it means making the\
output of the network on each piece of training data look less like\
a random array of 10 values, and more like an actual decision we want it to make.\
It's important to remember, this cost function involves an average over all of the\
training data, so if you minimize it, it means it's a better performance on all of those\
samples.\
The algorithm for computing this gradient efficiently,\
which is effectively the heart of how a neural network learns,\
is called backpropagation, and it's what I'm going to be talking about next video.\
There, I really want to take the time to walk through what exactly happens to\
each weight and bias for a given piece of training data,\
trying to give an intuitive feel for what's happening beyond the pile of relevant\
calculus and formulas.\
Right here, right now, the main thing I want you to know,\
independent of implementation details, is that what we mean when we\
talk about a network learning is that it's just minimizing a cost function.\
And notice, one consequence of that is that it's important for this cost function to have\
a nice smooth output, so that we can find a local minimum by taking little steps\
downhill.\
This is why, by the way, artificial neurons have continuously ranging activations,\
rather than simply being active or inactive in a binary way,\
the way biological neurons are.\
This process of repeatedly nudging an input of a function by some\
multiple of the negative gradient is called gradient descent.\
It's a way to converge towards some local minimum of a cost function,\
basically a valley in this graph.\
I'm still showing the picture of a function with two inputs, of course,\
because nudges in a 13,000 dimensional input space are a little hard to\
wrap your mind around, but there is a nice non-spatial way to think about this.\
Each component of the negative gradient tells us two things.\
The sign, of course, tells us whether the corresponding\
component of the input vector should be nudged up or down.\
But importantly, the relative magnitudes of all these\
components kind of tells you which changes matter more.\
You see, in our network, an adjustment to one of the weights might have a much\
greater impact on the cost function than the adjustment to some other weight.\
Some of these connections just matter more for our training data.\
More on gradient vectors\
So a way you can think about this gradient vector of our mind-warpingly massive\
cost function is that it encodes the relative importance of each weight and bias,\
that is, which of these changes is going to carry the most bang for your buck.\
This really is just another way of thinking about direction.\
To take a simpler example, if you have some function with two variables as an input,\
and you compute that its gradient at some particular point comes out as 3,1,\
then on the one hand you can interpret that as saying that when you're\
standing at that input, moving along this direction increases the function most quickly,\
that when you graph the function above the plane of input points,\
that vector is what's giving you the straight uphill direction.\
But another way to read that is to say that changes to this first variable have 3\
times the importance as changes to the second variable,\
that at least in the neighborhood of the relevant input,\
nudging the x-value carries a lot more bang for your buck.\
Gradient descent recap\
Let's zoom out and sum up where we are so far.\
The network itself is this function with 784 inputs and 10 outputs,\
defined in terms of all these weighted sums.\
The cost function is a layer of complexity on top of that.\
It takes the 13,000 weights and biases as inputs and spits out\
a single measure of lousiness based on the training examples.\
And the gradient of the cost function is one more layer of complexity still.\
It tells us what nudges to all these weights and biases cause the\
fastest change to the value of the cost function,\
which you might interpret as saying which changes to which weights matter the most.\
Analyzing the network\
So, when you initialize the network with random weights and biases,\
and adjust them many times based on this gradient descent process,\
how well does it actually perform on images it's never seen before?\
The one I've described here, with the two hidden layers of 16 neurons each,\
chosen mostly for aesthetic reasons, is not bad,\
classifying about 96% of the new images it sees correctly.\
And honestly, if you look at some of the examples it messes up on,\
you feel compelled to cut it a little slack.\
Now if you play around with the hidden layer structure and make a couple tweaks,\
you can get this up to 98%.\
And that's pretty good!\
It's not the best, you can certainly get better performance by getting more sophisticated\
than this plain vanilla network, but given how daunting the initial task is,\
I think there's something incredible about any network doing this well on images it's\
never seen before, given that we never specifically told it what patterns to look for.\
Originally, the way I motivated this structure was by describing a hope we might have,\
that the second layer might pick up on little edges,\
that the third layer would piece together those edges to recognize loops\
and longer lines, and that those might be pieced together to recognize digits.\
So is this what our network is actually doing?\
Well, for this one at least, not at all.\
Remember how last video we looked at how the weights of the connections from all\
the neurons in the first layer to a given neuron in the second layer can be\
visualized as a given pixel pattern that the second layer neuron is picking up on?\
Well, when we actually do that for the weights associated with these transitions,\
from the first layer to the next, instead of picking up on isolated little edges here\
and there, they look, well, almost random, just with some very loose patterns in the\
middle there.\
It would seem that in the unfathomably large 13,000 dimensional space\
of possible weights and biases, our network found itself a happy\
little local minimum that, despite successfully classifying most images,\
doesn't exactly pick up on the patterns we might have hoped for.\
And to really drive this point home, watch what happens when you input a random image.\
If the system was smart, you might expect it to feel uncertain,\
maybe not really activating any of those 10 output neurons or activating them\
all evenly, but instead it confidently gives you some nonsense answer,\
as if it feels as sure that this random noise is a 5 as it does that an actual\
image of a 5 is a 5.\
Phrased differently, even if this network can recognize digits pretty well,\
it has no idea how to draw them.\
A lot of this is because it's such a tightly constrained training setup.\
I mean, put yourself in the network's shoes here.\
From its point of view, the entire universe consists of nothing but clearly\
defined unmoving digits centered in a tiny grid,\
and its cost function never gave it any incentive to be anything but utterly\
confident in its decisions.\
So with this as the image of what those second layer neurons are really doing,\
you might wonder why I would introduce this network with the\
motivation of picking up on edges and patterns.\
I mean, that's just not at all what it ends up doing.\
Well, this is not meant to be our end goal, but instead a starting point.\
Frankly, this is old technology, the kind researched in the 80s and 90s,\
and you do need to understand it before you can understand more detailed modern\
variants, and it clearly is capable of solving some interesting problems,\
but the more you dig into what those hidden layers are really doing,\
the less intelligent it seems.\
Learning more\
Shifting the focus for a moment from how networks learn to how you learn,\
that'll only happen if you engage actively with the material here somehow.\
One pretty simple thing I want you to do is just pause right now and think deeply\
for a moment about what changes you might make to this system and how it perceives\
images if you wanted it to better pick up on things like edges and patterns.\
But better than that, to actually engage with the material,\
I highly recommend the book by Michael Nielsen on deep learning and neural networks.\
In it, you can find the code and the data to download and play with for this exact\
example, and the book will walk you through step by step what that code is doing.\
What's awesome is that this book is free and publicly available,\
so if you do get something out of it, consider joining me in making a donation towards\
Nielsen's efforts.\
I've also linked a couple other resources I like a lot in the description,\
including the phenomenal and beautiful blog post by Chris Ola and the articles in\
Distill.\
Lisha Li interview\
To close things off here for the last few minutes,\
I want to jump back into a snippet of the interview I had with Leisha Lee.\
You might remember her from the last video, she did her PhD work in deep learning.\
In this little snippet she talks about two recent papers that really dig into\
how some of the more modern image recognition networks are actually learning.\
Just to set up where we were in the conversation,\
the first paper took one of these particularly deep neural networks that's really good\
at image recognition, and instead of training it on a properly labeled dataset,\
shuffled all the labels around before training.\
Obviously the testing accuracy here was going to be no better than random,\
since everything's just randomly labeled. But it was still able to achieve\
the same training accuracy as you would on a properly labeled dataset.\
Basically, the millions of weights for this particular network were\
enough for it to just memorize the random data,\
which raises the question for whether minimizing this cost function\
actually corresponds to any sort of structure in the image, or is it just memorization?\
...to memorize the entire dataset of what the correct classification is.\
And so half a year later at ICML this year, there was not exactly rebuttal paper,\
but paper that addressed some aspects of like, hey,\
actually these networks are doing something a little bit smarter than that.\
If you look at that accuracy curve if you were just training on a random data set\
that curve went down very slowly, almost in a linear fashion.\
So you\'92re really struggling to find that local minimum of the right weights.\
Whereas if you're actually training on a structured dataset,\
one that has the right labels, you fiddle around a little bit in the beginning,\
but then you kind of dropped very fast to get to that accuracy level,\
and so in some sense it was easier to find that local maxima.\
And so what was also interesting about that is it brings into light another paper from\
actually a couple of years ago, which has a lot more simplifications about the network\
layers, but one of the results was saying how if you look at the optimization landscape,\
the local minima that these networks tend to learn are actually of equal quality,\
so in some sense if your dataset is structured,\
you should be able to find that much more easily.\
Closing thoughts\
My thanks, as always, to those of you supporting on Patreon.\
I've said before just what a game changer Patreon is,\
but these videos really would not be possible without you.\
I also want to give a special thanks to the VC firm Amplify Partners\
and their support of these initial videos in the series. Thank you.\

### Key ideas
- The cost function measures how bad the network is doing.
- Learning means minimizing the cost function.
- Gradient descent moves downhill on the cost surface.
- The negative gradient tells us how to change weights and biases.

---

## Chapter 3: Backpropagation

Here, we tackle backpropagation, the core algorithm behind how neural networks learn.\
After a quick recap for where we are, the first thing I'll do is an intuitive walkthrough\
for what the algorithm is actually doing, without any reference to the formulas.\
Then, for those of you who do want to dive into the math,\
the next video goes into the calculus underlying all this.\
Recap\
If you watched the last two videos, or if you're just jumping in with the appropriate\
background, you know what a neural network is, and how it feeds forward information.\
Here, we're doing the classic example of recognizing handwritten digits whose pixel\
values get fed into the first layer of the network with 784 neurons,\
and I've been showing a network with two hidden layers having just 16 neurons each,\
and an output layer of 10 neurons, indicating which digit the network is choosing\
as its answer.\
I'm also expecting you to understand gradient descent,\
as described in the last video, and how what we mean by learning is\
that we want to find which weights and biases minimize a certain cost function.\
As a quick reminder, for the cost of a single training example,\
you take the output the network gives, along with the output you wanted it to give,\
and add up the squares of the differences between each component.\
Doing this for all of your tens of thousands of training examples and\
averaging the results, this gives you the total cost of the network.\
And as if that's not enough to think about, as described in the last video,\
the thing that we're looking for is the negative gradient of this cost function,\
which tells you how you need to change all of the weights and biases,\
all of these connections, so as to most efficiently decrease the cost.\
Backpropagation, the topic of this video, is an\
algorithm for computing that crazy complicated gradient.\
And the one idea from the last video that I really want you to hold firmly\
in your mind right now is that because thinking of the gradient vector\
as a direction in 13,000 dimensions is, to put it lightly,\
beyond the scope of our imaginations, there's another way you can think about it.\
The magnitude of each component here is telling you how\
sensitive the cost function is to each weight and bias.\
For example, let's say you go through the process I'm about to describe,\
and you compute the negative gradient, and the component associated with the weight on\
this edge here comes out to be 3.2, while the component associated with this edge here\
comes out as 0.1.\
The way you would interpret that is that the cost of the function is 32 times more\
sensitive to changes in that first weight, so if you were to wiggle that value\
just a little bit, it's going to cause some change to the cost,\
and that change is 32 times greater than what the same wiggle to that second\
weight would give.\
Personally, when I was first learning about backpropagation,\
I think the most confusing aspect was just the notation and the index chasing of it all.\
But once you unwrap what each part of this algorithm is really doing,\
each individual effect it's having is actually pretty intuitive,\
it's just that there's a lot of little adjustments getting layered on top of each other.\
Intuitive walkthrough example\
So I'm going to start things off here with a complete disregard for the notation,\
and just step through the effects each training example has on the weights and biases.\
Because the cost function involves averaging a certain cost per example over all\
the tens of thousands of training examples, the way we adjust the weights and\
biases for a single gradient descent step also depends on every single example.\
Or rather, in principle it should, but for computational efficiency we'll do a little\
trick later to keep you from needing to hit every single example for every step.\
In other cases, right now, all we're going to do is focus\
our attention on one single example, this image of a 2.\
What effect should this one training example have\
on how the weights and biases get adjusted?\
Let's say we're at a point where the network is not well trained yet,\
so the activations in the output are going to look pretty random,\
maybe something like 0.5, 0.8, 0.2, on and on.\
We can't directly change those activations, we\
only have influence on the weights and biases.\
But it's helpful to keep track of which adjustments\
we wish should take place to that output layer.\
And since we want it to classify the image as a 2,\
we want that third value to get nudged up while all the others get nudged down.\
Moreover, the sizes of these nudges should be proportional\
to how far away each current value is from its target value.\
For example, the increase to that number 2 neuron's activation\
is in a sense more important than the decrease to the number 8 neuron,\
which is already pretty close to where it should be.\
So zooming in further, let's focus just on this one neuron,\
the one whose activation we wish to increase.\
Remember, that activation is defined as a certain weighted sum of all the\
activations in the previous layer, plus a bias,\
which is all then plugged into something like the sigmoid squishification function,\
or a ReLU.\
So there are three different avenues that can team\
up together to help increase that activation.\
You can increase the bias, you can increase the weights,\
and you can change the activations from the previous layer.\
Focusing on how the weights should be adjusted,\
notice how the weights actually have differing levels of influence.\
The connections with the brightest neurons from the preceding layer have the\
biggest effect since those weights are multiplied by larger activation values.\
So if you were to increase one of those weights,\
it actually has a stronger influence on the ultimate cost function than increasing\
the weights of connections with dimmer neurons,\
at least as far as this one training example is concerned.\
Remember, when we talk about gradient descent,\
we don't just care about whether each component should get nudged up or down,\
we care about which ones give you the most bang for your buck.\
This, by the way, is at least somewhat reminiscent of a theory in\
neuroscience for how biological networks of neurons learn, Hebbian theory,\
often summed up in the phrase, neurons that fire together wire together.\
Here, the biggest increases to weights, the biggest strengthening of connections,\
happens between neurons which are the most active,\
and the ones which we wish to become more active.\
In a sense, the neurons that are firing while seeing a 2 get\
more strongly linked to those firing when thinking about a 2.\
To be clear, I'm not in a position to make statements one way or another about\
whether artificial networks of neurons behave anything like biological brains,\
and this fires together wire together idea comes with a couple meaningful asterisks,\
but taken as a very loose analogy, I find it interesting to note.\
Anyway, the third way we can help increase this neuron's activation\
is by changing all the activations in the previous layer.\
Namely, if everything connected to that digit 2 neuron with a positive\
weight got brighter, and if everything connected with a negative weight got dimmer,\
then that digit 2 neuron would become more active.\
And similar to the weight changes, you're going to get the most bang for your buck\
by seeking changes that are proportional to the size of the corresponding weights.\
Now of course, we cannot directly influence those activations,\
we only have control over the weights and biases.\
But just as with the last layer, it's helpful to\
keep a note of what those desired changes are.\
But keep in mind, zooming out one step here, this\
is only what that digit 2 output neuron wants.\
Remember, we also want all the other neurons in the last layer to become less active,\
and each of those other output neurons has its own thoughts about\
what should happen to that second to last layer.\
So, the desire of this digit 2 neuron is added together with the desires\
of all the other output neurons for what should happen to this second to last layer,\
again in proportion to the corresponding weights,\
and in proportion to how much each of those neurons needs to change.\
This right here is where the idea of propagating backwards comes in.\
By adding together all these desired effects, you basically get a\
list of nudges that you want to happen to this second to last layer.\
And once you have those, you can recursively apply the same process to the\
relevant weights and biases that determine those values,\
repeating the same process I just walked through and moving backwards\
through the network.\
And zooming out a bit further, remember that this is all just how a single\
training example wishes to nudge each one of those weights and biases.\
If we only listened to what that 2 wanted, the network would\
ultimately be incentivized just to classify all images as a 2.\
So what you do is go through this same backprop routine for every other training example,\
recording how each of them would like to change the weights and biases,\
and average together those desired changes.\
This collection here of the averaged nudges to each weight and bias is,\
loosely speaking, the negative gradient of the cost function referenced\
in the last video, or at least something proportional to it.\
I say loosely speaking only because I have yet to get quantitatively precise\
about those nudges, but if you understood every change I just referenced,\
why some are proportionally bigger than others,\
and how they all need to be added together, you understand the mechanics for\
what backpropagation is actually doing.\
Stochastic gradient descent\
By the way, in practice, it takes computers an extremely long time to add\
up the influence of every training example every gradient descent step.\
So here's what's commonly done instead.\
You randomly shuffle your training data and then divide it into a whole\
bunch of mini-batches, let's say each one having 100 training examples.\
Then you compute a step according to the mini-batch.\
It's not going to be the actual gradient of the cost function,\
which depends on all of the training data, not this tiny subset,\
so it's not the most efficient step downhill,\
but each mini-batch does give you a pretty good approximation, and more importantly,\
it gives you a significant computational speedup.\
If you were to plot the trajectory of your network under the relevant cost surface,\
it would be a little more like a drunk man stumbling aimlessly down a hill but taking\
quick steps, rather than a carefully calculating man determining the exact downhill\
direction of each step before taking a very slow and careful step in that direction.\
This technique is referred to as stochastic gradient descent.\
There's a lot going on here, so let's just sum it up for ourselves, shall we?\
Backpropagation is the algorithm for determining how a single training\
example would like to nudge the weights and biases,\
not just in terms of whether they should go up or down,\
but in terms of what relative proportions to those changes cause the\
most rapid decrease to the cost.\
A true gradient descent step would involve doing this for all your tens of\
thousands of training examples and averaging the desired changes you get.\
But that's computationally slow, so instead you randomly subdivide the\
data into mini-batches and compute each step with respect to a mini-batch.\
Repeatedly going through all of the mini-batches and making these adjustments,\
you will converge towards a local minimum of the cost function,\
which is to say your network will end up doing a really good job on the training\
examples.\
So with all of that said, every line of code that would go into implementing backprop\
actually corresponds with something you have now seen, at least in informal terms.\
But sometimes knowing what the math does is only half the battle,\
and just representing the damn thing is where it gets all muddled and confusing.\
So for those of you who do want to go deeper, the next video goes through the same\
ideas that were just presented here, but in terms of the underlying calculus,\
which should hopefully make it a little more familiar as you see the topic in other\
resources.\
Before that, one thing worth emphasizing is that for this algorithm to work,\
and this goes for all sorts of machine learning beyond just neural networks,\
you need a lot of training data.\
In our case, one thing that makes handwritten digits such a nice example is that there\
exists the MNIST database, with so many examples that have been labeled by humans.\
So a common challenge that those of you working in machine learning will be familiar with\
is just getting the labeled training data you actually need,\
whether that's having people label tens of thousands of images,\
or whatever other data type you might be dealing with.\

### Key ideas
- Backpropagation determines how a single training example nudges weights and biases.
- It works backward through the network.
- The result is averaged across training examples or mini-batches.
- This is closely related to stochastic gradient descent.

---

## Chapter 4: Backpropagation calculus

The hard assumption here is that you've watched part 3,\
giving an intuitive walkthrough of the backpropagation algorithm.\
Here we get a little more formal and dive into the relevant calculus.\
It's normal for this to be at least a little confusing,\
so the mantra to regularly pause and ponder certainly applies as much here\
as anywhere else.\
Our main goal is to show how people in machine learning commonly think about\
the chain rule from calculus in the context of networks,\
which has a different feel from how most introductory calculus courses\
approach the subject.\
For those of you uncomfortable with the relevant calculus,\
I do have a whole series on the topic.\
The Chain Rule in networks\
Let's start off with an extremely simple network,\
one where each layer has a single neuron in it.\
This network is determined by three weights and three biases,\
and our goal is to understand how sensitive the cost function is to these variables.\
That way, we know which adjustments to those terms will\
cause the most efficient decrease to the cost function.\
And we're just going to focus on the connection between the last two neurons.\
Let's label the activation of that last neuron with a superscript L,\
indicating which layer it's in, so the activation of the previous neuron is a^(L-1).\
These are not exponents, they're just a way of indexing what we're talking about,\
since I want to save subscripts for different indices later on.\
Let's say that the value we want this last activation to be for\
a given training example is y, for example, y might be 0 or 1.\
So the cost of this network for a single training example is a^(L - y) squared.\
We'll denote the cost of that one training example as C0.\
As a reminder, this last activation is determined by a weight,\
which I'm going to call w(L), times the previous neuron's activation plus some bias,\
which I'll call b(L).\
And then you pump that through some special nonlinear function like the sigmoid or ReLU.\
It's actually going to make things easier for us if we give a special name to\
this weighted sum, like z, with the same superscript as the relevant activations.\
This is a lot of terms, and a way you might conceptualize it is that the weight,\
previous action and the bias all together are used to compute z,\
which in turn lets us compute a, which finally, along with a constant y,\
lets us compute the cost.\
And of course a(L-1) is influenced by its own weight and bias and such...\
but we're not going to focus on that right now.\
All of these are just numbers, right?\
And it can be nice to think of each one as having its own little number line.\
Our first goal is to understand how sensitive the\
cost function is to small changes in our weight w(L).\
Or phrased differently, what is the derivative of C with respect to w(L)?\
When you see this del w term, think of it as meaning some tiny nudge to W,\
like a change by 0.01, and think of this del C term as meaning\
whatever the resulting nudge to the cost is.\
What we want is their ratio.\
Conceptually, this tiny nudge to w(L) causes some nudge to z(L),\
which in turn causes some nudge to a(L), which directly influences the cost.\
So we break things up by first looking at the ratio of a tiny change to z(L) to\
this tiny change w(L), that is, the derivative of z(L) with respect to w(L).\
Likewise, you then consider the ratio of the change to a(L) to\
the tiny change in z(L) that caused it, as well as the ratio\
between the final nudge to C and this intermediate nudge to a(L).\
This right here is the chain rule, where multiplying together these\
three ratios gives us the sensitivity of C to small changes in w(L).\
Computing relevant derivatives\
So on screen right now, there's a lot of symbols,\
and take a moment to make sure it's clear what they all are,\
because now we're going to compute the relevant derivatives.\
The derivative of C with respect to a(L) works out to be 2(a(L)-y).\
Notice this means its size is proportional to the difference between the network's\
output and the thing we want it to be, so if that output was very different,\
even slight changes stand to have a big impact on the final cost function.\
The derivative of a(L) with respect to z(L) is just the derivative\
of our sigmoid function, or whatever nonlinearity you choose to use.\
And the derivative of z(L) with respect to w(L)... In this case comes out to be a(L-1).\
What do the derivatives mean?\
Now I don't know about you, but I think it's easy to get stuck head down in the\
formulas without taking a moment to sit back and remind yourself of what they all mean.\
In the case of this last derivative, the amount that the small nudge to the\
weight influenced the last layer depends on how strong the previous neuron is.\
Remember, this is where the neurons-that-fire-together-wire-together idea comes in.\
And all of this is the derivative with respect to w(L)\
only of the cost for a specific single training example.\
Since the full cost function involves averaging together all\
those costs across many different training examples,\
its derivative requires averaging this expression over all training examples.\
And of course, that is just one component of the gradient vector,\
which itself is built up from the partial derivatives of the\
cost function with respect to all those weights and biases.\
Sensitivity to weights/biases\
But even though that's just one of the many partial derivatives we need,\
it's more than 50% of the work.\
The sensitivity to the bias, for example, is almost identical.\
We just need to change out this del z del w term for a del z del b.\
And if you look at the relevant formula, that derivative comes out to be 1.\
Also, and this is where the idea of propagating backwards comes in,\
you can see how sensitive this cost function is to the activation of the previous layer.\
Namely, this initial derivative in the chain rule expression,\
the sensitivity of z to the previous activation, comes out to be the weight w(L).\
And again, even though we're not going to be able to directly influence\
that previous layer activation, it's helpful to keep track of,\
because now we can just keep iterating this same chain rule idea backwards\
to see how sensitive the cost function is to previous weights and previous biases.\
Layers with additional neurons\
And you might think this is an overly simple example, since all layers have one neuron,\
and things are going to get exponentially more complicated for a real network.\
But honestly, not that much changes when we give the layers multiple neurons,\
really it's just a few more indices to keep track of.\
Rather than the activation of a given layer simply being a(L),\
it's also going to have a subscript indicating which neuron of that layer it is.\
Let's use the letter k to index the layer L-1, and j to index the layer L.\
For the cost, again we look at what the desired output is,\
but this time we add up the squares of the differences between these last layer\
activations and the desired output.\
That is, you take a sum over a(L)j minus yj squared.\
Since there's a lot more weights, each one has to have a couple more\
indices to keep track of where it is, so let's call the weight of\
the edge connecting this kth neuron to the jth neuron, w(L)_jk.\
Those indices might feel a little backwards at first,\
but it lines up with how you'd index the weight matrix I talked about in\
the part 1 video.\
Just as before, it's still nice to give a name to the relevant weighted sum,\
like z, so that the activation of the last layer is just your special function,\
like the sigmoid, applied to z.\
You can see what I mean, where all of these are essentially the same equations we had\
before in the one-neuron-per-layer case, it's just that it looks a little more\
complicated.\
And indeed, the chain-ruled derivative expression describing how\
sensitive the cost is to a specific weight looks essentially the same.\
I'll leave it to you to pause and think about each of those terms if you want.\
What does change here, though, is the derivative of the cost\
with respect to one of the activations in the layer L-1.\
In this case, the difference is that the neuron influences\
the cost function through multiple different paths.\
That is, on the one hand, it influences a(L)0, which plays a role in the cost function,\
but it also has an influence on a(L)1, which also plays a role in the cost function,\
and you have to add those up.\
And that, well, that's pretty much it.\
Once you know how sensitive the cost function is to the\
activations in this second-to-last layer, you can just repeat\
the process for all the weights and biases feeding into that layer.\
Recap\
So pat yourself on the back!\
If all of this makes sense, you have now looked deep into the heart of backpropagation,\
the workhorse behind how neural networks learn.\
These chain rule expressions give you the derivatives that determine each component in\
the gradient that helps minimize the cost of the network by repeatedly stepping downhill.\
If you sit back and think about all that, this is a lot of layers of complexity to\
wrap your mind around, so don't worry if it takes time for your mind to digest it all.\
\

### Key ideas
- The math formalizes the intuitive backprop explanation.
- It uses calculus to compute gradients efficiently.
- It helps explain why the algorithm works.