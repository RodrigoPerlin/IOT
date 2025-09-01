# Projeto LED de Natal 🎄💡

Este projeto utiliza um Arduino para controlar 13 LEDs, criando diferentes efeitos de iluminação natalina. Os efeitos incluem:

1. Pisca um por um.
2. Pisca alternado (pares/ímpares).
3. Vai e volta tipo KITT.
4. Todos piscando juntos.

O link para o projeto no Tinkercad: [Projeto LED Natal](https://www.tinkercad.com/things/3qJB1KipZKs-projeto-led-natal/editel?returnTo=%2Fthings%2F3qJB1KipZKs-copy-of-fantastic-fulffy&sharecode=xXS8sfzERPwfJGZafK-Yc-DoKq1MTmPu2bmnGCLGgfQ)

---

## Código Arduino

```cpp
// --- Pinos dos LEDs (coloque conforme sua ligação) ---
int leds[] = {0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12};
int numLeds = 13;

void setup() {
  for (int i = 0; i < numLeds; i++) {
    pinMode(leds[i], OUTPUT);
  }
}

void loop() {
  efeito1(); // Um por um, 8 segundos total
  delay(1000);

  efeito2(); // Pisca alternado (pares/ímpares)
  delay(1000);

  efeito3(); // Vai e volta tipo KITT
  delay(1000);

  efeito4(); // Todos piscando juntos
  delay(1000);
}

// --- EFEITO 1: Pisca um por um, apaga o último ---
void efeito1() {
  int tempo = 8000 / numLeds; // Divide 8 segundos entre todos
  for (int i = 0; i < numLeds; i++) {
    digitalWrite(leds[i], HIGH);
    delay(tempo);
    if (i == numLeds - 1) {
      digitalWrite(leds[i], LOW);
    }
  }
}

// --- EFEITO 2: Pisca alternado ---
void efeito2() {
  for (int t = 0; t < 5; t++) { // Repete 5 vezes
    // Liga pares
    for (int i = 0; i < numLeds; i++) {
      digitalWrite(leds[i], (i % 2 == 0) ? HIGH : LOW);
    }
    delay(500);

    // Liga ímpares
    for (int i = 0; i < numLeds; i++) {
      digitalWrite(leds[i], (i % 2 != 0) ? HIGH : LOW);
    }
    delay(500);
  }
  // Apaga tudo no final
  for (int i = 0; i < numLeds; i++) {
    digitalWrite(leds[i], LOW);
  }
}

// --- EFEITO 3: Vai e volta tipo KITT ---
void efeito3() {
  for (int r = 0; r < 3; r++) { // Repete 3 vezes
    for (int i = 0; i < numLeds; i++) {
      acendeUnico(i);
    }
    for (int i = numLeds - 2; i > 0; i--) {
      acendeUnico(i);
    }
  }
}

void acendeUnico(int indice) {
  for (int i = 0; i < numLeds; i++) {
    digitalWrite(leds[i], LOW);
  }
  digitalWrite(leds[indice], HIGH);
  delay(100);
}

// --- EFEITO 4: Todos piscando juntos ---
void efeito4() {
  for (int t = 0; t < 5; t++) {
    for (int i = 0; i < numLeds; i++) {
      digitalWrite(leds[i], HIGH);
    }
    delay(300);
    for (int i = 0; i < numLeds; i++) {
      digitalWrite(leds[i], LOW);
    }
    delay(300);
  }
}
