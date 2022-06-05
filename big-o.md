---
description: Understanding time and space complexity
---

# BigO

A notation to formalise the efficiency of code (how much time does it take and how much space does it take in memory). It's a general way of counting these values, because you'll see we're not really interested in exact details, simply broad trends.

We are generally talking about how the time and space increase as inputs to our algorithms increase. Or put a different way, it describes the relationship between the input and the time it takes to run, and how one changes when the other changes.

#### Time complexity

When we're talking about time specifically there are a few common relationships (there are more than these though!)

| Relationship                  | Description                                                                                                                                                                                                                                                                                     |
| ----------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Constant time $$f(n) = 1$$    | As the size of the input grows, time doesn't change at all. It remains constant regardless of how large the input is.                                                                                                                                                                           |
| Linear time $$f(n) = n$$      | As the size of the input grow, time increases at the same rate. They have a linear relationship, and the increase ration remains the same. If you're thinking about it in terms of line graphs, the gradient remains constant.                                                                  |
| Log time $$f(n) = log n$$     | As the size of the input grows, time increases following a logarithmic relationship (a curve that gradually flattens off). You'll see examples of this as you learn more about the different algorithms, but see below for a graph to show you the relationship.                                |
| Quadratic time $$f(n) = n^2$$ | As the size of the input grows, the time increases following a quadratic relationship. This is generally considered a bad thing! For example if you increase the size of the input by 5, the time increases by 25. You'll see this often when using nested for loops so keep an eye out for it! |

Below is an example of a log x graph for those who haven't seen one or studied maths before.

{% embed url="https://upload.wikimedia.org/wikipedia/commons/thumb/1/17/Binary_logarithm_plot_with_ticks.svg/1200px-Binary_logarithm_plot_with_ticks.svg.png" %}
Log graph example
{% endembed %}
