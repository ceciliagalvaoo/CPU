# 🧠 CPU Simplificada de 8 Bits – Logisim

&emsp;Este projeto implementa uma **CPU de 8 bits com ciclo único**, construída do zero no simulador Logisim. A CPU é capaz de executar operações aritméticas e lógicas básicas a partir de instruções codificadas manualmente em uma memória ROM.

---

## ⚙️ Funcionalidades

- **Arquitetura de ciclo único**: cada instrução é buscada, decodificada e executada em um único pulso de clock.
- **ALU personalizada** com as seguintes operações:
  - Soma / Subtração (ADD / SUB)
  - Multiplicação (MULT)
  - Comparação (Set Less Than – SLT)
  - Operações lógicas: AND, OR, NOR
  - Shift lógico à esquerda (SHL) e à direita (SHR)
- **Registrador acumulador**: armazena o resultado atual e serve como entrada A da ALU.
- **Program Counter (PC)**: incrementa a cada pulso de clock, controlando qual linha da ROM será executada.
- **ROM com instruções fixas** no formato de 12 bits: `4 bits para operação` + `8 bits para operando`.
- **MUX de formatação final**: permite aplicar SHL ou SHR ao resultado da ALU antes de armazená-lo.
- **Display de 7 segmentos e hexadecimal**: exibe o valor atual do acumulador de forma visual e interativa.

---

## 📚 Formato da Instrução

Cada instrução possui 12 bits:

```
[ 4 bits de operação ][ 8 bits de operando ]
```

Exemplo:
- `30A` → ADD 10
- `332` → ADD 50
- `3FF` → SUB 1 (complemento de dois)
- `02C` → AND 60
- `1F0` → OR 240
- `2FF` → NOR 255
- `504` → MULT 4
- `4FF` → SLT 255



---

## 🧪 Como funciona cada ciclo

A cada pulso de clock:
1. O PC envia um endereço para a ROM.
2. A ROM devolve a instrução correspondente.
3. A ALU recebe:
   - Entrada A: valor do acumulador
   - Entrada B: operando da instrução
   - Seletor de operação: opcode da instrução
4. A ALU executa a operação.
5. O resultado passa por um MUX final (SHL/SHR).
6. O valor final é salvo no registrador acumulador.
7. O resultado é exibido nos displays.

---

## 💡 Observações

- O acumulador **não é resetado automaticamente** quando o PC volta a 0. Isso é o comportamento esperado em arquiteturas de 1 ciclo.
- O valor `FF` é interpretado como `-1` apenas em operações aritméticas, pois usa complemento de dois. Em operações lógicas, é tratado como `255`.

---

## 🧰 Tecnologias

- Logisim (versão padrão)
- Circuitos criados manualmente a partir de portas lógicas, multiplexadores, somadores, registradores, etc.

---

## ✍️ Conclusão 
&emsp;Este projeto foi fundamental para consolidar o entendimento prático de como os principais componentes de uma CPU se conectam e interagem em um ciclo de instrução completo. A construção manual de cada parte — desde a ALU até o registrador acumulador, passando pelo controle de fluxo com o PC e ROM — permitiu explorar conceitos essenciais da arquitetura de computadores de forma concreta e visual. Além de aplicar operações aritméticas e lógicas básicas, a CPU também foi estendida com funcionalidades adicionais como shift left/right e um multiplexador final, simulando aspectos comuns de pipelines reais. Ao final do projeto, a CPU demonstrou ser capaz de executar programas simples, mantendo estado entre ciclos e exibindo resultados em displays binários e hexadecimais. A experiência mostrou como lógica digital e controle se combinam para formar o coração de qualquer sistema computacional.
