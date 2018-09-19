Para todas as questões, considere que as variáveis `f`, `g`, `h`, `i` e `j` são do tipo inteiro (16 bits na arquitetura do MSP430), e que o vetor `A[]` é do tipo inteiro. Estas variáveis estão armazenadas nos seguintes registradores:

- f: R4
- g: R5
- h: R6
- i: R7
- j: R8
- A: R9

Utilize os registradores R11, R12, R13, R14 e R15 para armazenar valores temporários.

1. Traduza as seguintes linhas em C para a linguagem assembly do MSP430. Utilize somente as seguintes instruções: mov.w, add.w e sub.w.

(a) `f = 0;`

```C
mov.w #0, R4
```

(b) `g++;`

```C
mov.w #1, R11
add.w R11, R5
```

(c) `h--;`
```C
mov.w #1, R11
sub.w R11, R6
```
(d) `i += 2;`

```C
mov.w #2, R11
add.w R11, R7
```

(e) `j -= 2;`
```C
mov.w #2, R11
sub.w R11, R8
```

2. Traduza as seguintes linhas em C para a linguagem assembly do MSP430. Utilize somente as seguintes instruções: mov.w, add.w, sub.w, clr.w, dec.w, decd.w, inc.w e incd.w.

(a) `f = 0;`
```C
clr.w R4
```

(b) `g++;`
```C
inc.w R5
```

(c) `h--;`
```C
dec.w R6
```

(d) `i += 2;`
```C
incd.w R7
```

(e) `j -= 2;`
```C
decd.w R8
```

3. Traduza as seguintes linhas em C para a linguagem assembly do MSP430. Utilize somente as seguintes instruções: mov.w, add.w, sub.w, clr.w, dec.w, decd.w, inc.w e incd.w.

(a) `f *= 2;`
```C
mov.w R4,R11
add.w R11,R11
mov.w R11,R4
```

(b) `g *= 3;`
```C
mov.w R5,R11
mov.w R5,R12
add.w R11,R11
add.w R11,R12
mov.w R12,R5
```

(c) `h *= 4;`
```C
mov.w R6,R11
add.w R11,R11
add.w R11,R11
mov.w R11,R6
```
(d) `A[2] = A[1] + A[0];`
```C
mov.w 0(R9),R11
mov.w 2(R9),R12
add.w R11,R12
mov.w R12,4(R9)
```
(e) `A[3] = 2*f - 4*h;`

(f) `A[3] = 2*(f - 2*h);`
