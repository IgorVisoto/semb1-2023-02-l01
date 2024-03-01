# Questionário Sistemas Embarcados I

## 1. Explique brevemente o que é compilação cruzada (***cross-compiling***) e para que ela serve.
Geralmente ao escolhermos um micro-controlador, o mesmo tem uma arquitetura diferente do ambiente de desenvolvimento, sendo assim é preciso utilizar a compilação cruzada, para que se possa utilizar, por exemplo, um computador com sistema INTEL ou AMD, para desenvolver um código de um micro-controlador que utiliza arquitetura ARM.

## 2. O que é um código de inicialização ou ***startup*** e qual sua finalidade?
Ao executar um programa utilizando a função main(), diversas tarefas são integradas e foram executadas antes do início do nosso programa. 

Ao utilizarmos a arquitetura do ARM Cortex-M, como não possuímos sistema operacional, devemos fornecer um código com as tarefas a serem realizadas, e a esse código damos o nome de startup.c.

Podemos concluir então que o startup é a forma encontrada de fornecer a lista de tarefas a serem realizadas anteriormente ao nosso programa nos microcontroladores que não possuem um sistema operacional.


## 3. Sobre o utilitário **make** e o arquivo **Makefile responda**:

#### (a) Explique com suas palavras o que é e para que serve o **Makefile**.
O Makefile tem como sua principal função automatizar o processo de compilação, pois ao construir um programa, é necessário informar diversos parâmetros ao código, então é uma ferramenta que traz uma melhoria muito grande quando pensamos, por exemplo, em programas que possuem diversos arquivos fonte, pois torna muito menos trabalhoso encontrar falhas e alterar dados, por exemplo.
#### (b) Descreva brevemente o processo realizado pelo utilitário **make** para compilar um programa.
O make é utilizado para compilar as instruções que estão no arquivo Makefile. Então ao montar o seu makefile, colocando as informações necessárias, como: definição de variáveis, comentários, regras explícitas e implícitas, você utiliza o comando make para trazer essas informações ao programa que você está construindo o código, e precisa das informações acima.
O make é utilizado para compilar as instruções que estão no arquivo Makefile. Então ao montar o seu makefile, colocando as informações necessárias, como: definição de variáveis, comentários, regras explícitas e implícitas, você utiliza o comando make para trazer essas informações ao programa que você está construindo o código, e precisa das informações acima.

#### (c) Qual é a sintaxe utilizada para criar um novo **target**?
Para se criar um novo **target** devemos escrever o nome do arquivo separados por espaços. 

Exemplo:  

main.o: main.c

target:  arm-none-eabi-gcc -c -g -mcpu=cortex-m4 -mthumb -O0 -Wall main.c -o main.o

#### (d) Como são definidas as dependências de um **target**, para que elas são utilizadas?

Para definirmos as dependências de um target devemos atualizar o comando all, pois ao executar o makefile sem utilizar dependências, apenas o primeiro target será executado, para isso é preciso informar as dependências no makefile utilizando o all.

 Exemplo:

all: startup.o main.o

main.o: main.c
	$(CC) -c $(CFLAGS) $< -o $@

startup.o: startup.c
	$(CC) -c $(CFLAGS) $< -o $@

No exemplo acima, informamos que o main.o tem dependência do startup.o


#### (e) O que são as regras do **Makefile**, qual a diferença entre regras implícitas e explícitas?
O make é utilizado para compilar automaticamente programas e bibliotecas informadas no makefile, esses programas contidos no makefile são separados em diferentes tipos de elementos, dois deles são as regras implícitas e explícitas.

Que são: 

regras implícitas: Tem ligação com o nome do arquivo, dizendo quando refazer uma classe de arquivos levando em consideração seu nome e criar uma receita para atualizar esse arquivo.

regras explícitas: Utilizada para refazer um ou mais arquivos, listando os arquivos que dependem dela e chamando os pré-requisitos para os alvos.

## 4. Sobre a arquitetura **ARM Cortex-M** responda:

### (a) Explique o conjunto de instruções ***Thumb*** e suas principais vantagens na arquitetura ARM. Como o conjunto de instruções ***Thumb*** opera em conjunto com o conjunto de instruções ARM?
O conjunto de instruções Thumb é uma extensão do conjunto de instruções ARM e tem como objetivo fornecer maior eficiência em termos de tamanho de código e consumo de energia, especialmente em sistemas embarcados.
As instruções ARM são mais compactas e ocupam apenas 16 bits, enquanto as instruções ARM ocupam 32 bits, o que economiza significativamente espaço de armazenamento e reduz a quantidade de dados transferidos da memória para a unidade de processamento.

### (b) Explique as diferenças entre as arquiteturas ***ARM Load/Store*** e ***Register/Register***.

Tanto a arquitetura de carregamento/armazenamento ARM quanto a arquitetura de registro/registro são abordagens diferentes para lidar com operações de memória no processamento ARM.
 Na arquitetura de carregamento/armazenamento usada em processadores mais simples, chamada RISC, a memória não opera diretamente nos registradores, portanto, você carrega dados da memória em registradores  e armazena dados em registradores de memória.
 São necessárias instruções especiais.
 Desta forma,  as operações de acesso à memória são separadas das operações aritméticas.
 A arquitetura registrador/registro permite que operações aritméticas sejam realizadas diretamente entre registradores sem acesso à memória, tornando as operações mais eficientes e reduzindo dependências de memória.
 No entanto, isto aumenta a complexidade e exige a disponibilidade de mais registos

### (c) Os processadores **ARM Cortex-M** oferecem diversos recursos que podem ser explorados por sistemas baseados em **RTOS** (***Real Time Operating Systems***). Por exemplo, a separação da execução do código em níveis de acesso e diferentes modos de operação. Explique detalhadamente como funciona os níveis de acesso de execução de código e os modos de operação nos processadores **ARM Cortex-M**.

Os processadores ARM Cortex-M têm dois níveis de acesso principais: privilegiado e  não privilegiado.
 Os usuários privilegiados podem usar todas as instruções e acessar todos os recursos, enquanto os usuários não privilegiados têm acesso limitado.
 Dessa forma, o acesso  à memória, aos periféricos e às instruções em linguagem de máquina é restrito.
 Além disso, esses processadores possuem diversos modos de operação que afetam o conjunto de instruções acessíveis e o uso dos recursos do sistema.

### (d) Explique como os processadores ARM tratam as exceções e as interrupções. Quais são os diferentes tipos de exceção e como elas são priorizadas? Descreva a estratégia de **group priority** e **sub-priority** presente nesse processo.

### (e) Qual a diferença entre os registradores **CPSR** (***Current Program Status Register***) e **SPSR** (***Saved Program Status Register***)?
Ambos os registros no processador ARM Cortex M são usados ​​para armazenar informações sobre o estado atual  ou  salvo do processador durante a execução da instrução.
 Portanto, o CPSR, como o próprio nome sugere, mantém informações sobre o estado atual do processador ao executar instruções no processador, normalmente os estados dos sinalizadores que são afetados ao executar instruções do tipo condicional.
 SPSR salva o estado  CPSR antes de entrar no modo de exceção.
 Portanto, quando ocorre uma exceção, o estado do CPRS é copiado para o SPSR antes 

### (f) Qual a finalidade do **LR** (***Link Register***)?
Quando uma função é chamada, o endereço  para o qual a função precisa retornar é armazenado no registrador de link.
 Em outras palavras, é como um marcador  que indica para onde você precisa retornar quando todo o processo da função for finalizado.

### (g) Qual o propósito do Program Status Register (PSR) nos processadores ARM?
O PSR ARM é um registro de 32 bits que controla e reflete o status do processador.
 Eles permitem que as operações do sistema determinem rapidamente o status atual do processador e também habilitam código de baixo nível (baixo nível).
 Modifique com eficiência a execução do seu ambiente.


### (h) O que é a tabela de vetores de interrupção?
As tabelas de vetores de interrupção são a base para o gerenciamento de rotinas de tratamento de interrupções.
 Quando uma interrupção é acionada, o processador mantém seu estado atual e começa a executar a rotina apontada pelo vetor correspondente.
 Na arquitetura ARM, 15 vetores são reservados para exceções geradas, começando pelo primeiro vetor de interrupção, o “reset handler”, no endereço 0x0000 0004, e os endereços são alocados durante o processo de vinculação.
 Definir esta tabela é importante para evitar comportamentos inesperados quando ocorrem exceções não tratadas.
 Portanto, deve ser reservado espaço suficiente no início da memória flash para armazenar toda a tabela de dispositivos, o que requer uma alocação de 408 bytes.


### (i) Qual a finalidade do NVIC (**Nested Vectored Interrupt Controller**) nos microcontroladores ARM e como ele pode ser utilizado em aplicações de tempo real?

O NVIC é um componente  para gerenciar e responder a eventos de interrupção, independente de sua origem.
 Isso fornece uma maneira eficaz de lidar com essas situações de maneira ordenada e priorizada.
 Garante que as interrupções de alta prioridade sejam priorizadas e os eventos importantes sejam processados ​​primeiro, garantindo uma resposta rápida.
 Além disso, ele pode lidar com interrupções que ocorrem durante o processamento de outra interrupção, permitindo lidar com múltiplas situações de interrupção.
 Os NVICs são configuráveis ​​e podem ser adaptados aos requisitos específicos da aplicação.
 Em sistemas de tempo real, o NVIC garante  tratamento de interrupções eficiente e oportuno.

### (j) Em modo de execução normal, o Cortex-M pode fazer uma chamada de função usando a instrução **BL**, que muda o **PC** para o endereço de destino e salva o ponto de execução atual no registador **LR**. Ao final da função, é possível recuperar esse contexto usando uma instrução **BX LR**, por exemplo, que atualiza o **PC** para o ponto anterior. No entanto, quando acontece uma interrupção, o **LR** é preenchido com um valor completamente  diferente,  chamado  de  **EXC_RETURN**.  Explique  o  funcionamento  desse  mecanismo  e especifique como o **Cortex-M** consegue fazer o retorno da interrupção. 

### (k) Qual  a  diferença  no  salvamento  de  contexto,  durante  a  chegada  de  uma  interrupção,  entre  os processadores Cortex-M3 e Cortex M4F (com ponto flutuante)? Descreva em termos de tempo e também de uso da pilha. Explique também o que é ***lazy stack*** e como ele é configurado. 


## Referências

### Básicas

[1] [STM32F411xC Datasheet](https://www.st.com/resource/en/datasheet/stm32f411ce.pdf)

[2] [RM0383 Reference Manual](https://www.st.com/resource/en/reference_manual/rm0383-stm32f411xce-advanced-armbased-32bit-mcus-stmicroelectronics.pdf)

[3] [Using the GNU Compiler Collection (GCC)](https://gcc.gnu.org/onlinedocs/gcc/index.html)

[4] [GNU Make](https://www.gnu.org/software/make/manual/html_node/index.html)

### Vídeos Microsoft Teams

[5] [05 - Introdução à arquitetura de computadores](https://web.microsoftstream.com/embed/channel/f6b3a0de-e6f3-4652-b2d5-f1164032498a?app=microsoftteams&sort=undefined&l=pt-br#)

[6] [06 - Arquitetura Cortex-M Parte 1/2](https://web.microsoftstream.com/embed/channel/f6b3a0de-e6f3-4652-b2d5-f1164032498a?app=microsoftteams&sort=undefined&l=pt-br#)

[7] [07 - Arquitetura Cortex-M Parte 2/2](https://web.microsoftstream.com/embed/channel/f6b3a0de-e6f3-4652-b2d5-f1164032498a?app=microsoftteams&sort=undefined&l=pt-br#)

[8] [08 - Microcontroladores STM32](https://web.microsoftstream.com/embed/channel/f6b3a0de-e6f3-4652-b2d5-f1164032498a?app=microsoftteams&sort=undefined&l=pt-br#)

[9] [10 - Introdução à arquitetura de computadores](https://web.microsoftstream.com/embed/channel/f6b3a0de-e6f3-4652-b2d5-f1164032498a?app=microsoftteams&sort=undefined&l=pt-br#)

### Material Suplementar

[5] [A General Overview of What Happens Before main()](https://embeddedartistry.com/blog/2019/04/08/a-general-overview-of-what-happens-before-main/)
 
[6] [Bare metal embedded lecture-1: Build process](https://youtu.be/qWqlkCLmZoE?si=mn5yDnJYudQ1PpZH)
 
[7] [Bare metal embedded lecture-2: Makefile and analyzing relocatable obj file](https://youtu.be/Bsq6P1B8JqI?si=yuNLPj3JQ-2IT1yo)
 
[8] [Bare metal embedded lecture-3: Writing MCU startup file from scratch](https://youtu.be/2Hm8eEHsgls?si=c27MpZ47ApiMSwHR)
 
[9] [Lecture 15: Booting Process](https://youtu.be/3brOzLJmeek?si=MsHRUEJP8zofjwJQ)
