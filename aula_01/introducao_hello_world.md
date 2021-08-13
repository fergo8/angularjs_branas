# Aula 01 - Introdução e Hello World

O diagrama abaixo indica o esquema utilizado pelo professor para explicar o funcionamento das camadas que compõem o AngularJS.

![Controller Scope View](https://github.com/fergo8/angularjs_branas/blob/main/aula_01/controller_scope_view.png)

As três camadas representadas são:

* __View:__ São os arquivos HTML da página, onde escrevemos códigos utilizando as diretivas do AngularJS;
* __Controller:__ Camada onde são processados os fluxos da página, realizando cálculos ou qualquer outro tipo de ação;
* __Scope:__ É um intermediário entre View e Controller, de modo que estes não precisem estar em contato direto.

## Imprimindo Hello World na tela

A partir de uma estrutura básica de HTML é possível desenvolver utilizando AngularJS da mesma forma como utilizamos o JavaScript puro. Primeiro é necessário obter a biblioteca do AngularJS, e para isso temos duas formas:

* __Fazendo download:__ entrando no site do [AngularJS](https://angularjs.org) será possível baixar a biblioteca para usá-la localmente, sem necessidade de estar conectado à internet;

* __Referenciando direto no projeto:__ o site do AngularJS também disponibiliza um link para utilização sem a necessidade de download. Para isso, basta usar o link em uma tag `<script>` para fazer a referência, como abaixo:

```html
<script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.8.2/angular.min.js"></script>
```

Em seguida, é necessário adicionar em uma tag (geralmente na tag `<html>`) a diretiva `ng-app`. Diretivas são o assunto de aulas posteriores, por isso não serão aprofundadas nesse momento. Se dermos o nome "helloWorld" para esta diretiva, a tag ficará como abaixo:

```html
<html lang="pt-br" ng-app="helloWorld">
```

O próximo passo é criarmos um módulo (que vamos nomear de "helloWorld" também). Para tanto, em uma nova tag `<script>`, escrevemos o código abaixo:

```javascript
// Criamos o módulo "helloWorld"
angular.module("helloWorld", [])

// Dentro do módulo "helloWorld" criamos a controller "helloWorldController"
angular.module("helloWorld").controller("helloWorldController", $scope => {
    // Utilizamos o scope para atribuirmos uma mensagem
    $scope.message = "Hello World!"
})
```

Note que é necessário criarmos o módulo para, dentro dele, declararmos uma controller. Essa controller terá uma função anônima que terá __$scope__ como assinatura, e através desse __$scope__ podemos gerar recursos (variáveis e métodos) que podemos usar dentro da tag `<body>` do HTML.

No exemplo acima, já temos disponível uma variável __message__ atribuída com a mensagem "Hello World!". Sendo assim, o próximo e último passo seria utilizarmos essa variável no body, como abaixo:

```html
<!-- Criamos uma div e usamos a diretiva ng-controller -->
<div ng-controller="helloWorldController">
    <!-- Em seguida usamos a variável "message" -->
    {{message}}
</div>
```

No código acima foi utilizada a diretiva __ng-controller__ para definir que a variável __message__ (ou qualquer outro recurso que criarmos dentro da "helloWorldController") possa ser usada apenas dentro da `<div>`. Dessa forma podemos utilizar controllers diferentes em partes diferentes do projeto, o que torna tudo mais dinâmico.

[Clique aqui para ver o código completo](https://github.com/fergo8/angularjs_branas/blob/main/aula_01/index.html)

[Ir para aula 02](https://github.com/fergo8/angularjs_branas/blob/main/aula_02/usando_diretivas_pt1.md)
