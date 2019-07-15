# Chapter 1 - Introduction
* [Exercise 1.1](##-exercise-1.1)
## Exercise 1.1
In this exercise, we have to show that the solution of the coefficients <img src="/PRML/sol-chapter-1/tex/9a7d2e55e8d5b0ef2e33dd7f7ec556c1.svg?invert_in_darkmode&sanitize=true" align=middle width=69.51281204999998pt height=24.65753399999998pt/>, that minimize the sum-of-squares error function (1.2) of the polynomial (1.1), can be expressed in a form of <img src="/PRML/sol-chapter-1/tex/73c0dccc85d63aaea1af498011d37299.svg?invert_in_darkmode&sanitize=true" align=middle width=122.43733259999999pt height=32.256008400000006pt/> (1.122)  where   <img src="/PRML/sol-chapter-1/tex/a555f02e2373b915dac554e020f1411e.svg?invert_in_darkmode&sanitize=true" align=middle width=143.48198369999997pt height=32.256008400000006pt/> and <img src="/PRML/sol-chapter-1/tex/1441846f25ba72d790610b188732a3cb.svg?invert_in_darkmode&sanitize=true" align=middle width=136.0826808pt height=32.256008400000006pt/>        

The minimization of the sum-of-squares error function of the polynomail has a unqiue solution that can be found in closed form.  You can read section 1.1 in the  PRML book for more explaination.         

To find extrema: we look for the points where the derivatives are 0.     
<img src="/PRML/sol-chapter-1/tex/c063cfe40b69ea5557ee2fb24dcc4968.svg?invert_in_darkmode&sanitize=true" align=middle width=50.758403849999986pt height=28.92634470000001pt/>           
  In this exercise, we want to show that the coefficients <img src="/PRML/sol-chapter-1/tex/9a7d2e55e8d5b0ef2e33dd7f7ec556c1.svg?invert_in_darkmode&sanitize=true" align=middle width=69.51281204999998pt height=24.65753399999998pt/> minimize the sum-of-squares error function. (<img src="/PRML/sol-chapter-1/tex/fef9866d8ec0d5be48150c538105f387.svg?invert_in_darkmode&sanitize=true" align=middle width=54.55425524999999pt height=28.92634470000001pt/> )             
            
Note that:     

<img src="/PRML/sol-chapter-1/tex/b584facb31bf4b558b1740276893c710.svg?invert_in_darkmode&sanitize=true" align=middle width=407.22455729999996pt height=32.256008400000006pt/> -- (1.1)     
<img src="/PRML/sol-chapter-1/tex/4c159655574163a7be6fd8e45fc512c5.svg?invert_in_darkmode&sanitize=true" align=middle width=242.32595145pt height=32.256008400000006pt/> -- (1.2)         



Step 1:           
Plug in (1.1) into (1.2)      
> <img src="/PRML/sol-chapter-1/tex/8b399fe9f7df55d5d1bc8cfd43b33a24.svg?invert_in_darkmode&sanitize=true" align=middle width=306.8525196pt height=44.51174640000002pt/>      

Step 2: 
Use [chain rule](https://www.khanacademy.org/math/differential-calculus/dc-chain) and [partial derivative](https://www.khanacademy.org/math/multivariable-calculus/multivariable-derivatives/partial-derivative-and-gradient-articles/a/introduction-to-partial-derivatives) to get <img src="/PRML/sol-chapter-1/tex/6a771672bde41186f4fb6eefd762599d.svg?invert_in_darkmode&sanitize=true" align=middle width=22.444817999999994pt height=28.92634470000001pt/>       
                          
> <img src="/PRML/sol-chapter-1/tex/041279d84da164a9865c84331c07ff84.svg?invert_in_darkmode&sanitize=true" align=middle width=341.17454415000003pt height=37.80850590000001pt/> 

Step 3:            
                          
> <img src="/PRML/sol-chapter-1/tex/3312332a99ece9e53b0bb1f71ea43631.svg?invert_in_darkmode&sanitize=true" align=middle width=352.40989575000003pt height=37.80850590000001pt/> 

Step 4:               
Change [the order of summation](https://en.wikipedia.org/wiki/Summation#Identities)   (with multiple sums, the order of summation is not important, provided the bounds on the inner sum don’t depend on the index of the outer sum)                 
> <img src="/PRML/sol-chapter-1/tex/724309b9341fb6d71a044f49c0026b7a.svg?invert_in_darkmode&sanitize=true" align=middle width=372.4676604pt height=37.80850590000001pt/> 
                   
Hence,                  
> <img src="/PRML/sol-chapter-1/tex/73c0dccc85d63aaea1af498011d37299.svg?invert_in_darkmode&sanitize=true" align=middle width=122.43733259999999pt height=32.256008400000006pt/>

## Exercise 1.4
<img src="/PRML/sol-chapter-1/tex/a62a77a62f1a96d2b598f409ba568e73.svg?invert_in_darkmode&sanitize=true" align=middle width=258.07386825000003pt height=37.8085191pt/>  -- (1.27)
