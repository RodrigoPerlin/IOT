# Projeto Sensor de Umidade 💧

Este projeto utiliza um Arduino para monitorar o nível de umidade (ou nível de água) através de um sensor analógico.  
Dependendo do valor lido, LEDs vermelhos, amarelos e verdes acendem para indicar o nível de água.

O link para o projeto no Tinkercad: [Projeto Umidade](https://www.tinkercad.com/things/cOGISOLZnY3/editel?sharecode=ehG3IX9Hk-Cp7__7Sw6BL2MiDuF_rtJmjWO1U3_pV-g)

---

## Código Arduino

```cpp
// --- Pinos ---
#define Pin_Sensor A0
#define LED_VERMELHO_3 2
#define LED_VERMELHO_2 3
#define LED_VERMELHO_1 4
#define LED_AMARELO_3 5
#define LED_AMARELO_2 6
#define LED_AMARELO_1 7
#define LED_VERDE_3 8
#define LED_VERDE_2 9
#define LED_VERDE_1 10

int intensidade;

void setup() {
  Serial.begin(9600);
  pinMode(Pin_Sensor, INPUT);
  for (int i = 2; i <= 10; i++) {
    pinMode(i, OUTPUT);
  }
  Serial.println("Simulacao iniciada. Nivel de agua: Minimo");
}

// --- Função para controlar os LEDs ---
void leds(int v3, int v2, int v1, int a3, int a2, int a1, int g3, int g2, int g1) {
  digitalWrite(LED_VERMELHO_3, v3);
  digitalWrite(LED_VERMELHO_2, v2);
  digitalWrite(LED_VERMELHO_1, v1);
  digitalWrite(LED_AMARELO_3, a3);
  digitalWrite(LED_AMARELO_2, a2);
  digitalWrite(LED_AMARELO_1, a1);
  digitalWrite(LED_VERDE_3, g3);
  digitalWrite(LED_VERDE_2, g2);
  digitalWrite(LED_VERDE_1, g1);
}

void loop() {
  int sensorValue = analogRead(Pin_Sensor); // Lê o valor do sensor
  intensidade = map(sensorValue, 0, 876, 0, 9); // Mapeia para 0-9 com base no máximo 876

  // Exibe no Monitor Serial
  Serial.print("Valor do sensor: ");
  Serial.print(sensorValue);
  Serial.print(" | Nivel mapeado: ");
  Serial.print(intensidade);
  Serial.print(" | LEDs acesos: ");
  
  switch (intensidade) {
    case 0:
    case 1: // Nível mínimo: apenas LED_VERMELHO_3 aceso
      leds(1, 0, 0, 0, 0, 0, 0, 0, 0);
      Serial.println("1 (Vermelho 3)");
      break;
    case 2: // LED_VERMELHO_3 e LED_VERMELHO_2
      leds(1, 1, 0, 0, 0, 0, 0, 0, 0);
      Serial.println("2 (Vermelhos 3 e 2)");
      break;
    case 3: // LEDs vermelhos
      leds(1, 1, 1, 0, 0, 0, 0, 0, 0);
      Serial.println("3 (Vermelhos)");
      break;
    case 4: // LEDs vermelhos e LED_AMARELO_3
      leds(1, 1, 1, 1, 0, 0, 0, 0, 0);
      Serial.println("4 (Vermelhos e Amarelo 3)");
      break;
    case 5: // LEDs vermelhos e dois amarelos
      leds(1, 1, 1, 1, 1, 0, 0, 0, 0);
      Serial.println("5 (Vermelhos e Amarelos 3 e 2)");
      break;
    case 6: // LEDs vermelhos e todos amarelos
      leds(1, 1, 1, 1, 1, 1, 0, 0, 0);
      Serial.println("6 (Vermelhos e Amarelos)");
      break;
    case 7: // LEDs vermelhos, amarelos e LED_VERDE_3
      leds(1, 1, 1, 1, 1, 1, 1, 0, 0);
      Serial.println("7 (Vermelhos, Amarelos e Verde 3)");
      break;
    case 8: // LEDs vermelhos, amarelos e dois verdes
      leds(1, 1, 1, 1, 1, 1, 1, 1, 0);
      Serial.println("8 (Vermelhos, Amarelos e Verdes 3 e 2)");
      break;
    case 9: // Todos os LEDs acesos
      leds(1, 1, 1, 1, 1, 1, 1, 1, 1);
      Serial.println("9 (Todos os LEDs)");
      break;
    default: // Fora do intervalo: todos apagados
      leds(0, 0, 0, 0, 0, 0, 0, 0, 0);
      Serial.println("0 (Nenhum LED)");
      break;
  }

  delay(100); // Atraso de 100ms para estabilizar a leitura
}
