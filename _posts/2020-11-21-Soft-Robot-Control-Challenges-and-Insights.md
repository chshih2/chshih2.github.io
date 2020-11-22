---
layout: post
title: "Why Soft Robot Control is Hard?"
description: "soft robot control challenges and insights"
categories: [SoftRobot]
tags: [control]
redirect_from:
- /2020/11/21/
---
<script type="text/javascript" async
  src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-MML-AM_CHTML">
</script>

This post summarized [this article][1] by Barry Trimmer. I like this article because it points out some fundamental questions we need to answer and some potential directions based on mechanical, physics, and biology perspectives.

---

# Difference between soft and rigid robot control

* Rigid Robot
	* **Limited [degrees of freedom (DOF)][2]** (limited independent rotation and translation)
	* The control strategy is often by reducing DOF by coupling movements in different planes or driving with multiple actuators.
	* Work well with [forward kinematic model][3]
	* Most control strategies are based on the forward kinematic model.
	* Reliable sensory feedback
	* Not very general, versatile, nor robust compared to animal movements

* Soft Robot
	* **Infinite DOF**: deformation in all dimensions by twisting, buckling, folding, and wrinkling
	* [Time-dependent mechanics][4] like viscoelasticity
	* The control strategy might be reducing DOF by "pseudo-joints" and "traveling waves." These two motions are observed in octopus reaching and fetching
	* Or control strategy might NOT be reducing DOF motions. For example, octopus crawling through confined cavities. The body massively deforms and presses against the substrate in all dimensions.
	* Might be more versatile and robust than rigid robots because of the similar mechanism as in the animal movements

# Questions and Insights

* If current robots have the same scale of actuators and sensors as animals, can we produce animal-like capabilities?
* How do animal control so many actuators and sensors?
	* [Vertebrate motor control systems][5]
	* [Muscle synergies][6]
* What do we need to build a more robust general framework for soft robots?
	* Mechanical control theory
	* Physics of shape change
	* Embodiment view of motor control (see next)
* Can control be faster and require less real-time computation by increasing the complexity of the structure or materials?


[1]:https://www.liebertpub.com/doi/pdfplus/10.1089/soro.2014.1504?casa_token=jA_bHQ_FjckAAAAA:ELjBKwUwps0oVtVPLaqjI1qKp_gm1qC5c_H3yPq2x66I6LGiYKtlj5aqTK7UyrheXl0WsF5BYYKcohg
[2]:https://en.wikipedia.org/wiki/Degrees_of_freedom_(mechanics)
[3]:https://www.rosroboticslearning.com/forward-kinematics
[4]:https://www.brown.edu/Departments/Engineering/Courses/En221/Notes/Elasticity/Elasticity.htm
[5]:https://journals.physiology.org/doi/full/10.1152/physrev.00015.2019?rfr_dat=cr_pub++0pubmed&url_ver=Z39.88-2003&rfr_id=ori%3Arid%3Acrossref.org
[6]:https://www.frontiersin.org/articles/10.3389/fncom.2013.00051/full
