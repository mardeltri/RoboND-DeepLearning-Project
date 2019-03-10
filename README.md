## Project: Follow me

[//]: # (Image References)

[main]: ./misc_images/main.png
[run1_crowd]: ./misc_images/run1_crowd.PNG
[run2_short]: ./misc_images/run2_short.png
[run3_zigzag]: ./misc_images/run3_zigzag.png
[PatrolPath]: ./misc_images/PatrolPath.png
[following]: ./misc_images/following.png
[withoutTarget]: ./misc_images/withoutTarget.png
[withTarget]: ./misc_images/withTarget.png

<img src="./misc_images/main.png" width="350" />

In this project, a Fully Convolutional Network will be implemented and trained to detect a person with a
quadrotor. This simulation will be carried out in the provided FollowMeSim, which includes a city with people 
and the person to be tracked.

### Data Collection
The first step has been to take more pictures to train our network. As suggested in Data Collection Guide, three
situations have been considered:
* Data gathered by following the hero in a very dense crowd.
* Data gathered while in patrol directly over the hero, while they zigzag.
* Data gathered while the quad is on standard patrol.

Below, it can be seen the paths which have been implemented in FollowMeSim.

* Hero in a very dense crowd in following mode

<img src="./misc_images/run1_crowd.png" width="350" />

* Hero in a very dense crowd in patrol mode

<img src="./misc_images/run2_short.png" width="350" />

* Hero in zigzag while the quad is patrolling over it.
<img src="./misc_images/run3_zigzag.png" width="350" />

* Quad in standard patrol
<img src="./misc_images/PatrolPath.png" width="350" />

### Network architecture

FCN

encoder and decoder
encoder - extracts features that will be used laater by the decoder
Encoder -> Extract features from the layers
decoder -> it uses a second special technique of transposed convolutional layers to upsample the image

Replacement of fully-connected layers with convolutional layers presents an added advantage that during inference (testing your model), you can feed images of any size into your trained network.

One effect of convolutions or encoding in general is you narrow down the scope by looking closely 
at some picture and lose the bigger picture as a result. So even if we were to decode the output
of the encoder back to the original image size, some information has been lost. Skip connections
are a way of retaining the information easily.

Encoder 1 (?, 80, 80, 32)
Encoder 2 (?, 40, 40, 64)
Encoder 3 (?, 20, 20, 128)
1x1 Conv (?, 20, 20, 128)
Decoder 1 (?, 40, 40, 128)
Decoder 2 (?, 80, 80, 64)
Decoder 3 (?, 80, 80, 64)
Output Layer (?, 160, 160, 3)

### Hyperparameters

### Results

Scores for while the quad is following behind the target. 
number of validation samples intersection over the union evaulated on 542
average intersection over union for background is 0.9963649904368955
average intersection over union for other people is 0.374343463883581
average intersection over union for the hero is 0.9202535829853801
number true positives: 539, number false positives: 0, number false negatives: 0

# Scores for images while the quad is on patrol and the target is not visable
number of validation samples intersection over the union evaulated on 270
average intersection over union for background is 0.9909623240530145
average intersection over union for other people is 0.8147482312946245
average intersection over union for the hero is 0.0
number true positives: 0, number false positives: 27, number false negatives: 0

# Score to measure how well the neural network can detect the target from far away
number of validation samples intersection over the union evaulated on 322
average intersection over union for background is 0.9969959805429339
average intersection over union for other people is 0.4654899637565508
average intersection over union for the hero is 0.21417443633161937
number true positives: 123, number false positives: 1, number false negatives: 178

# Sum all the true positives, etc from the three datasets to get a weight for the score
0.7626728110599078

# The IoU for the dataset that never includes the hero is excluded from grading
0.567214009658

# Final grade score
0.432598703219

# Future Enhancements