---
layout: post
title: "Physical Reservoir Computing"
description: "Markdown features for the posts"
categories: [reservoir computing]
tags: [reservoir computing]
redirect_from:
  - /2020/05/02/
---
<script type="text/javascript" async
  src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-MML-AM_CHTML">
</script>

Reservoir computing (RC) is derived from recurrent neural network (RNN).
They are different from RNN in that the weights on the recurrent connections are
not trained (this part is called a reservoir), but only the weights in the
readout are trained to map to the desired value.
The basic frameworks include [**echo state network**](#ESN) (ESN) and
[**liquid state machine**](*LSM) (LSM).

<img src="RC.png" alt="conventional / physical RC" width="1000"/>

Physical reservoir computing (RC) follows the concept of reservoir and readout,
but it uses reservoirs based on physical phenomena.
The motivation for the physical implementation of reservoirs is to realize fast
information processing devices with low learning costs.
It also has advantage in hardware implementation without adaptive updating.
While it seems any physical dynamical systems can replace RNNs, there are some
[**requirements**](#requirements)

This note summarizes parts of
[Recent advances in physical reservoir computing: A review][1] that relate to
morphological computing, control, and frameworks with biological neurons.
This paper categorizes physical reservoirs based on the type of
[**dynamical system**](#dynamics) and [**physical phenomenon**](#physics).
It also discusses the [**challenges**](#challenges).

---
# Basic framework of RC

*  <a name="ESN">ESN

$$ \bf{x}(n) = \bf{f} ( W^{in} \bf{u}(n) + W \bf{x} (n-1) ) $$

$$ \bf{y}(n) = W^{out} \bf{x}(n) $$

where $$n$$ is discrete time, $$\bf{u}(n)$$ is the input, $$\bf{x}(n)$$ is the
reservoir state, $$\bf{y}(n)$$ is the output,
and $$\bf{f}$$ is the activation function.
The weight $$W^{in}$$ is for the input-reservoir connections,
$$W$$ is the weight in the reservoir,
and $$W^{out}$$ is the weight matrix in the readout.
Only $$W^{out}$$ is trained to minimize the difference between the network output
and the desired output.

*  <a name="LSM">LSM

The purpose of LSM is to develop biologically relevant learning models using
spiking neural networks (SNNs) with recurrent connectivity.
Therefore, the reservoir units are typically given by excitatory and inhibitory
spiking neurons,
and the connection between neurons depends on the distance between their positions.

$$ \bf{x}(t) = (\bf{L}^M u)(t) $$

$$ \bf{y}(t) = \bf{f}^M (\bf{x}(t)) $$

where $$x$$ and $$y$$ follow the denotation in ESN,
and $$t$$ represents continuous time.
The output $$u$$ here is encoded as a spike sequence,
$$\bf{L}^M$$ is the filter for transforming the input into the reservoir state,
and $$\bf{f}^M$$ is simply a readout mapping.

*  <a name="echo">Echo state property / Fading memory property

In order to approximate the desired output, the RNN-based reservoir must have
the echo state property, also known as fading memory property.
It means that the outputs corresponding to inputs that are close in
the recent past are close even if those input are very different in the distant
past, as if the system forgot earlier memory.
The property can be obtained if the spectral radius (i.e. the maximum absolute
eigenvalue of $$W$$) is less than unity for any input.

---

# <a name="requirements"></a>Requirements

These are the requirements for a physical reservoir to efficiently solve
computational tasks.

* High dimensionality

By mapping the inputs into high-dimensional space, it might facilitate the
separation of originally inseparable inputs.

* Nonlinearity

It is also for input separation.
Moreover, it can be useful for extracting nonlinear dependencies of inputs
in prediction tasks.

* Fading memory (short-term memory)

It corresponds to the [**echo state property**](#echo) in conventional RC.

* Separation property

It is required to separate the responses of a reservoir to distinct signals into
different classes, and to be insensitive to unessential noises.

---

# <a name="dynamics"></a>Dynamical system

* Delayed dynamical system

$$\frac{d\bf{x}(t)}{dt} = F(t,\bf{x}(t),\bf{x}(t-\tau))$$

where $$F$$ is a function determining the flow of the system,
and $$\tau>0$$ is the delay period.

Here is the single-node reservoir with delayed feedback.

<img src="delayed.png" alt="RC with delayed dynamical system" width="700"/>

The input is time-multiplexed by a mask function, and fe to the reservoir.
In the reservoir, there are $$N$$ virtual nodes dividing the delayed period $$\tau$$.
The time interval between two consecutive nodes is $$\theta := \tau/N$$.
The states of these nodes, $$x(t-(N-i)\theta)$$ for $$i=1,...,N$$, are used as
the reservoir state at time $$t$$.

* Cellular automata (CA)

CA is a simple dynamical system with discrete time and states.
The reservoir implementation facilitates its rich dynamics.

<img src="cellular_automata.png" alt="RC with cellular automata" width="600"/>

Inputs are first mapped to the initial states of CA through an encoding procedure.
Then, CA would start evolving based on its dynamics and the initial state.
The entire state of the CA evolution is vectorized and used as a feature vector.

* Coupled oscillators

A system of $$N$$ coupled oscillators can be described as:

$$\frac{d\bf{x}(t)}{dt}=F(\bf{x}_i(t))+G(\bf{x}_1(t),...,\bf{x}_N(t)),
for i=1,...,N $$

where $$\bf{x}_i(t)$$ is the oscillator $$i$$ state,
$$F$$ is the dynamics of individual oscillators, and $$G$$ is the coupling function.

---

# <a name="physics"></a>Physical phenomenon

*  Mechanical RC
    * Soft and compliant robots are difficult to control,
    but its complex dynamics can be leveraged for RC.
    * morphological computing: outsourcing computation to a physical body
    * mass-spring:
        * [pattern generators][2]
        * [property of the mechanical reservoir <-> locomotion learning][3]
    * muscular hydrostat system
        * [ESN-based controller for a soft arm][4]
        * [information processing][5] (for control)
        * [body dynamics as computational source][6] (for control)
    * robot control
        * [pneumatically driven soft arm][7]
        * [spine-driven quadruped robot][8]
        * [dog-like quadruped robot][9]
        * [less compliant quadrupedal robot][10]
*  Biological RC
    * [closed-loop reservoir with neurons to control a mobile robot][11]
    * [discussion of RC on robot control][12]

---

# <a name="challenges"></a>Challenges

* How to design physical reservoirs for achieving high computational performance?

* How much computational power can be attained by individual physical RC systems?

General issues include:

* preprocessing:
  adequate information transformation of input data is necessary for good performance.

* scaling:
  temporal and spatial scaling of input data affects performance.

* design of reservoir:
  selection of physical systems, their size and haper-parameters is important.
  Mathematical analysis may help determining the settings.

* training algorithm for the readout:
  this affects computation speed.

* evaluation of computational performance

  * task-dependent measure: accuracy...

  * [kernal quality][13]

  * [generalization ability][14]


---

[1]:https://www.sciencedirect.com/science/article/pii/S0893608019300784
[2]:https://link.springer.com/article/10.1007/s00422-012-0516-4
[3]:https://www.frontiersin.org/articles/10.3389/fnbot.2017.00016/full
[4]:https://ieeexplore.ieee.org/document/6252774
[5]:https://www.nature.com/articles/srep10487
[6]:https://royalsocietypublishing.org/doi/10.1098/rsif.2014.0437
[7]:https://muse.jhu.edu/article/661286
[8]:http://vigir.missouri.edu/~gdesouza/Research/Conference_CDs/IEEE_IROS_2013/media/files/1498.pdf
[9]:https://ieeexplore.ieee.org/abstract/document/5628051
[10]:https://ieeexplore.ieee.org/document/7354014
[11]:https://www.frontiersin.org/10.3389/conf.fnins.2016.93.00027/event_abstract
[12]:https://www.mitpressjournals.org/doi/abs/10.1162/isal_a_072
[13]:https://www.mitpressjournals.org/doi/10.1162/neco.2009.01-09-947
[14]:https://www.sciencedirect.com/science/article/abs/pii/S0893608007000433
