Para cada questão, escreva funções em C e/ou sub-rotinas na linguagem Assembly do MSP430. Reaproveite funções e sub-rotinas de uma questão em outra, se assim desejar. Leve em consideração que as sub-rotinas são utilizadas em um código maior, portanto utilize adequadamente os registradores R4 a R11. As instruções da linguagem Assembly do MSP430 se encontram ao final deste texto.

1. (a) Escreva uma função em C que calcule a raiz quadrada 'x' de uma variável 'S' do tipo float, utilizando o seguinte algoritmo: após 'n+1' iterações, a raiz quadrada de 'S' é dada por
```C
	x(n+1) = (x(n) + S/x(n))/2
```
O protótipo da função é:
```C
float RaizQuadrada(float S){

    int i;
    float res;

    res = S;

    for(i = 0; i <= 20; i++){
        res = (res + (S/res))/2;
    }

    return res;
}
```
(b) Escreva a sub-rotina equivalente na linguagem Assembly do MSP430. A variável 'S' é fornecida pelo registrador R15, e a raiz quadrada de 'S' (ou seja, a variável 'x') é fornecida pelo registrador R15 também.
```C
        ;Raiz Quadrada
        ; x(n+1) = (x(n) + S/x(n))/2
        ; S = R15

        mov.w #36, R15;          valor S
        mov.w #4, R12;           num de iteracoes

        mov.w R15, R14;          R14 recebe S, R15 vira x(n+1)
        mov.w R15, R13;          R13 vira x(n)
       
        cmp #0, R15;
        jeq FIM;

        cmp #0, R12;
        jeq FIM;
       
        LOOP:
           
        clr.w R11;               contador divisao
        mov.w R14, R10;          armazena S em R10  
        
        DIV:
        sub.w R13, R10;          S/x(n)
        inc.w R11;
        cmp R13, R10;
        jge DIV;

        clr.w R15;               x(n+1) = (x(n) + S/x(n))/2
        add.w R13, R15;          
        add.w R11, R15;
        rra.w R15;
        
        mov.w R15, R13;          atualiza x(n)
        
        dec.w R12;
        cmp #0, R12;
        jne LOOP;

        FIM:
```
2. (a) Escreva uma função em C que calcule 'x' elevado à 'N'-ésima potência, seguindo o seguinte protótipo: 
```C
int Potencia(int x, int n){

    if(n == 0){
        return 1;
    }

    else{
        return x*Potencia(x,n-1);
    }
}
```
(b) Escreva a sub-rotina equivalente na linguagem Assembly do MSP430. 'x' e 'n' são fornecidos através dos registradores R15 e R14, respectivamente, e a saída deverá ser fornecida no registrador R15.
```C
        ; Potencia
        ;x elevado a n
        ;R15 = x
        ;R14 = n
      
        mov.w #3, R15;		setando x
        mov.w #3, R14;		setando n
        
        ;mov.w R15, R13;         armazena x (repetida)
        clr.w R12;              limpa o contador da potencia
        inc.w R12;              R12 = 1
        clr.w R4;               R4 = 0
        clr.w R5;       
        inc.w R5;               R5 = 1

        ;condicao n = 0
        cmp #0, R14;
        jne POT;
        mov.w #1, R15
        jmp FIM;

        POT: 
        cmp R12, R14;           compara contador com n
        jeq FIM;                se contador == n, FIM
        mov.w R15, R13;
        clr.w R15;
        clr.w R11;              limpa o contador da multiplicacao


        MULT:
        add.w R13, R15;
        inc.w R11;               incrementa contador
        cmp R11, R14;
        jne MULT;                se contador != x, retorna

        inc.w R12; 
        jmp POT;

        FIM:
```
3. Escreva uma sub-rotina na linguagem Assembly do MSP430 que calcula a divisão de 'a' por 'b', onde 'a', 'b' e o valor de saída são inteiros de 16 bits. 'a' e 'b' são fornecidos através dos registradores R15 e R14, respectivamente, e a saída deverá ser fornecida através do registrador R15.
```C
        ;Divisao
        ;R15 = a , res
        ;R14 = b
        
        mov.w #18, R15;                 setando a
        mov.w #5, R14;                  setando b
       
        mov.w R15, R13;                 setando a em R13
        mov.w #0, R15;                  
        
        ;quociente maior que denominador
        cmp R14, R13;
        jge DIV;                         se R14 < R15, divide
        jmp FIM;
        
        DIV:
        sub.w R14, R13;
        inc.w R15
        cmp R14, R13;
        jge DIV;

        FIM:
```

4. Escreva uma sub-rotina na linguagem Assembly do MSP430 que calcula o resto da divisão de 'a' por 'b', onde 'a', 'b' e o valor de saída são inteiros de 16 bits. 'a' e 'b' são fornecidos através dos registradores R15 e R14, respectivamente, e a saída deverá ser fornecida através do registrador R15.
```C
	;Resto
        ;R15 = a , res
        ;R14 = b
        
        mov.w #3, R15;                 setando a
        mov.w #5, R14;                  setando b
       
        mov.w R15, R13;                 setando a em R13                 
        
        ;quociente maior que denominador
        cmp R14, R13;
        jge DIV;                         se R14 < R13, divide
        mov.w R14, R15;
        jmp FIM;
        
        DIV:
        sub.w R14, R13;
        cmp R14, R13;
        jge DIV;
        mov.w R13, R15

        FIM:

```
5. (a) Escreva uma função em C que indica a primalidade de uma variável inteira sem sinal, retornando o valor 1 se o número for primo, e 0, caso contrário. Siga o seguinte protótipo:
```C
int Primalidade(unsigned int x){

    int i;

    for(i = 2; i < x; i++){

        if(x%i == 0){
            return 0;
        }
    }

    return 1;

}		
```	

(b) Escreva a sub-rotina equivalente na linguagem Assembly do MSP430. A variável de entrada é fornecida pelo registrador R15, e o valor de saída também.
```C
	;Primalidade
        
        mov.w #17, R15;                  setando o numero
        mov.w R15, R14;                 armazenando o valor
        mov.w #2, R13;                  setando contador primario em 2
        
        clr.w R15;
        
        ; R15 = 0, 1, 2
        cmp #0, R14;
        jeq PRI;

        cmp #1, R14;
        jeq PRI;

        cmp #2, R14;
        jeq PRI;
        
        LOOP:
        
        mov.w R14, R10;                 armazenando copia do valor em R10
        cmp R14, R13;
        jge PRI;
        
        DIV:
        sub.w R13, R10;
        cmp R13, R10;
        jge DIV;
        inc.w R13;
        cmp #0, R10;
        jeq FIM;
        jmp LOOP;

        PRI:
        mov.w #1, R15;
  
        FIM:
```
6. Escreva uma função em C que calcula o duplo fatorial de n, representado por n!!. Se n for ímpar, n!! = 1*3*5*...*n, e se n for par, n!! = 2*4*6*...*n. Por exemplo, 9!! = 1*3*5*7*9 = 945 e 10!! = 2*4*6*8*10 = 3840. Além disso, 0!! = 1!! = 1.
O protótipo da função é:
```C
unsigned long long Duplo_Fat(unsigned long long int x){

    if(x == 0){
        return 1;
    }

    else if(x == 1){
        return 1;
    }

    else{
        return x*Duplo_Fat(x-2);
    }

}
```
7. (a) Escreva uma função em C que calcula a função exponencial da seguinte forma:
	
Considere o cálculo até o termo n = 20. O protótipo da função é double ExpTaylor(double x);
```C
double ExpTaylor(double x){

    double exp;

    int i, n, fat;

    exp = 0;

    for(i = 0; i <= 20; i++){

        fat = 1;

        for(n = i; n > 1; n--){
            fat *= n;
        }

        exp += pow(x, i)/fat;

    }

    return exp;
}
```
(b) Escreva a sub-rotina equivalente na linguagem Assembly do MSP430, mas considere que os valores de entrada e de saída são inteiros de 16 bits. A variável de entrada é fornecida pelo registrador R15, e o valor de saída também.



8. Escreva uma sub-rotina na linguagem Assembly do MSP430 que indica se um vetor esta ordenado de forma decrescente. Por exemplo:
[5 4 3 2 1] e [90 23 20 10] estão ordenados de forma decrescente.
[1 2 3 4 5] e [1 2 3 2] não estão.
O primeiro endereço do vetor é fornecido pelo registrador R15, e o tamanho do vetor é fornecido pelo registrador R14. A saída deverá ser fornecida no registrador R15, valendo 1 quando o vetor estiver ordenado de forma decrescente, e valendo 0 em caso contrário.

```C
#include<stdio.h>

int Vetor_Ordenado_Decrescente(int *p,int n)
{
	/*Vetor_Ordenado_Decrescente é uma função que analisa se um vetor é decrescente ou não,
	de forma que retorna 1 se for decrescente e 0 se for decrescente.
	p* é um ponteiro que aponta para a primeira posição do vetor e n é um valor inteiro com o tamanho do vetor*/
	
	int i;
	for (i=0;i<n;i++)
	{
		
		if((i>0)&&(p[i] >= p[i-1]))
		{
			return 0;
		}
	}
	/*Se todas as posições do vetor foram visualizadas, o vetor é decrescente e a função deve retornar 1.*/
	return 1;
}

void main()
{
	int vetor[5],i,verificador;
	
	for(i=0;i<5;i++)
	{
		scanf("%d",&vetor[i]);	
	}
	
	verificador = Vetor_Ordenado_Decrescente(vetor,5);
	if(verificador == 1)
	{
		printf("O vetor ");
		for(i=0;i<5;i++)
		{	
			printf("%d ",vetor[i]);
		}	
		printf("e' decrescente.\n");
	}
	else
	{
		printf("O vetor ");
		for(i=0;i<5;i++)
		{	
			printf("%d ",vetor[i]);
		}	
		printf("nao e' decrescente.\n");
	}
	
}
```
9. Escreva uma sub-rotina na linguagem Assembly do MSP430 que calcula o produto escalar de dois vetores, 'a' e 'b':
	
O primeiro endereço do vetor 'a' deverá ser passado através do registrador R15, o primeiro endereço do vetor 'b' deverá ser passado através do registrador R14, e o tamanho do vetor deverá ser passado pelo registrador R13. A saída deverá ser fornecida no registrador R15.
```C
#include<stdio.h>

int MULT_signed(int a, int b)
{
	if(a<0 && b<0)
	{
		a = -a;
		b = -b;
		return MULT_unsigned(a,b);
	}
	else if (a<0 && b>0)
	{
		a = -a;
		return -(MULT_unsigned(a,b));
	}
	else if (a>0 && b<0)
	{
		b = -b;
		return -(MULT_unsigned(a,b));
	}
	else
	{
		return MULT_unsigned(a,b);
	}

}

int MULT_unsigned(unsigned int a, unsigned int b)
{
if(b==0) return 0;
else
return a+MULT_unsigned(a, (b-1));
}

int Produto_Escalar_int(int *a,int *b, int n)
{
/*O ponteiro *a aponta para o endereço do primeiro vetor na memória e o ponteiro *b aponta para o endereço do
do segundo vetor na memória. O número n indica o tamanho do vetor. Esta função retorna um valor inteiro.
*/	

	int i,soma=0;
	for(i=0;i<n;i++)
	{
		soma += MULT_signed(a[i],b[i]);
	}
	return soma;
}

void main()
{
	int a[3],b[3],i,prod_escalar;
	printf("Insira o valor do vetor a\n");
	for(i=0;i<3;i++)
	{
		scanf("%d",&a[i]);
	}
	printf("Insira o valor do vetor b\n");
	for(i=0;i<3;i++)
	{
		scanf("%d",&b[i]);
	}
	prod_escalar = Produto_Escalar_int(a,b,3);
	printf("O produto escalar do vetor a = <%d,%d,%d> e b = <%d,%d,%d> e' a.b = %d.\n",a[0],a[1],a[2],b[0],b[1],b[2],prod_escalar);
}
```
10. (a) Escreva uma função em C que indica se um vetor é palíndromo. Por exemplo:
 	[1 2 3 2 1] e [0 10 20 20 10 0] são palíndromos.
 	[5 4 3 2 1] e [1 2 3 2] não são.
 Se o vetor for palíndromo, retorne o valor 1. Caso contrário, retorne o valor 0. O protótipo da função é:
 -----------------------------------------------------------------
 ```C
 int Palindromo(int vetor[ ], int tamanho);
 {
 	int i; k = tamanho-1; % O vetor começa no 0 e vai até o tamanho -1. Por isso o "k" recebe "tamanho -1"
 	%k é o que vai percorrer o vetor de trás para frente
 	%i percorrerá o vetor do início à metade 
 	tamanho = tamanho/2 - 1;
 	for(i=0;i<=tamanho;i++,k--)
 		{
 			if(vetor[i]!=vetor[k])
 			{
 			return 0;
 			}
 		}
 		return 1;
 }
 ```
 -----------------------------------------------------------------
 ```C
 int Palindromo(int vetor[ ], int tamanho);
 {
 	int *vetor_end = vetor+tamanho-1;
 	tamanho = tamanho/2 - 1;
 	for(;vetor < vetor_end; vetor++,vetor_end--)
 		{
 		???????
 		}
 		return 1;
 }
 ```
 -----------------------------------------------------------------
 (b) Escreva a sub-rotina equivalente na linguagem Assembly do MSP430. O endereço do vetor de entrada é dado pelo registrador R15, o tamanho do vetor é dado pelo registrador R14, e o resultado é dado pelo registrador R15.
 -----------------------------------------------------------------
 ```C
 Palindromo:	push R4
 		push R5
 		clr R4; i=0
 		mov R14,R5
 		dec R5; k = N - 1 % N é o tamanho
 		rra R14
 		dec R14; N = N - 1
 Palin_test:	cmp R4,R14
 		jl Palin_end
 		mov R4,R12
 		rla R12
 		add R15,R12
 		mov R5,R13
 		rla R13
 		add R15,R13
 		cmp 0(R12),0(R13)
 		jeq Palin_inc
 		pop R5
 		pop R4
 		clr R15
 		ret
