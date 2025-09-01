# Projeto Fumaça

**Descrição:**  
Este projeto utiliza um sensor de fumaça/gás para detectar a presença de fumaça no ambiente. Quando o nível de fumaça ultrapassa o limite definido, o LED vermelho acende, o LED verde apaga e o buzzer emite um som de sirene alternada. Caso contrário, o LED verde fica aceso e o buzzer desligado.  

**Link do projeto no Tinkercad:** [Clique aqui para abrir](https://www.tinkercad.com/things/k8RloaS17JK/editel?sharecode=OSxWFT30PfSST6HFxPWc5pMN8Gj8Y9rdWcEFo22Wm9o)

**Componentes:**
- Arduino
- Sensor de fumaça/gás (MQ-2 ou similar)
- Buzzer
- LED verde
- LED vermelho

---

## Código

```cpp
#define pino_sensor_analogico A0
#define pino_sensor_digital 4
#define pino_Buzzer 5
#define Led_Verde 6
#define Led_Vermelho 7

/* Variáveis para armazenar os dados do Sensor. */
int valor_analogico;
int valor_digital;

void setup() {
  /* Inicia a comunicação Serial na velocidade de 9600 bauds */
  Serial.begin(9600);
  /* Configura os pinos digitais como saída e entrada. */
  pinMode(pino_sensor_digital, INPUT);
  pinMode(pino_sensor_analogico, INPUT);
  pinMode(pino_Buzzer, OUTPUT);
  pinMode(Led_Verde, OUTPUT);
  pinMode(Led_Vermelho, OUTPUT);
}

void loop() {
  valor_analogico = analogRead(pino_sensor_analogico);
  valor_digital = digitalRead(pino_sensor_digital);
  Serial.print("Nível detetado: ");
  Serial.print(valor_analogico);
  Serial.print(" || ");

  /* Se o Sensor detectar gás ou fumaça */
  if (valor_analogico >= 500) {
    Serial.println("GÁS DETECTADO!!!");
    digitalWrite(Led_Verde, LOW);
    digitalWrite(Led_Vermelho, HIGH);
    
    /* Efeito de sirene alternada (tipo policial/ambulância) */
    tone(pino_Buzzer, 800);  // Frequência baixa
    delay(250);               // Duração da nota
    tone(pino_Buzzer, 1200); // Frequência alta
    delay(250);               // Duração da nota
  } else {
    Serial.println("GÁS AUSENTE!!!");
    digitalWrite(Led_Verde, HIGH);
    digitalWrite(Led_Vermelho, LOW);
    noTone(pino_Buzzer); // Desliga o buzzer
  }
}
