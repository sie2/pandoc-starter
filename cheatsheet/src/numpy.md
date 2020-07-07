---
title: Python
topic: NumPy
author: Emerson Sie
url: https://github.com/sie2
landscape: true
maketitle: false
toc: false
...

# Arrays {-}

To and from Python lists:
:   \ 

```python
x = np.array([1,2,3]) # from Python list
y = x.tolist()        # to Python list
```

Working with files:
:   \  

```python
x = np.genfromtxt('file.csv', delimiter=',')
x = np.savetxt('file.csv', a, delimiter=',')
```

Filled arrays:
:   \  

```python
np.zeros(3)
np.ones(3,4)
np.full((2,3),8)     # filled array
np.eye(5)            # 5x5 identity matrix
np.linspace(0,100,6) # linear spacing
np.arange(0,10,3)    # start, stop, step
```

Array properties:
:   \  

```python
x.size                # # of elements in x
x.ndim                # # of axes in x
x.shape               # shape of x
x.dtype               # data type of x
y = x.astype(int)     # convert data type
```

Views, deep copying:

```python
y = x.view()          # view of array x
y = x.copy()          # copy of array x
```

Reshaping, resizing:
:   \  

```python
x.ravel()            # view of x as 1D
x.flatten()          # copy of x as 1D
x.T                  # view of x transposed
x.swapaxes(0,1)      # copy of x transposed
x.reshape((3,4))     # view with shape (3,4)
x.resize((3,4))      # resize array in place
np.resize(x,(3,4))   # resize array by copy
```

Concatenate, stack, split, squeeze:
:   \  

```python
np.concatenate((x,y), axis=0) # existing axis
np.stack((x,y), axis=1)     # new axis
np.split(x, 3, axis=0)      # equal size split
np.split(x, [2,3,5], axis=0) # custom intervals
x.squeeze() # view of x with unit dims removed
```

Broadcasting rules:
:   \

> When operating on two arrays, NumPy compares their
> shapes element-wise. It starts with the trailing
> dimensions and works its way foward. 
> 
> Two dimensions are compatible when 
> 
> (@) they are equal, or
> (@) one of them is 1

![Broadcasting](img/broadcasting.png){ width=30% }\


Array slicing:
:   \  

```python
x[::-1]      # reversed view of x
x[:5]        # first 5 elements of x
x[5:]        # after index 5 inclusive
x[4:7]       # 4 to 7 noninclusive
x[1::2]  # every other elem, idx 1 onwards
x[5::-2] # every other elem, idx 5 down to 0
x[:,np.newaxis] # convert to column vector
```

Boolean indexing:
:   \  

```python
x > 5       # boolean mask of indices > 5
x[x > 5]    # array of elements > 5
```

Fancy indexing:
:   \  

```python
# 1D array of elems at idx 3,7,4
x[[3,7,4]]  
# 1D array of elems at idx (0,2),(1,1),(2,3)
x[[0,1,2],[2,1,3]]
# 2D array of elems with broadcast indexing
x[row[:,np.newaxis],col]
```

# Linear Algebra {-}

```python
np.dot(a,b)                 # dot product
np.inner(a,b)               # inner product
np.outer(a,b)               # outer product
np.matmul(a,b)              # matrix mult
np.kron(a,b)                # kronecker product
np.linalg.matrix_power(a,n) # matrix power
np.linalg.svd(a)            # SVD
np.linalg.eig(a)            # eigendecomp
```

# Random {-}

```python
np.random.rand(4,5)  # 4x5 floats in [0,1]
np.random.randint(5, size=(2,3)) # in [0,5)
```

# Statistics {-}

```python
x.sum(axis=0)    # sum
x.mean(axis=0)   # mean
x.median(axis=0) # median
x.var(axis=0)    # variance
x.std(axis=0)    # standard deviation
x.min(axis=0)    # minimum
x.max(axis=0)    # maximum
x.argmin(axis=0) # index of minimum
x.argmax(axis=0) # index of maximum
x.any(axis=0)    # true iff any nonzero
x.all(axis=0)    # true iff all nonzero
```

 <!--
```cpp
int main() {
    return 0;
}
```

\begin{tikzpicture}[join=round]
    \tikzstyle{conefill} = [fill=blue!20,fill opacity=0.8]
    \tikzstyle{ann} = [fill=white,font=\footnotesize,inner sep=1pt]
    \tikzstyle{ghostfill} = [fill=white]
         \tikzstyle{ghostdraw} = [draw=black!50]
    \filldraw[conefill](-.775,1.922)--(-1.162,.283)--(-.274,.5)
                        --(-.183,2.067)--cycle;
    \filldraw[conefill](-.183,2.067)--(-.274,.5)--(.775,.424)
                        --(.516,2.016)--cycle;
    \filldraw[conefill](.516,2.016)--(.775,.424)--(1.369,.1)
                        --(.913,1.8)--cycle;
    \filldraw[conefill](-.913,1.667)--(-1.369,-.1)--(-1.162,.283)
                        --(-.775,1.922)--cycle;
    \draw(1.461,.107)--(1.734,.127);
    \draw[arrows=<->](1.643,1.853)--(1.643,.12);
    \filldraw[conefill](.913,1.8)--(1.369,.1)--(1.162,-.283)
                        --(.775,1.545)--cycle;
    \draw[arrows=->,line width=.4pt](.274,-.5)--(0,0)--(0,2.86);
    \draw[arrows=-,line width=.4pt](0,0)--(-1.369,-.1);
    \draw[arrows=->,line width=.4pt](-1.369,-.1)--(-2.1,-.153);
    \filldraw[conefill](-.516,1.45)--(-.775,-.424)--(-1.369,-.1)
                        --(-.913,1.667)--cycle;
    \draw(-1.369,.073)--(-1.369,2.76);
    \draw(1.004,1.807)--(1.734,1.86);
    \filldraw[conefill](.775,1.545)--(1.162,-.283)--(.274,-.5)
                        --(.183,1.4)--cycle;
    \draw[arrows=<->](0,2.34)--(-.913,2.273);
    \draw(-.913,1.84)--(-.913,2.447);
    \draw[arrows=<->](0,2.687)--(-1.369,2.587);
    \filldraw[conefill](.183,1.4)--(.274,-.5)--(-.775,-.424)
                        --(-.516,1.45)--cycle;
    \draw[arrows=<-,line width=.4pt](.42,-.767)--(.274,-.5);
    \node[ann] at (-.456,2.307) {$r_0$};
    \node[ann] at (-.685,2.637) {$r_1$};
    \node[ann] at (1.643,.987) {$h$};
    \path (.42,-.767) node[below] {$x$}
        (0,2.86) node[above] {$y$}
        (-2.1,-.153) node[left] {$z$};
    % Second version of the cone
    \begin{scope}[xshift=3.5cm]
    \filldraw[ghostdraw,ghostfill](-.775,1.922)--(-1.162,.283)--(-.274,.5)
                                   --(-.183,2.067)--cycle;
    \filldraw[ghostdraw,ghostfill](-.183,2.067)--(-.274,.5)--(.775,.424) 
                                   --(.516,2.016)--cycle;
    \filldraw[ghostdraw,ghostfill](.516,2.016)--(.775,.424)--(1.369,.1)
                                   --(.913,1.8)--cycle;
    \filldraw[ghostdraw,ghostfill](-.913,1.667)--(-1.369,-.1)--(-1.162,.283)
                                   --(-.775,1.922)--cycle;
    \filldraw[ghostdraw,ghostfill](.913,1.8)--(1.369,.1)--(1.162,-.283)
                                   --(.775,1.545)--cycle;
    \filldraw[ghostdraw,ghostfill](-.516,1.45)--(-.775,-.424)--(-1.369,-.1)
                                   --(-.913,1.667)--cycle;
    \filldraw[ghostdraw,ghostfill](.775,1.545)--(1.162,-.283)--(.274,-.5)
                                   --(.183,1.4)--cycle;
    \filldraw[fill=red,fill opacity=0.5](-.516,1.45)--(-.775,-.424)--(.274,-.5)
                                         --(.183,1.4)--cycle;
    \fill(-.775,-.424) circle (2pt);
    \fill(.274,-.5) circle (2pt);
    \fill(-.516,1.45) circle (2pt);
    \fill(.183,1.4) circle (2pt);
    \path[font=\footnotesize]
            (.913,1.8) node[right] {$i\hbox{$=$}0$}
            (1.369,.1) node[right] {$i\hbox{$=$}1$};
    \path[font=\footnotesize]
            (-.645,.513) node[left] {$j$}
            (.228,.45) node[right] {$j\hbox{$+$}1$};
    \draw (-.209,.482)+(-60:.25) [yscale=1.3,->] arc(-60:240:.25);
    \fill[black,font=\footnotesize]
                    (-.516,1.45) node [above] {$P_{00}$}
                    (-.775,-.424) node [below] {$P_{10}$}
                    (.183,1.4) node [above] {$P_{01}$}
                    (.274,-.5) node [below] {$P_{11}$};
    \end{scope}
\end{tikzpicture}

-->
