1.  **Objetivo do Projeto:** Definir a linguagem e implementar uma **Máquina de Turing Universal (MTU)** determinística. A MTU recebe como entrada a descrição de outra Máquina de Turing `M` e uma palavra `w`, e então simula a execução de `M` com a entrada `w`.

2.  **Codificação da Entrada para a MTU:** A entrada completa para a MTU consiste na função de transição da máquina `M` (codificada como uma sequência de transições), seguida por um separador `$` e, por fim, a palavra de entrada `w` para a máquina `M`.

3.  **Codificação dos Estados:**
    * Cada estado é representado pelo símbolo `q` seguido por um número em **notação unária** que o identifica (por exemplo, `q1`, `q11`, `q111`).
    * O **estado inicial** é, especificamente, `q1`.
    * Há um **único estado final**, designado por `qf`, a partir do qual nenhuma transição se origina.

4.  **Codificação dos Símbolos da Fita:**
    * Símbolos genéricos são representados pelo símbolo `a` seguido por um número em **notação unária** (por exemplo, `a1`, `a11`).
    * O símbolo **branco** é representado especificamente por `b`.
    * O símbolo de **início de fita** é `s`.

5.  **Definição da Máquina de Turing `M`:** A máquina `M` a ser simulada é uma Máquina de Turing determinística com uma fita finita à esquerda e infinita à direita. Seus componentes são definidos da seguinte forma:
    * **`K` (Estados):** O conjunto de estados, codificados como descrito no item 3.
    * **`Σ` (Símbolos):** O conjunto de símbolos da fita, codificados como descrito no item 4.
    * **`δ` (Função de Transição):** Definida por uma sequência de transições, cada uma seguida por um separador `#`.
    * **`s` (Estado Inicial):** O estado `q1`.
    * **`H` (Estado Final):** O conjunto contendo apenas o estado `qf`.

6.  **Formato da Transição (`δ`):** Cada transição da máquina `M` é definida por uma tupla de 5 elementos na seguinte ordem: **estado origem; símbolo lido; símbolo escrito; movimento; estado destino**.
    * O **Movimento** do cabeçote é representado por um único símbolo do conjunto `{R, L}`, onde `R` denota movimento para a direita e `L` para a esquerda.

7.  **Condições de Parada:** A simulação da máquina `M` pela MTU irá parar (halting) se uma das seguintes condições for atendida:
    * A máquina `M` atinge seu único estado final, `qf`.
    * A máquina `M` atinge um estado (não-final) a partir do qual não existe nenhuma transição definida para o símbolo que está sendo lido na fita. 

8.  ***Convenção de Saída (Aceitação e Rejeição)***: O resultado da computação é indicado pela MTU na fita após a parada de `M`.
    * **Aceitação:** Se `M` para no estado final `qf`, a MTU deve escrever a constante **`#A`** na fita, a partir da primeira célula em branco à direita da palavra.
    * **Rejeição:** Se `M` para por não haver uma transição possível, a MTU deve escrever **`#R`** na mesma posição.

9.  **Representação da String de Entrada para a MTU:** A string completa a ser fornecida para a MTU é a justaposição da representação de todas as suas transições (separadas por `#`), seguida pelo separador `$` e a palavra de entrada `w` (uma sequência de símbolos).
   
10. **Fitas:** 
    1. **Fita 1:** Conteúdo atual da fita da `MTU`
    2. **Fita 2:** Codificação da `MT`
    3. **Fita 3:** Estado atual da `MT`

11. **Exemplos de uso:**
    1.  `q1a1a11Rq11#q11a11a111Lqf$`: Palavra vazia (Rejeitada)
    2.  `q1a1a11Rq11#q11a1a11Lq111#q11a1a11Rq1$a1`: Após leitura da  palavra, para em estado não final (Rejeitada)
    3. `q1a1a11Rq11#q11a11a111Lqf#q11a1a11Rq1$a1a11`: Após leitura da  palavra, para em estado final (Aceita)
    4.`q11a1a11Rq1#q1a1a11Rq11#q11a11a111Lqf$a1a11`: Mesma máquina e palavra do exemplo 3, mas começando a descrição da máquina em um estado que não seja o inicial. (Aceita)
	5.`q11a11a111Lqf#q11a1a11Rq1#q1a1a11Rq11$a11`: Ação que não possui transição do estado inicial. (Rejeitada)
