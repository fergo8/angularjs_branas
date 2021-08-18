# Aula 02 - Usando Diretivas (Parte 1)

De acordo com o professor, "Diretivas são __extensões__ da linguagem HTML que permitem a implementação de novos comportamentos, de forma declarativa". Sendo assim, cada diretiva possui funções específicas que vão desde atribuir valores, iterar em listas, definir views parciais, entre várias outras possibilidades.

Aqui vamos iniciar estudando as seis diretivas abaixo:

* _ng-app_
* _ng-controller_
* _ng-bind_
* _ng-repeat_
* _ng-model_
* _ng-click_

## Diretiva _ng-app_

A primeira diretiva a ser vista é a `ng-app` que já foi abordada na aula 01. Como vimos, ela é responsável por delimitar a região do HTML que vai reconhecer os códigos AngularJS. Essa diretiva pode ser incluída em qualquer tag do seu HTML, mas é mais comum (e mais lógico) ela ser adicionada na tag `<html>`, como vimos na aula 01, dessa forma garantimos que o AngularJS seja utilizado em qualquer lugar.

Exemplo de uso em um app de lista telefônica:

```html
<html ng-app="listaTelefonica">
    <head>
        <!-- configurações da página -->
    </head>
    <body>
        <!-- conteúdo da página -->
    </body>
</html>
```

## Diretiva _ng-controller_

Assim como o _ng-app_ indica os limites do AngularJS, a diretiva `ng-controller` tem como função delimitar a região das controllers no HTML. Após essa delimitação, podemos utilizar qualquer recurso AngulasJS que esteja atrelado à controller em questão. Para fins de exemplo, consideremos a controller chamada __listaTelefonicaController__ abaixo:

```javascript
angular.module("listaTelefonica", [])
angular.module("listaTelefonica").controller("listaTelefonicaController", $scope => {
    $scope.app = "Lista Telefônica"

    $scope.contatos = [
        { nome: "Pikachu", telefone: "11111111" },
        { nome: "Bulbasauro", telefone: "22222222" },
        { nome: "Charmander", telefone: "33333333" },
        { nome: "Squirtle", telefone: "44444444" }
    ]

    $scope.adicionarContato = contato => {
        $scope.contatos.push(angular.copy(contato))
        delete $scope.contato
    }
})
```

Note que ela possui três recursos definidos no `$scope`, sendo eles:

* _$scope.app_ - se comporta como uma variável com valor "Lista Telefônica" atribuído (chamei de app, mas poderia ser qualquer outra palavra);
* _$scope.contatos_ - um array de objetos onde definimos as chaves "nome" e "telefone" (sim, estou listando telefones de Pokémons hehe);
* _$scope.adicionarContato_ uma função para adicionar novos itens ao nosso array.

Estando nossa controller devidamente escrita em uma tag `<script>` ou em um arquivo JavaScript referenciado, o próximo passo é utilizar a diretiva `ng-controller` propriamente dita. Estou usando na tag `<body>`:

```html
<html ng-app="listaTelefonica">
    <head>
        <!-- configurações da página -->
    </head>
    <body ng-controller="listaTelefonicaController">
        <!-- conteúdo da página -->
    </body>
</html>
```

## Diretiva _ng-bind_

A diretiva `ng-bind` pode ser usada para imprimir recursos em tela, como por exemplo o nosso _$scope.app_. Contudo, este método pode não deixar as coisas tão claras devido a sua sintaxe.

Uma outra maneira de imprimir em tela algum recurso que esteja disponível na controller seria usando uma coisa chamada __expressão de interpolação__. Para tanto, basta utilizarmos uma dupla chave `{{}}` e acrescentar dentro dela o recurso desejado. Para exemplificar essas duas formas, vamos utilizar o nosso _$scope.app_ em uma tag `<h4>`:

```html
<!-- usando a diretiva ng-bind -->
<h4 ng-bind="app"></h4>
<!-- usando a expressão de interpolação -->
<h4>{{app}}</h4>
```

Note que em ambas as formas não é necessário utilizar o _$scope_ explicitamente, pois o AngularJS já entende apenas esse `app`.

## Diretiva _ng-repeat_

Esta diretiva funciona como um comando `for` de linguagens de programação tipo JavaScript, C#, Python etc. Sendo assim, utilizamos `ng-repeat` para iterar em uma lista, percorrendo cada elemento que a compõe. Lembra daquele array de contatos onde listamos telefones de Pokémons? Para iterar nele imprimindo cada contato em uma tag HTML de tabela, fazemos o seguinte:

```html
<table class="table table-striped">
    <tr>
        <th>Nome</th>
        <th>Telefone</th>
    </tr>
    <tr ng-repeat="contato in contatos">
        <td>{{contato.nome}}</td>
        <td>{{contato.telefone}}</td>
    </tr>
</table>
```

Dessa forma estamos percorrendo a lista __contatos__, sendo que cada item dessa lista estamos apelidando de __contato__. Com isso, criamos várias tags `<tr>` (uma para cada Pokémon da lista) imprimindo dentro dela um par de tags `<td>`, uma para o nome outro para o telefone.

Obs: estou usando classes do Bootstrap v4 para tornar essa tabela um pouco mais bonita.

## Diretiva _ng-model_

A penúltima diretiva abordada nesse texto, `ng-model`, tem como função o contrário da diretiva `ng-bind`. Ou seja, enquanto __bind__ imprime na View coisas que estão definidas na Controller, essa __model__ vai criar coisas na View (aqui estou falando de inputs) para transportá-las através do _$scope_ para a Controller.

Pensando na lista telefônica, temos até o momento um título disponível em `$scope.app` e temos nossa tabela constituída pelos itens do nosso array `$scope.contatos`. O próximo passo seria criarmos uma forma de adicionar novos Pokémons à lista e, para tanto, serão necessárias tags de input:

```html
<input class="form-control" type="text" ng-model="contato.nome" placeholder="Nome" />
<input class="form-control" type="text" ng-model="contato.telefone" placeholder="Telefone" />
```

Nos inputs acima temos as diretivas apontando _contato.nome_ e _contato.telefone_, ambos os eventos ficam aguardando o usuário escrever algo nos campos. Tudo o que for escrito neles pode ser acessado pelo `$scope.contato` de forma online, ou seja, na medida em que você escreve nos inputs o AngularJS armazena caracter a caracter, isso acontece devido ao recurso __Two Way Data Binding__.

## Diretiva _ng-click_

Por fim, agora que temos os campos de input para escrevermos os dados de novos Pokémons só falta uma última coisa: um botão para Adicionar na lista. Para tanto, usaremos a diretiva `ng-click`, que funciona da mesma forma que os eventos _onclick_ do JavaScript. Então vamos adicionar uma tag `<buttom>` com esta diretiva:

```html
<button class="btn btn-primary btn-block" ng-click="adicionarContato(contato)">Adicionar</button>
```

Neste botão estamos usando a diretiva para acionar aquela função que havíamos declarado lá no início em nossa Controller, aquela que chamamos _adicionarContato_. Note que estamos passando como parâmetro da função o nosso elemento _contato_ do _$scope_ (novamente não precisamos indicar algo como __$scope.contato__, pois o AngularJS já entende o _contato_ como item do _$scope_).

Só para relembrar, a nossa função é esta:

```javascript
$scope.adicionarContato = contato => {
    // Adiciona no array "contatos" uma cópia do novo item "contato" passado por parâmetro
    $scope.contatos.push(angular.copy(contato))
    // Apaga da memória os valores dentro de "contato"
    delete $scope.contato
}
```

__Dica:__ é importante que o novo item _contato_ esteja envolvido em um `angular.copy(contato)`, pois assim não temos problemas de referência deste objeto.

[Clique aqui para ver o código da aula 02 completo](https://github.com/fergo8/angularjs_branas/blob/main/aula_02/index.html)

[Ir para aula 03](https://github.com/fergo8/angularjs_branas/blob/main/aula_03/usando_diretivas_pt2.md)