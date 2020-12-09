---
layout: post
title: Basic Hamiltonian System
description: “Definitions and examples“
categories: [Hamiltonian]
tags: [control]
redirect_from:
- /2020/12/09/
---
<script type="text/javascript" async
  src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-MML-AM_CHTML">
</script>

I want to introduce [Energy Shaping Control of a CyberOctopus Soft Arm][1], my work with Heng-Sheng and Udit. I worked mostly on the paper's simulation and visualization, but I was deeply amazed by the elegant solution. To introduce this paper, we need to start from basic. This post is going to revisit the fundamentals of a [Hamiltonian system][2].

---
# Hamiltonian System
A Hamiltonian system is defined as a dynamical system with Hamiltonian equations:

$$\dot{x_i} = \frac{\partial H(x,p)}{\partial {p_i}}$$

$$\dot{p_i} = -\frac{\partial H(x,p)}{\partial {x_i}}$$

for $$i=1,2,…,n$$

where
- $$x$$ (state): generalized coordinates of the components of the system
- $$p$$ (momentum): generalized momenta of the components of the system
- $$H(x,p)$$ ([Hamiltonian function][4]): a smooth function with $$x$$ and $$p\in R^n$$
- $$n$$ (degree of freedom of a Hamiltonian system): number of pairs in Hamiltonian equation

There are theories for constructing $$x$$ and $$p$$ for different systems.


# Hamiltonian Function (Hamiltonian)
The meaning behind  $$H(x,p)$$ is to express the rate of change in time of the condition of a dynamic physical system—** a set of moving particles**.

Often time, the Hamiltonian of a system specifies its total energy— the sum of its kinetic energy and its potential energy —in terms of the  Lagrangian function

The Hamiltonian function originated as a generalized statement of the tendency of physical systems to undergo changes only by those processes that either **minimize or maximize the [action][3]** .

The derivative of $$H(x,p)$$ is 0. This indicates that $$H(x,p)$$ is constant. If we plot the curve $$H(x,p)=h$$ on the $$x-p$$ plane, i.e. phase space, we get a curve that constrains the system’s motion.

Since mechanical systems are often subjected to some conservation laws, we can determine the behavior using Hamiltonian by finding conservation laws for the system of interest.

# Example
A simple mass-spring system on a plane, i.e. $$n=1$$.

$$H(x,p)=\text{potential energy}+\text{kinetic energy}=\frac{1}{2}kx^2+\frac{p^2}{2m}=E$$

By assuming there is no friction, then the total energy $$E$$ is conserved in the mass-spring system. This equation indicates the curve is an ellipse. The motion can be derived as,

$$\dot{x} = \frac{\partial H(x,p)}{\partial {p}}=\frac{p}{m}=\text{velocity}$$

$$\dot{p} = -\frac{\partial H(x,p)}{\partial {x}}=-kx=\text{force}$$

[1]: https://arxiv.org/pdf/2004.05747.pdf
[2]:http://people.uleth.ca/~roussel/nld/Hamiltonian.pdf
[3]:https://www.britannica.com/science/action-physics
[4]:https://www.britannica.com/science/Hamiltonian-function
