# Aula 03 - Usando Diretivas (Parte 2)

Nessa segunda parte da aula sobre diretivas, serão abordados os itens da lista abaixo:

* _ng-disabled_
* _ng-options_
* _ng-class_
* _ng-style_
* _ng-hide_
* _ng-show_
* _ng-if_
* _ng-include_

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

Aqui nós vamos ver três maneiras de implementar essa diretiva, todas considerando o mesmo exemplo da aula anterior.

### Método 1

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

* __Ponto 2__ - na diretiva `ng-options` a sintaxe usada é bastante semelhante à utilizada no `ng-repeat` (abordado na aula anterior). Sendo assim, _operadora.nome_ indica qual campo dos objetos _operadora_ a expressão deve considerar para popular as opções do select.

Outro ponto interessante é a tag `<option>` que criamos dentro do select. Ela serve como opção default para a lista de operadoras.

### Método 2 (apelido)

Uma outra maneira de implementar essa diretiva é utilizando um apelido para indicar o campo nome de operadora. Por exemplo, se quisermos mostrar o _código_, mas apresentarmos para o back-end como _nome_, basta usarmos da seguinte maneira:

```html
<select class="form-control" ng-model="contato.operadora" ng-options="operadora.codigo as operadora.nome for operadora in operadoras">
    <option value="">Selecione...</option>
</select>
```

Sendo assim, _operadora.codigo_ será o valor passado e _operadora.nome_ será o apelido. Em todo caso, este não é o método mais comum no uso dessa diretiva.

### Método 3 (agrupando)

Um outro método seria agrupar os itens da nossa lista de _operadoras_ através de um atributo em comum dos objetos. Para exemplificar esse método, vamos modificar a estrutura do array, adicionando o atributo _operadora.categoria_, assim:

```javascript
$scope.operadoras = [
    { nome: "Vivo", codigo: 15, categoria: "Fixo" },
    { nome: "Tim", codigo: 41, categoria: "Celular" },
    { nome: "Claro", codigo: 21, categoria: "Celular" }
]
```

A partir dessa nova estrutura, vamos acrescentar na diretiva `ng-options` um novo elemento: o _group by_. Observe:

```html
<select class="form-control" ng-model="contato.operadora" ng-options="operadora.nome group by operadora.categoria for operadora in operadoras">
    <option value="">Selecione...</option>
</select>
```

Agora note que o campo dropdown será mostrado com uma separação entre as operadoras, organizando-as pelas categorias _Fixo_ e _Celular_ conforme o array.

## Diretiva _ng-class_

A seguir, vamos passar para a diretiva `ng-class`, cuja principal função é adicionar classes às tags HTML dinamicamente. Ou seja, podemos usá-la para incluir ou excluir classes das tags conforme regras predefinidas, com o objetivo de modificar o comportamento ou aparência dos elementos HTML da página.

Sendo assim, veremos esta diretiva na prática a partir do exemplo de Lista Telefônica. Agora a ideia é criar um checkbox ao lado de cada linha para podermos selecionar um ou mais contatos da nossa lista. Queremos __selecionar o contato de modo que a linha seja pintada__ de alguma cor, dando assim um destaque ao contato selecionado.

Para tanto, o primeiro passo é criarmos na tag `<style>` uma classe CSS definindo uma cor:

```css
.selecionado {
    background-color: pink !important;
}
```

__Obs:__ Eu escolhi esse rosinha simpático por gostar muito dele, mas se você for _homem hétero-cis_ e sentir que sua masculinidade frágil está sendo afetada sinta-se à vontade para escolher outra.

Em seguida, criaremos um input do tipo checkbox dentro da tabela (em uma nova coluna para manter a organização). Note que o input deve possuir uma diretiva `ng-model` indicando o novo atributo _contato.selecionado_. Este atributo será responsável por definir se o input foi clicado ou não, sendo nosso parâmetro para pintar ou não a linha. Veja como ficou a tabela:

```html
<table class="table table-striped">
    <tr>
        <th></th>
        <th>Nome</th>
        <th>Telefone</th>
        <th>Operadora</th>
    </tr>
    <tr ng-class="{selecionado: contato.selecionado}" ng-repeat="contato in contatos">
        <td><input type="checkbox" ng-model="contato.selecionado" /></td>
        <td>{{contato.nome}}</td>
        <td>{{contato.telefone}}</td>
        <td>{{contato.operadora.nome}}</td>
    </tr>
</table>
```

Considerando a tabela acima, utilizamos a diretiva `ng-class` para indicar quando a classe CSS _selecionado_ deve ser aplicada, ou seja, no momento em que clicarmos o checkbox de uma linha o atributo _contato.selecionado_ passará para o valor _true_, acionando assim nossa classe CSS.

Este mecanismo para selecionar e desselecionar os itens alterando seu CSS pode ser aplicado para escolhermos contatos que desejamos remover da lista. Contudo, essa implementação de um botão de _Excluir_ contatos vai repetir conceitos que já vimos no decorrer dessa aula, então vou detalhar isso em um texto a parte ([clique aqui para acessá-lo](https://github.com/fergo8/angularjs_branas/blob/main/aula_03/criando_botao_excluir.md)).

## Diretiva _ng-style_

A diretiva `ng-style` permite que utilizemos valores definidos na Controller como estilo CSS. Sendo assim, podemos criar um marcador colorido para indicar cada Pokémon da Lista Telefônica. Primeiro precisamos incluir um novo atributo _cor_ no nosso array _contatos_. Ele vai ficar dessa forma:

```javascript
$scope.contatos = [
    { nome: "Bulbasauro", telefone: "11111111", cor: "green", operadora: { nome: "Vivo", codigo: 15, categoria: "Fixo" } },
    { nome: "Charmander", telefone: "22222222", cor: "red", operadora: { nome: "Tim", codigo: 41, categoria: "Celular" } },
    { nome: "Squirtle", telefone: "33333333", cor: "blue", operadora: { nome: "Claro", codigo: 21, categoria: "Celular" } }
]
```

Em seguida, criamos outra coluna na tabela, onde criaremos uma `<div>` quadrada (width e height to mesmo tamanho). A diretiva `ng-style` será usada para definir dinamicamente o _background-color_ dessa div. Assim:

```html
<td><div style="width: 20px; height: 20px;" ng-style="{'background-color': contato.cor}"></div></td>
```

Assim definimos marcadores dinâmicos de cor para identificarmos os Pokémons da lista.

## Diretivas _ng-show_ e _ng-hide_

As diretivas `ng-show` e `ng-hide` têm o propósito inverso uma da outra. Ou seja, enquanto _show_ vai mostrar algo a partir de uma condição, _hide_ vai esconder esse algo, também mediante uma condição.

Por exemplo, vamos supor que o botão Excluir devesse aparecer apenas quando algum Pokémon fosse selecionado. Neste caso podemos usar o `ng-hide` no lugar daquele `ng-disabled`, dessa forma:

```html
<button class="btn btn-danger float-right" ng-click="removerContatos(contatos)" ng-hide="!isContatoSelecionado(contatos)">Excluir</button>
```

Sendo assim, nossa função _isContatoSelecionado_ seria a condição para que o botão Excluir aparecesse ou desaparecesse da tela. O mesmo poderíamos fazer com a tabela inteira. Vamos supor que ela só devesse aparecer caso houvesse pelo menos um Pokémon cadastrado na Lista Telefônica. Nesse caso, nós podemos usar a diretiva `ng-show` para esconder a tabela inteira da seguinte forma:

```html
<table class="table table-striped" ng-show="contatos.length > 0">
    <tr>
        <th></th>
        <th>Nome</th>
        <th>Telefone</th>
        <th>Operadora</th>
        <th></th>
    </tr>
    <tr ng-class="{'selecionado': contato.selecionado}" ng-repeat="contato in contatos">
        <td><input type="checkbox" ng-model="contato.selecionado" /></td>
        <td>{{contato.nome}}</td>
        <td>{{contato.telefone}}</td>
        <td>{{contato.operadora.nome}}</td>
        <td><div style="width: 20px; height: 20px;" ng-style="{'background-color': contato.cor}"></div></td>
    </tr>
</table>
```

Deste modo, a tabela apenas será mostrada se a condição _contatos.length > 0_ for verdadeira.