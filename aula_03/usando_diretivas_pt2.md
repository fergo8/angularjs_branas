# Aula 03 - Usando Diretivas (Parte 2)

Nessa segunda parte da aula sobre diretivas, serão abordados os itens da lista abaixo:

* _ng-disabled_

## Diretiva _ng-disabled_

A diretiva `ng-disabled` serve para desabilitarmos algum elemento HTML dinamicamente. Sendo assim, podemos utilizá-la em inputs ou botões.

Voltando ao projeto da Lista Telefônica criada na aula anterior, vamos usar a diretiva _ng-disabled_ no botão Adicionar. O objetivo é bloquearmos o botão quando os campos de _nome_ e _telefone_ estiverem ambos vazios. Para tanto, acrescentamos a lógica a seguir:

```html
<button class="btn btn-primary btn-block" ng-click="adicionarContato(contato)" ng-disabled="!contato.nome || !contato.telefone">Adicionar</button>
```

Note que a diretiva `ng-disabled` recebe como valor uma expressão booleana, ou seja, ele deve receber algo que resulte em _true_ ou _false_. Podemos considerar essa expressão como a mesma que nós costumamos usar em comandos `if` em qualquer [linguagem de programação imperativa](https://pt.wikipedia.org/wiki/Programação_imperativa). Deste modo, a expressão que utilizamos no nosso `<button>` significa que enquanto os campos _contato.nome_ e _contato.telefone_ estiverem vazios o botão Adicionar se manterá bloqueado para ser clicado.

__Obs:__ Em aulas futuras serão mostradas formas melhores de se fazer esse tipo de validação. No momento, o objetivo é mostrar o uso prático desta diretiva.

## Diretiva _ng-options_

