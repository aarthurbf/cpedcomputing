# CHECKPOINT EDGE COMPUTING

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
1. Ligue os LEDs (verde, amarelo e vermelho) aos pinos 8, 9 e 10, respectivamente.
2. Conecte o buzzer (piezo) ao pino 11.
3. O fotoresistor (LDR) deve ser ligado à porta analógica A0.
4. Use os resistores de 220 ohms para os LEDs e o resistor de 10 kiloohms para o LDR.

## Código do Projeto
~~~arduino
//Definindo as portas
int LEDGreen = 8; //Led Verde na está na porta 8
int LEDYellow = 9;// Led Amarela está na porta9 
int LEDRed = 10;// Led Vermelha está na porta 10
int Buzzer = 11;//Buzina está na porta 11

//Definindo o pinMode (entrada ou saida)
void setup() {
  Serial.begin(9600);//velocidade de transmissão de bits
  pinMode(LEDGreen, OUTPUT);//Led Verde dispositivo de saída
  pinMode(LEDYellow, OUTPUT);//Led Amarelo dispositivo de saída
  pinMode(LEDRed, OUTPUT);//Led Vermelha dispositivo de saída
  pinMode(Buzzer, OUTPUT);//Buzina dispositivo de saída
}

//Definindo o que o sistema irá fazer
void loop() {
  int LDR = analogRead(A0); //Definido a variável LDR como Analog, na porta A0
  Serial.println(LDR);      //Mostrar o valor da variável LDR no Monitor Serial
  
  //Condicionais
  //Se o valor da varável LDR for menor que 900
  int INT = map(LDR, 0, 1023, 0, 100);
  if(INT<45){
    digitalWrite(LEDGreen, HIGH);//Led Verde Acesa
    digitalWrite(LEDYellow, LOW);//Led Amarela Apagada
    digitalWrite(LEDRed, LOW);// Led Vermelha Apagada
  }
  //Senão Se o valor da váriavel LDR estiver entre 900 e 950
  else if(INT>45 and INT<80) {
    digitalWrite(LEDGreen, LOW);         //Led Verde Apagada
    digitalWrite(LEDYellow, HIGH);       //Led Amarela Acesa
    digitalWrite(LEDRed, LOW);           //Led Vermelha Apagada
    tone(Buzzer,150,3000);               //Soar(Buzina, no "tom" 440, por 3000 milisegudos (3 segundos)
    delay(4000);                         //delay de 1000 milosegundos (1segundos)para a buzina voltar a soar, sendo 3000 durente a buzina e 1000 após terminar de tocar
  }
  //Senão Se o valor da varável LDR for maior que 950
  else if( INT>80){
      digitalWrite(LEDGreen, LOW);//Led Verde Apagada
      digitalWrite(LEDYellow, LOW);//Led Amarela Apagada
      digitalWrite(LEDRed, HIGH);//Led Vermelha Acesa
      tone(Buzzer,440,3000);//Soar(Buzina, no "tom" 440, por 3000 milisegudos (3 segundos)
      delay(4000);//delay de 1000 milosegundos (1segundos)para a buzina voltar a soar, sendo 3000 durente a buzina e 1000 após terminar de tocar
    }
           
}
~~~

## Possíveis Erros
Se o projeto não funcionar, verifique:
Se os jumpers estão corretamente conectados.
Se os resistores estão nos valores indicados.
Se o código foi carregado corretamente na placa Arduino.

## Desafios
Modificar a sensibilidade do sensor LDR.
Inverter o comportamento dos LEDs (pouca luz apaga o LED, muita luz acende o LED).
