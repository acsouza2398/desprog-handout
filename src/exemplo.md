Problema da Mochila 1/0
======

O que é? 
---------

Nessa aula, será abordado dentro do tema de Divisão, Conquista e Programação Dinâmica, o uso do algoritmo dinâmico para resolver o problema da mochila. O problema da mochila, de forma sucinta, é um problema de otimização de espaço para o maior retorno possível.

Pareceu complicado? Vamos simplificar então.

Imagine uma mochila, que aguenta até um certo peso antes que rasgue, e vários objetos que queremos guardar nessa mochila, cada um tendo peso e valor próprio. Por causa do limite de peso, pode ser que tenhamos que deixar alguns objetos para trás. 

Mas como escolher quais objetos botar na mochila, e quais não? Como temos peso e valor do objeto, e o peso é usado para ver se a mochila aguenta os objetos, então o que determina se devemos guardá-los ou não é o seu valor! Quanto maior o valor, maior prioridade um objeto tem para ser guardado. 

Entendeu a lógica? Vamos praticar com um exercício então!

??? Questão 1

Considere uma mochila com limite de peso de 3kg com os seguintes itens:
* Item 1: 1 kg com valor de R$ 15,00
* Item 2: 2 kg com valor de R$ 20,00
* Item 3: 3 kg com valor de R$ 30,00

![](Q1_novo.png)

Intuitivamente, quais itens devem entrar na mochila para maximizar o seu valor?

!!! Aviso
Importante ressaltar que cada item só pode ser colocado UMA vez na mochila ou seja, caso a mochila tenha 2kg, o item 1 so pode ser contabilizado uma vez, totalizando um valor de R$ 15,00. Além disso, não pode adicionar um item de forma parcial ou um item que ultrapasse o limite de peso total.
!!!

::: Gabarito
Os itens 1 e 2, chegando a um peso máximo de 3kg com valor R$ 35,00

![](G1_novo.png)
:::

???

O problema parece simples para poucos itens com um limite de peso baixo. A partir do momento em que a lista de itens aumenta, e o limite de peso é elevado, fica mais difícil enxergar a solução otimizada. Com isso, fica necessário implementar a ajuda de um algoritmo para fazer essa otimização.

Opções de Algoritmo
---------

O problema da mochila é um problema de otimização, com aplicação real para empresas, e logo precisa de uma visão realista na hora de escolher qual algoritmo se deve usar para resolvê-lo. Embora haja algoritmos com melhor desempenho no que se refere à velocidade com que o programa roda, o algoritmo dinâmico é o mais confiável, pois ele sempre retorna a melhor resposta.
E como a confiabilidade dos resultados obtidos são muito valorizados por gestores, esse algoritmo é o melhor, principalmente em casos pequenos.

Agora que sabemos o POR QUÊ de usarmos esse algoritmo, está na hora de começarmos a entender COMO usamos esse algoritmo. Para isso, vamos montar a função. 

De forma mais técnica, o algoritmo de programação dinâmica para o problema da mochila recebe **três entradas** e devolve **uma saída**. 

A primeira entrada é uma lista de valores correspondente a cada objeto individualmente, e a segunda entrada uma lista de peso para cada um desses objetos. A posição que cada valor e peso ocupa nas listas e a mesma para um objeto, então nao precisamos nos preocupar com reorganização nesse sentido. 

A terceira entrada corresponde a quantidade de peso que a mochila pode carregar, sempre em forma de um inteiro. 

Por fim a saída corresponde ao valor final que a mochila vai ter no fim de todas as iterações, sendo que esse valor, para resolver o problema, tem que ser o maior possível.

Agora, vamos ver se você prestou atenção.

??? Questão 2

Quais devem ser os parâmetros que a função deverá receber?
Defina a chamada da função Mochila.

::: Gabarito

``` c
int Mochila(int L, int p[], int val[], int n){}
```
Onde:
* L é o limite de peso da mochila;
* p[ ] é a lista de pesos dos itens;
* val[ ] é a lista de valores dos itens;
* n é a quantidade de itens;

!!! Aviso
Para fins de simplificação, considera-se que a posição dos itens na lista de pesos e na lista de valores estão alinhados e se correspondem.
!!!
:::

???

Com a chamada da função pronta, os próximos passos são: definir a condição inicial, e então usar recursão para checar qual é o caso de maior valor: **com** ou **sem** o objeto em questão.

Bom...Não nos apressemos. Primeiro, vamos ver se você entendeu a recursão do nosso algoritmo.

??? Questão 3

Vamos pensar no caso base da recursão. O que acontece quando o limite da mochila é 0 ou se não há itens para colocar?

::: Gabarito
Como não tem espaço na mochila, o valor final fica 0. O mesmo é verdadeiro se não há itens para colocar na mochila mesmo com espaço.
:::

???

??? Questão 4

Com a intuição acima, desenvolva o caso base da recursão para resolver o problema da mochila.

!!! Dica
Desenvolva a base lembrando que o problema acaba quando não há mais itens para colocar dentro da mochila
!!!

::: Gabarito
``` c
int Mochila(int L, int p[], int val[], int n)
{
    // Condição Inicial
    if (n == 0 || L == 0)
        return 0;

}
```
:::

???

Com o caso base feito, vamos pensar um pouco em como itens entram ou saem da mochila. Para isso, vamos retomar o exemplo inicial da aula:
* Item 1: 1 kg com valor de R$ 15,00
* Item 2: 2 kg com valor de R$ 20,00
* Item 3: 3 kg com valor de R$ 30,00

??? Questão 5

Na situação em que o limite de peso é 3kg, escreva um pseudocódigo que mostre como o algoritmo deveria escolher o que entra na mochila.

!!! Aviso
Não coloque a resposta final, mas sim como o algoritmo iria selecionar e comparar os itens.
!!!

::: Gabarito
``` c
se(item 3 > item 1 + item 2){
    colocar item 3 na mochila
} caso contrario{
    colocar item 1 + 2 na mochila
}
```
É interessante notar que uma vez que escolhemos o item 1 para entrar na mochila, o limite da mochila diminui pelo peso do item 1 (3 - 1 = 2). Com isso, temos uma "nova" mochila para otimizar, mas dessa vez é uma mochila com limite de 2kg. Como nesse caso o único item que pode entrar na mochila é o item 2, pois o item 3 ultrapassa o limite da mochila, o valor final da nossa mochila original fica a soma do item 1 com o 2 que é R$ 35,00. Essa comparação com um valor de mochila menor é o porquê do uso da recursão.
:::

???

??? Questão 6

Levando em conta a intuição acima e o exemplo original, complete a função com a chamada recursiva. <br> <br>
Considere que há uma função auxiliar chamada maior_valor() que retorna o maior valor entre duas entradas.

::: Gabarito
``` c
int Mochila(int L, int p[], int val[], int n)
{
    // Condição Inicial
    if (n == 0 || L == 0)
        return 0;

    // Devolve o maior valor dentre dois casos:
    // (1) incluindo o n-ésimo item na mochila
    // (2) não incluindo o n-ésimo item na mochila
    return maior_valor(
        val[n - 1] + Mochila(L - p[n - 1], p, val, n - 1),
                                Mochila(L, p, val, n - 1));
}
```
:::

???

Notou algo de errado com essa função?

Ela não leva em conta um dos fatores que foi mencionado no começo da aula: o que acontece se o limite de peso for ultrapassado por um objeto.

??? Questão 7

Refaça a Questão 4, levando em conta o caso em que um objeto ultrapassa o limite de peso.

::: Gabarito
``` c
int Mochila(int L, int p[], int val[], int n)
{
    // Condição Inicial
    if (n == 0 || L == 0)
        return 0;

    // Se o peso do n-ésimo item for maior do que
    // a capacdade L da mochila, então esse item
    // não pode ser incluído na solução otimizada
    if (p[n - 1] > L)
        return Mochila(L, p, val, n - 1);
 
    // Devolve o maior valor dentre dois casos:
    // (1) incluindo o n-ésimo item na mochila
    // (2) não incluindo o n-ésimo item na mochila
    return maior_valor(
        val[n - 1] + Mochila(L - p[n - 1], p, val, n - 1),
                                Mochila(L, p, val, n - 1));
}
```
:::

???

??? Questão 8

Desenvolva a árvore de complexidade para o código de exemplo, especificando o quanto n variou apenas nos níveis da três primeiras recursões, e a partir daí, determine a complexidade da função recursiva.

::: Gabarito

``` c
         /
        | 1                    se n == 0 ou L == 0;
f(n) = <
        | 2Mochila(n-1) + 1    se n > 0 e L > 0.
         \
```

![](arvore.png)

A complexidade temporal do nosso algoritmo de recursão é O(2^n), devido ao fato de ser um algoritmo bem simples onde muitas repetições de operações desnecessárias são realizadas. Com esse desempenho bem ruim no que se refere à velocidade de execuçao do processo, se uma empresa tiver como prioridade maior a velocidade, ele não seria escolhido caso hovesse outras opções com. 

Apesar disso, como não há uso de estruturas temporárias, como listas por exemplo, que armazenam informação durante o processo, não há necessidade de memória extra, sendo a complexidade do uso de memória adicional da recursão simples realizada O(1).
:::

???

Melhorou, mas há jeitos menos custosos pra resolver esse problema. Como você calculou na questão anterior, a complexidade do algoritmo de recursão simples é alta e, apesar de não gastar muita memória, tem um tempo de execução muito alto devido a repetição desnecessária.

Para resolver isso, é interessante olhar para um outro tipo de algoritmo de mochila: a programação dinâmica. 

Com o uso de programação dinâmica para resolver o problema, a repetição excessiva da recurção pode ser evitada criando um array temporário **temp**.

Lembrando como funciona a programação dinâmica, o algoritmo consulta o array temporário para tomar as decisões de incluir um item ou não e preenche o array até chegar na resposta final do problema. Como o array segura todos os resultados das iterações passadas, não há mais necessidade da recursão, apenas a consulta e comparação com o array.

??? Questão 9

Com essas informações, desenvolva o algoritmo de Programação Dinâmica usado na resolução do problema da mochila. 

::: Gabarito
``` c
int Mochila(int L, int p[], int val[], int n)
{
    int i, w;
    int K[n + 1][L + 1];
 
    // Construindo array K[][] de baixo para cima
    for (i = 0; i <= n; i++)
    {
        for (w = 0; w <= L; w++)
        {
            if (i == 0 || w == 0)
                K[i][w] = 0;
            else if (p[i - 1] <= w)
                K[i][w] = max(val[i - 1]
                          + K[i - 1][w - p[i - 1]], K[i - 1][w]);
            else
                K[i][w] = K[i - 1][w];
        }
    }
 
    return K[n][L];
}
```
:::

???

??? Questão 10

Agora que temos o nosso algoritmo, desenvolva a árvore de complexidade para a nova versão do código, e use a mesma para determinar a sua complexidade.

::: Gabarito

``` c
         /
        | 1                   se i == 0 ou w == 0;
f(n) = <
        | Mochila(n-1) + 1    se i > 0  e w > 0.
         \
```

![](arvore2.png)

A complexidade temporal e de uso de memória auxiliar do nosso algoritmo é O(n) em ambos os casos, o que significa que se uma empresa tiver como prioridade maior a velocidade ou o quanto de memória é gasta, ele poderia acabar não sendo escolhido. 

Mas por ser um algoritmo estável, se uma empresa quiser dados confiáveis acima de tempo ou uso de memória, o que geralmente é o que ocorre em casos envolvendo objetos de valor muito alto, esse é o melhor algoritmo para esse serviço.
:::

???

Agora que temos o algoritmo pronto, vamos entender o que está acontecendo.

Como o algoritmo é recursivo, isso implica calcular subproblemas derivados do problema principal e reutilizar esses resultados no futuro para fins de comparação. Isso funciona através do preenchimento de uma matriz limite x itens:

|                             | 0 kg     | 1 kg     | 2 kg     | 3 kg     |     
|-----------------------------|----------|----------|----------|----------|
| **Item 1 (1 kg, R$ 15,00)** |          |          |          |          |  
| **Item 2 (2 kg, R$ 20,00)** |          |          |          |          |       
| **Item 3 (3 kg, R$ 30,00)** |          |          |          |          |          

As células dessa matriz são preenchidas linhas por coluna com o valor máximo da mochila dado seu limite de peso e itens considerados.

??? Questão 11

Preencha a primeira linha da tabela. Ou seja, considerando apenas o item 1, qual é o valor da mochila para cada limite de peso?

::: Gabarito
Para a primeira coluna, como o limite de peso é de 0 kg, o item 1 não pode ser incluido pois nao cabe, portanto o valor máximo da mochila é R$ 0,00.

A partir da segunda coluna, onde o limite de peso é 1 kg, é possível incluir o item 1. Com isso, o valor das colunas restantes é de R$ 15,00.

|                             | 0 kg     | 1 kg     | 2 kg     | 3 kg     | 
|-----------------------------|----------|----------|----------|----------|
| **Item 1 (1 kg, R$ 15,00)** | R$ 0,00  | R$ 15,00<br> <span style="color:red">(**item 1**) </span> | R$ 15,00 <br> <span style="color:red">(**item 1**) </span>| R$ 15,00 <br> <span style="color:red">(**item 1**) </span>| 
| **Item 2 (2 kg, R$ 20,00)** |          |          |          |          |         
| **Item 3 (3 kg, R$ 30,00)** |          |          |          |          |          
:::

???

O preenchimento da próxima linha é onde a recursão começa a importar. Até a segunda coluna, o preenchimento é igual a linha de cima, visto que não é possível incluir o item 2 quando o limite de peso é inferior ao seu peso. Na terceira coluna, há uma decisão a ser tomada: incluir o item 1 ou 2.<br><br>
Volte no algorítmo de recursão para responder essa próxima questão. Não use sua intuição para decidir qual será o proximo valor pois você não conseguirá fazer a mesma coisa com listas maiores e problemas mais complexos.

??? Questão 12

Preencha a segunda linha da tabela até a terceira coluna. Qual deve ser o item a ser incluido na terceira coluna? Por quê?

::: Gabarito

O item a ser incluido é o Item 2.<br>
<br>
Para tomar essa decisão, entre qual item adicionar, você teve que considerar duas possibilidades para fazer com os itens a serem adicionados e o peso da mochila; ou pegar o item 2, ou não pegar. Se escolhesse em não pegar, você deve obter o melhor valor que você conseguiria pegando o primeiro item, que nesse caso seria 15 reais. <br><br> Agora, se a escolha fosse pegar o item dois, o valor final seria o valor do item 2 MAIS o valor que você conseguiria com o primeiro item na coluna de 0kg. *2kg da mochila - 2kg do item dois*

|                             | 0 kg     | 1 kg     | 2 kg     | 3 kg     | 
|-----------------------------|----------|----------|----------|----------|
| **Item 1 (1 kg, R$ 15,00)** | R$ 0,00  | R$ 15,00<br> <span style="color:red">(**item 1**) </span> | R$ 15,00 <br> <span style="color:red">(**item 1**) </span>| R$ 15,00<br> <span style="color:red">(**item 1**) </span>  | 
| **Item 2 (2 kg, R$ 20,00)** | R$ 0,00  | R$ 15,00 <br> <span style="color:red">(**item 1**) </span>| R$ 20,00<br> <span style="color:red">(**item 2**) </span>  |          |                                             
| **Item 3 (3 kg, R$ 30,00)** |          |          |          |          |          

:::

???

Nas últimas duas colunas, o valor máximo é a somatória dos valores dos itens 1 e 2, visto que há espaço suficiente para incluir ambos os itens na mochila. <br>

Para a terceira linha da tabela, assim como para o item 2, as primeiras 3 colunas são identicas a linha de cima, pois não é possível incluir o item 3 ainda.

??? Questão 13

Preencha a terceira linha da tabela até a quarta coluna. Qual deve ser o(s) item(ns) a ser(em) incluido(s) na quarta coluna? Por quê?

::: Gabarito

Os itens a serem incluidos são os Items 1 e 2, pois o valor da soma dos itens 1 e 2 é maior do que do item 3. <br>
<br>
Para tomar essa decisão, você acabou levando em consideração qual era o maior valor entre os itens previamente incluidos, os itens 1 e 2, e o item a ser incluido, o item 3, para esse limite de peso. <br> <br>
É importante entender que para esse caso, ao considerar a inclusão do item 2, sobrou espaço para incluir o item 1, o que possibilitou a sua inclusão. Ao selecionar o item 2, o problema se transforma em um subproblema da mochila onde o limite de peso é 3 kg (coluna atual) - 2 kg (incluir Item 2) = 1 kg. Ja foi calculado esse resultado previamente e foi determinado que apenas o item 1 podia ser incluido com um valor de R$ 15,00. Com isso, é possível tirar o máximo entre os dois valores: R$ 35,00 > R$ 30,00. Portanto, os itens 1 e 2 seguem na mochila e o item 3 não.

|                             | 0 kg     | 1 kg     | 2 kg     | 3 kg     | 
|-----------------------------|----------|----------|----------|----------|
| **Item 1 (1 kg, R$ 15,00)** | R$ 0,00  | R$ 15,00<br> <span style="color:red">(**item 1**) </span>  | R$ 15,00<br> <span style="color:red">(**item 1**) </span>  | R$ 15,00<br> <span style="color:red">(**item 1**) </span>  | 
| **Item 2 (2 kg, R$ 20,00)** | R$ 0,00  | R$ 15,00<br> <span style="color:red">(**item 1**) </span>  | R$ 20,00 <br> <span style="color:red">(**item 2**) </span> | R$ 35,00 <br> <span style="color:red">(**item 1 + item 2**) </span>. |
| **Item 3 (3 kg, R$ 30,00)** | R$ 0,00  | R$ 15,00<br> <span style="color:red">(**item 1**) </span>  | R$ 20,00 <br> <span style="color:red">(**item 2**) </span> | R$ 35,00 <br> <span style="color:red">(**item 1 + item 2**) </span>. |          

!!! Aviso
Não passe para frente antes de entender como funciona a recursão na tabela.
!!!

:::

???

<!-- Agora que você já entendeu a como funciona, está na hora de completar a tabela!

??? Questão 6

Preencha a última célula restante. Qual deve ser o(s) item(ns) a ser(em) incluido(s) e qual é o valor final da mochila? Por quê?

::: Gabarito

Os itens a serem incluidos são os Items 1 e 3, pois o valor da soma dos itens 1 e 3 é maior do que a soma dos itens 1 e 2. <br>
O valor final da mochila é R$ 45,00 com peso de 4 kg.

|                             | 0 kg     | 1 kg     | 2 kg     | 3 kg     | 4 kg     |
|-----------------------------|----------|----------|----------|----------|----------|
| **Item 1 (1 kg, R$ 15,00)** | R$ 0,00  | R$ 15,00 | R$ 15,00 | R$ 15,00 | R$ 15,00 |
| **Item 2 (2 kg, R$ 20,00)** | R$ 0,00  | R$ 15,00 | R$ 20,00 | R$ 35,00 | R$ 35,00 |
| **Item 3 (3 kg, R$ 30,00)** | R$ 0,00  | R$ 15,00 | R$ 20,00 | R$ 35,00 | R$ 45,00 |

:::

??? -->

Agora que você já entendeu a como o problema funciona, resolva o problema a seguir:

??? Questão 14

Considere uma mochila com limite de peso de 7 kg com os seguintes itens:
* Item 1: 1 kg com valor de R$ 9,00
* Item 2: 2 kg com valor de R$ 12,00
* Item 3: 3 kg com valor de R$ 15,00
* Item 4: 5 kg com valor de R$ 20,00

![](Q2.png)


::: Gabarito
Os itens 1, 2 e 3, chegando a um peso de 6kg com valor R$ 36,00

![](G2.png)
:::

???
