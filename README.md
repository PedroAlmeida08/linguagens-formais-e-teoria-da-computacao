1.  **Objetivo do Projeto:** Implementar uma **Máquina de Turing Universal (MTU)** determinística. A MTU recebe como entrada a descrição de outra Máquina de Turing `M` e uma palavra `w`, e então simula a execução de `M` com a entrada `w`.

2.  **Codificação da Entrada para a MTU:** A entrada completa para a MTU consiste na função de transição da máquina `M` (codificada como uma sequência de transições), seguida por um separador `$` e, por fim, a palavra de entrada `w` para a máquina `M`.

3.  **Codificação dos Estados:**
    * Cada estado é representado pelo símbolo `q` seguido por um número em **notação unária** que o identifica (por exemplo, `q1`, `q11`, `q111`).
    * O **estado inicial** é, especificamente, `q1`.
    * Há um **único estado final**, designado por `qf`, a partir do qual nenhuma transição se origina.

4.  **Codificação dos Símbolos da Fita:**
    * Símbolos genéricos são representados pelo símbolo `a` seguido por um número em **notação unária** (por exemplo, `a1`, `a11`).
    * O símbolo **branco** é representado especificamente por `b`.

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
   
10. **Fita:** 
    A fita foi codificada de forma a simular 4 fitas, seguindo o seguinte formato: **(Entrada da MTU)&(Estado Atual)%(Símbolo Lido)@(Símbolos Escritos Até o Momento)**. Os parênteses foram utilizados apenas para fins ilustrativos e não são utilizados execução dessa MTU.
	Por exemplo: 
	A configuração q1a1a11Rq11#q11a11a111Lqf#q11a1a11Rq1$a1A11&q11%a11@a11
    1. **&q11** indica que o estado atual é o q11
    2. **%a11:** indica que o símbolo a ser lido é o a11
    3. **@a11:** indica que a execução da máquina até o momento, escreveu a11 na fita

11. **Funcionamento da Máquina**
		1. O estado atual (e inicial) é definido como `q1`
        2. O primeiro símbolo da palavra é lido (primeiro símbolo após `$`) e escrito após `%`.
        3. A máquina verifica o estado atual
        4. A máquina verifica se a partir do estado atual existe uma transição de saída.
        5. Se não houver, limpa a fita da escrita de todas as fitas simuladas e partir o primeiro caractere em branco após a palavra `w` escreve `#R` e transita ao único estado final `qf`.
        6. Se houver, verifica se essa transição de saída a partir do estado atual é uma transição que ocorre mediante a leitura do símbolo lido pela máquina (símbolo sobre o qual está o cabeçote da fita).
        7. Se não for, avança para a próxima transição.
        8. Se não houverem mais transições a serem lidas, limpa a fita da escrita de todas as fitas simuladas e partir o primeiro caractere em branco após a palavra `w` escreve `#R` e transita ao único estado final `qf`.
        9. Se for, verifica qual é o símbolo que deve ser escrito ao realizar essa transição e o escreve após o símbolo `@` se houver um espaço vazio após este símbolo ou, caso a máquina já tenha escrito algo, escreve o símbolo definido pela transição após o(s) símbolo(s) escrito(s) anteriormente.
        10. Verifica qual é e executa o movimento que deve ser executado ao realizar essa transição.
            1. Se for um movimento à direita (`R`) e o cabeçote já estiver sobre o último símbolo da palavra `w`, o cabeçote permanece na mesma posição.
            2. Se for um movimento à esquerda (`L`) e o cabeçote já estiver sobre o primeiro símbolo da palavra `w`, o cabeçote permanece na mesma posição.
		11. Verifica qual é o estado destino a partir da transição realizada e o escreve após o símbolo `&`, finalizando a transição e definindo-o como estado atual.
		12. Se o estado atual for `qf`, limpa a fita da escrita de todas as fitas simuladas e partir o primeiro caractere em branco após a palavra `w` escreve `#A` e transita ao único estado final `qf`.
		13. Se o estado atual não for `qf`, retorna ao passo 3.

12. **Testes Realizados**
    1. Palavra vazia
    2. Palavra sabidamente aceita
    3. Palavra a ser rejeitada
    4. Testes de funcionamento da máquina:
        1. Ausência de transição a partir do estado inicial
        2. Escrita e leitura de símbolos de tamanhos diferentes
            1. Por exemplo: a máquina está no estado q1 e transita para o estado q111 e é capaz de escrever essa informação sem sobreescrever outras já presentes na fita.
            2. O contrário também ocorre: a máquina está no estado q111 e transita para o estado q1 e é capaz de escrever essa informação sem deixar espaços em branco no meio da fita.

13. **Exemplos de uso:**
    1.  `q1a1a11Rq11#q11a11a111Lqf$`: Palavra vazia (Rejeitada)
    2.  `q1a1a11Rq11#q11a1a11Lq111#q11a1a11Rq1$a1`: Após leitura da  palavra, para em um estado não final que não possui transição de saída.(Rejeitada)
    3. `q1a1a11Rq11#q11a11a111Lqf#q11a1a11Rq1$a1a11`: Após leitura da  palavra, para em estado final. (Aceita)
    4.`q11a1a11Rq1#q1a1a11Rq11#q11a11a111Lqf$a1a11`: Mesma máquina e palavra do exemplo 3, mas começando a descrição da máquina em um estado que não seja o inicial. (Aceita)
	5.`q11a1a11Lqf#q11a11a111Rq1#q111a1a1Rq11$a11`: Conjunto de transições que não possuem transição de saída a partir do estado inicial. (Rejeitada)
