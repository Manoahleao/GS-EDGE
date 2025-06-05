# GS-EDGE

# 🌊 Sistema de Alerta Inteligente de Enchentes com Arduino

## 📌 Descrição do Problema

Em muitas regiões urbanas e ribeirinhas, chuvas intensas e rápidas elevações no nível da água causam alagamentos de ruas e residências. Esses eventos geram prejuízos materiais, colocam vidas em risco e exigem respostas rápidas por parte da população e autoridades.

## 🎯 Objetivo do Projeto

Desenvolver um sistema físico com Arduino capaz de:
- Monitorar o nível da água em tempo real
- Detectar condições de risco (chuva, umidade, enchente)
- Emitir alertas visuais (LEDs), sonoros (buzzer) e informativos (LCD)
- Ajudar comunidades vulneráveis a se prepararem com antecedência para possíveis inundações

---

## ⚙️ Componentes Utilizados

- Arduino Uno
- Sensor de temperatura e umidade DHT22
- Sensor ultrassônico HC-SR04 (nível da água)
- Display LCD 16x2 (sem I2C)
- LEDs: verde, laranja e vermelho
- Buzzer
- Jumpers e resistores

---

## 🔁 Lógica de Funcionamento

1. O sensor **DHT22** monitora a temperatura e umidade.
2. O sensor **HC-SR04** mede a distância da água até o sensor, calculando o **nível de água em %**.
3. De acordo com o nível:
   - **Verde**: Nível seguro
   - **Laranja**: Alerta de atenção
   - **Vermelho + buzzer**: Alerta crítico (risco de enchente)
4. As informações também são exibidas no **LCD**, incluindo temperatura, umidade e nível da água.

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
3. Interaja com os sensores:
   - DHT22: Altere a temperatura/umidade
   - HC-SR04: Mude a posição do obstáculo para simular aumento da água

---

## 🧠 Conhecimentos Aplicados

- Manipulação de sensores analógicos e digitais
- Controle de atuadores (LEDs, buzzer, LCD)
- Condições lógicas com `if/else`
- Mapeamento de valores com `map()`
- Exibição de dados no LCD
- Serial Monitor para debug

---

## 📁 Código Fonte

O código está em `flood_alert.ino`,

---




**Nome:** Manoah Leão e Caio Nascimento
**RM** 563713 e 

---

