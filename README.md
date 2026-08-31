# Prática: Controle de Microservo com Potenciômetro

[![Simular no Tinkercad](https://img.shields.io/badge/Simular%20no-Tinkercad-orange?style=for-the-badge&logo=autodesk)](COLOQUE_AQUI_O_LINK_DO_SEU_PROJETO)

## Descrição do Projeto

Este projeto implementa um sistema de controle de um microservo utilizando um Arduino UNO e um potenciômetro.

O potenciômetro funciona como um dispositivo de entrada, permitindo que o Arduino realize a leitura de diferentes valores analógicos. Esses valores são convertidos em ângulos entre **0° e 180°**, controlando a posição do microservo.

Ao girar o potenciômetro, o valor lido pelo Arduino é alterado e o microservo acompanha essa mudança, movimentando-se de acordo com a posição do potenciômetro.

Dessa forma, o projeto demonstra a integração entre um dispositivo de entrada e um atuador, utilizando o Arduino para realizar o processamento e o controle do movimento.

---

## Sequência de Funcionamento

- O potenciômetro é movimentado pelo usuário.
- O Arduino realiza a leitura do valor analógico através da entrada **A0**.
- O valor lido varia entre **0 e 1023**.
- O Arduino converte esse valor para um ângulo entre **0° e 180°**.
- O valor do ângulo é enviado para o microservo.
- O microservo movimenta-se de acordo com a posição do potenciômetro.
- O processo é repetido continuamente.

### Funcionamento do Sistema

| Componente | Função |
| :---: | :--- |
| Potenciômetro | Fornece o valor de entrada para o Arduino |
| Arduino UNO | Realiza a leitura e controla o microservo |
| Microservo | Executa o movimento de acordo com o valor recebido |

---

## Materiais Utilizados

| Qtd | Componente |
| :---: | :--- |
| 1 | Placa Arduino UNO |
| 1 | Protoboard |
| 1 | Potenciômetro |
| 1 | Microservo |
| — | Fios Jumper macho-macho |

---

## Ligações do Circuito

| Componente | Arduino |
| :---: | :---: |
| Potenciômetro - pino central | A0 |
| Potenciômetro - alimentação | 5V |
| Potenciômetro - GND | GND |
| Microservo - sinal | Pino 9 |
| Microservo - alimentação | 5V |
| Microservo - GND | GND |

---

## Imagem do Circuito

![Circuito Controle de Microservo com Potenciômetro](imagem-do-circuito.png)

---

## Código Utilizado

```cpp
#include <Servo.h>

// Cria o objeto do microservo
Servo meuServo;

// Pino do potenciômetro
const int potenciometro = A0;

// Pino do microservo
const int pinoServo = 9;

// Variáveis
int leitura;
int angulo;

void setup() {

  // Define o pino do servo
  meuServo.attach(pinoServo);

  // Inicia a comunicação serial
  Serial.begin(9600);
}

void loop() {

  // Faz a leitura do potenciômetro
  leitura = analogRead(potenciometro);

  // Converte o valor de 0-1023 para 0-180 graus
  angulo = map(leitura, 0, 1023, 0, 180);

  // Move o servo para o ângulo correspondente
  meuServo.write(angulo);

  // Mostra os valores no monitor serial
  Serial.print("Valor do potenciometro: ");
  Serial.print(leitura);

  Serial.print(" | Angulo do servo: ");
  Serial.println(angulo);

  // Pequeno intervalo
  delay(15);
}
```

---

## Funcionamento

O potenciômetro envia um valor analógico para a entrada **A0** do Arduino. Esse valor pode variar de **0 a 1023**.

A função `map()` transforma esse valor em uma faixa de **0° a 180°**. Em seguida, o comando `servo.write()` envia o ângulo para o microservo.

Assim, quando o potenciômetro é girado, o microservo altera sua posição de acordo com o movimento realizado.

---

## Link do Projeto no Tinkercad
https://www.tinkercad.com/things/eK1B60ceqiK-incredible-wluff/editel?returnTo=https%3A%2F%2Fwww.tinkercad.com%2Fdashboard&sharecode=hPiDN3zIYtIiqTza5o8yhCcqYhlgM6UaX0mrTUiR6Gg
