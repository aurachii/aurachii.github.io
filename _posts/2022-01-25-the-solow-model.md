## The Solow Model (I)

### The Production Function

###  Law for the Evolution of Capital

### The Savings Rule

### Equilibrium

### Code

```python
%matplotlib inline
import numpy as np
import matplotlib.pyplot as plt
plt.rcParams['figure.figsize'] = (10,6)


class solow:

    def __init__(self,n=0.05,s=0.25,δ=0.1,α=0.3,z=2.0,k=1.0):

      self.n,self.s,self.δ,self.α,self.z=n,s,δ,α,z
      self.k=k

    def h(self):
        n, s, δ, α, z = self.n, self.s, self.δ, self.α, self.z
        return (s * z * self.k**α + (1 - δ) * self.k) / (1 + n)

    def update(self):
        self.k =  self.h()

    def steady_state(self):
        n, s, δ, α, z = self.n, self.s, self.δ, self.α, self.z
        return ((s * z) / (n + δ))**(1 / (1 - α))

    def generate_sequence(self, t):
        path = []

        for i in range(t):
            path.append(self.k)
            self.update()
        return path

#Compute time series from five different initial conditions

s1 = solow()
s2 = solow(k=8.0)
s3 = solow(k=0.5)
s4= solow(k=0.1)
s5= solow(k=4.0)

T = 60
fig, ax = plt.subplots(figsize=(9, 6))

ax.plot([s1.steady_state()]*T, 'k-', label='steady state')

for s in s1, s2, s3, s4,s5:
    lb = f'capital series from initial state {s.k}'
    ax.plot(s.generate_sequence(T), 'o-', lw=2, alpha=0.6, label=lb)

ax.set_xlabel('$t$', fontsize=14)
ax.set_ylabel('$k_t$', fontsize=14)
ax.legend()
plt.show()
```


![](https://i.imgur.com/3k1mE17.png)
