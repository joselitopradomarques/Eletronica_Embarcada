1.	Quais as diferenças entre os barramentos de dados e de endereços?\
	O barramento de endereços apenas transmite endereços partindo da CPU em direção à memória RAM e a ROM.\
	Já o barramento de dados pode tanto ler quanto escrever da ROM, RAM e Single Memory Space para a CPU.

2.	Quais são as diferenças entre as memórias RAM e ROM?\
	RAM (Read Aleatory Memory): É um tipo de memória volátil, ou seja, quando a sua energização é cessada, seus dados são apagados.\
	ROM (Read Only Memory): Já esse tipo de memória é não-volátil, ou seja, quando a sua energização é cessada, seus dados são mantidos.

3.	Considere o código abaixo:

#include <stdio.h>
int main(void)
{
	int i;
	printf("Insira um número inteiro: ");
	scanf("%d", &i);
	if(i%2)
		printf("%d eh impar.\n");
	else
		printf("%d eh par.\n");
	return 0;
}
Para este código, responda:
	(a) A variável i é armazenada na memória RAM ou ROM? Por quê?
		A variável i é armazenada na 
	(b) O programa compilado a partir deste código é armazenado na memória RAM ou ROM? Por quê?
		A variável é alocada na RAM, visto que a memória ROM possui escrita lenta em comparação à memória RAM.
		
4.	Quais são as diferenças, vantagens e desvantagens das arquiteturas Harvard e Von Neumann?
		As diferenças entre as arquiteturas estão no barramento de dados para a ROM pois na arquitetura Harvard, a ROM só pode ser escrita, porém na arquitetura von Neumann, a ROM também pode ser escrtita, apesar da baixa velocidade.
		As vantagens da arquitetura Harvard incluem a possibilidade do acesso simultâneo das duas memórias, aumentandoa velocidade de processamento, de forma que pode buscar uma nova instrução enquanto executa a outra. Além disso, pode-se também ler uma instrução ao mesmo tempo que faz um acesso à memória de dados.
		Já a arquitetura Von Neumann utiliza uma arquitetura mais simples, dessa forma, mais lenta pois o barramento de dados é mais limitada em comparação com a arquitetura Harvard.
		Uma arrquitetura mais simples permite um preço menor, de forma que acaba se tornando uma vantagem para ela para funções que não demandem um processamento mais rápido.
		
5.	Considere a variável inteira i, armazenando o valor 0x8051ABCD. Se i é armazenada na memória a partir do endereço 0x0200, como ficam este byte e os seguintes, considerando que a memória é: (a) Little-endian; (b) Big-endian.
	a Little-Endian:
	Endereço 0x0200: CD 
	Endereço 0x0201: AB
	Endereço 0x0202: 51
	Endereço 0x0203: 80
	
	b) Big-Endian:
	Endereço 0x0200: 80 
	Endereço 0x0201: 51
	Endereço 0x0202: AB
	Endereço 0x0203: CD
	
6.	Sabendo que o processador do MSP430 tem registradores de 16 bits, como ele soma duas variáveis de 32 bits?
	Caso uma variável tenha 32 bits, ela será dividida em dois registradores. Primeiro, soma-se os 4 primeiros LSB. Esse resultado gerará uma variável de 4 bits e uma flag c. Essa flag c será somada aos 4 bits MSB da primeira variável e posteriormente, esse resultado será comado aos 4 bits MSB da segunda variável. Esse resultado também gerará uma flag c, e dessa forma, pode-se tomar um número com quantos bits desejar, desde que a memória consiga comportar esse número.
