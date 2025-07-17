# Unit II: Computer Arithmetic

## 0. Syllabus
Computer Arithmetic: Addition and Subtraction, Tools Compliment Representation, Signed Addition and Subtraction, Multiplication and division, Booths Algorithm, Division Operation, Floating Point Arithmetic Operation. design of Arithmetic unit

## 1. Introduction to Computer Arithmetic

### Number Systems and Computer Representation
```
┌─────────────────────────────────────────────────────────────┐
│                 COMPUTER ARITHMETIC OVERVIEW               │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Computer Arithmetic: Mathematical operations performed     │
│  by computers using binary number system                   │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                NUMBER SYSTEMS                           │ │
│  │                                                         │ │
│  │  ┌─────────────┐ ┌─────────────┐ ┌─────────────┐        │ │
│  │  │   DECIMAL   │ │   BINARY    │ │     HEX     │        │ │
│  │  │   Base 10   │ │   Base 2    │ │   Base 16   │        │ │
│  │  │             │ │             │ │             │        │ │
│  │  │   0-9       │ │    0,1      │ │   0-9,A-F   │        │ │
│  │  │             │ │             │ │             │        │ │
│  │  │    15       │ │    1111     │ │     F       │        │ │
│  │  │    25       │ │   11001     │ │    19       │        │ │
│  │  │   255       │ │ 11111111    │ │    FF       │        │ │
│  │  └─────────────┘ └─────────────┘ └─────────────┘        │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                BINARY ARITHMETIC                        │ │
│  │                                                         │ │
│  │  Why Binary in Computers:                              │ │
│  │  • Digital circuits work with ON/OFF states            │ │
│  │  • Easy to implement with electronic switches          │ │
│  │  • Reliable and noise-resistant                        │ │
│  │  • Simple logic operations                             │ │
│  │                                                         │ │
│  │  Binary Digit (Bit): 0 or 1                           │ │
│  │  Byte: 8 bits                                          │ │
│  │  Word: Multiple bytes (16, 32, 64 bits)                │ │
│  │                                                         │ │
│  │  Range for n-bit binary:                               │ │
│  │  Unsigned: 0 to 2^n - 1                               │ │
│  │  Signed: -2^(n-1) to 2^(n-1) - 1                      │ │
│  └─────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

### Binary Representation Concepts
```
┌─────────────────────────────────────────────────────────────┐
│                BINARY REPRESENTATION                       │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                UNSIGNED INTEGERS                        │ │
│  │                                                         │ │
│  │  8-bit unsigned representation:                        │ │
│  │                                                         │ │
│  │  Bit Position: │ 7│ 6│ 5│ 4│ 3│ 2│ 1│ 0│              │ │
│  │  Bit Weight:   │128│64│32│16│ 8│ 4│ 2│ 1│              │ │
│  │                                                         │ │
│  │  Example: 150₁₀                                        │ │
│  │  Binary:      │ 1│ 0│ 0│ 1│ 0│ 1│ 1│ 0│              │ │
│  │  Calculation: 128 + 16 + 4 + 2 = 150                  │ │
│  │                                                         │ │
│  │  Range: 0 to 255 (2⁸ - 1)                             │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                SIGNED INTEGERS                          │ │
│  │                                                         │ │
│  │  Three representations for signed numbers:             │ │
│  │                                                         │ │
│  │  1. SIGN-MAGNITUDE:                                    │ │
│  │     MSB = sign bit (0=+, 1=-)                          │ │
│  │     Remaining bits = magnitude                          │ │
│  │                                                         │ │
│  │     +5: 0101    -5: 1101                              │ │
│  │     Range: -(2ⁿ⁻¹-1) to +(2ⁿ⁻¹-1)                    │ │
│  │                                                         │ │
│  │  2. ONE'S COMPLEMENT:                                  │ │
│  │     Negative = bitwise complement of positive          │ │
│  │                                                         │ │
│  │     +5: 0101    -5: 1010                              │ │
│  │     Range: -(2ⁿ⁻¹-1) to +(2ⁿ⁻¹-1)                    │ │
│  │                                                         │ │
│  │  3. TWO'S COMPLEMENT: (Most Common)                   │ │
│  │     Negative = one's complement + 1                    │ │
│  │                                                         │ │
│  │     +5: 0101    -5: 1011                              │ │
│  │     Range: -2ⁿ⁻¹ to +(2ⁿ⁻¹-1)                        │ │
│  │                                                         │ │
│  │  Note: Two's complement is the most common method for   │ │
│  │        representing signed integers in computers.         │ │
│  └─────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

## 2. Two's Complement Representation

### Understanding Two's Complement
```
┌─────────────────────────────────────────────────────────────┐
│                TWO'S COMPLEMENT SYSTEM                     │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Two's Complement: Standard method for representing         │
│  signed integers in computer systems                       │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │              CONVERSION PROCESS                         │ │
│  │                                                         │ │
│  │  To find -X in two's complement:                       │ │
│  │                                                         │ │
│  │  Step 1: Write X in binary                             │ │
│  │  Step 2: Invert all bits (one's complement)            │ │
│  │  Step 3: Add 1 to the result                           │ │
│  │                                                         │ │
│  │  Example: Find -13 in 8-bit two's complement           │ │
│  │                                                         │ │
│  │  Step 1: +13 = 00001101                               │ │
│  │  Step 2: Invert = 11110010                            │ │
│  │  Step 3: Add 1 = 11110011                             │ │
│  │                                                         │ │
│  │  Therefore: -13 = 11110011                             │ │
│  │                                                         │ │
│  │  Verification: 128+64+32+16+2+1 = 243                 │ │
│  │                256 - 243 = 13 ✓                       │ │
│  │                                                         │ │
│  │  Note: The two's complement representation is unique and  │ │
│  │        allows for a single representation of zero.       │ │
│  │        This is why it's the most common method.         │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                8-BIT EXAMPLES                           │ │
│  │                                                         │ │
│  │  Decimal │  Binary   │  Two's Complement               │ │
│  │  ────────┼───────────┼─────────────────────             │ │
│  │    +127  │ 01111111  │      01111111                   │ │
│  │    +1    │ 00000001  │      00000001                   │ │
│  │    +0    │ 00000000  │      00000000                   │ │
│  │    -1    │    ---    │      11111111                   │ │
│  │    -2    │    ---    │      11111110                   │ │
│  │   -127   │    ---    │      10000001                   │ │
│  │   -128   │    ---    │      10000000                   │ │
│  │                                                         │ │
│  │  Key Properties:                                       │ │
│  │  • Only one representation for zero                    │ │
│  │  • MSB indicates sign (0=+, 1=-)                      │ │
│  │  • Easy addition/subtraction                           │ │
│  │  • Range: -128 to +127 (8-bit)                        │ │
│  └─────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

### Advantages of Two's Complement
```
┌─────────────────────────────────────────────────────────────┐
│            ADVANTAGES OF TWO'S COMPLEMENT                  │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                KEY ADVANTAGES                           │ │
│  │                                                         │ │
│  │  1. UNIQUE ZERO REPRESENTATION:                        │ │
│  │     Only one bit pattern for zero (00000000)           │ │
│  │     Unlike sign-magnitude and one's complement         │ │
│  │                                                         │ │
│  │  2. SIMPLE ARITHMETIC:                                 │ │
│  │     Addition and subtraction use same circuit          │ │
│  │     No special handling for signs                      │ │
│  │                                                         │ │
│  │  3. OVERFLOW DETECTION:                                │ │
│  │     Easy to detect arithmetic overflow                 │ │
│  │     Based on carry bits and sign bits                  │ │
│  │                                                         │ │
│  │  4. HARDWARE EFFICIENCY:                               │ │
│  │     Simplest to implement in digital circuits          │ │
│  │     Reduces hardware complexity                        │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │               SIGN EXTENSION                            │ │
│  │                                                         │ │
│  │  When extending bit width, replicate the sign bit:     │ │
│  │                                                         │ │
│  │  8-bit to 16-bit extension examples:                   │ │
│  │                                                         │ │
│  │  +13: 00001101 → 0000000000001101                     │ │
│  │  -13: 11110011 → 1111111111110011                     │ │
│  │                                                         │ │
│  │  Rule: Copy MSB to all new positions                   │ │
│  │  • Positive numbers: pad with 0s                       │ │
│  │  • Negative numbers: pad with 1s                       │ │
│  │                                                         │ │
│  │  This preserves the numerical value                    │ │
│  └─────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

## 3. Binary Addition and Subtraction

### Binary Addition
```
┌─────────────────────────────────────────────────────────────┐
│                    BINARY ADDITION                         │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                BASIC RULES                              │ │
│  │                                                         │ │
│  │  Binary Addition Truth Table:                          │ │
│  │                                                         │ │
│  │   A │ B │ Cin │ Sum │ Cout                             │ │
│  │  ───┼───┼─────┼─────┼─────                             │ │
│  │   0 │ 0 │  0  │  0  │  0                              │ │
│  │   0 │ 0 │  1  │  1  │  0                              │ │
│  │   0 │ 1 │  0  │  1  │  0                              │ │
│  │   0 │ 1 │  1  │  0  │  1                              │ │
│  │   1 │ 0 │  0  │  1  │  0                              │ │
│  │   1 │ 0 │  1  │  0  │  1                              │ │
│  │   1 │ 1 │  0  │  0  │  1                              │ │
│  │   1 │ 1 │  1  │  1  │  1                              │ │
│  │                                                         │ │
│  │  Boolean Expressions:                                  │ │
│  │  Sum = A ⊕ B ⊕ Cin                                     │ │
│  │  Cout = AB + Cin(A ⊕ B)                                │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │               ADDITION EXAMPLES                         │ │
│  │                                                         │ │
│  │  Example 1: 13 + 11 (4-bit)                           │ │
│  │                                                         │ │
│  │    Carry:  0 1 1 1 0                                  │ │
│  │           ┌─────────────┐                              │ │
│  │      13:  │ 1 1 0 1 │                              │ │
│  │    + 11:  │ 1 0 1 1 │                              │ │
│  │           ├─────────────┤                              │ │
│  │      24:  │1 1 0 0 0│                              │ │
│  │           └─────────────┘                              │ │
│  │                                                         │ │
│  │  Step-by-step:                                         │ │
│  │  Position 0: 1+1 = 10₂ (0, carry 1)                   │ │
│  │  Position 1: 0+1+1 = 10₂ (0, carry 1)                 │ │
│  │  Position 2: 1+0+1 = 10₂ (0, carry 1)                 │ │
│  │  Position 3: 1+1+1 = 11₂ (1, carry 1)                 │ │
│  │                                                         │ │
│  │  Result: 11000₂ = 24₁₀ ✓                              │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                OVERFLOW DETECTION                       │ │
│  │                                                         │ │
│  │  Overflow occurs when result exceeds representable     │ │
│  │  range for the given number of bits                    │ │
│  │                                                         │ │
│  │  For Two's Complement Addition:                        │ │
│  │  Overflow = Cn ⊕ Cn-1                                  │ │
│  │  (where Cn = final carry, Cn-1 = carry into MSB)      │ │
│  │                                                         │ │
│  │  Example: 4-bit overflow                               │ │
│  │                                                         │ │
│  │      +7:  0111                                         │ │
│  │    + +2:  0010                                         │ │
│  │           ────                                         │ │
│  │      +9:  1001  (appears as -7!)                      │ │
│  │                                                         │ │
│  │  Carry into MSB = 0, Final carry = 0                  │ │
│  │  But result is wrong! Overflow occurred.              │ │
│  └─────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

### Binary Subtraction
```
┌─────────────────────────────────────────────────────────────┐
│                   BINARY SUBTRACTION                       │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │              SUBTRACTION METHODS                        │ │
│  │                                                         │ │
│  │  Method 1: Direct Subtraction                          │ │
│  │  • Borrow from higher-order bits when needed           │ │
│  │  • Complex to implement in hardware                    │ │
│  │                                                         │ │
│  │  Method 2: Addition of Two's Complement (Preferred)    │ │
│  │  • Convert A - B to A + (-B)                           │ │
│  │  • Use same addition hardware                          │ │
│  │  • Simpler and more efficient                          │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │        SUBTRACTION USING TWO'S COMPLEMENT              │ │
│  │                                                         │ │
│  │  Example: 13 - 11 using 4-bit arithmetic               │ │
│  │                                                         │ │
│  │  Step 1: Represent numbers                             │ │
│  │    13 = 1101₂                                          │ │
│  │    11 = 1011₂                                          │ │
│  │                                                         │ │
│  │  Step 2: Find two's complement of 11                   │ │
│  │    11 = 1011₂                                          │ │
│  │    Invert: 0100₂                                       │ │
│  │    Add 1: 0101₂ = -11                                  │ │
│  │                                                         │ │
│  │  Step 3: Add 13 + (-11)                               │ │
│  │                                                         │ │
│  │    Carry: 1 1 1 1 0                                   │ │
│  │          ┌─────────────┐                               │ │
│  │     13:  │ 1 1 0 1 │                               │ │
│  │   +(-11): │ 0 1 0 1 │                               │ │
│  │          ├─────────────┤                               │ │
│  │      2:  │1 0 0 1 0│                               │ │
│  │          └─────────────┘                               │ │
│  │               ↑                                        │ │
│  │            Discard carry                               │ │
│  │                                                         │ │
│  │  Result: 0010₂ = 2₁₀ ✓                                │ │
│  └─────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

## 4. Signed Addition and Subtraction

### Signed Arithmetic Operations
```
┌─────────────────────────────────────────────────────────────┐
│              SIGNED ADDITION & SUBTRACTION                 │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                ADDITION CASES                           │ │
│  │                                                         │ │
│  │  Case 1: Both numbers positive                         │ │
│  │    (+7) + (+3) = +10                                   │ │
│  │    0111 + 0011 = 1010                                  │ │
│  │    Result: 1010 = +10 ✓                               │ │
│  │                                                         │ │
│  │  Case 2: Both numbers negative                         │ │
│  │    (-7) + (-3) = -10                                   │ │
│  │    1001 + 1101 = 10110                                 │ │
│  │    Discard carry: 0110 = -10 ✓                        │ │
│  │                                                         │ │
│  │  Case 3: Positive + Negative (|+| > |−|)              │ │
│  │    (+7) + (-3) = +4                                    │ │
│  │    0111 + 1101 = 10100                                 │ │
│  │    Discard carry: 0100 = +4 ✓                         │ │
│  │                                                         │ │
│  │  Case 4: Positive + Negative (|+| < |−|)              │ │
│  │    (+3) + (-7) = -4                                    │ │
│  │    0011 + 1001 = 1100                                  │ │
│  │    Result: 1100 = -4 ✓                                │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │               OVERFLOW CONDITIONS                       │ │
│  │                                                         │ │
│  │  Overflow occurs in these cases:                       │ │
│  │                                                         │ │
│  │  1. Two positive numbers sum to negative result        │ │
│  │     (+) + (+) = (−) ← OVERFLOW                         │ │
│  │                                                         │ │
│  │  2. Two negative numbers sum to positive result        │ │
│  │     (−) + (−) = (+) ← OVERFLOW                         │ │
│  │                                                         │ │
│  │  NO overflow when:                                     │ │
│  │  • Adding numbers with different signs                 │ │
│  │  • Result within representable range                   │ │
│  │                                                         │ │
│  │  Example of overflow:                                  │ │
│  │    (+6) + (+3) in 4-bit system                        │ │
│  │    0110 + 0011 = 1001                                  │ │
│  │    Result: 1001 = -7 (Wrong!)                         │ │
│  │    Expected: +9 (not representable in 4-bit)          │ │
│  └─────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

### Hardware Implementation
```
┌─────────────────────────────────────────────────────────────┐
│               HARDWARE FOR SIGNED ARITHMETIC               │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │              ADDER/SUBTRACTOR CIRCUIT                   │ │
│  │                                                         │ │
│  │                                                         │ │
│  │     A          B                                       │ │
│  │     │          │                                       │ │
│  │     ▼          ▼                                       │ │
│  │  ┌─────┐  ┌─────────┐                                  │ │
│  │  │     │  │   XOR   │ ←── Sub/Add Control              │ │
│  │  │     │  │  Gates  │     (0=Add, 1=Sub)               │ │
│  │  │  A  │  └─────────┘                                  │ │
│  │  │     │       │                                       │ │
│  │  │     │       ▼                                       │ │
│  │  │     │   B' (or B)                                   │ │
│  │  │     │       │                                       │ │
│  │  │     ▼       ▼                                       │ │
│  │  │ ┌─────────────────┐                                 │ │
│  │  │ │   FULL ADDER    │                                 │ │
│  │  │ │     CHAIN       │                                 │ │
│  │  │ │                 │                                 │ │
│  │  │ │  FA → FA → FA   │                                 │ │
│  │  │ │   ↑    ↑    ↑   │                                 │ │
│  │  │ │ Carry Chain     │                                 │ │
│  │  │ └─────────────────┘                                 │ │
│  │  │          │                                          │ │
│  │  │          ▼                                          │ │
│  │  │       Result                                        │ │
│  │  │          │                                          │ │
│  │  │          ▼                                          │ │
│  │  │  ┌─────────────┐                                    │ │
│  │  │  │  OVERFLOW   │                                    │ │
│  │  │  │  DETECTION  │                                    │ │
│  │  │  └─────────────┘                                    │ │
│  │  └─────┘                                               │ │
│  │                                                         │ │
│  │  Operation:                                            │ │
│  │  • For addition: B passes through unchanged            │ │
│  │  • For subtraction: B is inverted (one's complement)   │ │
│  │  • Carry-in = 1 for subtraction (completes 2's comp)  │ │
│  └─────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

## 5. Multiplication and Division

### Multiplication
```
┌─────────────────────────────────────────────────────────────┐
│                    MULTIPLICATION                          │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                BASIC RULES                              │ │
│  │                                                         │ │
│  │  Multiplication Truth Table:                           │ │
│  │                                                         │ │
│  │   A │ B │ Product                                 │ │
│  │  ───┼───┼──────────────────────────────────────────────┤ │
│  │   0 │ 0 │ 0                                       │ │
│  │   0 │ 1 │ 0                                       │ │
│  │   1 │ 0 │ 0                                       │ │
│  │   1 │ 1 │ 1                                       │ │
│  │                                                         │ │
│  │  Boolean Expressions:                                  │ │
│  │  Product = A * B                                     │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │               MULTIPLICATION EXAMPLES                   │ │
│  │                                                         │ │
│  │  Example 1: 13 * 11 (4-bit)                           │ │
│  │                                                         │ │
│  │    Product: 143₁₀                                    │ │
│  │    Binary: 10001111                                 │ │
│  │                                                         │ │
│  │  Step-by-step:                                         │ │
│  │  Position 0: 1*1 = 1                                 │ │
│  │  Position 1: 1*1 = 1                                 │ │
│  │  Position 2: 0*1 = 0                                 │ │
│  │  Position 3: 0*1 = 0                                 │ │
│  │  Position 4: 1*1 = 1                                 │ │
│  │  Position 5: 1*1 = 1                                 │ │
│  │  Position 6: 1*1 = 1                                 │ │
│  │  Position 7: 1*1 = 1                                 │ │
│  │                                                         │ │
│  │  Result: 10001111₂ = 143₁₀ ✓                          │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                OVERFLOW DETECTION                       │ │
│  │                                                         │ │
│  │  Overflow occurs when result exceeds representable     │ │
│  │  range for the given number of bits                    │ │
│  │                                                         │ │
│  │  For Two's Complement Multiplication:                  │ │
│  │  Overflow = MSB of product is not the same as MSB of A │ │
│  │  and MSB of B                                         │ │
│  │                                                         │ │
│  │  Example: 4-bit overflow                              │ │
│  │                                                         │ │
│  │      +7:  0111                                        │ │
│  │    * +2:  0010                                        │ │
│  │           ────                                        │ │
│  │      +14: 1110  (appears as -2!)                      │ │
│  │                                                         │ │
│  │  MSB of product = 1, MSB of A = 0, MSB of B = 0         │ │
│  │  But result is wrong! Overflow occurred.               │ │
│  └─────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

### Division
```
┌─────────────────────────────────────────────────────────────┐
│                    DIVISION                                │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                BASIC RULES                              │ │
│  │                                                         │ │
│  │  Division Truth Table:                                 │ │
│  │                                                         │ │
│  │   A │ B │ Quotient │ Remainder                        │ │
│  │  ───┼───┼──────────┼──────────────────────────────────┤ │
│  │   0 │ 0 │    ---    │    ---                            │ │
│  │   0 │ 1 │    ---    │    ---                            │ │
│  │   1 │ 0 │    ---    │    ---                            │ │
│  │   1 │ 1 │   1        │   0                                │ │
│  │                                                         │ │
│  │  Boolean Expressions:                                  │ │
│  │  Quotient = A / B                                     │ │
│  │  Remainder = A % B                                     │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │               DIVISION EXAMPLES                         │ │
│  │                                                         │ │
│  │  Example 1: 13 / 3 (4-bit)                            │ │
│  │                                                         │ │
│  │    Quotient: 4₁₀                                     │ │
│  │    Binary: 1100                                     │ │
│  │                                                         │ │
│  │  Step-by-step:                                         │ │
│  │  Position 0: 1/3 = 0, Remainder = 1                    │ │
│  │  Position 1: 10/3 = 3, Remainder = 1                    │ │
│  │  Position 2: 100/3 = 3, Remainder = 1                    │ │
│  │  Position 3: 1000/3 = 3, Remainder = 1                    │ │
│  │                                                         │ │
│  │  Result: 1100₂ = 4₁₀ ✓                                │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                OVERFLOW DETECTION                       │ │
│  │                                                         │ │
│  │  Overflow occurs when divisor is zero                    │ │
│  │                                                         │ │
│  │  Example: 13 / 0                                    │ │
│  │                                                         │ │
│  │  Quotient: 13 / 0 = undefined                         │ │
│  │  Remainder: 13 % 0 = undefined                         │ │
│  │                                                         │ │
│  │  Result: undefined                                   │ │
│  └─────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

## 6. Booth's Algorithm

### Understanding Booth's Algorithm
```
┌─────────────────────────────────────────────────────────────┐
│                BOOTH'S ALGORITHM                            │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Booth's Algorithm: Efficient method for multiplying         │
│  signed integers in two's complement representation         │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                BOOTH'S ALGORITHM                        │ │
│  │                                                         │ │
│  │  Booth's Algorithm Steps:                              │ │
│  │                                                         │ │
│  │  1. Initialize: Set A = 0, Q = Multiplicand,            │ │
│  │              M = Multiplier, and Q0 = 0                 │ │
│  │  2. Check Q0Qn:                                        │ │
│  │     • If 00 or 11, shift AQ and Qn-1                    │ │
│  │     • If 01, add M to AQ and shift AQ and Qn-1           │ │
│  │     • If 10, subtract M from AQ and shift AQ and Qn-1     │ │
│  │  3. Repeat until all bits of multiplier are processed     │ │
│  │  4. Result is in AQ                                    │ │
│  │                                                         │ │
│  │  Example: Multiply -5 by 3 (4-bit two's complement)      │ │
│  │                                                         │ │
│  │  Step 1: Initialize: A = 0, Q = 1011, M = 1011, Q0 = 0    │ │
│  │  Step 2: Check Q0Qn: 11, shift AQ and Qn-1                │ │
│  │  Step 3: Check Q0Qn: 11, shift AQ and Qn-1                │ │
│  │  Step 4: Check Q0Qn: 10, subtract M from AQ and shift      │ │
│  │          AQ and Qn-1                                   │ │
│  │  Step 5: Result is in AQ = 11100110                       │ │
│  │                                                         │ │
│  │  Verification: -5 * 3 = -15                            │ │
│  │  15 in binary: 00001111                               │ │
│  │  -15 in two's complement: 11110001                     │ │
│  │  11100110 in two's complement: 11110001                │ │
│  │                                                         │ │
│  │  Result: 11100110 = -15 ✓                            │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                OVERFLOW DETECTION                       │ │
│  │                                                         │ │
│  │  Overflow occurs when result exceeds representable     │ │
│  │  range for the given number of bits                    │ │
│  │                                                         │ │
│  │  For Two's Complement Multiplication:                  │ │
│  │  Overflow = MSB of product is not the same as MSB of A │ │
│  │  and MSB of M                                         │ │
│  │                                                         │ │
│  │  Example: 4-bit overflow                              │ │
│  │                                                         │ │
│  │      +7:  0111                                        │ │
│  │    * +2:  0010                                        │ │
│  │           ────                                        │ │
│  │      +14: 1110  (appears as -2!)                      │ │
│  │                                                         │ │
│  │  MSB of product = 1, MSB of A = 0, MSB of M = 0         │ │
│  │  But result is wrong! Overflow occurred.               │ │
│  └─────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

## 7. Floating Point Arithmetic Operation

### Understanding Floating Point Representation
```
┌─────────────────────────────────────────────────────────────┐
│                FLOATING POINT REPRESENTATION               │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Floating Point Representation:                             │
│  Standard format for representing real numbers             │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                FLOATING POINT                         │ │
│  │                                                         │ │
│  │  Sign: 1 bit                                          │ │
│  │  Exponent: 8 bits                                     │ │
│  │  Mantissa: 23 bits                                    │ │
│  │                                                         │ │
│  │  Example: 3.14159 in floating point                   │ │
│  │  Binary: 0 10000001 00100100110011001100110           │ │
│  │                                                         │ │
│  │  Sign: 0 (positive)                                   │ │
│  │  Exponent: 10000001 (8+1 = 9)                        │ │
│  │  Mantissa: 00100100110011001100110                   │ │
│  │                                                         │ │
│  │  Value: 3.14159                                     │ │
│  │                                                         │ │
│  │  Range: 1.175494351E-38 to 3.402823466E+38            │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                OVERFLOW DETECTION                       │ │
│  │                                                         │ │
│  │  Overflow occurs when result exceeds representable     │ │
│  │  range for the given number of bits                    │ │
│  │                                                         │ │
│  │  For Floating Point Addition/Subtraction:               │ │
│  │  Overflow = Exponent overflow                          │ │
│  │                                                         │ │
│  │  Example: 1.0E+308 + 1.0E+308                        │ │
│  │                                                         │ │
│  │  Result: Infinity                                    │ │
│  │                                                         │ │
│  │  Overflow: Exponent overflow                          │ │
│  │                                                         │ │
│  │  Result: Infinity                                    │ │
│  └─────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

### Floating Point Addition
```
┌─────────────────────────────────────────────────────────────┐
│                FLOATING POINT ADDITION                      │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Floating Point Addition:                                   │
│  Aligning and adding mantissas                             │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                FLOATING POINT ADDITION                  │ │
│  │                                                         │ │
│  │  Steps:                                              │ │
│  │  1. Align the mantissas                               │ │
│  │  2. Add the mantissas                                 │ │
│  │  3. Normalize the result                              │ │
│  │                                                         │ │
│  │  Example: 1.0E+308 + 1.0E+308                        │ │
│  │                                                         │ │
│  │  Step 1: Align mantissas                               │ │
│  │  Step 2: Add mantissas                                 │ │
│  │  Step 3: Normalize result                              │ │
│  │                                                         │ │
│  │  Result: Infinity                                    │ │
│  │                                                         │ │
│  │  Overflow: Exponent overflow                          │ │
│  │                                                         │ │
│  │  Result: Infinity                                    │ │
│  └─────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

### Floating Point Subtraction
```
┌─────────────────────────────────────────────────────────────┐
│                FLOATING POINT SUBTRACTION                   │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Floating Point Subtraction:                                 │
│  Aligning and subtracting mantissas                         │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                FLOATING POINT SUBTRACTION               │ │
│  │                                                         │ │
│  │  Steps:                                              │ │
│  │  1. Align the mantissas                               │ │
│  │  2. Subtract the mantissas                             │ │
│  │  3. Normalize the result                              │ │
│  │                                                         │ │
│  │  Example: 1.0E+308 - 1.0E+308                        │ │
│  │                                                         │ │
│  │  Step 1: Align mantissas                               │ │
│  │  Step 2: Subtract mantissas                             │ │
│  │  Step 3: Normalize result                              │ │
│  │                                                         │ │
│  │  Result: 0.0E+308                                    │ │
│  │                                                         │ │
│  │  Overflow: Exponent underflow                          │ │
│  │                                                         │ │
│  │  Result: 0.0E+308                                    │ │
│  └─────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

### Floating Point Multiplication
```
┌─────────────────────────────────────────────────────────────┐
│                FLOATING POINT MULTIPLICATION                │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Floating Point Multiplication:                               │
│  Multiplying mantissas and adding exponents                   │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                FLOATING POINT MULTIPLICATION            │ │
│  │                                                         │ │
│  │  Steps:                                              │ │
│  │  1. Multiply mantissas                                │ │
│  │  2. Add exponents                                     │ │
│  │  3. Normalize the result                              │ │
│  │                                                         │ │
│  │  Example: 1.0E+308 * 1.0E+308                        │ │
│  │                                                         │ │
│  │  Step 1: Multiply mantissas                                │ │
│  │  Step 2: Add exponents                                     │ │
│  │  Step 3: Normalize result                              │ │
│  │                                                         │ │
│  │  Result: Infinity                                    │ │
│  │                                                         │ │
│  │  Overflow: Exponent overflow                          │ │
│  │                                                         │ │
│  │  Result: Infinity                                    │ │
│  └─────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

### Floating Point Division
```
┌─────────────────────────────────────────────────────────────┐
│                FLOATING POINT DIVISION                      │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Floating Point Division:                                    │
│  Dividing mantissas and subtracting exponents                 │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                FLOATING POINT DIVISION                  │ │
│  │                                                         │ │
│  │  Steps:                                              │ │
│  │  1. Divide mantissas                                   │ │
│  │  2. Subtract exponents                                 │ │
│  │  3. Normalize the result                              │ │
│  │                                                         │ │
│  │  Example: 1.0E+308 / 1.0E+308                        │ │
│  │                                                         │ │
│  │  Step 1: Divide mantissas                                   │ │
│  │  Step 2: Subtract exponents                                 │ │
│  │  Step 3: Normalize result                              │ │
│  │                                                         │ │
│  │  Result: 1.0E+0                                    │ │
│  │                                                         │ │
│  │  Overflow: Exponent underflow                          │ │
│  │                                                         │ │
│  │  Result: 1.0E+0                                    │ │
│  └─────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

## 8. Design of Arithmetic Unit

### Arithmetic Unit Components
```
┌─────────────────────────────────────────────────────────────┐
│                ARITHMETIC UNIT COMPONENTS                  │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                ADDER/SUBTRACTOR                        │ │
│  │                                                         │ │
│  │  Addition and subtraction hardware                      │ │
│  │  components                                        │ │
│  │                                                         │ │
│  │  ┌─────────────────────────────────────────────────────┐ │
│  │  │                ADDER/SUBTRACTOR                      │ │
│  │  │                                                         │ │
│  │  │  A          B                                       │ │
│  │  │  │          │                                       │ │
│  │  │  │          ▼                                       │ │
│  │  │  │  ┌─────┐  ┌─────────┐                              │ │
│  │  │  │  │     │  │   XOR   │ ←── Sub/Add Control          │ │
│  │  │  │  │     │  │  Gates  │     (0=Add, 1=Sub)           │ │
│  │  │  │  │  A  │  └─────────┘                              │ │
│  │  │  │  │     │       │                                   │ │
│  │  │  │  │     │       ▼                                   │ │
│  │  │  │  │     │   B' (or B)                               │ │
│  │  │  │  │     │       │                                   │ │
│  │  │  │  │     │     ▼                                     │ │
│  │  │  │  │  ┌─────────────────┐                             │ │
│  │  │  │  │  │   FULL ADDER    │                             │ │
│  │  │  │  │  │     CHAIN       │                             │ │
│  │  │  │  │  │                 │                             │ │
│  │  │  │  │  │  FA → FA → FA   │                             │ │
│  │  │  │  │  │   ↑    ↑    ↑   │                             │ │
│  │  │  │  │  │ Carry Chain     │                             │ │
│  │  │  │  │  └─────────────────┘                             │ │
│  │  │  │  │          │                                        │ │
│  │  │  │  │          ▼                                        │ │
│  │  │  │  │       Result                                        │ │
│  │  │  │  │          │                                        │ │
│  │  │  │  │          ▼                                        │ │
│  │  │  │  │  ┌─────────────┐                                    │ │
│  │  │  │  │  │  OVERFLOW   │                                    │ │
│  │  │  │  │  │  DETECTION  │                                    │ │
│  │  │  │  │  └─────────────┘                                    │ │
│  │  │  │  └─────┘                                               │ │
│  │  │  │                                                         │ │
│  │  │  │  Operation:                                            │ │
│  │  │  │  • For addition: B passes through unchanged            │ │
│  │  │  │  • For subtraction: B is inverted (one's complement)   │ │
│  │  │  │  • Carry-in = 1 for subtraction (completes 2's comp)  │ │
│  │  │  └─────────────────────────────────────────────────────┘ │
│  │  └─────────────────────────────────────────────────────────┘ │
│  │                                                             │ │
│  │  ┌─────────────────────────────────────────────────────────┐ │
│  │  │                MULTIPLIER/DIVIDER                       │ │
│  │  │                                                         │ │
│  │  │  Multiplication and division hardware                    │ │
│  │  │  components                                        │ │
│  │  │                                                         │ │
│  │  │  ┌─────────────────────────────────────────────────────┐ │
│  │  │  │                MULTIPLIER/DIVIDER                      │ │
│  │  │  │                                                         │ │
│  │  │  │  A          B                                       │ │
│  │  │  │  │          │                                       │ │
│  │  │  │  │          ▼                                       │ │
│  │  │  │  │  ┌─────┐  ┌─────────┐                              │ │
│  │  │  │  │  │     │  │   XOR   │ ←── Sub/Add Control          │ │
│  │  │  │  │  │     │  │  Gates  │     (0=Add, 1=Sub)           │ │
│  │  │  │  │  │  A  │  └─────────┘                              │ │
│  │  │  │  │  │     │       │                                   │ │
│  │  │  │  │  │     │       ▼                                   │ │
│  │  │  │  │  │     │   B' (or B)                               │ │
│  │  │  │  │  │     │       │                                   │ │
│  │  │  │  │  │     │     ▼                                     │ │
│  │  │  │  │  │  ┌─────────────────┐                             │ │
│  │  │  │  │  │  │   FULL ADDER    │                             │ │
│  │  │  │  │  │  │     CHAIN       │                             │ │
│  │  │  │  │  │  │                 │                             │ │
│  │  │  │  │  │  │  FA → FA → FA   │                             │ │
│  │  │  │  │  │  │   ↑    ↑    ↑   │                             │ │
│  │  │  │  │  │  │ Carry Chain     │                             │ │
│  │  │  │  │  │  └─────────────────┘                             │ │
│  │  │  │  │  │          │                                        │ │
│  │  │  │  │  │          ▼                                        │ │
│  │  │  │  │  │       Result                                        │ │
│  │  │  │  │  │          │                                        │ │
│  │  │  │  │  │          ▼                                        │ │
│  │  │  │  │  │  ┌─────────────┐                                    │ │
│  │  │  │  │  │  │  OVERFLOW   │                                    │ │
│  │  │  │  │  │  │  DETECTION  │                                    │ │
│  │  │  │  │  │  └─────────────┘                                    │ │
│  │  │  │  │  └─────┘                                               │ │
│  │  │  │  │                                                         │ │
│  │  │  │  │  Operation:                                            │ │
│  │  │  │  │  • For addition: B passes through unchanged            │ │
│  │  │  │  │  • For subtraction: B is inverted (one's complement)   │ │
│  │  │  │  │  • Carry-in = 1 for subtraction (completes 2's comp)  │ │
│  │  │  │  └─────────────────────────────────────────────────────┘ │
│  │  └─────────────────────────────────────────────────────────┘ │
│  │                                                             │ │
│  │  ┌─────────────────────────────────────────────────────────┐ │
│  │  │                FLOATING POINT UNIT                       │ │
│  │  │                                                         │ │
│  │  │  Floating point unit components                         │ │
│  │  │                                                         │ │
│  │  │  ┌─────────────────────────────────────────────────────┐ │
│  │  │  │                FLOATING POINT UNIT                      │ │
│  │  │  │                                                         │ │
│  │  │  │  Sign: 1 bit                                          │ │
│  │  │  │  Exponent: 8 bits                                     │ │
│  │  │  │  Mantissa: 23 bits                                    │ │
│  │  │  │                                                         │ │
│  │  │  │  Example: 3.14159 in floating point                   │ │
│  │  │  │  Binary: 0 10000001 00100100110011001100110           │ │
│  │  │  │                                                         │ │
│  │  │  │  Sign: 0 (positive)                                   │ │
│  │  │  │  Exponent: 10000001 (8+1 = 9)                        │ │
│  │  │  │  Mantissa: 00100100110011001100110                   │ │
│  │  │  │                                                         │ │
│  │  │  │  Value: 3.14159                                     │ │
│  │  │  │                                                         │ │
│  │  │  │  Range: 1.175494351E-38 to 3.402823466E+38            │ │
│  │  │  └─────────────────────────────────────────────────────┘ │
│  │  └─────────────────────────────────────────────────────────┘ │
│  │                                                             │ │
│  │  ┌─────────────────────────────────────────────────────────┐ │
│  │  │                OVERFLOW DETECTION                       │ │
│  │  │                                                         │ │
│  │  │  Overflow occurs when result exceeds representable     │ │
│  │  │  range for the given number of bits                    │ │
│  │  │                                                         │ │
│  │  │  For Floating Point Addition/Subtraction:               │ │
│  │  │  Overflow = Exponent overflow                          │ │
│  │  │                                                         │ │
│  │  │  Example: 1.0E+308 + 1.0E+308                        │ │
│  │  │                                                         │ │
│  │  │  Result: Infinity                                    │ │
│  │  │                                                         │ │
│  │  │  Overflow: Exponent overflow                          │ │
│  │  │                                                         │ │
│  │  │  Result: Infinity                                    │ │
│  │  └─────────────────────────────────────────────────────────┘ │
│  └─────────────────────────────────────────────────────────────┘
```

### Floating Point Addition
```
┌─────────────────────────────────────────────────────────────┐
│                FLOATING POINT ADDITION                      │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Floating Point Addition:                                   │
│  Aligning and adding mantissas                             │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                FLOATING POINT ADDITION                  │ │
│  │                                                         │ │
│  │  Steps:                                              │ │
│  │  1. Align the mantissas                               │ │
│  │  2. Add the mantissas                                 │ │
│  │  3. Normalize the result                              │ │
│  │                                                         │ │
│  │  Example: 1.0E+308 + 1.0E+308                        │ │
│  │                                                         │ │
│  │  Step 1: Align mantissas                               │ │
│  │  Step 2: Add mantissas                                 │ │
│  │  Step 3: Normalize result                              │ │
│  │                                                         │ │
│  │  Result: Infinity                                    │ │
│  │                                                         │ │
│  │  Overflow: Exponent overflow                          │ │
│  │                                                         │ │
│  │  Result: Infinity                                    │ │
│  └─────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

### Floating Point Subtraction
```
┌─────────────────────────────────────────────────────────────┐
│                FLOATING POINT SUBTRACTION                   │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Floating Point Subtraction:                                 │
│  Aligning and subtracting mantissas                         │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                FLOATING POINT SUBTRACTION               │ │
│  │                                                         │ │
│  │  Steps:                                              │ │
│  │  1. Align the mantissas                               │ │
│  │  2. Subtract the mantissas                             │ │
│  │  3. Normalize the result                              │ │
│  │                                                         │ │
│  │  Example: 1.0E+308 - 1.0E+308                        │ │
│  │                                                         │ │
│  │  Step 1: Align mantissas                               │ │
│  │  Step 2: Subtract mantissas                             │ │
│  │  Step 3: Normalize result                              │ │
│  │                                                         │ │
│  │  Result: 0.0E+308                                    │ │
│  │                                                         │ │
│  │  Overflow: Exponent underflow                          │ │
│  │                                                         │ │
│  │  Result: 0.0E+308                                    │ │
│  └─────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

### Floating Point Multiplication
```
┌─────────────────────────────────────────────────────────────┐
│                FLOATING POINT MULTIPLICATION                │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Floating Point Multiplication:                               │
│  Multiplying mantissas and adding exponents                   │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                FLOATING POINT MULTIPLICATION            │ │
│  │                                                         │ │
│  │  Steps:                                              │ │
│  │  1. Multiply mantissas                                │ │
│  │  2. Add exponents                                     │ │
│  │  3. Normalize the result                              │ │
│  │                                                         │ │
│  │  Example: 1.0E+308 * 1.0E+308                        │ │
│  │                                                         │ │
│  │  Step 1: Multiply mantissas                                │ │
│  │  Step 2: Add exponents                                     │ │
│  │  Step 3: Normalize result                              │ │
│  │                                                         │ │
│  │  Result: Infinity                                    │ │
│  │                                                         │ │
│  │  Overflow: Exponent overflow                          │ │
│  │                                                         │ │
│  │  Result: Infinity                                    │ │
│  └─────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

### Floating Point Division
```
┌─────────────────────────────────────────────────────────────┐
│                FLOATING POINT DIVISION                      │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Floating Point Division:                                    │
│  Dividing mantissas and subtracting exponents                 │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                FLOATING POINT DIVISION                  │ │
│  │                                                         │ │
│  │  Steps:                                              │ │
│  │  1. Divide mantissas                                   │ │
│  │  2. Subtract exponents                                 │ │
│  │  3. Normalize the result                              │ │
│  │                                                         │ │
│  │  Example: 1.0E+308 / 1.0E+308                        │ │
│  │                                                         │ │
│  │  Step 1: Divide mantissas                                   │ │
│  │  Step 2: Subtract exponents                                 │ │
│  │  Step 3: Normalize result                              │ │
│  │                                                         │ │
│  │  Result: 1.0E+0                                    │ │
│  │                                                         │ │
│  │  Overflow: Exponent underflow                          │ │
│  │                                                         │ │
│  │  Result: 1.0E+0                                    │ │
│  └─────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

### Floating Point Unit Components
```
┌─────────────────────────────────────────────────────────────┐
│                FLOATING POINT UNIT COMPONENTS               │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                FLOATING POINT UNIT                       │ │
│  │                                                         │ │
│  │  Floating point unit components                         │ │
│  │                                                         │ │
│  │  ┌─────────────────────────────────────────────────────┐ │
│  │  │                FLOATING POINT UNIT                      │ │
│  │  │                                                         │ │
│  │  │  Sign: 1 bit                                          │ │
│  │  │  Exponent: 8 bits                                     │ │
│  │  │  Mantissa: 23 bits                                    │ │
│  │  │                                                         │ │
│  │  │  Example: 3.14159 in floating point                   │ │
│  │  │  Binary: 0 10000001 00100100110011001100110           │ │
│  │  │                                                         │ │
│  │  │  Sign: 0 (positive)                                   │ │
│  │  │  Exponent: 10000001 (8+1 = 9)                        │ │
│  │  │  Mantissa: 00100100110011001100110                   │ │
│  │  │                                                         │ │
│  │  │  Value: 3.14159                                     │ │
│  │  │                                                         │ │
│  │  │  Range: 1.175494351E-38 to 3.402823466E+38            │ │
│  │  │                                                         │ │
│  │  │  Overflow occurs when result exceeds representable     │ │
│  │  │  range for the given number of bits                    │ │
│  │  │                                                         │ │
│  │  │  For Floating Point Addition/Subtraction:               │ │
│  │  │  Overflow = Exponent overflow                          │ │
│  │  │                                                         │ │
│  │  │  Example: 1.0E+308 + 1.0E+308                        │ │
│  │  │                                                         │ │
│  │  │  Result: Infinity                                    │ │
│  │  │                                                         │ │
│  │  │  Overflow: Exponent overflow                          │ │
│  │  │                                                         │ │
│  │  │  Result: Infinity                                    │ │
│  │  └─────────────────────────────────────────────────────┘ │
│  │  └─────────────────────────────────────────────────────────┘ │
│  │                                                             │ │
│  │  ┌─────────────────────────────────────────────────────────┐ │
│  │  │                OVERFLOW DETECTION                       │ │
│  │  │                                                         │ │
│  │  │  Overflow occurs when result exceeds representable     │ │
│  │  │  range for the given number of bits                    │ │
│  │  │                                                         │ │
│  │  │  For Floating Point Addition/Subtraction:               │ │
│  │  │  Overflow = Exponent overflow                          │ │
│  │  │                                                         │ │
│  │  │  Example: 1.0E+308 + 1.0E+308                        │ │
│  │  │                                                         │ │
│  │  │  Result: Infinity                                    │ │
│  │  │                                                         │ │
│  │  │  Overflow: Exponent overflow                          │ │
│  │  │                                                         │ │
│  │  │  Result: Infinity                                    │ │
│  │  └─────────────────────────────────────────────────────────┘ │
│  └─────────────────────────────────────────────────────────────┘
```

### Floating Point Addition
```
┌─────────────────────────────────────────────────────────────┐
│                FLOATING POINT ADDITION                      │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Floating Point Addition:                                   │
│  Aligning and adding mantissas                             │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                FLOATING POINT ADDITION                  │ │
│  │                                                         │ │
│  │  Steps:                                              │ │
│  │  1. Align the mantissas                               │ │
│  │  2. Add the mantissas                                 │ │
│  │  3. Normalize the result                              │ │
│  │                                                         │ │
│  │  Example: 1.0E+308 + 1.0E+308                        │ │
│  │                                                         │ │
│  │  Step 1: Align mantissas                               │ │
│  │  Step 2: Add mantissas                                 │ │
│  │  Step 3: Normalize result                              │ │
│  │                                                         │ │
│  │  Result: Infinity                                    │ │
│  │                                                         │ │
│  │  Overflow: Exponent overflow                          │ │
│  │                                                         │ │
│  │  Result: Infinity                                    │ │
│  └─────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

### Floating Point Subtraction
```
┌─────────────────────────────────────────────────────────────┐
│                FLOATING POINT SUBTRACTION                   │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Floating Point Subtraction:                                 │
│  Aligning and subtracting mantissas                         │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                FLOATING POINT SUBTRACTION               │ │
│  │                                                         │ │
│  │  Steps:                                              │ │
│  │  1. Align the mantissas                               │ │
│  │  2. Subtract the mantissas                             │ │
│  │  3. Normalize the result                              │ │
│  │                                                         │ │
│  │  Example: 1.0E+308 - 1.0E+308                        │ │
│  │                                                         │ │
│  │  Step 1: Align mantissas                               │ │
│  │  Step 2: Subtract mantissas                             │ │
│  │  Step 3: Normalize result                              │ │
│  │                                                         │ │
│  │  Result: 0.0E+308                                    │ │
│  │                                                         │ │
│  │  Overflow: Exponent underflow                          │ │
│  │                                                         │ │
│  │  Result: 0.0E+308                                    │ │
│  └─────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

### Floating Point Multiplication
```
┌─────────────────────────────────────────────────────────────┐
│                FLOATING POINT MULTIPLICATION                │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Floating Point Multiplication:                               │
│  Multiplying mantissas and adding exponents                   │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                FLOATING POINT MULTIPLICATION            │ │
│  │                                                         │ │
│  │  Steps:                                              │ │
│  │  1. Multiply mantissas                                │ │
│  │  2. Add exponents                                     │ │
│  │  3. Normalize the result                              │ │
│  │                                                         │ │
│  │  Example: 1.0E+308 * 1.0E+308                        │ │
│  │                                                         │ │
│  │  Step 1: Multiply mantissas                                │ │
│  │  Step 2: Add exponents                                     │ │
│  │  Step 3: Normalize result                              │ │
│  │                                                         │ │
│  │  Result: Infinity                                    │ │
│  │                                                         │ │
│  │  Overflow: Exponent overflow                          │ │
│  │                                                         │ │
│  │  Result: Infinity                                    │ │
│  └─────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

### Floating Point Division
```
┌─────────────────────────────────────────────────────────────┐
│                FLOATING POINT DIVISION                      │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Floating Point Division:                                    │
│  Dividing mantissas and subtracting exponents                 │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                FLOATING POINT DIVISION                  │ │
│  │                                                         │ │
│  │  Steps:                                              │ │
│  │  1. Divide mantissas                                   │ │
│  │  2. Subtract exponents                                 │ │
│  │  3. Normalize the result                              │ │
│  │                                                         │ │
│  │  Example: 1.0E+308 / 1.0E+308                        │ │
│  │                                                         │ │
│  │  Step 1: Divide mantissas                                   │ │
│  │  Step 2: Subtract exponents                                 │ │
│  │  Step 3: Normalize result                              │ │
│  │                                                         │ │
│  │  Result: 1.0E+0                                    │ │
│  │                                                         │ │
│  │  Overflow: Exponent underflow                          │ │
│  │                                                         │ │
│  │  Result: 1.0E+0                                    │ │
│  └─────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

### Floating Point Unit Components
```
┌─────────────────────────────────────────────────────────────┐
│                FLOATING POINT UNIT COMPONENTS               │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                FLOATING POINT UNIT                       │ │
│  │                                                         │ │
│  │  Floating point unit components                         │ │
│  │                                                         │ │
│  │  ┌─────────────────────────────────────────────────────┐ │
│  │  │                FLOATING POINT UNIT                      │ │
│  │  │                                                         │ │
│  │  │  Sign: 1 bit                                          │ │
│  │  │  Exponent: 8 bits                                     │ │
│  │  │  Mantissa: 23 bits                                    │ │
│  │  │                                                         │ │
│  │  │  Example: 3.14159 in floating point                   │ │
Computer Arithmetic: Addition and Subtraction, Tools Compliment Representation, Signed Addition and Subtraction, Multiplication and division, Booths Algorithm, Division Operation, Floating Point Arithmetic Operation. design of Arithmetic unit  