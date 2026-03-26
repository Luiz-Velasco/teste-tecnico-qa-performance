# 🚀 Teste de Performance - BlazeDemo

## 📌 Objetivo

Realizar testes de performance na aplicação https://www.blazedemo.com, simulando o fluxo de compra de passagem aérea e avaliando se o sistema atende ao seguinte critério de aceitação:

* **250 requisições por segundo**
* **Tempo de resposta no percentil 90 (P90) inferior a 2 segundos**

---

## 🧪 Cenário Testado

Fluxo completo de compra de passagem:

1. Acessar página inicial (Home)
2. Buscar voos (Find Flights)
3. Selecionar voo (Select Flight)
4. Finalizar compra (Purchase)

Validação realizada através de assertion verificando a mensagem:

```
Thank you for your purchase today!
```

---

## 🛠️ Ferramenta Utilizada

* Apache JMeter 5.6.3

---

## ⚙️ Teste de Carga

### Configuração

* Threads (usuários): 200
* Ramp-up: 5 segundos
* Loop: Contínuo
* Temporizador: Constant Throughput Timer = **250 req/s**

---

### 📊 Resultados

| Métrica        | Resultado |
| -------------- | --------- |
| Throughput     | ~5 req/s  |
| P90 (90% Line) | ~1362 ms  |
| Taxa de erro   | 0%        |

---

### 📈 Análise

* O sistema apresentou **boa performance em tempo de resposta**, mantendo o P90 abaixo de 2 segundos.
* Entretanto, o throughput máximo atingido foi de aproximadamente **5 requisições por segundo**, muito abaixo do esperado (250 req/s).
* Mesmo com aumento do número de usuários virtuais, **não houve ganho significativo de vazão**.

---

## 🔥 Teste de Pico (Spike Test)

### Configuração

* Threads (usuários): 200
* Ramp-up: 2 segundos
* Loop: 1

---

### 📊 Resultados

| Métrica           | Resultado             |
| ----------------- | --------------------- |
| Taxa de erro      | 100%                  |
| Tempo de resposta | 0 ms                  |
| Throughput        | ~400 req/s (não real) |

---

### 📈 Análise

Durante o teste de pico, foi simulado um aumento abrupto de usuários simultâneos.

Observou-se taxa de erro de 100%, com tempos de resposta zerados, indicando falha imediata nas requisições.

O throughput elevado observado não representa processamento real, mas sim respostas de erro retornadas rapidamente.

---

## ⚠️ Conclusão Geral

O sistema **não atende ao critério de aceitação** estabelecido.

Apesar de apresentar bom tempo de resposta em baixa carga, a aplicação:

* Não escala com aumento de usuários
* Não atinge o throughput esperado de 250 req/s
* Falha completamente sob carga de pico

Isso indica limitações de escalabilidade e ausência de resiliência sob alta concorrência.

---

## ▶️ Como Executar o Teste

1. Abrir o Apache JMeter
2. Importar o arquivo `teste.jmx`
3. Executar o teste clicando em **Start (▶️)**
4. Acompanhar os resultados no **Relatório Agregado**

---

## 📁 Estrutura do Projeto

```
/teste-performance
 ├── teste.jmx
 └── README.md
```

---

## 💡 Considerações Finais

Os testes realizados demonstram que o sistema não está preparado para cenários de alta carga e picos de acesso, sendo necessário avaliar melhorias na arquitetura e infraestrutura para suportar maior volume de requisições.

---

## 👨‍💻 Autor

Luiz Velasco
