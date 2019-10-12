### Monte Carlo Strategy ###

<div class="alert alert-block alert-info" style="background-color:black; color:white; border-color:white">
<b>Brownian Motion</b>
    
The process $\{W(t)\}_{t\geq0}$ is said to be (standard) Brownian Motion if the follwoing are satisfied: 
    <ul style="list-style-type:disc;">
            <li>$W(0)=0$</li>
            <li>For $s,t\geq0$ the random variable $W(s+t)-W(s) \sim N(0,t)$</li>
            <li>Whenever $0\leq t_0\leq t_1\leq....<t_n$ , the quantities $W(t_1)-W(t_0),W(t_2)-W(t_1),....,W(t_n)-W(t_{n-1})$ are *independent*</li>
            <li>$W(t)$ is a *continuous* function of $t$ with probability $1$</li>
    </ul>   
    
</div>
                
##### Deriving Ito's Lemma (*Time Independent*)

Let us suppose that the asset price $S$ satisifies the **Stochastic Differential Equation (SDE)** 

$$ dS = \mu dt + \sigma dW $$

where $\mu (t)$ and $\sigma(t)$ depends on the time-interval we look at (say 10D period) and the $W(s)$ for $s\leq t$ is a Brownian motion i.e the random fluctuation in a stock-price $S$  

Now consider a function $f(S(t),t)$ of asset price where $f$ has a *continuoous second derivative* (i.e $f\in C^2 (0,T)$). For simplicity, let us assume that $f$ is *independent* of time i.e $f=f(S)$. Then by **Taylor's Theorem**: 

$$ f(S+dS) = f(S) + f'(S)dS + \frac{1}{2}f''(S)(dS)^2+o((dS)^2) $$

Now: $dS = \mu dt + \sigma dW \\ (dS)^2 = \mu^2(dt)^2+2\mu\sigma dt*dW + \sigma^2(dW)^2$

But since $dW$ has order $\sqrt{dt}$ then it has order $dt$. So overall we have: 
$$ (dS)^2 = \sigma^2(dW)^2 + o(dt)$$

After suitable subsitution, we overall get that: 
<p>$$ f(S+dS) - f(S) = f'(S)[\mu dt+\sigma dW] + \frac{1}{2}f''(S)\sigma^2(dW)^2 + o(dt) $$ <\p>
       
Since $W(t)$ is a Brownian Motion $\implies$ $dW=W(t+dt) - W(t)$ is a Brownian Motion with $dW \sim N(0,dt) \\ \implies E[(dW)^2]= Var(dW)+0 \\ \implies =dt$

So in the limit and replacing $(dW)^2$ by $dt$ , we get: 
       
$$df = \frac{df}{dS}(\mu dt+\sigma dW) + \frac{1}{2}\frac{d^2f}{dS^2}\sigma^2dt$$
    
<div class="alert alert-block alert-info" style="background-color:black; color:white; border-color:white">
<b>Ito's Lemma (Time Independent)</b>
    
Let $f(S)$ be a continuous twice differentiable and suppose that: 
    $$ dS = \mu dt + \sigma dW$$
Then: 
    $$df = \frac{df}{dS}(\mu dt+\sigma dW) + \frac{1}{2}\frac{d^2f}{dS^2}\sigma^2dt$$
When written out in the Integral form: 
    $$ f(S(T)) - f(S(0)) = \int_{0}^{T} \left(\mu dt+\sigma dW\right) dt + \int_{0}^{T} \sigma\frac{df}{dS} dW$$
    
Thus we get a relationship between a *Stochastic Integral* and a *Standard Integral* with respect to *time*. 
</div>
        
    
##### A model for stock price     

Consider an asset with price $S(t)$ that evolves according to the SDE 
$$ dS = \mu Sdt + \sigma SdW$$

Over a period $dt$, the price changes by a **deterministic quantity** $\mu Sdt$ (representing some underlying deterministic growth) and a **random quantity** $\sigma SdW$ (where \$\sigma$ measures the volatility of the asset). 
    
It is useful to work in terms of $log(S(t))$ so we define: 
    $$ f(S) = log(S) \\ f'(S) = \frac{1}{S} \\ f''(S) = -\frac{1}{S^2} $$
    
    
So after plugging the following in the SDE we get: 
    
   $$ df = \left(\mu - \frac{1}{2}\sigma^2\right) + \sigma dW $$
    
Plugging into **Ito's Lemma** we get: 

$$ log(S(T)) - log(S(0)) = \left(\mu - \frac{1}{2}\sigma^2\right)T + \sigma W(T) \quad (*)$$
    
    
<div class="alert alert-block alert-info" style="background-color:black; color:white; border-color:white">
    
We conclude that: 
	
$$ log\left(\frac{S(T)}{S(0)}\right) \sim N\left((\mu - \frac{1}{2}\sigma^2)T,\sigma^2T\right) $$
The above equation can be generalised to give the following: 

$$ log\left(\frac{S(t+\Delta t)}{S(t)}\right) \sim N\left((\mu - \frac{1}{2}\sigma^2)\Delta t,\sigma^2\Delta t\right)$$
	
So we say that $Y = \frac{S(t)}{S(0)}$ is **log-normally distributed** with: 
$$ E[Y] = exp\left[{\eta+\frac{1}{2}\sigma^2}t\right] \\ $$
where $\eta = (\mu - \frac{1}{2}\sigma^2)t$
</div>
           
Using $(*)$ we can show that: 
	
$$ S(t+\Delta t) = S(t)*exp\left[\left(\mu - \frac{1}{2}\sigma^2\right)\Delta t + \sigma W(t)\right]$$
	
where $\mu$ is **1+log-return's mean** and $\sigma$ is **1+log-return's standard deviation**
    
    
In my algorithm: 
<span style="color:red">
	$$ \Delta t = 1 \quad \text{since I have daily data} \\ 
	S_{t+1} = S_t*exp\left[\left(\mu - \frac{1}{2}\sigma^2\right) + \sigma W_t\right] $$
 
</span>
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    $$ffd$$
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    g