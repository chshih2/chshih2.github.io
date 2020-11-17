---
layout: post
title: System Identification and Laplace Transform
description: “System identification using step response, impulse response and sine sweep”
categories: [control]
tags: [SystemIdentification]
redirect_from:
 - /2020/11/12/
---
<script type="text/javascript" async
  src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-MML-AM_CHTML">
</script>



Being a TA this semester gives me more joy than I ever expected. I was worried about teaching online (COVID19). Without face to face interaction, it is hard to tell if the students understand or not. However, I got the students' feedback all the time, and I enjoyed the class. I would spend days preparing slides that I was not obligated to do. From reviewing materials and gathering different perspectives and interpretations of the concept, I wanted to fill in the gap between hands-on work in the lab and the lectures' theory. Putting knowledge into words with toy examples and graphs was not easy. I finally understood why some people said we learn more when we teach. Other than that, the joy of getting students' improvements and positive feedback is enormous.

System identification is one of the topics I taught, and here is my note for the lecture. When I was an undergrad, I was not familiar with the term “system identification.” It shows up here and there, sometimes with a step function, sometimes with an impulse function, and sometimes with a sine sweep. This post put these three methods together with analysis using Laplace transform.

---

# First-Order System
The first-order linear system is one of the most practical models. The input-output relationship can be described with a first-order differential equation. Furthermore, there are only two critical factors for this kind of system-- DC gain and time constant. Once we find these two values, we know how the system behaves. Even with a higher-order system, sometimes we can observe a dominant first-order mode. Then, we can ignore those terms and consider the system as a first-order system.

A first-order time-invariant system has a characterization equation in the following form

$$\tau \frac{dh(t)}{dt}+h(t)=k\,f(t)$$

where h is the system response to the force $$f(t)$$. The gain and the time constant are $$k$$ and $$\tau$$.

We can get the solution for this equation using Laplace transform. Based on the input force function, we can observe the features of the corresponding analytical solution. Therefore, if there is a new system, we can inversely figure out the factors $$k$$ and $$\tau$$ by checking the output. The Laplace transform of the system is

$$\tau s H(s) +H(s)=kF(s)$$

Here the only conversion I use from the Laplace table is
$$f^{(N)}(t) \Leftrightarrow s^nF(s)$$.

The system transfer function

$$G(s)=H(s)/F(s)=\frac{k}{1+\tau s}$$


# Step Response
A step function is

$$
u(t) =
    \begin{cases}
      1 & \text{if $t\geq0$}\\
      0 & \text{otherwise}
    \end{cases}  
$$

And its Laplace transform can be found in a table
$$U(s)=\frac{1}{s}$$

<center><img src="stepSys.jpeg" alt="step input to an unknown system" width="300"/></center>

Inputting a step function to the unknown first-order system will give us an output $$Y(s)$$

$$Y(s)=U(s)G(s)=\frac{1}{s}\frac{k}{1+\tau s}=\frac{k}{s+\frac{1}{\tau}}+\frac{k}{s}$$

The last step is obtained from doing [Partial-Fraction Decomposition][1]. Rearranging the equation this way makes it easier to do the inverse Laplace transform back to time domain.

$$y(t)=-ke^{-\frac{t}{\tau}+ku(t)}$$

<center><img src="stepOut.jpeg" alt="Output of a step input to an unknown system" width="500"/></center>

Plotting out the function, we can see this equation is quite simple. There are two phases-- transient and steady-state of the response. Amazingly, they correspond to the equation well. The first term has an exponential to the power of a negative sign multiply by the time. As time increases, this term is going to decay exponentially. Since the term's effect will be close to zero or negligible, we say it is transient. The second term, on the other hand, is just the input multiply by the gain. The only time factor is inside the input function. Therefore, it is called a steady-state response. Together, we can conclude the system's response is simply a scale of the input, with the gain $$k$$, while the transient to that response depends on the time constant $$\tau$$.

If we do not know about the system, we can give a step function and observe the output graph. The gain $$k$$ is the scale factor between the original step function and the steady-state amplitude. To get the time constant $$\tau$$ is tricker. Note that we can plug in $$t=\tau$$ for the amplitude. This gives us

$$y(\tau)=-ke^{\frac{\tau}{\tau}}+ku(\tau)=k(1-e^{-1})=0.6321k$$

Therefore, we can find the time that gives us 63% of the steady-state amplitude for our $$\tau$$. It is called the __63% rule__.
Once the time constant and the gain are found from the plot, we are successfully identify the unknown system.

# Impulse Response
An impulse function $$\delta(t)$$ has a non-zero value at only one instant. We can approximate this in real life with a hammer strike.
Its Laplace transform can be found in a table
$$D(s)=1$$

<center><img src="impSys.jpeg" alt="impulse input to an unknown system" width="300"/></center>

Inputting an impulse function to the unknown first-order system will give us an output $$Y(s)$$

$$Y(s)=D(s)G(s)=1\frac{k}{1+\tau s}=\frac{k}{\tau}\frac{1}{s+\frac{1}{\tau}}$$


Again, rearranging the equation this way makes it easier to do the inverse Laplace transform back to time domain. Using the transformation listed in Laplace table, $$e^{-\alpha t}f|t| \Leftrightarrow \frac{1}{s+\alpha}$$, we get the system response
$$y(t)=\frac{k}{\tau}e^{-\frac{t}{\tau}}$$


<center><img src="impOut.jpeg" alt="Output of an impulse input to an unknown system" width="300"/></center>


By plugging in two different time values, we obtain two amplitudes. The ratio of them cancels out the coefficient for the exponential.

$$\frac{y(t_1)}{y(t_2)}=e^{\frac{(t_2-t_1)}{\tau}}$$

and rewrite the equation, we can calculate the time constant

$$\tau=\frac{t_2-t_1}{ln(\frac{y(t_1)}{y(t_2)})}$$

After getting the time constant, we can obtain the gain from the response equation.

# Higher-Order System and Bode Plot
For a higher-order system, the system response is more complicated. Luckily we can use a bode plot to visualize the system's transfer function. It is nothing more than a frequency spectrum. It records the amplitude and the phase of the transfer function versus frequency. However, to capture a broader range of frequency, the x-axis is in log scale. The Bode plot also uses dB for the magnitude. With a known system, the corresponding bode plot can look like the black line in the graph.

<center><img src="bodePlot.jpeg" alt="bode plot of a transfer function magnitude" width="500"/></center>


The [corner frequencies][2] result from poles and zeros, which determine the system behavior. All of this sounds great and works well theoretically, but we don't know the system in reality.

Inspired by what we have been doing, we can input some signals and observe the output to gain insight into the system. For example, we don't know a system "?", but we randomly put in some numbers and get these results.

<center><img src="sysTest.jpeg" alt="guessing a system by observing input and output" width="200"/></center>

It's not hard to guess the system "?" is "+1".

That's precisely we want to want to do to identify our system, but what are the good signal that can be used to test out general complicated systems?


# Frequency Response (Sine Sweep)
It turns out that a harmonic signal with a specific frequency is a perfect candidate. For example, if we input this kind of function into a system.

<center><img src="sinSys.jpeg" alt="gharmonic input to an unknown system" width="500"/></center>


The system response can be written as a function of the unknown system $$H$$

$$y(t)=|H(j\omega_0)|cos(\omega_0 t + \angle H(j\omega_0))$$


This equation shows that the output is still a cosine function with the same frequency as the input.

However, the magnitude now is scaled by $$|H(j\omega_0)|$$,
and has a phase shift $$\angle H(j\omega_0)$$. Visually, this means


<center><img src="sinOut.jpeg" alt="Output of a harmonic input to an unknown system" width="500"/></center>


Therefore, for a specific frequency, we can use the graph to obtain the system's magnitude and phase. By sweeping through multiple frequencies, we can reconstruct the bode plot. The final transfer function for the system is

$$H(j\omega)=|H(j\omega_0)|e^{ \angle H(j\omega)}$$


[1]:[Partial-Fraction Decomposition: General Techniques](https://www.purplemath.com/modules/partfrac.htm)
[2]:[Bode plot - Wikipedia](https://en.wikipedia.org/wiki/Bode_plot)
