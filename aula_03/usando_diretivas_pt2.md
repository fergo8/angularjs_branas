# Aula 03 - Usando Diretivas (Parte 2)

Nessa segunda parte da aula sobre diretivas, serão abordados os itens da lista abaixo:

* _ng-disabled_
* _ng-options_

## Diretiva _ng-disabled_

A diretiva `ng-disabled` serve para desabilitarmos algum elemento HTML dinamicamente. Sendo assim, podemos utilizá-la em inputs ou botões.

Voltando ao projeto da Lista Telefônica criada na aula anterior, vamos usar a diretiva _ng-disabled_ no botão Adicionar. O objetivo é bloquearmos o botão quando os campos de _nome_ e _telefone_ estiverem ambos vazios. Para tanto, acrescentamos a lógica a seguir:

```html
<button class="btn btn-primary btn-block" ng-click="adicionarContato(contato)" ng-disabled="!contato.nome || !contato.telefone">Adicionar</button>
```

Note que a diretiva `ng-disabled` recebe como valor uma expressão booleana, ou seja, ele deve receber algo que resulte em _true_ ou _false_. Podemos considerar essa expressão como a mesma que nós costumamos usar em comandos `if` em qualquer [linguagem de programação imperativa](https://pt.wikipedia.org/wiki/Programação_imperativa). Deste modo, a expressão que utilizamos no nosso `<button>` significa que enquanto os campos _contato.nome_ e _contato.telefone_ estiverem vazios o botão Adicionar se manterá bloqueado para ser clicado.

__Obs:__ Em aulas futuras serão mostradas formas melhores de se fazer esse tipo de validação. No momento, o objetivo é mostrar o uso prático desta diretiva.

## Diretiva _ng-options_

A próxima diretiva a ser vista é a `ng-options`, utilizada para criar as opções em uma tag `<select>`. Com ela, nosso intuito será pegar uma lista de objetos do back-end via JavaScript (pela Controller) e imprimi-la na tela, gerando assim um campo de opções selecionáveis.

No caso do nosso exemplo da Lista Telefônica, podemos usar o `ng-options` para gerar uma lista de operadoras. Sendo assim, o primeiro passo é estabelecermos na Controller um array de operadoras, da maneira abaixo:

```javascript
$scope.operadoras = [
    { nome: "Vivo", codigo: 15 },
    { nome: "Tim", codigo: 41 },
    { nome: "Claro", codigo: 21 },
]
```

Com isso, teremos disponível no nosso _$scope_ o array operadoras, que utilizaremos para compôr os itens da tag `<select>`. A seguir, criaremos a seguinte tag logo acima do botão de Adicionar:

```html
<select class="form-control" ng-model="contato.operadora" ng-options="operadora.nome for operadora in operadoras">
    <option value="">Selecione...</option>
</select>
```

Aqui devemos notar dois pontos importantes:

* __Ponto 1__ - veja que existe a necessidade de utilizarmos um `ng-model` para delimitar um objeto _contato.operadora_. Isso servirá para o AngularJS identificar e construir corretamente a estrutura do objeto _operadora_ a ser selecionado.

* __Ponto 2__ - na diretiva `ng-options` a sintaxe usada é bastante semelhante à utilizada no `ng-repeat` (abordado na aula ainterior).