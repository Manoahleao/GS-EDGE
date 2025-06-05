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



**Nomes:** Manoah Leão e Caio Nascimento
**RM** 563713 e 

---

