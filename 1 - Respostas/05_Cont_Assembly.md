Para as questões 2 a 5, considere que as variáveis `f`, `g`, `h`, `i` e `j` são do tipo inteiro (16 bits na arquitetura do MSP430), e que o vetor `A[]` é do tipo inteiro. Estas variáveis estão armazenadas nos seguintes registradores:
	f: R4
	g: R5
	h: R6
	i: R7
	j: R8
	A: R9
Utilize os registradores R11, R12, R13, R14 e R15 para armazenar valores temporários.

1. Escreva os trechos de código assembly do MSP430 para:\
	(a) Somente setar o bit menos significativo de R5.\
	```C
	mov.w #01,R11
	bis.w R5,R11
	mov.w R11,R5
	```
	(b) Somente setar dois bits de R6: o menos significativo e o segundo menos significativo.\
	```C
	mov.w #03,R11
	bis.w R6,R11
	mov.w R11,R6
	```
	(c) Somente zerar o terceiro bit menos significativo de R7.\
	```C
	mov.w #04,R11
	bis.w R7,R11
	mov.w R11,R7
	```
	(d) Somente zerar o terceiro e o quarto bits menos significativo de R8.\
	```C
	mov.w #0C,R11
	bis.w R8,R11
	mov.w R11,R8
	```
	(e) Somente inverter o bit mais significativo de R9.\
	```C
	mov.w #04,R11
	bis.w R9,R11
	mov.w R11,R9
	```
	(f) Inverter o nibble mais significativo de R10, e setar o nibble menos significativo de R10.\
	```C
	mov.w R10,R11
	xor.w #F0,R11
	bic.w #0F,R11
	mov.w R11,R10
	```

2. "Traduza" o seguinte trecho de código em C para o assembly do MSP430:

```C
if(j<i) f = g+h+10;
else f = g-h-10;
```
------------------------------------------------------------------------
|f: R4|g: R5|h: R6|i: R7|j: R8|A: R9|
```C
	cmp R7,R8
	mov R5,R11
	mov R6,R12
	add #10,R12
	jeq Else
	add R12,R11
	jmp End
Else:	sub R12,R11
End:	ret
```

3. "Traduza" o seguinte trecho de código em C para o assembly do MSP430:

```C
while(save[i]!=k) i++;
```
------------------------------------------------------------------------
|f: R4|g: R5|h: R6|i: R7|j: R8|k: R9|
```C
LOOP:	mov.w R7,R12		;Armazenando o valor de i em um registrador temporário (R12 = i)
	rla R12			;Multiplicando i por 2 (R12 = 2*i)
	add.w R10, R12		;R10 = save ; R12 = save + 2*i;
	cmp 0(R12),R9		;Comparar save[i] com k
	jeq END			;Pular para o fim caso save[i] = k
	inc.w R7		;i+=1;
	jmp LOOP		;Voltar para o loop inicial pois a condicional foi aceita
END:	ret			; Saiu do loop
```

4. "Traduza" o seguinte trecho de código em C para o assembly do MSP430:

```C
for(i=0; i<100; i++) A[i] = i*2;
```
------------------------------------------------------------------------
|f: R4|g: R5|h: R6|i: R7|j: R8|k: R9|
```C

```
5. "Traduza" o seguinte trecho de código em C para o assembly do MSP430:

```C
for(i=99; i>=0; i--) A[i] = i*2;
```
