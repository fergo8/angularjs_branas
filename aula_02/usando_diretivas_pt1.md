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