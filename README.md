1.  **Objetivo do Projeto:** Definir a linguagem e implementar uma **Máquina de Turing Universal (MTU)** determinística. [cite_start]A MTU recebe como entrada a descrição de outra Máquina de Turing `M` e uma palavra `w`, e então simula a execução de `M` com a entrada `w`[cite: 1, 2].

2.  [cite_start]**Codificação da Entrada para a MTU:** A entrada completa para a MTU consiste na função de transição da máquina `M` (codificada como uma sequência de transições), seguida por um separador `$` e, por fim, a palavra de entrada `w` para a máquina `M`[cite: 3, 19].

3.  **Codificação dos Estados:**
    * [cite_start]Cada estado é representado pelo símbolo `q` seguido por um número em **notação unária** que o identifica (por exemplo, `q1`, `q11`, `q111`)[cite: 10, 12].
    * [cite_start]O **estado inicial** é, especificamente, `q1`[cite: 11].
    * [cite_start]Há um **único estado final**, designado por `qf`, a partir do qual nenhuma transição se origina[cite: 11].

4.  **Codificação dos Símbolos da Fita:**
    * [cite_start]Símbolos genéricos são representados pelo símbolo `a` seguido por um número em **notação unária** (por exemplo, `a1`, `a11`)[cite: 13, 14].
    * [cite_start]O símbolo **branco** é representado especificamente por `b`[cite: 14].
    * [cite_start]O símbolo de **início de fita** é `s`[cite: 15].

5.  [cite_start]**Definição da Máquina de Turing `M`:** A máquina `M` a ser simulada é uma Máquina de Turing determinística com uma fita finita à esquerda e infinita à direita[cite: 2]. Seus componentes são definidos da seguinte forma:
    * **`K` (Estados):** O conjunto de estados, codificados como descrito no item 3.
    * **`Σ` (Símbolos):** O conjunto de símbolos da fita, codificados como descrito no item 4.
    * [cite_start]**`δ` (Função de Transição):** Definida por uma sequência de transições, cada uma seguida por um separador `#`[cite: 4, 18].
    * [cite_start]**`s` (Estado Inicial):** O estado `q1`[cite: 11].
    * [cite_start]**`H` (Estado Final):** O conjunto contendo apenas o estado `qf`[cite: 11].

6.  [cite_start]**Formato da Transição (`δ`):** Cada transição da máquina `M` é definida por uma tupla de 5 elementos na seguinte ordem: **estado origem; símbolo lido; símbolo escrito; movimento; estado destino**[cite: 8].
    * [cite_start]O **Movimento** do cabeçote é representado por um único símbolo do conjunto `{R, L}`, onde `R` denota movimento para a direita e `L` para a esquerda[cite: 16].

7.  **Condições de Parada:** A simulação da máquina `M` pela MTU irá parar (halting) se uma das seguintes condições for atendida:
    * [cite_start]A máquina `M` atinge seu único estado final, `qf`[cite: 5].
    * [cite_start]A máquina `M` atinge um estado (não-final) a partir do qual não existe nenhuma transição definida para o símbolo que está sendo lido na fita[cite: 5].

8.  ***Convenção de Saída (Aceitação e Rejeição)***: O resultado da computação é indicado pela MTU na fita após a parada de `M`.
    * [cite_start]**Aceitação:** Se `M` para no estado final `qf`, a MTU deve escrever a constante **`#A`** na fita, a partir da primeira célula em branco à direita da palavra[cite: 6].
    * [cite_start]**Rejeição:** Se `M` para por não haver uma transição possível, a MTU deve escrever **`#R`** na mesma posição[cite: 7].

9.  [cite_start]**Representação da String de Entrada para a MTU:** A string completa a ser fornecida para a MTU é a justaposição da representação de todas as suas transições (separadas por `#`), seguida pelo separador `$` e a palavra de entrada `w` (uma sequência de símbolos)[cite: 3, 19]. Por exemplo: `q1a1a11Rq11#q11a11a111Lqf$sa1a11`.
