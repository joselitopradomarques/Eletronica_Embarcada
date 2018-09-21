Para todas as questões, considere que as variáveis `f`, `g`, `h`, `i` e `j` são do tipo inteiro (16 bits na arquitetura do MSP430), e que o vetor `A[]` é do tipo inteiro. Estas variáveis estão armazenadas nos seguintes registradores:

- f: R4
- g: R5
- h: R6
- i: R7
- j: R8
- A: R9

Utilize os registradores R11, R12, R13, R14 e R15 para armazenar valores temporários.

1. Traduza as seguintes linhas em C para a linguagem assembly do MSP430. Utilize somente as seguintes instruções: mov.w, add.w, sub.w, clr.w, dec.w, decd.w, inc.w e incd.w.

(a) `f *= 5;`
```C
mov R4,R11
mov R4,R12
add R11,R11
add R11,R11
add R11,R12
mov R12,R4
```

(b) `g *= 6;`
```C
mov R5,R11
add R11,R11
mov R11,R12
add R12,R12
add R12,R11
mov R11,R5
```

(d) `A[2] = 6*A[1] + 5*A[0];`
```C
mov 2(R9),R11
mov 2(R9),R12
add R11,R11
add R11,R11
add R12,R12
add R11,R12
mov 0(R9),R13
mov 0(R9),R14
mov R13,R13
mov R13,R13
add R13,R14
add R14,R12
mov R12, 4(R9)
```

(e) `A[3] = 3*f - 5*h;`
```C
mov R4,R11
mov R11,R12
add R11,R11
add R11,R12
mov R6,R13
mov R13,R14
add R14,R14
add R14,R14
add R13,R14
sub R14,R12
mov R12,6(R9)
```

(f) `A[5] = 6*(f - 2*h);`
```C
mov R4, R11
mov R6,R12
add R12,R12
sub R12,R11
mov R11,R13
add R11,R11
add R13,R13
add R13,R13
add R11,R13
mov R13,10(R9)
```
