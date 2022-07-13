---
title: "Test"
date: 2022-07-04T20:06:15-07:00
draft: true
math: true
---

Contents

1. [Code](#code)
2. [KaTeX](#katex)
3. [Tables](#tables)

## Code

```python
def my_function(x, y):
    """
    """
    return x + y**2
```

```R
my_function <- function(x, y) {
    x + y^2
}
```

```julia
function my_function(x, y)
    x + y^2
end
```

## KaTeX

Display mode

$$
\overline{x} = \frac{1}{n}\sum_{i}x_{i}
$$

Aligned environments

$$
\begin{equation}
\begin{aligned}
\min_{x_{i}, y_{i}, \lbrace G_{ij} \rbrace_{j \neq i}} \quad & c_{i}(\mathbf{x},
\mathbf{G}) \\\
\text{s.t.} \quad & E[v_{i}(y_{i})] \geq \underline{u}_{i}
\end{aligned}
\end{equation}
$$

## Tables

| Left | Center | Right |
|------|:------:|------:|
| Foo  |  Bar   |   Baz |

