### MD5 vs SHA-1 ###
MD5 and SHA-1 have a lot in common; SHA-1 was clearly inspired on either MD5 or MD4, or both (SHA-1 is a patched version of SHA-0, which was published in 1993, while MD5 was described as a RFC in 1992).

The main structural differences are the following:

SHA-1 has a larger state: 160 bits vs 128 bits.
SHA-1 has more rounds: 80 vs 64.
SHA-1 rounds have an extra bit rotation and the mixing of state words is slightly different (mostly to account for the fifth word).
Bitwise combination functions and round constants are different.
Bit rotation counts in SHA-1 are the same for all rounds, while in MD5 each round has its own rotation count.
The message words are pre-processed in SHA-0 and SHA-1. In MD5, each round uses one of the 16 message words "as is"; in SHA-0, the 16 message words are expanded into 80 derived words with a sort of word-wise linear feedback shift register. SHA-1 furthermore adds a bit rotation to these word derivation.
The extra bit rotation is what makes SHA-1 distinct from SHA-0; it also makes SHA-1 much stronger against collision attacks, and, indeed, SHA-0 collisions have been found (with effort 239239, thus highly doable) while SHA-1 collisions still remain theoretical.

We don't have a true theory of what makes a hash function strong. However, we can still have some "gut feelings", and my own intestine tells me that in the case of MD-like functions (MD4, MD5, SHA-0, SHA-1, and the SHA-2 functions), the two important points are:

Rotating bits a lot. Collision attacks based on differential paths try to induce small differences and keep them from propagating non-linearly everywhere; a useful tool for that is the lack of carry beyond the upper bits in word-wise additions (a difference in the upper bit in one of the operands of an addition modulo 232232 propagates to the output with probability 11; two such differences cancel each other reliably). The 1-bit rotation added in SHA-1 is effective at making differential paths harder to find.

Doing "enough work". If you count the number of elementary operations per input byte (which more or less translates to code size or speed, especially on GPU), you will see that **SHA-1 is about 30% heavier than MD5, while SHA-256 is close to twice heavier than SHA-1. SHA-3 candidates were also, as a rule, "heavier" than SHA-1 (some could get faster by leveraging SIMD opcodes in CPU, but still had more operations per input byte).**