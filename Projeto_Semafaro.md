# Projeto Semáforo

Este projeto simula um semáforo utilizando um **Arduino Uno** e três LEDs (vermelho, amarelo e verde).  

Material de apoio: [Tinkercad](https://www.tinkercad.com/things/00zGfcGCEQh/editel?sharecode=Bl_y1ck4JVDeIMskAZBmGr7wItmtTNtsI-KFGfcqtpA)

---

## Componentes Utilizados

- Arduino Uno
- LED vermelho, LED amarelo, LED verde
- Resistores (220Ω ou 330Ω)
- Protoboard e fios de conexão

---

## Código do Projeto

```cpp
int led_vermelho = 5;
int led_amarelo = 6;
int led_verde = 7;

void setup() {
  pinMode(led_vermelho, OUTPUT);
  pinMode(led_amarelo, OUTPUT);
  pinMode(led_verde, OUTPUT);
}

void loop() {
  // LED vermelho aceso (Pare) - 5 segundos
  digitalWrite(led_vermelho, HIGH);
  digitalWrite(led_amarelo, LOW);
  digitalWrite(led_verde, LOW);
  delay(5000);

  // LED verde aceso (Siga) - 3,5 segundos
  digitalWrite(led_vermelho, LOW);
  digitalWrite(led_amarelo, LOW);
  digitalWrite(led_verde, HIGH);
  delay(3500);

  // LED amarelo aceso (Atenção) - 2 segundos
  digitalWrite(led_vermelho, LOW);
  digitalWrite(led_amarelo, HIGH);
  digitalWrite(led_verde, LOW);
  delay(2000);
}

void loop() {
 
digitalWrite(led_vermelho, 1);
digitalWrite(led_amarelo, 0);
digitalWrite(led_verde, 0);
delay(5000);

   
digitalWrite(led_vermelho, 0);
digitalWrite(led_amarelo, 0);
digitalWrite(led_verde, 1);
delay(3500);

  
digitalWrite(led_vermelho, 0);
digitalWrite(led_amarelo, 1);
digitalWrite(led_verde, 0);
delay(2000);

} 
  

