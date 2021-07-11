# Estudos Teóricos - Javascript :books:
O objetivo desse repositório é organizar algumas teorias importantes do javascript, para melhorar a qualidade dos meus estudos e fixar melhor o conteúdo. Fique a vontade para utilizar também!

<em>Inspiration: [@isadorastan - estudos repository](https://github.com/isadorastan/estudos)</em>

## Sumário
1. [Hoisting](#hoisting)
2. [Escopo](#escopo)
3. [Variáveis](#variaveis)
4. [Arrow Functions](#arrowfunc)

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

    ```



```js

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
