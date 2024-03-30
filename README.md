## Projeto de Medição de Luz com Arduino
Este projeto utiliza um Arduino para medir a quantidade de luz ambiente e controlar LEDs de acordo com a luminosidade. O sistema possui três estágios de iluminação, indicados por LEDs de diferentes cores e acompanhados por beeps sonoros. Vamos criar um arquivo .readme para documentar esse projeto.

## Descrição do Projeto
O objetivo é criar um sistema que monitore a intensidade de luz em um ambiente e ajuste os LEDs conforme a luminosidade. Aqui estão os detalhes:

## Funcionamento:
Se a luz estiver baixa, o LED verde estará aceso.
Se a luminosidade aumentar, o LED amarelo acenderá.
Se o ambiente estiver muito claro, o LED vermelho será ativado, acompanhado por um alerta sonoro.

## Componentes Necessários:
* Arduino Uno
* Placa de protoboard
* 3 LEDs (verde, amarelo e vermelho)
* 1 fotoresistor (LDR - Light Dependent Resistor)
* 1 buzzer (piezo)
* 3 resistores de 220 ohms
* 1 resistor de 10 kiloohms
  
## Funcionamento Ambiental:
O sistema deve estar em um ambiente escuro para funcionar corretamente.
Foi desenvolvido para controlar a intensidade de luz em uma vinícola, onde o vinho é armazenado.
Montagem do Circuito

## Conecte os componentes conforme o esquema abaixo:
. Ligue os LEDs (verde, amarelo e vermelho) aos pinos 8, 9 e 10, respectivamente.
. Conecte o buzzer (piezo) ao pino 11.
. O fotoresistor (LDR) deve ser ligado à porta analógica A0.
. Use os resistores de 220 ohms para os LEDs e o resistor de 10 kiloohms para o LDR.

## Código do Projeto

// Projeto de Medição de Luz Ambiente

int LEDGreen = 8;   // LED Verde na porta 8
int LEDYellow = 9;  // LED Amarelo na porta 9
int LEDRed = 10;    // LED Vermelho na porta 10
int Buzzer = 11;    // Buzina na porta 11

void setup() {
  Serial.begin(9600);  // Velocidade de transmissão de bits
  pinMode(LEDGreen, OUTPUT);
  pinMode(LEDYellow, OUTPUT);
  pinMode(LEDRed, OUTPUT);
  pinMode(Buzzer, OUTPUT);
}

void loop() {
  int LDR = analogRead(A0);  // Leitura do sensor LDR
  Serial.println(LDR);       // Mostra o valor no Monitor Serial

  // Condições para os LEDs
  int INT = map(LDR, 0, 1023, 0, 100);
  if (INT < 45) {
    digitalWrite(LEDGreen, HIGH);
    digitalWrite(LEDYellow, LOW);
    digitalWrite(LEDRed, LOW);
  } else if (INT > 45 && INT < 80) {
    digitalWrite(LEDGreen, LOW);
    digitalWrite(LEDYellow, HIGH);
    digitalWrite(LEDRed, LOW);
  } else {
    digitalWrite(LEDGreen, LOW);
    digitalWrite(LEDYellow, LOW);
    digitalWrite(LEDRed, HIGH);
    tone(Buzzer, 1000);  // Beep no LED vermelho
  }
  delay(10);
}

## Possíveis Erros
Se o projeto não funcionar, verifique:
Se os jumpers estão corretamente conectados.
Se os resistores estão nos valores indicados.
Se o código foi carregado corretamente na placa Arduino.

## Desafios
Modificar a sensibilidade do sensor LDR.
Inverter o comportamento dos LEDs (pouca luz apaga o LED, muita luz acende o LED).
