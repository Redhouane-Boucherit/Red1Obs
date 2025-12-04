
# 🧮 1. What Is a Congruential Generator?

A **congruential generator** produces a sequence of pseudorandom numbers using modular arithmetic of the form:

# ⭐ **Linear Congruential Generator (LCG)**

The most common type.

Xn+1=(aXn+c)mod  mX_{n+1} = (aX_n + c) \mod mXn+1​=(aXn​+c)modm

Where:

- **m** = modulus
    
- **a** = multiplier
    
- **c** = increment
    
- **X₀** = seed
    

### Output:

Un=XnmU_n = \frac{X_n}{m}Un​=mXn​​

---

# 🧩 2. Types of Congruential Generators

### **1. LCG (Linear Congruential Generator)**

General form: Xn+1=(aXn+c)mod  mX_{n+1} = (aX_n + c) \mod mXn+1​=(aXn​+c)modm

### **2. MCG (Multiplicative Congruential Generator)**

Special case of LCG:

c=0c = 0c=0

### **3. Lehmer Generator (Multiplicative with prime modulus)**

Xn+1=gXnmod  pX_{n+1} = g X_n \mod pXn+1​=gXn​modp

### **4. Combined LCG**

Multiple LCGs combined to improve quality (e.g., L’Ecuyer’s generator “MRG32k3a”).

---

# 📌 3. Example of a Simple LCG

Let’s choose:

- m = 16
    
- a = 5
    
- c = 3
    
- X₀ = 7
    

Compute next few numbers:

1. X1=(5⋅7+3)mod  16=38mod  16=6X_1 = (5·7 + 3) \mod 16 = 38 \mod 16 = 6X1​=(5⋅7+3)mod16=38mod16=6
    
2. X2=(5⋅6+3)mod  16=33mod  16=1X_2 = (5·6 + 3) \mod 16 = 33 \mod 16 = 1X2​=(5⋅6+3)mod16=33mod16=1
    
3. X3=(5⋅1+3)mod  16=8mod  16=8X_3 = (5·1 + 3) \mod 16 = 8 \mod 16 = 8X3​=(5⋅1+3)mod16=8mod16=8
    

Sequence: **7, 6, 1, 8, …**

---

# 🟢 4. Advantages

### ✔ Very fast

One of the fastest PRNGs—ideal for simulations, Monte Carlo, or FPGA/embedded use.

### ✔ Small footprint

Requires only a multiplier, adder, and modulo operation.

### ✔ Easy to implement in hardware (FPGA)

### ✔ Good for:

- Simulations
    
- Embedded systems
    
- Games
    
- Statistical applications
    
- Monte Carlo methods (non-secure)
    

---

# 🔴 5. Disadvantages

### ❌ Not Cryptographically Secure

LCGs are predictable:

- After observing a few outputs, an attacker can calculate **a**, **c**, **m**, and **seed**.
    
- Sequence is linear and thus statistically weak.
    

### ❌ Patterns in higher dimensions

Even a “good” LCG forms **hyperplanes** in multidimensional space.

### ❌ Short periods

Maximum period is m.

---

# ❗ 6. LCG and NIST Standards

### ✔ Approved for cryptography?

**NO.**  
LCGs fail NIST cryptographic requirements.

### NIST Standards rejecting LCGs:

#### ❌ **NIST SP 800-90A**

Does not include LCGs in approved DRBGs.

#### ❌ **NIST SP 800-22 tests**

LCGs fail many randomness tests unless carefully chosen.

#### ❌ **NIST SP 800-90B entropy tests**

LCGs have **zero entropy** (fully deterministic).

➡️ **LCGs cannot be used in any FIPS 140-3 cryptographic module.**

---

# 🛠️ 7. Congruential Generators in FPGA Hardware

LCGs are extremely easy to implement:

### Hardware structure:

`register X multiplier * a adder + c mod m (usually bit mask if m = 2^k)`

### For FPGAs:

- Choosing **m = 2^n** simplifies modulus
    
- Implemented in <10 LUTs
    

But again—**not secure**.

---

# 📘 8. High-Quality Congruential Generators

Modern improved variants:

|Generator|Notes|
|---|---|
|**MRG32k3a (L’Ecuyer)**|Very good quality, long period|
|**PCG (Permuted Congruential Generator)**|State-of-art non-crypto PRNG|
|**MWC (Multiply-with-Carry)**|Better randomness|
|**Xorshift / Xoshiro**|Not congruential but similar hardware class|

Still: **non-cryptographic use only**.

---

# 🎯 Summary

|Aspect|LCG|
|---|---|
|Speed|⭐⭐⭐⭐⭐|
|Hardware cost|⭐⭐⭐⭐⭐|
|Randomness quality|⭐⭐|
|Cryptographically secure|❌ No|
|NIST-Approved RNG|❌ No|
|Good for FPGA TRNG?|❌ No (it's a PRNG)|

✔ Simple  
✔ Fast  
❌ Not secure  
❌ Not NIST-approved for cryptography