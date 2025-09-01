# Projeto Luminosidade

**Descrição:**  
Este projeto utiliza um sensor LDR para medir a luminosidade do ambiente.  
- Se o valor do sensor for menor ou igual a 600 (ambiente escuro), o LED vermelho acende e o LED verde apaga.  
- Se o valor for maior que 600 (ambiente claro), o LED verde acende e o LED vermelho apaga.  
O valor do sensor também é exibido no Monitor Serial para monitoramento.

**Link do projeto no Tinkercad:** [Clique aqui para abrir](https://www.tinkercad.com/things/aosOMpTlloA/editel?sharecode=PR1FIdMlgqo01KApmrGHs-rmlItMkcd9PjOEjIqtq9w)

**Componentes:**
- Arduino
- Sensor LDR
- LED verde
- LED vermelho
- Resistores (para LEDs e LDR)

---

## Código

```cpp
int ledRED = 7;
int ledGREEN = 6;
int LDR = A0;
int leituraSensor = 0;

void setup()
{ 
  pinMode(ledRED, OUTPUT);
  pinMode(ledGREEN, OUTPUT);
  pinMode(LDR, INPUT);
  Serial.begin(9600);
}

void loop()
{
  leituraSensor = analogRead(LDR);
  Serial.println(leituraSensor);
  delay(300);
  
  if (leituraSensor <= 600){
    digitalWrite(ledRED, 1);
    digitalWrite(ledGREEN, 0);
  } else {
    digitalWrite(ledGREEN, 1);
    digitalWrite(ledRED, 0);
  }
}
