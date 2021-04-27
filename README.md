# iFood MLOps Readme

> Thiw repository is the documentation of my solution for the iFood ML Engineer test.

## 1. Case Solution

TODO

## 2. Going to the Cloud

TODO

## 3. Bonus

What a fun! I have used the [Radare2](https://github.com/radareorg/radare2) software to reverse engineer the binaries.
The usage of C standard library to process strings (the famous *string.h*) speeded up the hacking process since it 
helped to understand the expected input. Also, the data area was full of hints since comparisons were made against data 
stored on it.

### 3.1. Level 01

The easiest one. The main code area used *string.h* to compare the input string with the one stored on the data area. 
Just had to take into account the (little) endianness used by the x86 processor.

> **Solution:** 

 - 1F00d{P13c3_0f_C4k3}

### 3.2. Level 01

This one required a two step solution. The first was to find out that the entry must be 21 characters long, again the 
*string.h* lib *len* method made things easier. The second one was way more tougher. It resembled a XOR encryption 
process and I had to use brute force strategy to break it with minor tweaks to speed it up. The key was to find out the 
periodic characteristic of the input. The code bellow took 4 seconds to run o my machine, a Intel(R) Core(TM) i7-8665U 
CPU @ 1.90GHz with 16 GB of memory.

```python
def main(a, b, c):

    chars = [0] * 18
    chars = chars + [a, b, c]

    if len(chars) == 0x15:
        f = 0x1337
        for char in chars:
            temp = char * int(0x1234)
            f = f ^ temp
        if f == 0xa48b7:
            print([hex(char) for char in chars])
            return True
        else:
            return False


if __name__ == '__main__':

    for i in range(0x7e):
        for j in range(0x7e):
            for k in range(0x7e):
                r = main(i, j, k)
                if r:
                    break
```

> **Solutions:** Many possible solutions.

 - BY{BY{BY{BY{BY{BY{BY{
 - B{YB{YB{YB{YB{YB{YB{Y
 - YB{YB{YB{YB{YB{YB{YB{
 - Y{BY{BY{BY{BY{BY{BY{B
 - {YB{YB{YB{YB{YB{YB{YB
 - {BY{BY{BY{BY{BY{BY{BY

### 3.3. Level 03

Haven't had the opportunity to try it out. :disappointed:

