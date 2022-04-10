Concepts: https://www.youtube.com/watch?v=--tnZMuoK3E

## Salt
Salts are short random set of characters, that will be concatenated with passwords, before they are hashed. The usage of salts prevents the hacks with [Rainbow Tables](https://en.wikipedia.org/wiki/Rainbow_table).

Salts are ususally not encrypted.

![[Salt.png]]

## Pepper
Pepers are very short random strings, that are added to the end of password and encrypted with it.

Pepper is not stored in system. 1-character pepper with only 1 letter makes the brute force hack 52 times harder.
![[Pepper.png]]


