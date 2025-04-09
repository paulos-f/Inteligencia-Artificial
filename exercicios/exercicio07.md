---

## ❄️ **Controle Fuzzy para Ar-Condicionado com Arduino**

### 📌 **Descrição do Problema**

Um sistema de ar-condicionado convencional liga ou desliga o compressor de forma abrupta com base em um único valor de temperatura, resultando em desconforto térmico e consumo desnecessário de energia. A proposta é implementar um **sistema de controle fuzzy** com Arduino que leve em consideração **a temperatura ambiente e a umidade relativa** para ajustar **a velocidade de um ventilador** (simulando a intensidade de resfriamento).

---

### 📥 **Entradas (Sensores)**

1. **Sensor de Temperatura (ex: DHT11/DHT22 ou LM35)**
   - **Universo**: 15°C a 35°C
   - **Conjuntos Fuzzy**:
     - **Frio**
     - **Agradável**
     - **Quente**
   - **Funções de Pertinência**:
     - Frio: triangular entre 15–20–25  
     - Agradável: triangular entre 20–25–30  
     - Quente: triangular entre 25–30–35

2. **Sensor de Umidade Relativa (ex: DHT11/DHT22)**
   - **Universo**: 20% a 90%
   - **Conjuntos Fuzzy**:
     - **Baixa**
     - **Média**
     - **Alta**
   - **Funções de Pertinência**:
     - Baixa: triangular entre 20–35–50  
     - Média: triangular entre 40–55–70  
     - Alta: triangular entre 60–75–90

---

### 📤 **Saída (Atuador)**

1. **Ventoinha com controle PWM (ex: cooler de 12V)**
   - **Universo**: 0 (desligado) a 255 (máxima velocidade)
   - **Conjuntos Fuzzy**:
     - **Baixa**
     - **Média**
     - **Alta**
   - **Funções de Pertinência**:
     - Baixa: triangular entre 0–64–128  
     - Média: triangular entre 64–128–192  
     - Alta: triangular entre 128–192–255

---

### 🧠 **Regras Fuzzy (If-Then)**

| Temperatura | Umidade | Velocidade da Ventoinha |
|-------------|---------|--------------------------|
| Frio        | Baixa   | Baixa                   |
| Frio        | Alta    | Média                   |
| Agradável   | Média   | Baixa                   |
| Quente      | Baixa   | Média                   |
| Quente      | Alta    | Alta                    |
| Agradável   | Alta    | Média                   |
| Frio        | Média   | Baixa                   |
| Quente      | Média   | Alta                    |
| Agradável   | Baixa   | Baixa                   |

---

### 🛠️ **Resumo de Componentes para Arduino**

| Componente         | Função                      |
|--------------------|-----------------------------|
| Arduino Uno/Nano   | Processador central         |
| Sensor DHT11/DHT22 | Mede temperatura e umidade  |
| Transistor TIP120  | Controla a ventoinha via PWM|
| Ventoinha 12V      | Simula o ar-condicionado    |
| Fonte externa 12V  | Alimenta a ventoinha        |

---

### 📎 **Observações Finais**

- A lógica fuzzy melhora o **conforto térmico** adaptando-se suavemente ao ambiente.
- Pode ser facilmente implementada com bibliotecas como [`fuzzy.h`](https://github.com/karpathy/Arduino-Fuzzy) ou escrita manualmente usando funções `if-else` com pesos.
- O sistema pode ser estendido para incluir **presença de pessoas**, **nível de CO₂**, ou até **controle via Bluetooth/Wi-Fi**.

---
