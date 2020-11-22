---
layout: post
title: "Zsh Basics and a Script for Grid Search"
description: "zsh script that does grid search for tuning parameters"
categories: [zsh]
tags: [tuningparameters]
redirect_from:
- /2020/11/20/
---
<script type="text/javascript" async
  src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-MML-AM_CHTML">
</script>

Last year, when Apple replaces bash with zsh as the default shell in macOS Catalina, I was half-forced to switch over. The process turned out to be a breeze, and I am thrilled by how many features zsh offers. First of all, I can now use the themes that work for me using  [Oh-My-Zsh](https://github.com/robbyrussell/oh-my-zsh) . Other than that, I like the fact that in Zsh, Tab completion is like a drop-down menu, and I can navigate between options. I can also type the directories with only part of the words, and Zsh will fix the spelling and completion of terms. I also feel Zsh shows a more precise error when something goes wrong. That saves me a bunch of time! These are the reasons why I did a script in zsh when today I needed to do a grid search.


Grid search is an easy method to tune hyper-parameters by tracking the performance of grids. One of the easiest ways, known as Exhaustive Grid Search, is to specify grids of parameter values explicitly. Like [sklearn][1], some libraries provide this function, but sometimes it's not intuitive to couple with our customized model. Since we can write for loops and record the performance directly, why not just do a shell script on top of our python code?  The code is [**here**](#grid_search), and you're welcome to skip the basics.


---
# For Loop
```
for (( i = 0; i < 10; i++ )); do
  echo $i
done

```

It will output ten lines with numbers from 0 to 9.
What if we don't want the output to be multiple lines? We can use "-n" flag!

```
for (( i = 0; i < 10; i++ )); do
  echo -n $i
done
```

This gives us "0123456789%"

Since we need to define the grid ourselves, we can give a list.

```
list=(2 3 5 7 11 13)
for i in $list; do
  echo -n $i
done
```

The output is "23571113%"

To give spaces between the number, we can put a space " " after "$i". This is because the script connect the strings for us this way.
```
list=(2 3 5 7 11 13)
for i in $list; do
  echo -n $i" "
done
```

Now, we have separate numbers "2 3 5 7 11 13 %".

# Write to File
As in bash, zsh uses redirection. That means if we want to write these numbers to a file named "abc.txt" we can do
```
list=(2 3 5 7 11 13)
for i in $list; do
  echo -n $i" ">>abc.txt
done
```
Then the content of the text file will be the same as the previous output.
The operator ">" writes the output to the file while ">>" appends the output to the file.

Writing output of a python script to the text file is also easy.
```
list=(2 3 5 7 11 13)
for I in $list; do
  echo -n $I" ">>abc.txt
  python print10times.py $i >> abc.txt
done
```

The content inside "abc.txt" is
```
2 2222222222
3 3333333333
5 5555555555
7 7777777777
11 11111111111111111111
13 13131313131313131313
```

My "print10times.py" is simply
```
import sys
a=sys.argv[1]
print(a*10)
```

# <a name="grid_search"></a>Grid Search

To do the grid search, we only need to modify the above code to have multiple for loops, and record the loss or accuracy of each model.

```
parameter_name="list"
parameter_name2="list2"

list="2 3 5 7 11 13"
list2="0.1 0.3"

for i ( $=list ); do
  for lr ( $=list2 ); do
    echo -n $i" "$lr" ">>abc.txt
    python last_loss.py $i >> abc.txt
  done
done

python render_grid.py $list $list2 $parameter_name $parameter_name2


```

Since I want to pass in the lists I have to "render_grid.py" for post data processing, I change the list into string. Then, I use "$=list" to do [expansion][2] in the for loop conditions.

In summary, the for loops go through every model with value in the parameter list and record each models' losses. Then we can use [heatmap][3] function to visualize which pair results in smallest loss. Here is what I do in "render_grid.py"

```
import sys
import matplotlib.pyplot as plt
import numpy as np

with open("abc.txt") as f:
    data=f.readlines()


float_data=[]
for index in range(len(data)):
    float_data.append([float(value) for value in data[index].split("\n")[0].split(" ")])

rows=list(map(float,sys.argv[1].split(" ")))
columns=list(map(float,sys.argv[2].split(" ")))

table=[]
index=0

for i in range(len(rows)):
    column=[]
    for j in range(len(columns)):
        column.append(float_data[index][2])
        print(index,float_data[index][2])
        index+=1
    table.append(column)

fig, ax = plt.subplots()
im = ax.imshow(table)

ax.set_xticks(np.arange(len(columns)))
ax.set_yticks(np.arange(len(rows)))
ax.set_xticklabels(columns)
ax.set_yticklabels(rows)
ax.set_xlabel(sys.argv[3])
ax.set_ylabel(sys.argv[4])

for i in range(len(rows)):
    for j in range(len(columns)):
        text = ax.text(j, i, "%.2f"%table[i][j],
                       ha="center", va="center", color="w")

ax.set_title("loss")
fig.tight_layout()
plt.show()

```
Basically, it reads "abc.txt" and generates a table that can be used to produce the heat map

<center><img src="heatmap.png" alt="heat map of the grid search" width="500"/></center>

I generated the loss randomly here. If these are the real losses I got, a reasonable choice of (parameter, parameter2) from (list,list2) is the minima (0.1,7.0).

[1]: https://scikit-learn.org/stable/modules/grid_search.html
[2]: [zsh: 14 Expansion](http://zsh.sourceforge.net/Doc/Release/Expansion.html#Parameter-Expansion)
[3]:[Creating annotated heatmaps — Matplotlib 3.1.2 documentation](https://matplotlib.org/3.1.1/gallery/images_contours_and_fields/image_annotated_heatmap.html)
