

![[Pasted image 20251203214323.png]]
![[Pasted image 20251203214349.png]]
![[Pasted image 20251203214419.png]]
# Frequency Test
[Youtube](https://www.youtube.com/watch?v=jARtJZ7R0mo)
![[Pasted image 20251204085511.png]]

# Maurer's Universal Statistical test
[Youtube](https://www.youtube.com/watch?v=jARtJZ7R0mo)
![[Pasted image 20251204090312.png]]

![[Pasted image 20251204090534.png]]
![[Pasted image 20251204090710.png]]

![[Pasted image 20251204091433.png]]


![[Pasted image 20251204085937.png]]
![[Pasted image 20251204092314.png]]

# Test Methodes in Arabic
[Youtube](https://www.youtube.com/watch?v=xLI0o_6eDys)

![[Pasted image 20251204102000.png]]

![[Pasted image 20251204102454.png]]


# Which standard is required for FPGA TRNG approval?

## **Required NIST Standards for Approving an FPGA TRNG**

To get a TRNG _approved for cryptographic use_, the **mandatory** standards are:

## ⭐ **1. NIST SP 800-90B — Entropy Source Requirements (MANDATORY)**

This is the **primary and required** standard for certifying any TRNG (hardware entropy source).

It defines:

### ✔ Required entropy tests

- Startup tests
    
- Continuous health tests
    
- Entropy estimation methods
    
- Predictability requirements
    
- Noise source model
    
- Conditioning function requirements
    

### ✔ Output requirements

A TRNG must **demonstrate a minimum entropy rate** and pass the statistical validation prescribed in 90B.

➡️ **If your FPGA TRNG does not pass NIST 800-90B entropy-source validation, it cannot be certified.**

---

## ⭐ **2. NIST SP 800-90C — Full RNG Construction (MANDATORY for full validation)**

90C specifies how to combine:

- **Entropy source (TRNG)**
    
- **DRBG (from 800-90A)**
    
- **Conditioning functions (SHA-2, AES, etc.)**
    

to create a **NIST-approved RNG subsystem**.

If you're doing **full module approval** (FIPS submission), 90C rules **must** be followed.

---

## ⭐ **3. NIST SP 800-90A — DRBG Requirement (MANDATORY for FIPS systems)**

If your TRNG feeds a DRBG (common in cryptographic systems):

- CTR_DRBG
    
- HMAC_DRBG
    
- Hash_DRBG
    

Then 90A applies.

---

## ❗Important Note

### **NIST SP 800-22 is _NOT_ sufficient and is _NOT_ required.**

800-22 is only a _statistical randomness test suite_, useful for research and initial debugging.  
It **cannot** approve a TRNG for cryptographic use.

---

## 🔐 **If seeking FIPS 140-3 Certification**

Your TRNG must comply with:

### ✔ FIPS 140-3

(cryptographic module validation)

### ✔ NIST SP 800-90B

(entropy source validation)

### ✔ NIST SP 800-90C

(overall RNG subsystem)

### ✔ NIST SP 800-90A (if DRBG included)

FIPS 140-3 labs **will reject** designs tested only with SP 800-22.

---

## 🎯 Summary (what you MUST use)

|Approval Goal|Required Standards|
|---|---|
|Use TRNG in cryptographic product|**NIST 800-90B**|
|Full RNG subsystem compliance|**NIST 800-90A/B/C**|
|FIPS 140-3 certification|**800-90A/B/C + FIPS 140-3**|
|Simple randomness testing|(Optional) 800-22|

✔ **800-90B is the key standard for FPGA TRNG approval.**  
✔ **800-22 alone is not accepted.**
