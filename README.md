# automacao-api
 Implementação da Automação de API com scripts de testes utilizando Postman, JS e Gitlab para integração na pipeline.

Coisas que precisam ser esclarecidas:
* Objetivo
Projeto em funcionamento no gitlab em ambiente Dev. Aqui é somente uma cópia para futuras avaliações e consultas. Não irá rodar ou estar implementado.


* Ferramentas utilizadas
- Postman
- Runner (nativo do postman) para testar a automação via interface gráfica
- Newman local para testar automação via linha de comando
- JavaScript para escrever scripts de teste
- Variáveis globais para utilização nos scripts
- Configuração .gitlab-ci.yml para criar estágio de automação na pipeline
- Gitlab para rodar automação na pipeline

* Dependências
- NPM para instalar Newman local


* Comandos
npm install -g newman (para instalar newman local)
git add . (para adicionar collection.json e globals.json)
git commit -m ``mensagem do deploy`` (para commitar e adicionar mensagem no commit)
git push (para subir alterações para o repositório)


* Passos para rodar automação
- Exportar collection.json
- Exportar variáveis globais.json
- Baixar e instalar git
- Criar repositório de automação de API no gitlab
- Clonar repositório via HTTP ou SSH local na máquina
- Colocar collection.json e globals.json no repositório local
- Adicionar comando git via linha de comando (ver lista de comandos acima)
- Ir no arquivo .gitlab-cy.yml e adicionar comandos:
```
stages:
    - test

postman_tests:
    stage: test
    image: 
        name: postman/newman:alpine
        entrypoint: [""]
    trigger:
       project: automated-tests/Prodesp.DO.Admin.Edition
       branch: automated-tests
    script:
        - newman --version
        - newman run postman_collection.json --global-var $workspace.postman_globals.json
 ```
 **Explicação**
 
 *O comando acima tem por base somente a parte (estágio) da automação na pipeline. Então acima está declarado um único stage (- test) e abaixo declarado a cadeia de comandos nomeada (postman_tests) apontando o stage test, o ambiente virtual docker do postman utilizada para rodar no servidor Ubuntu (gitlab). 
 Em trigger como o nome já diz é o gatilho para que a automação rode, em project está apontando o repositório e em branch apontando em qual branch está os testes automatizados.
 Mais abaixo está declado o scripts com newman --version para exibir a versão do newman (não obrigatório) e newman run apontando a collection.json e váriaveis globais.json do repositório*
