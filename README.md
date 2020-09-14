# Part Of Speech Tagging

Introduction – 
Correct part of speech tagging is the AI problem in which demands a part of speech associated with word in the sentence. 
Main problem here is a word can have multiple part of speech tags depending on its use. 
For example a word can be noun in some cases and same word can be verb in different case depending upon 
the position of the word in the sentence. The problem is implemented using three different algorithms-

  ## 1)Bays Net – 
    
    It’s a simplified way to solve this problem. To solve the maximum probability of the word 
    with certain part of speech is picked. For example. Let’s consider the case of the word “The” Here
    we have maximum probability for the as determiner and the probability of “the” with remaining part of
    speeches is well below the max value. So by this logic we have returned the as determiner. Its provides 
    the accuracy as 92% for the words but when whole sentence is taken into the consideration the accuracy 
    goes down to 39%. As here we don’t consider the relation of the words label and its dependency on the 
    label of the previous word.

  ## 2)Viterbi – 
  As there is dependency of the part of speech of the word is on the part of the speech of the initial word. 
  This case can be handled by the Viterbi algorithms. Here we consider three types of the probabilities. 
    a. Start Probability- Provides the probability of the label occurrence at 1st position. 
        Here we have the list of size 12 with probability of each part of speech on 1st location of the sentence. 
    b. Emission – It’s the probability of the all word with all 12 part of speeches separately. 
        It will provide us the probabilities of the all the words from the training data with all possible part of speeches. 
        In some cases the trained data don’t carry few values which can occur in the final where testing is 
         carried out on the data. Here some small value is taken as the probability of the word with all part of speeches. 
    c. Transition – It’s the probability of the part of speeches occurrence from part of speech tag of the initial word. 
        It has matrix of 12*12. Which will provide the probability values of part of speech transition.

In the algorithm part of speech tagging is calculated based on all the probability values above mentioned. 
Here we will go on traversing from the 1st word of the sentence till the last. 
Here the multiplication of the transition and the emission probabilities is carried out and the maximum value 
of the probability is picked. By this logic, the part of speech tag of the certain word after certain part of speech is considered.
For example the noun occurrence after determiner. And later the maximum value is picked. 
Here accuracy is increased and is 95 % of the words while accuracy of the sentence is 53.70% which is better than simple bays net.

## 3. Complex MCMC – 
    
    Gibbs sampling which is mainly used to handle the complex bays nets. 
    After considering the random labels for each word in the sentence. Here we consider the random number 
    for finding out the most stable output of the over the cumulative probabilities. 
    The final value of the part of speech is calculated based on the position where the random number lies between 0 and 1.
    The cumulative probability will give us the better value for the part of speech tag. 
    Here the random value is generated for 400 times and the last occurrence is picked for the final part of speech.

## Posteriori Log – 
Here the log value is calculated for the posterior value. Posterior value is calculated 
    using emission as well as transition probability. It’s calculated on the final output label list of 
    the sentence obtained from the algorithms. We calculate the value by considering prior probability.

Final Output Accuracy achieved- So far scored 2000 sentences with 29442 words. 

## Words correct: Sentences correct: 0. Ground truth: 100.00% 100.00% 
## 1. Simple: 92.13% 39.45% 2. HMM: 94.68% 53.70% 3. Complex: 88.89% 28.50%

## Problems Faced- 
  While training the data and calculating the emission probability, the data set generated might 
not have few values that can occur during the final sentences. So some small value is assigned to the probability
value when considered during the algorithm. Small value taken is smaller than the smallest value out of the all 
obtained values. During the Gibbs sampling algorithm the cumulative probability is calculated. Here we needed to 
normalise the probabilities as we added some small values for words without emission probabilities. Hence the sum 
of probabilities for the word can go above 1 and that is needed to be handled.
