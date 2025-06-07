# GS-EDGE

# 🌊 Sistema de Alerta Inteligente de Enchentes com Arduino

## 📌 Descrição do Problema

Em muitas regiões urbanas e ribeirinhas, chuvas intensas e rápidas elevações no nível da água causam alagamentos de ruas e residências. Esses eventos geram prejuízos materiais, colocam vidas em risco e exigem respostas rápidas por parte da população e autoridades.

## 🎯 Objetivo do Projeto

Desenvolver um sistema físico com Arduino capaz de:
- Monitorar o nível da água em tempo real
- Emitir alertas visuais (LEDs), sonoros (buzzer) e informativos (LCD)
- Ajudar comunidades vulneráveis a se prepararem com antecedência para possíveis inundações

---

## ⚙️ Componentes Utilizados

- Arduino Uno
- Sensor ultrassônico HC-SR04 (nível da água)
- Display LCD 16x2 (sem I2C)
- LEDs: verde, laranja e vermelho
- Buzzer
- Jumpers e resistores

---

## 🔁 Lógica de Funcionamento


1. O sensor **HC-SR04** mede a distância da água até o sensor, calculando o **nível de água em %**.
2. De acordo com o nível:
   - **Verde**: Nível seguro
   - **Laranja**: Alerta de atenção
   - **Vermelho + buzzer**: Alerta crítico (risco de enchente)
4. As informações do nível da água também são exibidas no LCD

---

## 🧪 Simulação Online

Você pode testar o funcionamento completo no Wokwi (sem precisar instalar nada).

🔗 **Link para simulação Wokwi:**  
👉 [Acesse aqui] (https://wokwi.com/projects/432948051224198145)
---

## 📽️ Vídeo Demonstrativo

🎬 **Assista à apresentação do projeto:**  


---

## 💻 Como Simular

1. Acesse o link do Wokwi
2. Clique em **"Start Simulation"**
3. Interaja com o sensor:
   - HC-SR04: Mude a posição do nível da água

---

## 🧠 Conhecimentos Aplicados

- Manipulação de sensores analógicos e digitais
- Controle de atuadores (LEDs, buzzer, LCD)
- Condições lógicas com `if/else`
- Exibição de dados no LCD


---

## Código

#include <LiquidCrystal_I2C.h>
#include <Wire.h>

// Definir pinos dos LEDs
const int ledVerde = 2;
const int ledAmarelo = 3;
const int ledVermelho = 4;
const int buzzer = 5;

// Definir pino do sensor ultrassônico HC-SR04
const int trigPin = 9;
const int echoPin = 10;

// Definir profundidade total do rio em cm
const float profundidadeTotalRioCm = 300.0; // 3 metros = 300 cm

// Inicializar o LCD com endereço I2C 
LiquidCrystal_I2C lcd(0x27, 16, 2); 

void setup() {
  Serial.begin(9600);

  // Configurar pinos dos LEDs e buzzer como OUTPUT
  pinMode(ledVerde, OUTPUT);
  pinMode(ledAmarelo, OUTPUT);
  pinMode(ledVermelho, OUTPUT);
  pinMode(buzzer, OUTPUT);

  // Configurar pinos do sensor ultrassônico
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);

  // Inicializar o LCD
  lcd.init();
  lcd.backlight(); // Ligar a luz de fundo do LCD
  lcd.setCursor(0, 0);
  lcd.print("Nivel do Rio:");
}

void loop() {
  // Limpar o TrigPin
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);

  // Acionar o TrigPin por 10 microssegundos
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);

  // Medir a duração do pulso no EchoPin
  long duration = pulseIn(echoPin, HIGH);

  // Calcular a distância em cm
  // A distância é (duração * velocidade do som) / 2 (ida e volta)
  float distanciaCm = duration * 0.0343 / 2;

  // Calcular o nível da água
  // Nível da água = Profundidade total do rio - distância medida pelo sensor
  float nivelAguaCm = profundidadeTotalRioCm - distanciaCm;
  float nivelAguaMetros = nivelAguaCm / 100.0; // Converter para metros

  // Exibir a distância e o nível da água no Serial Monitor (para debug)
  Serial.print("Distancia do sensor: ");
  Serial.print(distanciaCm);
  Serial.println(" cm");
  Serial.print("Nivel da Agua: ");
  Serial.print(nivelAguaMetros);
  Serial.println(" metros");

  // Limpar os LEDs e o buzzer antes de definir o novo estado
  digitalWrite(ledVerde, LOW);
  digitalWrite(ledAmarelo, LOW);
  digitalWrite(ledVermelho, LOW);
  noTone(buzzer); // Desliga o buzzer se estiver ligado

  // Lógica dos LEDs e buzzer baseada no nível da água
  if (nivelAguaMetros <= 2.0) {
    digitalWrite(ledVerde, HIGH);
    lcd.setCursor(0, 1);
    lcd.print("Nivel: OK       "); // Espaços para limpar a linha
  } else if (nivelAguaMetros > 2.0 && nivelAguaMetros <= 2.9) {
    digitalWrite(ledAmarelo, HIGH);
    lcd.setCursor(0, 1);
    lcd.print("Nivel: RISCO    ");
  } else if (nivelAguaMetros > 2.9) {
    digitalWrite(ledVermelho, HIGH);
    tone(buzzer, 1000); // Toca o buzzer com uma frequência de 1000 Hz
    lcd.setCursor(0, 1);
    lcd.print("Nivel: PERIGO!!! ");
  }

  // Atualiza o LCD com o valor do nível da água
  lcd.setCursor(10, 0); // Posição para imprimir o nível
  lcd.print(nivelAguaMetros, 2); // Imprime com 2 casas decimais
  lcd.print("m");

  delay(1000); // Aguarda 1 segundo antes da próxima leitura

  Serial.print("Duration (micros): ");
Serial.println(duration);

Serial.print("Distancia calculada (cm): ");
Serial.println(distanciaCm);

}
---
{
  "version": 1,
  "author": "Anonymous maker",
  "editor": "wokwi",
  "parts": [
    { "type": "wokwi-arduino-uno", "id": "uno", "top": 29.4, "left": -125.4, "attrs": {} },
    {
      "type": "wokwi-led",
      "id": "led1",
      "top": -80.4,
      "left": -140.2,
      "attrs": { "color": "green" }
    },
    {
      "type": "wokwi-led",
      "id": "led2",
      "top": -80.4,
      "left": -44.2,
      "attrs": { "color": "red" }
    },
    {
      "type": "wokwi-led",
      "id": "led3",
      "top": -80.4,
      "left": -92.2,
      "attrs": { "color": "red" }
    },
    {
      "type": "wokwi-buzzer",
      "id": "bz1",
      "top": -151.2,
      "left": 11.4,
      "attrs": { "volume": "0.1" }
    },
    { "type": "wokwi-hc-sr04", "id": "ultrasonic1", "top": -152.1, "left": 120.7, "attrs": {} },
    {
      "type": "wokwi-lcd1602",
      "id": "lcd1",
      "top": 112,
      "left": 303.2,
      "attrs": { "pins": "i2c" }
    },
    {
      "type": "wokwi-resistor",
      "id": "r1",
      "top": -5.65,
      "left": -163.2,
      "attrs": { "value": "1000" }
    },
    {
      "type": "wokwi-resistor",
      "id": "r2",
      "top": -5.65,
      "left": -57.6,
      "attrs": { "value": "1000" }
    },
    {
      "type": "wokwi-resistor",
      "id": "r3",
      "top": -15.25,
      "left": 48,
      "attrs": { "value": "1000" }
    }
  ],
  "connections": [
    [ "led1:C", "r1:1", "green", [ "v38.4", "h10" ] ],
    [ "led3:C", "r2:1", "green", [ "v38.4", "h19.6" ] ],
    [ "led2:C", "r3:1", "green", [ "v0" ] ],
    [ "led2:A", "uno:GND.1", "green", [ "v0" ] ],
    [ "led3:A", "uno:GND.1", "green", [ "v0" ] ],
    [ "led1:A", "uno:GND.1", "green", [ "v0" ] ],
    [ "bz1:2", "uno:5", "green", [ "v0" ] ],
    [ "r1:2", "uno:GND.2", "green", [ "v0" ] ],
    [ "r2:2", "uno:GND.2", "green", [ "v0" ] ],
    [ "r3:2", "uno:GND.2", "green", [ "v249.6", "h-68.4" ] ],
    [ "bz1:1", "uno:GND.2", "green", [ "v0" ] ],
    [ "ultrasonic1:VCC", "uno:5V", "red", [ "v326.4", "h-153.6", "v-19.2" ] ],
    [ "ultrasonic1:GND", "uno:GND.3", "black", [ "v336", "h-1.2" ] ],
    [ "ultrasonic1:TRIG", "uno:9", "green", [ "v0" ] ],
    [ "ultrasonic1:ECHO", "uno:10", "green", [ "v0" ] ],
    [ "lcd1:GND", "uno:GND.3", "black", [ "h0" ] ],
    [ "lcd1:VCC", "uno:5V", "red", [ "h0" ] ],
    [ "lcd1:SDA", "uno:A4", "green", [ "h0" ] ],
    [ "lcd1:SCL", "uno:A5", "green", [ "h0" ] ]
  ],
  "dependencies": {}
}
---
# Wokwi Library List
# See https://docs.wokwi.com/guides/libraries

# Automatically added based on includes:
LiquidCrystal I2C

---

**Nomes:** Manoah Leão e Caio Nascimento
**RM** 563713 e 561383

---

