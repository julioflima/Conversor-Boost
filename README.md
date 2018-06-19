# CONVERSOR BOOST

##### UNIVERSIDADE FEDERAL DO CEARÁ, CAMPUS SOBRAL
##### 
##### ENGENHARIA ELÉTRICA, DISCIPLINA ELETRÔNICA DE POTÊNCIA
##### 

##### 1. FLÁVIA PEROZA RUIZ
##### 2. JULIO CESAR FERREIRA LIMA
##### 3. MATHEUS PIRES DE FARIAS
##### 4. YARA MACHADO OLIVEIRA

> ISSO É APENAS UM RESUMO, PARA MAIOR RIQUEZA DE DETALHES VER A VERSÃO EM PDF "Relatório de Potência.pdf".

## 1. INTRODUÇÃO

Quando se trata de mudanças em níveis de tensão em corrente contínua, não é
possível ser feito através de transformadores. A conversão de uma tensão contínua de um
nível a outro e feita a partir de conversores CC.
Existem algumas topologias de circuitos conversores, dentre elas quatro se
destacam: buck, boost, buck-boost e cùk. Todas essas topologias são baseadas no uso de
chaves eletrônicas (diodos, MOSFETs, etc) e indutores. O uso de capacitores em circuitos
conversores é comum pois são usados como filtros da tensão de saída.
Esses conversores normalmente são usados como reguladores chaveados. A
regulação é feita a partir de um PWM de frequência e uma chave (MOSFET, TGJ ou
IGBT). Para um melhor entendimento do processo de chaveamento é necessário o
conceito inicial de tempo de chave aberta e fechada, em um período T e uma razão cíclica
(duty cycle). O princípio do duty cycle é mostrado na figura 1.
Figura 1: Chaveamento em uma tensão de entrada Vs.


### 1 .1. CONVERSOR BOOST

O conversor boost é um conversor chaveado elevador, ou seja, fornece um ganho
de tensão na saída. Além disso, também apresenta características de fonte de corrente na
entrada e fonte de tensão na saída. O circuito do conversor boost é mostrado na figura 2.


Analisando esse circuito em seus dois modos de operação referentes ao
chaveamento, chave aberta e chave fechada, podemos observar duas situações para a
variação de corrente do indutor.
Para as análises feitas a seguir, consideraremos as seguintes características do duty
cycle, como mostrada na figura 3 e a equação 1.1.


#### 1.1.1. Chave fechada

Analisando a figura 4, conversor com a chave fechada, percebemos que a tensão em
cima do indutor, VL, é a mesma que VS de entrada.


Considerando a taxa de variação da corrente como constante, aumentando
linearmente enquanto a chave estiver fechada, e que o tempo em que a chave permanece
fechada é DT,a variação da corrente pode ser calculada por:



#### 1.1.2. CHAVE ABERTA

A figura 5 demonstra o funcionamento do circuito com a chave aberta. Analisando
percebemos que a tensão em cima do indutor se torna (VS - VO).

Fazendo a mesma análise para a variação da corrente feita para a chave fechada,
consideramos o tempo de chave aberto como (1-D)T. A equação 1.4 nos fornece a
variação da corrente no indutor para o circuito com a chave aberta.

#### 1.1.3. Ganho

Tomando as equações 1.3 e 1.4 como referência e igualando, obtemos a expressão
de ganho do conversor boost, mostrada na equação 1.5.

#### 1.1.4. Cálculo da corrente

Em conversores ideais podemos considerar a potência de entrada e de saída como
as mesmas. A partir disso encontramos uma reação para a corrente média do indutor, dada
pela equação.

Partindo disso são determinados os valores máximos e mínimos da corrente no
indutor. Observamos através da figura 6 o valor médio e as variações.

#### 1.1.5. Indutância mínima

Para uma condução contínua de corrente no indutor, a corrente deve ser maior que
zero. Igualamos então a equação 1.7 a zero para obtermos a indutância mínima no modo
contínuo.

Vale ressaltar que este valor é o de indutância mínima, não é o mesmo usado no
projeto. O indutor usado no conversor será calculado através das equações 1.3 e 1.4, de
acordo com os parâmetros que serão usados no projeto.


#### 1.1.6. Ondulação de tensão na saída

De acordo com a forma de onda da figura 7 encontramos a carga no capacitor
apenas calculando a área coberta de ranhuras.

Partindo da equação 1.10, observamos que a corrente do capacitor é proporcional
à derivada da tensão de saída. Considerando que corrente é a derivada da carga em função
do tempo, obtemos a equação 1.11.

Com isso, encontramos a expressão característica da variação da tensão de saída
de um conversor boost.

#### 1.1.7. Corrente no diodo

No conversor boost, o diodo se encontra em série com o indutor quando a chave
está aberta, a forma de onda será similar à da corrente no indutor quando o a chave estiver
aberta e zero quando a chave estiver fechada, como mostra a figura 8.

### 1.2. GERADOR DE PWM

O CI usado para realizar o chaveamento do projeto é o SG3525, através de um
PWM (modulação por largura de pulso). O circuito montado é similar ao da figura 9, onde
em RX é feito o ajuste da razão cíclica e em R 1 a frequência.


Fonte: Práticas de laboratório de Eletrônica de Potência.
Teoricamente, a saída do SG3525 deveria ser ligada na chave (MOSFET). Porém,
ao realizar essa ligação direta poderia gerar riscos de queimar os componentes. No
projeto, foi montado um circuito de chaveamento do MOSFET.


#### 1.2.1. Circuito de chaveamento do mosfet

O circuito de chaveamento do MOSFET foi montado como na figura 10. A análise
do circuito apresentado na figura 10 é fundamentada em estados bem definidos de corte
e saturação do MOSFET, cujo sinal é gerado pelo drive de acionamento da figura 9.


Para um sinal de nível alto (5V), gerado por Vpulse, o transistor Q 2 entra em
saturação, conduzindo uma corrente no coletor de IC2. O divisor de tensão composto por
R 4 e R 5 garante que o transistor Q 3 entre em saturação e conduza uma corrente IE3, parte
dessa corrente é responsável pela condução do primeiro diodo (D 1 ). Com isso, Q 1 entra
em corte, fazendo com que um impulso elevado de corrente seja necessário e uma tensão
VGS surge entre gate (G) e source (S). Quando Vpulse gerar um sinal baixo (0V), o
transistor Q 2 entra em corte e não circulará a corrente IC2. Com isso, os terminais de base
e emissor do transistor Q 3 passam a ficar no mesmo potencial (15V), logo estará em
estado de corte. A carga armazenada no capacitor intrínseco do MOSFET, Cgs, contribui
para o aparecimento de uma tensão que polariza Q 1. O transistor Q 1 é levado a saturação
e drena rapidamente a carga armazenada da etapa anterior.

### 1.3. CARGA

Como carga foram usados 7 resistores de 39Ω e 10W em paralelo, resultando em
uma resistência equivalente de 18,18Ω e dissipando 70W de potência.


## 2. OBJETIVOS

Projetar um conversor boost com uma elevação de tensão de 15V na entrada para
35V na saída, com 70W de potência na saída. As ondulações máximas na corrente do
indutor, na tensão e na corrente de saída devem ser de 10%. Após isso, realizar a
comparação entre o que foi simulado e os resultados obtidos experimentalmente.


## 3. METODOLOGIA

Ao longo do projeto, sabia-se que muitas modificações seriam feitas e haveriam
muitas contas a se fazer e a se refazer. Devido a essa problemática, buscando otimizar o
tempo na determinação de parâmetros foi elaborada uma planilha, em que todas as
fórmulas foram inseridas de modo visual, assim como todas os cálculos. Cada variável
foi adotada um nome de forma que em caso de erro era possível visualizar a fórmula com
nomes e não mais apenas com um rótulo aleatório o que poderia ter gerado muitos erros.
No intuito de validar a planilha, todos os cálculos e resultados providos por ela
foram refeitos a mão, no entanto apenas uma vez, todas as outras vezes os cálculos foram
validados por esta prévia validação. No entanto com o uso a modificação de dados poderia
levar a modificação de fórmulas de maneira descontrolada e imprevisível sem a garantia
que alguém percebesse tal modificação. Com o objetivo de contornar esta problemática,
fora bloqueada todas as células da planilha que não fossem entrada de dados e apenas
permitidas as que correspondessem aos parâmetros de projeto, as variáveis de entrada se
encontram abaixo, juntamente com seus valores utilizados. Não fora adotada nenhuma
senha em caso de necessidade de mudança de algo, bastando apenas clicar no botão para
desbloquear, contudo o fato de obrigatoriamente ter de se clicar em um específico botão,
já garante um maior nível de confiabilidade nos cálculos. A planilha desenvolvida
encontra-se no repositório público [3].

No desenvolvimento das placas de circuito impresso, foi utilizado o software
Kicad, que é Open Source e agrega muito de outros softwares industriais como o Altium.
Com facilidade é possível gerar um projeto de eletrônica com este, uma vez que ele se
assemelha em muito a softwares de simulação como PSIM, Proteus, etc, no entanto ele
destina-se apenas ao design.
A maior facilidade que o Kicad oferece, é por conter uma vasta quantidade de
componentes de comuns no mercado, assim como o encapsulamento destes, muitos em
3 D. Outra grande vantagem na sua utilização, é na facilidade de se anexar novos
dispositivos encontrados por meio da Internet, por conta de uma vasta comunidade que

se dedica a compartilhar estes, assim como a concepção de novos componentes, inclusive
em 3D. A possibilidade de visualização em 3D possibilita que problemas de espaço
característicos desses tipos de projeto sejam resolvidos ainda durante a fase de projeto,
não onerando tempo na prototipagem [ANEXO 9.1]. Com isso o esquemático
desenvolvido em todos os circuitos está demonstrado no anexo [ANEXO 9. 2 ]. Também
fora disponibilizado uma visão da placa de circuito impresso com a legenda dos
componentes no intuito de facilitar a montagem [ANEXO 9.3]. Assim como foi
disponibilizado o arquivo, que se impresso e utilizada a técnica de produção de placas de
circuito impresso termotransferência, poderá ser reproduzido o protótipo aqui
desenvolvido [ANEXO 9.3].
Os arquivos aqui desenvolvidos, como esquemático e placa referentes ao software
Kicad, assim como as simulações desenvolvidas no software PSIM encontram-se no
repositório público [ 3 ].


## 4. PROCEDIMENTO

Para a implementação do conversor boost foram necessários cálculos para o
dimensionamento correto dos componentes. Para esses cálculos foram usados os
parâmetros da tabela 1.

### 4.1. CÁLCULOS DO CONVERSOR BOOST

#### 4.1.1. Resistência e tensão de saída

Para a escolha da tensão de saída, usamos como parâmetros os valores das
resistências de 10W que tínhamos disponíveis. Para obtenção do valor de potência
exigido (70W) utilizamos 7 resistores de 39Ω que dissipam 10W de potência, obtendo
uma carga equivalente de cerca de 18,18Ω. Com os resistores já definidos, partimos da
equação da potência para a definição da tensão de saída, que é demonstrada na equação
3.1.

Substituindo os valores fornecidos anteriormente, obtemos uma tensão de saída
de aproximadamente 35,67V


#### 4.1.2. Corrente média no indutor

Tomando como base a equação de ganho de um conversor boost e considerando
que a tensão da fonte adotada foi de 15V, podemos encontrar um valor para o duty cycle,
como mostrado na equação 3.2.

Adotando os valores mostrados acima obtemos um duty cycle de
aproximadamente 0,57952.
A corrente média no indutor pode ser calculada a partir da equação 3.3, já
demonstrada na introdução.

Obtendo assim uma corrente média no indutor de 4,6667A.

#### 4.1.3 Indutância mínima

Uma preocupação necessária no projeto do conversor é que o indutor opere de
modo contínuo, sendo assim, é necessário que asseguremos que o valor utilizado seja
superior ao valor obtido na expressão abaixo.


Assim, para garantir que o indutor opere de modo contínuo, garantindo que a
corrente que passe por ele seja sempre positiva, se faz necessário assegura-se que o valor
do indutor utilizado seja maior que o calor obtido a partir da equação 3.4.

#### 4.1.4 Cálculo do indutor

Primeiramente foi calculado a corrente de entrada de acordo com a
potência de saída e a tensão de entrada.


#### 4.1.4.1 Corrente no indutor

A partir da equação que segue, podemos obter a corrente de entrada, que é igual a
corrente no indutor.


#### 4.1.4.2 Corrente de saída

Utilizando a potência de saída e a tensão de saída, podemos obter a corrente de
saída a partir da equação abaixo:


Com os valore obtidos, finalmente podemos calcular o valor teórico do indutor,
de acordo com a tensão de saída, ondulação de corrente de entrada, o ciclo de trabalho e
a frequência a partir da equação que segue, levando em consideração que a ondulação de
corrente deve estar em função da tensão de entrada, do ciclo de trabalho, a indutância e a
frequência, ∆i:


O indutor implementado na prática foi feito de forma manual, obtendo um valor
de 1,5 mH, garantindo dessa forma a ondulação de corrente no mesmo em um valor de
10%.

#### 4.1.5 Cálculo do capacitor

Tendo como sendo 10% de ondulação de saída uma das limitações do projeto,
temos que tomar esse parâmetro para projetar o capacitor capaz de atender a essa
demanda. Para tal, foi utilizado a equação que segue:


Na prática utilizamos um capacitor 22uF, que foi o suficiente para que o
ripple da tensão sobre o capacitor não ultrapassasse os 10%.

### 4.2. DIMENSIONAMENTO DO INDUTOR

#### 4.2.1. Núcleos magnéticos

Para a construção o mais próximo do ideal do conversor, todos os elementos que
o constituem devem ser devidamente projetados, porém na construção de conversores
CC-CC, fatores como o surgimento de componentes parasitas devem ser levados em
consideração, como por exemplo: Capacitâncias parasitas, indutâncias de magnetização,
etc.
Na construção do núcleo magnético do indutor geralmente é usado um material
chamado ferrite, composto por óxido de ferro e possui poucas perdas quando é utilizado


em altas frequências, tendo como um dos problemas da sua utilização a sua fragilidade,
podendo ser comparada a fragilidade do vidro comum.


Duas informações importantes do núcleo são a Área de secção transversal (Ae) e
a Área da Janela (Aw). Dados esses dois valores, pode-se calcular os demais dados do
mesmo.
Figura 12: Núcleo de Ferrite tipo E-E, enfatizando suas áreas de janela e
transversal.

#### 4.2.2. Cálculos dos parâmetros.

O projeto do indutor se baseia nas Leis de Faraday e Àmpere, onde através de
algumas manipulações matemáticas se obterá:

#### 4.2.4. Entreferro

É necessário a utilização do entreferro no circuito magnético, sendo a indutância
proporcional ao número de espiras ao quadrado e inversamente proporcional a relutância.
Por mais alta que seja a permeabilidade magnética do material, ele possui uma
relutância. Nesse caso o valor da indutância independe da relutância do núcleo, assim:


O valor do entreferro será distribuído igualmente nas pernas
laterais do núcleo.

#### 4.2.5. Secção dos condutores

Considerando que o conversor opera em uma alta frequência, devido ao seu
chaveamento, assim, um efeito pelicular considerável, uma vez que a densidade de
corrente ficará na periferia, causando uma redução na área efetiva do condutor.
A equação a seguir define qual a bitola do condutor para conduzir a corrente do
enrolamento:

Assim sendo necessário calcular o número de condutores em paralelo para que
seja possível a condução da corrente necessária sem que exista um superaquecimento
dos mesmos.

Para a última etapa do projeto do indutor, temos que verificar se é possível
associar estes condutores na janela do núcleo. Assim, se Ex<1 é possível a utilização
deste núcleo, verificando essa máxima, utilizamos:



### 4.3. CIRCUITO SIMULADO

Após os cálculos dos parâmetros do conversor Boost, o mesmo foi simulado
utilizando o software PSIM para que posteriormente pudesse ser implementado no
circuito físico.

A tensão na fonte, onda em azul, é constante, visto que este é um conversor
CC-CC e foi implementada uma fonte de tensão contínua de 15V. Já a corrente
passa apenas pelo indutor com a chave fechada, carregando-o e, quando a chave
está aberta, ele é descarregado através do capacitor e carga, passando pelo diodo,
com corrente eficaz de 4,66A.

Na figura 13 observa-se as formas de onda de tensão (em azul) e de
corrente (vermelha) na carga a partir do momento que o conversor é ligado. A
ondulação de tensão de saída corresponde a 6 ,85% da tensão rms, que é de 35,68V
e a ondulação de corrente na carga também é de 6 ,85% da corrente rms, que é
1 , 96 퐴. Para melhor observar estas formas de onda na carga, elas são apresentadas
ampliadas na figura 14.

Com isso, é mostrada também a potência ativa de saída, igual a 69,94W,
praticamente igual à potência solicitada nas especificações, que é de 70W.


Para melhor visualização da forma de onda a mesma foi ampliada, obtendo
o mostrado na figura 16.

Com a chave fechada a corrente que sai da fonte passa totalmente pelo
indutor, que se carrega e se mantém assim até que a chave abra e ele comece a
descarregar pelo capacitor, por isso a onda é desta forma, com valor rms igual a
18,14V.

O mesmo ocorre para a forma de onda da corrente, foi mostrado desde o
momento em que o circuito começa seu funcionamento na figura 17, mas para
melhor analisá-la é necessário dar zoom.

O valor rms da corrente no indutor é de 4,66A e ela aumenta enquanto a
chave está fechada e começa a decair quando a chave se abre. A ondulação de
corrente nesse componente é de 5 ,94%, um valor dentro do aceitável.

O valor eficaz de tensão na chave obtido nesta simulação é de 25,30V e o
de corrente é de 3,30A. Como no software os componentes são tratados como
ideal, quando não há corrente na chave a tensão na mesma é máxima, visto que
ela está aberta, podendo ser considerada um circuito aberto. Já quando a tensão é
nula, a corrente é máxima, então a chave pode ser considerada um curto-circuito.
Figura 21: Formas de Onda de Tensão e Corrente no Diodo


O valor eficaz de tensão no diodo é de 24,28V  e de corrente é equivalente
a 3,40A. A partir das formas de onda acima é possível notar que quando há
corrente no diodo a tensão no mesmo é nula, pois, como é considerado ideal, se
comporta como um curto-circuito, do mesmo modo que ocorre com a chave
mostrada anteriormente. Já quando o diodo está em aberto a tensão é negativa pois
é a tensão reversa nele, que possui valor igual à tensão na carga (aproximadamente
36V), porém com sinal oposto.


## 5. EXPERIMENTO

### 5.1. CIRCUITO DE CHAVEAMENTO

O circuito de drive montado é o demonstrado na figura 22, um integrador que gera
uma onda PWM em dois canais. Foram feitos os ajustes necessários para suprir as
especificações do projeto, a uma frequência de 20kHz a fim de obter o chaveamento
necessário para o Mosfet(IRF640), a partir disso dimensionamos o valor do capacitor C 1
para 10nF, R 1 é um resistor variável (Trimpot 50K), onde podemos realizar o ajuste para
obter a frequência ideal. Para o resistor Ry foi usado um resistor de 10K. Em Rx também
foi usado um resistor variável (Trimpot 50K), para ser feito o ajuste do duty-cycle.

Um circuito totem pole foi usado para melhoria do funcionamento do driver. Esse
circuito é obtido através da associação de dois diodos para aumentar o duty-cycle a partir
das tuas portas do CI-3525, obtendo uma onda de até cerca de 90% de ciclo de trabalho.
Os diodos usados foram do tipo Shotcky, de modo que o tempo de recuperação fosse
baixo.

Usando o osciloscópio para medir a onda do chaveamento PWM, obtemos as
formas especificadas na figura 23. Vale destacar que o driver foi alimentado com uma
tensão de 15V e frequência de 20kHz.
Figura 23 : Forma de onda do PWM (laranja) x Tensão na saída (azul)


### 5.2. CIRCUITO DE POTÊNCIA

Após os cálculos e simulações feitas no PSIM, foi realizada a montagem da parte
prática, como mostrado na figura 24 e 25.

Após a montagem do circuito foram feitas as devidas medições. Os parâmetros
estabelecidos pela equipe eram de 15V na entrada e 35V na saída.

Fonte: Autores
Ao compararmos a onda obtida com a simulada, observamos que a onda medida
contém leves ruídos, porém estes não são de grande relevância na medição da tensão final,
gerando uma tensão de 14,8V, o que representa uma diferença de cerca de 1,33% do valor
previamente estabelecido. Com a placa alimentada nos 15V de entrada, a tensão na saída
foi medida. O valor médio encontrado foi de 35,9V, possuindo um erro de cerca de 1,02%
do valor estipulado, observados na figura 26. Comparando com a simulação, o resultado
foi bem satisfatório.

Com a alicate amperímetro do osciloscópio, foram medidos os valores de corrente
na carga, que estão comparados aos de tensão.


O valor de corrente médio obtido gira em torno de 2%. Sendo assim, notamos que
o conversor boost projetado está gerando resultados satisfatórios e coerentes com a
simulação.

### 5.3. CIRCUITO DE CARGA

Com o intuito de verificar de fato a potência calculada fora montada uma placa
exclusivamente para teste, que consistem em uma associação de resistores (3x 150Ω, 3x
120Ω e 1x 100Ω) todos em paralelo que combinadas dão aproximadamente a resistência
de carga 18.18Ω, na prática devido a tolerância dos resistores a resistência de carga
modificou-se um pouco ao que foi estimado, no entanto o circuito ainda comportou-se de
forma estável superando os cálculos de potência. Segue abaixo a figura 27 do resultado.

As chaves encontradas na placa possibilitam o teste com variação de carga, assim
como também um distúrbio, em caso de futura implementação de uma malha fechada por
meio de um controle. A placa de driver, já está pronta para essa expansão, contando com
bornes de saída para alimentação do controlador, assim como um borne de entrada com
o valor da saída do controlador. Nesse intuito poderiam ser utilizados controladores PID
e PI, pelo menos. Desse modo os efeitos provocados pela variação da carga, seriam
estabilizados por meio dos controladores, assim a tensão deveria ainda ficar estável, sem
necessidade de modificação do duty-cicle de modo manual, a modificação deste ficaria a
cargo do controlador.


## 6. CONCLUSÃO

Em resumo, o conversor Boost funciona sendo alimentado por uma tensão CC e a
eleva na saída de forma que essa tensão também seja constante. Como os dispositivos
utilizados são chave, diodo, indutor, capacitor e resistor e a maioria deles opera como
circuito aberto ou como curto circuito em diferentes momentos, há uma certa ondulação
de tensão e corrente na carga, porém dentro do aceitável de acordo com as especificações
de projeto.
A simulação do circuito foi de suma importância para analisar seu funcionamento
e comportamento quando alguns parâmetros eram modificados, assim alterações
poderiam ser feitas antes da execução do projeto na placa. Apesar de ser possível fazer
determinadas previsões, deve-se lembrar que a teoria e a prática diferem um pouco, visto
que em cálculos e em simulações são considerados componentes ideais, e não reais. Os
elementos reais dissipam calor, perdendo energia, entre outros fatores como a obtenção
manual do indutor calculado, que fazem com que a execução do projeto se torne mais
difícil.
É relevante citar foi necessário implementar dissipadores, pois componentes como
o MOSFET dissipam muito calor, dada a potência trabalhada, que é de 70W. Além disso,
para que o conversor funcionasse com um duty cycle maior que 0,5 foi preciso utilizar as
duas saídas do CI SG3525 num pequeno circuito eletrônico que somasse as duas, pois o
ciclo de trabalho do projeto em questão era de 0,58.
Pelo fato de não ser controlado, caso este conversor CC-CC do tipo Boost tenha
alguns de seus parâmetros alterados, os demais não serão ajustados, obtendo valores
diferentes dos esperados.
Com isso, na execução do projeto final da disciplina de Eletrônica de Potência,
observou-se a importância de um bom planejamento e estudo do funcionamento do
circuito a ser implementado. Em função disso, o conversor teve uma boa resposta e, como
esperado, elevou a tensão de 15V de entrada para uma tensão de 35V de saída, ambas
contínuas, com a carga estabelecida, obedecendo os parâmetros de projeto, possibilitando
um maior conhecimento prático desse conteúdo, além das práticas em laboratório.


## 7. REFERÊNCIAS BIBLIOGRÁFICAS

```
[1] Hart, D. W. (2012). Eletrônica de Potência. (R. Abdo, Trad.) Porto Alegre,
Rio Grande do Sul, Brasil: AMGH Editora Ltda.
[2] BARBI, Ivo. (2011). Projetos de fontes chaveadas. Florianópolis: Edição do
Autor.
```
