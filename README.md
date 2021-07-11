# Estudos Teóricos - Javascript :books:
O objetivo desse repositório é organizar algumas teorias importantes do javascript, para melhorar a qualidade dos meus estudos e fixar melhor o conteúdo. Fique a vontade para utilizar também!

## Hoisting :fishing_pole_and_fish:
### O que é o hoisting?
É o conceito de que as declarações de variável e função são colocadas na memória durante a fase de compilação, mas permanecem exatamente onde você as digitou. Isso, permite que você use uma função ou variável antes mesmo de declará-la.

fonte: https://developer.mozilla.org/pt-BR/docs/Glossary/Hoisting

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

## Escopo :mailbox:
### O que é um escopo?
Escopo é a acessibilidade de objetos, variáveis e funções em diferentes partes do código.
Em outras palavras, o que determina quais são os dados que podem ser acessados em uma determinada parte do código é o escopo.
Imagine que o escopo é uma caixa e tudo que for criado nessa caixa pode ser acessado por qualquer objeto dentro da mesma. Um escopo é criado sempre que definimos uma função:

```js

    function hello(name) {
        // Isto aqui é um escopo
    }

```


fonte: https://imasters.com.br/desenvolvimento/escopos-em-javascript

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