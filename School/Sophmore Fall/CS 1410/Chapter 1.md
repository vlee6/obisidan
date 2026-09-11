### Levels of Abstraction

|                      |                                                                                                       |
| -------------------- | ----------------------------------------------------------------------------------------------------- |
| **Physics**          | How electrons move around in devices                                                                  |
| **Device**           | ie. transistors                                                                                       |
| **Analog Circuits**  | Collections of devices that handle analog signals, ie. op-amps                                        |
| **Digital Circuits** | Collections of devices that handle digital signals                                                    |
| **Logic**            | ie. adders and memories from digital circuits                                                         |
| **Architecture**     | ie. Intel's x86, which defines an instruction set and registers                                       |
| **Operating System** | Software, handles low level details like accessing memory or displaying to screens (think of drivers) |
| **Programs**         | The stuff we write in Python or C++                                                                   |

- Hierarchy: divide a system into modules, divide those modules into pieces that are easy to understand
- Modularity: make sure modules can easily connect to each other
- Regularity: modules should be able to be reused many times; there shouldn't be a unique module for everything

### Binary and Hexidecimal
$$
10110_2=1*2^4+0*2^3+1*2^2+1*2^1+1*2^0=22_{10}
$$
$$
2ED_{16}=2*16^2+14*16^1+13*16^0=749_{10}
$$
Left most value is the most significant, right most is the least significant.

### Bytes
- Eight bits is called a **byte**
- Four bits or half a byte is called a **nibble**
- Word size is dependent on architecture, 64-bit processors have 64 bit words or 8 byte words.

### Two's Complement
Way to represent negative numbers that still works with binary addition. An interesting property of Two's complement is that if the most signficant (left most) bit is $1$, the number is negative and vice versa.

Given a number $x$ represented in binary, to find $-x$, simply:
1. Flip all the bits
2. Add binary 1 (ie. 0001 in 4-bits)

```
5 = 0 1 0 1
flip = 1 0 1 0
add one = 1 0 1 0 = -5

  0 1 0 1         (5)
+ 1 0 1 1       + (-5)
---------       ------
1 0 0 0 0          0
^
|
Overflowed out
```

To extend a two's complement number to more bits, just repeat the most significant digit (sign bit).

| System           | Range, $N$ bits       |
| ---------------- | --------------------- |
| Unsigned         | $[0, 2^N-1]$          |
| Two's Complement | $-2^{N-1}, 2^{N-1}-1$ |

### Logic Gates
**NOT** $Y=\bar{A}$
- Takes one input, returns one output, inverts it

**BUF** $Y=A$
- Takes one input, returns one output, does nothing to it

**AND** $Y=AB$
- Takes two inputs, returns one output. $Y$ is true if and only if both $A$ and $B$ are true

**OR** $Y=A+B$
- Takes two inputs, returns one output. $Y$ is true if either $A$ or $B$ is true.

**XOR** $Y=A \oplus B$
- Takes two inputs, returns one output. $Y$ is true if only one of $A$ or $B$ is true, false if BOTH are true.

### Voltages and Logic Levels
0V is ground and $V_{DD}$ is 5V or 3.3V or even lower.
![[Pasted image 20260908152315.png]]
Different logic families have different output/input highs and output/input lows. We don't want inputs to fall into the forbiggen zone since we won't know whether they're be HIGH or LOW.