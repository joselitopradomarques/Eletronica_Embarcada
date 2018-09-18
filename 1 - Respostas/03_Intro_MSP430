1.  Dada uma variável a do tipo char (um byte), escreva os trechos de código em C para: 
  (a) Somente setar o bit menos significativo de a.
    a = a|0x01;
  (b) Somente setar dois bits de a: o menos significativo e o segundo menos significativo.
    a = a|0x03;
  (c) Somente zerar o terceiro bit menos significativo de a.
    a = a&0x0B;
  (d) Somente zerar o terceiro e o quarto bits menos significativo de a.
    a = a&0x03;
  (e) Somente inverter o bit mais significativo de a.
    a = a^0x80;
  (f) Inverter o nibble mais significativo de a, e setar o nibble menos significativo de a.
    a = a^0xF0;
    a = a|0x0F;

2.  Considerando a placa Launchpad do MSP430, escreva o código em C para piscar os dois LEDs ininterruptamente.
    
    #include <msp430g2553.h>
    int main(void)
      {
       WDTCTL = WDTPW | WDTHOLD;
       P1OUT = 0x00;
       P1DIR = 0x41;
       for(;;)
       {
        P1OUT|= 0x41;
        P1OUT &= ~(0x41);
       }
      }
    
    
3.  Considerando a placa Launchpad do MSP430, escreva o código em C para piscar duas vezes os dois LEDs sempre que o usuário pressionar o botão.
      #include <msp430g2553.h>
      #define BTN BIT3
      #define LED1 BIT0
      #define LED2 BIT6
      
      int main(void){
       WDTCTL = WDTPW | WDTHOLD;
       P1OUT = 0x00;
       P1DIR = LED1 + LED2;
       for(;;)
       {
       if(P1IN & BTN == 0)
         P1OUT |= LED1 + LED2;
         P1OUT &= ~(LED1 + LED2);
         P1OUT |= LED1 + LED2;
         P1OUT &= ~(LED1 + LED2);

       }
      }

4.  Considerando a placa Launchpad do MSP430, faça uma função em C que pisca os dois LEDs uma vez.

      void blink(void)
      {
        P1OUT|= 0x41;
        P1OUT &= ~(0x41);
      }

5.  Reescreva o código da questão 2 usando a função da questão 4.

#include <msp430g2553.h>

#define LED1 BIT0
#define LED2 BIT6
#define LEDS BIT0 + BIT6

void blink(void)
      {
        P1OUT|= LEDS;
        P1OUT &= ~(LEDS);
      }

int main(void)
      {
       WDTCTL = WDTPW | WDTHOLD;
       P1OUT = 0x00;
       P1DIR = LEDS;
       for(;;)
         {
          blink();
          blink();
         }
      }

6.  Reescreva o código da questão 3 usando a função da questão 4.

#include <msp430g2553.h>

#define BTN BIT3
#define LED1 BIT0
#define LED2 BIT6
#define LEDS BIT0 + BIT6

void blink(void)
      {
        P1OUT|= LEDS;
        P1OUT &= ~(LEDS);
      }

      
int main(void){
       WDTCTL = WDTPW | WDTHOLD;
       P1OUT = 0x00;
       P1DIR = LEDS;
       
       for(;;)
         {
         if(P1IN & BTN == 0)
           blink();
           blink();
         }
      }
