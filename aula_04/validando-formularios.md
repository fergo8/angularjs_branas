# Aula 04 - Validando Formulários

Na aula a seguir, focaremos em diretivas e propriedades voltadas para validação de formulários. Sendo assim, veremos as diretivas abaixo:

* _ng-required_
* _$valid_
* _$invalid_

## Diretiva _ng-required_

A diretiva `ng-required` é utilizada para indicar quais campos de um formulário serão obrigatórios. Tratando-se de um formulário, devemos ter os _inputs_ encapsulados em uma tag `<form>`, da mesma forma que estamos acostumados a fazer em páginas em HTML puro.

Portanto, para implementarmos essa diretiva na nossa Lista Telefônica das aulas passadas, o primeiro passo seria envolver nossos campos no formulário. Observe:

```html
<form name="contatoForm">
    <input class="form-control" type="text" ng-model="contato.nome" placeholder="Nome" ng-required="true" />
    <input class="form-control" type="text" ng-model="contato.telefone" placeholder="Telefone" ng-required="true" />

    <select class="form-control" ng-model="contato.operadora" ng-options="operadora.nome group by operadora.categoria for operadora in operadoras">
        <option value="">Selecione uma operadora...</option>
    </select>
</form>
```


Agora, note os seguintes pontos:

1- Nossa tag `<form>` precisa ter o atributo _name_, pois o AngularJS entende esse atributo como um novo objeto criado no _$scope_, podendo ser manipulado na Controller.

2- Em cada tag `<input>` adicionamos uma diretiva `ng-required` com o valor _true_ indicando a necessidade do campo estar preenchido.

## Propriedades _$valid_ e _$invalid_

Uma vez que temos o formulário denominado _contatoForm_, podemos utilizar esse novo objeto para efetuarmos a validação dos campos. Se você voltar na aula anterior, lembrará que criamos um botão _Adicionar_ que serve para incluirmos novos Pokémons à Lista Telefônica.

Sendo assim, naquela aula criamos uma validação com a diretiva `ng-disabled` afim de bloquear o botão caso não houvesse dados digitados nos _inputs_ do formulário. O problema é que a validação criada naquele momento não é muito declarativa, uma vez que criamos toda uma expressão com operadores lógicos. No entanto, existe uma maneira bem mais declarativa para indicar as condições do bloqueio desse botão _Adicionar_.

É aí que entram as propriedades _$valid_ e _$invalid_. Ambas possuem valores booleanos, sendo assim podem ser usadas no lugar daquela expressão _!contato.nome || !contato.telefone_. Observe abaixo como o `ng-disabled` ficou:

```html
<button class="btn btn-primary float-left" ng-click="adicionarContato(contato)" ng-disabled="contatoForm.$invalid">Adicionar</button>
```

__Obs:__ também poderíamos usar a expressão `ng-disabled="!contatoForm.$valid"`, que daria no mesmo.