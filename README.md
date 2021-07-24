# Estudos Teóricos - Javascript :books:
O objetivo desse repositório é organizar algumas teorias importantes do javascript, para melhorar a qualidade dos meus estudos e fixar melhor o conteúdo. Fique a vontade para utilizar também!

<em>Inspiration: [@isadorastan - estudos repository](https://github.com/isadorastan/estudos)</em>

## Sumário
1. [Hoisting](#hoisting)
2. [Escopo](#escopo)
3. [Variáveis](#variaveis)
4. [Arrow Functions](#arrowfunc)
5. [Manipulação de Strings](#manipulacao_string)
6. [Manipulação de Arrays](#manipulacao_array)

[Clique aqui para ir à pasta de estudos práticos](praticas/README.md)

<h2 id="hoisting">Hoisting :fishing_pole_and_fish:</h2>

### O que é o hoisting?
É o conceito de que as declarações de variável e função são colocadas na memória durante a fase de compilação, mas permanecem exatamente onde você as digitou. Isso, permite que você use uma função ou variável antes mesmo de declará-la.

<em>fonte: [MDN Glossary - Hoisting](https://developer.mozilla.org/pt-BR/docs/Glossary/Hoisting)</em>

```js
    myName("Gabriela");
    function myName(name) {
        console.log("O meu nome é " + name);
        // OUTPUT: O meu nome é Gabriela
    }

```

A função foi chamada antes mesmo de ser declarada, mas funciona.


O mesmo acontece para variáveis, mas nesse caso, o javascript eleva as declarações, não as inicializações.

```js
    console.log(num); // OUTPUT: undefined --> só foi declarada
    var num;
    num = 6;
    console.log(num) // OUTPUT: 6 -> agora inicializada

```

```js
    num = 6; // inicialização
    console.log(num); // OUTPUT: 6;
    var num; // declaração


```

<h2 id="escopo">Escopo :mailbox:</h2>

### O que é um escopo?
Escopo é a acessibilidade de objetos, variáveis e funções em diferentes partes do código.
Em outras palavras, o que determina quais são os dados que podem ser acessados em uma determinada parte do código é o escopo.
Imagine que o escopo é uma caixa e tudo que for criado nessa caixa pode ser acessado por qualquer objeto dentro da mesma. Um escopo é criado sempre que definimos uma função:

```js
    function hello(name) {
        // Isto aqui é um escopo
    }

```


<em>fonte: https://imasters.com.br/desenvolvimento/escopos-em-javascript</em>

* Escopo Global
    * Uma variável global é definida quando declaramos uma variável fora de qualquer função, assim ela torna <strong>acessível a qualquer parte da nossa aplicação ou site, podendo ser lida e alterada.</strong>
* Escopo Local
    * Uma variável se torna local quando ela é declarada dentro de uma função, de tal maneira a qual ela somente estará <strong> acessível dentro dessa função.</strong>

    ```js
        function foo() {
            var name = 'Gabriela'
            let color = 'Blue'
            const age = 22
        }

        foo();

        //tentando acessar fora do escopo da função
        console.log(name); // name is not defined
        console.log(color); // color is not defined
        console.log(age); // age is not defined

        //    Conclusão: name, color e age não existem fora do escopo da função foo. 
        //Isso significa, que podemos ter múltiplas funções com variáveis e constantes com o mesmo nome, mas que retornarão valores diferentes.

        function color() {
            const color = 'pink'
            console.log(color) // pink
        }

        function color2() {
            const color = 'yellow'
            console.log(color) //yellow
        }

        color();
        color2();
    ```




* Escopo de Bloco
    * Não existia no JS escopo de bloco. Ou seja, for whiles e ifs não tinham escopo próprio. Porém com o ECMAScript 6 foi possível criar escopos de bloco usando as variáveis let e const, <strong>que são acessíveis somente dentro do bloco.</strong>

    > Escopos criados por funções são chamados de function scopes, enquanto escopos criados por estruturas de controle são chamados de block scopes.

* Escopos Aninhados
    * Todo escopo é fechado para acessos externos, de forma que escopos superiores não conseguem acessar escopos internos, mas o contrário é permitido.

    ```js
    function foo() {
        function bar() {

        }
    }
    
    ```

    Quando criamos outra função dentro da função foo, estamos colocando outra caixa dentro do escopo da função.

<h2 id="variaveis">Variáveis :package:</h2>

* var
    * É içada (veja em [Hoisting](#hoisting))
    * Tem escopo abrangente -> se for declarada dentro de um bloco -> vaza do escopo
    * Escopo global e função -> não tem escopo de bloco
    * Praticamente não são mais usadas em aplicações devidos aos problemas de escopo -> <strong>substituídas por let e const</strong>


```js
    if(true) {
        var global = 2; // vaza de dentro do bloco
    }

    function teste() {
        var global = 4;
        console.log(global); //4
    }

    console.log(global); //2 -> acessa a que vazou do if

```

* let e const
    * Tem escopo de bloco e de função
    * Sofrem hoisting (são elevadas) para o topo do bloco que foram definidas → porém não é atribuido o valor de undefined como acontece com var → continuam não inicializadas e dão erro caso sejam chamadas antes de suas declarações.
    * A grande diferença entre as duas é que <strong>consts não podem ser reatribuídas</strong> enquanto lets sim.

    ```js
        function name() {
	        console.log(name); // ❌ retorna erro porque ainda não foi inicializada
	        let name = 'gabriela';
	        console.log(name); // 👍🏼 gabriela
	        name = 'gabriela 2'; // 👍🏼 pode ser reatruída
        }

        const num = 6;
        num = 8; // ❌ Não pode ser reatribuída porque é const
    ```

<h2 id="arrowfunc">Arrow Functions :arrow_right:</h2>

### O que são arrow functions?
<em>fonte: [Marco Bruno - YT](https://www.youtube.com/watch?v=3EkS9-P3cIM)</em>

Uma nova forma de escrita de uma função, sempre é uma função anônima

```js
const sum = (number1, number2) => {
    return number1 + number2;
}

console.log(sum(10,2)) // OUTPUT: 12

```

### Easter Eggs da Arrow Function
* retornando sem return
    * Se você usa uma arrow function sem as chaves, consegue retornar sem usar a <em>keyword</em> return

    ```js
    const sum = (number1,number2) => number1 + number2;

    console.log(sum(10, 2)) // OUTPUT: 12

    ```

* sem parâmetros

    ```js
    const myName = () => 'Gabriela';

    console.log(myName()); // OUTPUT: Gabriela

    ```

* só um parâmetro
    * Quando você tem 1 único parâmetro os <strong>parênteses se tornam opcionais</strong>

    ```js 
        //com parênteses
        const double = (number) => number * 2;
        console.log(double(20)) // OUTPUT: 40

        //sem parênteses
        const double = number => number * 2;
        console.log(double(20)) // OUTPUT: 40

    ```
* retornando um JSON sem return
    * Como um JSON é definido por chaves, elas são confundidas com as chaves da arrow function. Assim, é impossível retornar sem return, já que para não utilizá-lo é necessário retirar as chaves. A opção que temos é trocar as chaves da Arrow Function por parênteses. Exemplo:

    ```js
        const getPerson() = () => ({name: 'Gabriela', age: 22});

        console.log(getPerson());

    ```


<h2 id="manipulacao_string">Manipulação de Strings :exclamation:</h2>

* Propriedade
    * length -> retorna tamanho da string
* Métodos 
    * toLowerCase -> coloca todas as letras da string em minúsculas
    ```js
    let name = 'GABRIELA';
    console.log(name.toLowerCase()) // OUTPUT: gabriela
    ```

    * toUpperCase -> coloca todas as letras da string em maiúsculas

    ```js 
    let name = 'Gabriela';
    console.log(name.toUpperCase()) // OUTPUT: GABRIELA

    ```

    * trim -> remove os espaços em branco do início ou do final da string, se existir

    ```js
    let name = '   Gabriela    '
    console.log(name.length) // OUTPUT: 15 - length conta os espaços
    name = name.trim(); //reatribuição retirando os espaços
    console.log(name.length) // OUTPUT: 8

    ```

    * padStart/padEnd -> para preencher uma string com um determinado caractere. 
        * O primeiro parâmetro é o comprimento que a string deverá ter depois de preenchida e o segundo é com qual caractere a string será preenchida

    ```js
    let number = "5025";
    let newNumber = number.padStart(9, "*");
    console.log(newNumber); // OUTPUT: *****5025
    ```

    * replace -> quando é necessário substituir uma substring dentro de um texto por outra. O método replace procura a primeira vez em que o termo do primeiro parâmetro aparece no texto e substitui pelo termo do segundo parâmetro

    ```js
    let texto = "A linguagem PHP é muito poderosa";
    let resultado = texto.replace('PHP', 'Javascript')
    ```

    * substr -> método nativo que extrai uma substring dentro de uma string. 
        * Parâmetros: posição de inicio da substring a ser extraída, e quantidade de caracteres da substring
    ```js
    let frase = 'Meu nome é Gabriela';
    frase.substr(11, 8); // OUTPUT: Gabriela
    ```

    * substring -> método nativo que extrai uma substring dentro de uma string. 
        * Parâmetros: posição inicial da substring a ser extraída, posição final da substring a ser extraída.

    ```js
    let frase = 'Meu nome é Gabriela';
    frase.substring(11, 19); // OUTPUT: Gabriela
    ```
    * indexOf -> pesquisar por uma substring dentro de uma string. 
        * Retorna posição inicial da substring dentro da string. E, se não achar, retornará -1

    ```js
    let frase = 'Meu nome é Gabriela';
    frase.indexOf('Gabriela') // OUTPUT: 11
    frase.indexOf('Javascript') // OUTPUT: -1 (Não encontrado)
    ```

    * split -> método que vai quebrar a string em diversas partes
        * Parâmetro: caractere (toda vez que o método encontrar esse caractere na string, ela irá ser quebrada)
        * saída sempre será um array

    ```js
    let name = 'Gabriela Menezes'
    let array = name.split(" ") // OUTPUT: ["Gabriela", "Menezes"]
    console.log(array[0]) // OUTPUT: Gabriela
    ``` 
<h2 id="manipulacao_array">Manipulação de Array :exclamation:</h2>

* slice && splice 
    - slice (fatia) - O método slice() retorna uma cópia de parte de um array a partir de um subarray criado entre as posições início e fim (fim não é necessário) de um array original
        * O array original **NÃO É ALTERADO**
        ```js
            //Extrair frutas
            let lista = ['Banana', 'Maçã', 'Pêra', 'Mamão', 'Melancia', 'Arroz', 'Feijão', 'Macarrão', 'Ovos']

            let frutas = lista.slice(0, 5)
            console.log(frutas) // OUTPUT: ['Banana', 'Maçã', 'Pêra', 'Mamão', Melancia];

            console.log(lista) // OUTPUT: ['Banana', 'Maçã', 'Pêra', 'Mamão', 'Melancia', 'Arroz', 'Feijão', 'Macarrão', 'Ovos'] 
        ```
    - splice: O método splice() **altera o conteúdo** de uma lista, adicionando novos elementos enquanto remove elementos antigos
        * Parâmetros: índice, deleteCount, elemento1, ...., elementoN
            - **índice:** indica o indice o qual deve iniciar a alterar a lista
            - **deleteCount:** indica o número de elementos a serem removidos a partir do indice inicial (primeiro parâmetro)
            - **elemento1,...elementoN:** Os elementos que serão adicionados na lista

            ```js
                const items = ["Arroz", "Feijão", "Macarrão"]
                // a partir do 1 estou adicionando carne e tomate. E não remove nada
                items.splice(1, 0, "Carne", "Tomate")

                console.log(items) // OUTPUT: ["Arroz", "Carne", "Tomate", "Feijão", "Macarrão"]

                //deletando 2 itens a partir do item 1
                items.splice(1, 2)
                console.log(items) //  OUTPUT: ["Arroz", "Feijão", "Macarrão"]

                // Adicionando os itens no index 1 em diante 
                items.splice(0, 1, "Molho de Tomate", "Orégano", "Queijo Ralado")

                console.log(items) //OUTPUT: ["Molho de Tomate", "Orégano", "Queijo Ralado", "Feijão", "Macarrão"]
            ```
* forEach
    - Responsável por percorrer **todos** os itens de um array e executar uma determinada função
        * ForEach recebe uma _Função Callback_(Veja em [Glossário](#glossary)) como parâmetro
            * A função de callback, por sua vez, também pode receber parâmetros - são 3: valorAtual, índice e array

        ```js
            let person = [
                {nome: Gabriela},
                {nome: Menezes},
                {nome: Andrade},
                {nome: Mendes}
            ];

            // O valorAtual na primeira iteração é referente ao valor da primeira posição do nosso array
            // O valorAtual na segunda iteração é referente ao valor da segunda posição do nosso array 
            // O valorAtual na terceira iteração é referente ao valor da terceira posição do nosso array

            // O índice é referente ao índice de posição do array

            //meuArray não muda a cada iteração, ele só é uma referencia àquele que chamou função ForEach
            person.ForEach((valorAtual, indice, meuArray) => {
                console.log(valorAtual)
                // 1 iteração: {nome: Gabriela}
                // 2 iteração: {nome: Menezes}
                // 3 iteração: {nome: Andrade}
                // 4 iteração: {nome: Mendes}

                console.log(indice)
                // 1 iteração - 0
                // 2 iteração - 1
                // 3 iteração - 2
                // 4 iteração - 4
            })
        ```
* Map
    - Também é responsável por percorrer todos os itens de um array, mas retorna um array do mesmo tamanho do original com alguma modificação feita
        * Map recebe uma _Função Callback_(Veja em [Glossário](#glossary)) como parâmetro
            * A função de callback, por sua vez, também pode receber parâmetros - são 3: valorAtual, índice e array

            ```js
                let numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
                //tabuada de 2
                numbers.map(number => number * 2) // OUTPUT: [2, 4, 6, 8, 10, 12, 14, 16, 18, 20]

                let names = ["Gabriela", "Pedro", "Maria Eduarda", "Ana Beatriz"]
                names.map(name => `${name} Menezes`) // OUTPUT: ["Gabriela Menezes", "Pedro Menezes", "Maria Eduarda Menezes", "Ana Beatriz Menezes"]
            ```







<h2 id="glossary">Glossário :notebook:</h2>

* Função CallBack - Uma função callback é uma função passada a outra função como argumento 
