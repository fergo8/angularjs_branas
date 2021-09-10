# Aula 04 - Validando Formulários

Na aula a seguir, focaremos em diretivas e abordagens voltadas para validação de formulários. Sendo assim, veremos as diretivas abaixo:

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

