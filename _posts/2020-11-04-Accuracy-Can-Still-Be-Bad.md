---
layout: post
title: How 99% Accuracy Can Still Be Bad in ML
description: “example of high accuracy being bad and causes of classification errors”
categories: [ML]
tags: [accountability]
redirect_from:
 - /2020/11/04/
---

<script type="text/javascript" async
  src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-MML-AM_CHTML">
</script>


Once I had a long discussion with friends on if AI / ML is going to take over the medical diagnosis.
Even though I work in the ML area and have high hopes for this field's potential, I doubt the industry will change much in recent years. Set aside the fact that we all want a person to talk to, have sympathy, and understand our pain if we are sick, I think ML's techniques are just not there yet.
My friend thought otherwise. He argued with many studies that yield 99% accuracy, and some even bypassed the doctors' performance.
I agreed that ML techniques could identify patterns in detail better than human beings in some cases. However, I was not sure about these numbers without knowing their evaluation metrics. Are the algorithms 99% accurate on True positive? What about the performance of false positive and false negative?

I recently started a learning path, “[Master the Fundamentals of AI and Machine Learning][1],” on LinkedIn Learning. They put together some courses that can help you construct or recap the essential materials for the topic.  One thing that surprised me is that the first course was about AI accountability. While other classes usually start with applications to boost audience excitement, I believe it's crucial to put straight out front the glitches to avoid misusage and wrong interpretation.


---
# A 99% accurate model on a rare disease
One cool example in the course is this disease-screening model with 99% accuracy can give us false belief that it is practical. I modified the table to make it easier to understand.

The accuracy here means the AI model can correctly identify 99% of patients who have the disease. Therefore, 1% of healthy patients can receive false results of having the disease. If this model is for a disease that happens on one out of 100  people, in a population of 1billion people, there will be 10 million people with the disease. By multiplying 10 million with 99%, we get the true positive cases to be 9.9 million. For the remaining 1 billion - 10 million healthy people, 0.01% of them (9.9 million again) are getting false positive cases. This means if somebody gets a positive test result, there is 50% chance that he does not have the disease.  With even rarer diseases, the same calculations lead us to this table.

 (Unit in  % / million / million / million / ratio)

| disease rate      |  carriers   | true positives | false positives |
|:----- | :-----:     | :-----:         | -----:          |
|  1% | 10   |9.9   | 9.9|
| 0.1%   | 1 | 0.99 |9.99|
| 0.01%   | 0.1 | 0.099 |9.999|
| 0.001%   | 0.01 | 0.0099 |9.9999|
| 0.0001%   | 0.001 | 0.00099 |9.99999|



The key to understand what is really happening here is the Bayes’ equation:

$$P(having \,the \,disease \, | \, positive \,result) = \frac{P(positive \,result \, | \, having \,the \,disease)P(having \,the \,disease)}{P(positive\, result)}.$$

Therefore, for a rare disease that is 0.0001%, we can calculate the probability of a person having the disease as

$$P(having\, the\, disease \, | \, positive \,result) = \frac{0.99\times 0.000001}{(0.001+0.00099)/1000}=0.009899 %.$$

(The 1000 is for 1 billion people. We are just changing the unit here.)

If someone got a positive result in this case, the probability of having the disease is 0.009899%. How unacceptable this test is? Lol.

---

# Other causes of classification errors
Here are other causes of classification errors, and the examples are from my personal experiences and understanding.

* Limited variability in data sets.

It’s not covering all possibilities. For example, training a model to recognize facial expression with data on only one specific race. The model won’t work well on all human kinds.

* Homogeneous raters

The dataset is biased from people’s subjective opinion. For example, using a group of people that don’t believe that tomatoes are fruits to label fruits in images. The classifier trained with the data won’t know tomatoes are recognized as fruits for some other people.



[1]:https://www.linkedin.com/learning/paths/master-the-fundamentals-of-ai-and-machine-learning
