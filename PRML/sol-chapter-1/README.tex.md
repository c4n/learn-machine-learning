# Chapter 1 - Introduction

## Exercise 1.1
In this exercise, we have to show that the solution of the coefficients $\mathbf{w}=\left\{w_{i}\right\}$, that minimize the sum-of-squares error function (1.2) of the polynomial (1.1), can be expressed in a form of $\sum_{j=0}^{M} A_{i j} w_{j}=T_{i}$ (1.122)  where   $A_{i j}=\sum_{n=1}^{N}\left(x_{n}\right)^{i+j}$ and $T_{i}=\sum_{n=1}^{N}\left(x_{n}\right)^{i} t_{n}$        

The minimization of the sum-of-squares error function of the polynomail has a unqiue solution that can be found in closed form.  You can read section 1.1 in the  PRML book for more explaination.         

To find extrema: we look for the points where the derivatives are 0.     
$\frac{\partial E}{\partial \mathbf{w}} = 0$           
  In this exercise, we want to show that the coefficients $\mathbf{w}=\left\{w_{i}\right\}$ minimize the sum-of-squares error function. ($\frac{\partial E}{\partial w_i} = 0$ )             
            
Note that:     

$y(x, \mathbf{w})=w_{0}+w_{1} x+w_{2} x^{2}+\ldots+w_{M} x^{M}=\sum_{j=0}^{M} w_{j} x^{j}$ - (1.1)     
$E(\mathbf{w})=\frac{1}{2} \sum_{n=1}^{N}\left\{y\left(x_{n}, \mathbf{w}\right)-t_{n}\right\}^{2}$ - (1.2)         



Step 1:           
Plug in (1.1) into (1.2)      
$E(\mathbf{w})=\frac{1}{2} \sum_{n=1}^{N}\left\{ \left(\sum_{j=0}^{M} w_{j} \left(x_{n}  \right)^{j}  \right)-t_{n}\right\}^{2}$      

Step 2: 
Use [chain rule](https://www.khanacademy.org/math/differential-calculus/dc-chain) and [partial derivative](https://www.khanacademy.org/math/multivariable-calculus/multivariable-derivatives/partial-derivative-and-gradient-articles/a/introduction-to-partial-derivatives) to derive $\frac{\partial E}{\partial w_i}$       
                          
$\frac{\partial E}{\partial w_i} = \sum_{n=1}^{N}\left\{ \left(\sum_{j=0}^{M} w_{j} \left(x_{n}  \right)^{j}  \right)-t_{n}\right\}\left(x_{n}  \right)^{i}= 0 $ 

Step 3:            
                          
$\frac{\partial E}{\partial w_i} = \sum_{n=1}^{N}\left\{ \left(\sum_{j=0}^{M} w_{j} \left(x_{n}  \right)^{i+j}  \right)- \left(x_{n}  \right)^{i} t_{n}  \right\ }= 0 $ 

Step 4:               
Change [the order of summation](https://en.wikipedia.org/wiki/Summation#Identities)   (With multiple sums, the order of summation is not important, provided the bounds on the inner sum don’t depend on the index of the outer sum)                 
$\frac{\partial E}{\partial w_i} =\sum_{j=0}^{M} \left\{ \left(\sum_{n=1}^{N} w_{j} \left(x_{n}  \right)^{i+j}  \right) \right\} = \sum_{n=1}^{N} \left(x_{n}  \right)^{i} t_{n}  $ 
                   
Hence,                  
$\sum_{j=0}^{M} A_{i j} w_{j}=T_{i}$
