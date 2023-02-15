# Floating Point Numbers

- Computers use IEEE standard binary floating-point representation of numbers.
- The IEEE standard defines a number as a sign bit, an exponent, and a mantissa.
  - The sign bit is 1 for negative numbers and 0 for positive numbers.
  - The exponent is a binary number that encodes the power of 2 that the mantissa should be multiplied by.
  - The mantissa is a binary number between 1 and 2 that encodes the fractional part of the number.

The formula for converting a floating point number to a decimal number is:

${-1}^s \times 2^{e-bias} \times (1 + \sum_{i=1}^n m_i \times 2^{-i})$

- `s` is the sign bit.
- `bias` is $2^{k-1} - 1$ where $k$ is the number of bits in the exponent.
  - $127$ for single precision.
  - $1023$ for double precision.
- $1 + \sum_{i=1}^n m_i \times 2^{-i}$ is the mantissa.
  - It is 1 plus the sum of the bits in the mantissa multiplied by $2^{-i}$ where $i$ is the bit number.

## Float Representation

Floating point numbers are represented in binary.
They can either be single precision (32 bits) or double precision (64 bits).

### Float Precision

- Sign bit is 1 bit.
- Exponent is 8 bits.
- Mantissa is 23 bits.

### Double Precision

- Sign bit is 1 bit.
- Exponent is 11 bits.
- Mantissa is 52 bits.

## Conversion

### Converting Float to Decimal

`float`: $11000000011000010011000000000000$

- `s`: $1$
  - The number is negative.
- `e`: $10000000$
  1. $10000000_2 = 128_{10}$
  2. $\text{bias = } 128 - 127 = 1$
- `m`: $11000010011000000000000$
  1. $2^{-1} + 2^{-2} + 2^{-7} + 2^{-10} + 2^{-11} = 0.5 + 0.25 + 0.0078125 + 0.0009765625 + 0.00048828125 = 0.75927734375$
  2. $1 + 0.75927734375 = 1.75927734375$

Converting to decimal:

$-1^s \times 2^{e-bias} \times (1 + m) = -1 \times 2^{1} \times 1.75927734375 = 3.51655274$

### Converting Decimal to Float

1. Extract the sign bit.
2. Convert the decimal number to binary.
3. Normalize the binary number and extract the exponent.
   - $e = x + \text{bias} = x + 2^{k-1} - 1$ where $k$ is the number of bits in the exponent.
4. Extract the mantissa.
   - $m = 1 + \sum_{i=1}^n m_i \times 2^{-i}$
   - Round to the number of bits in the mantissa.

#### Example: `-123.456`

1. $s = 1$
2. $123.456 = 1111011.01110100101111000110101_2$
3. $1111011.01110100101111000110101_2 = 1.11101101110100101111000110101_2 \times 2^6$
   - $e = 6 + 127 = 133 = 10000101$
4. $m = 11101101110100101111001$

`float`: $11000010111101101110100101111001_2$

## Machine-Epsilon

- Computer Numbers (CNs) are the finite precision numbers that a computer can represent.
- The machine-epsilon $\epsilon$ is the difference between 1 and the next CN.
  - For single precision, $\epsilon = 2^{-23} = 1.19 \times 10^{-7}$.
  - For double precision, $\epsilon = 2^{-52} = 2.22 \times 10^{-16}$.
- When trying to store a number $1 < x < 1 + \epsilon$, the computer will round to the nearest CN.

The gap between two consecutive CNs around $x$ scales with $x$ as $\epsilon|x|$.

$fl(x)$ is the CN closest to $x$.

$fl(x) = x(1 + \alpha)$
where $\alpha$ is the error.

$|\alpha| = \frac{|fl(x) - x|}{|x|} \le \frac{\epsilon}{2}$

## Arithmetic

- The rules of standard arithmetic do not apply to floating point numbers.
- The arithmetic results of two CNs are not necessarily CNs.
- The exponent field has to match the exponent of the largest.
