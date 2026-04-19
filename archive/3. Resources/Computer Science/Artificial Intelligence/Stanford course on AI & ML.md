l- field that gives computer the ability to learn.
- There are 2 main types of algorithms. 
- Supervised learning 
- Unsupervised Learning.



Supervised learning 
- You have a set of inputs X and you predict an output Y
- The inputs are labeled with the correct a nswers y on which the algo train/Learns
- It is called supervised as there are examples that the algorithm can learn from 
- There au 2 types of supervised learning
- Regression and classification 
- Regression is to predict an integer from infinitely many possible values
- Classification can predict one value from a set of small possible values.
- classification need not necessarily predict numbers. 
- Predicting the price of a house when we have a set of known prices is an example of regression
- Predicting whether a patient has cancer or not u an example of classification.

Unsupervised Learning
- there we try to find pattern in the data without any labels. 
- So the output him would be something interesting that the algo learns from the data. 
- Clustering is a type of unsupervised leaving. 
- for eg how google clusters news to specific stories each day 
- Anomaly Detection and Dimentionality Reduction are unsupervised learning algos also 
- 
bebe


Linear regression

Terminology 
Training Set This is the data that is used to train the model
X is the input variable also called as feature 
y is the output variable also called target
m is the number of traing examples 
y-hat is used to denote an estimate 
when there is a single input variable or feature it is called as a uni variate linear regression.

f(x)= wx+b 

here w and b are parameters of the model of the variables that you can adjust during training

The point of linear regression is to find the value of f(x) that best fits the data 
we calculate y-hat using wx + b which is the predicted value for X 
 Then we can define a cost function that would calculate the error between y which is the target value and y-hat 
 the most popular function is the squared error cost function in linear regression


Gradient Decent Algo


![[Screenshot 2024-09-08 at 1.13.00 AM.png]]




![[Screenshot 2024-09-08 at 1.47.22 AM.png]]

- Scaling Features 
- So if there  is a big difference between the scale of the 2 features then gradient descent won't work in the most optimized way so for example of you have era of the room which is in thousands and no of rooms as feature than this can cause issues as both parameters will have very varying effect as the formula would be WIXI  W2X2
- To avoid this issue we can use scale the featnes 
- That is normalise the featuers between smaller values like 0 and I 
- Learning Rate 
- L It's a very important valu to be selected while training a model 
- It basically tells how fast the model Learns. 
- Higher value wr the model will learn faster but the cost function might not converge on the minimum


```handwritten-ink
{
	"versionAtEmbed": "0.2.6",
	"filepath": "Assets/Ink/Writing/2024.9.21 - 21.10pm.writing"
}
```



```handwritten-ink
{
	"versionAtEmbed": "0.2.6",
	"filepath": "Assets/Ink/Writing/2024.10.5 - 23.34pm.writing"
}
```
- Classification 
- 