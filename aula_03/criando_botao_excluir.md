# Criando botao Excluir

O texto a seguir complementa a [aula 03](https://github.com/fergo8/angularjs_branas/blob/main/aula_03/usando_diretivas_pt2.md). Sendo assim, vamos ver como criar o botão de Excluir contatos da nossa Lista Telefônica. São três passos:

### Passo 1

Primeiro criamos no _$scope_ a função _removerContatos_. Ela irá receber por parâmetro o array de _contatos_ para ser processado. Como o próprio nome da função já diz, o objetivo dela é mexer na lista de contatos, removendo todos os contatos selecionados (ou seja, todo que estiverem com o atributo _contato.selecionado_ igual a _true_).

Para isso, podemos utilizar o método JavaScript _filter_, como abaixo:

```javascript
$scope.removerContatos = contatos => {
    $scope.contatos = contatos.filter(contato => { if (!contato.selecionado) return contato })
}
```

Note que o método _filter_ recebe por parâmetro uma função que retorna apenas os contatos que tiverem o _contato.selecionado_ igual a _false_, em seguida reatribuindo nossa lista _$scope.contatos_ para receber os resultados desse filtro. Com isso, atualizaremos o array removendo/filtrando os contatos selecionados.

### Passo 2

Agora fazemos o botão no HTML utilizando a diretiva `ng-click` para acionar nossa nova função _removerContatos_. Observe:

```html
<button class="btn btn-danger float-right" ng-click="removerContatos(contatos)" ng-disabled="isContatoSelecionado(contatos)">Excluir</button>
```

__Obs:__ usei umas classes do Bootstrap para deixar o botão mais bonitinho.

### Passo 3

Por fim, criaremos uma função para desabilitar o botão Excluir quando não houver contato selecionado. Note que acrescentei no botão um `ng-disabled` para chamar essa nova função. Portanto, vamos a ela:

```javascript
$scope.isContatoSelecionado = contatos => {
    return contatos.some(contato => { return contato.selecionado })
}
```

A função _isContatoSelecionado_ também recebe por parâmetro nosso array _contatos_ e retorna _true_ ou _false_ dependendo do resultado de seu processamento. Para tanto, utilizamos o método _some_, cujo objetivo é retornar _true_ se pelo menos um item da lista estiver com o atributo _contato.selecionado_ igual _true_.

Feito isso, agora é só testar o botão.

[Volte para a Aula 03 clicando aqui](https://github.com/fergo8/angularjs_branas/blob/main/aula_03/usando_diretivas_pt2.md)